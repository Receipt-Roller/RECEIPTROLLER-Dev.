# Receipt Data Management

Receipt data management collects and stores transaction details, including customer information, payment methods, details of purchased items, applied discounts and taxes, and staff information. Membership program usage, coupon application history, and subscription details are also managed. This enables efficient organization of store sales data and tracking of customer purchase history and payment details. Customizable information can also be included for receipt printing.

# Receipt Data Type

| Field Name                       | Type           | Description                            |
|-----------------------------------|----------------|----------------------------------------|
| organizationId                    | string         | Organization ID                        |
| receiptId                         | string         | Receipt ID                             |
| transactionType                   | int            | Transaction type (e.g., 1=Purchase, 2=Return) |
| cancelType                        | int            | Cancellation type                      |
| terminalTransactionId             | string         | Terminal Transaction ID                |
| terminalTransactionDateTime       | string (ISO8601) | Terminal Transaction DateTime        |
| timestamp                         | string (ISO8601) | Receipt creation timestamp            |
| channelId                         | string         | Channel ID                             |
| terminalId                        | string         | Terminal ID                            |
| customer.customerId               | string         | Customer ID                            |
| customer.customerName             | string         | Customer name                          |
| customer.customerPrintName        | string         | Customer print name                    |
| customer.customerGroup            | string         | Customer group                         |
| customer.customerCode             | string         | Customer code                          |
| customer.customerMemo             | string         | Customer memo                          |
| customer.destinationEmail         | string         | Customer email                         |
| customer.destinationSms           | string         | Customer SMS number                    |
| customer.destinationLineMid       | string         | Customer LINE MID                      |
| roundingPosition                  | int            | Rounding position                      |
| roundingMethod                    | int            | Rounding method                        |
| memo                              | string         | Receipt memo                           |
| tags                              | string         | Tags attached to receipt               |
| barcode                           | string         | Barcode                                |
| themeId                           | string         | Theme ID                               |
| store.storeId                     | string         | Store ID                               |
| store.storeCode                   | string         | Store code                             |
| store.storeName                   | string         | Store name                             |
| store.storePrintName              | string         | Store print name                       |
| store.storeAddress                | string         | Store address                          |
| store.storePrintAddress           | string         | Store print address                    |
| store.storeRegisgrationName       | string         | Store registration name                |
| store.storeRegisgrationCode       | string         | Store registration code                |
| store.storeTel                    | string         | Store phone number                     |
| store.storeMemo                   | string         | Store memo                             |
| staff.staffId                     | string         | Staff ID                               |
| staff.staffCode                   | string         | Staff code                             |
| staff.staffName                   | string         | Staff name                             |

## Payment Information

| Field Name                       | Type           | Description                            |
|-----------------------------------|----------------|----------------------------------------|
| paymentSummary.shippingFee        | int            | Shipping fee                           |
| paymentSummary.serviceFee         | int            | Service fee                            |
| paymentSummary.otherFee           | int            | Other fees                             |
| paymentSummary.grandTotal         | int            | Grand total                            |
| paymentSummary.depositMethod      | int            | Deposit method                         |
| paymentSummary.deposit            | int            | Deposit amount                         |
| paymentSummary.change             | int            | Change                                 |
| paymentSummary.subTotal           | int            | Subtotal                               |
| paymentSummary.subTotalDiscountAmount | int        | Subtotal discount amount               |
| paymentSummary.subTotalDiscountRate | float        | Subtotal discount rate                 |
| paymentSummary.subtotalDiscountPrice | int         | Subtotal after discount                |
| paymentSummary.taxes              | array          | Tax details                            |

### Tax Details

| Field Name                       | Type           | Description                            |
|-----------------------------------|----------------|----------------------------------------|
| taxes.taxIfInclude                | int            | Tax-included amount                    |
| taxes.taxIfExclude                | int            | Tax-excluded amount                    |
| taxes.taxPercentageIfInclude      | int            | Tax rate (included)                    |
| taxes.taxPercentageIfExclude      | int            | Tax rate (excluded)                    |
| taxes.applicableSubTotalAmount    | int            | Applicable subtotal amount             |

## Item Information (itemDetailLines)

| Field Name                       | Type           | Description                            |
|-----------------------------------|----------------|----------------------------------------|
| itemDetailLines.lineId            | string         | Line ID                                |
| itemDetailLines.itemId            | string         | Item ID                                |
| itemDetailLines.itemType          | int            | Item type                              |
| itemDetailLines.salesType         | int            | Sales type                             |
| itemDetailLines.productId         | string         | Product code                           |
| itemDetailLines.productCode       | string         | Product code                           |
| itemDetailLines.productName       | string         | Product name                           |
| itemDetailLines.taxCategory       | int            | Tax category                           |
| itemDetailLines.price             | int            | Price                                  |
| itemDetailLines.salesPrice        | int            | Sales price                            |
| itemDetailLines.quantity          | int            | Quantity                               |
| itemDetailLines.taxDivision       | string         | Tax division                           |
| itemDetailLines.taxFreeDivision   | int            | Tax-free division                      |
| itemDetailLines.taxFreeAmount     | int            | Tax-free amount                        |
| itemDetailLines.categoryId        | string         | Category ID                            |
| itemDetailLines.categoryName      | string         | Category name                          |
| itemDetailLines.taxRate           | string         | Tax rate                               |
| itemDetailLines.unitNonDiscountSum| int            | Sum before discount                    |
| itemDetailLines.bargainName       | string         | Bargain name                           |
| itemDetailLines.bargainDiscountProportional | int | Bargain discount rate                  |
| itemDetailLines.taxIncludeProportional | int    | Tax-included discount rate             |
| itemDetailLines.taxExcludeProportional | int    | Tax-excluded discount rate             |
| itemDetailLines.unitDiscountSum   | int            | Sum after discount                     |
| itemDetailLines.unitDiscountName  | string         | Discount name                          |
| itemDetailLines.discountPriceProportional | int   | Discount price                         |
| itemDetailLines.discountCouponProportional | int  | Discount coupon                        |
| itemDetailLines.couponDiscount    | int            | Coupon discount amount                 |
| itemDetailLines.taxes             | array          | Tax information     |

