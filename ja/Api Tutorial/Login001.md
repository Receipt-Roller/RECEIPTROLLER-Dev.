# ログイン　(/account/login)

APIを利用するには、**アクセストークン**が必要です。アクセストークンは、APIを利用する際にあなたの会員情報を証明するものです。

普段お使いの{RECEIPT}ROLLERアカウントのメールアドレスとパスワードでログインできます。まだアカウントをお持ちでない方は、[こちらからご登録ください](https://receiptroller.com/identity/account/register?culture=ja)。

## 認証方法

ログイン後に取得したアクセストークンは、他のAPIエンドポイントへのリクエストで使用します。各リクエストのヘッダーに以下のようにトークンを含めてください。

```
Authorization: Bearer {YOUR TOKEN HERE}
```

---

# リクエスト

- **エンドポイント**

  ```
  POST https://api.receiptroller.com/account/login
  ```

- **ヘッダー**

  ```
  Content-Type: application/json
  Accept: application/json
  ```

- **リクエストボディ**

  | フィールド名 | 型       | 必須 | 説明                                                        |
  |--------------|----------|------|-------------------------------------------------------------|
  | userName     | string   | 必須 | 登録しているメールアドレス                                      |
  | password     | string   | 必須 | パスワード                                                    |
  | expire       | datetime | 任意 | トークンの有効期限（指定しない場合はデフォルトの有効期限が適用されます） |

### リクエスト例

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/account/login' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "userName": "your_email@example.com",
  "password": "your_password",
  "expire": "2022-12-25T22:11:52.130Z"
}'
```

---

# レスポンス

- **ステータスコード**

  - **200 OK**: 認証成功
  - **400 Bad Request**: リクエストが不正
  - **401 Unauthorized**: 認証失敗（メールアドレスまたはパスワードが間違っている可能性があります）

- **レスポンスボディ**

  | フィールド名 | 型       | 説明           |
  |--------------|----------|----------------|
  | token        | string   | アクセストークン   |
  | expire       | datetime | トークンの有効期限 |

### レスポンス例（成功時）

```json
{
  "token": "{YOUR TOKEN HERE}",
  "expire": "2022-12-25T22:11:52.13Z"
}
```

### エラーレスポンス例

```json
{
  "error": "Invalid credentials",
  "status": 401
}
```

---

## トークンの使用方法

取得したアクセストークンは、他のAPIリクエストのヘッダーに以下のように追加してください。

```
Authorization: Bearer {YOUR TOKEN HERE}
```

### トークンを使用したリクエスト例

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/receipts' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN HERE}'
```

---

## エラーハンドリング

API利用時にエラーが発生した場合、以下の形式でエラーレスポンスが返されます。

- **レスポンスボディ**

  | フィールド名 | 型     | 説明            |
  |--------------|--------|-----------------|
  | error        | string | エラーメッセージ    |
  | status       | int    | HTTPステータスコード |

### 共通のHTTPステータスコード

- **400 Bad Request**: リクエスト内容が不正です。
- **401 Unauthorized**: 認証に失敗しました。
- **403 Forbidden**: アクセス権がありません。
- **404 Not Found**: リソースが見つかりません。
- **500 Internal Server Error**: サーバー内部でエラーが発生しました。

---

# アカウント情報の取得（/account/me）

...

このエンドポイントは、現在ログインしている、または保持しているトークンが誰のものかを確認するために使用されます。認証されたユーザーのアカウント情報を取得するため、アクセストークンが必要です。

## 認証方法

事前にログインしてアクセストークンを取得し、以下のヘッダーにトークンを含めてリクエストします。

```
Authorization: Bearer {YOUR TOKEN HERE}
```

---

# リクエスト

- **エンドポイント**

  ```
  GET https://api.receiptroller.com/account/me
  ```

- **ヘッダー**

  ```
  Authorization: Bearer {YOUR TOKEN HERE}
  ```

---

# レスポンス

- **ステータスコード**

  - **200 OK**: アカウント情報取得成功
  - **401 Unauthorized**: 認証エラー（トークンが無効、または未提供）

- **レスポンスボディ**

  | フィールド名 | 型       | 説明           |
  |--------------|----------|----------------|
  | id           | string   | ユーザーID      |
  | userName     | string   | ユーザー名      |
  | email        | string   | メールアドレス  |

---

## レスポンス例

```json
{
  "id": "12345",
  "userName": "user_example",
  "email": "user@example.com"
}
```
