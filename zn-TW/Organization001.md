# 組織資料管理

每個帳戶可以管理多個組織。在每個組織下，可以有多個商店，每個商店可以有多個終端機。這種階層架構允許通過 API 端點進行組織、商店和終端機層級的數據管理。

## 組織資料

以下欄位可用於檢視或編輯組織資料：

| 名稱            | 類型   | 必填   | 最大長度 | 備註                          |
|------------------|--------|--------|---------|-------------------------------|
| id               | String |        | 68      | 只讀，組織 ID                   |
| name             | String | 必填   | 68      | 組織名稱                       |
| postalCode       | String | 必填   | 12      | 郵政編號                       |
| country          | String | 必填   | 24      | 國家                           |
| prefecture       | String | 必填   | 24      | 省/縣                          |
| locality         | String | 必填   | 24      | 城市                           |
| address1         | String | 必填   | 24      | 地址 1                         |
| address2         | String |        | 24      | 地址 2（建築、房間）            |
| tel              | String | 必填   | 24      | 電話號碼                       |
| email            | String | 必填   | 48      | 電子郵件地址                   |
| validPlans       | Object |        |         | 只讀，有效方案列表              |

---

# 獲取組織列表 (/account/organizations)

此端點用於檢索組織列表。

---

## 請求

- **端點**

    ```
    GET https://api.receiptroller.com/account/organizations
    ```

- **標頭**

    ```
    Accept: application/json
    Authorization: Bearer {YOUR TOKEN}
    ```

---

## 回應

- **狀態碼**

    ```
    200 OK: 處理成功。
    401 Unauthorized: 認證失敗。
    ```

- **回應主體**

    | 欄位名稱  | 類型   | 描述           |
    |-----------|--------|----------------|
    | id        | String | 組織 ID        |
    | name      | String | 組織名稱       |

---

### 回應範例

```json
[
  {
    "id": "1a2b3c4d-5678-9101-1121-3141abc12345",
    "name": "大阪食品超市"
  },
  {
    "id": "4e5f6g7h-1234-5678-9101-1121def56789",
    "name": "神戶時尚購物中心"
  },
  {
    "id": "9i8j7k6l-4321-8765-2109-2233ghi98765",
    "name": "京都茶館"
  },
  {
    "id": "5m6n7o8p-8765-4321-0987-6677klm54321",
    "name": "涉谷電子商店"
  }
]
```

## 錯誤處理

在使用 API 時發生錯誤時，錯誤回應將以以下格式返回。

- **回應主體**

    | 欄位名稱 | 類型   | 描述           |
    |----------|--------|----------------|
    | error    | String | 錯誤訊息        |
    | status   | Int    | HTTP 狀態碼     |

---

### 錯誤回應範例

- **401 Unauthorized (認證失敗時)**

    ```json
    {
      "error": "未經授權的存取。無效或缺少令牌。",
      "status": 401
    }
    ```

- **404 Not Found (找不到組織時)**

    ```json
    {
      "error": "找不到組織。",
      "status": 404
    }
    ```

- **500 Internal Server Error (發生伺服器錯誤時)**

    ```json
    {
      "error": "發生意外的伺服器錯誤。",
      "status": 500
    }
    ```

---
# 獲取組織詳細資料 (/account/organization/{id})

此端點用於檢索特定組織的詳細資料。

---

## 請求

- **端點**

    ```
    GET https://api.receiptroller.com/account/organization/{id}
    ```

- **標頭**

    ```
    Accept: application/json
    Authorization: Bearer {YOUR TOKEN}
    ```

- **路徑參數**

    | 參數名稱  | 類型   | 必填   | 描述           |
    |-----------|--------|--------|----------------|
    | id        | String | 必填   | 組織 ID        |

### 請求範例

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/account/organization/8fe6866d-c5e1-4703-875d-d2bdfa10bc2a' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}'
```

---

## 回應

- **狀態碼**

    ```
    200 OK: 成功處理。
    404 Not Found: 找不到組織。
    ```

- **回應主體**

    | 欄位名稱     | 類型   | 描述            |
    |--------------|--------|----------------|
    | id           | String | 組織 ID        |
    | name         | String | 組織名稱       |
    | postalCode   | String | 郵政編號       |
    | country      | String | 國家           |
    | prefecture   | String | 省/縣          |
    | locality     | String | 城市/鎮         |
    | address1     | String | 地址 1         |
    | address2     | String | 地址 2         |
    | tel          | String | 電話號碼       |
    | email        | String | 電子郵件地址   |
    | validPlans   | Array  | 有效方案列表    |

### 回應範例

```json
{
  "id": "8fe6866d-c5e1-4703-875d-d2bdfa10bc2a",
  "name": "東京動漫",
  "postalCode": "1600022",
  "country": "日本",
  "prefecture": "東京",
  "locality": "新宿",
  "address1": "新宿 3-5-6",
  "address2": "ABC 大樓",
  "tel": "03-1234-5678",
  "email": "info@tokyoanime.jp",
  "validPlans": ["standard", "premium"]
}
```

---
# 組織資訊更新 (/account/organization/update)

此端點允許更新組織的資訊。

---

## 請求

- **端點**

    ```
    POST https://api.receiptroller.com/account/organization/update
    ```

- **標頭**

    ```
    Content-Type: application/json
    Accept: application/json
    Authorization: Bearer {YOUR TOKEN}
    ```

- **請求主體**

    | 欄位名稱         | 類型   | 必填   | 描述             |
    |------------------|--------|--------|------------------|
    | id               | string | 必填   | 組織 ID           |
    | name             | string | 選填   | 組織名稱         |
    | postalCode       | string | 選填   | 郵政編號         |
    | country          | string | 選填   | 國家             |
    | prefecture       | string | 選填   | 省/縣            |
    | locality         | string | 選填   | 城市             |
    | address1         | string | 選填   | 地址 1           |
    | address2         | string | 選填   | 地址 2           |
    | tel              | string | 選填   | 電話號碼         |
    | email            | string | 選填   | 電子郵件地址     |

---

### 請求範例

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/account/organization/update' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
  "id": "c6a1ef30-12d4-4d9a-b6e0-f47c3e1a8349",
  "name": "大阪電子",
  "postalCode": "5300001",
  "country": "日本",
  "prefecture": "大阪",
  "locality": "大阪市",
  "address1": "北區梅田 2-4-6"
}'
```

---

## 回應

- **狀態碼**

    ```
    200 OK: 成功處理。
    ```

- **回應主體**

    | 欄位名稱         | 類型   | 描述             |
    |------------------|--------|------------------|
    | id               | string | 組織 ID           |
    | name             | string | 組織名稱         |
    | postalCode       | string | 郵政編號         |
    | country          | string | 國家             |
    | prefecture       | string | 省/縣            |
    | locality         | string | 城市             |
    | address1         | string | 地址 1           |
    | address2         | string | 地址 2           |
    | tel              | string | 電話號碼         |
    | email            | string | 電子郵件地址     |

---

### 回應範例

```json
{
  "id": "c6a1ef30-12d4-4d9a-b6e0-f47c3e1a8349",
  "name": "大阪電子",
  "postalCode": "5300001",
  "country": "日本",
  "prefecture": "大阪",
  "locality": "大阪市",
  "address1": "北區梅田 2-4-6",
  "address2": "梅田大樓 3F",
  "tel": "06-1234-5678",
  "email": "contact@osakaelectronics.jp"
}
```

---