## Subscription Information

| Field Name                       | Type           | Description                            |
|-----------------------------------|----------------|----------------------------------------|
| subscriptions.lineId              | string         | Line ID                                |
| subscriptions.subscriptionCode    | string         | Subscription code                      |
| subscriptions.description         | string         | Subscription description               |
| subscriptions.charged             | int            | Charged amount                         |
| subscriptions.unitInCharge        | string         | Unit in charge                         |
| subscriptions.validSince          | string (ISO8601) | Subscription validity start           |
| subscriptions.validUntil          | string (ISO8601) | Subscription validity end             |
| subscriptions.paymentMethod       | string         | Payment method                         |
| subscriptions.memo                | string         | Memo                                   |
| subscriptions.maxCall             | int            | Maximum call                           |
| subscriptions.called              | int            | Calls made                             |
| subscriptions.chargedBy           | string         | Charged by                             |
| subscriptions.isExpired           | boolean        | Expired or not                         |
| subscriptions.expireHandled       | string (ISO8601) | Expiry handled date                  |
| subscriptions.chargeResponseStatus| string         | Charge response status                 |
| subscriptions.chargeResponseMessage| string        | Charge response message                |

---

# Receipt Data Retrieval (`/{organizationId}/receipts`)

## Request

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/receipts' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "storeId": "1234-store-5678",
    "terminalId": "tm-001",
    "keyword": "Receipt search",
    "sort": "transactionId asc",
    "currentPage": 1,
    "itemsPerPage": 10,
    "year": 2024,
    "month": 9
}'
```

- **storeId**: Store ID
- **terminalId**: Terminal ID
- **keyword**: Search keyword
- **sort**: Sorting order (`transactionId asc` or `transactionId desc`)
- **currentPage**: Current page (for pagination)
- **itemsPerPage**: Number of items per page (max 1000)
- **year**: Year to search for
- **month**: Month to search for

## Response

```json
{
  "items": [
    {
      "receipt": {
        "organizationId": "1234-organization-5678",
        "receiptId": "rec-001",
        "transactionType": 1,
        "cancelType": 0,
        "terminalTransactionId": "txn-001",
        "terminalTransactionDateTime": "2024-09-26T01:24:01.437Z",
        "timestamp": "2024-09-26T01:24:01.437Z",
        "channelId": "ch-001",
        "terminalId": "tm-001",
        "customer": {
          "customerId": "cust-001",
          "customerName": "Taro Yamada",
          "customerPrintName": "Taro Yamada",
          "customerGroup": "VIP",
          "customerCode": "C123456",
          "customerMemo": "No special notes",
          "destinationEmail": "example@email.com",
          "destinationSms": "090-1234-5678",
          "destinationLineMid": "line-id-001",
          "membershipPrograms": [
            {
              "membershipProgramName": "Gold Member",
              "membershipProgramPointsUsed": "100",
              "membershipProgramPointsAdded": "50",
              "membershipProgramPointsAfter": "150",
              "membershipProgramPointsBefore": "100",
              "membershipProgramPointsNote": "Campaign points"
            }
          ]
        },
        "roundingPosition": 2,
        "roundingMethod": 1,
        "memo": "Receipt memo",
        "tags": "sale,discount",
        "barcode": "BRC123456",
        "themeId": "theme-001",
        "store": {
          "storeId": "1234-store-5678",
          "storeCode": "S001",
          "storeName": "Shibuya Store",
          "storePrintName": "Shibuya",
          "storeAddress": "1-2-3 Dogenzaka, Shibuya-ku, Tokyo",
          "storePrintAddress": "Shibuya-ku, Tokyo",
          "storeRegisgrationName": "Shibuya Store LLC",
          "storeRegisgrationCode": "RG123456",
          "storeTel": "03-1234-5678",
          "storeMemo": "Store memo"
        },
        "staff": {
          "staffId": "stf-001",
          "staffCode": "S001",
          "staffName": "Ichiro Suzuki"
        },
        "paymentSummary": {
          "shippingFee": 500,
          "serviceFee": 300,
          "otherFee": 200,
          "grandTotal": 10000,
          "despoitMethod": 1,
          "deposit": 10000,
          "change": 0,
          "subTotal": 9200,
          "subTotalDiscountAmount": 300,
          "subTotalDiscountRate": 3.5,
          "subtotalDiscountPrice": 8900,
          "taxes": [
            {
              "taxIfInclude": 500,
              "taxIfExclude": 400,
              "taxPercentageIfInclude": 8,
              "taxPercentageIfExclude": 5,
              "applicableSubTotalAmount": 8900
            }
          ]
        },
        "coupon": {
          "couponName": "10% off coupon",
          "couponPointsUsed": 100,
          "couponPointsAdded": 50,
          "couponPointsAfter": 150,
          "couponPointsBefore": 100,
          "couponNote": "Coupon applied"
        },
        "transactionId": "txn-001"
      },
      "itemDetailLines": [
        {
          "lineId": "line-001",
          "itemId": "item-001",
          "itemType": 1,
          "salesType": 0,
          "productId": "prod-001",
          "productCode": "P001",
          "productName": "Product A",
          "taxCategory": 1,
          "price": 1000,
          "salesPrice": 900,
          "quantity": 1,
          "taxDivision": "inclusive",
          "taxFreeDivision": 0,
          "taxFreeAmount": 0,
          "categoryId": "cat-001",
          "categoryName": "Food",
          "taxRate": "8%",
          "unitNonDiscountSum": "1000",
          "bargainName": "Special price",
          "bargainDiscountProportional": "100",
          "taxIncludeProportional": "80",
          "taxExcludeProportional": "70",
          "unitDiscountSum": "900",
          "unitDiscountName": "Discount",
          "discountPriceProportional": "100",
          "discountCouponProportional": "50",
          "couponDiscount": "50",
          "taxes": [
            {
              "taxIfInclude": 80,
              "taxIfExclude": 70,
              "taxPercentageIfInclude": 8,
              "taxPercentageIfExclude": 5,
              "applicableSubTotalAmount": 900
            }
          ]
        }
      ],
      "subscriptions": [
        {
          "lineId": "sub-001",
          "subscriptionCode": "SUB123",
          "description": "Subscription A",
          "charged": 1500,
          "unitInCharge": "JPY",
          "validSince": "2024-09-26T01:24:01.437Z",
          "validUntil": "2024-12-26T01:24:01.437Z",
          "paymentMethod": "Credit card",
          "memo": "Subscription memo",
          "maxCall": 10,
          "called": 2,
          "chargedBy": "Service A",
          "isExipred": false,
          "exipireHandled": "2024-09-26T01:24:01.437Z",
          "chargeResponseStatus": "success",
          "chargeResponseMessage": "Success"
        }
      ]
    }
  ],
  "currentPage": 1,
  "itemsPerPage": 10,
  "totalItems": 1,
  "totalPages": 1,
  "keyword": "Receipt search",
  "sort": "transactionId asc"
}
```

## Error Response

- **400 Bad Request**: Invalid request format
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

- **404 Not Found**: Receipt not found
  ```json
  {
    "error": "Receipt not found"
  }
  ```

---

# Receipt Details Retrieval (`/{organizationId}/{yyyyMM}/{storeId}/receipt/{id}`)

## Request

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/{organizationId}/{yyyyMM}/{storeId}/receipt/{id}' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}'
```

