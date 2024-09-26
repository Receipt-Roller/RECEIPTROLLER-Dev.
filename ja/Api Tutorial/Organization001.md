# 組織データ管理

各アカウントは、複数の組織を管理することができます。各組織の下には複数の店舗があり、さらにその下には複数の端末が配置されています。この階層構造を通じて、各エンドポイントでは組織、店舗、端末ごとのデータ管理が可能です。

## 組織データ

組織データは以下の項目が表示・編集可能です。

| 名前              | タイプ    | 必須  | 最大値 | メモ                 |
|-------------------|-----------|-------|--------|----------------------|
| id                | 文字列    |       | 68文字 | 閲覧のみ、組織ID      |
| name              | 文字列    | 必須  | 68文字 | 組織名               |
| postalCode        | 文字列    | 必須  | 12文字 | 郵便番号             |
| country           | 文字列    | 必須  | 24文字 | 国名                 |
| prefecture        | 文字列    | 必須  | 24文字 | 都道府県             |
| locality          | 文字列    | 必須  | 24文字 | 市区町村             |
| address1          | 文字列    | 必須  | 24文字 | 住所、番地           |
| address2          | 文字列    |       | 24文字 | ビル名、部屋名        |
| tel               | 文字列    | 必須  | 24文字 | 電話番号             |
| email             | 文字列    | 必須  | 48文字 | メールアドレス       |
| smaregiContractId | 文字列    |       |        | 閲覧のみ             |
| validPlans        | オブジェクト |       |        | 閲覧のみ、有効プランの一覧 |

---

# 組織一覧の取得 (/account/organizations)

## リクエスト

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/account/organizations' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}'
```

## レスポンス

```json
[
  {
    "id": "9356c405-b51a-4c40-8a11-9898c6d4be66",
    "name": "下田商店"
  },
  {
    "id": "8fe6866d-c5e1-4703-875d-d2bdfa10bc2a",
    "name": "TOKYO ANIME"
  },
  {
    "id": "e53f4703-66cf-4d08-b6fe-77a1c65b4607",
    "name": "ABCクッキー"
  },
  {
    "id": "61fd7924-6a42-4837-bd84-6b9f3046c033",
    "name": "渋谷アパレル"
  }
]
```

---

# 組織詳細取得 (/account/organization/{id})

## リクエスト

```bash
curl -X 'GET' \
  'https://api.receiptroller.com/account/organization/8fe6866d-c5e1-4703-875d-d2bdfa10bc2a' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}'
```

## レスポンス

```json
{
  "id": "8fe6866d-c5e1-4703-875d-d2bdfa10bc2a",
  "name": "TOKYO ANIME",
  "postalCode": "",
  "country": "",
  "prefecture": "",
  "locality": "",
  "address1": "",
  "address2": null,
  "tel": null,
  "email": null,
  "smaregiContractId": null,
  "validPlans": []
}
```

---

# 組織情報の更新 (/account/organization/update)

## リクエスト

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/account/organization/update' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
  "id": "8fe6866d-c5e1-4703-875d-d2bdfa10bc2a",
  "name":"TOKYO ANIME",
  "postalCode": "3800096",
  "country": "JAPAN",
  "prefecture": "長野県",
  "locality": "長野市",
  "address1": "鶴賀七瀬123-12"
}'
```

## レスポンス

```json
{
  "id": "8fe6866d-c5e1-4703-875d-d2bdfa10bc2a",
  "name": "TOKYO ANIME",
  "postalCode": "3800096",
  "country": "JAPAN",
  "prefecture": "長野県",
  "locality": "長野市",
  "address1": "鶴賀七瀬123-12",
  "address2": null,
  "tel": null,
  "email": null,
  "smaregiContractId": null
}
```

---

# 組織の作成 (/account/organization/create)

## リクエスト

```bash
curl -X 'POST' \
  'https://api.receiptroller.com/account/organization/create' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer {YOUR TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
  "name":"新しい組織名",
  "postalCode": "1234567",
  "country": "JAPAN",
  "prefecture": "東京都",
  "locality": "渋谷区",
  "address1": "道玄坂1-2-3",
  "address2": "ビル101",
  "tel": "03-1234-5678",
  "email": "neworg@example.com"
}'
```

## レスポンス

```json
{
  "id": "新しい組織ID",
  "name": "新しい組織名",
  "postalCode": "1234567",
  "country": "JAPAN",
  "prefecture": "東京都",
  "locality": "渋谷区",
  "address1": "道玄坂1-2-3",
  "address2": "ビル101",
  "tel": "03-1234-5678",
  "email": "neworg@example.com"
}
```

