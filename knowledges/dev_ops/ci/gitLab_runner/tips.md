# TIPS

- React アプリで実践
  * リポジトリ: https://gitlab.com/NaoeS/gitlab_runner_test
  * 参考
    + https://dev.classmethod.jp/articles/gitlab-runner-ci-cd-1/
    + https://qiita.com/jintz/items/f1105df12fe4fc8a45ca
  * AmazonLinux2 t2.micro 上に GitLab Runner をインストール

- Rails アプリで実践
  * リポジトリ: https://gitlab.com/NaoeS/wiz_arc/-/blob/master/.gitlab-ci.yml
  * 参考
    + https://docs.gitlab.com/ee/ci/examples/test-and-deploy-ruby-application-to-heroku.html#configure-the-project
    + https://qiita.com/masQuerade/items/86e1bc37c16c4bc83ca8
  * マイグレーション後に RSpec のテストを 4 件実行
    + t2.micro だと CI 実行時に CPU 使用率が 80% を超えるためテストとなると t2.medium ぐらいは必要

- 料金
  * t2.medium の稼働で 24$/month ぐらい
  * スポットインスタンスを使用してる人もいる。これなら高スペックを安価に回せそう？
    + https://qiita.com/tetsukay/items/cd9c3a6c432191dff25f
