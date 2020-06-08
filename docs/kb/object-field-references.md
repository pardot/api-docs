# Object Field References

Each field returned by the API maps to a field within the Pardot user interface. The tables in this section list all fields that can be returned and/or updated via the API. Consider the following limitations:

+ Fields marked as 'Editable' can be manipulated through `create`, `update`, and `upsert` requests.
+ 'Required' denotes that the specified field can't be left without a value during `insert` and some `upsert` requests. `update` requests that clear a required field are declined.
* During `update` requests, the parameter names submitted to the API and tag names in the API's response match field names within the Pardot user interface unless otherwise specified.


## Account

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|||Pardot ID for this account|
|&lt;level&gt;|string|||The level of product for the account|
|&lt;website&gt;|string|||Account website|
|&lt;vanity_domain&gt;|string|||Custom vanity domain name|
|&lt;plugin_campaign_id&gt;|integer|||Plugin ID for account campaign|
|&lt;tracking_code_template&gt;|string|||Markup and code for use in tracking templates|
|&lt;address1&gt;|string|||Account contact address, line 1|
|&lt;address2&gt;|string|||Account contact address, line 2|
|&lt;city&gt;|string|||Account contact city|
|&lt;state&gt;|string|||Account contact state|
|&lt;territory&gt;|string|||Account contact territory|
|&lt;zip&gt;|integer|||Account contact zip code|
|&lt;country&gt;|string|||Account contact country (full string)|
|&lt;phone&gt;|string|||Account contact phone number|
|&lt;fax&gt;|string|||Account contact fax number|


## Campaign

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this campaign|
|&lt;name&gt;|string||X|Campaign's name|
|&lt;cost&gt;|integer||X|Cost associated to the campaign|

## Custom Field

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this custom field|
|&lt;name&gt;|string||X|Custom field's name|
|&lt;field_id&gt;|string|||API ID for custom field|
|&lt;type&gt;|string||X|type of field|
|&lt;type_id&gt;|integer|||Pardot ID for custom field's type|
|&lt;created_at&gt;|timestamp|||Time custom field is created in Pardot; Time is reported in API user's preferred timezone|
|&lt;updated_at&gt;|timestamp|||Last time custom field was updated; Time is reported in API user's preferred timezone|
|&lt;is_record_multiple_responses&gt;|boolean||X|If true, this custom field will record multiple responses|
|&lt;crm_id&gt;|string||X|The CRM ID of the field you want to map to this custom field|
|&lt;is_use_values&gt;|boolean||X|If true, this custom field uses predefined values|


## Custom Redirect

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this custom redirect|
|&lt;name&gt;|string|||Custom redirect's name|
|&lt;Url&gt;|string|||URL for the custom redirect|
|&lt;destination&gt;|string|||URL the custom redirect leads to|
|&lt;campaign&gt;|string|||The campaign associated with this custom redirect|
|&lt;created_at&gt;|timestamp|||Time custom redirect is created in Pardot; Time is reported in API user's  preferred timezone|
|&lt;updated_at&gt;|timestamp|||Last time custom redirect was updated; Time is reported in API user's preferred timezone|


## Dynamic Content

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this dynamic content|
|&lt;name&gt;|string|||Dynamic content's name|
|&lt;embedCode&gt;|string|||Code to embed this dynamic content onto your webpage|
|&lt;embedUrl&gt;|string|||URL to embed this dynamic content|
|&lt;baseContent&gt;|string|||The default dynamic content|
|&lt;basedOn&gt;|string|||Field that this dynamic content is based on|
|&lt;variation&gt;|node|||The variation of content prospect will see based on the field's value<br>**Note:** Information about a variation is returned in a &lt;variation&gt; node in the XML response.  It contains the value of the field in the &lt;comparison&gt; tag and the content of the variation in the &lt;content&gt; tag|
|&lt;created_at&gt;|timestamp|||Time dynamic content is created in Pardot; Time is reported in API user's preferred timezone|
|&lt;updated_at&gt;|timestamp|||Last time dynamic content was updated; Time is reported in API user's preferred timezone|


