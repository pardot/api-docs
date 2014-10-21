# Sending One To One Emails


## [](#supported-operations-a-name-supported-operations-id-supported-operations-a-)Supported Operations<a name="82871-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [User](../object-field-references#email) section of [Object Field References](../object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `send` | `/api/email/version/ 3/do/send/prospect_id/ **_<prospect_id>?..._**` | `user_key, api_key, campaign_id, (email_template_id OR (text_content, name, subject, & ((from_email & from_name) OR from_user_id)))` | Sends a one-to-one email to the prospect identified by `<prospect_id>` |
| `send` | `/api/email/version/ 3/do/send/prospect_email/ **_<prospect_email>?..._**` | `user_key, api_key, campaign_id, (email_template_id OR (text_content, name, subject, & ((from_email & from_name) OR from_user_id)))` | Sends a one-to-one email to the prospect identified by `<prospect_email>` |

## [](#supported-parameters-)Supported Parameters

| Parameter              | Required         | Type                                                                | Description |
|------------------------|------------------|------------------------------------------------------------------------|-------------|
| user_key | x | string | Your API user key. Required for all API requests. |
| api_key | x | string | Your api_key. Provided by authentication request. Required for all API requests. |
| campaign_id | x | integer | The id of the campaign you'd like this email associated with. |
| prospect_id | x**** | integer | The id of the prospect you're sending the email to. |
| prospect_email | x**** | string | The email of the prospect you're sending the email to. |
| from_name | x** | string | The name of the sending user. |
| from_email | x** | string | The email of the sending user. |
| from_user_id | x** | string | The user id of the sending user. |
| replyto_email |  | string | The email address where replies should be sent. |
| tags[] |  | string | The name of the tag you'd like to create or associate with this email. You can post multiple tags[] for multiple tags. |
| operational_email |  | boolean | When set, the email will be sent to the prospect regardless of opt-out status. Your account must have this feature enabled to use this setting. |
| name | x* | string | The name of the email within Pardot. |
| subject | x* | string | The subject of the email. |
| text_content | x* | string | The text body of the email. This must contain either %%unsubscribe%% or %%email_preference_center%%. |
| html_content |  | string | The html body of the email. This must contain either %%unsubscribe%% or %%email_preference_center%%. |
| email_template_id | x*** | integer | The id of the email template to use. |
| format |  | (xml or json) | The format which the response will be sent. Xml is default. |

\* field is required if an `email_template_id` is not
provided.

** (`from_email` &amp; `from_name`) or `from_user_id` is required if an `email_template_id` is not provided.

*** if provided, the email template will be used first, then `name`, `replyto_email`, `subject`, `text_content`, and `html_content` will override the template contents if they're provided.

**** `prospect_id` or `prospect_email` is required.

## [](#example-requests-)Example Requests

This API request example made with cURL, will immediately send an email based on a template to a single prospect.

```
curl https://pi.pardot.com/api/email/version/3/do/send \
--data-urlencode user_key={user_key} \
--data-urlencode api_key={api_key} \
--data-urlencode campaign_id=54321 \
--data-urlencode prospect_email=prospect@somecompany.com \
--data-urlencode email_template_id=6789 \
--data-urlencode format=json
```

## [](#xml-response-format-)XML Response Format

```
<rsp stat="ok" version="1.0">
    <email>
        ...
    </email>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<email>` | Parent tag. Contains data fields for target email. For complete field listing, see [email](../object-field-references#email) in [Object Field References](../object-field-references). |
