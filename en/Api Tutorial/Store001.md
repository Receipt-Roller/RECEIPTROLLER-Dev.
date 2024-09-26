# Store Data Management

To use store data, you must have an organization ID and an access token. Multiple stores can be managed under each organization. This section explains how to retrieve and manage store information.

---

# Retrieve Store List (`/{organizationId}/stores`)

## Request

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

- **keyword**: Search keyword.
- **currentPage**: Current page (pagination).
- **itemsPerPage**: Items per page (max 1000).
- **sort**: Sort order (`storeName asc`, `storeName desc`, `storeCode asc`, `storeCode desc`).

## Response

```json
{
  "stores": {
    "items": [
      {
        "id": "9356c405-b51a-4c40-8a11-9898c6d4be66",
        "organizationId": "1234-organization-5678",
        "storeCode": "001",
        "storeName": "Shibuya Store",
        "storePrintName": "Shibuya Store",
        "storeAddress": "1-2-3 Dogenzaka, Shibuya, Tokyo",
        "storePrintAddress": "Dogenzaka 1-2-3, Shibuya",
        "storeRegistrationName": "Shibuya Store Inc.",
        "storeRegistrationCode": "RG12345678",
        "storeTel": "03-1234-5678",
        "storeMemo": "Store memo content"
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


## Error Responses

- **401 Unauthorized**: Authentication error (invalid token).
  
  ```json
  {
    "error": "Invalid or missing token"
  }
  ```

- **400 Bad Request**: Authentication error (incorrect fields or page number).
  ```json
  {
    "error": "Invalid request format"
  }
  ```

- **404 Not Found**: Organization does not exist.
  ```json
  {
     "error": "Organization not found"
  }
  ```

---

# Store Search by Phone Number (`/{organizationId}/stores/phonenumber`)

## Request

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

- **phoneNumber**: Store's phone number to search.
- **currentPage**: Current page for pagination.
- **itemsPerPage**: Number of items per page (up to 1000).
- **sort**: Sort order (`storeName asc`, `storeName desc`, `storeCode asc`, or `storeCode desc`).

## Response

```json
{
  "stores": {
    "items": [
      {
        "id": "9356c405-b51a-4c40-8a11-9898c6d4be66",
        "organizationId": "1234-organization-5678",
        "storeCode": "001",
        "storeName": "Shibuya Store",
        "storePrintName": "Shibuya Store",
        "storeAddress": "1-2-3 Dogenzaka, Shibuya, Tokyo",
        "storePrintAddress": "1-2-3 Dogenzaka, Shibuya, Tokyo",
        "storeRegistrationName": "Shibuya Store Co., Ltd.",
        "storeRegistrationCode": "RG12345678",
        "storeTel": "03-1234-5678",
        "storeMemo": "Store memo content"
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

## Error Response

- **404 Not Found**: No store matches the phone number.
```json
{
  "error": "Store not found"
}
```

- **400 Bad Request**: Invalid request format.
```json
{
  "error": "Invalid request format"
}
```

- **401 Unauthorized**: Authentication error.
```json
{
  "error": "Invalid or missing token"
}
```

---

# Retrieve Store Details (`/{organizationId}/store/{id}`)

## Request

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/{organizationId}/store/{id}' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}'
```

## Response

```json
{
  "id": "9356c405-b51a-4c40-8a11-9898c6d4be66",
  "organizationId": "1234-organization-5678",
  "storeCode": "001",
  "storeName": "Shibuya Store",
  "storePrintName": "Shibuya Store",
  "storeAddress": "1-2-3 Dogenzaka, Shibuya, Tokyo",
  "storePrintAddress": "1-2-3 Dogenzaka, Shibuya",
  "storeRegistrationName": "Shibuya Store Ltd.",
  "storeRegistrationCode": "RG12345678",
  "storeTel": "03-1234-5678",
  "storeMemo": "Store memo details"
}
```

## Error Responses

- **404 Not Found**: When the specified `storeId` is not found.
```json
{
  "error": "Store not found"
}
```

- **401 Unauthorized**: When authentication fails (invalid token).
```json
{
  "error": "Invalid or missing token"
}
```

- **400 Bad Request**: When the `storeId` format is invalid.
```json
{
  "error": "Invalid store ID format"
}
```

---

# Store Creation (`/{organizationId}/store/create`)

## Request

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/store/create' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "storeCode": "001",
    "storeName": "New Store Name",
    "storePrintName": "New Store Print Name",
    "storeAddress": "123 Shibuya Dogenzaka, Tokyo",
    "storePrintAddress": "Shibuya Dogenzaka 123",
    "storeRegistrationName": "Shibuya Store LLC",
    "storeRegistrationCode": "RG12345678",
    "storeTel": "03-1234-5678",
    "storeMemo": "Store memo details"
}'
```

## Request Body

- **storeCode**: Store code
- **storeName**: Store name
- **storePrintName**: Store print name
- **storeAddress**: Store address
- **storePrintAddress**: Print address
- **storeRegistrationName**: Registration name
- **storeRegistrationCode**: Registration code
- **storeTel**: Store telephone number
- **storeMemo**: Store memo

## Response

```json
{
  "id": "new-store-id",
  "organizationId": "1234-organization-5678",
  "storeCode": "001",
  "storeName": "New Store Name",
  "storePrintName": "New Store Print Name",
  "storeAddress": "123 Shibuya Dogenzaka, Tokyo",
  "storePrintAddress": "Shibuya Dogenzaka 123",
  "storeRegistrationName": "Shibuya Store LLC",
  "storeRegistrationCode": "RG12345678",
  "storeTel": "03-1234-5678",
  "storeMemo": "Store memo details"
}
```

## Error Response

- **400 Bad Request**: Invalid request
  ```json
  {
    "error": "Invalid request format"
  }
  ```

- **401 Unauthorized**: Authentication error
  ```json
  {
    "error": "Invalid or missing token"
  }
  ```

- **409 Conflict**: Store code already exists
  ```json
  {
    "error": "Store code already exists"
  }
  ```

---

# Store Information Update (`/{organizationId}/store/update`)

## Request

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/store/update' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "storeCode": "001",
    "storeName": "Updated Store Name",
    "storePrintName": "Updated Store Print Name",
    "storeAddress": "1-2-3 Shinjuku, Tokyo",
    "storePrintAddress": "Shinjuku 1-2-3",
    "storeRegistrationName": "Shinjuku Store LLC",
    "storeRegistrationCode": "RG98765432",
    "storeTel": "03-5678-1234",
    "storeMemo": "Updated store memo"
}'
```

## Request Body

- **storeCode**: Store code
- **storeName**: Store name
- **storePrintName**: Store print name
- **storeAddress**: Store address
- **storePrintAddress**: Store print address
- **storeRegistrationName**: Store registration name
- **storeRegistrationCode**: Store registration code
- **storeTel**: Store phone number
- **storeMemo**: Store memo

**Note**: Fields with `null` will not be updated. If an empty string is provided, it will overwrite the current value.

## Response

```json
{
  "id": "9356c405-b51a-4c40-8a11-9898c6d4be66",
  "organizationId": "1234-organization-5678",
  "storeCode": "001",
  "storeName": "Updated Store Name",
  "storePrintName": "Updated Store Print Name",
  "storeAddress": "1-2-3 Shinjuku, Tokyo",
  "storePrintAddress": "Shinjuku 1-2-3",
  "storeRegistrationName": "Shinjuku Store LLC",
  "storeRegistrationCode": "RG98765432",
  "storeTel": "03-5678-1234",
  "storeMemo": "Updated store memo"
}
```

## Error Response

- **400 Bad Request**: Invalid request
  ```json
  {
    "error": "Invalid request format"
  }
  ```

- **401 Unauthorized**: Authentication error
  ```json
  {
    "error": "Invalid or missing token"
  }
  ```

- **404 Not Found**: Store not found
  ```json
  {
    "error": "Store not found"
  }
  ```