## Email

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this email|
|&lt;name&gt;|string|||Name of this email|
|&lt;subject&gt;|string|||Email Subject|
|&lt;message&gt;|XML Object|||Contains text and html elements of different formats|
|&lt;created_at&gt;|Timestamp|||Time the Email is created|



## Email Clicks

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this email click|
|&lt;prospect_id&gt;|integer|||Pardot ID for the associated prospect|
|&lt;url&gt;|string|||URL of the email click|
|&lt;list_email_id&gt;|integer|||Pardot ID for the associated list email. Value not present if null.|
|&lt;drip_program_action_id&gt;|integer|||Pardot ID for the associated drip program action. Value not present if null.|
|&lt;email_template_id&gt;|integer|||Pardot ID for the associated email template. Value not present if null.|
|&lt;tracker_redirect_id&gt;|integer|||Pardot ID for the associated tracker redirect. Value not present if null.|
|&lt;created_at&gt;|timestamp|||Time that email click occurs; Time is reported in API user's preferred timezone|


## Form

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this form|
|&lt;name&gt;|string|||Form's name|
|&lt;campaign_id&gt;|string|||Pardot ID of the campaign associated with this form|
|&lt;embed_code&gt;|string|||The code used to embed the form on your webpage|
|&lt;created_at&gt;|timestamp|||Time form is created in Pardot; Time is reported in API user's    preferred timezone|
|&lt;updated_at&gt;|timestamp|||Last time form was updated; Time is reported in API user's    preferred timezone|


## Identified Company

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this identified company|
|&lt;name&gt;|string|||Identified Company's name|
|&lt;street_address&gt;|string|||Identified Company's street address|
|&lt;city&gt;|string|||Identified Company's city|
|&lt;state&gt;|string|||Identified Company's state|
|&lt;postal_code&gt;|string|||Identified Company's postal code|
|&lt;country&gt;|string|||Identified Company's country|
|&lt;email&gt;|string|||Identified Company's email address|


## Lifecycle History

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID of this lifecycle history|
|&lt;prospect_id&gt;|integer|||Pardot's ID for the prospect in this stage|
|&lt;previous_stage_id&gt;|integer|||Pardot ID of the stage this prospect previously was in|
|&lt;next_stage_id&gt;|integer|||Pardot ID of the stage this prospect is in next|
|&lt;seconds_elapsed&gt;|integer|||Number of seconds for prospect to get to current stage|
|&lt;created_at&gt;|timestamp|||Time lifecycle history is created in Pardot; Time is reported in API user's preferred timezone|


## Lifecycle Stage

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID of this lifecycle stage|
|&lt;name&gt;|string|||Lifecycle stage's name|
|&lt;position&gt;|integer|||Lifcycle stage's position in lifecycle|
|&lt;is_locked&gt;|boolean|||If true, lifecycle stage is locked|


## List

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID of this list|
|&lt;name&gt;|string||X|List's name (internal to Pardot)|
|&lt;is_public&gt;|boolean||X|If true, list will show on EPC pages to prospects|
|&lt;is_dynamic&gt;|boolean|||If true, list has prospects dynamically added to it via a set of chosen rules|
|&lt;title&gt;|string||X|List's title (visible to subscribers)|
|&lt;description&gt;|string||X|List's description|
|&lt;is_crm_visible&gt;|boolean||X|If true, list is visible in CRM to add or remove from|
|&lt;created_at&gt;|timestamp|||Time list is created in Pardot; Time is reported in API user's preferred timezone|
|&lt;updated_at&gt;|timestamp|||Last time list was updated; Time is reported in API user's preferred timezone|


