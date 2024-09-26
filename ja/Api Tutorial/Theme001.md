# テーマデータの管理

テーマはレシートに紐づけることができ、レシートのデザインやレシートに追加するコンテンツを指定することができます。購入データに紐づけてクーポンの表示や、カスタマイズされたメッセージの表示などが可能です。

---

## テーマの主な機能

- **レシートデザインのカスタマイズ**: テーマを使用して、レシートの全体的な見た目や配色を変更できます。
- **コンテンツの追加**: ヘッダーやフッター、特定のセクションにカスタムHTMLコンテンツを追加できます。
- **動的コンテンツの表示**: 購入データに基づいて、クーポンや特別なメッセージを表示することができます。

---

## テーマの利用方法

1. **テーマの作成**: 新しいテーマを作成します。詳細は[テーマの作成](/{organizationId}/theme/create)をご参照ください。

2. **テーマの取得**: 既存のテーマを取得します。詳細は[テーマの取得](/{organizationId}/theme/{id})をご参照ください。

3. **テーマの更新**: 既存のテーマを更新します。詳細は[テーマの更新](/{organizationId}/theme/update)をご参照ください。

4. **テーマの適用**: 作成または更新したテーマをレシートに適用します。レシート生成時にテーマIDを指定してください。

---

# テーマ一覧の取得 (/{organizationId}/themes)

このエンドポイントでは、指定した組織内のテーマ一覧を取得できます。テーマはレシートのデザインや、レシートに追加するコンテンツを管理するために使用されます。購入データに紐づけてクーポンの表示や、カスタマイズされたメッセージの表示などが可能です。

---

## リクエスト

- **エンドポイント**

      POST https://api.receiptroller.com/{organizationId}/themes

- **ヘッダー**

      Content-Type: application/json
      Accept: application/json
      Authorization: Bearer {YOUR TOKEN HERE}

- **リクエストボディ**

  | フィールド名    | 型     | 必須 | 説明                                           |
  |-----------------|--------|------|------------------------------------------------|
  | storeId         | string | 任意 | 店舗ID                                          |
  | keyword         | string | 任意 | テーマ検索キーワード                            |
  | currentPage     | int    | 任意 | 現在のページ（ページネーション）                |
  | itemsPerPage    | int    | 任意 | ページごとのアイテム数。上限は1000件です         |
  | sort            | string | 任意 | 並び順（例: "name asc", "name desc"）          |

### リクエスト例

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

---

## レスポンス

- **ステータスコード**

  - **200 OK**: 正常に処理されました。

- **レスポンスボディ**

  | フィールド名                  | 型       | 説明                             |
  |-------------------------------|----------|----------------------------------|
  | themes                        | object   | テーマ情報のオブジェクト           |
  | ├─ items                      | array    | テーマの配列                      |
  | ├─ currentPage                | int      | 現在のページ                      |
  | ├─ itemsPerPage               | int      | ページごとのアイテム数            |
  | ├─ totalItems                 | int      | 全アイテム数                      |
  | ├─ totalPages                 | int      | 全ページ数                        |
  | ├─ keyword                    | string   | 検索に使用したキーワード          |
  | └─ sort                       | string   | 適用された並び順                  |

各テーマオブジェクトのフィールド:

  | フィールド名                     | 型     | 説明                          |
  |----------------------------------|--------|-------------------------------|
  | id                               | string | テーマのID                     |
  | organizationId                   | string | 組織のID                       |
  | name                             | string | テーマの名前                   |
 

### レスポンス例

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

---

## レスポンスの注意事項

- 取得できなかった項目や空の値の項目はレスポンスに含まれない場合があります。

---

## エラーハンドリング

API利用時にエラーが発生した場合、以下の形式でエラーレスポンスが返されます。

- **レスポンスボディ**

  | フィールド名 | 型     | 説明            |
  |--------------|--------|-----------------|
  | error        | string | エラーメッセージ    |
  | status       | int    | HTTPステータスコード |

### エラーレスポンス例

- **400 Bad Request（リクエストが不正な場合）**

      {
        "error": "Invalid request parameters.",
        "status": 400
      }

- **401 Unauthorized（認証エラーの場合）**

      {
        "error": "Unauthorized access. Invalid or missing token.",
        "status": 401
      }

- **403 Forbidden（アクセス権がない場合）**

      {
        "error": "Forbidden. You do not have access to this resource.",
        "status": 403
      }

