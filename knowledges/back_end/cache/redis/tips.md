# TIPS

- Redis へのアトミックな登録
  * setnx() + setex() で Redis へデータを登録できるが、一度に行える set() が使用できる

- セッションの生成に上限を持たすため、Redis を使用して押し出しが実現できないか模索した。
  * セッションの実体に加えてセッション ID のリストが必要となる
  * ソート済みセット型を使用した
    + ZADD コマンドでデータを追加するが、スコアも一緒に追加すると勝手にソートを行ってくれる
    + ZRANGE や ZREVRANGE で昇順や降順で取得できたりする。便利

- Redis でトランザクションを実現する方法として以下のコマンドがある
  * MULTI
    + 複数のコマンドをひと纏めにして実行するコマンド。実行が直列に行われることが保証されるので、他プロセスの割り込みによる不整合を防ぐことができる。

```
# redis-rb による例
require "redis"

redis = Redis.new

redis.multi do |multi|
  multi.rpush('list', 'hoge')
  # rpush 後、他プロセスで redis.rpush('list', 'piyo') が実行されたとする
  multi.rpush('list', 'fuga')
end

# ['hoge', 'fuga', 'piyo'] が出力される
p redis.lrange('list', 0, -1)
```

  * WATCH
    + キーに対して楽観ロックをかけることができる。MULTI とセットで使用する。キーの値に依存してコマンドを実行する場合、取得時と実行時で値が変わっていると不整合となるので、これを防ぐために使用する。

```
redis.set('key', 'hoge')

result = redis.watch('key') do
  hoge = redis.get('key')
  # get 後、他プロセスでキーの値が変更されたとする
  redis.multi do |multi|
    multi.set('key', "#{hoge}_fuga")
  end
end

# multi の実行に失敗し、nil が返却される
fail unless result
```

  * Redis のコマンドのみで処理を完結できる場合は MULTI でよい。Rails.cache などを用いて Ruby で操作した後に保存する場合は WATCH を使ってロックをかける。使い分けが重要。

- セッションの押し出し処理について
  * ソート済みセット型が使える
  * ソート済みセット型は ZADD コマンドでデータを追加するが、スコアも一緒に追加すると勝手にソートを行ってくれる
    + `ZRANGE` や `ZREVRANGE` で昇順や降順で取得できたりする
  * ただこの型自体に有効期限を設定することはできないため、スコアをタイムスタンプなどに設定して取得する際にセッション切れかどうか判断する処理が必要

- Redis の String 型 と Hash 型について
  * String は登録に強い。Hash はメモリ削減となる
    + http://laporz.blogspot.com/2015/01/redis-hash-vs-json-string.html

- Redis にはロールバックの概念がない
  * 失敗する状況でコマンドを実行しても内部的に例外などは発生しない
  * 実行結果を受け取ることはできる

- Rails から Redis に接続する際の接続情報は redis:// を付ける
  * 例：redis://hostname:6379/1
  * 末尾の数字は DB 振り分けに使用できる。テスト用など
