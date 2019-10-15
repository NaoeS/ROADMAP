# TIPS

- 一度きりレンダリングする HOC
  * https://gist.github.com/koba04/0233ffa25fd77472fe4f#file-staticcomponent-js
  * 一度きりの描画で問題ない場合はこれを参考に HOC を作成すると負荷が軽減される
  * 子供となるコンポーネントの型で悩んだが、SFC or そうでないコンポーネントに対応する React.ComponentType 型で解決

- React の StrictMode
  * 非推奨のライフサイクルを使用していたらコンソールで怒られる
  * 自前で書いたコンポーネント以外にも、ライブラリ内で使用していたら怒られる
  * styled-components は古いライフサイクルを使用しているみたいなので次バージョンに期待

- React Saga
  * API 処理に限らず非同期処理を取りまとめてくれるすごいやつ
