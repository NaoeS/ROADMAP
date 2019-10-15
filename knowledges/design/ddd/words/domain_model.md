# ドメインモデル

## バリデーション
- 集約作成後に行われる遅延バリデーションはドメインイベントの発行を止めることができない
  * 作成してはならない場合にイベントが発行されてしまう
  * 値オブジェクトや集約の initialize でバリデーションを行うこととした

```
#
# メールアドレス(値オブジェクト)
#
# @!attribute [r] raw
#   @return [String] 値
#
UserEmail = Struct.new(:raw) do
  #
  # 初期化
  #
  def initialize(raw)
    change_raw(raw)
  end

  private

  def change_raw(raw)
    fail Common::Errors::InvalidArgument if raw.nil?
    fail Common::Errors::InvalidArgument if raw.empty?
    fail Common::Errors::InvalidArgument if raw !~ URI::MailTo::EMAIL_REGEXP

    self.raw = raw
  end
end
```

## ドメインイベント
- イベントの重複問題（Ruby）
  * ドメインモデルの作成時、`initialize` でセッター用の `change_xxx` メソッドを実行してメンバの値を設定していた
  * しかし、`change_xxx` でドメインイベントを発行するとドメインモデル作成時にも発行されてしまうことに
  * それはまずいため、メンバに値をセットする場合は `attr_writer` を使用することに
    + `nil` 不可などのアサーションがある場合は `hoge=` でオーバーライドして対応
  * これだけでは外から自由に値を変更されるため、`attr_writer` は `private` に隠し、`new or change_xxx` 経由でしかメンバにアクセスできないようにした
