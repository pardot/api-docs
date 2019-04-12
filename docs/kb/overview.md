# Pardot API Documentation

Welcome!

## Overview

The Pardot API allows your application to access current data within Pardot. Through the API, several common operations can be performed on Pardot objects. Operations include:

*   `create` -- Creates a new object with the specified parameters.
*   `read` -- Retrieves information about the specified object.
*   `query` -- Retrieves objects that match specified criteria.
*   `update` -- Updates elements of an existing object.
*   `upsert` -- Updates elements of an existing object if it exists.  If the object does not exist, one is created using the supplied parameters.

Developers must authenticate with the API before issuing requests.  Refer to the [Authentication](kb/api-version-3/authentication) section for details about this procedure. For more information about proper request syntax, see the [Using the Pardot API](kb/api-version-3/using-the-pardot-api) section.

Some considerations must be taken while performing requests. When performing `update` requests, only the fields specified in the request are updated, and all others are left unchanged. If a required field is cleared during an `update`, the request will be declined.

## Authentication

A few prerequisites must be met to successfully authenticate a
connection to the API.

1.  All requests to the Pardot API must be made via SSL encrypted
connection.
2.  Authentication requests must use HTTP POST.
3.  Obtain the `email`, `password`, and `user_key` (available in Pardot under **{your email address} > Settings** in the API User Key row) for the Pardot user account that will be submitting API requests. If you need assistance in acquiring your user key, contact your Pardot support representative.

With these requirements met, an API key must be acquired. Both User and API keys are unique to individual users. API keys are valid for 60 minutes. In contrast, user keys are valid indefinitely. To authenticate, issue the following request (having replaced the values denoted by `<carets>` with values for your account):

```
POST: https://pi.pardot.com/api/login/version/3
message body: email=<email>&password=<password>&user_key=<user_key>
```

| **Parameter** | **Required**   | **Description**                                        |
| ------------- | :------------: | ----------------------------------------------------- |
| `email`       | X              | The email address of your user account                 |
| `password`    | X              | The password of your user account                      |
| `user_key`    | X              | The 32-bit hexadecimal user key for your user account  |

If authentication was successful, a 32-character hexadecimal API
key will be returned in the following format:

```
<rsp stat="ok" version="1.0">
    <api_key>5a1698a233e73d7c8ccd60d775fbc68a</api_key>
</rsp>
```

Otherwise, the response will contain the following:

```
<rsp stat="fail" version="1.0">
    <err code="15">Login failed</err>
</rsp>
```

Subsequent authentication requests will return either the current valid API key or a newly generated API key if the previous one had expired.


## Using the API

The Pardot API handles a variety of requests for many of the
objects available through the Pardot user interface. Most requests
to the API use the following standardized format. All requests must
use either HTTP GET or POST. Although GET requests are secure due
to the use of SSL, we recommend using POST, with sensitive or
lengthy parameter values being part of the POST message body.
Developers are responsible for issuing requests with the following
components:

```
POST: https://pi.pardot.com/api/<object>/version/3/do/<operator>/<identifier_field>/<identifier>
message body: api_key=<your_api_key>&user_key=<your_user_key>&<parameters_for_request>

GET: https://pi.pardot.com/api/<object>/version/3/do/<operator>/<identifier_field>/<identifier>?api_key=<your_api_key>&user_key=<your_user_key>&<parameters_for_request>
```

| **Parameter** | **Required**   | **Description**                                        |
| ------------- | :------------: | ----------------------------------------------------- |
| `object`       | X              | The object type to be returned by the API request                |
| `operator`    | X              | The operation to be performed on the specified object type                    |
| `identifier_field`    | X              | The field to be used as the identifier for the specified object  |
| `identifier`       | X              | The identifier for the specified object(s)              |
| `your_api_key`    | X              | The API key that was obtained during [Authentication](kb/api-version-3/authentication)                   |
| `your_user_key`    | X              | The user key that was used during [Authentication](kb/api-version-3/authentication)  |
| `format`    |               | The API data format. Either xml or json (xml is default)                   |
| `parameters_for_request`    |               | Parameters specific to your request; See the articles listed under [Using the Pardot API](kb/api-version-3/using-the-pardot-api) in the [Table of Contents](kb/api-version-3/intro-and-table-of-contents#contents) |

The ordering of parameters is arbitrary. Parameters are passed using conventional HTML parameter syntax, with `'?'` indicating the start of the parameter string (for GET requests only) and `'&'` as the separator between parameters. With the exception of `<format>` and `<parameters_for_request>`, all components are required. Data returned from the API is formatted using JSON or XML 1.0 with UTF-8 character encoding. Keep in mind that some characters in the response may be encoded as HTML entities, requiring client-side decoding. Also, keep in mind that all parameters specified in an API request MUST be URL-encoded before they are submitted.

In general, the API will return XML or JSON containing a current version of the target object's data. However, unsuccessful requests will return a short response containing an error code and message. See [Error Codes &amp; Messages](kb/api-version-3/error-codes-and-messages) for error descriptions and suggested remedies.

<a name="14767-changing-xml-response-format" id=
"changing-xml-response-format"></a>

## Changing the API Response Format

The Pardot API supports several output formats, each of which returns different levels of detail in the XML or JSON response. Output formats are defined by specifying the `output` request parameter. Supported output formats include:

*   `full` -- Returns all supported data for the Pardot object and all objects associated with it.
*   `simple` -- Returns all supported data for the data for the Pardot object.
*   `mobile` -- Returns an abbreviated version of the object data. This output format is ideal for mobile applications.
*   `bulk` -- Returns basic data for an object (does not provide total object count). Used for querying [large amounts of data](kb/bulk-data-pull/). 

If the output request parameter is not defined, the output format defaults to `full`. See the XML Response Format sections for each object for details about the formats.

## Supported API wrappers

* [ruby-pardot](https://www.github.com/Pardot/ruby-pardot)
* [pardot-java-client](https://github.com/Crim/pardot-java-client)
