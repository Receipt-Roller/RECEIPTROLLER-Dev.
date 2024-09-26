# レシートデータの管理

レシートデータ管理では、取引に関する詳細情報を収集し、保存します。これには、顧客情報、支払い方法、購入商品の詳細、適用された割引や税金、スタッフの情報などが含まれます。また、メンバーシッププログラムやクーポンの適用履歴、サブスクリプション情報も管理します。これにより、店舗の売上データを効率的に整理し、顧客ごとの購入履歴や支払情報の追跡が可能になります。レシートには印刷用のカスタマイズ可能な情報を含めることもできます。

# レシートデータ型

| フィールド名                      | 型            | 説明                                  |
|-----------------------------------|---------------|---------------------------------------|
| organizationId                    | string        | 組織のID                              |
| receiptId                         | string        | レシートID                            |
| transactionType                   | int           | 取引タイプ (例: 1=購入, 2=返品)         |
| cancelType                        | int           | キャンセルタイプ                       |
| terminalTransactionId             | string        | 端末取引ID                            |
| terminalTransactionDateTime       | string (ISO8601) | 端末取引日時                        |
| timestamp                         | string (ISO8601) | レシートの作成タイムスタンプ         |
| channelId                         | string        | チャネルID                            |
| terminalId                        | string        | 端末ID                                |
| customer.customerId               | string        | 顧客ID                                |
| customer.customerName             | string        | 顧客の名前                            |
| customer.customerPrintName        | string        | 顧客印刷用の名前                      |
| customer.customerGroup            | string        | 顧客グループ                          |
| customer.customerCode             | string        | 顧客コード                            |
| customer.customerMemo             | string        | 顧客メモ                              |
| customer.destinationEmail         | string        | 顧客のEメール                         |
| customer.destinationSms           | string        | 顧客のSMS番号                         |
| customer.destinationLineMid       | string        | 顧客のLINE MID                        |
| roundingPosition                  | int           | 丸めの位置                            |
| roundingMethod                    | int           | 丸めの方法                            |
| memo                              | string        | レシートメモ                          |
| tags                              | string        | レシートに付けられたタグ              |
| barcode                           | string        | バーコード                            |
| themeId                           | string        | テーマID                              |
| store.storeId                     | string        | 店舗ID                                |
| store.storeCode                   | string        | 店舗コード                            |
| store.storeName                   | string        | 店舗名                                |
| store.storePrintName              | string        | 店舗印刷用の名前                      |
| store.storeAddress                | string        | 店舗の住所                            |
| store.storePrintAddress           | string        | 店舗印刷用の住所                      |
| store.storeRegisgrationName       | string        | 店舗登録名                            |
| store.storeRegisgrationCode       | string        | 店舗登録コード                        |
| store.storeTel                    | string        | 店舗電話番号                          |
| store.storeMemo                   | string        | 店舗メモ                              |
| staff.staffId                     | string        | スタッフID                            |
| staff.staffCode                   | string        | スタッフコード                        |
| staff.staffName                   | string        | スタッフ名                            |

## 支払い情報

| フィールド名                      | 型            | 説明                                  |
|-----------------------------------|---------------|---------------------------------------|
| paymentSummary.shippingFee        | int           | 配送料                                |
| paymentSummary.serviceFee         | int           | サービス料                            |
| paymentSummary.otherFee           | int           | その他の料金                          |
| paymentSummary.grandTotal         | int           | 合計金額                              |
| paymentSummary.depositMethod      | int           | 預金方法                              |
| paymentSummary.deposit            | int           | 預金額                                |
| paymentSummary.change             | int           | 釣銭                                  |
| paymentSummary.subTotal           | int           | 小計                                  |
| paymentSummary.subTotalDiscountAmount | int       | 小計割引額                            |
| paymentSummary.subTotalDiscountRate | float      | 小計割引率                            |
| paymentSummary.subtotalDiscountPrice | int       | 割引後小計                            |
| paymentSummary.taxes              | array         | 税金の詳細                            |

### 税金の詳細

| フィールド名                      | 型            | 説明                                  |
|-----------------------------------|---------------|---------------------------------------|
| taxes.taxIfInclude                | int           | 税込み額                              |
| taxes.taxIfExclude                | int           | 税抜き額                              |
| taxes.taxPercentageIfInclude      | int           | 税率（込み）                          |
| taxes.taxPercentageIfExclude      | int           | 税率（抜き）                          |
| taxes.applicableSubTotalAmount    | int           | 適用された小計金額                    |

