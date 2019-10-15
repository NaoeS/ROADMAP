# TIPS

- requestAnimationFrame について
  * アニメーションを行う場合は requestAnimationFrame() を使うのが推奨されている
  * requestAnimationFrame() はブラウザ判断で実行可能な状態で実行されるため、x 秒置きに必ず実行しなければいけない仕様だと微妙
  * しかし timestamp が取得できるため「最低 x 秒経過していたら実行する」ということはできる
  * 60 FPS ぐらい実行されるため負荷が高いと懸念していたが、CPU 使用率は setInterval() より軽い
