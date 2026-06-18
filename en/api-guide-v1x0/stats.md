<!-- pre-align:aligned sig=ec416b7f4d48 -->

<!-- Style added for the new layout. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- The title has been changed to <h1> for the new layout. -->
<h1>Statistics</h1>

**Notification > Notification Hub > API v1.0 User Guide > Statistics**



<span id="statsV1x0001ReadStats"></span>

## Get Statistics

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
| eventCategory | Query | Enum | O | Event category |
| messageChannel | Query | Enum | X | Message channel. If not set, statistics data is retrieved for all message channels, and the event category can only be set to message sending (MESSAGE_SEND).<br> |
| statsKeyId | Query | String | X | Statistics key ID. |
| messageId | Query | String | X | Message ID. |
| templateId | Query | String | X | Template ID. |
| eventDateTimeFrom | Query | DateTime | X | Start date and time (inclusive) for retrieving statistics events. Applied up to year, month, day, hour, and minute. Seconds and milliseconds are not used.<br> Example: "2023-12-31T00:00:30.999+09:00" is processed as "2023-12-31T00:00:00.000+09:00". |
| eventDateTimeTo | Query | DateTime | X | End date and time (exclusive) for retrieving statistics events. Applied up to year, month, day, hour, and minute. Seconds and milliseconds are not used.<br> Example: "2024-01-01T00:00:30.999+09:00" is processed as "2024-01-01T00:00:00.000+09:00". |
| statsType | Query | Enum | X | Statistics type<br> - MINUTELY: Grouped between 0 and 59 minutes<br> - HOURLY: Grouped between 0 and 23 hours<br> - DAILY: Grouped between 0 and 30 days<br> - BY_DAY_OF_WEEK: Grouped by day of the week (Monday through Sunday)<br> Example: If statsType is set to BY_DAY_OF_WEEK, even if you retrieve 30 days of data, the data is grouped by day of the week (Monday through Sunday). |
| timeZone | Query | String | X | Time zone for statistics retrieval. Examples: Asia/Seoul, UTC, America/New_York<br> You can set the desired time zone when receiving data during statistics retrieval. In general, set the time zone of the client or browser performing the query.<br> For example, if you retrieve statistics data grouped by day of the week from outside Korea, the data may not be returned as expected due to time zone differences. |
| statsCriteria | Query | Array | X | Query criteria. The available query criteria vary depending on the configured event category.<br> |
| extra1 | Query | String | X | Additional collected data. |
| extra2 | Query | String | X | Additional collected data. |
| extra3 | Query | String | X | Additional collected data. |

* The available event categories vary depending on the message channel.

  | Message Channel | Event Category |
      | --- | --- |
  | SMS | MESSAGE_SEND, INTERNATIONAL_MESSAGE_SEND |
  | ALIMTALK, RCS, EMAIL, PUSH | MESSAGE_SEND |
* The start date and time is included in the query period, and the end date and time is excluded from the query period.
    * Example: To retrieve data for January 1, 2025, set eventDateTimeFrom to 2025-01-01T00:00:00.000+09:00 and eventDateTimeTo to 2025-01-02T00:00:00.000+09:00.
* In addition to events, up to three additional fields (extra1, extra2, extra3) are provided for extra collected data.
  The type of additional data collected varies depending on the configured event category.

  | Event Category | Additional Data 1 | Additional Data 2 | Additional Data 3 |
      | --- | --- | --- | --- |
  | MESSAGE_SEND | Sending type (SMS, LMS, MMS, etc.) | Message purpose (NORMAL, AUTH, AD) | Sender information (sender number, sender domain, etc.) |
  | INTERNATIONAL_MESSAGE_SEND | Sending type (SMS, LMS, MMS, etc.) | Message purpose (NORMAL, AUTH, AD) | Sender information (sender number, sender domain, etc.) |


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
| header | Object | O | |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| stats | Object | O | |
| stats.columns | Array | O | Events for the event category are returned as columns.<br>The EVENT_DATE_TIME column indicates the date and time when the event occurred.<br> |
| stats.rows | Array | O | All fields except EVENT_DATE_TIME are returned according to the event category.<br><br> |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Get Statistics

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