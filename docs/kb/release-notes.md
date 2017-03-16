# Release Notes

Here you'll find the latest updates on what's changed in the Pardot API and API documentation.

## March 2017

### Visitor Activities 

A few updates where made to the `query` endpoint for both version 3 and 4. These include:

* any email activity that is part of an email list will now include the list_email_id
* any email activity that belongs to an email which used an email template, will include the email_template_id
* new filters are available to query visitor activities by [object type](api-version-4/visitor-activities/#supported-search-criteria):
	* custom_url_only
	* email_only
	* file_only
	* form_only
	* form_handler_only
	* landing_page_only

#### Email

* when using the `read` endpoint, you can now remove the email text and html body message from the response by setting [include_message](api-version-4/emails/#supported-parameters) to false.

#### Other

In the documents under the "Manipulating the Result Set" section for many of the objects, it was identified the `sort_by` 
parameter incorrectly stated the default sort by option was id. We removed that statement as you'll want to specify what 
you want to sort by depending on your needs. 
