# API (version 3) - Using the Pardot API


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
| `your_api_key`    | X              | The API key that was obtained during [Authentication](../authentication)                   |
| `your_user_key`    | X              | The user key that was used during [Authentication](../authentication)  |
| `format`    |               | The API data format. Either xml or json (xml is default)                   |
| `your_user_key`    |               | Parameters specific to your request; See the articles listed under [Using the Pardot API](../using-the-pardot-api) in the [Table of Contents](../intro-and-table-of-contents#contents) |

The ordering of parameters is arbitrary. Parameters are passed using conventional HTML parameter syntax, with `'?'` indicating the start of the parameter string (for GET requests only) and `'&'` as the separator between parameters. With the exception of `<format>` and `<parameters_for_request>`, all components are required. Data returned from the API is formatted using JSON or XML 1.0 with UTF-8 character encoding. Keep in mind that some characters in the response may be encoded as HTML entities, requiring client-side decoding. Also, keep in mind that all parameters specified in an API request MUST be URL-encoded before they are submitted.

In general, the API will return XML or JSON containing a current version of the target object's data. However, unsuccessful requests will return a short response containing an error code and message. See [Error Codes &amp; Messages](../error-codes-and-messages) for error descriptions and suggested remedies.

<a name="14767-changing-xml-response-format" id=
"changing-xml-response-format"></a>

## Changing the API Response Format

The Pardot API supports several output formats, each of which returns different levels of detail in the XML or JSON response. Output formats are defined by specifying the `output` request parameter. Supported output formats include:

*   `full` -- Returns all supported data for the Pardot object and all objects associated with it.
*   `simple` -- Returns all supported data for the data for the Pardot object.
*   `mobile` -- Returns an abbreviated version of the object data. This output format is ideal for mobile applications.

If the output request parameter is not defined, the output format defaults to `full`. See the XML Response Format sections for each object for details about the formats.
