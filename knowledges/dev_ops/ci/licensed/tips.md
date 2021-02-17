# TIPS

- licensed は GitHub が公開しているライセンス調査ツール（Ruby Gem）
  * https://github.com/github/licensed
  * 元々は GitHub の社内ツールだったものだが、OSS 化された

- プロジェクト配下のライブラリを走査し、ライセンス情報を抜き出してくれる
  * Bower, NPM, Yarn といった Node 関連のものから、Go, pip と幅広くカバーしている
  * `bundle exec licensed cache` を実行すると、デフォルトで `.licenses` ディレクトリに結果が出力される
    + NPM では node_modules を参照しているらしく、`npm install` が必須
    + fsevents などの MacOS 専用のライブラリがある場合、Linux 環境ではインストールがスキップされる
    + そのため、licensed でライセンスが存在しないエラーが発生する場合がある。`npm install -f` などで強制インストールすると良い

- YAML 形式の設定ファイルに許可するライセンスの種類を設定することで、違反ライブラリがないか調べることが可能
  * https://github.com/github/licensed/blob/master/docs/configuration.md#applications
  * cache 後に `bundle exec licensed status` を実行することでテストが可能

- cache したライセンス情報をひとまとめにした NOTICE ファイルも出力可能
  * cache 後に `bundle exec licensed notices` を実行する

- CI に組み込んで運用すると便利
  * 違反ライブラリがないか検閲
  * NOTICE ファイルを出力することでライブラリのライセンス一覧を作成

- フロントアプリのライセンス表示
  * webpack などを使用すると JS が難読化されてライセンス情報が消失してしまう場合がある
  * ビルド後のファイルに NOTICE ファイルの URL をコメント追加することで対応可能
    + 参考: https://www.oh-benri-tools.com/blogs/5

設定ファイルの例

```
# .licensed.yml

# npm のみを調査
sources:
  npm: true

# 許可するライセンスのリスト
allowed:
  - mit
  - apache-2.0
  - bsd-2-clause
  - bsd-3-clause
  - cc0-1.0
  - isc
  - 0bsd

# 何らかの理由で licensed がライセンス情報を取得できなかった場合、
# 目視確認して問題なければ reviewed リストに加えて対応する
reviewed:
  npm:
    - '@webassemblyjs/helper-fsm'
    - '@webassemblyjs/leb128'
    - '@xtuc/ieee754'
    - 'anser'
    - 'atob'
    - 'cacache'
    - 'caniuse-lite'
    - 'color-convert'
    - 'dom-serializer'
    - 'domain-browser'
    - 'electron-to-chromium'
    - 'figgy-pudding'
    - 'filesize'
```
