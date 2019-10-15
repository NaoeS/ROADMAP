# TIPS

- ルーティングのネスト
  * 1 階層に留めておくのが無難
    + id で一意に特定できるのであれば、show, edit, destroy などのアクションは外に置いておく
    + `shallow` オプションを使用するのもいい手

- ActiveRecord の inverse_of について
  * 1 対多の関連において、1 側 と多側の参照を同一のものにするためのオプション
  * 設定しないと別々の参照を持つ形となるため、片方を変更してももう片方には伝播しなくなり、不整合が生じる場合がある
    + https://shoken.hatenablog.com/entry/2015/07/14/095211

- ログ出力について
  * パスワード、メールアドレスをフィルタリングできる機能が標準で備わってたりする
    + https://railsguides.jp/security.html#%E3%83%AD%E3%82%B0%E5%87%BA%E5%8A%9B

- 多言語化について
  * [ActiveModel の human_attribute_name メソッド](https://railsguides.jp/active_model_basics.html#translation%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB)
  * [便利メソッド](https://qiita.com/Kta-M/items/bd4ba36a58ad602a9d8b)
  * [HTML タグ出力について](https://qiita.com/tnj/items/c9e893124c1b000b5355)

- View のエスケープ方法について
  * https://qiita.com/iwamot/items/74c2bd9ebd3ac6458837

- モジュール名を大文字対応させる
  * ActiveSupport::Inflector.inflections

- turbolink について
  * a タグだけに適応され、画面をキャッシュするのみ
  * Ajax は ujs がキモ。turbolinks が行うものではない