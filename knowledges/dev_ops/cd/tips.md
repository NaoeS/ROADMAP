# TIPS

- デプロイ手法参考
  * https://clonos.jp/knowledge/detail14/
  * https://garafu.blogspot.com/2018/11/release-strategy.html

- インプレースデプロイ
  * 新しいデプロイ資源を上書きで配置し、再起動を行う

- シンボリックリンク切り替え
  * デプロイ資源のシンボリックリンクを旧→新に切り替えて行う
  * 場合によっては再起動が必要になる

- ローリングデプロイ
  * LB の先にある複数のサーバに段階的にデプロイを行う

- カナリアリリース
  * LB の先にある複数のサーバのうち一つにデプロイを行い、一部のユーザに新環境を試してもらう
  * 新バージョンにアクセスするユーザーを炭鉱で毒ガスを検知する「カナリア」に見立てて名付けられた

- ブルーグリーンデプロイメント
  * 稼働中(ブルー)とは別の環境(グリーン)にデプロイし、問題なければ LB をグリーンに切り替える
  * グリーンで問題が発生した場合は、ブルーに戻して対処する

- イミュータブルデプロイメント
  * ブルーグリーンと似ているが、古い環境は削除されるためイミュータブルなデプロイとなる
  * コンテナを活用するデプロイとなる
