# 組織データ管理

各アカウントは、複数の組織を管理することができます。各組織の下には複数の店舗があり、さらにその下には複数の端末が配置されています。この階層構造を通じて、各エンドポイントでは組織、店舗、端末ごとのデータ管理が可能です。

## 組織データ

組織データは以下の項目が表示・編集可能です。

| 名前              | タイプ    | 必須  | 最大値 | メモ                 |
|-------------------|-----------|-------|--------|----------------------|
| id                | 文字列    |       | 68文字 | 閲覧のみ、組織ID      |
| name              | 文字列    | 必須  | 68文字 | 組織名               |
| postalCode        | 文字列    | 必須  | 12文字 | 郵便番号             |
| country           | 文字列    | 必須  | 24文字 | 国名                 |
| prefecture        | 文字列    | 必須  | 24文字 | 都道府県             |
| locality          | 文字列    | 必須  | 24文字 | 市区町村             |
| address1          | 文字列    | 必須  | 24文字 | 住所、番地           |
| address2          | 文字列    |       | 24文字 | ビル名、部屋名        |
| tel               | 文字列    | 必須  | 24文字 | 電話番号             |
| email             | 文字列    | 必須  | 48文字 | メールアドレス       |
| validPlans        | オブジェクト |       |        | 閲覧のみ、有効プランの一覧 |

---
# 組織一覧の取得 (/account/organizations)

このエンドポイントでは、組織の一覧情報を取得できます。

---

## リクエスト

- **エンドポイント**

    ```
    GET https://api.receiptroller.com/account/organizations
    ```

- **ヘッダー**

    ```
    Accept: application/json
    Authorization: Bearer {YOUR TOKEN}
    ```

---

## レスポンス

- **ステータスコード**

    ```
    200 OK: 正常に処理されました。
    401 Unauthorized: 認証に失敗しました。
    ```

- **レスポンスボディ**

    | フィールド名   | 型     | 説明           |
    |----------------|--------|----------------|
    | id             | string | 組織のID       |
    | name           | string | 組織の名前     |

---

### レスポンス例

```json
[
  {
    "id": "1a2b3c4d-5678-9101-1121-3141abc12345",
    "name": "Osaka Food Mart"
  },
  {
    "id": "4e5f6g7h-1234-5678-9101-1121def56789",
    "name": "Kobe Fashion Outlet"
  },
  {
    "id": "9i8j7k6l-4321-8765-2109-2233ghi98765",
    "name": "Kyoto Tea House"
  },
  {
    "id": "5m6n7o8p-8765-4321-0987-6677klm54321",
    "name": "Shibuya Electronics"
  }
]
```

## エラーハンドリング

API利用時にエラーが発生した場合、以下の形式でエラーレスポンスが返されます。

- **レスポンスボディ**

    | フィールド名 | 型     | 説明                |
    |-------------|--------|---------------------|
    | error       | string | エラーメッセージ     |
    | status      | int    | HTTPステータスコード |

---

### エラーレスポンス例

- **401 Unauthorized（認証に失敗した場合）**

    ```json
    {
      "error": "Unauthorized access. Invalid or missing token.",
      "status": 401
    }
    ```

- **404 Not Found（組織が見つからない場合）**

    ```json
    {
      "error": "Organization not found.",
      "status": 404
    }
    ```

- **500 Internal Server Error（サーバー内部エラーの場合）**

    ```json
    {
      "error": "An unexpected server issue occurred.",
      "status": 500
    }
    ```

---

# 組織詳細取得 (/account/organization/{id})

このエンドポイントでは、特定の組織の詳細情報を取得できます。

---

## リクエスト

- **エンドポイント**

    ```
    GET https://api.receiptroller.com/account/organization/{id}
    ```

- **ヘッダー**

    ```
    Accept: application/json
    Authorization: Bearer {YOUR TOKEN}
    ```

- **パスパラメータ**

    | パラメータ名  | 型     | 必須 | 説明        |
    |--------------|--------|------|-------------|
    | id           | string | 必須 | 組織のID     |