## 商品情報 (itemDetailLines)

| フィールド名                      | 型            | 説明                                  |
|-----------------------------------|---------------|---------------------------------------|
| itemDetailLines.lineId            | string        | 行ID                                  |
| itemDetailLines.itemId            | string        | 商品ID                                |
| itemDetailLines.itemType          | int           | 商品タイプ                            |
| itemDetailLines.salesType         | int           | 販売タイプ                            |
| itemDetailLines.productId         | string        | 商品コード                            |
| itemDetailLines.productCode       | string        | 商品コード                            |
| itemDetailLines.productName       | string        | 商品名                                |
| itemDetailLines.taxCategory       | int           | 税カテゴリ                            |
| itemDetailLines.price             | int           | 価格                                  |
| itemDetailLines.salesPrice        | int           | 販売価格                              |
| itemDetailLines.quantity          | int           | 数量                                  |
| itemDetailLines.taxDivision       | string        | 税区分                                |
| itemDetailLines.taxFreeDivision   | int           | 非課税区分                            |
| itemDetailLines.taxFreeAmount     | int           | 非課税額                              |
| itemDetailLines.categoryId        | string        | カテゴリID                            |
| itemDetailLines.categoryName      | string        | カテゴリ名                            |
| itemDetailLines.taxRate           | string        | 税率                                  |
| itemDetailLines.unitNonDiscountSum| int           | 割引前合計                            |
| itemDetailLines.bargainName       | string        | 特価名                                |
| itemDetailLines.bargainDiscountProportional | int | 割引率                                |
| itemDetailLines.taxIncludeProportional | int    | 税込み割引率                          |
| itemDetailLines.taxExcludeProportional | int    | 税抜き割引率                          |
| itemDetailLines.unitDiscountSum   | int           | 割引後合計                            |
| itemDetailLines.unitDiscountName  | string        | 割引名                                |
| itemDetailLines.discountPriceProportional | int   | 割引額                                |
| itemDetailLines.discountCouponProportional | int  | クーポン割引                          |
| itemDetailLines.couponDiscount    | int           | クーポン割引額                        |
| itemDetailLines.taxes             | array         | 税金情報                              |

## サブスクリプション

| フィールド名                      | 型            | 説明                                  |
|-----------------------------------|---------------|---------------------------------------|
| subscriptions.lineId              | string        | 行ID                                  |
| subscriptions.subscriptionCode    | string        | サブスクリプションコード               |
| subscriptions.description         | string        | サブスクリプション説明                 |
| subscriptions.charged             | int           | 請求金額                              |
| subscriptions.unitInCharge        | string        | 請求単位                              |
| subscriptions.validSince          | string (ISO8601) | 有効期間の開始                      |
| subscriptions.validUntil          | string (ISO8601) | 有効期間の終了                      |
| subscriptions.paymentMethod       | string        | 支払い方法                            |
| subscriptions.memo                | string        | メモ                                  |
| subscriptions.maxCall             | int           | 最大コール数                          |
| subscriptions.called              | int           | コール済み数                          |
| subscriptions.chargedBy           | string        | 請求元                                |
| subscriptions.isExipred           | boolean       | 有効期限が切れているかどうか           |
| subscriptions.exipireHandled      | string (ISO8601) | 有効期限処理日                      |
| subscriptions.chargeResponseStatus| string        | 請求ステータス                        |
| subscriptions.chargeResponseMessage| string       | 請求メッセージ                        |



# レシートデータの取得 (`/{organizationId}/receipts`)



