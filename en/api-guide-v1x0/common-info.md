<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Common Information on Notification Hub API v1.0</h1>

**Notification > Notification Hub > API v1.0 User Guide > Common Information**

<span id="notification-hub-api-common-information"></span>

!!! danger "Caution"
    * Notification Hub API v1.0 is currently in an alpha state, is not stabilized, and experimental features may be added or removed.
    * The API is subject to change at any time, and changes may be made without notice.
    * Notification Hub will change to the official version after it is in General Availability (GA).
    * The parts that are subject to change include everything described in this document: API endpoints, authentication, request limits, requests, responses, fields, etc.

<span id="api-endpoint"></span>

## API Endpoint

| Region     | Endpoint |
|--------| ----- |
| Global | https://notification-hub.api.nhncloudservice.com |

* Notification Hub uses global endpoints regardless of regions.

<span id="authentication-and-permissions"></span>

## Authentication and Authorization

```
X-NHN-Authorization: {accessToken}
```

* Obtain an issued authorization token and set it in the **X-NHN-Authorization** request header when calling the Notification Hub API.

### Example of Authentication Token Issuance

#### IntelliJ HTTP

```http
POST https://oauth.api.nhncloudservice.com/oauth2/token/create
Content-Type: application/x-www-form-urlencoded
Authorization: Basic {{oauthAuthorization}}
```

#### cURL

```curl
curl -X POST "https://oauth.api.nhncloudservice.com/oauth2/token/create" \
     -H "Content-Type: application/x-www-form-urlencoded" \
     -H "Authorization: Basic {{oauthAuthorization}}"
```

* **oauthAuthorization** is the Base64-encoded value of the **User Access Key ID** and **Secret Access Key** combined with **USER_ACCESS_KEY_ID:SECRET_ACCESS_KEY**.
* **User Access Key ID** and **Secret Access Key** can be created and managed in **API Security Settings** in the**top right corner** after logging in.
* For more information about authentication token issuance, please refer to **User Guide** > **NHN Cloud** > **Public API** > **API Authentication** > **Authentication Token**.

<span id="date-time-format"></span>

## Date and Time Formats

* Dates and times use the **ISO 8601 extended** format.
    * [ISO 8601 - Date and time notation](https://ko.wikipedia.org/wiki/ISO_8601)
* The following **ISO 8601** formats are available
    * YYYY-MM-DDThh:mm+hh:mm
    * YYYY-MM-DDThh:mmZ
    * YYYY-MM-DDThh:mm:ss+hh:mm
    * YYYY-MM-DDThh:mm:ssZ
    * YYYY-MM-DDThh:mm:ss.sss+hh:mm
    * YYYY-MM-DDThh:mm:ss.sssZ
* **T** is the separator between date and time.
* **+hh:mm** or **Z** represents the Time Zone Designator.
* The units of seconds and milliseconds are not used in the Notification Hub API and features.
* In the API response, the date and time are represented in the format **YYYY-MM-DDThh:mm:ss.sss+09:000**.

<span id="response"></span>

## Response Common Information

<span id="succeed-response"></span>

### [Failure response body]

The HTTP status code for a successful response is **200 OK**.

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

<span id="failed-response"></span>

### [Failure response body]

The HTTP status codes for the failure response are **4xx** and **5xx**.

```json
{
    "header": {
        "isSuccessful": false,
        "resultCode": 400629,
        "resultMessage": "Contains information about the failure."
    }
}
```

| Name | Type | Description |
| --- | --- | --- |
| header.isSuccessful | Boolean | API call is successful or not |
| header.resultCode | Integer | The result code. Success has a value of 0 and failure has a value of 400000 or higher. |
| header.resultMessage | String | The result message, which contains information about the failure. |

* The first three digits of the **resultCode** are the same as the HTTP status code, and the last three digits are the detail code.
* The resulting messages are subject to change at any time. We do not recommend using the result messages for business logic.
* The result message is available in Korean, English, and Japanese, depending on the **Accept-Language** request header.
* If you set the value to** true** in the **X-NC-ALWAYS-200-OK** request header when calling the API, it will respond with HTTP status code **200 OK** on failure responses.

<span id="rate-limit"></span>

## Request Number Limit
* Notification Hub limits the number of API requests to prevent certain clients from taking up excessive resources and to ensure the reliability of the service.
* The number of API requests per second. It is limited to 300 Requests Per Second (RPS).

!!! danger "Caution"
    * The request count is measured differently by the client, the time difference between the server and the client, and network latency, so the calculated value may vary.
    * If the number of requests exceeds 300 RPS, the server will reject the client's request with an HTTP status code 429 (Too Many Requests) response.
    * If the client retries immediately when a request is rejected, the server's rejection of the request might persist for a long time.
    * It is recommended that the client invoke an increasing retry interval, such as an exponential backoff, when a request is rejected.

<span id="example-api-calls"></span>

## Example of API Calls

The Notification Hub API User Guide provides examples of API calls with **IntelliJ HTTP** and **cURL**.

### IntelliJ HTTP
* IntelliJ HTTP is an HTTP client plugin for IntelliJ IDEA that can be run from JetBrains IDEs or from the command line.
    * [JetBrains - IntelliJ HTTP Client](https://www.jetbrains.com/help/idea/http-client-in-product-code-editor.html)
        * Guide on how to use the IntelliJ HTTP Client, grammar.
    * [JetBrains Marketplace - IntelliJ HTP Client](https://plugins.jetbrains.com/plugin/13121-http-client)
        * Link to the IntelliJ HTTP Client plug-in.
    * [JetBrains - IntelliJ HTTP Cient CLI](https://blog.jetbrains.com/idea/2022/12/http-client-cli-run-requests-and-tests-on-ci/)
        * Introduction to the CLI to run IntelliJ HTTP (\*.http) files in an environment without IntelliJ.
    * [Docker - IntelliJ HTTP Client Image](https://hub.docker.com/r/jetbrains/intellij-http-client)
        * Link to the IntelliJ HTTP Client docker image.
    * [JetBrains - Define environment variables](https://www.jetbrains.com/help/idea/http-client-in-product-code-editor.html#environment-variables)
        * Guide on how to set IntelliJ HTTP Client environment variables.
      

**Example of IntelliJ HTTP environment variable configuration file (htt-client.env.json)**

```json
{
   "default": {
     "endpoint": "https://notification-hub.api.nhncloudservice.com",
     "appKey": "App key",
     "accessToken": "Authentication token"
   }
}
```

### cURL

* cURL is a command-line tool that can be run from the command line and supports a variety of protocols.
    * [cURL](https://curl.se/)
        * The official homepage for cURL.
    * [cURL - Wikipedia](https://ko.wikipedia.org/wiki/CURL)
        * Wikipedia on cURL.

**Example of cURL environment variable settings**

```
ENDPOINT=https://notification-hub.api.nhncloudservice.com
APP_KEY=App key
ACCESS_TOKEN=Authorization token
```
