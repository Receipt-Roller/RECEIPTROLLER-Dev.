# Organization Data Management

Each account can manage multiple organizations. Under each organization, there are multiple stores, and each store can have multiple terminals. This hierarchy allows for data management at the organization, store, and terminal levels via the API endpoints.

## Organization Data

The following fields are available for viewing or editing in the organization data:

| Name             | Type      | Required | Max Length | Notes                          |
|------------------|-----------|----------|------------|---------------------------------|
| id               | String    |          | 68         | Read-only, organization ID      |
| name             | String    | Required | 68         | Organization name               |
| postalCode       | String    | Required | 12         | Postal code                     |
| country          | String    | Required | 24         | Country                         |
| prefecture       | String    | Required | 24         | Prefecture                      |
| locality         | String    | Required | 24         | City                            |
| address1         | String    | Required | 24         | Address line 1                  |
| address2         | String    |          | 24         | Address line 2 (building, room) |
| tel              | String    | Required | 24         | Phone number                    |
| email            | String    | Required | 48         | Email address                   |
| validPlans       | Object    |          |            | Read-only, list of active plans |

---

# Fetching Organization List (/account/organizations)

This endpoint retrieves the list of organizations.

---

## Request

- **Endpoint**

    ```
    GET https://api.receiptroller.com/account/organizations
    ```

- **Headers**

    ```
    Accept: application/json
    Authorization: Bearer {YOUR TOKEN}
    ```

---

## Response

- **Status Codes**

    ```
    200 OK: Successfully processed.
    401 Unauthorized: Authentication failed.
    ```

- **Response Body**

    | Field Name  | Type   | Description   |
    |-------------|--------|---------------|
    | id          | String | Organization ID |
    | name        | String | Organization name |

---

### Example Response

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

## Error Handling

If an error occurs while using the API, the following format will be returned in the error response.

- **Response Body**

    | Field Name | Type   | Description      |
    |------------|--------|------------------|
    | error      | String | Error message    |
    | status     | Int    | HTTP status code |

---

### Example Error Responses

- **401 Unauthorized (When authentication fails)**

    ```json
    {
      "error": "Unauthorized access. Invalid or missing token.",
      "status": 401
    }
    ```

- **404 Not Found (When organization is not found)**

    ```json
    {
      "error": "Organization not found.",
      "status": 404
    }
    ```

- **500 Internal Server Error (When a server error occurs)**

    ```json
    {
      "error": "An unexpected server issue occurred.",
      "status": 500
    }
    ```

---

# Fetch Organization Details (/account/organization/{id})

This endpoint retrieves the details of a specific organization.

---

## Request

- **Endpoint**

    ```
    GET https://api.receiptroller.com/account/organization/{id}
    ```

- **Headers**

    ```
    Accept: application/json
    Authorization: Bearer {YOUR TOKEN}
    ```

- **Path Parameters**

    | Parameter Name | Type   | Required | Description   |
    |----------------|--------|----------|---------------|
    | id             | String | Required | Organization ID |