### リクエスト例

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/account/organization/8fe6866d-c5e1-4703-875d-d2bdfa10bc2a' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}'
```

---

## レスポンス

- **ステータスコード**

    ```
    200 OK: 正常に処理されました。
    404 Not Found: 組織が見つかりません。
    ```

- **レスポンスボディ**

    | フィールド名         | 型     | 説明               |
    |----------------------|--------|--------------------|
    | id                   | string | 組織のID           |
    | name                 | string | 組織の名前         |
    | postalCode           | string | 郵便番号           |
    | country              | string | 国                 |
    | prefecture           | string | 都道府県           |
    | locality             | string | 市町村             |
    | address1             | string | 住所1              |
    | address2             | string | 住所2              |
    | tel                  | string | 電話番号           |
    | email                | string | メールアドレス     |
    | validPlans           | array  | 有効なプラン情報    |

### レスポンス例

```json
{
  "id": "8fe6866d-c5e1-4703-875d-d2bdfa10bc2a",
  "name": "TOKYO ANIME",
  "postalCode": "1600022",
  "country": "JAPAN",
  "prefecture": "東京都",
  "locality": "新宿区",
  "address1": "新宿3丁目5-6",
  "address2": "ABCビル",
  "tel": "03-1234-5678",
  "email": "info@tokyoanime.jp",
  "validPlans": ["basic", "premium"]
}
```

---

# 組織情報の更新 (/account/organization/update)

このエンドポイントでは、組織の情報を更新します。

---

## リクエスト

- **エンドポイント**

    ```
    POST https://api.receiptroller.com/account/organization/update
    ```

- **ヘッダー**

    ```
    Content-Type: application/json
    Accept: application/json
    Authorization: Bearer {YOUR TOKEN}
    ```

- **リクエストボディ**

    | フィールド名   | 型     | 必須 | 説明            |
    |---------------|--------|------|-----------------|
    | id            | string | 必須 | 組織のID         |
    | name          | string | 任意 | 組織名           |
    | postalCode    | string | 任意 | 郵便番号         |
    | country       | string | 任意 | 国               |
    | prefecture    | string | 任意 | 都道府県         |
    | locality      | string | 任意 | 市町村           |
    | address1      | string | 任意 | 住所1            |
    | address2      | string | 任意 | 住所2            |
    | tel           | string | 任意 | 電話番号         |
    | email         | string | 任意 | メールアドレス   |
    | smaregiContractId | string | 任意 | スマレジ契約ID   |

### リクエスト例

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/account/organization/update' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
  "id": "8fe6866d-c5e1-4703-875d-d2bdfa10bc2a",
  "name":"TOKYO ANIME",
  "postalCode": "3800096",
  "country": "JAPAN",
  "prefecture": "長野県",
  "locality": "長野市",
  "address1": "鶴賀七瀬123-12"
}'
```

---

## レスポンス

- **ステータスコード**

    ```
    200 OK: 正常に処理されました。
    ```

- **レスポンスボディ**

    | フィールド名         | 型     | 説明               |
    |----------------------|--------|--------------------|
    | id                   | string | 組織のID           |
    | name                 | string | 組織の名前         |
    | postalCode           | string | 郵便番号           |
    | country              | string | 国                 |
    | prefecture           | string | 都道府県           |
    | locality             | string | 市町村             |
    | address1             | string | 住所1              |
    | address2             | string | 住所2              |
    | tel                  | string | 電話番号           |
    | email                | string | メールアドレス     |
    | smaregiContractId    | string | スマレジ契約ID     |

### レスポンス例

```json
{
  "id": "8fe6866d-c5e1-4703-875d-d2bdfa10bc2a",
  "name": "TOKYO ANIME",
  "postalCode": "3800096",
  "country": "JAPAN",
  "prefecture": "長野県",
  "locality": "長野市",
  "address1": "鶴賀七瀬123-12",
  "address2": null,
  "tel": null,
  "email": null,
  "smaregiContractId": null
}
```
