# ログイン

APIを利用する際にはTokenが必要になります。 TokenとはAPIを利用する際に必用となる、会員情報を示すものになります。
普段利用している{RECEIPT}ROLLERのメールアドレスとパスワードで利用することができます。
まだアカウントを登録されていない方はこちらからご登録ください。
https://receiptroller.com/identity/account/register?culture=ja


# リクエスト

<table class="table">
<tr>
<td>userName</td>
<td>登録されているメールアドレス</td>
</tr>


<tr>
<td>password</td>
<td>パスワード</td>
</tr>

<tr>
<td>expire</td>
<td>有効期限、ここで指定した期日まで発行されたトークンは有効となります。</td>
</tr>

</table>

## リクエスト例


```
curl -X 'POST' \
  'https://api.receiptroller.com/account/login' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "userName": "{USER NAME}",
  "password": "{PASSWORD}",
  "expire": "2022-12-25T22:11:52.130Z"
}'
```

# レスポンス

<table class="table">
<tr>
<td>token</td>
<td>アクセストークン</td>
</tr>

<tr>
<td>expire</td>
<td>トークンの有効期限。</td>
</tr>

</table>

## レスポンス例


```
{
  "token": "{YOUR TOKEN HERE}",
  "expire": "2022-12-25T22:11:52.13Z"
}

```
