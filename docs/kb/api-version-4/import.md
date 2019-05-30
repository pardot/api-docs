Copy text from version 3 when final and modify as needed.

### Matching & Upsert behavior

If a row in the CSV file can be matched to an existing prospect, all fields specified will be updated. If a matching prospect cannot be found, a new prospect will be created. Any field that is left blank will be overwritten with NULL. All standard and custom fields are supported.

In API Version 4, you must specify either the "prospect_id" or "salesforce_fid" identifier (Salesforce ID of a synced prospect). If you don't specify an identifier, or the prospect that is matched is in the recycle bin, that record won't be upserted unless the restoreDeleted option was specified during import creation. The rest of the import isn't affected when a record is skipped.

Copy text from version 3 when final and modify as needed.
