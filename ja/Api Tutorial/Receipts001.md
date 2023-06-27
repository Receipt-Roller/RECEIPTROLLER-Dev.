レシートローラーAPIでレシートの作成または取得する方法をご紹介します。

APIのSwaggerドキュメントは下記をご参照ください。
https://api.receiptroller.com/index.html

# レシートの作成

## レシート作成時のリクエスト

レシート作成時は下記の値をポストしてください。
ポスト先は　`/{organizationId}/receipt/upsert`  になります。 

```
{
  "transactionType": 0,
  "cancelType": "string",
  "terminalTransactionId": "string",
  "terminalTransactionDateTime": "2023-06-26T14:32:01.101Z",
  "storeId": "string",
  "terminalId": "string",
  "staffId": "string",
  "customerId": "string",
  "customerCode": "string",
  "customerGroup": "string",
  "timeOfEnter": "2023-06-26T14:32:01.101Z",
  "numberOfParty": 0,
  "customerMemo": "string",
  "items": [
    {
      "itemId": "string",
      "itemTypes": 0,
      "salesTypes": 0,
      "productId": "string",
      "productCode": "string",
      "productName": "string",
      "salesPrice": 0,
      "qt": 0
    }
  ],
  "subTotal": 0,
  "subTotalDiscountAmount": 0,
  "subTotalDiscountRate": 0,
  "nameOfPoint": "string",
  "pointsUsed": 0,
  "pointsAdded": 0,
  "totalPointsAfetr": 0,
  "totalPointsBefore": 0,
  "pointAs": 0,
  "nameOfMile": "string",
  "milesUsed": 0,
  "milesAdded": 0,
  "milesPointsAfetr": 0,
  "milesPointsBefore": 0,
  "milesNote": "string",
  "taxPercentageIfInclude": 0,
  "taxPercentageIfExclude": 0,
  "roundingPosition": 0,
  "roundingMethod": 0,
  "shippingFee": 0,
  "serviceFee": 0,
  "otherFee": 0,
  "grandTotal": 0,
  "despoitMethod": 0,
  "deposit": 0,
  "change": 0,
  "isClosed": true,
  "closingDate": "2023-06-26T14:32:01.101Z",
  "memo": "string",
  "tags": "string",
  "barcode": "string",
  "themeId": "string"
}
```
各項目は下記の通りです。

|名前|タイプ|必須|備考|
|:--|:--|:--|:--|
|transactionType|数値|必須|0=通常販売　現在指定できるのは0のみとなっています。|
|cancelType|数値||0=通常キャンセル　現在指定できるのは0のみとなっています。|
|terminalTransactionId|文字列|必須|POS端末にて生成された取引Id|
|terminalTransactionDateTime|文字列|必須|POS端末にて生成された取引時刻 yyyy-MM-dd HH:mm:ss.fff zzz |
|storeId|文字列|必須|レシートローラーに登録されている店舗Id|
|terminalId|文字列|必須|レシートローラーに登録されている端末Id|
|staffId|文字列|必須|POS端末に登録されているスタッフId|
|customerId|文字列||レシートローラーに登録されている仮顧客Id|
|customerCode|文字列||POS端末に登録されている顧客Id|
|customerGroup|文字列||POS端末に登録されている顧客グループId|
|timeOfEnter|文字列||POS端末に登録されている来店時刻|
|numberOfParty|数値||POS端末に登録されている来店人数|
|customerMemo|文字列||顧客メモ|
|items|オブジェクト||購入アイテムの配列|
|subTotal|数値|必須|小数点2桁まで指定可能、`items`が空指定の時のみ有効、指定されている場合は自動計算された値が上書きされます。|
|subTotalDiscounmtAmount|数値||小数点2桁まで指定可能、小計に対しての割引金額|
|subTotalDiscounmtRate|数値||小数点2桁まで指定可能、10%オフの場合は0.1を指定、50%オフの場合は0.5を指定、掛ける数字を指定してください。`subTotalDiscountAmount`が指定されている場合は`subTotalDiscountAmount`が優先されます。|
|nameOfPoint|文字列||店舗で利用されているポイントプログラムの名称|
|pointUsed|数値||利用されたポイント数|
|pointAdded|数値||付与されたポイント数|
|totalPointAfter|数値||決済後のポイント合計値|
|totalPointBefore|数値||決済前のポイント合計値|
|taxPercentageIfInclude|数値||税率（内税の場合）|
|taxPercentageIfExclude|数値||税率（外税の場合）|
|roundingPosition|数値||指定した小数点位置|
|roundingMethod|数値||0=捨て、1=四捨五入、2=切り上げ、3=切り捨て|
|shippingFee|数値||配送費|
|serviceFee|数値||サービス費|
|otherFee|数値||その他手数料|
|grandTotal|数値|必須|合計値|
|depositiMethod|数値||支払い方法、1=現金、2=その他|
|depositi|数値||預かり金額|
|change|数値||おつり|
|closed|真偽値||対象のトランザクションが締め済みかどうか|
|closingDate|文字列||締め時刻|
|memo|文字列||備考|
|tags|文字列||コンマで区切られたタグ文字列|
|barcode|文字列||バーコード文字列|
|themeId|文字列|必須|対象テーマId|