## List Membership

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this list membership|
|&lt;list_id&gt;|integer|X||Pardot ID of the list for this membership|
|&lt;prospect_id&gt;|integer|X||Pardot ID of the prospect for this membership|
|&lt;opted_out&gt;|integer||X|If value is 1, the prospect is unsubscribed from receiving emails from this list|
|&lt;created_at&gt;|timestamp|||Time that this membership is created in Pardot; Time is reported in API user's preferred timezone|
|&lt;updated_at&gt;|timestamp|||Last time that this membership was updated; Time is reported in API user's preferred timezone|

## Opportunity

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this opportunity|
|&lt;campaign_id&gt;|integer|X|X|Pardot ID of the campaign associated with this opportunity<br>**Note**: Information about an opportunity's campaign association is returned in a &lt;campaign&gt; node in the XML response. However, updates to campaign associations are made by providing campaign_id=&lt;campaign_id&gt; during an UPDATE&gt; request. See [XML Response Formats](/kb/api-version-4/opportunities#xml-response-formats) in [Using Opportunities](/kb/api-version-4/opportunities#using-opportunities) for more details.|
|&lt;name&gt;|string|X|X|Opportunity's name|
|&lt;value&gt;|float|X|X|Opportunity's value <br>**Restrictions**: value must be a positive numeric value|
|&lt;probability&gt;|integer|X|X|Opportunity's probability <br>**Restrictions**: value must be a positive numeric value between 0 and 100 inclusive|
|&lt;type&gt;|string||X|Opportunity's type|
|&lt;stage&gt;|string||X|Opportunity's stage|
|&lt;status&gt;|string||X|Opportunity's status <br>**Restrictions**: status must be either won, lost, or open|
|&lt;closed_at&gt;|timestamp||X|Opportunity's closed date<br>**Note**: if this is left blank, the closed_at timestamp (Closed Date within the app) is not set, even when the Opportunity's stage, status or probability are set to indicate opportunity closure|
|&lt;created_at&gt;|timestamp|||Time opportunity is created in Pardot; Time is reported in API user's preferred timezone|
|&lt;updated_at&gt;|timestamp|||Last time opportunity was updated in Pardot; Time is reported in API user's preferred timezone|


## Profile

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this profile|
|&lt;name&gt;|string|||Profile's name|


## Profile Criteria

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this profile criteria|
|&lt;name&gt;|string|||Profile criteria's name|
|&lt;matches&gt;|string||X|The matching status of this profile criteria with the current prospect<br>**Restrictions:** Updates can be performed by using the values match, nomatch, or unknown|


