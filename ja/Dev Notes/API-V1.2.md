V1.2では下記の項目を改修し変更いたします。本番反映時期は追ってご連絡いたします。

# レシート作成時のリクエストモデル変更

1. `cancelType` は数値とします、今は値`0`のみが値となりますが、`0`以外の値も取り扱う予定です。
2. `customer`に関する値はオブジェクトとして外出しします。
3. `point`または`mile`に関する値はオブジェクトとして外だしします。
4. `tax`に関する値はオブジェクトとして外だしします。
5. `isClosed`, `closingDate`は廃止いたします。
6. `Subtotal`, `GrandTotal`, `Deposit`などは `PaymentSummary`オブジェクトとして外出しします。
7. `items`内の`salesPrice`のほかに、`price`を追加します。`price`は通常価格、`salesPrice`は販売価格となります。差分は値引きとして自動計算されます。
8. `items`内の`itemId`は`LineItemId`に名前変更します。
9. `items`内の`itemTypes`は`LineItemType`に変更します。
10. `items`内に`tax`に関するオブジェクトを追加します。
11. リクエストエラーがあった際にはエラーを戻すようにいたします。

# レシート作成時のレスポンスモデルの変更

1. `rowKey` を `receiptId`に名前変更します。
2. `partitionKey`を廃止します。
3. `eTag`を廃止します。
4. `itemListJsonString`を廃止します。
5. `store`に関する値をオブジェクトとして外出しします。
6. `staff`に関する値はオブジェクトとして外だしします。
7. `customer`に関する値はオブジェクトとして外出しします。
8. `isClosed`, `closingDate`は廃止いたします。
9. `tax`に関する値はオブジェクトとして外だしします。
10. `point`または`mile`に関する値はオブジェクトとして外だしします。
11. `Subtotal`, `GrandTotal`, `Deposit`などは `PaymentSummar`yオブジェクトとして外出しします。
12. `senderLogJsonString` を廃止します。
13. `ocrText`, `ocrResult`, `receiptStatus`, `expenseCategory`, `readAndApproved`, `isReadable`, `imageLocation`を廃止します。
14. `amount`を廃止し、`GrandTotal`に統一します。
15. `smaregiTransactionJson` を廃止します。
16. `coupon`に関する値はオブジェクトとして外だしします。
17. `receiptItemsをitemDetailLines`に名前変更します。
18. `itemDetailLines`内、`rowKey`を`lineId`に名前変更します。
19. `itemDetailLines`内、`partitionKey`を廃止します。
20. `itemDetailLines`内、`detailId`は`itemId`に名前変更します。
21. `itemDetailLines`内、`detailType`は`itemType`に名前変更します。
22. `itemDetailLines`内、eTagは廃止します。
23. `itemDetailLines`内、`printReceiptProductName`を廃止します、`productName`と統一します。
24. `itemDetailLines`内、`productBundleGroupId`を廃止します。
25. `itemDetailLines`内、値引きに関する値はオブジェクトとして外出します。
26. `subscription`内、`rowKey`を`subscriptionId`に名前変更します。
27. `subscription`内、`partitionKey`を廃止します。
28. `subscription`内、`eTag`を廃止します。
29. `subscription`内、`timestamp`を廃止します。
30. `subscription`内、`validSinceEpoch`、`validUntilEpoc`をを廃止します。

以上これらの変更いたします。
