# TIPS

- Nginx, Puma の同時接続数 について
  * Nginx は worker_process * worker_connection
    + https://qiita.com/toshihirock/items/f3aac142882c9c320b7f
  * Puma は worker * thread（ActiveRecord のコネクションプールも考慮が必要！）
    + https://blog.kasei-san.com/entry/2017/05/21/162837ß