## Prospect

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this prospect|
|&lt;campaign_id&gt;|integer||X|Pardot ID of the campaign associated with this prospect<br>**Note**: Information about a prospect's campaign association is returned in a &lt;campaign&gt; node in the XML response. However, updates to campaign associations are made by providing campaign_id=&lt;campaign_id&gt; during an &lt;UPDATE&gt; request. See [XML Response Formats](/kb/api-version-4/prospects/#xml-response-format) in [Using Prospects](/kb/api-version-4/prospects#using-prospects) for more details.|
|&lt;salutation&gt;|string||X|Prospect's formal prefix|
|&lt;first_name&gt;|string||X|Prospect's first name|
|&lt;last_name&gt;|string||X|Prospect's last name|
|&lt;email&gt;|string|X|X|Prospect's email address|
|&lt;password&gt;|string||X|Prospect's password|
|&lt;company&gt;|string||X|Prospect's company|
|&lt;prospect_account_id&gt;|integer||X|Prospect's account ID|
|&lt;website&gt;|string||X|Prospect's website URL|
|&lt;job_title&gt;|string||X|Prospect's job title|
|&lt;department&gt;|string||X|Prospect's department|
|&lt;country&gt;|string||X|Prospect's country|
|&lt;address_one&gt;|string||X|Prospect's address, line 1|
|&lt;address_two&gt;|string||X|Prospect's address, line 2|
|&lt;city&gt;|string||X|Prospect's city|
|&lt;state&gt;|string||X|Prospect's US state|
|&lt;territory&gt;|string||X|Prospect's territory|
|&lt;zip&gt;|string||X|Prospect's postal code|
|&lt;phone&gt;|string||X|Prospect's phone number|
|&lt;fax&gt;|string||X|Prospect's fax number|
|&lt;source&gt;|string||X|Prospect's source|
|&lt;annual_revenue&gt;|string||X|Prospect's annual revenue|
|&lt;employees&gt;|string||X|Prospect's number of employees|
|&lt;industry&gt;|string||X|Prospect's industry|
|&lt;years_in_business&gt;|string||X|Prospect's number of years in business|
|&lt;comments&gt;|string||X|Comments about this prospect|
|&lt;notes&gt;|string||X|Notes about this prospect|
|&lt;score&gt;|integer||X|Prospect's score|
|&lt;grade&gt;|string|||Prospect's letter grade|
|&lt;last_activity_at&gt;|timestamp|||Time stamp of this prospect's latest visitor activity; Time is reported in API user's preferred timezone|
|&lt;recent_interaction&gt;|string|||Describes the prospect's most recent interaction with Pardot|
|&lt;crm_lead_fid&gt;|string|||Prospect's lead ID in a supported CRM system|
|&lt;crm_contact_fid&gt;|string|||Prospect's contact ID in a supported CRM system|
|&lt;crm_owner_fid&gt;|string|||Prospect's owner ID in a supported CRM system|
|&lt;crm_account_fid&gt;|string|||Account ID in a supported CRM system|
|&lt;crm_last_sync&gt;|timestamp|||Last time this prospect was synced with a supported CRM system|
|&lt;crm_url&gt;|string|||URL to view the prospect within the CRM system|
|&lt;is_do_not_email&gt;|boolean||X|If value is 1, prospect prefers not to be emailed|
|&lt;is_do_not_call&gt;|boolean||X|If value is 1, prospect prefers not to be called|
|&lt;opted_out&gt;|boolean|||If value is 1, prospect has opted out of marketing communications|
|&lt;is_reviewed&gt;|boolean||X|If value is 1, prospect has been reviewed|
|&lt;is_starred&gt;|boolean||X|If value is 1, prospect has been starred|
|&lt;is_archived&gt;|boolean||X|If value is 1, prospect has been archived|
|&lt;created_at&gt;|timestamp|||Time prospect is created in Pardot; Time is reported in API user's preferred timezone|
|&lt;updated_at&gt;|timestamp|||Last time prospect was updated in Pardot; Time is reported in API user's preferred timezone|


## Prospect Account

**Note:** Prospect account fields are fully customizable. To get the
most accurate field metadata for your Pardot account, use the
describe operation on the prospectAccount API endpoint.

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID of the prospect account|
|&lt;name&gt;|string|X||The name prospect account|

## Tag

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this tag|
|&lt;name&gt;|string|||Tag's name|
|&lt;created_at&gt;|timestamp|||Time tag is created in Pardot; Time is reported in API user's preferred timezone|
|&lt;updated_at&gt;|timestamp|||Last time tag was updated; Time is reported in API user's        preferred timezone|


## Tag Object

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID of the tag object|
|&lt;tag_id&gt;|integer|||The Pardot ID of the tag|
|&lt;type&gt;|string|||The type of object associated with the tag|
|&lt;object_id&gt;|integer|||The Pardot ID of the object|
|&lt;created_at&gt;|timestamp|||Time tag is associated with the object in Pardot; Time is reported in API user's preferred timezone|


## User

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID of the user|
|&lt;email&gt;|string|||User's email address|
|&lt;first_name&gt;|string|||User's first name|
|&lt;last_name&gt;|string|||User's last name|
|&lt;job_title&gt;|string|||User's job title|
|&lt;role&gt;|string|||User's role|
|&lt;created_at&gt;|timestamp|||Time user is created in Pardot; Time is reported in the API user's preferred timezone|
|&lt;updated_at&gt;|timestamp|||Last time user was updated in Pardot; Time is reported in the API user's preferred timezone|


