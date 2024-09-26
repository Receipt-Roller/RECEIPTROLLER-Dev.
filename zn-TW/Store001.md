# 商店數據管理

要使用商店數據，您需要擁有組織ID和存取令牌。在每個組織下可以管理多個商店。本節說明如何檢索和管理商店資訊。

---

# 檢索商店列表 (`/{organizationId}/stores`)

## 請求

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/stores' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "keyword": "Shibuya",
    "currentPage": 1,
    "itemsPerPage": 10,
    "sort": "storeName asc"
}'
```

- **keyword**: 搜索關鍵字。
- **currentPage**: 當前頁面（分頁）。
- **itemsPerPage**: 每頁顯示項目數量（上限1000）。
- **sort**: 排序方式（`storeName asc`, `storeName desc`, `storeCode asc`, `storeCode desc`）。

## 回應

```json
{
  "stores": {
    "items": [
      {
        "id": "9356c405-b51a-4c40-8a11-9898c6d4be66",
        "organizationId": "1234-organization-5678",
        "storeCode": "001",
        "storeName": "澀谷店",
        "storePrintName": "Shibuya Store",
        "storeAddress": "東京澀谷道玄坂1-2-3",
        "storePrintAddress": "澀谷區道玄坂1-2-3",
        "storeRegistrationName": "澀谷店股份有限公司",
        "storeRegistrationCode": "RG12345678",
        "storeTel": "03-1234-5678",
        "storeMemo": "商店備註內容"
      }
    ],
    "currentPage": 1,
    "itemsPerPage": 10,
    "totalItems": 1,
    "totalPages": 1,
    "keyword": "Shibuya",
    "sort": "storeName asc"
  }
}
```

## 錯誤回應

- **401 未授權**: 認證錯誤（令牌無效）。
  
  ```json
  {
    "error": "Invalid or missing token"
  }
  ```

- **400 錯誤請求**: 認證錯誤（欄位錯誤或頁面號碼不正確）。
  ```json
  {
    "error": "Invalid request format"
  }
  ```

- **404 找不到**: 組織不存在。
  ```json
  {
     "error": "Organization not found"
  }
  ```

---
# 透過電話號碼搜尋商店 (`/{organizationId}/stores/phonenumber`)

## 請求

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

- **phoneNumber**: 要搜尋的商店電話號碼。
- **currentPage**: 當前頁面（分頁）。
- **itemsPerPage**: 每頁項目數（最多1000）。
- **sort**: 排序方式（`storeName asc`、`storeName desc`、`storeCode asc` 或 `storeCode desc`）。

## 回應

```json
{
  "stores": {
    "items": [
      {
        "id": "9356c405-b51a-4c40-8a11-9898c6d4be66",
        "organizationId": "1234-organization-5678",
        "storeCode": "001",
        "storeName": "澀谷店",
        "storePrintName": "Shibuya Store",
        "storeAddress": "東京澀谷道玄坂1-2-3",
        "storePrintAddress": "東京澀谷道玄坂1-2-3",
        "storeRegistrationName": "澀谷店股份有限公司",
        "storeRegistrationCode": "RG12345678",
        "storeTel": "03-1234-5678",
        "storeMemo": "商店備註內容"
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

## 錯誤回應

- **404 找不到**: 沒有匹配的商店。
```json
{
  "error": "Store not found"
}
```

- **400 錯誤請求**: 無效的請求格式。
```json
{
  "error": "Invalid request format"
}
```

- **401 未授權**: 認證錯誤。
```json
{
  "error": "Invalid or missing token"
}
```

---
# 取得商店詳細資料 (`/{organizationId}/store/{id}`)

## 請求

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/{organizationId}/store/{id}' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}'
```

## 回應

```json
{
  "id": "9356c405-b51a-4c40-8a11-9898c6d4be66",
  "organizationId": "1234-organization-5678",
  "storeCode": "001",
  "storeName": "澀谷店",
  "storePrintName": "澀谷店",
  "storeAddress": "東京澀谷道玄坂1-2-3",
  "storePrintAddress": "東京澀谷道玄坂1-2-3",
  "storeRegistrationName": "澀谷商店有限公司",
  "storeRegistrationCode": "RG12345678",
  "storeTel": "03-1234-5678",
  "storeMemo": "商店備註內容"
}
```

## 錯誤回應

- **404 找不到**: 當指定的 `storeId` 不存在時。
```json
{
  "error": "Store not found"
}
```

- **401 未授權**: 當認證失敗（無效的令牌）。
```json
{
  "error": "Invalid or missing token"
}
```

- **400 錯誤請求**: 當 `storeId` 格式無效時。
```json
{
  "error": "Invalid store ID format"
}
```

---

# 創建商店 (`/{organizationId}/store/create`)

## 請求

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/store/create' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "storeCode": "001",
    "storeName": "新商店",
    "storePrintName": "新商店列印名稱",
    "storeAddress": "東京澀谷道玄坂123號",
    "storePrintAddress": "澀谷道玄坂123號",
    "storeRegistrationName": "澀谷商店股份有限公司",
    "storeRegistrationCode": "RG12345678",
    "storeTel": "03-1234-5678",
    "storeMemo": "商店備註內容"
}'
```

## 請求本文

- **storeCode**: 商店代碼
- **storeName**: 商店名稱
- **storePrintName**: 商店列印名稱
- **storeAddress**: 商店地址
- **storePrintAddress**: 列印地址
- **storeRegistrationName**: 商店註冊名稱
- **storeRegistrationCode**: 註冊代碼
- **storeTel**: 商店電話號碼
- **storeMemo**: 商店備註

## 回應

```json
{
  "id": "新商店id",
  "organizationId": "1234-organization-5678",
  "storeCode": "001",
  "storeName": "新商店",
  "storePrintName": "新商店列印名稱",
  "storeAddress": "東京澀谷道玄坂123號",
  "storePrintAddress": "澀谷道玄坂123號",
  "storeRegistrationName": "澀谷商店股份有限公司",
  "storeRegistrationCode": "RG12345678",
  "storeTel": "03-1234-5678",
  "storeMemo": "商店備註內容"
}
```

## 錯誤回應

- **400 錯誤請求**: 無效的請求
  ```json
  {
    "error": "Invalid request format"
  }
  ```

- **401 未授權**: 認證錯誤
  ```json
  {
    "error": "Invalid or missing token"
  }
  ```

- **409 衝突**: 商店代碼已存在
  ```json
  {
    "error": "Store code already exists"
  }
  ```

---

# 更新商店資訊 (`/{organizationId}/store/update`)

## 請求

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/store/update' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "storeCode": "001",
    "storeName": "更新的商店名稱",
    "storePrintName": "更新的商店列印名稱",
    "storeAddress": "東京新宿1-2-3",
    "storePrintAddress": "新宿1-2-3",
    "storeRegistrationName": "新宿商店股份有限公司",
    "storeRegistrationCode": "RG98765432",
    "storeTel": "03-5678-1234",
    "storeMemo": "更新的商店備註"
}'
```

## 請求本文

- **storeCode**: 商店代碼
- **storeName**: 商店名稱
- **storePrintName**: 商店列印名稱
- **storeAddress**: 商店地址
- **storePrintAddress**: 商店列印地址
- **storeRegistrationName**: 商店註冊名稱
- **storeRegistrationCode**: 商店註冊代碼
- **storeTel**: 商店電話號碼
- **storeMemo**: 商店備註

**注意**: 欄位值為 `null` 時將不會更新。如果提供了空字符串，將覆蓋當前值。

## 回應

```json
{
  "id": "9356c405-b51a-4c40-8a11-9898c6d4be66",
  "organizationId": "1234-organization-5678",
  "storeCode": "001",
  "storeName": "更新的商店名稱",
  "storePrintName": "更新的商店列印名稱",
  "storeAddress": "東京新宿1-2-3",
  "storePrintAddress": "新宿1-2-3",
  "storeRegistrationName": "新宿商店股份有限公司",
  "storeRegistrationCode": "RG98765432",
  "storeTel": "03-5678-1234",
  "storeMemo": "更新的商店備註"
}
```

## 錯誤回應

- **400 錯誤請求**: 無效的請求
  ```json
  {
    "error": "Invalid request format"
  }
  ```

- **401 未授權**: 認證錯誤
  ```json
  {
    "error": "Invalid or missing token"
  }
  ```

- **404 找不到**: 找不到商店
  ```json
  {
    "error": "Store not found"
  }
  ```

---