## リクエスト

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/{organizationId}/receipts' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
    "storeId": "1234-store-5678",
    "terminalId": "tm-001",
    "keyword": "レシート検索",
    "sort": "transactionId asc",
    "currentPage": 1,
    "itemsPerPage": 10,
    "year": 2024,
    "month": 9
}'
```

- **storeId**: 店舗ID
- **terminalId**: 端末ID
- **keyword**: 検索キーワード
- **sort**: 並び順（`transactionId asc` または `transactionId desc`）
- **currentPage**: 現在のページ（ページネーション）
- **itemsPerPage**: ページごとのアイテム数。上限は1000件です。
- **year**: 検索対象の年
- **month**: 検索対象の月

## レスポンス

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
          "customerName": "山田 太郎",
          "customerPrintName": "ヤマダ タロウ",
          "customerGroup": "VIP",
          "customerCode": "C123456",
          "customerMemo": "特記事項なし",
          "destinationEmail": "example@email.com",
          "destinationSms": "090-1234-5678",
          "destinationLineMid": "line-id-001",
          "membershipPrograms": [
            {
              "membershipProgramName": "ゴールドメンバー",
              "membershipProgramPointsUsed": "100",
              "membershipProgramPointsAdded": "50",
              "membershipProgramPointsAfter": "150",
              "membershipProgramPointsBefore": "100",
              "membershipProgramPointsNote": "キャンペーン加算"
            }
          ]
        },
        "roundingPosition": 2,
        "roundingMethod": 1,
        "memo": "レシートメモ内容",
        "tags": "セール,特典",
        "barcode": "BRC123456",
        "themeId": "theme-001",
        "store": {
          "storeId": "1234-store-5678",
          "storeCode": "S001",
          "storeName": "渋谷ストア",
          "storePrintName": "渋谷店",
          "storeAddress": "東京都渋谷区道玄坂1-2-3",
          "storePrintAddress": "渋谷区道玄坂1-2-3",
          "storeRegisgrationName": "渋谷ストア有限会社",
          "storeRegisgrationCode": "RG123456",
          "storeTel": "03-1234-5678",
          "storeMemo": "店舗メモ"
        },
        "staff": {
          "staffId": "stf-001",
          "staffCode": "S001",
          "staffName": "鈴木 一郎"
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
          "couponName": "10%オフクーポン",
          "couponPointsUsed": 100,
          "couponPointsAdded": 50,
          "couponPointsAfter": 150,
          "couponPointsBefore": 100,
          "couponNote": "クーポン適用"
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
          "productName": "商品A",
          "taxCategory": 1,
          "price": 1000,
          "salesPrice": 900,
          "quantity": 1,
          "taxDivision": "内税",
          "taxFreeDivision": 0,
          "taxFreeAmount": 0,
          "categoryId": "cat-001",
          "categoryName": "食品",
          "taxRate": "8%",
          "unitNonDiscountSum": "1000",
          "bargainName": "特価",
          "bargainDiscountProportional": "100",
          "taxIncludeProportional": "80",
          "taxExcludeProportional": "70",
          "unitDiscountSum": "900",
          "unitDiscountName": "割引",
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
          "description": "サブスクリプションA",
          "charged": 1500,
          "unitInCharge": "円",
          "validSince": "2024-09-26T01:24:01.437Z",
          "validUntil": "2024-12-26T01:24:01.437Z",
          "paymentMethod": "クレジットカード",
          "memo": "サブスクリプションメモ",
          "maxCall": 10,
          "called": 2,
          "chargedBy": "サービスA",
          "isExipred": false,
          "exipireHandled": "2024-09-26T01:24:01.437Z",
          "chargeResponseStatus": "success",
          "chargeResponseMessage": "成功"
        }
      ]
    }
  ],
  "currentPage": 1,
  "itemsPerPage": 10,
  "totalItems": 1,
  "totalPages": 1,
  "keyword": "レシート検索",
  "sort": "transactionId asc"
}
```

## エラーレスポンス

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

- **404 Not Found**: 指定されたレシートが見つからない場合
  ```json
  {
    "error": "Receipt not found"
  }
  ```
---
# レシート詳細の取得 (`/{organizationId}/{yyyyMM}/{storeId}/receipt/{id}`)

