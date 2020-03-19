# Official Pardot API Documentation

> **IMPORTANT: Support for passing credentials via querystring is deprecated and will return an error response. Please update your API client as soon as possible.**
>
> Refer to the [Using the API > Request Format](#using-the-api) section below for further details.

Welcome! All up-to-date documentation of Pardot's official API is housed here. A few things of note:

* If you have a question about the API, feel free to [open a ticket](https://help.salesforce.com/articleView?id=000181929&type=1) with our Support team.
* To report an inconsistency in the documentation, please [open an issue on GitHub](https://github.com/Pardot/api-docs/issues). [Pull requests](https://github.com/Pardot/api-docs/pulls) are welcome as well!
* If you've written your own library or wrapper for Pardot's API, submit a [pull request](https://github.com/Pardot/api-docs/pulls) updating the `index.md` file with a link to your repository, and we'll be glad to consider linking it up.
* For the latest information on updates to the API and related documentation, refer to the [Release Notes](kb/release-notes).

## Using the API

The Pardot API allows your application to access current data within Pardot. Through the API, several common operations can be performed on Pardot objects. Operations include:

*   `create` -- Creates a new object with the specified parameters.
*   `read` -- Retrieves information about the specified object.
*   `query` -- Retrieves objects that match specified criteria.
*   `update` -- Updates elements of an existing object.
*   `upsert` -- Updates elements of an existing object if it exists.  If the object does not exist, one is created using the supplied parameters.

Developers must authenticate with the API before issuing requests.  Refer to the [Authentication](#authentication) section for details about this procedure.

Some considerations must be taken while performing requests. When performing `update` requests, only the fields specified in the request are updated, and all others are left unchanged. If a required field is cleared during an `update`, the request will be declined.

### Request Format

All requests to the API:

* Must use either HTTP `GET` or `POST`
* Must pass credentials in an HTTP `Authorization` header

#### Sample GET Request

```
GET https://pi.pardot.com/api/<object>/version/3/do/<op>/<id_field>/<id>?<params> HTTP/1.1
Authorization: Pardot api_key=<your_api_key>, user_key=<your_user_key>
```

#### Sample POST Request

```
POST https://pi.pardot.com/api/<object>/version/3/do/<op>/<id_field>/<id> HTTP/1.1
Authorization: Pardot api_key=<your_api_key>, user_key=<your_user_key>

<params>
```

#### Request Parameters

| **Parameter**            | **Required**   | **Description**                                                         |
| ------------------------ | -------------- | ----------------------------------------------------------------------- |
| `object`                 | X              | The object type to be returned by the API request                       |
| `op`                     | X              | The operation to be performed on the specified object type              |
| `id_field`               | X              | The field to be used as the identifier for the specified object         |
| `id`                     | X              | The identifier for the specified object(s)                              |
| `your_api_key`           | X              | The API key that was obtained during [Authentication](#authentication)  |
| `your_user_key`          | X              | The user key that was used during [Authentication](#authentication)     |
| `format`                 |                | The API data format. Either xml or json (xml is default)                |
| `params`                 |                | Parameters specific to your request; See individual methods for details |

The ordering of parameters is arbitrary. Parameters are passed using conventional HTML parameter syntax, with `'?'` indicating the start of the parameter string (for GET requests only) and `'&'` as the separator between parameters. With the exception of `<format>` and `<params>`, all components are required. Data returned from the API is formatted using JSON or XML 1.0 with UTF-8 character encoding. Keep in mind that some characters in the response may be encoded as HTML entities, requiring client-side decoding. Also, keep in mind that all parameters specified in an API request MUST be URL-encoded before they are submitted.

In general, the API will return XML or JSON containing a current version of the target object's data. However, unsuccessful requests will return a short response containing an error code and message. See [Error Codes &amp; Messages](kb/api-version-3/error-codes-messages) for error descriptions and suggested remedies.

<a name="14767-changing-xml-response-format" id="changing-xml-response-format"></a>

## Version 3 and Version 4 differences

In order to accommodate a new feature related to prospects,
we have created a new version of our APIs - version 4.
We are now allowing multiple prospects to share an email address on some Pardot accounts.
Eventually this will be available for all Pardot accounts.
If your account has this feature active now, then you MUST use version 4.
Everyone else can continue using version 3.
Version 4 may use slightly different input syntax where prospects are involved,
and may return multiple prospects where version 3 returned one.
Please check out the appropriate version's documentation for more exact usage details.

If your account uses v4, then upon login to the APIs,
a data tag will be returned as such: `<version>4</version>`.
If your account requires version 3, you will not see this tag.

## Changing the API Response Format

The Pardot API supports several output formats, each of which returns different levels of detail in the XML or JSON response. Output formats are defined by specifying the `output` request parameter. Supported output formats include:

*   `full` -- Returns all supported data for the Pardot object and all objects associated with it.
*   `simple` -- Returns all supported data for the data for the Pardot object.
*   `mobile` -- Returns an abbreviated version of the object data. This output format is ideal for mobile applications.
*   `bulk` -- Returns basic data for an object (does not provide total object count). Used for querying [large amounts of data](kb/bulk-data-pull/).

If the output request parameter is not defined, the output format defaults to `full`. See the XML Response Format sections for each object for details about the formats.

## Authentication

### Request Format

Authentication requests sent to the Pardot API:

1.  Must be made via SSL encrypted connection
2.  Must use HTTP `POST`
3.  Must contain the `email`, `password`, and `user_key` for the Pardot user account that will be submitting API requests

Login requests that meet these criteria will be granted an API key.

API user keys are available in Pardot under **{your email address} > Settings** in the API User Key row. If you need assistance in acquiring your user key, contact your Pardot support representative.

In accounts with [Salesforce User Sync enabled](https://help.salesforce.com/articleView?id=pardot_sf_connector_setup_user_sync_considerations.htm&type=5), you must authenticate with a Pardot-only user. SSO users aren't supported.

> Both User and API keys are unique to individual users. API keys are valid for 60 minutes. In contrast, user keys are valid indefinitely.

#### Sample POST Request

```
POST https://pi.pardot.com/api/login/version/3 HTTP/1.1

email=<email>&password=<password>&user_key=<user_key>
```

#### Request Parameters

| **Parameter** | **Required**   | **Description**                                              |
| ------------- | -------------- | ------------------------------------------------------------ |
| `email`       | X              | The email address of your user account                       |
| `password`    | X              | The password of your user account                            |
| `user_key`    | X              | The 32-character hexadecimal user key for your user account  |

If authentication was successful, a 32-character hexadecimal API key will be returned in the following format:

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

## Rate Limits

We enforce API rate limits in two ways:

* daily requests
* concurrent requests

### Daily Requests

Pardot Pro customers are allocated 25,000 API requests per day. Pardot Ultimate customers can make up to 100,000 API requests a day.
These limits reset at the beginning of the day based on your accounts time zone settings. Any request made exceeding the
limits will result in an [error code 122](/kb/error-codes-messages/#error-code-122)

You can check you current daily usages in the accounts "usage and limits" page.

### Concurrent Requests

In order to interact with our API more efficiently, you can have up to five concurrent API requests. Any connection over five
will result in an [error code 66](/kb/error-codes-messages/#error-code-66) response.

## Sample Code

Here's an example of calling the Pardot API using a simple PHP client using the cURL library.

Note: we strongly recommend **against** using PHP's `file_get_contents` function to call the Pardot API, since it makes error handling extremely cumbersome.

```
<?php

/**
 * Class SamplePardotApiClient
 *
 * Example PHP client to call the Pardot API
 */
class SamplePardotApiClient
{
    const BASE_URL = "https://pi.pardot.com/api/";

    /** @var int $apiVersion */
    private $apiVersion;

    /** @var string $format  */
    private $format;

    public function __construct($apiVersion, $format = 'xml')
    {
        $this->apiVersion = $apiVersion;
        $this->format = $format;
    }

    /**
     * @param string $endpoint
     * @param string $operation
     * @param array $data
     * @param array $headers
     * @param array $queryParams
     * @return array
     * @throws Exception
     */
    public function post($endpoint, $operation, $data = [], $headers = [], $queryParams = [])
    {
        $curl_handle = $this->initRequest($endpoint, $operation, $headers, $queryParams);
        curl_setopt($curl_handle, CURLOPT_POST, true);
        // Add POST data if given
        if (!empty($data)) {
            curl_setopt($curl_handle, CURLOPT_POSTFIELDS, $data);
        }

        return $this->executeCall($curl_handle);
    }

    /**
     * @param string $endpoint
     * @param string $operation
     * @param array $headers
     * @param array $queryParams
     * @return array
     * @throws Exception
     */
    public function get($endpoint, $operation, $headers = [], $queryParams = [])
    {
        $curl_handle = $this->initRequest($endpoint, $operation, $headers, $queryParams);

        return $this->executeCall($curl_handle);
    }

    /**
     * @param string $endpoint
     * @param string $operation
     * @param array $headers
     * @param array $queryParams
     * @return false|resource
     */
    private function initRequest($endpoint, $operation, $headers = [], $queryParams = [])
    {
        // Construct our full URL to the Pardot API
        $url = $this->buildUrl($endpoint, $operation);
        // Add desired format to any query string params provided
        $queryParams['format'] = $this->format;
        // Build query string params into an encoded string
        $queryString = http_build_query($queryParams, null, '&');
        // Append query string params to URL
        $url .= "?{$queryString}";

        // Init curl handle and set standard curl options: timeouts / require SSL / verify SSL
        $curl_handle = curl_init($url);
        curl_setopt($curl_handle, CURLOPT_CONNECTTIMEOUT, 5);
        curl_setopt($curl_handle, CURLOPT_TIMEOUT, 30);
        curl_setopt($curl_handle, CURLOPT_PROTOCOLS, CURLPROTO_HTTPS);
        curl_setopt($curl_handle, CURLOPT_SSL_VERIFYHOST, 2);
        curl_setopt($curl_handle, CURLOPT_RETURNTRANSFER, 1);

        // Add any headers passed in such as Authorization header
        if (!empty($headers)) {
            curl_setopt($curl_handle, CURLOPT_HTTPHEADER, $headers);
        }

        return $curl_handle;
    }

    /**
     * @param string $endpoint
     * @param string $operation
     * @return string
     */
    private function buildUrl($endpoint, $operation = "")
    {
        if ($endpoint === 'login') {
            return self::BASE_URL . "login";
        }

        return self::BASE_URL . "{$endpoint}/version/{$this->apiVersion}/do/{$operation}";
    }

    /**
     * @param $curl_handle
     * @return array
     * @throws Exception
     */
    private function executeCall($curl_handle)
    {
        // Execute our call to the Pardot API
        $rsp = curl_exec($curl_handle);
        // Gather the HTTP response code and last effective URL called
        $httpCode = curl_getinfo($curl_handle, CURLINFO_HTTP_CODE);
        $url = curl_getinfo($curl_handle, CURLINFO_EFFECTIVE_URL);

        // Handle errors in calls, this could be a log or an exception thrown as written here
        if (!$rsp) {
            $errorMessage = curl_error($curl_handle);
            curl_close($curl_handle);
            throw new Exception("Error calling API. HTTP Code: {$httpCode}. Message: {$errorMessage}");
        }
        curl_close($curl_handle);

        // Output call response for informational purposes
        echo("URL: {$url}" . PHP_EOL);
        echo("HTTP Response Code: {$httpCode}" . PHP_EOL);
        echo("Response: {$rsp}" . PHP_EOL . PHP_EOL);

        return [$httpCode, $rsp];
    }

}

// Setup user credentials
$credentials = [
    'user_key' => '12345678890abcdef12345678890abcdef',
    'email' => 'email@example.com',
    'password' => 'pass1234'
];

// Prepare to call version 3 or 4 of the API with JSON or XML responses
$client = new SamplePardotApiClient(3, 'json');

// Authenticate to Pardot - Must be a POST with credentials in the message body
list($httpCode, $rsp) = $client->post('login', '', $credentials, null);
// Capture the api_key from a successful login response
// api_key is good for 1 hour and can be reused on subsequent calls
$apiKey = json_decode($rsp, true)['api_key'];

// Create Authorization Header from api_key
$authHeader = ["Authorization: Pardot user_key={$credentials['user_key']},api_key={$apiKey}"];

// Call Prospect Query
list($httpCode, $rsp) = $client->get('prospect', 'query', $authHeader, ['limit' => 1]);
// Call VisitorActivity Query
list($httpCode, $rsp) = $client->get('visitorActivity', 'query', $authHeader, ['limit' => 1]);
// Create a Campaign
list($httpCode, $rsp) = $client->post(
    'campaign',
    'create',
    ['name' => 'A Campaign', 'cost' => 100],
    $authHeader
);
```

## Supported API wrappers

* [ruby-pardot](https://www.github.com/Pardot/ruby-pardot)
* [python-pypardot4](https://github.com/mneedham91/PyPardot4) for version 4 of the API
* [pardot-java-client](https://github.com/Crim/pardot-java-client)