## Response

```json
{
  "receipt": {
    "organizationId": "1234-organization-5678",
    "receiptId": "rec-001",
    "transactionType": 1,
    "cancelType": 0,
    "terminalTransactionId": "txn-001",
    "terminalTransactionDateTime": "2024-09-26T01:28:18.815Z",
    "timestamp": "2024-09-26T01:28:18.815Z",
    "channelId": "ch-001",
    "terminalId": "tm-001",
    "customer": {
      "customerId": "cust-001",
      "customerName": "Taro Yamada",
      "customerPrintName": "Taro Yamada",
      "customerGroup": "VIP",
      "customerCode": "C123456",
      "customerMemo": "No special notes",
      "destinationEmail": "example@email.com",
      "destinationSms": "090-1234-5678",
      "destinationLineMid": "line-id-001",
      "membershipPrograms": [
        {
          "membershipProgramName": "Gold Member",
          "membershipProgramPointsUsed": "100",
          "membershipProgramPointsAdded": "50",
          "membershipProgramPointsAfter": "150",
          "membershipProgramPointsBefore": "100",
          "membershipProgramPointsNote": "Campaign points"
        }
      ]
    },
    "roundingPosition": 2,
    "roundingMethod": 1,
    "memo": "Receipt memo",
    "tags": "sale,discount",
    "barcode": "BRC123456",
    "themeId": "theme-001",
    "store": {
      "storeId": "1234-store-5678",
      "storeCode": "S001",
      "storeName": "Shibuya Store",
      "storePrintName": "Shibuya",
      "storeAddress": "1-2-3 Dogenzaka, Shibuya-ku, Tokyo",
      "storePrintAddress": "Shibuya-ku, Tokyo",
      "storeRegisgrationName": "Shibuya Store LLC",
      "storeRegisgrationCode": "RG123456",
      "storeTel": "03-1234-5678",
      "storeMemo": "Store memo"
    },
    "staff": {
      "staffId": "stf-001",
      "staffCode": "S001",
      "staffName": "Ichiro Suzuki"
    },
    "paymentSummary": {
      "shippingFee": 500,
      "serviceFee": 300,
      "otherFee": 200,
      "grandTotal": 10000,
      "despoitMethod": 1,
      "deposit": 10000,
      "change": 0,
      "subTotal": 9200,
      "subTotalDiscountAmount": 300,
      "subTotalDiscountRate": 3.5,
      "subtotalDiscountPrice": 8900,
      "taxes": [
        {
          "taxIfInclude": 500,
          "taxIfExclude": 400,
          "taxPercentageIfInclude": 8,
          "taxPercentageIfExclude": 5,
          "applicableSubTotalAmount": 8900
        }
      ]
    },
    "coupon": {
      "couponName": "10% off coupon",
      "couponPointsUsed": 100,
      "couponPointsAdded": 50,
      "couponPointsAfter": 150,
      "couponPointsBefore": 100,
      "couponNote": "Coupon applied"
    },
    "transactionId": "txn-001"
  },
  "itemDetailLines": [
    {
      "lineId": "line-001",
      "itemId": "item-001",
      "itemType": 1,
      "salesType": 0,
      "productId": "prod-001",
      "productCode": "P001",
      "productName": "Product A",
      "taxCategory": 1,
      "price": 1000,
      "salesPrice": 900,
      "quantity": 1,
      "taxDivision": "inclusive",
      "taxFreeDivision": 0,
      "taxFreeAmount": 0,
      "categoryId": "cat-001",
      "categoryName": "Food",
      "taxRate": "8%",
      "unitNonDiscountSum": "1000",
      "bargainName": "Special price",
      "bargainDiscountProportional": "100",
      "taxIncludeProportional": "80",
      "taxExcludeProportional": "70",
      "unitDiscountSum": "900",
      "unitDiscountName": "Discount",
      "discountPriceProportional": "100",
      "discountCouponProportional": "50",
      "couponDiscount": "50",
      "taxes": [
        {
          "taxIfInclude": 80,
          "taxIfExclude": 70,
          "taxPercentageIfInclude": 8,
          "taxPercentageIfExclude": 5,
          "applicableSubTotalAmount": 900
        }
      ]
    }
  ],
  "subscriptions": [
    {
      "lineId": "sub-001",
      "subscriptionCode": "SUB123",
      "description": "Subscription A",
      "charged": 1500,
      "unitInCharge": "JPY",
      "validSince": "2024-09-26T01:28:18.815Z",
      "validUntil": "2024-12-26T01:28:18.815Z",
      "paymentMethod": "Credit card",
      "memo": "Subscription memo",
      "maxCall": 10,
      "called": 2,
      "chargedBy": "Service A",
      "isExipred": false,
      "exipireHandled": "2024-09-26T01:28:18.815Z",
      "chargeResponseStatus": "success",
      "chargeResponseMessage": "Success"
    }
  ]
}
```

