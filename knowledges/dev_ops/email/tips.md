# TIPS

- セキュリティ設定
  * SPF(Sender Policy Framework)
    + 送信元メールサーバの IP と送信元ドメインの DNS レコードを確認することでなりすましを防止する認証技術
  * DKIM(DomainKeys Identified Mail)
    + 送信元ドメインの DNS レコードの署名情報を用いてなりすましを防止する認証技術
  * DMARC(Domain-based Message Authentication, Reporting, and Conformance)
    + SPF or DKIM またはその両方が認証に失敗した場合に、受信サーバの振る舞いを送信側が定義する仕組み
    + 受信サーバは認証が失敗した場合に、定義に従って「何もしない」「迷惑メールフォルダに入れる」「受信自体を拒否する」どれかを選択する
    + 送信者側は受信サーバが作成するメール送信状況のレポートを受け取れる
    + レポートは XML 形式で、どれくらい送信に合格したか、失敗したかを知れる
    + 受信サーバが DMARC を導入していない場合は、上記いずれも行われない
    + 日本の通信事業者が受信サーバに DMARC を導入する際には法的留意点が存在する
      - https://www.soumu.go.jp/main_sosiki/joho_tsusin/d_syohi/m_mail/legal.html
  * BIMI(Brand Indicators for Message Identification)
    + DMARC と VMC を用いて受信側のメールボックスにロゴ表示を行う技術
    + VMC は商標登録されているロゴの所有権を証明する認証技術
    + 2021 年現在では世界的な普及率は低い。黎明期ではあるがブランディングとしても有用なため広がりを見せそう
