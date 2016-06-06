# Reading Emails


## Supported Operations<a name="71862-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [Email](object-field-references#email) section of [Object Field References](object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `read` | `/api/email/version/3/do/read/id/<email id>?...` | `user_key, api_key, email` | Returns the data for the email specified by `<id>`. `<id>` is the Pardot ID of the target target email. |


## XML Response Format

```
<rsp stat="ok" version="1.0">
    <email>
        ...
    </email>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<email>` | Parent tag. Contains data fields for target email. For complete field listing, see [email](object-field-references#email) in [Object Field References](object-field-references). |

# Querying Email Stats


## Supported Operations<a name="25691-supported-operations" id="supported-operations"></a>
For a complete list of fields involved in user operations, see the [Email](object-field-references#email) section of [Object Field References](object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `stats` | `/api/email/version/3/do/stats/id/<email id>?...` | `user_key, api_key, email` | Returns the statistical data for the email specified by <id>. <id> is the Pardot ID of the target target email.

## [](#xml-response-format-)XML Response Format

```
<rsp stat="ok" version="1.0">
    <stats>
        <sent>...</sent>
        <delivered>...</delivered>
        <total_clicks>...</total_clicks>
        <unique_clicks>...</unique_clicks>
        <soft_bounced>...</soft_bounced>
        <hard_bounced>...</hard_bounced>
        <opt_outs>...</opt_outs>
        <spam_complaints>...</spam_complaints>
        <opens>...</opens>
        <unique_opens>...</unique_opens>
        <delivery_rate>...</delivery_rate>
        <opens_rate>...</opens_rate>
        <click_through_rate>...</click_through_rate>
        <unique_click_through_rate>...</unique_click_through_rate>
        <click_open_ratio>...</click_open_ratio>
        <opt_out_rate>...</opt_out_rate>
        <spam_complaint_rate>...</spam_complaint_rate>
    </stats>
</rsp>
```

| **Tag** | **Description** |
| ------- | --------------- |
| `<stats>` | Contains the resulting email stats for the specified email id. |
| `<sent>` | Contains the number of emails sent. |
| `<delivered>` | Contains the number of emails delivered. |
| `<total_clicks>` | Contains the number of total clicks for the email. |
| `<unique_clicks>` | Contains the number of unique clicks for the email. |
| `<soft_bounced>` | Contains the number of soft bounces for the email. |
| `<hard_bounced>` | Contains the number of hard bounces for the email. |
| `<opt_outs>` | Contains the number of opt outs for the email |
| `<spam_complaints>` | Contains the number of spam complaints for the email. |
| `<opens>` | Contains the number of opens for the email. |
| `<unique_opens>` | Contains the number of unique opens for the email. |
| `<delivery_rate>` | Contains the delivery rate based on the number of emails sent |
| `<opens_rate>` | Contains the open rate based on the number of emails delivered |
| `<click_through_rate>` | Contains the click through rate based on the number of emails delivered |
| `<unique_click_through_rate>` | Contains the unique click through rate based on the number of emails delivered |
| `<click_open_ratio>` | Contains the ratio between email clicks and opens |
| `<opt_out_rate>` | Contains the opt out rate based on the number of emails delivered |
| `<spam_complaint_rate>` | Contains the spam complaint rate based on the number of emails delivered |

# Sending One To One Emails


## [](#supported-operations-a-name-supported-operations-id-supported-operations-a-)Supported Operations<a name="82871-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [Email](object-field-references#email) section of [Object Field References](object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `send` | `/api/email/version/ 3/do/send/prospect_id/<prospect_id>?...` | `user_key, api_key, campaign_id, (email_template_id OR (text_content, name, subject, & ((from_email & from_name) OR from_user_id)))` | Sends a one-to-one email to the prospect identified by `<prospect_id>` |
| `send` | `/api/email/version/ 3/do/send/prospect_email/<prospect_email>?...` | `user_key, api_key, campaign_id, (email_template_id OR (text_content, name, subject, & ((from_email & from_name) OR from_user_id)))` | Sends a one-to-one email to the prospect identified by `<prospect_email>` |

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
| `<email>` | Parent tag. Contains data fields for target email. For complete field listing, see [email](object-field-references#email) in [Object Field References](object-field-references). |

# Sending List Emails


## [](#supported-operations-a-name-supported-operations-id-supported-operations-a-)Supported Operations<a name="82871-supported-operations" id="supported-operations"></a>

For a complete list of fields involved in user operations, see the [Email](object-field-references#email) section of [Object Field References](object-field-references).

| **Operation** | **URL Format**                             | **Required Parameters** | **Description**  |
| ------------- | ------------------------------------------ | ----------------------- | -----------------|
| `send` | `/api/email/version/3/do/send` | `user_key, api_key, list_ids[], campaign_id, (email_template_id OR (text_content, name, subject, & ((from_email & from_name) OR from_user_id)))` | Sends an email to all the prospects in a list identified by `list_ids[]` |

## [](#supported-parameters-)Supported Parameters

| Parameter              | Required         | Type                                                                | Description |
|------------------------|------------------|------------------------------------------------------------------------|-------------|
| user_key | x | string | Your API user key. Required for all API requests. |
| api_key | x | string | Your api_key. Provided by authentication request. Required for all API requests. |
| campaign_id | x | integer | The id of the campaign you'd like this email associated with. |
| from_name | x** | string | The name of the sending user. |
| from_email | x** | string | The email of the sending user. |
| from_user_id | x** | string | The user id of the sending user. |
| from_assigned_user | | boolean | If the prospect has an assigned user, send the email from that user. |
| from_account_owner | | boolean | If the prospect has an account owner, send the email from that user. |
| replyto_email |  | string | The email address where replies should be sent. |
| list_ids[] | x | integer | The id of the list you'd like to mail to. You can post multiple list_ids[] for multiple lists |
| suppression_list_ids[] |  | integer | The id of the list you'd like to suppress mailing to. You can post multiple suppression_list_ids[] for multiple lists. |
| tags[] |  | string | The name of the tag you'd like to create or associate with this email. You can post multiple tags[] for multiple tags. |
| operational_email |  | boolean | When set, the email will be sent to the prospect regardless of opt-out status. Your account must have this feature enabled to use this setting. |
| name | x* | string | The name of the email within Pardot. |
| subject | x* | string | The subject of the email. |
| text_content | x* | string | The text body of the email. This must contain either %%unsubscribe%% or %%email_preference_center%%. |
| html_content |  | string | The html body of the email. This must contain either %%unsubscribe%% or %%email_preference_center%%. |
| email_template_id | x*** | integer | The id of the email template to use. |
| scheduled_time | | ISO8601 string | The ISO8601 date and time which the email should be sent. |
| format |  | (xml or json) | The format which the response will be sent. Xml is default. |

\* field is required if an `email_template_id` is not
provided.

** (`from_email` &amp; `from_name`) or `from_user_id` is required if an `email_template_id` is not provided.

*** if provided, the email template will be used first, then `name`, `from_assigned_user`, `replyto_email`, `subject`, `text_content`, and `html_content` will override the template contents if they're provided.

## [](#example-requests-)Example Requests

This API request example made with cURL, will schedule an email based on a template to be sent on October 31st at 5pm GMT-4 to 4 prospect lists with 2 suppression lists. It will be sent from the assigned user, if one is assigned, and it also assigns 3 tags to the email.

```
curl https://pi.pardot.com/api/email/version/3/do/send \
--data-urlencode user_key={user_key} \
--data-urlencode api_key={api_key} \
--data-urlencode campaign_id=54321 \
--data-urlencode from_assigned_user=1 \
--data-urlencode email_template_id=6789 \
--data-urlencode list_ids[]=123 \
--data-urlencode list_ids[]=456 \
--data-urlencode list_ids[]=789 \
--data-urlencode list_ids[]=101 \
--data-urlencode suppression_list_ids[]=987 \
--data-urlencode suppression_list_ids[]=654 \
--data-urlencode tags[]=new_prospect_email \
--data-urlencode tags[]=cart_abandoned \
--data-urlencode tags[]=subtotal_over_200 \
--data-urlencode scheduled_time=2013-10-31T17:00:00-0400 \
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
| `<email>` | Parent tag. Contains data fields for target email. For complete field listing, see [email](object-field-references#email) in [Object Field References](object-field-references). |