## Error Response

- **400 Bad Request**: Invalid request format
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

- **404 Not Found**: Receipt not found
  ```json
  {
    "error": "Receipt not found"
  }
  ```
---

# Create Receipt (`/{organizationId}/receipt/create`)

## Request

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/receipt/create' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "transactionType": 0,
    "cancelType": 0,
    "terminalTransactionId": "txn-001",
    "terminalTransactionDateTime": "2024-09-26T01:31:10.197Z",
    "storeId": "1234-store-5678",
    "terminalId": "tm-001",
    "staff": {
      "staffId": "stf-001",
      "staffCode": "S001",
      "staffName": "Ichiro Suzuki"
    },
    "coupon": [
      {
        "couponName": "10% Off",
        "couponPointsUsed": 100,
        "couponPointsAdded": 50,
        "couponPointsAfter": 150,
        "couponPointsBefore": 100,
        "couponNote": "Coupon applied"
      }
    ],
    "customer": {
      "customerId": "cust-001",
      "customerName": "Taro Yamada",
      "customerPrintName": "Taro Yamada",
      "customerGroup": "VIP",
      "customerCode": "C123456",
      "customerMemo": "No special notes",
      "destinationEmail": "example@email.com",
      "destinationSms": "090-1234-5678",
      "destinationLineMid": "line-id-001",
      "membershipPrograms": [
        {
          "membershipProgramName": "Gold Member",
          "membershipProgramPointsUsed": "100",
          "membershipProgramPointsAdded": "50",
          "membershipProgramPointsAfter": "150",
          "membershipProgramPointsBefore": "100",
          "membershipProgramPointsNote": "Campaign points"
        }
      ]
    },
    "items": [
      {
        "lineItemId": "item-001",
        "lineItemType": 0,
        "salesTypes": 0,
        "productId": "prod-001",
        "productCode": "P001",
        "productName": "Product A",
        "salesPrice": 900,
        "qt": 1,
        "taxes": [
          {
            "taxIfInclude": 80,
            "taxIfExclude": 70,
            "taxPercentageIfInclude": 8,
            "taxPercentageIfExclude": 5,
            "applicableSubTotalAmount": 900
          }
        ]
      }
    ],
    "roundingPosition": 0,
    "roundingMethod": 1,
    "paymentSummary": {
      "shippingFee": 500,
      "serviceFee": 300,
      "otherFee": 200,
      "grandTotal": 10000,
      "despoitMethod": 1,
      "deposit": 10000,
      "change": 0,
      "subTotal": 9200,
      "subTotalDiscountAmount": 300,
      "subTotalDiscountRate": 3.5,
      "subtotalDiscountPrice": 8900,
      "taxes": [
        {
          "taxIfInclude": 500,
          "taxIfExclude": 400,
          "taxPercentageIfInclude": 8,
          "taxPercentageIfExclude": 5,
          "applicableSubTotalAmount": 8900
        }
      ]
    },
    "memo": "Receipt memo",
    "tags": "sale,discount",
    "barcode": "BRC123456",
    "themeId": "theme-001",
    "currency": "JPY"
}'
```

### Notes

- **storeId**, **staffId**, **customerId** are not validated.
- **terminalId** must be validated and exist.
- **terminalTransactionId** uniqueness is not checked.
- **roundingMethod**: 
  - `0`: Round down
  - `1`: Round to nearest (round half-up)
  - `2`: Round up
- **tags** are comma-separated.
- **themeId** defaults to the default theme if no match is found.

## Response

```json
{
  "receipt": {
    "organizationId": "1234-organization-5678",
    "receiptId": "rec-001",
    "transactionType": 0,
    "cancelType": 0,
    "terminalTransactionId": "txn-001",
    "terminalTransactionDateTime": "2024-09-26T01:31:10.199Z",
    "timestamp": "2024-09-26T01:31:10.199Z",
    "channelId": "ch-001",
    "terminalId": "tm-001",
    "customer": {
      "customerId": "cust-001",
      "customerName": "Taro Yamada",
      "customerPrintName": "Taro Yamada",
      "customerGroup": "VIP",
      "customerCode": "C123456",
      "customerMemo": "No special notes",
      "destinationEmail": "example@email.com",
      "destinationSms": "090-1234-5678",
      "destinationLineMid": "line-id-001",
      "membershipPrograms": [
        {
          "membershipProgramName": "Gold Member",
          "membershipProgramPointsUsed": "100",
          "membershipProgramPointsAdded": "50",
          "membershipProgramPointsAfter": "150",
          "membershipProgramPointsBefore": "100",
          "membershipProgramPointsNote": "Campaign points"
        }
      ]
    },
    "roundingPosition": 0,
    "roundingMethod": 0,
    "memo": "Receipt memo",
    "tags": "sale, discount",
    "barcode": "BRC123456",
    "themeId": "theme-001",
    "store": {
      "storeId": "1234-store-5678",
      "storeCode": "S001",
      "storeName": "Shibuya Store",
      "storePrintName": "Shibuya",
      "storeAddress": "1-2-3 Dogenzaka, Shibuya-ku, Tokyo",
      "storePrintAddress": "Shibuya-ku, Tokyo",
      "storeRegisgrationName": "Shibuya Store LLC",
      "storeRegisgrationCode": "RG123456",
      "storeTel": "03-1234-5678",
      "storeMemo": "Store memo"
    },
    "staff": {
      "staffId": "stf-001",
      "staffCode": "S001",
      "staffName": "Ichiro Suzuki"
    },
    "paymentSummary": {
      "shippingFee": 500,
      "serviceFee": 300,
      "otherFee": 200,
      "grandTotal": 10000,
      "despoitMethod": 1,
      "deposit": 10000,
      "change": 0,
      "subTotal": 9200,
      "subTotalDiscountAmount": 300,
      "subTotalDiscountRate": 3.5,
      "subtotalDiscountPrice": 8900,
      "taxes": [
        {
          "taxIfInclude": 500,
          "taxIfExclude": 400,
          "taxPercentageIfInclude": 8,
          "taxPercentageIfExclude": 5,
          "applicableSubTotalAmount": 8900
        }
      ]
    },
    "coupon": {
      "couponName": "10% Off",
      "couponPointsUsed": 100,
      "couponPointsAdded": 50,
      "couponPointsAfter": 150,
      "couponPointsBefore": 100,
      "couponNote": "Coupon applied"
    },
    "transactionId": "txn-001"
  },
  "itemDetailLines": [
    {
      "lineId": "line-001",
      "itemId": "item-001",
      "itemType": 0,
      "salesType": 0,
      "productId": "prod-001",
      "productCode": "P001",
      "productName": "Product A",
      "taxCategory": 1,
      "price": 1000,
      "salesPrice": 900,
      "quantity": 1,
      "taxDivision": "inclusive",
      "taxFreeDivision": 0,
      "taxFreeAmount": 0,
      "categoryId": "cat-001",
      "categoryName": "Food",
      "taxRate": "8%",
      "unitNonDiscountSum": "1000",
      "bargainName": "Special price",
      "bargainDiscountProportional": "100",
      "taxIncludeProportional": "80",
      "taxExcludeProportional": "70",
      "unitDiscountSum": "900",
      "unitDiscountName": "Discount",
      "discountPriceProportional": "100",
      "discountCouponProportional": "50",
      "couponDiscount": "50",
      "taxes": [
        {
          "taxIfInclude": 80,
          "taxIfExclude": 70,
          "taxPercentageIfInclude": 8,
          "taxPercentageIfExclude": 5,
          "applicableSubTotalAmount": 900
        }
      ]
    }
  ],"subscriptions": [
    {
      "lineId": "sub-001",
      "subscriptionCode": "SUB123",
      "description": "Subscription A",
      "charged": 1500,
      "unitInCharge": "JPY",
      "validSince": "2024-09-26T01:31:10.199Z",
      "validUntil": "2024-12-26T01:31:10.199Z",
      "paymentMethod": "Credit Card",
      "memo": "Subscription memo",
      "maxCall": 10,
      "called": 2,
      "chargedBy": "Service A",
      "isExpired": false,
      "expireHandled": "2024-09-26T01:31:10.199Z",
      "chargeResponseStatus": "success",
      "chargeResponseMessage": "Successful"
    }
  ]
}
```

--- 

# Receipt Data OCR Analysis (`/{organizationId}/receipt/read`)

This endpoint performs OCR on a receipt image at the specified URL and returns the receipt information.

## Request

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/receipt/read' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "url": "https://example.com/receipt-image.jpg"
}'
```