### Request Example

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/account/organization/8fe6866d-c5e1-4703-875d-d2bdfa10bc2a' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}'
```

---

## Response

- **Status Codes**

    ```
    200 OK: Processed successfully.
    404 Not Found: Organization not found.
    ```

- **Response Body**

    | Field Name     | Type   | Description        |
    |----------------|--------|--------------------|
    | id             | String | Organization ID    |
    | name           | String | Organization name  |
    | postalCode     | String | Postal code        |
    | country        | String | Country            |
    | prefecture     | String | Prefecture         |
    | locality       | String | City/Town          |
    | address1       | String | Address line 1     |
    | address2       | String | Address line 2     |
    | tel            | String | Phone number       |
    | email          | String | Email address      |
    | validPlans     | Array  | List of valid plans|

### Example Response

```json
{
  "id": "8fe6866d-c5e1-4703-875d-d2bdfa10bc2a",
  "name": "TOKYO ANIME",
  "postalCode": "1600022",
  "country": "JAPAN",
  "prefecture": "Tokyo",
  "locality": "Shinjuku",
  "address1": "Shinjuku 3-5-6",
  "address2": "ABC Building",
  "tel": "03-1234-5678",
  "email": "info@tokyoanime.jp",
  "validPlans": ["basic", "premium"]
}
```

---

# Update Organization Information (/account/organization/update)

This endpoint allows you to update an organization’s information.

---

## Request

- **Endpoint**

    ```
    POST https://api.receiptroller.com/account/organization/update
    ```

- **Headers**

    ```
    Content-Type: application/json
    Accept: application/json
    Authorization: Bearer {YOUR TOKEN}
    ```

- **Request Body**

    | Field Name        | Type   | Required | Description        |
    |-------------------|--------|----------|--------------------|
    | id                | String | Required | Organization ID    |
    | name              | String | Optional | Organization name  |
    | postalCode        | String | Optional | Postal code        |
    | country           | String | Optional | Country            |
    | prefecture        | String | Optional | Prefecture         |
    | locality          | String | Optional | City               |
    | address1          | String | Optional | Address line 1     |
    | address2          | String | Optional | Address line 2     |
    | tel               | String | Optional | Phone number       |
    | email             | String | Optional | Email address      |

---

### Request Example

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/account/organization/update' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
  "id": "8fe6866d-c5e1-4703-875d-d2bdfa10bc2a",
  "name": "TOKYO ANIME",
  "postalCode": "3800096",
  "country": "JAPAN",
  "prefecture": "Nagano",
  "locality": "Nagano City",
  "address1": "Tsuruga Nanase 123-12"
}'
```

---

## Response

- **Status Codes**

    ```
    200 OK: Successfully processed.
    ```

- **Response Body**

    | Field Name         | Type   | Description           |
    |--------------------|--------|-----------------------|
    | id                 | String | Organization ID       |
    | name               | String | Organization name     |
    | postalCode         | String | Postal code           |
    | country            | String | Country               |
    | prefecture         | String | Prefecture            |
    | locality           | String | City                  |
    | address1           | String | Address line 1        |
    | address2           | String | Address line 2        |
    | tel                | String | Phone number          |
    | email              | String | Email address         |

---

# Organization Information Update (/account/organization/update)

This endpoint allows updating an organization’s information.

---

## Request

- **Endpoint**

    ```
    POST https://api.receiptroller.com/account/organization/update
    ```

- **Headers**

    ```
    Content-Type: application/json
    Accept: application/json
    Authorization: Bearer {YOUR TOKEN}
    ```

- **Request Body**

    | Field Name        | Type   | Required | Description        |
    |-------------------|--------|----------|--------------------|
    | id                | string | Required | Organization ID    |
    | name              | string | Optional | Organization name  |
    | postalCode        | string | Optional | Postal code        |
    | country           | string | Optional | Country            |
    | prefecture        | string | Optional | Prefecture         |
    | locality          | string | Optional | City               |
    | address1          | string | Optional | Address line 1     |
    | address2          | string | Optional | Address line 2     |
    | tel               | string | Optional | Phone number       |
    | email             | string | Optional | Email address      |

---

### Request Example

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/account/organization/update' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
  "id": "c6a1ef30-12d4-4d9a-b6e0-f47c3e1a8349",
  "name": "Osaka Electronics",
  "postalCode": "5300001",
  "country": "JAPAN",
  "prefecture": "Osaka",
  "locality": "Osaka City",
  "address1": "Kita-ku Umeda 2-4-6"
}'
```

---

## Response

- **Status Codes**

    ```
    200 OK: Successfully processed.
    ```

- **Response Body**

    | Field Name         | Type   | Description           |
    |--------------------|--------|-----------------------|
    | id                 | string | Organization ID       |
    | name               | string | Organization name     |
    | postalCode         | string | Postal code           |
    | country            | string | Country               |
    | prefecture         | string | Prefecture            |
    | locality           | string | City                  |
    | address1           | string | Address line 1        |
    | address2           | string | Address line 2        |
    | tel                | string | Phone number          |
    | email              | string | Email address         |

---

### Example Response

```json
{
  "id": "c6a1ef30-12d4-4d9a-b6e0-f47c3e1a8349",
  "name": "Osaka Electronics",
  "postalCode": "5300001",
  "country": "JAPAN",
  "prefecture": "Osaka",
  "locality": "Osaka City",
  "address1": "Kita-ku Umeda 2-4-6",
  "address2": "Umeda Building 3F",
  "tel": "06-1234-5678",
  "email": "contact@osakaelectronics.jp"
}
```
