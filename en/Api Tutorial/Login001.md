# Login and Access Tokens

This page explains how to obtain the access token necessary to use the {RECEIPT}ROLLER API. To interact with the API, you must first log in and obtain an access token, which proves your credentials and should be included in the header of each API request.

## Login (/account/login)

An **access token** is required to use the API. It proves your identity and is obtained using the email and password of your {RECEIPT}ROLLER account. If you don’t have an account, [register here](https://receiptroller.com/identity/account/register?culture=en).

### Authentication Method

Once logged in, include the access token in the header of subsequent API requests like this:

```
Authorization: Bearer {YOUR TOKEN HERE}
```

---

## Request

- **Endpoint**

  ```
  POST https://api.receiptroller.com/account/login
  ```

- **Headers**

  ```
  Content-Type: application/json
  Accept: application/json
  ```

- **Request Body**

  | Field      | Type     | Required | Description                                                 |
  |------------|----------|----------|-------------------------------------------------------------|
  | userName   | string   | Yes      | The registered email address                                |
  | password   | string   | Yes      | The account password                                        |
  | expire     | datetime | Optional | Expiration time of the token (default applies if not set)    |

### Request Example

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

## Response

- **Status Codes**

  - **200 OK**: Authentication successful.
  - **400 Bad Request**: Invalid request.
  - **401 Unauthorized**: Authentication failed (incorrect email or password).

- **Response Body**

  | Field   | Type     | Description          |
  |---------|----------|----------------------|
  | token   | string   | Access token         |
  | expire  | datetime | Token expiration     |

### Successful Response Example

```json
{
  "token": "{YOUR TOKEN HERE}",
  "expire": "2022-12-25T22:11:52.13Z"
}
```

### Error Response Example

```json
{
  "error": "Invalid credentials",
  "status": 401
}
```

---

## Using the Token

Once you've obtained the access token, include it in the headers of other API requests like this:

```
Authorization: Bearer {YOUR TOKEN HERE}
```

### Example of a Request with Token

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/receipts' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN HERE}'
```

---

## Error Handling

When an error occurs, the API returns a response in the following format:

- **Response Body**

  | Field  | Type     | Description       |
  |--------|----------|-------------------|
  | error  | string   | Error message     |
  | status | int      | HTTP status code  |

### Common HTTP Status Codes

- **400 Bad Request**: The request was invalid.
- **401 Unauthorized**: Authentication failed.
- **403 Forbidden**: You don't have access to this resource.
- **404 Not Found**: The resource could not be found.
- **500 Internal Server Error**: A server error occurred.

---

# Get Account Info (/account/me)

This endpoint is used to retrieve account information about the currently logged-in user or validate the provided access token. An access token is required to retrieve the authenticated user's account details.

## Authentication Method

Include the token you obtained during login in the headers:

```
Authorization: Bearer {YOUR TOKEN HERE}
```

---

## Request

- **Endpoint**

  ```
  GET https://api.receiptroller.com/account/me
  ```

- **Headers**

  ```
  Authorization: Bearer {YOUR TOKEN HERE}
  ```

---

## Response

- **Status Codes**

  - **200 OK**: Successfully retrieved account info.
  - **401 Unauthorized**: Invalid or missing token.

- **Response Body**

  | Field     | Type     | Description         |
  |-----------|----------|---------------------|
  | id        | string   | User ID             |
  | userName  | string   | Username            |
  | email     | string   | Email               |

---

## Response Example

```json
{
  "id": "12345",
  "userName": "user_example",
  "email": "user@example.com"
}
```