- **404 Not Found（リソースが見つからない場合）**

      {
        "error": "Themes not found.",
        "status": 404
      }

- **500 Internal Server Error（サーバー内部エラーの場合）**

      {
        "error": "An unexpected server issue occurred.",
        "status": 500
      }

---

# テーマの取得 (/{organizationId}/theme/{id})

このエンドポイントでは、指定したテーマIDに対応するテーマの詳細情報を取得できます。テーマはレシートのデザインや、レシートに追加するコンテンツを管理するために使用されます。購入データに紐づけてクーポンの表示や、カスタマイズされたメッセージの表示などが可能です。

---

## リクエスト

- **エンドポイント**

      GET https://api.receiptroller.com/{organizationId}/theme/{id}

- **ヘッダー**

      Accept: application/json
      Authorization: Bearer {YOUR TOKEN HERE}

- **パスパラメータ**

  | パラメータ名       | 型     | 必須 | 説明          |
  |--------------------|--------|------|---------------|
  | organizationId     | string | 必須 | 組織のID      |
  | id                 | string | 必須 | テーマのID    |

### リクエスト例

    curl -X 'GET' \
      'https://api.receiptroller.com/{organizationId}/theme/{id}' \
      -H 'accept: application/json' \
      -H 'Authorization: Bearer {YOUR TOKEN HERE}'

---

## レスポンス

- **ステータスコード**

  - **200 OK**: 正常に処理されました。
  - **404 Not Found**: 指定されたテーマが見つかりません。

- **レスポンスボディ**

  | フィールド名                     | 型     | 説明                          |
  |----------------------------------|--------|-------------------------------|
  | id                               | string | テーマのID                     |
  | organizationId                   | string | 組織のID                       |
  | name                             | string | テーマの名前                   |
  | backgroundColor                  | string | 背景色（例: "#ffffff"）         |
  | foreColor                        | string | 前景色（文字色）（例: "#000000"）|
  | headerContentHtml                | string | ヘッダー部分のHTMLコンテンツ     |
  | afterItemsContentHtml            | string | 商品一覧の後に表示されるHTML     |
  | afterGrandTotalContentHtml       | string | 合計金額の後に表示されるHTML     |
  | afterPaymentMethodContentHtml    | string | 支払い方法の後に表示されるHTML   |
  | footerContentHtml                | string | フッター部分のHTMLコンテンツ     |

### レスポンス例

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

---

## レスポンスの注意事項

- 取得できなかった項目や空の値の項目はレスポンスに含まれない場合があります。

---

## エラーハンドリング

API利用時にエラーが発生した場合、以下の形式でエラーレスポンスが返されます。

- **レスポンスボディ**

  | フィールド名 | 型     | 説明            |
  |--------------|--------|-----------------|
  | error        | string | エラーメッセージ    |
  | status       | int    | HTTPステータスコード |

### エラーレスポンス例

- **404 Not Found（テーマが見つからない場合）**

      {
        "error": "Theme not found.",
        "status": 404
      }

- **401 Unauthorized（認証エラーの場合）**

      {
        "error": "Unauthorized access. Invalid or missing token.",
        "status": 401
      }

- **403 Forbidden（アクセス権がない場合）**

      {
        "error": "Forbidden. You do not have access to this resource.",
        "status": 403
      }

- **500 Internal Server Error（サーバー内部エラーの場合）**

      {
        "error": "An unexpected server issue occurred.",
        "status": 500
      }

---


# テーマの作成 (/{organizationId}/theme/create)

このエンドポイントを使用して、新しいテーマを作成できます。テーマはレシートのデザインや、レシートに表示されるコンテンツを管理するためのものです。背景色や前景色（文字色）のカスタマイズ、ヘッダーやフッターに表示するHTMLコンテンツなどを設定することができます。購入データに基づくクーポンやメッセージの表示もテーマを通じて制御可能です。

---

## リクエスト

- **エンドポイント**

      POST https://api.receiptroller.com/{organizationId}/theme/create

- **ヘッダー**

      Content-Type: application/json
      Accept: application/json
      Authorization: Bearer {YOUR TOKEN HERE}

