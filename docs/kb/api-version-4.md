# API Version 4

In order to accommodate a new feature related to prospects,
we have created a new version of our APIs - version 4.
We are now allowing multiple prospects to share an email address on some Pardot accounts.
If your account has this feature active now, then you MUST use version 4.
Everyone else can continue using version 3.

For more information on the API in general, check out the [Overview Page](/).

For specific API endpoints, please select from the "Version 4" list above.

## Key Differences

Version 4 may use slightly different input syntax where prospects are involved,
and may return multiple prospects where version 3 returned one.
Please check out the appropriate version's documentation for more exact usage details.

If your account uses version 4 of the API, then you must include the version 4 tag in your requests.
Failure to do so will result in an error about the API being requested.

The biggest change in the APIs in this version are that we now allow for multiple prospect records with the same email address.
A few examples of what that means:

* Prospect Create by email will create a new prospect for each time the call is made.
* Prospect Upsert by email will also always create under this specification.
* Prospect Update by email will no longer work (we don't necessarily know which prospect you're talking about)

### Requesting an API key

An exception to this rule is requesting an `api_key` through the login API.
You may use `/version/3` or `/version/4` for this call.
To let you know that you must use version 4, we will return a `<version>4</version>` tag in the response.
This version tag will not be included if your account cannot use version 4.

Request:
```
POST: https://pi.pardot.com/api/login/version/3
message body: email=<email>&password=<password>&user_key=<user_key>
```

Response:
```
<rsp stat="ok" version="1.0">
  <api_key>1234abcd</api_key>
  <version>4</version>
</rsp>
```