## Visit

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|||Pardot ID for this visit|
|&lt;visitor_id&gt;|integer|||Pardot ID for the associated visitor|
|&lt;prospect_id&gt;|integer|||Pardot ID for the associated prospect|
|&lt;visitor_page_view_count&gt;|integer|||Number of page views for this visit|
|&lt;first_visitor_page_view_at&gt;|timestamp|||Time of first page view for this visit; Time is reported in API user's preferred timezone|
|&lt;last_visitor_page_view_at&gt;|timestamp|||Time of last page view for this visit; Time is reported in API user's preferred timezone|
|&lt;duration_in_seconds&gt;|integer|||Length of this visit|
|&lt;campaign_parameter&gt;|string|||Visit's campaign parameter utm_campaign from Google Analytics|
|&lt;medium_parameter&gt;|string|||Visit's medium parameter utm_medium from Google Analytics|
|&lt;source_parameter&gt;|string|||Visit's source parameter utm_source from Google Analytics|
|&lt;content_parameter&gt;|string|||Visit's content parameter utm_content from Google Analytics|
|&lt;term_parameter&gt;|string|||Visit's term parameter utm_term from Google Analytics|
|&lt;created_at&gt;|timestamp|||Time visit is created in Pardot; Time is reported in API user's preferred timezone|
|&lt;updated_at&gt;|timestamp|||Last time visit was updated in Pardot; Time is reported in API user's preferred timezone|

## Visitor

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this visitor|
|&lt;page_view_count&gt;|integer|||Number of page views by this visitor|
|&lt;ip_address&gt;|string|||Visitor's IP address|
|&lt;hostname&gt;|string|||Visitor's hostname|
|&lt;campaign_parameter&gt;|string|||Visitor's campaign parameter utm_campaign from Google Analytics|
|&lt;medium_parameter&gt;|string|||Visitor's medium parameter utm_medium from Google Analytics|
|&lt;source_parameter&gt;|string|||Visitor's source parameter utm_source from Google Analytics|
|&lt;content_parameter&gt;|string|||Visitor's content parameter utm_content from Google Analytics|
|&lt;term_parameter&gt;|string|||Visitor's term parameter utm_term from Google Analytics|
|&lt;created_at&gt;|timestamp|||Time visitor is created in Pardot; Time is reported in API user's preferred timezone|
|&lt;updated_at&gt;|timestamp|||Last time visitor was updated in Pardot; Time is reported in API user's preferred timezone|


