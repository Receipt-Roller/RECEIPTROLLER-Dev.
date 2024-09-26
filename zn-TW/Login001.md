# 登入與存取令牌

本頁將說明如何獲取使用 {RECEIPT}ROLLER API 所需的存取令牌。要與 API 互動，您必須首先登入並取得存取令牌，此令牌證明您的憑證，應包含在每個 API 請求的標頭中。

## 登入 (/account/login)

**存取令牌** 是使用 API 所必需的。它證明了您的身份，並使用您的 {RECEIPT}ROLLER 帳戶的電子郵件和密碼取得。如果您沒有帳戶，請[點擊這裡註冊](https://receiptroller.com/identity/account/register?culture=zh-tw)。

### 認證方式

一旦登入，請在後續的 API 請求中，將存取令牌包含在標頭中，如下所示：

```
Authorization: Bearer {YOUR TOKEN HERE}
```

---

## 請求

- **端點**

  ```
  POST https://api.receiptroller.com/account/login
  ```

- **標頭**

  ```
  Content-Type: application/json
  Accept: application/json
  ```

- **請求主體**

  | 欄位        | 類型     | 必填   | 描述                                            |
  |-------------|----------|--------|-------------------------------------------------|
  | userName    | string   | 是     | 註冊的電子郵件地址                              |
  | password    | string   | 是     | 帳戶密碼                                        |
  | expire      | datetime | 選填   | 令牌的過期時間（若未設定，則應用預設值）          |

### 請求範例

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

## 回應

- **狀態碼**

  - **200 OK**: 驗證成功。
  - **400 Bad Request**: 無效的請求。
  - **401 Unauthorized**: 驗證失敗（電子郵件或密碼錯誤）。

- **回應主體**

  | 欄位     | 類型     | 描述                 |
  |----------|----------|----------------------|
  | token    | string   | 存取令牌              |
  | expire   | datetime | 令牌過期時間          |

### 成功回應範例

```json
{
  "token": "{YOUR TOKEN HERE}",
  "expire": "2022-12-25T22:11:52.13Z"
}
```

### 錯誤回應範例

```json
{
  "error": "Invalid credentials",
  "status": 401
}
```

---

## 使用存取令牌

獲取存取令牌後，請在其他 API 請求的標頭中包含此令牌，如下所示：

```
Authorization: Bearer {YOUR TOKEN HERE}
```

### 附帶令牌的請求範例

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/receipts' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN HERE}'
```

---

## 錯誤處理

發生錯誤時，API 會返回以下格式的回應：

- **回應主體**

  | 欄位   | 類型     | 描述               |
  |--------|----------|--------------------|
  | error  | string   | 錯誤訊息           |
  | status | int      | HTTP 狀態碼         |

### 常見 HTTP 狀態碼

- **400 Bad Request**: 無效的請求。
- **401 Unauthorized**: 驗證失敗。
- **403 Forbidden**: 您無權訪問此資源。
- **404 Not Found**: 無法找到該資源。
- **500 Internal Server Error**: 伺服器內部錯誤。

---

# 獲取帳戶信息 (/account/me)

此端點用於檢索當前登入用戶的帳戶信息，或驗證提供的存取令牌。需要存取令牌來檢索已驗證用戶的帳戶詳細信息。

## 認證方式

在標頭中包含您在登入時獲得的令牌：

```
Authorization: Bearer {YOUR TOKEN HERE}
```

---

## 請求

- **端點**

  ```
  GET https://api.receiptroller.com/account/me
  ```

- **標頭**

  ```
  Authorization: Bearer {YOUR TOKEN HERE}
  ```

---

## 回應

- **狀態碼**

  - **200 OK**: 成功檢索帳戶信息。
  - **401 Unauthorized**: 無效或缺少存取令牌。

- **回應主體**

  | 欄位     | 類型     | 描述                 |
  |----------|----------|----------------------|
  | id       | string   | 用戶 ID              |
  | userName | string   | 用戶名               |
  | email    | string   | 電子郵件             |

---

## 回應範例

```json
{
  "id": "12345",
  "userName": "user_example",
  "email": "user@example.com"
}
```
