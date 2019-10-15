# TIPS

- NULL が許容されるカラムについて
  * インデックスはどのような挙動をするのか気になったので調べた
  * NULL もインデックスが貼られるらしい。この人はインデックスのデータ量が増えてしまうことを懸念している
    + http://d.hatena.ne.jp/manjuphobia/20100609/1276092532
  * NULL と 非 NULL に偏りがあり、かつ少数派を検索するなら問題はないとのこと。B-Tree の探索時に邪魔にならなければ良いのだろうか
    + https://techblog.istyle.co.jp/archives/1514
