# TIPS

- Rspec の日本語問題
  * 登録したオブジェクトの属性を検証する時などは `it '登録された XXX の属性が正しいこと' do` のように書くかもしれない
  * しかし、自メソッドのテストなのに受け身はどうなの？とか、`正しいこと` は自明ではないか？
  * `it 'XXX を返却すること' do` が完結で良い
    + メソッドの最終処理に着目した
    + 冗長性を無くした
    + `正しいこと` は基本的には使わない。パターン分けがある場合に考える

- 時間操作系のテストについて
  * Rails 4.1 以降 `travel_to` が使えるようになった
    + https://qiita.com/kuboon/items/1fab1339c7b7b2424551
  * `ActiveSupport::Testing::TimeHelpers` にあるメソッドなのでテストで使うなら `timecop` より適切そう
  * ちなみに `travel_to` は usec を 0 に丸めるので、ミリ秒を指定しても意味がない

- Rpsec で API テストをする際、POST リクエストの Boolean 型が文字列になる件
  * リクエストが `application/x-www-form-urlencoded` でパースされると、`Boolean` は文字列に、配列は中身を文字列で展開されてしまう
  * 環境変数の `CONTENT_TYPE` を `application/json` に変えるか、リクエストする際に `as: :json` オプションを付けることにより解決する
    + https://qiita.com/shozawa/items/998d97e8b6778fc8f2d9
    + https://sinshutu-kibotu.hatenablog.jp/entry/2018/07/06/202132

- Rspec で JSON の一部プロパティだけ存在確認したい時
  * `be_json_including` マッチャを使う
