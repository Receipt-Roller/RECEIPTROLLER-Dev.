# Theme Data Management

Themes can be associated with receipts, allowing customization of receipt design and additional content. You can display coupons, customized messages, and more based on purchase data.

---

## Main Features of Themes

- **Receipt Design Customization**: Modify the overall appearance and color scheme of receipts.
- **Content Addition**: Add custom HTML content to headers, footers, or specific sections.
- **Dynamic Content Display**: Display coupons or special messages based on purchase data.

---

## How to Use Themes

1. **Create a Theme**: Create a new theme. See [Create a Theme](/{organizationId}/theme/create) for details.
2. **Retrieve Themes**: Get existing themes. See [Retrieve Themes](/{organizationId}/theme/{id}) for details.
3. **Update Themes**: Update existing themes. See [Update Themes](/{organizationId}/theme/update) for details.
4. **Apply Themes**: Apply themes to receipts by specifying the theme ID when generating receipts.

---

# Retrieve Theme List (/{organizationId}/themes)

This endpoint retrieves a list of themes within the specified organization, used to manage receipt design and content like coupons or custom messages.

---

## Request

- **Endpoint**

      POST https://api.receiptroller.com/{organizationId}/themes

- **Headers**

      Content-Type: application/json
      Accept: application/json
      Authorization: Bearer {YOUR TOKEN HERE}

- **Request Body**

  | Field          | Type   | Required | Description                         |
  |----------------|--------|----------|-------------------------------------|
  | storeId        | string | Optional | Store ID                            |
  | keyword        | string | Optional | Theme search keyword                |
  | currentPage    | int    | Optional | Current page for pagination         |
  | itemsPerPage   | int    | Optional | Number of items per page (max 1000) |
  | sort           | string | Optional | Sorting order (e.g., "name asc")    |

### Sample Request

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/themes' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN HERE}' \
  -H 'Content-Type: application/json' \
  -d '{
  "storeId": "1234-store-5678",
  "keyword": "modern",
  "currentPage": 1,
  "itemsPerPage": 10,
  "sort": "name asc"
}'
```

---

## Response

- **Status Code**

  - **200 OK**: Successfully processed.

- **Response Body**

  | Field                         | Type    | Description                           |
  |-------------------------------|---------|---------------------------------------|
  | themes                        | object  | Theme information object              |
  | ├─ items                      | array   | Array of themes                       |
  | ├─ currentPage                | int     | Current page                          |
  | ├─ itemsPerPage               | int     | Number of items per page              |
  | ├─ totalItems                 | int     | Total number of items                 |
  | ├─ totalPages                 | int     | Total number of pages                 |
  | ├─ keyword                    | string  | Keyword used in search                |
  | └─ sort                       | string  | Sorting order applied                 |

### Sample Response

```json
{
  "themes": {
    "items": [
      {
        "id": "theme123",
        "organizationId": "1234-organization-5678",
        "name": "Modern Theme"
      }
    ],
    "currentPage": 1,
    "itemsPerPage": 10,
    "totalItems": 1,
    "totalPages": 1,
    "keyword": "modern",
    "sort": "name asc"
  }
}
```

---

## Response Notes

- Items or fields that could not be retrieved or are empty may not be included in the response.

---

## Error Handling

In case of errors during API usage, error responses will be returned in the following format.

- **Response Body**

  | Field     | Type   | Description           |
  |-----------|--------|-----------------------|
  | error     | string | Error message         |
  | status    | int    | HTTP status code      |

### Error Response Examples

- **400 Bad Request (Invalid Request Parameters)**

```json
{
  "error": "Invalid request parameters.",
  "status": 400
}
```

- **401 Unauthorized (Authentication Error)**

```json
{
  "error": "Unauthorized access. Invalid or missing token.",
  "status": 401
}
```

- **403 Forbidden (Access Denied)**

```json
{
  "error": "Forbidden. You do not have access to this resource.",
  "status": 403
}
```

- **404 Not Found (Themes Not Found)**

```json
{
  "error": "Themes not found.",
  "status": 404
}
```

- **500 Internal Server Error (Server Issue)**

```json
{
  "error": "An unexpected server issue occurred.",
  "status": 500
}
```

---
# Retrieve Theme (/{organizationId}/theme/{id})

This endpoint allows you to retrieve detailed information about a specific theme by its theme ID. Themes are used to manage the design and content of receipts, such as displaying coupons or customized messages based on purchase data.

---

## Request

- **Endpoint**

      GET https://api.receiptroller.com/{organizationId}/theme/{id}

- **Headers**

      Accept: application/json
      Authorization: Bearer {YOUR TOKEN HERE}

- **Path Parameters**

  | Parameter       | Type   | Required | Description   |
  |-----------------|--------|----------|---------------|
  | organizationId  | string | Required | Organization ID |
  | id              | string | Required | Theme ID       |

### Sample Request

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/{organizationId}/theme/{id}' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN HERE}'
```

---

## Response

- **Status Codes**

  - **200 OK**: Request processed successfully.
  - **404 Not Found**: The specified theme was not found.

- **Response Body**

  | Field                          | Type   | Description                      |
  |---------------------------------|--------|----------------------------------|
  | id                              | string | Theme ID                         |
  | organizationId                  | string | Organization ID                  |
  | name                            | string | Theme name                       |
  | backgroundColor                 | string | Background color (e.g., "#ffffff")|
  | foreColor                       | string | Foreground color (e.g., "#000000")|
  | headerContentHtml               | string | HTML content for the header      |
  | afterItemsContentHtml           | string | HTML displayed after item list   |
  | afterGrandTotalContentHtml      | string | HTML displayed after grand total |
  | afterPaymentMethodContentHtml   | string | HTML displayed after payment     |
  | footerContentHtml               | string | HTML content for the footer      |

### Sample Response

```json
{
  "id": "theme123",
  "organizationId": "1234-organization-5678",
  "name": "Modern Theme",
  "backgroundColor": "#ffffff",
  "foreColor": "#000000",
  "headerContentHtml": "<h1>Welcome to Our Store</h1>",
  "afterItemsContentHtml": "<p>Thank you for shopping!</p>",
  "afterGrandTotalContentHtml": "<p>Grand Total includes taxes.</p>",
  "afterPaymentMethodContentHtml": "<p>Paid via credit card.</p>",
  "footerContentHtml": "<footer>© 2024 Example Corp.</footer>"
}
```

---

## Response Notes

- Fields that are not retrieved or have empty values may be omitted from the response.

---

## Error Handling

If an error occurs while using the API, error responses will be returned in the following format.

- **Response Body**

  | Field  | Type   | Description            |
  |--------|--------|------------------------|
  | error  | string | Error message          |
  | status | int    | HTTP status code       |

### Error Response Examples

- **404 Not Found (Theme Not Found)**

```json
{
  "error": "Theme not found.",
  "status": 404
}
```

- **401 Unauthorized (Authentication Error)**

```json
{
  "error": "Unauthorized access. Invalid or missing token.",
  "status": 401
}
```

- **403 Forbidden (Access Denied)**

```json
{
  "error": "Forbidden. You do not have access to this resource.",
  "status": 403
}
```

- **500 Internal Server Error (Server Issue)**

```json
{
  "error": "An unexpected server issue occurred.",
  "status": 500
}
```

---