## リクエスト

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/{organizationId}/{yyyyMM}/{storeId}/receipt/{id}' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}'
```

## レスポンス

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
      "customerName": "山田 太郎",
      "customerPrintName": "ヤマダ タロウ",
      "customerGroup": "VIP",
      "customerCode": "C123456",
      "customerMemo": "特記事項なし",
      "destinationEmail": "example@email.com",
      "destinationSms": "090-1234-5678",
      "destinationLineMid": "line-id-001",
      "membershipPrograms": [
        {
          "membershipProgramName": "ゴールドメンバー",
          "membershipProgramPointsUsed": "100",
          "membershipProgramPointsAdded": "50",
          "membershipProgramPointsAfter": "150",
          "membershipProgramPointsBefore": "100",
          "membershipProgramPointsNote": "キャンペーン加算"
        }
      ]
    },
    "roundingPosition": 2,
    "roundingMethod": 1,
    "memo": "レシートメモ内容",
    "tags": "セール,特典",
    "barcode": "BRC123456",
    "themeId": "theme-001",
    "store": {
      "storeId": "1234-store-5678",
      "storeCode": "S001",
      "storeName": "渋谷ストア",
      "storePrintName": "渋谷店",
      "storeAddress": "東京都渋谷区道玄坂1-2-3",
      "storePrintAddress": "渋谷区道玄坂1-2-3",
      "storeRegisgrationName": "渋谷ストア有限会社",
      "storeRegisgrationCode": "RG123456",
      "storeTel": "03-1234-5678",
      "storeMemo": "店舗メモ"
    },
    "staff": {
      "staffId": "stf-001",
      "staffCode": "S001",
      "staffName": "鈴木 一郎"
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
      "couponName": "10%オフクーポン",
      "couponPointsUsed": 100,
      "couponPointsAdded": 50,
      "couponPointsAfter": 150,
      "couponPointsBefore": 100,
      "couponNote": "クーポン適用"
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
      "productName": "商品A",
      "taxCategory": 1,
      "price": 1000,
      "salesPrice": 900,
      "quantity": 1,
      "taxDivision": "内税",
      "taxFreeDivision": 0,
      "taxFreeAmount": 0,
      "categoryId": "cat-001",
      "categoryName": "食品",
      "taxRate": "8%",
      "unitNonDiscountSum": "1000",
      "bargainName": "特価",
      "bargainDiscountProportional": "100",
      "taxIncludeProportional": "80",
      "taxExcludeProportional": "70",
      "unitDiscountSum": "900",
      "unitDiscountName": "割引",
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
      "description": "サブスクリプションA",
      "charged": 1500,
      "unitInCharge": "円",
      "validSince": "2024-09-26T01:28:18.815Z",
      "validUntil": "2024-12-26T01:28:18.815Z",
      "paymentMethod": "クレジットカード",
      "memo": "サブスクリプションメモ",
      "maxCall": 10,
      "called": 2,
      "chargedBy": "サービスA",
      "isExipred": false,
      "exipireHandled": "2024-09-26T01:28:18.815Z",
      "chargeResponseStatus": "success",
      "chargeResponseMessage": "成功"
    }
  ]
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

- **404 Not Found**: 指定されたレシートが見つからない場合
  ```json
  {
    "error": "Receipt not found"
  }
  ```

---

# レシートの作成 (`/{organizationId}/receipt/create`)

## リクエスト

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
      "staffName": "鈴木 一郎"
    },
    "coupon": [
      {
        "couponName": "10%オフ",
        "couponPointsUsed": 100,
        "couponPointsAdded": 50,
        "couponPointsAfter": 150,
        "couponPointsBefore": 100,
        "couponNote": "クーポン適用"
      }
    ],
    "customer": {
      "customerId": "cust-001",
      "customerName": "山田 太郎",
      "customerPrintName": "ヤマダ タロウ",
      "customerGroup": "VIP",
      "customerCode": "C123456",
      "customerMemo": "特記事項なし",
      "destinationEmail": "example@email.com",
      "destinationSms": "090-1234-5678",
      "destinationLineMid": "line-id-001",
      "membershipPrograms": [
        {
          "membershipProgramName": "ゴールドメンバー",
          "membershipProgramPointsUsed": "100",
          "membershipProgramPointsAdded": "50",
          "membershipProgramPointsAfter": "150",
          "membershipProgramPointsBefore": "100",
          "membershipProgramPointsNote": "キャンペーン加算"
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
        "productName": "商品A",
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
    "memo": "レシートメモ",
    "tags": "セール,特典",
    "barcode": "BRC123456",
    "themeId": "theme-001",
    "currency": "JPY"
}'
```

### 注意事項

- **storeId**、**staffId**、**customerId** については検証が行われません。
- **terminalId** は検証され、実在の端末IDである必要があります。
- **terminalTransactionId** のユニーク性は検証されません。
- **roundingMethod**: 
  - `0`: 切り捨て
  - `1`: 四捨五入 (0.5 以上を切り上げ)
  - `2`: 切り上げ
