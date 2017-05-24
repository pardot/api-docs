# Release Notes

This page contains the release notes for the Pardot API and related documentation.

## May 2017

### Prospects
* fixed various broken links in the documentation.
* fixed bug where the error array in the version 4 batch endpoints response was not correctly indexed.
* added information explaining the error response when using batch actions in v4.

## April 2017

### Prospects

`read` end-point (v4):

* This update will bring the v4 read end point into sync with the v3 end point. Archived prospects previously included in `read` responses will now be excluded when `email` is used to identify the target prospect.

## March 2017

### Visitor Activities 

`query` end-point (v3-4):

* any email activity that is related to an email list will now include the list_email_id
* any email activity that is related to an email generated from an email template will include the email_template_id
* [filter visitor activities by various object types](api-version-4/visitor-activities/#supported-search-criteria):
	* custom_url_only
	* email_only
	* file_only
	* form_only
	* form_handler_only
	* landing_page_only

#### Email

* when using the `read` end-point, you can exclude the email text and HTML body message from the response by setting [include_message](api-version-4/emails/#supported-parameters) to false.


#### Prospect
* `prospect_account_id` field is now returned by default on `query` API calls. This includes calls made with the `output`=`bulk` parameter.
#### Other

Mentions of default value: `id` for the `sort_by` query parameter have been removed from API documentation for clarity.
