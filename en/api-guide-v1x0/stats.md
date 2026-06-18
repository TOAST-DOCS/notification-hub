<!-- pre-align:aligned sig=ec416b7f4d48 -->

<!-- Style added for the new form. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- The title has been changed to <h1> for the new form. -->
<h1>Statistics</h1>

**Notification > Notification Hub > API v1.0 User Guide > Statistics**



<span id="statsV1x0001ReadStats"></span>

## Retrieve Statistics

Retrieves statistics events based on the time the events occurred.<br>


**Request**

```
GET /stats/v1.0/stats
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| eventCategory | Query | Enum | O | Event category  |
| messageChannel | Query | Enum | X | Message channel. If not set, statistics data for all message channels is retrieved, and the event category can only be set to MESSAGE_SEND.<br>  |
| statsKeyId | Query | String | X | Statistics key ID.  |
| messageId | Query | String | X | Message ID.  |
| templateId | Query | String | X | Template ID.  |
| eventDateTimeFrom | Query | DateTime | X | Start date and time of the statistics event query (inclusive). Applied up to the year, month, day, hour, and minute. Seconds and milliseconds are not used.<br> Example: \"2023-12-31T00:00:30.999+09:00\" is processed as \"2023-12-31T00:00:00.000+09:00\".  |
| eventDateTimeTo | Query | DateTime | X | End date and time of the statistics event query (exclusive). Applied up to the year, month, day, hour, and minute. Seconds and milliseconds are not used.<br> Example: \"2024-01-01T00:00:30.999+09:00\" is processed as \"2024-01-01T00:00:00.000+09:00\".  |
| statsType | Query | Enum | X | Statistics type<br> - MINUTELY: Grouped from minute 0 to minute 59<br> - HOURLY: Grouped from hour 0 to hour 23<br> - DAILY: Grouped from day 0 to day 30<br> - BY_DAY_OF_WEEK: Grouped by day of the week (Monday through Sunday)<br> Example: If statsType is set to BY_DAY_OF_WEEK, even when retrieving 30 days of data, the data is grouped by day of the week (Monday through Sunday).  |
| timeZone | Query | String | X | Time zone for statistics queries. Example: Asia/Seoul, UTC, America/New_York <br> You can set the time zone to receive statistics data in your preferred time zone. In general, set the time zone of the client or browser making the query.<br> For example, if you query statistics data grouped by day of the week from outside Korea, the data may not match what you expect because of the time zone difference.  |
| statsCriteria | Query | Array | X | Query criteria. The available query criteria vary depending on the event category that is set.<br>  |
| extra1 | Query | String | X | Additionally collected data.  |
| extra2 | Query | String | X | Additionally collected data.  |
| extra3 | Query | String | X | Additionally collected data.  |

* The available event categories vary depending on the message channel.

  | Message Channel | Event Category |
      | --- | --- |
  | SMS | MESSAGE_SEND, INTERNATIONAL_MESSAGE_SEND |
  | ALIMTALK, RCS, EMAIL, PUSH | MESSAGE_SEND |
* The start date and time is included in the query period, and the end date and time is not included in the query period.
    * Example: To query data for January 1, 2025, set eventDateTimeFrom to 2025-01-01T00:00:00.000+09:00 and eventDateTimeTo to 2025-01-02T00:00:00.000+09:00.
* In addition to events, 3 additional fields (extra1, extra2, extra3) are collected. The type of additionally collected data varies depending on the event category that is set.

  | Event Category | Additional Data 1 | Additional Data 2 | Additional Data 3 |
      | --- | --- | --- | --- |
  | MESSAGE_SEND | Sending type (SMS, LMS, MMS, etc.) | Sending purpose (NORMAL, AUTH, AD) | Sender information (sender number, sender domain, etc.) |
  | INTERNATIONAL_MESSAGE_SEND | Sending type (SMS, LMS, MMS, etc.) | Sending purpose (NORMAL, AUTH, AD) | Sender information (sender number, sender domain, etc.) |


**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->

This API does not require a request body.



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "stats" : {
    "columns" : [ {
      "name" : "EVENT_DATE_TIME"
    }, {
      "name" : "REQUESTED"
    }, {
      "name" : "SENT"
    }, {
      "name" : "SEND_FAILED"
    }, {
      "name" : "DELIVERED"
    }, {
      "name" : "DELIVERY_FAILED"
    }, {
      "name" : "OPENED"
    } ],
    "rows" : [ {
      "EVENT_DATE_TIME" : "2023-12-31T00:00:00.000+09:00",
      "REQUESTED" : 10,
      "SENT" : 10,
      "SEND_FAILED" : 1,
      "DELIVERED" : 7,
      "DELIVERY_FAILED" : 1,
      "OPENED" : 1
    } ]
  }
}
```

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| stats | Object | O |  |
| stats.columns | Array | O | Events for the event category are returned as columns.<br>The EVENT_DATE_TIME column indicates the date and time the event occurred.<br> |
| stats.rows | Array | O | Fields other than the EVENT_DATE_TIME field are returned based on the event category.<br><br> |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve Statistics

GET {{endpoint}}/stats/v1.0/stats?eventCategory={{eventCategory}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/stats/v1.0/stats?eventCategory=${eventCategory}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>