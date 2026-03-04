<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>Statistics</h1>

**Notification > Notification Hub > API v1.0 User Guide > Statistics**



<span id="statsV1x0001ReadStats"></span>

## Query Statistics

Retrieve statistical events based on the event timestamp.<br>


**Request**

```
GET /stats/v1.0/stats
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| eventCategory | Query  | V1x0EventCategory | Y | Event category  |
| messageChannel | Query  | V1x0MessageChannel | N | The message channel. If left blank, statistics for all channels are retrieved. In this case, the event category is restricted to 'MESSAGE_SEND'.<br>  |
| statsKeyId | Query  | String | N | Statistics key ID.  |
| messageId | Query  | String | N | Message ID.  |
| templateId | Query  | String | N | Template ID.  |
| eventDateTimeFrom | Query  | Date | N | Start timestamp for statistics (inclusive). Applied up to the minute. Seconds and milliseconds are ignored.<br> e.g., \"2023-12-31T00:00:30.999+09:00\" is treated as \"2023-12-31T00:00:00.000+09:00\".  |
| eventDateTimeTo | Query  | Date | N | End timestamp for statistics (exclusive). Applied up to the minute. Seconds and milliseconds are ignored.<br> e.g., \"2024-01-01T00:00:30.999+09:00\" is treated as \"2024-01-01T00:00:00.000+09:00\".  |
| statsType | Query  | V1x0StatsType | N | Statistics type<br> - MINUTELY: Groups data by minute (0–59)<br> - HOURLY: Groups data by hour (0–23)<br> - DAILY: Groups data by day of the month (1–30)<br> - BY_DAY_OF_WEEK: Groups data by day of the week (Mon–Sun)<br> e.g., If set timeGrouping to BY_DAY_OF_WEEK, a 30-day data range will be aggregated into 7 groups, one for each day of the week.  |
| timeZone | Query  | String | N | Specifies the timezone for statistics (e.g., Asia/Seoul, UTC) <br> Set this to your local or browser timezone to ensure data is correctly grouped and displayed according to your local time. Set this to your local or browser timezone. This ensures that time-based grouping (e.g., daily statistics) accurately reflects your local time and prevents data discrepancies across different regions.  |
| statsCriteria | Query  | List | N | Query criteria. Options are dynamically updated based on the selected event category.<br>  |
| extra1 | Query  | String | N | Additional data collected.  |
| extra2 | Query  | String | N | Additional data collected.  |
| extra3 | Query  | String | N | Additional data collected.  |

* The configurable event categories depend on message channels.

    | Message channel | Event category |
    | --- | --- |
    | SMS | MESSAGE_SEND, INTERNATIONAL_MESSAGE_SEND |
    | ALIMTALK, RCS, EMAIL, PUSH | MESSAGE_SEND |
* The start date and time are inclusive, while the end date and time are exclusive.
    * e.g., To retrieve data for January 1, 2025, set eventDateTimeFrom to 2025-01-01T00:00:00.000+09:00 and eventDateTimeTo to 2025-01-02T00:00:00.000+09:00.
* Three additional fields (extra1, extra2, extra3) are provided for supplemental data collection.
The type of data collected in these additional fields varies depending on the configured event category.

    | Event category | Additional data 1 | Additional data 2 | Additional data 3 |
    | --- | --- | --- | --- |
    | MESSAGE_SEND | Delivery type (SMS, LMS, MMS) | Delivery purpose (NORMAL, AUTH, AD) | Sender information (sender ID, sender domain, etc.) |
    | INTERNATIONAL_MESSAGE_SEND | Delivery type (SMS, LMS, MMS, etc.) | Delivery purpose (NORMAL, AUTH, AD) | Sender information (sender ID, sender domain, etc.) |


**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

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

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the operation was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| stats | Object | |
| stats.columns | Array | Events for each event category are responded with columns.<br>The EVENT_DATE_TIME column indicates the date and time the event occurred.<br> |
| stats.rows | Array | Except for the EVENT_DATE_TIME field, all other fields are responded with according to the event category.<br><br> |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>