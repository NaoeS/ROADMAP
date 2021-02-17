# TIPS

- HTML5 タグ一覧
  * [W3C](https://www.w3.org/TR/2014/REC-html5-20141028/sections.html#the-article-element)
  * [MDN](https://developer.mozilla.org/ja/docs/Web/HTML/Element)
  * その他記事
    + https://qiita.com/cheez921/items/1d6844e22f1e728a475e

- MDN の HTML チュートリアル
  * https://developer.mozilla.org/ja/docs/Web/Guide/HTML/HTML5

- HTML 5 アウトライン
  * https://qiita.com/minami-actindi/items/176ffeeb6d660badab56
  * [チェッカー](https://gsnedders.html5.org/outliner/)

- iframe のセキュリティ
  * sandbox 属性を付与することで内部コンテンツの動作を制限する
    + https://developer.mozilla.org/ja/docs/Web/HTML/Element/iframe#attr-sandbox
    + `allow-scripts` と `allow-same-origin` は同時に指定してはならない
  * srcdoc 属性を使用する場合は、HTML文字列をサニタイズして悪意があるコードを指定しないようにする
    + 自前実装よりライブラリを使用するほうが良い
    + https://github.com/cure53/DOMPurify