/ items

|名前|タイプ|必須|備考|
|:--|:--|:--|:--|
|itemId|文字列||レシートローラーによって付与されるLineId|
|itemTypes|数値||商品タイプ、任意の数値|
|salesTypes|数値||0=売上、現在は0のみ入力可能|
|productId|文字列||商品Id|
|productCode|文字列||商品コード|
|productName|文字列||商品名|
|salesPrice|数値||販売価格|
|qt|数値||個数|

## レシート作成時のレスポンス

レシート作成リクエストが正常に行われると下記のフォーマットでJsonデータが戻されます。

```
{
  "receipt": {
    "rowKey": "string",
    "partitionKey": "string",
    "organizationId": "string",
    "transactionType": 0,
    "cancelType": 0,
    "terminalTransactionId": "string",
    "terminalTransactionDateTime": "2023-06-26T14:33:27.871Z",
    "timestamp": "2023-06-26T14:33:27.871Z",
    "eTag": {},
    "channelId": "string",
    "itemListJsonString": "string",
    "storeId": "string",
    "storePrintName": "string",
    "storePrintAddress": "string",
    "terminalId": "string",
    "staffId": "string",
    "staffPrintName": "string",
    "customerId": "string",
    "destinationEmail": "string",
    "destinationSms": "string",
    "destinationLineMid": "string",
    "customerCode": "string",
    "customerGroup": "string",
    "customerPrintName": "string",
    "timeOfEnter": "2023-06-26T14:33:27.871Z",
    "numberOfParty": 0,
    "customerMemo": "string",
    "subTotal": 0,
    "subTotalDiscountAmount": 0,
    "subTotalDiscountRate": 0,
    "subtotalDiscountPrice": "string",
    "nameOfPoint": "string",
    "pointsUsed": 0,
    "pointsAdded": 0,
    "totalPointsAfetr": 0,
    "totalPointsBefore": 0,
    "pointAs": 0,
    "nameOfMile": "string",
    "milesUsed": 0,
    "milesAdded": 0,
    "milesPointsAfter": 0,
    "milesPointsBefore": 0,
    "milesNote": "string",
    "taxPercentageIfInclude": 0,
    "taxIfInclude": 0,
    "taxInclude": "string",
    "taxExclude": "string",
    "taxPercentageIfExclude": 0,
    "roundingPosition": 0,
    "roundingMethod": 0,
    "shippingFee": "string",
    "serviceFee": "string",
    "otherFee": "string",
    "grandTotal": 0,
    "depositMethod": 0,
    "deposit": 0,
    "depositCash": 0,
    "depositCredit": 0,
    "change": 0,
    "isClosed": true,
    "closingDate": "2023-06-26T14:33:27.871Z",
    "memo": "string",
    "tags": "string",
    "barcode": "string",
    "themeId": "string",
    "senderLogJsonString": "string",
    "ocrText": "string",
    "ocrResult": "string",
    "receiptStatus": "string",
    "expenseCategory": "string",
    "readAndApproved": "2023-06-26T14:33:27.871Z",
    "isReadable": true,
    "imageLocation": "string",
    "storeTel": "string",
    "storeAddressPrint": "string",
    "storeCode": "string",
    "transactionId": "string",
    "amount": 0,
    "inTaxSalesTotal": "string",
    "outTaxSalesTotal": "string",
    "nonTaxSalesTotal": "string",
    "couponDiscount": "string",
    "smaregiTransactionJson": "string"
  },
  "receiptItems": [
    {
      "rowKey": "string",
      "partitionKey": "string",
      "detailId": "string",
      "detailType": 0,
      "salesType": 0,
      "timestamp": "2023-06-26T14:33:27.871Z",
      "eTag": {},
      "productId": "string",
      "productCode": "string",
      "productName": "string",
      "taxCategory": 0,
      "price": 0,
      "salesPrice": 0,
      "quantity": 0,
      "taxDivision": "string",
      "taxFreeDivision": 0,
      "taxFreeAmount": 0,
      "cateogyrId": "string",
      "categoryName": "string",
      "productBundleGroupId": "string",
      "printReceiptProductName": "string",
      "taxRate": "string",
      "unitNonDiscountSum": "string",
      "bargainName": "string",
      "bargainDiscountProportional": "string",
      "taxIncludeProportional": "string",
      "taxExcludeProportional": "string",
      "unitDiscountSum": "string",
      "unitDiscountName": "string"
    }
  ],
  "subscription": {
    "rowKey": "string",
    "partitionKey": "string",
    "timestamp": "2023-06-26T14:33:27.871Z",
    "eTag": {},
    "subscriptionCode": "string",
    "description": "string",
    "charged": 0,
    "unitInCharge": "string",
    "validSince": "2023-06-26T14:33:27.871Z",
    "validSinceEpoch": 0,
    "validUntil": "2023-06-26T14:33:27.871Z",
    "validUntilEpoch": 0,
    "paymentMethod": "string",
    "memo": "string",
    "maxCall": 0,
    "called": 0,
    "chargedBy": "string",
    "isExipred": true,
    "exipireHandled": "2023-06-26T14:33:27.871Z",
    "chargeResponseStatus": "string",
    "chargeResponseMessage": "string"
  }
}
```

