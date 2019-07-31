# What is Version 4?

In order to accommodate multiple prospects with the same email address,
we have created a new version of our APIs - version 4.
If your Pardot org has this feature enabled now, then you must use version 4.
If your Pardot org does not have this featured enabled, you must use version 3.

To determine if your Pardot org has this feature enabled, [check out this guide.](http://help.pardot.com/customer/portal/articles/2461386-how-can-i-find-out-if-my-account-allows-multiple-prospects-with-the-same-email-address-)

For more information on the API in general, check out the [Overview Page](/).

For specific API endpoints, please select from the "Version 4" list above.


# Transitioning from version 3 to version 4
If you are going to
[upgrade your Pardot org to allow multiple prospects with the same email address,](http://help.pardot.com/customer/portal/articles/2518686-enabling-multiple-prospects-with-the-same-email-address)
and you use the api, you will need to follow the guidelines below.

## Determining when these changes are applicable

As soon your Pardot org is upgraded to allow multiple prospects with the same email address, your current API session will be cleared and you must log in again.
Upon logging in, a new field will be returned in the login response.
This will be your indication that you may no longer use version 3 (or any other previous version), and must now use the version 4 syntax.
Here's what that will look like:

Request:
```
POST: https://pi.pardot.com/api/login/version/3
message body: email=<email>&password=<password>&user_key=<user_key>
```

Response (Before transition):
```
<rsp stat="ok" version="1.0">
  <api_key>1234abcd</api_key>
</rsp>
```

Response (After transition):
```
<rsp stat="ok" version="1.0">
  <api_key>5678qwertyuiop</api_key>
  <version>4</version>
</rsp>
```

*Note: Using version 3 to login will continue to work, even though all other endpoints will require version 4*

## Request Path Changes

You will need to modify your request to use the `/version/4` path. For example:

Before transition:
```
GET: https://pi.pardot.com/api/prospect/version/3/read/id/1
```
After transition:
```
GET: https://pi.pardot.com/api/prospect/version/4/read/id/1
```


## Prospect API changes

Most of the changes in version 4 occur around the prospect APIs.
When you begin using the version 4 APIs, your logic should know about these changes ([full documentation can be found here](/kb/api-version-4/prospects))

* **New reference field:**  Prospects can now be referenced using the Salesforce CRM Identifier, known to the api as the `fid` field.
This `fid` field refers to the id of the Lead or Contact record in Salesforce.
You can find the lead id (begins with 00Q) or the contact id (begins with 003) in the URL when viewing a lead or contact as seen below.
Or, you can get multiple contacts or lead ids from Salesforce using the export tool.
<img src="/img/lead_identifier_example.png" width="100%">
* **Create:** Prospects can still be created with a referenced `email` address.
If you call the create api with the same email address multiple times, each call will create a new prospect.
Previously, you would get an error.
* **Read:** When making a read query, querying by `email` will return all prospects that share that email address.
Querying by Pardot `id` or Salesforce `fid` will only return the one matching prospect.
* **Update:** Prospects can no longer be updated when referenced via `email` alone.
This is because there may now be multiple prospects with the same email address.
Instead, you must use either the Pardot `id` or Salesforce `fid` references.
* **Upsert:** Upsert query by `email` will *always* create a new prospect.
Upsert by Pardot `id` or Salesforce `fid` will update or create as needed.
See [Upserting Prospects](/kb/api-version-4/prospects/#upserting-prospects) for more details.
* **Delete:** Delete query must reference by Pardot `id` or Salesforce `fid`.
* **Batch processing:**  Examples of batch processing can be found [here](/kb/api-version-4/prospects/#endpoints-for-batch-processing)

## Opportunity API changes

[Full documentation can be found here.](/kb/api-version-4/opportunities/)

* **Create:** Creating an opportunity using a `prospect_email` reference must correspond to an existing prospect.
If there are multiple prospects with that email address, the prospect with the most recent activity date will be used.
If you want to apply the opportunity to a specific prospect, then you must reference the prospect using `prospect_id`.
* **Query:** If you query using a `prospect_email` reference, you will receive opportunities that correspond with any prospects that share that email address.
if you want a specific prospect then query by the `prospect_id`.

## Visitor API changes

[Full documentation can be found here.](/kb/api-version-4/visitors/)

* **Assign:** Assigning by `prospect_email` alone (no `prospect_id`) will return an error.
