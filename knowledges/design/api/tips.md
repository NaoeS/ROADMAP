# TIPS

- リクエスト長
  * RFC2616 によれば、どれだけ長くてもサーバで対応できるのが望ましいと書いてある
    + 無理ならば 414 (Request-URI Too Long) を返却するべきとも
    + https://triple-underscore.github.io/RFC2616-ja.html#section-3.2.1
  * Apache, Nginx, AWS ALB などでは制限が設けられている。ブラウザなどでも違いがある模様
    + https://yomon.hatenablog.com/entry/2017/08/25/012347
  * Nginx では下記のディレクティブでリクエスト長が制限されている
    + `client_header_buffer_size`, `large_client_header_buffers`
    + 前者の設定を超過した場合は、後者の設定が適用される
    + http://mogile.web.fc2.com/nginx/http/ngx_http_core_module.html#client_header_buffer_size

- GraphQL について
  * https://www.webprofessional.jp/rest-2-0-graphql/