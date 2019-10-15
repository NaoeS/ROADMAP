# TIPS

- Jest における Date オブジェクトのモック方法
  * 色々とアプローチ方法がある
    + https://github.com/facebook/jest/issues/2234
  * 結局 jest.fn() で擬似 constructor を作成し、グローバルの Date に代入する方法を採った
  * afterEach() で本来の Date に戻すことを忘れない
