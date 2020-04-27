# Authentication

To access the Pardot API with an SSO enabled user (including users synced from Salesforce), you must use a Salesforce OAuth endpoint for authentication. To access the Pardot API with a Pardot-only user (created within Pardot and not synced to Salesforce), you must use the Pardot API login endpoint for authentication. These options are described below.

## Via Salesforce OAuth

Prerequisites:

1. You must have [Salesforce OAuth setup](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_oauth_and_connected_apps.htm) in the org. To setup up a connected app for OAuth, the "pardot_api" scope must be one of the selected OAuth scopes. Otherwise, OAuth flows other than username/password flow will not be usable with the Pardot API.

2. You must have the Pardot Business Unit ID with that you are trying to authenticate with. You can find [Pardot Business Unit ID](https://login.salesforce.com/lightning/setup/PardotAccountSetup/home) here for your org.

### Obtain Salesforce Access Token

To use Pardot API with an SSO user, you must first get a salesforce access token. The example below uses the username/password OAuth flow to obtain an access token for simplicity. Any OAuth flow can be used to obtain an access token. In many use cases, other OAuth flows are more appropriate than username/password flow. For example, a web app with user interaction would likely use either user agent flow or web server flow. See [Salesforce OAuth setup](https://help.salesforce.com/articleView?id=remoteaccess_oauth_flows.htm) for details.

#### Sample POST Request for OAuth Token

```
POST https://login.salesforce.com/services/oauth2/token HTTP/1.1

grant_type=password
client_id=<client_id>
client_secret=<client_secret>
username=<username>
password=<password>
```

#### Request Parameters

| **Parameter**  | **Required**   | **Description**                                              |
| -------------  | -------------- | ------------------------------------------------------------ |
| `grant_type`   | X 	          | The value must be "password"			                     |
| `client_id`    | X              | The consumer key  				                             |
| `client_secret`| X              | The consumer secret 										 |
| `username`	 | X              | The email address of the SSO user account 					 |
| `password`	 | X              | The password of the SSO user account 						 |

If authentication is successful, an access token is be returned. See [Salesforce OAuth documentation](https://help.salesforce.com/articleView?id=remoteaccess_oauth_username_password_flow.htm) for the response format.

### Using Access Token with Pardot

After you get the access token, you must pass it and the Pardot Business Unit ID using the `Authorization` and `Pardot-Business-Unit-Id` headers.

#### Sample Request

```
POST https://pi.pardot.com/api/<object>/version/<version>/do/<op> HTTP/1.1

Authorization: Bearer <access_token>
Pardot-Business-Unit-Id: <business_unit_id>
```

#### Request Parameters

| **Parameter** 	| **Required**   | **Description**                                              |
| ------------- 	| -------------- | ------------------------------------------------------------ |
| `access_token`	| X              | Access token obtained from Salesforce OAuth Endpoint         |
| `business_unit_id`| X              | Pardot Business Unit ID 			                            |


If a valid access token is provided with a valid business unit ID, the Pardot endpoint should work as expected.

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