## Visitor Activity

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this visitor activity|
|&lt;prospect_id&gt;|integer|||Pardot ID for the associated prospect|
|&lt;visitor_id&gt;|integer|||Pardot ID for the associated visitor|
|&lt;type&gt;|integer|||Visitor activity's type number; See listing below|
|&lt;type_name&gt;|string|||Visitor activity's type name; See listing below|
|&lt;details&gt;|string|||Details about this visitor activity such as the name of the object associated with this activity, the search phrase used in a site search query, etc.|
|&lt;email_id&gt;|integer|||Pardot ID of the email associated with this visitor activity<br>**Note:** This node appears only if this visitor activity has an email associated with it|
|&lt;email_template_id&gt;|integer|||Pardot ID of the email template associated with this visitor activity<br>**Note:** This node appears only if this visitor activity has an email associated with it|
|&lt;list_email_id&gt;|integer|||Pardot ID of the list email associated with this visitor activity<br>**Note:** This node appears only if this visitor activity has an email associated with it|
|&lt;form_id&gt;|integer|||Pardot ID of the form associated with this visitor activity<br>**Note:** This node appears only if this visitor activity has a form associated with it|
|&lt;form_handler_id&gt;|integer|||Pardot ID of the form handler associated with this visitor activity<br>**Note:** This node appears only if this visitor activity has a form handler associated with it|
|&lt;site_search_query_id&gt;|integer|||Pardot ID of the site search query associated with this visitor activity<br>**Note:** This node appears only if this visitor activity has a site search query associated with it|
|&lt;landing_page_id&gt;|integer|||Pardot ID of the landing page associated with this visitor activity<br>**Note:** This node appears only if this visitor activity has a landing page associated with it|
|&lt;paid_search_ad_id&gt;|integer|||Pardot ID of the paid search ad associated with this visitor activity <br>**Note:** This node appears only if this visitor activity has a paid search ad associated with it|
|&lt;multivariate_test_variation_id&gt;|integer|||Pardot ID of the multivariate test variation associated with this visitor activity<br>**Note:** This node appears only if this visitor activity has a multivariate test variation associated with it|
|&lt;visitor_page_view_id&gt;|integer|||Pardot ID of the visitor page view associated with this visitoractivity<br>**Note:** This node appears only if this visitor activity has a visitor page view associated with it|
|&lt;file_id&gt;|integer|||Pardot ID of the file associated with this visitor activity<br>**Note:** This node appears only if this visitor activity has a file associated with it|
|&lt;custom_redirect_id&gt;|integer|||Pardot ID of the custom redirect associated with this visitor activity Note: This node appears only if this visitor activity has a custom redirect associated with it|
|&lt;campaign&gt;|object|||Campaign information including id, name, and cost.|
|&lt;created_at&gt;|timestamp|||Time that visitor activity occurred; Time is reported in API user's preferred timezone|
|&lt;updated_at&gt;|timestamp|||Time that visitor activity update occurred; Time is reported in API user's preferred timezone|

<a name="visitor-activity-types" id="visitor-activity-types"></a>Visitor Activities may have the following values for
<code>&lt;type&gt;</code>

+ 1 - Click
+ 2 - View
+ 3 - Error
+ 4 - Success
+ 5 - Session
+ 6 - Sent
+ 7 - Search
+ 8 - New Opportunity
+ 9 - Opportunity Won
+ 10 - Opportunity Lost
+ 11 - Open
+ 12 - Unsubscribe Page
+ 13 - Bounced
+ 14 - Spam Complaint
+ 15 - Email Preference Page
+ 16 - Resubscribed
+ 17 - Click (Third Party)
+ 18 - Opportunity Reopened
+ 19 - Opportunity Linked
+ 20 - Visit
+ 21 - Custom URL click
+ 22 - Olark Chat
+ 23 - Invited to Webinar
+ 24 - Attended Webinar
+ 25 - Registered for Webinar
+ 26 - Social Post Click
+ 27 - Video View
+ 28 - Event Registered
+ 29 - Event Checked In
+ 30 - Video Conversion
+ 31 - UserVoice Suggestion
+ 32 - UserVoice Comment
+ 33 - UserVoice Ticket
+ 34 - Video Watched (≥ 75% watched)
+ 35 - Indirect Unsubscribe Open
+ 36 - Indirect Bounce
+ 37 - Indirect Resubscribed
+ 38 - Opportunity Unlinked
+ Other - Unknown


## Visitor Page View

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|||Pardot ID for this visitor page view|
|&lt;url&gt;|string|||Page view URL|
|&lt;title&gt;|string|||Page title|
|&lt;created_at&gt;|timestamp|||Time page view occurred; Time is reported in API user's preferred timezone|

## Visitor Referrer

|Field Name|Data Type|Required|Editable|Description|
|--- |--- |--- |--- |--- |
|&lt;id&gt;|integer|X||Pardot ID for this visitor referrer|
|&lt;referrer&gt;|string|||Referrer's URL|
|&lt;vendor&gt;|string|||Referrer's vendor (such as 'Google' or 'Yahoo')|
|&lt;type&gt;|string|||Referrer's type (such as 'Natural Search')|
|&lt;query&gt;|string|||Referrer's search query|