- **tags** はカンマ区切りです。
- **themeId** が一致しない場合、デフォルトのテーマが適用されます。

## レスポンス

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
      "customerName": "山田 太郎",
      "customerPrintName": "ヤマダ タロウ",
      "customerGroup": "VIP",
      "customerCode": "C123456",
      "customerMemo": "特記事項なし",
      "destinationEmail": "example@email.com",
      "destinationSms": "090-1234-5678",
      "destinationLineMid": "line-id-001",
      "membershipPrograms": [
        {
          "membershipProgramName": "ゴールドメンバー",
          "membershipProgramPointsUsed": "100",
          "membershipProgramPointsAdded": "50",
          "membershipProgramPointsAfter": "150",
          "membershipProgramPointsBefore": "100",
          "membershipProgramPointsNote": "キャンペーン加算"
        }
      ]
    },
    "roundingPosition": 0,
    "roundingMethod": 0,
    "memo": "レシートメモ",
    "tags": "セール, 特典",
    "barcode": "BRC123456",
    "themeId": "theme-001",
    "store": {
      "storeId": "1234-store-5678",
      "storeCode": "S001",
      "storeName": "渋谷ストア",
      "storePrintName": "渋谷店",
      "storeAddress": "東京都渋谷区道玄坂1-2-3",
      "storePrintAddress": "渋谷区道玄坂1-2-3",
      "storeRegisgrationName": "渋谷ストア有限会社",
      "storeRegisgrationCode": "RG123456",
      "storeTel": "03-1234-5678",
      "storeMemo": "店舗メモ"
    },
    "staff": {
      "staffId": "stf-001",
      "staffCode": "S001",
      "staffName": "鈴木 一郎"
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
      "couponName": "10%オフ",
      "couponPointsUsed": 100,
      "couponPointsAdded": 50,
      "couponPointsAfter": 150,
      "couponPointsBefore": 100,
      "couponNote": "クーポン適用"
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
      "productName": "商品A",
      "taxCategory": 1,
      "price": 1000,
      "salesPrice": 900,
      "quantity": 1,
      "taxDivision": "内税",
      "taxFreeDivision": 0,
      "taxFreeAmount": 0,
      "categoryId": "cat-001",
      "categoryName": "食品",
      "taxRate": "8%",
      "unitNonDiscountSum": "1000",
      "bargainName": "特価",
      "bargainDiscountProportional": "100",
      "taxIncludeProportional": "80",
      "taxExcludeProportional": "70",
      "unitDiscountSum": "900",
      "unitDiscountName": "割引",
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
      "description": "サブスクリプションA",
      "charged": 1500,
      "unitInCharge": "円",
      "validSince": "2024-09-26T01:31:10.199Z",
      "validUntil": "2024-12-26T01:31:10.199Z",
      "paymentMethod": "クレジットカード",
      "memo": "サブスクリプションメモ",
      "maxCall": 10,
      "called": 2,
      "chargedBy": "サービスA",
      "isExipred": false,
      "exipireHandled": "2024-09-26T01:31:10.199Z",
      "chargeResponseStatus": "success",
      "chargeResponseMessage": "成功"
    }
  ]
}
```

--- 

# レシートデータのOCR分析 (`/{organizationId}/receipt/read`)

このエンドポイントは、指定したURLの画像からOCRでレシートデータを読み取り、レシート情報を返します。

## リクエスト

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

### 注意事項

- 指定されたURLの画像からOCRによるレシートデータ解析を行います。
- OCRの結果、レシートとして認識できない場合や画像が存在しない場合はエラーになります。
- サブスクリプションが無効な場合もエラーが返されます。

## レスポンス

OCRの成功時には、レスポンスはレシートの作成と同じ形式です（詳しくは `/receipt/create` のレスポンスを参照）。

### エラーレスポンス例

- **404 Not Found**: 画像が存在しない、または読めない場合
  ```json
  {
    "error": "Image not found or unreadable"
  }
  ```

- **400 Bad Request**: レシートとして認識できない場合
  ```json
  {
    "error": "Unable to recognize receipt from image"
  }
  ```

- **403 Forbidden**: サブスクリプションが無効な場合
  ```json
  {
    "error": "Subscription is not active"
  }
  ```

---

# Base64画像のOCR分析 (`/{organizationId}/receipt/upload-read`)

このエンドポイントは、Base64エンコードされた画像をOCR分析し、レシートデータとして返します。

## リクエスト

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

### 注意事項

- `imageInBase64String` フィールドにBase64でエンコードされた画像データを渡します。
- OCRによるレシートデータの解析を行い、解析結果を返します。

## レスポンス

OCR分析に成功すると、レスポンスはレシート作成時のレスポンスと同じ形式です（詳しくは `/receipt/create` のレスポンスを参照）。

### エラーレスポンス例

- **400 Bad Request**: 画像が不正、または解析できない場合
  ```json
  {
    "error": "Invalid or unreadable image data"
  }
  ```

- **403 Forbidden**: サブスクリプションが無効な場合
  ```json
  {
    "error": "Subscription is not active"
  }
  ```


--- 

# Base64画像の精算レシートOCR分析 (`/{organizationId}/receipt/store/{storeId}/readtype/{readType}/upload-read`)

このエンドポイントは、Base64エンコードされた精算レシート画像をOCRで解析し、レシートデータを返します。

## リクエスト

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

### 注意事項

- `imageInBase64String` フィールドにBase64でエンコードされたレシート画像データを渡します。
- OCRによる決済レシートデータの解析を行い、解析結果を返します。

## レスポンス

**注意事項**: 読み取れなかった項目や存在しない項目については、レスポンスに含まれません。返却されるフィールドは、解析結果に基づいて取得できた情報のみです。


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
        "lastUpdatedDateTime": "2024-09-26T02:10:09.257Z",
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
                            "language": "en",
                            "boundingBox": [
                                0,
                                0,
                                600,
                                50
                            ],
                            "appearance": {
                                "style": {
                                    "name": "bold",
                                    "confidence": 0.99
                                }
                            },
                            "text": "Store Name: Example Store",
                            "words": [
                                {
                                    "boundingBox": [
                                        0,
                                        0,
                                        300,
                                        50
                                    ],
                                    "text": "Store",
                                    "confidence": 0.98
                                },
                                {
                                    "boundingBox": [
                                        300,
                                        0,
                                        600,
                                        50
                                    ],
                                    "text": "Name:",
                                    "confidence": 0.98
                                },
                                {
                                    "boundingBox": [
                                        0,
                                        50,
                                        600,
                                        100
                                    ],
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
    "ocrLines": [
        {
            "lineOrder": 1,
            "lineText": "Store Name: Example Store",
            "words": [
                {
                    "handWriteingText": "Store Name:",
                    "topLeftX": 0,
                    "topLeftY": 0,
                    "text": "Store Name: Example Store"
                }
            ]
        }
    ],
    "subscription": {
        "partitionKey": "org123",
        "rowKey": "sub456",
        "timestamp": "2024-09-26T02:04:09.257Z",
        "eTag": {},
        "subscriptionCode": "SUB123",
        "description": "OCR analysis subscription",
        "priceCurrency": "JPY",
        "charged": 500,
        "chargedPrice": "500",
        "chargedQuality": 1,
        "unitPrice": "500",
        "validSince": "2024-09-25T00:00:00.000Z",
        "validSinceEpoch": 1695692400,
        "validUntil": "2024-12-31T23:59:59.999Z",
        "validUntilEpoch": 1704076799,
        "paymentMethod": "CreditCard",
        "memo": "OCR analysis for receipts",
        "maxCall": 1000,
        "called": 300,
        "chargedBy": "Automatic Billing",
        "isExpired": false,
        "expireHandled": "2024-12-31T23:59:59.999Z",
        "chargeResponseStatus": "Success",
        "chargeResponseMessage": "Transaction complete"
    }
}
```

### エラーレスポンス例

#### 画像が存在しない場合
```json
{
  "error": "Image not found",
  "status": 404
}
```
#### OCRでレシートとして認識できなかった場合
```json
{
 "error": "Unable to process receipt from image",
  "status": 422
}
```
#### サブスクリプションが有効でない場合
```json
{
  "error": "Subscription not active",
  "status": 403
}
```
#### サーバー処理に失敗した場合
```json
{
  "error": "An unexpected server issue occurred",
  "status": 500
}
```
