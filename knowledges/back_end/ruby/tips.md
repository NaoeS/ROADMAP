# TIPS

- Ruby の URI モジュールの定数に email の正規表現が存在する
  * https://www.rubydoc.info/stdlib/uri/URI/MailTo

- Ruby で正規表現オブジェクトを作成する際は %r を使用すると便利
  * https://blog.toshimaru.net/ruby-percent-notation/#r

- Ruby ではセッターを private にしても self を付けないとならない
  * self を付けないとただ単純にローカル変数が参照されるだけとなる
  * 考えてみると当たり前だが、private なメソッドはレシーバを付けない、と思い込んでいると足払いされるので注意

- Ruby の Struct で定数定義する時の注意
  * Struct で素直に定数を定義すると外側のクラス直下に定義されてしまう
  * 正しい名前空間に定義するためには、Struct を定義した後に定数を定義する
  ```
  # Hoge::CONST 扱いになる
  module Hoge
    HogeStruct = Struct.new(:raw) do
      CONST = [1, 2, 3].freeze
    end
  end

  # Hoge::HogeStruct::CONST に定義される
  module Hoge
    HogeStruct = Struct.new(:raw)

    HogeStruct::CONST = [1, 2, 3].freeze
  end
  ```

- Net::HTTP で POST したら 404 エラーが返却された
  * net/https の引数形式が間違っている可能性がある
  ```
  # アロー表記で 'Content-Type' => 'application/json' と書くのが正しい

  Net::HTTP.post(
    URI.parse('https:://hoge.com'),
    body.to_json,
    'Content-Type': 'application/json' # 誤
  )
  ```

- Gem 比較サイト
  * https://www.ruby-toolbox.com/
  * https://github.com/Sdogruyol/awesome-ruby