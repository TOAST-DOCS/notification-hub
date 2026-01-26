<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>Outgoing Info</h1>

**Notification > Notification Hub > API v1.0 User Guide > Outgoing Info**



<span id="senderV1x0001RegisterExternalUnsubscribePhoneNumber"></span>

## Request to Register External 080 Opt-out Number

Request to register the external 080 opt-out number.


### Request

```
POST /sender/v1.0/unsubscribe-phone-numbers/external
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

### Request parameter

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |



### Request body

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "unsubscribePhoneNumber" : "0801234567",
  "corporationName" : "company name"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| unsubscribePhoneNumber | String | Y | External 080 opt-out number |
| corporationName | String | Y | Company name |



### Response body

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



### Request example


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Request to Register External 080 Opt-out Number

POST {{endpoint}}/sender/v1.0/unsubscribe-phone-numbers/external
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "unsubscribePhoneNumber" : "0801234567",
  "corporationName" : "company name"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/sender/v1.0/unsubscribe-phone-numbers/external" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "unsubscribePhoneNumber" : "0801234567",
  "corporationName" : "company name"
}'
```

</details>
<span id="senderV1x0002TerminateExternalUnsubscribePhoneNumber"></span>

## Deregister External 080 Opt-out Number

Deregister the external 080 opt-out number.


### Request

```
DELETE /sender/v1.0/unsubscribe-phone-numbers/external/{unsubscribePhoneNumber}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

### Request parameter

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | Access token |
| unsubscribePhoneNumber | Path | String | Y | External 080 opt-out number |



### Request body

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.



### Response body

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



### Request example


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Deregister External 080 Opt-out Number

DELETE {{endpoint}}/sender/v1.0/unsubscribe-phone-numbers/external/{{unsubscribePhoneNumber}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/sender/v1.0/unsubscribe-phone-numbers/external/${unsubscribePhoneNumber}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
<span id="senderV1x0003ReadUnsubscribePhoneNumbers"></span>

## View 080 Opt-out Number List

View 080 opt-out number list.


### Request

```
GET /sender/v1.0/unsubscribe-phone-numbers
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

### Request parameter

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | Access token |
| unsubscribePhoneNumber | Query | String | N | Opt-out number (LIKE search) |
| limit | Query | Integer | N | If limit is not set, default is 50 (maximum 1,000) |
| offset | Query | Integer | N | If offset is not set, default is 0 |



### Request body

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.



### Response body

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "unsubscribePhoneNumbers" : [ {
    "unsubscribePhoneNumber" : "0801234567",
    "corporationName" : "company name",
    "shareStatus" : "PRIMARY",
    "provider" : "INTERNAL",
    "status" : "READY",
    "terminable" : true,
    "requestedDateTime" : "2024-10-29T06:00:01.000+09:00",
    "startedDateTime" : "2024-10-29T06:00:01.000+09:00",
    "deletedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | Total count |
| unsubscribePhoneNumbers | Array | List of 080 opt-out numbers |
| unsubscribePhoneNumbers[].unsubscribePhoneNumber | String | 080 opt-out numbers |
| unsubscribePhoneNumbers[].corporationName | String | Company name |
| unsubscribePhoneNumbers[].shareStatus | String | 080 opt-out number sharing status<br>[PRIMARY (directly 080 opt-out number), SECONDARY (shared 080 number)] |
| unsubscribePhoneNumbers[].provider | String | 080 opt-out number provider type<br>[INTERNAL (internal issued number), EXTERNAL (externally registered number)] |
| unsubscribePhoneNumbers[].status | String | 080 opt-out number status<br>[READY (ready), RESERVE_USE (under review), IN_USE (in use), TERMINATED (termination)] |
| unsubscribePhoneNumbers[].terminable | Boolean | Whether termination is possible |
| unsubscribePhoneNumbers[].requestedDateTime | String | Request date |
| unsubscribePhoneNumbers[].startedDateTime | String | Activation date |
| unsubscribePhoneNumbers[].deletedDateTime | String | Cancellation date |



### Request example


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View 080 Opt-out Number List

GET {{endpoint}}/sender/v1.0/unsubscribe-phone-numbers
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/sender/v1.0/unsubscribe-phone-numbers" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
<span id="senderV1x0004ReadUnsubscribePhoneNumber"></span>

## Search Single 080 Opt-out Number

Search single 080 opt-out number.


### Request

```
GET /sender/v1.0/unsubscribe-phone-numbers/{unsubscribePhoneNumber}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

### Request parameter

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | Access token |
| unsubscribePhoneNumber | Path | String | Y | Opt-out number |



### Request body

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.



### Response body

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "unsubscribePhoneNumber" : {
    "unsubscribePhoneNumber" : 0801234567,
    "corporationName" : "company name",
    "shareStatus" : "PRIMARY",
    "provider" : "INTERNAL",
    "status" : "READY",
    "terminable" : true,
    "requestedDateTime" : "2024-10-29T06:00:01.000+09:00",
    "startedDateTime" : "2024-10-29T06:00:01.000+09:00",
    "deletedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| unsubscribePhoneNumber | Object | |
| unsubscribePhoneNumber.unsubscribePhoneNumber | String | 080 opt-out number |
| unsubscribePhoneNumber.corporationName | String | Company name |
| unsubscribePhoneNumber.shareStatus | String | 080 opt-out number share status <br>[PRIMARY (self-registered 080 number), SECONDARY (shared 080 number)] |
| unsubscribePhoneNumber.provider | String | 080 opt-out number provider type <br>[INTERNAL (Internally Issued Number), EXTERNAL (Externally Registered Number)] |
| unsubscribePhoneNumber.status | String | 080 opt-out number status <br>[READY (Ready), RESERVE_USE (Under Review), IN_USE (In Use), TERMINATED (Terminated)] |
| unsubscribePhoneNumber.terminable | Boolean | Whether termination is possible |
| unsubscribePhoneNumber.requestedDateTime | String | Application Date |
| unsubscribePhoneNumber.startedDateTime | String | Activation Date |
| unsubscribePhoneNumber.deletedDateTime | String | Termination Date |



### Request example


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Search Single 080 Opt-out Number

GET {{endpoint}}/sender/v1.0/unsubscribe-phone-numbers/{{unsubscribePhoneNumber}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/sender/v1.0/unsubscribe-phone-numbers/${unsubscribePhoneNumber}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
