# 店舗データ管理

店舗データを利用する場合は、組織Idとアクセストークンが必ず必要です。各組織の下に複数の店舗を管理できます。このセクションでは、店舗情報の取得・管理について説明します。

---

# 店舗一覧の取得 (`/{organizationId}/stores`)

## リクエスト

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/stores' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "keyword": "渋谷",
    "currentPage": 1,
    "itemsPerPage": 10,
    "sort": "storeName asc"
}'
```

- **keyword**: 検索に使用されるキーワード
- **currentPage**: 現在のページ（ページネーション）
- **itemsPerPage**: ページごとのアイテム数。上限は1000件です。
- **sort**: 並び順（`storeName asc`, `storeName desc`, `storeCode asc`, `storeCode desc` のいずれか）

## レスポンス

```json
{
  "stores": {
    "items": [
      {
        "id": "9356c405-b51a-4c40-8a11-9898c6d4be66",
        "organizationId": "1234-organization-5678",
        "storeCode": "001",
        "storeName": "渋谷ストア",
        "storePrintName": "渋谷ストア",
        "storeAddress": "東京都渋谷区道玄坂1-2-3",
        "storePrintAddress": "渋谷区道玄坂1-2-3",
        "storeRegistrationName": "渋谷ストア有限会社",
        "storeRegistrationCode": "RG12345678",
        "storeTel": "03-1234-5678",
        "storeMemo": "店舗メモ内容"
      }
    ],
    "currentPage": 1,
    "itemsPerPage": 10,
    "totalItems": 1,
    "totalPages": 1,
    "keyword": "渋谷",
    "sort": "storeName asc"
  }
}
```

## エラーレスポンス

- **401 Unauthorized**: 認証エラー（無効なトークンの場合）
  ```json
  {
    "error": "Invalid or missing token"
  }
  ```

- **400 Bad Request**: 不正なリクエスト（無効なフィールドやページ番号）
  ```json
  {
    "error": "Invalid request format"
  }
  ```

- **404 Not Found**: 組織が存在しない場合
  ```json
  {
    "error": "Organization not found"
  }
  ```

---
# 店舗電話番号による検索 (`/{organizationId}/stores/phonenumber`)

## リクエスト

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/stores/phonenumber' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "phoneNumber": "03-1234-5678",
    "currentPage": 1,
    "itemsPerPage": 10,
    "sort": "storeName asc"
}'
```

- **phoneNumber**: 検索対象の店舗の電話番号
- **currentPage**: 現在のページ（ページネーション）
- **itemsPerPage**: ページごとのアイテム数。上限は1000件です。
- **sort**: 並び順（`storeName asc`, `storeName desc`, `storeCode asc`, `storeCode desc` のいずれか）

## レスポンス

```json
{
  "stores": {
    "items": [
      {
        "id": "9356c405-b51a-4c40-8a11-9898c6d4be66",
        "organizationId": "1234-organization-5678",
        "storeCode": "001",
        "storeName": "渋谷ストア",
        "storePrintName": "渋谷ストア",
        "storeAddress": "東京都渋谷区道玄坂1-2-3",
        "storePrintAddress": "渋谷区道玄坂1-2-3",
        "storeRegistrationName": "渋谷ストア有限会社",
        "storeRegistrationCode": "RG12345678",
        "storeTel": "03-1234-5678",
        "storeMemo": "店舗メモ内容"
      }
    ],
    "currentPage": 1,
    "itemsPerPage": 10,
    "totalItems": 1,
    "totalPages": 1,
    "keyword": "03-1234-5678",
    "sort": "storeName asc"
  }
}
```

## エラーレスポンス

- **404 Not Found**: 電話番号に一致する店舗が見つからない場合
  ```json
  {
    "error": "Store not found"
  }
  ```

- **400 Bad Request**: 不正なリクエストフォーマット
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

---

# 店舗詳細の取得 (`/{organizationId}/store/{id}`)

