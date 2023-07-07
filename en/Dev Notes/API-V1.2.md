Following items are changed for Version 1.2.

# Upsert Receipt Request Model will be changed.
1. `cancelType` will be a numeric value. Currently, only the value `0` is used, but we plan to handle values other than `0`.
2. Export values related to `customer` as an object. The contents in `customer` will be `customerId`, `customerCode`, `customerGroup`, `customerPrintName`, `customerMemo`.
3. Export values related to `point` or `mile` as an object. It will be an array inside `customer`. The array name will be `membershipPrograms`, with `membershipProgramName`, `membershipProgramPointsUsed`, `membershipProgramPointsAdded`, `membershipProgramPointsAfter`, `membershipProgramPointsBefore`, `membershipProgramPointsNote`.
4. Export values related to `tax` as an array object. This object will be defined inside `PaymentSummary`. The object name will be `taxes`, with `taxPercentageIfInclude`, `taxPercentageIfExclude`, `applicableSubTotalAmount`.
5. `isClosed`, `closingDate` will no longer be available.
6. `Subtotal`, `GrandTotal`, `Deposit` etc. will be exported as the `PaymentSummary` object. `PaymentSummary` will consist of `grandTotal`, `subTotal`, `taxes`, `subTotalDiscountAmount`, `shippingFee`, `serviceFee`, `otherFee`, `depositMethod`, `deposit`, `change`.
7. Add `price` in addition to `salesPrice` in `items`. `price` will be the normal price, and `salesPrice` will be the sales price. The difference will be automatically calculated as a discount.
8. In `items`, rename `itemId` to `LineItemId`.
9. In `items`, change `itemTypes` to `LineItemType`.
10. Add an array object related to `taxes` in `items`.
11. Add `currency`. Please use ISO4217 for values.
12. If there is a request error, an error will be returned.

# Upsert Receipt Response Model will be changed.

1. Rename `rowKey` to `receiptId`.
2. `partitionKey` will no longer be available.
3. `eTag` will no longer be available.
4. `itemListJsonString` will no longer be available.
5. Export values related to `store` as an object. The contents in `store` will be `storeId`, `storeCode`, `storeName`, `storeRegisgrationName`, `storeRegisgrationCode`, `storeTel`, `storeAddress`, `storeMemo`.
6. Export values related to `staff` as an object. The contents in `staff` will be `staffId`, `staffCode`, `staffName`.
7. Export values related to `customer` as an object. The contents in `customer` will be `customerId`, `customerCode`, `customerGroup`, `customerPrintName`, `customerMemo`.
8. `isClosed` and `closingDate` will no longer be available.
9. Export values related to `tax` as an object. The values in `taxes` will be `taxPercentageIfInclude`, `taxPercentageIfExclude`, `applicableSubTotalAmount`.
10. Export values related to `point` or `mile` as an object. The array name will be `membershipPrograms`, with `membershipProgramName`, `membershipProgramPointsUsed`, `membershipProgramPointsAdded`, `membershipProgramPointsAfter`, `membershipProgramPointsBefore`, `membershipProgramPointsNote`.
11. `Subtotal`, `GrandTotal`, `Deposit` etc. will be exported as the `PaymentSummary` object. `PaymentSummary` will consist of `grandTotal`, `subTotal`, `taxes`, `subTotalDiscountAmount`, `shippingFee`, `serviceFee`, `otherFee`, `depositMethod`, `deposit`, `change`.
12. `senderLogJsonString` will no longer be available.
13. `ocrText`, `ocrResult`, `receiptStatus`, `expenseCategory`, `readAndApproved`, `isReadable`, `imageLocation` will no longer be available.
14. `amount` will no longer be available and will be unified with `GrandTotal`.
15. `smaregiTransactionJson` will no longer be available.
16. Export values related to `coupon` as an object. The array name will be `coupons`, with `couponName`, `couponPointsUsed`, `couponPointsAdded`, `couponPointsAfter`, `couponPointsBefore`, `couponNote`.
17. Rename `receiptItems` to `itemDetailLines`.
18. In `itemDetailLines`, rename `rowKey` to `lineId`.
19. In `itemDetailLines`, `partitionKey` will no longer be available.
20. In `itemDetailLines`, rename `detailId` to `itemId`.
21. In `itemDetailLines`, rename `detailType` to `itemType`.
22. In `itemDetailLines`, `eTag` will no longer be available.
23. In `itemDetailLines`, `printReceiptProductName` will no longer be available and will be unified with `productName`.
24. In `itemDetailLines`, `productBundleGroupId` will no longer be available.
25. In `itemDetailLines`, export discount-related values as an object.
26. In `subscription`, rename `rowKey` to `subscriptionId`.
27. In `subscription`, `partitionKey` will no longer be available.
28. In `subscription`, `eTag` will no longer be available.
29. In `subscription`, `timestamp` will no longer be available.
30. In `subscription`, `validSinceEpoch`, `validUntilEpoch` will no longer be available.