- **リクエストボディ**

  | フィールド名                     | 型     | 必須 | 説明                          |
  |----------------------------------|--------|------|-------------------------------|
  | name                             | string | 必須 | テーマの名前                   |
  | backgroundColor                  | string | 任意 | 背景色（例: "#ffffff"）         |
  | foreColor                        | string | 任意 | 前景色（文字色）（例: "#000000"）|
  | headerContentHtml                | string | 任意 | ヘッダー部分のHTMLコンテンツ     |
  | afterItemsContentHtml            | string | 任意 | 商品一覧の後に表示されるHTML     |
  | afterGrandTotalContentHtml       | string | 任意 | 合計金額の後に表示されるHTML     |
  | afterPaymentMethodContentHtml    | string | 任意 | 支払い方法の後に表示されるHTML   |
  | footerContentHtml                | string | 任意 | フッター部分のHTMLコンテンツ     |

### リクエスト例

    curl -X 'POST' \
      'https://api.receiptroller.com/{organizationId}/theme/create' \
      -H 'accept: application/json' \
      -H 'Authorization: Bearer {YOUR TOKEN HERE}' \
      -H 'Content-Type: application/json' \
      -d '{
      "name": "Modern Theme",
      "backgroundColor": "#ffffff",
      "foreColor": "#000000",
      "headerContentHtml": "<h1>Welcome to Our Store</h1>",
      "afterItemsContentHtml": "<p>Thank you for shopping!</p>",
      "afterGrandTotalContentHtml": "<p>Grand Total includes taxes.</p>",
      "afterPaymentMethodContentHtml": "<p>Paid via credit card.</p>",
      "footerContentHtml": "<footer>© 2024 Example Corp.</footer>"
    }'

---

## レスポンス

- **ステータスコード**

  - **201 Created**: テーマが正常に作成されました。

- **レスポンスボディ**

  | フィールド名                     | 型     | 説明                          |
  |----------------------------------|--------|-------------------------------|
  | name                             | string | テーマの名前                   |
  | backgroundColor                  | string | 背景色                         |
  | foreColor                        | string | 前景色（文字色）               |
  | headerContentHtml                | string | ヘッダー部分のHTMLコンテンツ     |
  | afterItemsContentHtml            | string | 商品一覧の後に表示されるHTML     |
  | afterGrandTotalContentHtml       | string | 合計金額の後に表示されるHTML     |
  | afterPaymentMethodContentHtml    | string | 支払い方法の後に表示されるHTML   |
  | footerContentHtml                | string | フッター部分のHTMLコンテンツ     |

### レスポンス例

    {
      "name": "Modern Theme",
      "backgroundColor": "#ffffff",
      "foreColor": "#000000",
      "headerContentHtml": "<h1>Welcome to Our Store</h1>",
      "afterItemsContentHtml": "<p>Thank you for shopping!</p>",
      "afterGrandTotalContentHtml": "<p>Grand Total includes taxes.</p>",
      "afterPaymentMethodContentHtml": "<p>Paid via credit card.</p>",
      "footerContentHtml": "<footer>© 2024 Example Corp.</footer>"
    }

---

## レスポンスの注意事項

- 取得できなかった項目や空の値の項目はレスポンスに含まれない場合があります。

---

## エラーハンドリング

API利用時にエラーが発生した場合、以下の形式でエラーレスポンスが返されます。

- **レスポンスボディ**

  | フィールド名 | 型     | 説明            |
  |--------------|--------|-----------------|
  | error        | string | エラーメッセージ    |
  | status       | int    | HTTPステータスコード |

### エラーレスポンス例

- **400 Bad Request（リクエストが不正な場合）**

      {
        "error": "Invalid request parameters.",
        "status": 400
      }

- **401 Unauthorized（認証エラーの場合）**

      {
        "error": "Unauthorized access. Invalid or missing token.",
        "status": 401
      }

- **403 Forbidden（アクセス権がない場合）**

      {
        "error": "Forbidden. You do not have access to this resource.",
        "status": 403
      }

- **500 Internal Server Error（サーバー内部エラーの場合）**

      {
        "error": "An unexpected server issue occurred.",
        "status": 500
      }

---

# テーマの更新 (/{organizationId}/theme/update)

このエンドポイントは、既存のテーマを更新する際に使用されます。テーマはレシートのデザインや表示内容に関連しており、背景色や前景色、ヘッダーやフッターのHTMLコンテンツを変更することができます。たとえば、購買データに基づくカスタマイズされたメッセージやクーポンを表示する際に役立ちます。

---

## リクエスト

- **エンドポイント**

      POST https://api.receiptroller.com/{organizationId}/theme/update

- **ヘッダー**

      Content-Type: application/json
      Accept: application/json
      Authorization: Bearer {YOUR TOKEN HERE}

