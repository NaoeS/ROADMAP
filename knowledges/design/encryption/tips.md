# TIPS

- CBC のパディングオラクル攻撃について
  * 秘密鍵を持たずとも、暗号文ブロックのパディングを使用して解読する攻撃手法
  * オラクルとはあの某ソフトウェア会社ではなく、神託の意。サーバが復号結果の可否を返却する神託機械になることからそう呼ばれるようになった。
    + https://www.goto.info.waseda.ac.jp/~kiire/crypto/pad-oracle.php
  * ちなみに、Rails の暗号化モジュールである ActiveSupport::MessageEncryptor はこの攻撃を防ぐ機構（署名）を組み込んでいる
    + その影響か暗号化後の文字列が異様に長い。
    + https://github.com/rails/rails/blob/607470c9b40388a5fc454ec9363c7af2d51fcf1e/activesupport/lib/active_support/message_encryptor.rb#L151
  * Ruby で攻撃を再現した人
    + http://inaz2.hatenablog.com/entry/2015/12/23/000923