|名前|タイプ|備考|
|:--|:--|:--|
|rowKey|文字列|レシートId|
|partitionKey|文字列|レシートサブId|
|transactionType|数値|取引タイプ、0=通常販売　現在指は0のみとなっています。|
|cancelType|数値|0=通常キャンセル　現在は0のみとなっています。|
|terminalTransactionId|文字列|POS端末にて生成された取引Id|
|terminalTransactionDateTime|文字列|POS端末にて生成された取引時刻 yyyy-MM-dd HH:mm:ss.fff zzz|
|storeId|文字列|店舗Id|
|terminalId|文字列|端末Id|
|customerId|文字列|顧客Id|
|customerCode|文字列|顧客コード|
|customerGroup|文字列|顧客グループId|
|timeOfEnter|文字列|来店時刻|
|numberOfParty|数値|来店人数|
|customerMemo|文字列|顧客メモ|
|subTotal|数値|小計|
|subTotalDiscountAmount|数値|値引き前小計|
|subTotalDiscountRate|数値|値引き率|
|nameOfPoint|文字列|ポイント名|
|pointsUsed|数値|利用されたポイント値|
|pointsAdded|数値|付与されたポイント値|
|totalPointsAfetr|数値|決済前のポイント合計値|
|totalPointsBefore|数値|決済後のポイント合計値|
|taxPercentageIfInclude|数値|税率（内税の場合）|
|taxPercentageIfExclude|数値|税率（外税の場合）|
|roundingPosition|数値|指定した小数点位置|
|roundingMethod|数値|0=捨て、1=四捨五入、2=切り上げ、3=切り捨て|
|shippingFee|数値|配送費|
|serviceFee|数値|サービス費|
|otherFee|数値|その他手数料|
|grandTotal|数値|合計|
|despoitMethod|数値|支払い方法、1=現金、2=その他|
|deposit|数値|預かり金額|
|change|数値|おつり|
|isClosed|真偽値|締めたか否か|
|memo|文字列|備考|
|tags|文字列|タグ|
|barcode|文字列|バーコード|
|themeId|文字列|テーマId|
|senderLogJsonString|文字列|購入者への送信ログ|
|ocrText|文字列|OCRで読み込んだテキスト|
|ocrResult|文字列|OCRで読み込んだテキストの詳細|
|receiptStatus|文字列|レシートのステータス|
|expenceCategory|文字列|経費項目|
|readAndApproved|文字列|経費精算承認プロセスステータス|
|isReadable|真偽値|読込可能・不可能のフラグ|
|imageLocation|文字列|読込レシート保存場所|
|storeTel|文字列|店舗電話番号|
|storeAddressPrint|文字列|表示用店舗住所|
|storeCode|文字列|店舗コード|
|transactionId|文字列|レシートId|
|inTaxSalesTotal|数値|内税合計|
|outTaxSalesTotal|数値|外税合計|
|nonTaxSalesTotal|数値|免税対象合計|
|couponDiscount|数値|クーポン値引き|
|smaregiTransactionJson|文字列|スマレジ取引データ|
|receiptItems|オブジェクト|購入アイテム詳細|
|subscription|オブジェクト|対象サブスクリプション情報|