## リクエスト

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/{organizationId}/store/{id}' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}'
```

## レスポンス

```json
{
  "id": "9356c405-b51a-4c40-8a11-9898c6d4be66",
  "organizationId": "1234-organization-5678",
  "storeCode": "001",
  "storeName": "渋谷ストア",
  "storePrintName": "渋谷ストア",
  "storeAddress": "東京都渋谷区道玄坂1-2-3",
  "storePrintAddress": "渋谷区道玄坂1-2-3",
  "storeRegistrationName": "渋谷ストア有限会社",
  "storeRegistrationCode": "RG12345678",
  "storeTel": "03-1234-5678",
  "storeMemo": "メモ内容"
}
```

## エラーレスポンス

- **404 Not Found**: 指定された `storeId` が存在しない場合
  ```json
  {
    "error": "Store not found"
  }
  ```

- **401 Unauthorized**: 認証に失敗した場合（無効なトークン）
  ```json
  {
    "error": "Invalid or missing token"
  }
  ```

- **400 Bad Request**: 無効な `storeId` 形式の場合
  ```json
  {
    "error": "Invalid store ID format"
  }
  ```

---
# 店舗の作成 (`/{organizationId}/store/create`)

## リクエスト

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/store/create' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "storeCode": "001",
    "storeName": "新しい店舗名",
    "storePrintName": "新しい店舗名",
    "storeAddress": "東京都渋谷区道玄坂1-2-3",
    "storePrintAddress": "渋谷区道玄坂1-2-3",
    "storeRegisgrationName": "渋谷ストア有限会社",
    "storeRegisgrationCode": "RG12345678",
    "storeTel": "03-1234-5678",
    "storeMemo": "店舗メモ内容"
}'
```

## リクエストボディ

- **storeCode**: 店舗コード
- **storeName**: 店舗名
- **storePrintName**: 印刷用店舗名
- **storeAddress**: 店舗住所
- **storePrintAddress**: 印刷用店舗住所
- **storeRegisgrationName**: 店舗登録名
- **storeRegisgrationCode**: 店舗登録コード
- **storeTel**: 店舗電話番号
- **storeMemo**: 店舗メモ

## レスポンス

```json
{
  "id": "新しい店舗ID",
  "organizationId": "1234-organization-5678",
  "storeCode": "001",
  "storeName": "新しい店舗名",
  "storePrintName": "新しい店舗名",
  "storeAddress": "東京都渋谷区道玄坂1-2-3",
  "storePrintAddress": "渋谷区道玄坂1-2-3",
  "storeRegistrationName": "渋谷ストア有限会社",
  "storeRegistrationCode": "RG12345678",
  "storeTel": "03-1234-5678",
  "storeMemo": "店舗メモ内容"
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

- **409 Conflict**: 店舗コードが重複している場合
  ```json
  {
    "error": "Store code already exists"
  }
  ```

---

# 店舗情報の更新 (`/{organizationId}/store/update`)

## リクエスト

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/store/update' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "storeCode": "001",
    "storeName": "更新された店舗名",
    "storePrintName": "更新された店舗名",
    "storeAddress": "東京都新宿区新宿1-2-3",
    "storePrintAddress": "新宿区新宿1-2-3",
    "storeRegisgrationName": "新宿ストア有限会社",
    "storeRegisgrationCode": "RG98765432",
    "storeTel": "03-5678-1234",
    "storeMemo": "更新された店舗メモ"
}'
```

## リクエストボディ

- **storeCode**: 店舗コード
- **storeName**: 店舗名
- **storePrintName**: 印刷用店舗名
- **storeAddress**: 店舗住所
- **storePrintAddress**: 印刷用店舗住所
- **storeRegisgrationName**: 店舗登録名
- **storeRegisgrationCode**: 店舗登録コード
- **storeTel**: 店舗電話番号
- **storeMemo**: 店舗メモ

**注意**: 各フィールドが `null` の場合は変更されませんが、空文字列が指定された場合、その値で上書きされます。

## レスポンス

```json
{
  "id": "9356c405-b51a-4c40-8a11-9898c6d4be66",
  "organizationId": "1234-organization-5678",
  "storeCode": "001",
  "storeName": "更新された店舗名",
  "storePrintName": "更新された店舗名",
  "storeAddress": "東京都新宿区新宿1-2-3",
  "storePrintAddress": "新宿区新宿1-2-3",
  "storeRegistrationName": "新宿ストア有限会社",
  "storeRegistrationCode": "RG98765432",
  "storeTel": "03-5678-1234",
  "storeMemo": "更新された店舗メモ"
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

- **404 Not Found**: 店舗が見つからない場合
  ```json
  {
    "error": "Store not found"
  }
  ```


