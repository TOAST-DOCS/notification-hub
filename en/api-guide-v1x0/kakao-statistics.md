<!-- pre-align:aligned sig=ff946ac84827 -->

<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>Kakao Statistics</h1>

**Notification > Notification Hub > API v1.0 User Guide > Kakao Statistics**

Retrieves statistics data provided by KakaoBizCenter.
Statistics data can be retrieved on a daily (DAILY) or monthly (MONTHLY) basis by sender key.
DAILY: Only data within the last 90 days can be retrieved, with a maximum retrieval range of 90 days.
MONTHLY: Only data within the last 3 months can be retrieved, with a maximum retrieval range of 3 months.

* Real-time statistics are not provided. Data collected the previous day is provided daily at around 7 AM.
* AlimTalk statistics are initially provided on D+1 and finalized on D+2.
* Valid read counts are not duplicated for the same message.
* Click counts are duplicated for the same message.
* If the number of successful sends is 10 or fewer, valid read counts and click counts are not provided.

<a id="delivery-statistics"></a>

### Delivery Statistics

Retrieves the daily send count, valid read count, and click count by sender profile. You can filter by period, send identifier, message type, and more.

<a id="template-statistics"></a>

### Template Statistics

Retrieves the daily send count, valid read count, and click count by template and group tag. You can filter by period, message type, and more.

* Brand message freestyle is only provided when a group tag is used.



<span id="kakaobizcenterV1x0001ReadAlimtalkDeliveryStatistics"></span>

<a id="retrieve-alimtalk-delivery-statistics"></a>

## Retrieve AlimTalk Delivery Statistics

Retrieves AlimTalk delivery statistics.
Retrieves the daily send count, valid read count, and click count by sender profile. You can filter by period, send identifier, message type, and more.

The retrieval period (startDate ~ endDate) is a maximum of 3 months.


**Request**

```
GET /kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/ALIMTALK
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| senderKey | Query | String | O | Sender key. |
| periodType | Query | Enum | O | Retrieval period unit. |
| startDate | Query | String | O | Retrieval start date. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) |
| endDate | Query | String | O | Retrieval end date. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) startDate ~ endDate is a maximum of 3 months. |
| messageType | Query | Enum | X | Message type. |
| receiveUserType | Query | Enum | X | Send identifier. |
| limit | Query | Number | X | If limit is not set, the default value is 500. (Maximum 1,000) |
| offset | Query | Number | X | If offset is not set, the default value is 0. |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->

This API does not require a request body.



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "alimtalkDeliveryStatistics" : [ {
    "date" : "2026-01-15",
    "messageType" : "AT",
    "receiveUserType" : "PhoneNumber",
    "totalSendRequestCount" : 1000,
    "validSendRequestCount" : 950,
    "validReadCount" : 800
  } ]
}
```

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | O | Total count |
| alimtalkDeliveryStatistics | Array | O |  |
| alimtalkDeliveryStatistics[].date | String | O | Date (daily: YYYY-MM-DD, monthly: YYYY-MM) |
| alimtalkDeliveryStatistics[].messageType | String | O | AlimTalk message type<br>[AT (standard AlimTalk), AI (image AlimTalk)] |
| alimtalkDeliveryStatistics[].receiveUserType | String | O | Send identifier<br>[PhoneNumber (phone number), AppUserId (app user ID), UserKey (user key), None (no recipient identifier)] |
| alimtalkDeliveryStatistics[].totalSendRequestCount | Integer | O | Total send request count |
| alimtalkDeliveryStatistics[].validSendRequestCount | Integer | O | Valid send request count |
| alimtalkDeliveryStatistics[].validReadCount | Integer | O | Valid read count |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve AlimTalk delivery statistics

