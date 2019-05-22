Copy text from version 3 when final and modify as needed.

### Matching & Upsert behavior

If a row in the CSV file can be matched to an existing prospect, all fields specified will be updated. If a matching prospect cannot be found, a new prospect will be created. Any field that is left blank will be overwritten with NULL. All standard and custom fields are supported.

In API Version 4, an identifier **must** be specified, either “prospect_id” or “salesforce_fid” (Salesforce ID of a synced prospect). If no identifier is specified, OR if the prospect that is matched is in the recycle bin, that record will fail to upsert unless the restoreDeleted option was specified during import creation. The rest of the import will continue processing.

Copy text from version 3 when final and modify as needed.
