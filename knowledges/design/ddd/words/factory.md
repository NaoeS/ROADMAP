# ファクトリ

## 集約上のファクトリ
- 集約内にファクトリメソッドとして定義して、別の集約を生成する時などに利用する
  * 集約内のコンストラクタで設定した値を使用して別の集約を作成できる時などに有用
  * 複雑なビジネスロジックが内包されていても、それをクライアント側が知る必要がない
  * ユビキタス言語で表現できる振る舞いであることが条件

```
module SignUpSessions
  #
  # サインアップセッション
  #
  class SignUpSession
    attr_reader :user_identity, :user_email

    def initialize(identity, user_identity, user_email)
      self.identity = identity
      self.user_identity = user_identity
      self.user_email = user_email
    end

    # サインアップセッションからユーザを作成するファクトリメソッド
    def create_user(user_identity, time_zone)
      Users::User.new(
        user_identity,
        user_email,
        time_zone
      )
    end
  end
end

```