/receiptItems

|名前|タイプ|備考|
|:--|:--|:--|
|rowKey|文字列|購入ラインId|
|partitionKey|文字列|レシートId|
|detailId|文字列|任意の購入ラインId|
|detailType|文字列|任意の購入ラインタイプ|
|salesType|数値|販売タイプ|
|timestamp|文字列|データ保存時刻|
|eTag|文字列|タグ情報|
|productId|文字列|商品Id|
|productCode|文字列|商品コード|
|productName|文字列|商品名|
|taxCategory|文字列|税金カテゴリー|
|price|数値|価格|
|salesPrice|数値|販売価格|
|quantity|数値|個数う|
|taxDivision|文字列|税金グループ|
|taxFreeDivision|文字列|免税グループ|
|taxFreeAmount|数値|免税対象額|
|cateogyrId|文字列|商品カテゴリーId|
|categoryName|文字列|商品カテゴリー名|
|productBundleGroupId|文字列|商品バンドルグループId|
|printReceiptProductName|文字列|表示用商品名|
|taxRate|数値|税率|
|unitNonDiscountSum|数値|値引き対象外金額|
|bargainName|文字列|値引き名|
|bargainDiscountProportional|数値|値引き対象金額|
|taxIncludeProportional|数値|内税対象金額|
|taxExcludeProportional|数値|外税対象金額|
|unitDiscountSum|文字列|値引きユニット名|
|unitDiscountName|文字列|値引き名|

/subscription

|名前|タイプ|備考|
|:--|:--|:--|
|rowKey|文字列|購読プランId|
|partitionKey|文字列|購読プラン、サブId|
|timestamp|文字列|データ取得時刻|
|eTag|文字列|タグ|
|subscriptionCode|文字列|プランコード|
|description|文字列|説明文|
|charged|数値|課金されたユニット値|
|unitInCharge|文字列|課金されたユニット、現在は 'call'のみ|
|validSince|文字列|プランの有効開始時刻|
|validSinceEpoch|数値||
|validUntil|文字列|プランの無効時刻|
|validUntilEpoch|数値||
|paymentMethod|文字列|プラン支払い方法|
|memo|文字列|備考|
|maxCall|数値|プランコール最大数|
|called|数値|すでにコールされている数|
|chargedBy|文字列|課金したユーザーId|
|isExipred|文字列|プランが無効の場合|
|exipireHandled|文字列|プランの追加購入したUserId|
|chargeResponseStatus|文字列|追加購入に関するステータス|
|chargeResponseMessage|文字列|追加購入に関するメッセージ|
