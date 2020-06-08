# Authentication

To access the Pardot API with an SSO enabled user (including users synced from Salesforce), you must use a Salesforce OAuth endpoint for authentication. To access the Pardot API with a Pardot-only user (created within Pardot and not synced to Salesforce), you must use the Pardot API login endpoint for authentication. These options are described below.

## Via Pardot API login endpoint

### Request Format

Authentication requests sent to the Pardot API:

1.  Must be made via SSL encrypted connection
2.  Must use HTTP `POST`
3.  Must contain the `email`, `password`, and `user_key` for the Pardot user account that will be submitting API requests

Login requests that meet these criteria are granted an API key.

API user keys are available in Pardot under **{your email address} > Settings** in the API User Key row. For assistance in acquiring your user key, contact your Pardot support representative.

In accounts with [Salesforce User Sync enabled](https://help.salesforce.com/articleView?id=pardot_sf_connector_setup_user_sync_considerations.htm&type=5), you must authenticate with a Pardot-only user. SSO users aren't supported with this authentication type. [OAuth](#via-salesforce-oauth) authentication must be used for SSO users.

> Both User and API keys are unique to individual users. API keys are valid for 60 minutes. In contrast, user keys are valid indefinitely.

#### Sample POST Request

```
POST https://pi.pardot.com/api/login/version/3 HTTP/1.1

email=<email>&password=<password>&user_key=<user_key>
```

#### Request Parameters

| **Parameter** | **Required**   | **Description**                                              |
| -- | --- | --- |
| `email`       | X | User account email address |
| `password`    | X | User account password |
| `user_key`    | X | User account 32-character hexadecimal user key |

If authentication was successful, an API key will be returned in the following format:

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

Subsequent authentication requests return either the current valid API key or a newly generated API key if the previous one expired.
