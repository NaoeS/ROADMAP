# 暗号化

## 鍵生成
- 秘密鍵生成用のタスクとして Rails には rake secret がある
  * https://github.com/rails/rails/blob/b2eb1d1c55a59fee1e6c4cba7030d8ceb524267c/railties/lib/rails/tasks/misc.rake#L4

## ActiveSupport::MessageEncryptor
- 暗号化ライブラリ
- 出力される暗号文は `#{暗号文字列}--#{初期化ベクトル}` を Base64 変換したものとなる
  * 初期化ベクトルは同じ秘密鍵で暗号化しても毎回違う暗号文字列にするために使われる存在
  * 初期化ベクトル自体は外部に漏れても問題ない
  * 暗号モードが CBC なので、暗号化の際は初期化ベクトルを起点として暗号化が行われていく

```
class MyEncryptor
  def encrypt(message)
    encryptor.encrypt_and_sign(identity.raw) # 暗号化
  end

  def decrypt(encrypted_message)
    encryptor.decrypt_and_verify(serialized_identity) # 復号
  end

  private

  def encryptor
    ActiveSupport::MessageEncryptor.new('super_good_key', cipher: 'aes-256-cbc') # 暗号器作成
  end
end
```
