# Terminal Data Management

Terminals belong under organizations but don’t necessarily have to be under a store. The terminal's assigned store can also be changed. This section explains how to retrieve and manage terminal information.

---

# Retrieve Terminal Data (`/{organizationId}/terminals`)

## Request

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/terminals' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "storeId": "1234-store-5678",
    "keyword": "terminal",
    "planId": "standard-plan",
    "currentPage": 1,
    "itemsPerPage": 10,
    "sort": "terminalCode asc"
}'
```

- **storeId**: Store ID
- **keyword**: Search keyword
- **planId**: Plan ID linked to the terminal
- **currentPage**: Current page (pagination)
- **itemsPerPage**: Number of items per page (max 1000)
- **sort**: Sort order (`terminalCode asc` or `terminalCode desc`)

## Response

```json
{
  "terminals": {
    "items": [
      {
        "id": "abc123-terminal-456",
        "organizationId": "1234-organization-5678",
        "storeId": "1234-store-5678",
        "terminalCode": "TM-001",
        "memo": "Terminal memo content",
        "planId": "standard-plan"
      }
    ],
    "currentPage": 1,
    "itemsPerPage": 10,
    "totalItems": 1,
    "totalPages": 1,
    "keyword": "terminal",
    "sort": "terminalCode asc"
  }
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

- **404 Not Found**: Specified `storeId` or `planId` does not exist
  ```json
  {
    "error": "Store or plan not found"
  }
  ```
# Retrieve Terminal Details (`/{organizationId}/terminal/{id}`)

## Request

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/{organizationId}/terminal/{id}' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}'
```

## Response

```json
{
  "id": "abc123-terminal-456",
  "organizationId": "1234-organization-5678",
  "storeId": "1234-store-5678",
  "terminalCode": "TM-001",
  "memo": "Terminal memo content",
  "planId": "standard-plan"
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

- **404 Not Found**: Specified `terminalId` does not exist
  ```json
  {
    "error": "Terminal not found"
  }
  ```
# Create Terminal (`/{organizationId}/terminal/create`)

## Request

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/terminal/create' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "storeId": "1234-store-5678",
    "terminalCode": "TM-002",
    "memo": "New terminal memo"
}'
```

## Request Body

- **storeId**: Store ID (required)
- **terminalCode**: Terminal code (required)
- **memo**: Memo (optional)

## Response

```json
{
  "id": "new-terminal-id",
  "organizationId": "1234-organization-5678",
  "storeId": "1234-store-5678",
  "terminalCode": "TM-002",
  "memo": "New terminal memo",
  "planId": "standard-plan"
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

- **409 Conflict**: Terminal code already exists
  ```json
  {
    "error": "Terminal code already exists"
  }
  ```
# Update Terminal (`/{organizationId}/terminal/update`)

## Request

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
    "memo": "Updated terminal memo"
}'
```

## Request Body

- **id**: Terminal ID (required)
- **storeId**: Store ID (optional, if changing)
- **terminalCode**: Terminal code (required)
- **memo**: Memo (optional)

## Response

```json
{
  "id": "abc123-terminal-456",
  "organizationId": "1234-organization-5678",
  "storeId": "1234-store-5678",
  "terminalCode": "TM-002",
  "memo": "Updated terminal memo",
  "planId": "standard-plan"
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

- **404 Not Found**: Terminal not found
  ```json
  {
    "error": "Terminal not found"
  }
  ```

- **409 Conflict**: Terminal code already exists
  ```json
  {
    "error": "Terminal code already exists"
  }
  ```
