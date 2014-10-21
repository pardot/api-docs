# API (version 3) - Overview


The Pardot API allows your application to access current data within Pardot.  Through the API, several common operations can be performed on Pardot objects.  Operations include:

*   `create` -- Creates a new object with the specified parameters.
*   `read` -- Retrieves information about the specified object.
*   `query` -- Retrieves objects that match specified criteria.
*   `update` -- Updates elements of an existing object.
*   `upsert` -- Updates elements of an existing object if it exists.  If the object does not exist, one is created using the supplied parameters.

Developers must authenticate with the API before issuing requests.  Refer to the [Authentication](../authentication) section for details about this procedure.  For more information about proper request syntax, see the [Using the Pardot API](../using-the-pardot-api) section.

Some considerations must be taken while performing requests. When performing `update` requests, only the fields specified in the request are updated, and all others are left unchanged.  If a required field is cleared during an `update`, the request will be declined.

Objects available through the API correspond to objects within the Pardot user interface.  These objects may include:

*   [Opportunities](../using-opportunities)
*   [Prospects](../using-prospects)
*   [Users](../using-users)
*   [Visitors](../using-visitors)
