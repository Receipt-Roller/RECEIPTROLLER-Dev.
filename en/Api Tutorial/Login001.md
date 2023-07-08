# Managing Account with {RECEIPT}ROLLER API

The {RECEIPT}ROLLER API allows you to log in and view your profile.

## Login

Before logging in, you must have an account. If you do not have an account yet, please visit https://receiptroller.com/en and create a business account first.

To log in, use the `/account/login` endpoint. This endpoint accepts POST requests.

Here's an example of a request body for the login endpoint:

```json
{
  "userName": "string",
  "password": "string",
  "expire": "2023-07-08T00:22:48.519Z"
}
```

If the login is successful, you should get a return value like this:

```json
{
  "token": "string",
  "expire": "2023-07-08T00:22:48.545Z"
}
```

The token is a Bearer token that you can pass in the header of the API requests.

If the login is not successful, you will get an error response with a 400 status, like this:

```json
{
  "type": "string",
  "title": "string",
  "status": 0,
  "detail": "string",
  "instance": "string",
  "additionalProp1": "string",
  "additionalProp2": "string",
  "additionalProp3": "string"
}
```

Please read the error message and try to resolve the issue.

## View Profile

To view your profile, use the following endpoint:

`/account/me`

This endpoint lets you check the currently logged-in user's profile. 

Once you have obtained the Bearer token from the login process, you can call the `/account/me` endpoint to check your profile.

The `/account/me` endpoint accepts GET requests. Make sure to pass the Bearer token in the header of your API request.

Here's an example of the response you should receive:

```json
{
  "userName": "string",
  "roles": [
    "string"
  ]
}
```