### Notes

- OCR analyzes the image at the specified URL to extract receipt data.
- Errors occur if the image is unreadable or doesn't contain a recognizable receipt.
- Errors will also occur if the subscription is inactive.

## Response

The response format is the same as creating a receipt (see `/receipt/create` response).

### Error Response Examples

- **404 Not Found**: When the image is not found or unreadable
  ```json
  {
    "error": "Image not found or unreadable"
  }
  ```

- **400 Bad Request**: If the receipt cannot be recognized
  ```json
  {
    "error": "Unable to recognize receipt from image"
  }
  ```

- **403 Forbidden**: If the subscription is inactive
  ```json
  {
    "error": "Subscription is not active"
  }
  ```
# Base64 Image OCR Analysis (`/{organizationId}/receipt/upload-read`)

This endpoint analyzes a Base64-encoded image using OCR and returns the receipt data.

## Request

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/receipt/upload-read' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "imageInBase64String": "{BASE64_ENCODED_IMAGE}"
}'
```

### Notes

- Pass the Base64-encoded image data in the `imageInBase64String` field.
- OCR will analyze the image and return the results as receipt data.

## Response

If the OCR analysis is successful, the response format is the same as when creating a receipt (refer to `/receipt/create` response).

### Error Response Examples

- **400 Bad Request**: If the image is invalid or unreadable
  ```json
  {
    "error": "Invalid or unreadable image data"
  }
  ```

- **403 Forbidden**: If the subscription is inactive
  ```json
  {
    "error": "Subscription is not active"
  }
  ```

  # Base64 Settlement Receipt OCR Analysis (`/{organizationId}/receipt/store/{storeId}/readtype/{readType}/upload-read`)

This endpoint analyzes a Base64-encoded settlement receipt image using OCR and returns the receipt data.

## Request

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/receipt/store/{storeId}/readtype/{readType}/upload-read' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "imageInBase64String": "{BASE64_ENCODED_IMAGE}"
}'
```