- **リクエストボディ**

  | フィールド名                     | 型     | 必須 | 説明                          |
  |----------------------------------|--------|------|-------------------------------|
  | id                               | string | 必須 | テーマのID                     |
  | name                             | string | 必須 | テーマの名前                   |
  | backgroundColor                  | string | 任意 | 背景色（例: "#ffffff"）         |
  | foreColor                        | string | 任意 | 前景色（文字色）（例: "#000000"）|
  | headerContentHtml                | string | 任意 | ヘッダー部分のHTMLコンテンツ     |
  | afterItemsContentHtml            | string | 任意 | 商品一覧の後に表示されるHTML     |
  | afterGrandTotalContentHtml       | string | 任意 | 合計金額の後に表示されるHTML     |
  | afterPaymentMethodContentHtml    | string | 任意 | 支払い方法の後に表示されるHTML   |
  | footerContentHtml                | string | 任意 | フッター部分のHTMLコンテンツ     |

### リクエスト例

    curl -X 'POST' \
      'https://api.receiptroller.com/{organizationId}/theme/update' \
      -H 'accept: application/json' \
      -H 'Authorization: Bearer {YOUR TOKEN HERE}' \
      -H 'Content-Type: application/json' \
      -d '{
      "id": "theme123",
      "name": "Updated Theme",
      "backgroundColor": "#eeeeee",
      "foreColor": "#111111",
      "headerContentHtml": "<h1>Updated Header</h1>",
      "afterItemsContentHtml": "<p>Updated After Items</p>",
      "afterGrandTotalContentHtml": "<p>Updated After Grand Total</p>",
      "afterPaymentMethodContentHtml": "<p>Updated After Payment Method</p>",
      "footerContentHtml": "<footer>© 2024 Updated Corp.</footer>"
    }'

---

## レスポンス

- **ステータスコード**

  - **200 OK**: テーマが正常に更新されました。

- **レスポンスボディ**

  | フィールド名                     | 型     | 説明                          |
  |----------------------------------|--------|-------------------------------|
  | id                               | string | テーマのID                     |
  | organizationId                   | string | 組織のID                       |
  | name                             | string | テーマの名前                   |
  | backgroundColor                  | string | 背景色                         |
  | foreColor                        | string | 前景色（文字色）               |
  | headerContentHtml                | string | ヘッダー部分のHTMLコンテンツ     |
  | afterItemsContentHtml            | string | 商品一覧の後に表示されるHTML     |
  | afterGrandTotalContentHtml       | string | 合計金額の後に表示されるHTML     |
  | afterPaymentMethodContentHtml    | string | 支払い方法の後に表示されるHTML   |
  | footerContentHtml                | string | フッター部分のHTMLコンテンツ     |

### レスポンス例

    {
      "id": "theme123",
      "organizationId": "1234-organization-5678",
      "name": "Updated Theme",
      "backgroundColor": "#eeeeee",
      "foreColor": "#111111",
      "headerContentHtml": "<h1>Updated Header</h1>",
      "afterItemsContentHtml": "<p>Updated After Items</p>",
      "afterGrandTotalContentHtml": "<p>Updated After Grand Total</p>",
      "afterPaymentMethodContentHtml": "<p>Updated After Payment Method</p>",
      "footerContentHtml": "<footer>© 2024 Updated Corp.</footer>"
    }

---

## レスポンスの注意事項

- 取得できなかった項目や空の値の項目はレスポンスに含まれない場合があります。

---

## エラーハンドリング

API利用時にエラーが発生した場合、以下の形式でエラーレスポンスが返されます。

- **レスポンスボディ**

  | フィールド名 | 型     | 説明            |
  |--------------|--------|-----------------|
  | error        | string | エラーメッセージ    |
  | status       | int    | HTTPステータスコード |

### エラーレスポンス例

- **400 Bad Request（リクエストが不正な場合）**

      {
        "error": "Invalid request parameters.",
        "status": 400
      }

- **401 Unauthorized（認証エラーの場合）**

      {
        "error": "Unauthorized access. Invalid or missing token.",
        "status": 401
      }

- **403 Forbidden（アクセス権がない場合）**

      {
        "error": "Forbidden. You do not have access to this resource.",
        "status": 403
      }

- **404 Not Found（テーマが見つからない場合）**

      {
        "error": "Theme not found.",
        "status": 404
      }

- **500 Internal Server Error（サーバー内部エラーの場合）**

      {
        "error": "An unexpected server issue occurred.",
        "status": 500
      }

