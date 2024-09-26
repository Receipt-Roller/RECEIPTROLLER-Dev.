# 端末データ管理

端末は組織の下にあり、必ずしも店舗の下にある必要はありません。また、端末の所属店舗は変更可能です。このセクションでは、端末情報の取得・管理について説明します。

---

# 端末データの取得 (`/{organizationId}/terminals`)

## リクエスト

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/terminals' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "storeId": "1234-store-5678",
    "keyword": "端末",
    "planId": "standard-plan",
    "currentPage": 1,
    "itemsPerPage": 10,
    "sort": "terminalCode asc"
}'
```

- **storeId**: 店舗ID
- **keyword**: 検索キーワード
- **planId**: 端末に紐づくプランID
- **currentPage**: 現在のページ（ページネーション）
- **itemsPerPage**: ページごとのアイテム数。上限は1000件です。
- **sort**: 並び順（`terminalCode asc` または `terminalCode desc`）

## レスポンス

```json
{
  "terminals": {
    "items": [
      {
        "id": "abc123-terminal-456",
        "organizationId": "1234-organization-5678",
        "storeId": "1234-store-5678",
        "terminalCode": "TM-001",
        "memo": "端末メモ内容",
        "planId": "standard-plan"
      }
    ],
    "currentPage": 1,
    "itemsPerPage": 10,
    "totalItems": 1,
    "totalPages": 1,
    "keyword": "端末",
    "sort": "terminalCode asc"
  }
}
```

## エラーレスポンス

- **400 Bad Request**: 不正なリクエスト
  ```json
  {
    "error": "Invalid request format"
  }
  ```

- **401 Unauthorized**: 認証エラー
  ```json
  {
    "error": "Invalid or missing token"
  }
  ```

- **404 Not Found**: 指定された `storeId` または `planId` が存在しない場合
  ```json
  {
    "error": "Store or plan not found"
  }
  ```

---
# 端末詳細の取得 (`/{organizationId}/terminal/{id}`)

## リクエスト

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/{organizationId}/terminal/{id}' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}'
```

## レスポンス

```json
{
  "id": "abc123-terminal-456",
  "organizationId": "1234-organization-5678",
  "storeId": "1234-store-5678",
  "terminalCode": "TM-001",
  "memo": "端末メモ内容",
  "planId": "standard-plan"
}
```

## エラーレスポンス

- **400 Bad Request**: 不正なリクエスト
  ```json
  {
    "error": "Invalid request format"
  }
  ```

- **401 Unauthorized**: 認証エラー
  ```json
  {
    "error": "Invalid or missing token"
  }
  ```

- **404 Not Found**: 指定された `terminalId` が存在しない場合
  ```json
  {
    "error": "Terminal not found"
  }
  ```

---

# 端末の作成 (`/{organizationId}/terminal/create`)

## リクエスト

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/terminal/create' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "storeId": "1234-store-5678",
    "terminalCode": "TM-002",
    "memo": "新しい端末メモ"
}'
```

## リクエストボディ

- **storeId**: 店舗ID（必須）
- **terminalCode**: 端末コード（必須）
- **memo**: メモ（任意）

## レスポンス

```json
{
  "id": "新しい端末ID",
  "organizationId": "1234-organization-5678",
  "storeId": "1234-store-5678",
  "terminalCode": "TM-002",
  "memo": "新しい端末メモ",
  "planId": "standard-plan"
}
```

## エラーレスポンス

- **400 Bad Request**: 不正なリクエスト
  ```json
  {
    "error": "Invalid request format"
  }
  ```

- **401 Unauthorized**: 認証エラー
  ```json
  {
    "error": "Invalid or missing token"
  }
  ```

- **409 Conflict**: 端末コードが既に存在する場合
  ```json
  {
    "error": "Terminal code already exists"
  }
  ```

  ---
  
# 端末の更新 (`/{organizationId}/terminal/update`)

## リクエスト

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/terminal/update' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "id": "abc123-terminal-456",
    "storeId": "1234-store-5678",
    "terminalCode": "TM-002",
    "memo": "更新された端末メモ"
}'
```

## リクエストボディ

- **id**: 端末ID（必須）
- **storeId**: 店舗ID（任意、変更がある場合）
- **terminalCode**: 端末コード（必須）
- **memo**: メモ（任意）

## レスポンス

```json
{
  "id": "abc123-terminal-456",
  "organizationId": "1234-organization-5678",
  "storeId": "1234-store-5678",
  "terminalCode": "TM-002",
  "memo": "更新された端末メモ",
  "planId": "standard-plan"
}
```

## エラーレスポンス

- **400 Bad Request**: 不正なリクエスト
  ```json
  {
    "error": "Invalid request format"
  }
  ```

- **401 Unauthorized**: 認証エラー
  ```json
  {
    "error": "Invalid or missing token"
  }
  ```

- **404 Not Found**: 端末が存在しない場合
  ```json
  {
    "error": "Terminal not found"
  }
  ```

- **409 Conflict**: 端末コードが既に存在する場合
  ```json
  {
    "error": "Terminal code already exists"
  }
  ```