### Notes

- Provide Base64-encoded receipt image data in the `imageInBase64String` field.
- OCR analyzes the settlement receipt and returns the results.

## Response

**Note**: The response will only contain fields for successfully extracted information. Missing fields indicate unreadable or non-existent data.

```json
{
    "rotatedImageUrl": "https://example.com/rotatedImage.jpg",
    "organizationId": "org-1234",
    "receipt": {
         "id": "org-1234-receipt-5678",
        "timestamp": "2024-09-26T02:04:09.257Z",
        "createdAt": "2024-09-26T02:04:09.257Z",
        "isTotalSalesReceipt": true,
        "currency": "JPY",
        "setId": "set-1001",
        "nameOfStore": "Shibuya Store",
        "address": "1-2-3 Shibuya, Tokyo",
        "prefecture": "Tokyo",
        "locality": "Shibuya",
        "phoneNumber": "03-1234-5678",
        "terminalId": "terminal-001",
        "settlementDateTime": "2024-09-26T01:54:32.506Z",
        "subtotal": "10000",
        "subTotalDiscount": "500",
        "subTotalDiscountExIntTax": "450",
        "subTotalDiscountRate": "5%",
        "subTotalDiscountRateExIntTax": "4.5%",
        "useOfPoints": "200",
        "singleItemDiscount": "100",
        "roundingDownDiscount": "0",
        "total": "9500",
        "totalCash": "5000",
        "totalCredit": "4500",
        "totalSmaregiPaymentIcReader": "0",
        "totalSmaregiPaymentVega3000": "0",
        "TotalSmaregiPaygate": "0",
        "totalPaymentMaster": "0",
        "totalPmJmups": "0",
        "totalPmThincacloud": "0",
        "totalFgCenter": "0",
        "totalRakutenPay": "0",
        "totalStoresCoiney": "0",
        "totalSquare": "4500",
        "totalJetsCats300Cats330": "0",
        "totalJetsJtC17u": "0",
        "totalJmupsJtc30l": "0",
        "totalJtc31qJetsCloud": "0",
        "totalJtvt10": "0",
        "totalOtegaruPayCredit": "0",
        "totalOtegaruPayEMoney": "0",
        "totalOtegaruPayJmups2Pocket": "0",
        "totalInfoxJtc16u": "0",
        "totalVeega3000Mobile2": "0",
        "totalSteraTerminal": "0",
        "totalSaturn1000eSaturn1000l": "0",
        "totalSmartcoin": "0",
        "totalStarPay": "0",
        "totalDracoin": "0",
        "totalProductVouchers": "0",
        "totalPromotionVouchers": "0",
        "totalChangeDifference": "0",
        "totalTransportIC": "0",
        "TotalAlipay": "0",
        "TotalWeChatPay": "0",
        "TotalSaleOnCredit": "0",
        "salesTax": "950",
        "taxIncluded": "10000",
        "taxExcluded": "9000",
        "taxExemptionTargetAmount": "0",
        "taxExemptionAmount": "0",
        "totalExcludedFromSalesExcludedTaxExcluded": "0",
        "totalReceivedExcludedFromSales": "0",
        "totalReceivedExcludedFromSalesCash": "0",
        "totalReceivedExcludedFromSalesCredit": "0",
        "totalReceivedExcludedFromSalesSmaregiPaymentIcReader": "0",
        "totalReceivedExcludedFromSalesSmaregiPaymentVega3000": "0",
        "TotalReceivedExcludedFromSalesSmaregiPaygate": "0",
        "totalReceivedExcludedFromSalesPaymentMaster": "0",
        "totalReceivedExcludedFromSalesPmJmups": "0",
        "totalReceivedExcludedFromSalesPmThincacloud": "0",
        "totalReceivedExcludedFromSalesFgCenter": "0",
        "totalReceivedExcludedFromSalesRakutenPay": "0",
        "totalReceivedExcludedFromSalesStoresCoiney": "0",
        "totalReceivedExcludedFromSalesSquare": "4500",
        "totalReceivedExcludedFromSalesJetsCats300Cats330": "0",
        "totalReceivedExcludedFromSalesJetsJtC17u": "0",
        "totalReceivedExcludedFromSalesJmupsJtc30l": "0",
        "totalReceivedExcludedFromSalesJtc31qJetsCloud": "0",
        "totalReceivedExcludedFromSalesJtvt10": "0",
        "totalReceivedExcludedFromSalesOtegaruPayCredit": "0",
        "totalReceivedExcludedFromSalesOtegaruPayEMoney": "0",
        "totalReceivedExcludedFromSalesOtegaruPayJmups2Pocket": "0",
        "totalReceivedExcludedFromSalesInfoxJtc16u": "0",
        "totalReceivedExcludedFromSalesVeega3000Mobile2": "0",
        "totalReceivedExcludedFromSalesSteraTerminal": "0",
        "totalReceivedExcludedFromSalesSaturn1000eSaturn1000l": "0",
        "totalReceivedExcludedFromSalesSmartcoin": "0",
        "totalReceivedExcludedFromSalesStarPay": "0",
        "totalReceivedExcludedFromSalesDracoin": "0",
        "totalReceivedExcludedFromSalesProductVouchers": "0",
        "totalReturned": "0",
        "totalReturnedCash": "0",
        "totalReturnedCredit": "0",
        "totalReturnedSmaregiPaymentIcReader": "0",
        "totalReturnedSmaregiPaymentVega3000": "0",
        "TotalReturnedSmaregiPaygate": "0",
        "totalReturnedPaymentMaster": "0",
        "totalReturnedPmJmups": "0",
        "totalReturnedPmThincacloud": "0",
        "totalReturnedFgCenter": "0",
        "totalReturnedRakutenPay": "0",
        "totalReturnedStoresCoiney": "0",
        "totalReturnedSquare": "0",
        "totalReturnedJetsCats300Cats330": "0",
        "totalReturnedJetsJtC17u": "0",
        "totalReturnedJmupsJtc30l": "0",
        "totalReturnedJtc31qJetsCloud": "0",
        "totalReturnedJtvt10": "0",
        "totalReturnedOtegaruPayCredit": "0",
        "totalReturnedOtegaruPayEMoney": "0",
        "totalReturnedOtegaruPayJmups2Pocket": "0",
        "totalReturnedInfoxJtc16u": "0",
        "totalReturnedVeega3000Mobile2": "0",
        "totalReturnedSteraTerminal": "0",
        "totalReturnedSaturn1000eSaturn1000l": "0",
        "totalReturnedSmartcoin": "0",
        "totalReturnedStarPay": "0",
        "totalReturnedDracoin": "0",
        "totalReturnedProductVouchers": "0",
        "totalCancelled": "0",
        "totalCancelledCash": "0",
        "totalCancelledCredit": "0",
        "totalCancelledSmaregiPaymentIcReader": "0",
        "totalCancelledSmaregiPaymentVega3000": "0",
        "TotalCancelledSmaregiPaygate": "0",
        "totalCancelledPaymentMaster": "0",
        "totalCancelledPmJmups": "0",
        "totalCancelledPmThincacloud": "0",
        "totalCancelledFgCenter": "0",
        "totalCancelledRakutenPay": "0",
        "totalCancelledStoresCoiney": "0",
        "totalCancelledSquare": "0",
        "totalCancelledJetsCats300Cats330": "0",
        "totalCancelledJetsJtC17u": "0",
        "totalCancelledJmupsJtc30l": "0",
        "totalCancelledJtc31qJetsCloud": "0",
        "totalCancelledJtvt10": "0",
        "totalCancelledOtegaruPayCredit": "0",
        "totalCancelledOtegaruPayEMoney": "0",
        "totalCancelledOtegaruPayJmups2Pocket": "0",
        "totalCancelledInfoxJtc16u": "0",
        "totalCancelledVeega3000Mobile2": "0",
        "totalCancelledSteraTerminal": "0",
        "totalCancelledSaturn1000eSaturn1000l": "0",
        "totalCancelledSmartcoin": "0",
        "totalCancelledStarPay": "0",
        "totalCancelledDracoin": "0",
        "totalCancelledProductVouchers": "0",
        "netSales": "9500",
        "netSalesPointUsedSalesIncluded": "200",
        "taxAndTotalExcludedFromSalesInTotal": "0",
        "salesTargetItemsTotalIncludeTaxIncluded": "10000",
        "salesTargetItemsTotalExcludeTaxIncluded": "9000",
        "soldItemsAmountInSales": "9500",
        "returnedItemsAmountInSales": "0",
        "totalPointUsedSales": "200",
        "totalTransactions": "50",
        "totalCustomers": "45",
        "standardTransactions": "30",
        "standardTransactionsCash": "15",
        "standardTransactionsCredit": "15",
        "standardTransactionsSmaregiPaymentIcReader": "0",
        "standardTransactionsSmaregiPaymentVega3000": "0",
        "StandardTransactionsSmaregiPaygate": "0",
        "standardTransactionsPaymentMaster": "0",
        "standardTransactionsPmJmups": "0",
        "standardTransactionsPmThincacloud": "0",
        "standardTransactionsFgCenter": "0",
        "standardTransactionsRakutenPay": "0",
        "standardTransactionsStoresCoiney": "0",
        "standardTransactionsSquare": "15",
        "standardTransactionsJetsCats300Cats330": "0",
        "standardTransactionsJetsJtC17u": "0",
        "standardTransactionsJmupsJtc30l": "0",
        "standardTransactionsJtc31qJetsCloud": "0",
        "standardTransactionsJtvt10": "0",
        "standardTransactionsOtegaruPayCredit": "0",
        "standardTransactionsOtegaruPayEMoney": "0",
        "standardTransactionsOtegaruPayJmups2Pocket": "0",
        "standardTransactionsInfoxJtc16u": "0",
        "standardTransactionsVeega3000Mobile2": "0",
        "standardTransactionsSteraTerminal": "0",
        "standardTransactionsSaturn1000eSaturn1000l": "0",
        "standardTransactionsSmartcoin": "0",
        "standardTransactionsStarPay": "0",
        "standardTransactionsDracoin": "0",
        "standardTransactionsProductVouchers": "0",
        "standardTransactionsCancelled": "0",
        "taxExemptionTransactions": "0",
        "otherTransactions": "20",
        "otherDepositTransactions": "10",
        "otherDepositCancellationTransactions": "0",
        "otherWithdrawalTransactions": "5",
        "otherWithdrawalCancellationTransactions": "0",
        "otherAdvancePaymentTransactions": "5",
        "otherAdvancePaymentCancellationTransactions": "0",
        "otherAdvancePaymentRefundedTransactions": "0",
        "otherAdvancePaymentRefundedCancellationTransactions": "0",
        "otherPointAdditionTransactions": "0",
        "otherPointAdditionCancellationTransactions": "0",
        "otherPointDeductionTransactions": "0",
        "otherPointDeductionCancellationTransactions": "0",
        "otherReservationTransactions": "0",
        "otherReservationCancellationTransactions": "0",
        "otherCouponTicketsTransactions": "0",
        "otherCouponTicketsCancellationTransactions": "0",
        "totalMoneyInAndOutAmount": "5000",
        "totalTipsCashAmount": "0",
        "totalTipsCreditAmount": "0",
        "totalTipsCashTransactions": "0",
        "totalTipsCreditTransactions": "0",
        "settlementCash10KYenBills": "2",
        "settlementCash5KYenBills": "1",
        "settlementCash2KYenBills": "0",
        "settlementCash1KYenBills": "10",
        "settlementCash500YenCoins": "0",
        "settlementCash100YenCoins": "0",
        "settlementcash50YenCoins": "0",
        "settlementCash10YenCoins": "0",
        "settlementCash5YenCoins": "0",
        "settlementCash1YenCoins": "0",
        "settlementCashChangeReserved": "100",
        "settlementCashBankDeposit": "4000",
        "settlementCashMoneyReservedForNextDay": "500",
        "settlementCashShortage": "100",
        "totalSalesExcludedFromSales": "0",
        "totalSalesExcludedFromSalesExcludeTaxIncluded": "0",
        "totalSalesExcludedFromSalesIncludeTaxIncluded": "0",
        "tax8Price": "800",
        "tax10Price": "1000",
        "tax8TargetAmount": "8000",
        "tax10TargetAmount": "10000",
        "tax8ExemptionPrice": "0",
        "tax10ExemptionPrice": "0",
        "tax8ExemptionTargetAmount": "0",
        "tax10ExemptionTargetAmount": "0",
        "departmentApparelSalesTotal": "3000",
        "departmentApparelSalesTotalExcludeTax": "2700",
        "departmentGoodsSalesTotal": "7000",
        "departmentGoodsSalesTotalExcludeTax": "6300",
        "totalSettlementCount": "50",
        "CustomField1": "string",
        "CustomField2": "string",
        "CustomField3": "string",
        "CustomField4": "string",
        "CustomField5": "string",
        "CustomField6": "string",
        "CustomField7": "string",
        "CustomField8": "string",
        "CustomField9": "string",
        "CustomField10": "string"
    },
    "ocr": {
        "status": 0,
        "createdDateTime": "2024-09-26T02:04:09.257Z",
        "analyzeResult": {
            "version": "1.0",
            "modelVersion": "2024-09",
            "readResults": [
                {
                    "page": 1,
                    "language": "en",
                    "angle": 0,
                    "width": 600,
                    "height": 800,
                    "unit": "pixel",
                    "lines": [
                        {
                            "text": "Store Name: Example Store",
                            "words": [
                                {
                                    "text": "Store",
                                    "confidence": 0.98
                                },
                                {
                                    "text": "Name:",
                                    "confidence": 0.98
                                },
                                {
                                    "text": "Example Store",
                                    "confidence": 0.99
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    },
    "subscription": {
        "subscriptionCode": "SUB123",
        "description": "OCR analysis subscription",
        "charged": 500,
        "validSince": "2024-09-25T00:00:00.000Z",
        "validUntil": "2024-12-31T23:59:59.999Z",
        "chargeResponseStatus": "Success",
        "chargeResponseMessage": "Transaction complete"
    }
}
```

### Error Response Examples

#### Image not found
```json
{
  "error": "Image not found",
  "status": 404
}
```

#### Unable to recognize receipt from image
```json
{
  "error": "Unable to process receipt from image",
  "status": 422
}
```

#### Subscription not active
```json
{
  "error": "Subscription not active",
  "status": 403
}
```

#### Server error
```json
{
  "error": "An unexpected server issue occurred",
  "status": 500
}
```

