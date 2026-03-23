<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>Group Tag</h1>




<span id="kakaobizcenterV10GroupTagsGet"></span>

## List All Group Tags

Retrieves the full list of group tags in KakaoBizCenter.

**Request**

```
GET /kakaobizcenter/v1.0/group-tags
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | Access token |
| senderKey | Query  | String | O | Sender profile key |



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
  "groupTags" : [ {
    "groupTagKey" : "b85552999bbb335777d16fbbbbbb552b3078aaa",
    "groupTagName" : "20240619-00001"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| groupTags | Array | O |  |
| groupTags[].groupTagKey | String | O | Group tag key |
| groupTags[].groupTagName | String | O | Group tag name |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List all group tags

GET {{endpoint}}/kakaobizcenter/v1.0/group-tags?senderKey={{senderKey}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/group-tags?senderKey=${senderKey}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
<span id="kakaobizcenterV10GroupTagsGroupTagKeyDelete"></span>

## Delete a Group Tag

Deletes a group tag in KakaoBizCenter.

**Request**

```
DELETE /kakaobizcenter/v1.0/group-tags/{groupTagKey}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | Access token |
| groupTagKey | Path  | String | O | Group tag key |
| senderKey | Query  | String | O | Sender profile key |



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
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Delete a Group Tag

DELETE {{endpoint}}/kakaobizcenter/v1.0/group-tags/{{groupTagKey}}?senderKey={{senderKey}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/kakaobizcenter/v1.0/group-tags/${groupTagKey}?senderKey=${senderKey}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
<span id="kakaobizcenterV10GroupTagsGroupTagKeyGet"></span>

## Get a Group Tag

Retrieves a group tag in KakaoBizCenter.

**Request**

```
GET /kakaobizcenter/v1.0/group-tags/{groupTagKey}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | Access token |
| groupTagKey | Path  | String | O | Group tag key |
| senderKey | Query  | String | O | Sender profile key |



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
  "groupTag" : {
    "groupTagKey" : "b85552999bbb335777d16fbbbbbb552b3078aaa",
    "groupTagName" : "20240619-00001"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| groupTag | Object | O |  |
| groupTag.groupTagKey | String | O | Group tag key |
| groupTag.groupTagName | String | O | Group tag name |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Get a group tag

GET {{endpoint}}/kakaobizcenter/v1.0/group-tags/{{groupTagKey}}?senderKey={{senderKey}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/group-tags/${groupTagKey}?senderKey=${senderKey}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
<span id="kakaobizcenterV10GroupTagsGroupTagKeyPut"></span>

## Modify a Group Tag

Modifies a group tag in KakaoBizCenter.

**Request**

```
PUT /kakaobizcenter/v1.0/group-tags/{groupTagKey}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | Access token |
| groupTagKey | Path  | String | O | Group tag key |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "newGroupTagName" : "20240619-00001"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| senderKey | String | O | Sender profile key |
| newGroupTagName | String | O | New group tag name |



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "groupTag" : {
    "groupTagKey" : "b85552999bbb335777d16fbbbbbb552b3078aaa",
    "groupTagName" : "20240619-00001"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| groupTag | Object | O |  |
| groupTag.groupTagKey | String | O | Group tag key |
| groupTag.groupTagName | String | O | Group tag name |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Modify a Group Tag

PUT {{endpoint}}/kakaobizcenter/v1.0/group-tags/{{groupTagKey}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "newGroupTagName" : "20240619-00001"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/kakaobizcenter/v1.0/group-tags/${groupTagKey}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "newGroupTagName" : "20240619-00001"
}'
```

</details>
<span id="kakaobizcenterV10GroupTagsPost"></span>

## Register a Group Tag

Registers a group tag in KakaoBizCenter.

**Request**

```
POST /kakaobizcenter/v1.0/group-tags
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | Access token |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "groupTagName" : "20240619-00001"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| senderKey | String | O | Sender profile key |
| groupTagName | String | O | Group tag name |



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "groupTag" : {
    "groupTagKey" : "b85552999bbb335777d16fbbbbbb552b3078aaa",
    "groupTagName" : "20240619-00001"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| groupTag | Object | O |  |
| groupTag.groupTagKey | String | O | Group tag key |
| groupTag.groupTagName | String | O | Group tag name |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Register a group tag

POST {{endpoint}}/kakaobizcenter/v1.0/group-tags
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "groupTagName" : "20240619-00001"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/kakaobizcenter/v1.0/group-tags" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "groupTagName" : "20240619-00001"
}'
```

</details>
