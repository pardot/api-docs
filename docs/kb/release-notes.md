# Release Notes

This page contains the release notes for the Pardot API and related documentation.

## March 2017

### Visitor Activities 

`query` end-point (v3-4):

* any email activity that is related to an email list will now include the list_email_id
* any email activity that is related to an email generated from an email template, will include the email_template_id
* [filter visitor activities by various object types](api-version-4/visitor-activities/#supported-search-criteria):
	* custom_url_only
	* email_only
	* file_only
	* form_only
	* form_handler_only
	* landing_page_only

#### Email

* when using the `read` end-point, you can exclude the email text and HTML body message from the response by setting [include_message](api-version-4/emails/#supported-parameters) to false.

#### Other

Mentions of default value: `id` for the `sort_by` query parameter have been removed from API documentation for clarity.
