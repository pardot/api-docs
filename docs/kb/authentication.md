# Authentication

## Via Salesforce OAuth

Prerequisites:

1. Must have [Salesforce OAuth setup](https://developer.salesforce.com/docs/atlas.en-us.api_streaming.meta/api_streaming/code_sample_auth_oauth.htm) in the org.
2. Should have the Pardot Business Unit ID with which you are trying to authenticate with. [Pardot Business Unit ID](https://login.salesforce.com/lightning/setup/PardotAccountSetup/home) can be found here for your org.

### Obtain Salesforce Access Token

To use Pardot API with an SSO user, you must first get a salesforce access token.

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

If authentication was successful, a access token will be returned.

### Using Access Token with Pardot

Once you have the access token and the Pardot business Unit ID, both of these can be used to call any endpoint within Pardot.

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


If a valid access token if provided with a valid business unit ID, the Pardot endpoint should work as expected. 

## Via API Keys

### Request Format

Authentication requests sent to the Pardot API:

1.  Must be made via SSL encrypted connection
2.  Must use HTTP `POST`
3.  Must contain the `email`, `password`, and `user_key` for the Pardot user account that will be submitting API requests

Login requests that meet these criteria will be granted an API key.

API user keys are available in Pardot under **{your email address} > Settings** in the API User Key row. If you need assistance in acquiring your user key, contact your Pardot support representative.

In accounts with [Salesforce User Sync enabled](https://help.salesforce.com/articleView?id=pardot_sf_connector_setup_user_sync_considerations.htm&type=5), you must authenticate with a Pardot-only user. SSO users aren't supported with this authentication type. [OAuth](#via-salesforce-oauth) authentication must be used for SSO users.

> Both User and API keys are unique to individual users. API keys are valid for 60 minutes. In contrast, user keys are valid indefinitely.

#### Sample POST Request

```
POST https://pi.pardot.com/api/login/version/3 HTTP/1.1

email=<email>&password=<password>&user_key=<user_key>
```

#### Request Parameters

| **Parameter** | **Required**   | **Description**                                              |
| ------------- | -------------- | ------------------------------------------------------------ |
| `email`       | X              | The email address of your user account                       |
| `password`    | X              | The password of your user account                            |
| `user_key`    | X              | The 32-character hexadecimal user key for your user account  |

If authentication was successful, a 32-character hexadecimal API key will be returned in the following format:

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

Subsequent authentication requests will return either the current valid API key or a newly generated API key if the previous one had expired.