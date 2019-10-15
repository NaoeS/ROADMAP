# Rails.cache

## 概要
- キャッシュの実装が抽象化されるため、Redis でも memcached にも対応できる
- Rails.cache の I/F を一律で使用するのでミドルウェアの変更に強い（DDDともリンクしている？

## Redis
- Rails 5.2 から Redis キャッシュストアが組み込まれた
- オブジェクトをそのまま write できるし、read した時にオブジェクトを復元できる
  * 内部では Marshal を用いている