GET {{endpoint}}/kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/ALIMTALK?senderKey={{senderKey}}&periodType={{periodType}}&startDate={{startDate}}&endDate={{endDate}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/ALIMTALK?senderKey=${senderKey}&periodType=${periodType}&startDate=${startDate}&endDate=${endDate}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="kakaobizcenterV1x0002ReadAlimtalkTemplateStatistics"></span>

<a id="retrieve-alimtalk-template-statistics"></a>

## Retrieve AlimTalk Template Statistics

Retrieves AlimTalk template statistics.
Retrieves the daily send count, valid read count, and click count by template and group tag. You can filter by period, message type, and more.

The retrieval period (startDate ~ endDate) is a maximum of 3 months.


**Request**

```
GET /kakaobizcenter/v1.0/kakao-statistics/template-statistics/ALIMTALK
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| senderKey | Query | String | O | Sender key. |
| periodType | Query | Enum | O | Retrieval period unit. |
| startDate | Query | String | O | Retrieval start date. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) |
| endDate | Query | String | O | Retrieval end date. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) startDate ~ endDate is a maximum of 3 months. |
| kakaoTemplateCode | Query | String | X | Kakao template code. |
| messageType | Query | Enum | X | Message type. |
| limit | Query | Number | X | If limit is not set, the default value is 500. (Maximum 1,000) |
| offset | Query | Number | X | If offset is not set, the default value is 0. |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->

This API does not require a request body.



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "alimtalkTemplateStatistics" : [ {
    "date" : "2026-01-15",
    "messageType" : "AT",
    "templateCode" : "template_001",
    "totalSendSuccessCount" : 950,
    "validReadCount" : 800,
    "totalClickCount" : 500
  } ]
}
```

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | O | Total count |
| alimtalkTemplateStatistics | Array | O |  |
| alimtalkTemplateStatistics[].date | String | O | Date (daily: YYYY-MM-DD, monthly: YYYY-MM) |
| alimtalkTemplateStatistics[].messageType | String | O | AlimTalk message type<br>[AT (standard AlimTalk), AI (image AlimTalk)] |
| alimtalkTemplateStatistics[].templateCode | String | O | Template code |
| alimtalkTemplateStatistics[].totalSendSuccessCount | Integer | O | Total send success count |
| alimtalkTemplateStatistics[].validReadCount | Integer | O | Valid read count |
| alimtalkTemplateStatistics[].totalClickCount | Integer | O | Total click count |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve AlimTalk template statistics

GET {{endpoint}}/kakaobizcenter/v1.0/kakao-statistics/template-statistics/ALIMTALK?senderKey={{senderKey}}&periodType={{periodType}}&startDate={{startDate}}&endDate={{endDate}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/kakao-statistics/template-statistics/ALIMTALK?senderKey=${senderKey}&periodType=${periodType}&startDate=${startDate}&endDate=${endDate}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="kakaobizcenterV1x0003ReadBrandmessageDeliveryStatistics"></span>

<a id="retrieve-brand-message-delivery-statistics"></a>

## Retrieve Brand Message Delivery Statistics

Retrieves brand message delivery statistics.
Retrieves the daily send count, valid read count, and click count by sender profile. You can filter by period, send identifier, message type, and more.

The retrieval period (startDate ~ endDate) is a maximum of 3 months.


**Request**

```
GET /kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/BRANDMESSAGE
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| senderKey | Query | String | O | Sender key. |
| periodType | Query | Enum | O | Retrieval period unit. |
| startDate | Query | String | O | Retrieval start date. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) |
| endDate | Query | String | O | Retrieval end date. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) startDate ~ endDate is a maximum of 3 months. |
| messageSpec | Query | Enum | X | Send type. |
| chatBubbleType | Query | Enum | X | Message type. |
| targeting | Query | Enum | X | Whether send targeting is applied. |
| friendType | Query | Enum | X | Friend type. |
| receiveUserType | Query | Enum | X | Send identifier. |
| limit | Query | Number | X | If limit is not set, the default value is 500. (Maximum 1,000) |
| offset | Query | Number | X | If offset is not set, the default value is 0. |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->

This API does not require a request body.



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "brandmessageDeliveryStatistics" : [ {
    "date" : "2026-01-15",
    "receiveUserType" : "PhoneNumber",
    "messageSpec" : "BASIC",
    "chatBubbleType" : "TEXT",
    "friendType" : "F",
    "targeting" : "M",
    "totalSendRequestCount" : 1000,
    "validSendRequestCount" : 950,
    "validReadCount" : 800,
    "totalClickCount" : 500
  } ]
}
```

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | O | Total count |
| brandmessageDeliveryStatistics | Array | O |  |
| brandmessageDeliveryStatistics[].date | String | O | Date (daily: YYYY-MM-DD, monthly: YYYY-MM) |
| brandmessageDeliveryStatistics[].receiveUserType | String | O | Send identifier<br>[PhoneNumber (phone number), AppUserId (app user ID), UserKey (user key), None (no recipient identifier)] |
| brandmessageDeliveryStatistics[].messageSpec | String | O | Send type<br>[BASIC (basic), FREESTYLE (freestyle)] |
| brandmessageDeliveryStatistics[].chatBubbleType | String | O | Message type<br>[TEXT (text), IMAGE (image), WIDE (wide image), WIDE_ITEM_LIST (wide item list), CAROUSEL_FEED (carousel feed), PREMIUM_VIDEO (premium video), COMMERCE (commerce), CAROUSEL_COMMERCE (carousel commerce)] |
| brandmessageDeliveryStatistics[].friendType | String | O | Friend type<br>[F (friend), N (non-friend)] |
| brandmessageDeliveryStatistics[].targeting | String | O | Whether send targeting is applied<br>[M (all users who agreed to receive marketing), N (excluding channel friends), I (channel friends only), F (all channel friends)] |
| brandmessageDeliveryStatistics[].totalSendRequestCount | Integer | O | Total send request count |
| brandmessageDeliveryStatistics[].validSendRequestCount | Integer | O | Valid send request count |
| brandmessageDeliveryStatistics[].validReadCount | Integer | O | Valid read count |
| brandmessageDeliveryStatistics[].totalClickCount | Integer | O | Total click count |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve brand message delivery statistics

GET {{endpoint}}/kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/BRANDMESSAGE?senderKey={{senderKey}}&periodType={{periodType}}&startDate={{startDate}}&endDate={{endDate}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/BRANDMESSAGE?senderKey=${senderKey}&periodType=${periodType}&startDate=${startDate}&endDate=${endDate}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="kakaobizcenterV1x0004ReadBrandmessageTemplateStatistics"></span>

<a id="retrieve-brand-message-template-statistics"></a>

## Retrieve Brand Message Template Statistics

Retrieves brand message template statistics.
Retrieves the daily send count, valid read count, and click count by template and group tag. You can filter by period, message type, and more.

The retrieval period (startDate ~ endDate) is a maximum of 3 months.


**Request**

```
GET /kakaobizcenter/v1.0/kakao-statistics/template-statistics/BRANDMESSAGE
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| senderKey | Query | String | O | Sender key. |
| periodType | Query | Enum | O | Retrieval period unit. |
| startDate | Query | String | O | Retrieval start date. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) |
| endDate | Query | String | O | Retrieval end date. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) startDate ~ endDate is a maximum of 3 months. |
| kakaoTemplateCode | Query | String | X | Kakao template code. |
| groupTagKey | Query | String | X | Group tag key. |
| messageSpec | Query | Enum | X | Send type. |
| chatBubbleType | Query | Enum | X | Message type. |
| targeting | Query | Enum | X | Whether send targeting is applied. |
| friendType | Query | Enum | X | Friend type. |
| limit | Query | Number | X | If limit is not set, the default value is 500. (Maximum 1,000) |
| offset | Query | Number | X | If offset is not set, the default value is 0. |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->

This API does not require a request body.



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "brandmessageTemplateStatistics" : [ {
    "date" : "2026-01-15",
    "templateCode" : "template_001",
    "groupTagKey" : "group_tag_001",
    "messageSpec" : "BASIC",
    "chatBubbleType" : "TEXT",
    "friendType" : "F",
    "targeting" : "M",
    "totalSendSuccessCount" : 950,
    "validReadCount" : 800,
    "totalClickCount" : 500
  } ]
}
```

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | O | Total count |
| brandmessageTemplateStatistics | Array | O |  |
| brandmessageTemplateStatistics[].date | String | O | Date (daily: YYYY-MM-DD, monthly: YYYY-MM) |
| brandmessageTemplateStatistics[].templateCode | String | O | Template code |
| brandmessageTemplateStatistics[].groupTagKey | String | X | Group tag key |
| brandmessageTemplateStatistics[].messageSpec | String | O | Send type<br>[BASIC (basic), FREESTYLE (freestyle)] |
| brandmessageTemplateStatistics[].chatBubbleType | String | O | Message type<br>[TEXT (text), IMAGE (image), WIDE (wide image), WIDE_ITEM_LIST (wide item list), CAROUSEL_FEED (carousel feed), PREMIUM_VIDEO (premium video), COMMERCE (commerce), CAROUSEL_COMMERCE (carousel commerce)] |
| brandmessageTemplateStatistics[].friendType | String | O | Friend type<br>[F (friend), N (non-friend)] |
| brandmessageTemplateStatistics[].targeting | String | O | Whether send targeting is applied<br>[M (all users who agreed to receive marketing), N (excluding channel friends), I (channel friends only), F (all channel friends)] |
| brandmessageTemplateStatistics[].totalSendSuccessCount | Integer | O | Total send success count |
| brandmessageTemplateStatistics[].validReadCount | Integer | O | Valid read count |
| brandmessageTemplateStatistics[].totalClickCount | Integer | O | Total click count |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve brand message template statistics

GET {{endpoint}}/kakaobizcenter/v1.0/kakao-statistics/template-statistics/BRANDMESSAGE?senderKey={{senderKey}}&periodType={{periodType}}&startDate={{startDate}}&endDate={{endDate}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/kakao-statistics/template-statistics/BRANDMESSAGE?senderKey=${senderKey}&periodType=${periodType}&startDate=${startDate}&endDate=${endDate}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>