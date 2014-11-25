# API (version 3) - Authentication


A few prerequisites must be met to successfully authenticate a
connection to the API.

1.  All requests to the Pardot API must be made via SSL encrypted
connection.
2.  Authentication requests must use HTTP POST.
3.  Obtain the `email`, `password`, and `user_key` (available in Pardot under **{your email address} > Settings** in the API User Key row) for the Pardot user account that will be submitting API requests. If you need assistance in acquiring your user key, contact your Pardot support representative.

With these requirements met, an API key must be acquired. Both User and API keys are unique to individual users. API keys are valid for 60 minutes. In contrast, user keys are valid indefinitely. To authenticate, issue the following request (having replaced the values denoted by `<carets>` with values for your account):

```
POST: https://pi.pardot.com/api/login/version/3
message body: email=<email>&password=<password>&user_key=<user_key>
```

| **Parameter** | **Required**   | **Description**                                        |
| ------------- | :------------: | ----------------------------------------------------- |
| `email`       | X              | The email address of your user account                 |
| `password`    | X              | The password of your user account                      |
| `user_key`    | X              | The 32-bit hexadecimal user key for your user account  |

If authentication was successful, a 32-character hexadecimal API
key will be returned in the following format:

```
<rsp stat="ok" version="1.0">
    <api_key>5a1698a233e73d7c8ccd60d775fbc68a</api_key>
</rsp>
```

Otherwise, the response will contain the following:

```
<rsp stat="fail" version="1.0">
    <err code="15">Login failed</err>
</rsp>
```

Subsequent authentication requests will return either the
current valid API key or a newly generated API key if the previous
one had expired.
