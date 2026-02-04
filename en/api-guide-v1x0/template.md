<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>Template</h1>

**Notification > Notification Hub > API v1.0 User Guide > Template**



<span id="templateV1x0001CreateSmsTemplate"></span>

## Register SMS Template

Register a template.

**Request**

```
POST /template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday Service Hours",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience. :)",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | Y | Template name |
| categoryId | String | N | Category ID |
| messagePurpose | String | N | Message contents<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | Template type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.senderPhoneNumber | String | N | Outgoing number |
| content | Object | Y |  |
| content.messageType | String | N | Message type (SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| content.title | String | N | Message title |
| content.body | String | N | Message body |
| content.attachmentIds | Array | N | Up to 3 attachments |



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "templateId" : "A9z0A9z0"
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| templateId | String | The template ID issued when registering the template. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Register SMS Template

POST {{endpoint}}/template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday Service Hours",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience. :)",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/SMS/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday Service Hours",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience. :)",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>
<span id="templateV1x0002ReadSmsTemplateList"></span>

## View SMS Template List

View template lists.

**Request**

```
GET /template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateName | Query  | String | N | Template name (LIKE search) |
| limit | Query | Integer | N | If limit is not set, default is 20 (maximum 1,000) |
| offset | Query | Integer | N | If offset is not set, default is 0 |



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
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "Delivery completed",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | Total number of cases |
| templates | Array | |
| templates[].templateId | String | The template ID issued when registering the template. |
| templates[].templateName | String | The template name |
| templates[].categoryId | String | The category ID |
| templates[].messageChannel | String | The message channel.<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | The content type.<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array | |
| templates[].createdDateTime | String | Created at |
| templates[].updatedDateTime | String | Updated at |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View SMS Template List

GET {{endpoint}}/template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/SMS/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0003ReadSmsTemplate"></span>

## View SMS Template Details

View SMS template details.

**Request**

```
GET /template/v1.0/SMS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



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
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "template name",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "sender" : {
      "senderPhoneNumber" : "01012341234"
    },
    "content" : {
      "messageType" : "SMS",
      "title" : "Holiday Service Hours",
      "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience. :)",
      "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| template | Object | |
| template.templateId | String | The template ID issued when registering the template. |
| template.templateName | String | Template name |
| template.categoryId | String | Category ID |
| template.messageChannel | String | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | The type of content sent.<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array | |
| template.templateLanguage | String | Template Type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object | |
| template.sender.senderPhoneNumber | String | Sender Number |
| template.content | Object | |
| template.content.messageType | String | Message Type (SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| template.content.title | String | Message Title |
| template.content.body | String | Message Body |
| template.content.attachmentIds | Array | Up to 3 attachment IDs |
| template.createdDateTime | String | Created at |
| template.updatedDateTime | String | Updated at |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View SMS Template Details

GET {{endpoint}}/template/v1.0/SMS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/SMS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0004UpdateSmsTemplate"></span>

## Modify SMS Template

Modify a SMS template.

**Request**

```
PUT /template/v1.0/SMS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday Service Hours",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience. :)",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | Y | Template name |
| messagePurpose | String | N | Delivery content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | Template type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N | |
| sender.senderPhoneNumber | String | N | Sender number |
| content | Object | Y | |
| content.messageType | String | N | Message type (SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| content.title | String | N | Message title |
| content.body | String | N | Message body |
| content.attachmentIds | Array | N | Up to 3 attachment IDs |



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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Modify SMS Template

PUT {{endpoint}}/template/v1.0/SMS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday Service Hours",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience. :)",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/SMS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday Service Hours",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience. :)",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>
<span id="templateV1x0005DeleteSmsTemplate"></span>

## Delete SMS Template

Delete a template.

**Request**

```
DELETE /template/v1.0/SMS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Delete SMS Template

DELETE {{endpoint}}/template/v1.0/SMS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/SMS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0006CreateAlimtalkTemplate"></span>

## Register Alimtalk Template

Register a template.

**Request**

```
POST /template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
    "senderProfileType" : "NORMAL"
  },
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "#{Name}, your order has been successfully placed.",
    "templateAd" : "Follow our channel to receive marketing messages and updates via KakaoTalk",
    "templateExtra" : "* Please note that real-time availability can lead to overlapping bookings. If we cannot accommodate your stay, your reservation.\\n* Contact: 1234-1234",
    "templateTitle" : "123,450 KRW",
    "templateSubtitle" : "Approval Details",
    "templateHeader" : "Your order has been confirmed",
    "templateItem" : {
      "list" : [ {
        "title" : "item title",
        "description" : "item description"
      } ],
      "summary" : {
        "title" : "summary title",
        "description" : "summary description"
      }
    },
    "templateItemHighlight" : {
      "title" : "highlight title",
      "description" : "highlight description",
      "attachmentId" : "YaX2DA4Weab2",
      "imageUrl" : "https://example.com/thumbnail.jpg"
    },
    "templateRepresentLink" : {
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "attachmentId" : "YaX2DA4Weab2",
    "templateImageName" : "image.png",
    "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "securityFlag" : false,
    "categoryCode" : "999999",
    "buttons" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "button name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "Quick link name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ]
  },
  "additionalProperty" : {
    "templateCode" : "templateCode",
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | Y | Template name |
| categoryId | String | N | Category ID |
| messagePurpose | String | N | Sent content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | Template type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N | |
| sender.senderKey | String | N | Sender profile sender key |
| sender.senderProfileType | String | N | Sender profile type<br>[GROUP, NORMAL] |
| content | Object | Y | |
| content.templateMessageType | String | N | Template message type (BA: Basic, EX: Additional information, AD: Channel addition, MI: Complex, default: BA) |
| content.templateEmphasizeType | String | N | Template highlight type (NONE: default, TEXT: highlight, IMAGE: image type, ITEM_LIST: item list type, default: NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| content.templateContent | String | N | Template body |
| content.templateAd | String | N | Channel addition notification message (template message type: channel addition type, fixed value if composite type) |
| content.templateExtra | String | N | Template additional information (required if template message type is [additional information type/composite type]), substitution variables cannot be used, URLs can be included |
| content.templateTitle | String | N | Template title (maximum 50 characters, Android: 2 lines, truncation of 23 or more characters, iOS: 2 lines, truncation of 27 or more characters) |
| content.templateSubtitle | String | N | Template text (up to 50 characters; Android: 18 characters or more are truncated; iOS: 21 characters or more are truncated) |
| content.templateHeader | String | N | Template header, variable input allowed |
| content.templateItem | Object | N |  |
| content.templateItem.list | Array | N |  |
| content.templateItem.list[].title | String | N | Item Title |
| content.templateItem.list[].description | String | N | Item Description |
| content.templateItem.summary | Object | N | |
| content.templateItem.summary.title | String | N | Summary Title |
| content.templateItem.summary.description | String | N | Summary Description (only variables, currency units, numbers, commas, and periods allowed) |
| content.templateItemHighlight | Object | N | | |
| content.templateItemHighlight.title | String | N | Item Highlight Title (up to 30 characters, 21 characters if a thumbnail image is present) |
| content.templateItemHighlight.description | String | N | Item Highlight Description (up to 19 characters, 13 characters if a thumbnail image is present) |
| content.templateItemHighlight.attachmentId | String | N | Template Attachment ID |
| content.templateItemHighlight.imageUrl | String | N | Thumbnail image address |
| content.templateRepresentLink | Object | N | |
| content.templateRepresentLink.linkMo | String | N | Primary link mobile web link |
| content.templateRepresentLink.linkPc | String | N | Primary link PC web link |
| content.templateRepresentLink.schemeIos | String | N | Primary link iOS app link |
| content.templateRepresentLink.schemeAndroid | String | N | Primary link Android app link |
| content.attachmentId | String | N | Template attachment ID |
| content.templateImageName | String | N | Template image name |
| content.templateImageUrl | String | N | Template image link |
| content.securityFlag | Boolean | N | Template security status (default: false) |
| content.categoryCode | String | N | Template category code (see template category query API, default: 999999) |
| content.buttons | Array | N | Template button |
| content.buttons[].ordering | Integer | N | Template button order |
| content.buttons[].type | String | N | Template Button Type (WL: Web Link, AL: App Link, DS: Delivery Tracking, BK: Bot Keyword, MD: Message Forwarding, BC: Chat Conversion, BT: Bot Conversion, AC: Channel Addition, BF: Business Form, P1: Image Security Transmission Plugin ID, P2: Personal Information Use Plugin ID, P3: One-Click Payment Plugin ID)<br>[WL, AL, DS, BK, MD, BC, BT, AC, BF, P1, P2, P3] |
| content.buttons[].name | String | N | Template button name |
| content.buttons[].linkMo | String | N | Template button mobile web link |
| content.buttons[].linkPc | String | N | Template button PC web link |
| content.buttons[].schemeIos | String | N | Template button iOS app link |
| content.buttons[].schemeAndroid | String | N | Template button Android app link |
| content.buttons[].bizFormId | Integer | N | Template button business form ID (required for BF type) |
| content.quickReplies | Array | N | Template shortcut |
| content.quickReplies[].ordering | Integer | N | Template shortcut order |
| content.quickReplies[].type | String | N | Template shortcut type (WL: Web Link, AL: App Link, BK: Bot Keyword, BC: Chat Conversion, BT: Bot Conversion, BF: Business Form)<br>[WL, AL, BK, BC, BT, BF] |
| content.quickReplies[].name | String | N | Template shortcut name |
| content.quickReplies[].linkMo | String | N | Template mobile web shortcut link |
| content.quickReplies[].linkPc | String | N | Template PC web shortcut link |
| content.quickReplies[].schemeIos | String | N | Template iOS app shortcut link |
| content.quickReplies[].schemeAndroid | String | N | Template Android app shortcut link |
| content.quickReplies[].bizFormId | Integer | N | Template shortcut business form ID (required for BF type) |
| additionalProperty | Object | N | | |
| additionalProperty.templateCode | String | N | Template code (English, Number, -, _) |
| additionalProperty.kakaoTemplateCode | String | N | Kakao template code |



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "templateId" : "A9z0A9z0"
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| templateId | String | When registering a template, the template ID issued |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Register AlimTalk Template

POST {{endpoint}}/template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
    "senderProfileType" : "NORMAL"
  },
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "#{Name}, your order has been successfully placed.",
    "templateAd" : "Follow our channel to receive marketing messages and updates via KakaoTalk",
    "templateExtra" : "* Please note that real-time availability can lead to overlapping bookings. If we cannot accommodate your stay, your reservation.\\n* Contact: 1234-1234",
    "templateTitle" : "123,450 KRW",
    "templateSubtitle" : "Approval Details",
    "templateHeader" : "Your order has been confirmed",
    "templateItem" : {
      "list" : [ {
        "title" : "item title",
        "description" : "item description"
      } ],
      "summary" : {
        "title" : "summary title",
        "description" : "summary description"
      }
    },
    "templateItemHighlight" : {
      "title" : "highlight title",
      "description" : "highlight description",
      "attachmentId" : "YaX2DA4Weab2",
      "imageUrl" : "https://example.com/thumbnail.jpg"
    },
    "templateRepresentLink" : {
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "attachmentId" : "YaX2DA4Weab2",
    "templateImageName" : "image.png",
    "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "securityFlag" : false,
    "categoryCode" : "999999",
    "buttons" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "button name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "Quick link name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ]
  },
  "additionalProperty" : {
    "templateCode" : "templateCode",
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
    "senderProfileType" : "NORMAL"
  },
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "#{Name}, your order has been successfully placed.",
    "templateAd" : "Follow our channel to receive marketing messages and updates via KakaoTalk",
    "templateExtra" : "* Please note that real-time availability can lead to overlapping bookings. If we cannot accommodate your stay, your reservation.\\n* Contact: 1234-1234",
    "templateTitle" : "123,450 KRW",
    "templateSubtitle" : "Approval Details",
    "templateHeader" : "Your order has been confirmed",
    "templateItem" : {
      "list" : [ {
        "title" : "item title",
        "description" : "item description"
      } ],
      "summary" : {
        "title" : "summary title",
        "description" : "summary description"
      }
    },
    "templateItemHighlight" : {
      "title" : "highlight title",
      "description" : "highlight description",
      "attachmentId" : "YaX2DA4Weab2",
      "imageUrl" : "https://example.com/thumbnail.jpg"
    },
    "templateRepresentLink" : {
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "attachmentId" : "YaX2DA4Weab2",
    "templateImageName" : "image.png",
    "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "securityFlag" : false,
    "categoryCode" : "999999",
    "buttons" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "button name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "Quick link name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ]
  },
  "additionalProperty" : {
    "templateCode" : "templateCode",
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}'
```

</details>
<span id="templateV1x0007ReadAlimtalkTemplateList"></span>

## View AlimTalk Template List

View a template list.

**Request**

```
GET /template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateName | Query  | String | N | Template name (LIKE search) |
| senderKey | Query | String | N | Sender key |
| templateStatus | Query | String | N | Template status |
| limit | Query | Integer | N | If limit is not set, the default is 20 (maximum 1,000) |
| offset | Query | Integer | N | If offset is not set, the default is 0 |



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
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "Delivered",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | Total number of cases |
| templates | Array | |
| templates[].templateId | String | Template ID issued when registering a template |
| templates[].templateName | String | Template name |
| templates[].categoryId | String | Category ID |
| templates[].messageChannel | String | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | Sent content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array | |
| templates[].createdDateTime | String | Created at |
| templates[].updatedDateTime | String | Modified at |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View AlimTalk Template List

GET {{endpoint}}/template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0008ReadAlimtalkSenderTemplates"></span>

## View AlimTalk Sender-Related Templates

View templates associated with the sender or their assigned groups. (Template for the sender or group containing the sender)

**Request**

```
GET /template/v1.0/ALIMTALK/senders/{senderKey}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| senderKey | Path  | String | Y | Outgoing key |
| templateName | Query  | String | N | Template name (LIKE search) |
| templateStatus | Query | String | N | Template status |
| limit | Query | Integer | N | If limit is not set, default is 20 (maximum 1,000) |
| offset | Query | Integer | N | If offset is not set, default is 0 |



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
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "Delivered",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | Total counts |
| templates | Array |  |
| templates[].templateId | String | Template ID issued when registering a template |
| templates[].templateName | String | Template name |
| templates[].categoryId | String | Category ID |
| templates[].messageChannel | String | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | Sent content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array | |
| templates[].createdDateTime | String | Created at  |
| templates[].updatedDateTime | String | Modified at |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View AlimTalk Sender-Related Templates

GET {{endpoint}}/template/v1.0/ALIMTALK/senders/{{senderKey}}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/senders/${senderKey}/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0009ReadAlimtalkTemplate"></span>

## View AlimTalk Template Details

View template details.

**Request**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



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
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "template name",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "sender" : {
      "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
      "senderProfileId" : "@nhnCloud",
      "senderProfileType" : "GROUP"
    },
    "additionalProperty" : {
      "templateCode" : "templateCode",
      "kakaoTemplateCode" : "kakaoTemplateCode",
      "comments" : [ {
        "id" : 1,
        "content" : "sample inquiry",
        "userName" : "user name",
        "createdAt" : "2024-10-29T06:00:01.000+09:00",
        "attachments" : [ {
          "originalFileName" : "file name example",
          "filePath" : "/path/to/file"
        } ],
        "status" : "REQ"
      } ],
      "status" : "APPROVED",
      "block" : false,
      "dormant" : false
    },
    "content" : {
      "templateMessageType" : "BA",
      "templateEmphasizeType" : "NONE",
      "templateContent" : "#{Name}, your order has been successfully placed.",
      "templateAd" : "Follow our channel to receive marketing messages and updates via KakaoTalk",
      "templateExtra" : "* Please note that real-time availability can lead to overlapping bookings. If we cannot accommodate your stay, your reservation.\\n* Contact: 1234-1234",
      "templateTitle" : "123,450 KRW",
      "templateSubtitle" : "Approval Details",
      "templateHeader" : "Your order has been confirmed",
      "templateItem" : {
        "list" : [ {
          "title" : "item title",
          "description" : "item description"
        } ],
        "summary" : {
          "title" : "summary title",
          "description" : "summary description"
        }
      },
      "templateItemHighlight" : {
        "title" : "highlight title",
        "description" : "highlight description",
        "attachmentId" : "YaX2DA4Weab2",
        "imageUrl" : "https://example.com/thumbnail.jpg"
      },
      "templateRepresentLink" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "attachmentId" : "YaX2DA4Weab2",
      "templateImageName" : "image.png",
      "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
      "securityFlag" : false,
      "categoryCode" : "999999",
      "buttons" : [ {
        "ordering" : 1,
        "type" : "WL",
        "name" : "button name",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ],
      "quickReplies" : [ {
        "ordering" : 1,
        "type" : "WL",
        "name" : "Quick link name",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ]
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| template | Object |  |
| template.templateId | String | Template ID issued when registering a template |
| template.templateName | String | Template name |
| template.categoryId | String | Category ID |
| template.messageChannel | String | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | Sending content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array | |
| template.templateLanguage | String | Template type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object | |
| template.sender.senderKey | String | Sender profile sender key |
| template.sender.senderProfileId | String | KakaoTalk channel name |
| template.sender.senderProfileType | String | Sender profile type<br>[GROUP, NORMAL] |
| template.additionalProperty | Object | |
| template.additionalProperty.templateCode | String | Template code (English, numbers, -, _) |
| template.additionalProperty.kakaoTemplateCode | String | Kakao template code |
| template.additionalProperty.comments | Array | Template inquiry list |
| template.additionalProperty.comments[].id | Integer | Inquiry ID |
| template.additionalProperty.comments[].content | String | Inquiry content |
| template.additionalProperty.comments[].userName | String | Author |
| template.additionalProperty.comments[].createdAt | String | Created at |
| template.additionalProperty.comments[].attachments | Array | Inquiry attachments |
| template.additionalProperty.comments[].status | String | Inquiry status (REQ: Request, INQ: Inquiry, APR: Approved, REJ: Rejected, REP: Reply)<br>[REQ, INQ, APR, REJ, REP] |
| template.additionalProperty.status | String | REG: Request, REQ: Under review, APR: Approved, REJ: Rejected<br>[REG, REQ, APR, REJ] |
| template.additionalProperty.templateModificationStatus | String | REG: Request, REQ: Under review, APR: Approved, REJ: Rejected<br>[REG, REQ, APR, REJ] |
| template.additionalProperty.block | Boolean | Whether the template is blocked |
| template.additionalProperty.dormant | Boolean | Whether the template is dormant |
| template.content | Object | |
| template.content.templateMessageType | String | Template message type (BA: basic, EX: additional information, AD: channel addition, MI: composite, default: BA) |
| template.content.templateEmphasizeType | String | Template highlight type (NONE: basic, TEXT: highlight, IMAGE: image, ITEM_LIST: item list, default: NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| template.content.templateContent | String | Template body |
| template.content.templateAd | String | Channel addition notification message (template message type: channel addition, fixed value if composite) |
| template.content.templateExtra | String | Template additional information (required if template message type is [additional information/complex]), cannot use substitution variables, can include URLs |
| template.content.templateTitle | String | Template title (up to 50 characters, Android: 2 lines, 23 characters or more are truncated; iOS: 2 lines, 27 characters or more are truncated) |
| template.content.templateSubtitle | String | Template subtitle (up to 50 characters, Android: 18 characters or more are truncated; iOS: 21 characters or more are truncated) |
| template.content.templateHeader | String | Template header, variable Input possible |
| template.content.templateItem | Object |  |
| template.content.templateItem.list | Array |  |
| template.content.templateItem.list[].title | String | Item title |
| template.content.templateItem.list[].description | String | Item description |
| template.content.templateItem.summary | Object | |
| template.content.templateItem.summary.title | String | Summary title |
| template.content.templateItem.summary.description | String | Summary description (only variables, currency units, numbers, commas, and periods are allowed) |
| template.content.templateItemHighlight | Object | |
| template.content.templateItemHighlight.title | String | Item highlight title (up to 30 characters, 21 characters if a thumbnail image is present) |
| template.content.templateItemHighlight.description | String | Item highlight description (up to 19 characters, 13 characters if a thumbnail image is present) |
| template.content.templateItemHighlight.attachmentId | String | Template attachment file ID |
| template.content.templateItemHighlight.imageUrl | String | Thumbnail image address |
| template.content.templateRepresentLink | Object | |
| template.content.templateRepresentLink.linkMo | String | Mobile web link |
| template.content.templateRepresentLink.linkPc | String | PC web link |
| template.content.templateRepresentLink.schemeIos | String | iOS app link |
| template.content.templateRepresentLink.schemeAndroid | String | Android app link |
| template.content.attachmentId | String | Template attachment file ID |
| template.content.templateImageName | String | Template image name |
| template.content.templateImageUrl | String | Template image link |
| template.content.securityFlag | Boolean | Template security (default: false) |
| template.content.categoryCode | String | Template category code (refer to template category lookup API, default: 999999) |
| template.content.buttons | Array | Template button |
| template.content.buttons[].ordering | Integer | Template button order |
| template.content.buttons[].type | String | Template button type (WL: web link, AL: app link, DS: delivery tracking, BK: bot keyword, MD: message delivery, BC: consultation chat conversion, BT: bot conversion, AC: channel addition, BF: business form, P1: image security transmission plugin ID, P2: personal information use plugin ID, P3: one-click payment plugin ID)<br>[WL, AL, DS, BK, MD, BC, BT, AC, BF, P1, P2, P3] |
| template.content.buttons[].name | String | Template button name |
| template.content.buttons[].linkMo | String | Template button mobile web link |
| template.content.buttons[].linkPc | String | Template button PC web link |
| template.content.buttons[].schemeIos | String | Template button iOS app link |
| template.content.buttons[].schemeAndroid | String | Template button Android app link |
| template.content.buttons[].bizFormId | Integer | Template button business form ID (required for BF type) |
| template.content.quickReplies | Array | Template shortcut |
| template.content.quickReplies[].ordering | Integer | Template shortcut order |
| template.content.quickReplies[].type | String | Template shortcut type (WL: Web Link, AL: App Link, BK: Bot Keyword, BC: Chat Conversion, BT: Bot Conversion, BF: Business Form)<br>[WL, AL, BK, BC, BT, BF] |
| template.content.quickReplies[].name | String | Template shortcut name |
| template.content.quickReplies[].linkMo | String | Template shortcut mobile web link |
| template.content.quickReplies[].linkPc | String | Template PC web shortcut link |
| template.content.quickReplies[].schemeIos | String | Template iOS app shortcut link |
| template.content.quickReplies[].schemeAndroid | String | Template Android app shortcut link |
| template.content.quickReplies[].bizFormId | Integer | Template shortcut business form ID (required for BF type) |
| template.createdDateTime | String | Created at |
| template.updatedDateTime | String | Modified at |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View AlimTalk Template Details

GET {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0010UpdateAlimtalkTemplate"></span>

## Modify AlimTalk Template

Modify a template.

**Request**

```
PUT /template/v1.0/ALIMTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "#{Name}, your order has been successfully placed.",
    "templateAd" : "Follow our channel to receive marketing messages and updates via KakaoTalk",
    "templateExtra" : "* Please note that real-time availability can lead to overlapping bookings. If we cannot accommodate your stay, your reservation.\\n* Contact: 1234-1234",
    "templateTitle" : "123,450 KRW",
    "templateSubtitle" : "Approval Details",
    "templateHeader" : "Your order has been confirmed",
    "templateItem" : {
      "list" : [ {
        "title" : "item title",
        "description" : "item description"
      } ],
      "summary" : {
        "title" : "summary title",
        "description" : "summary description"
      }
    },
    "templateItemHighlight" : {
      "title" : "highlight title",
      "description" : "highlight description",
      "attachmentId" : "YaX2DA4Weab2",
      "imageUrl" : "https://example.com/thumbnail.jpg"
    },
    "templateRepresentLink" : {
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "attachmentId" : "YaX2DA4Weab2",
    "templateImageName" : "image.png",
    "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "securityFlag" : false,
    "categoryCode" : "999999",
    "buttons" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "button name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "Quick link name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ]
  },
  "additionalProperty" : {
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | Y | Template name |
| messagePurpose | String | N | Sending content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| content | Object | Y | |
| content.templateMessageType | String | N | Template message type (BA: basic, EX: additional information, AD: channel addition, MI: composite, default: BA) |
| content.templateEmphasizeType | String | N | Template highlight type (NONE: basic, TEXT: highlight, IMAGE: image, ITEM_LIST: item list, default: NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| content.templateContent | String | N | Template body |
| content.templateAd | String | N | Channel addition notification message (template message type: channel addition, fixed value if composite) |
| content.templateExtra | String | N | Template additional information (required when the template message type is [Additional Information/Composite]), substitution variables are not allowed, URLs can be included |
| content.templateTitle | String | N | Template title (up to 50 characters, Android: 2 lines, 23 or more characters are truncated, iOS: 2 lines, 27 or more characters are truncated) |
| content.templateSubtitle | String | N | Template additional text (up to 50 characters, Android: 18 or more characters are truncated, iOS: 21 or more characters are truncated) |
| content.templateHeader | String | N | Template header, variables can be entered |
| content.templateItem | Object | N | | |
| content.templateItem.list | Array | N | | |
| content.templateItem.list[].title | String | N | Item title |
| content.templateItem.list[].description | String | N | Item description |
| content.templateItem.summary | Object | N | |
| content.templateItem.summary.title | String | N | Summary title |
| content.templateItem.summary.description | String | N | Summary description (only variables, currency units, numbers, commas, and periods are allowed) |
| content.templateItemHighlight | Object | N | |
| content.templateItemHighlight.title | String | N | Item highlight title (up to 30 characters, 21 characters if a thumbnail image is present) |
| content.templateItemHighlight.description | String | N | Item highlight description (up to 19 characters, 13 characters if a thumbnail image is present) |
| content.templateItemHighlight.attachmentId | String | N | Template attachment ID |
| content.templateItemHighlight.imageUrl | String | N | Thumbnail image URL |
| content.templateRepresentLink | Object | N | | |
| content.templateRepresentLink.linkMo | String | N | Primary link mobile web link |
| content.templateRepresentLink.linkPc | String | N | Primary link PC web link |
| content.templateRepresentLink.schemeIos | String | N | Primary link iOS app link |
| content.templateRepresentLink.schemeAndroid | String | N | Primary link Android app link |
| content.attachmentId | String | N | Template attachment ID |
| content.templateImageName | String | N | Template image name |
| content.templateImageUrl | String | N | Template image link |
| content.securityFlag | Boolean | N | Template security status (default: false) |
| content.categoryCode | String | N | Template category code (refer to the template category query API, default: 999999) |
| content.buttons | Array | N | Template button |
| content.buttons[].ordering | Integer | N | Template button order |
| content.buttons[].type | String | N | Template button type (WL: Web Link, AL: App Link, DS: Delivery Tracking, BK: Bot Keyword, MD: Message Forwarding, BC: Consultation Chat Conversion, BT: Bot Conversion, AC: Channel Addition, BF: Business Form, P1: Image Security Transmission Plugin ID, P2: Personal Information Use Plugin ID, P3: One-Click Payment Plugin ID)<br>[WL, AL, DS, BK, MD, BC, BT, AC, BF, P1, P2, P3] |
| content.buttons[].name | String | N | Template button name |
| content.buttons[].linkMo | String | N | Template button mobile web link |
| content.buttons[].linkPc | String | N | Template button PC web link |
| content.buttons[].schemeIos | String | N | Template button iOS app link |
| content.buttons[].schemeAndroid | String | N | Template button Android app link |
| content.buttons[].bizFormId | Integer | N | Template button business form ID (required for BF type) |
| content.quickReplies | Array | N | Template shortcut |
| content.quickReplies[].ordering | Integer | N | Template shortcut order |
| content.quickReplies[].type | String | N | Template shortcut type (WL: Web Link, AL: App Link, BK: Bot Keyword, BC: Chat Conversion, BT: Bot Conversion, BF: Business Form)<br>[WL, AL, BK, BC, BT, BF] |
| content.quickReplies[].name | String | N | Template shortcut name |
| content.quickReplies[].linkMo | String | N | Template mobile web shortcut link |
| content.quickReplies[].linkPc | String | N | Template PC web shortcut link |
| content.quickReplies[].schemeIos | String | N | Template iOS app shortcut link |
| content.quickReplies[].schemeAndroid | String | N | Template Android app shortcut link |
| content.quickReplies[].bizFormId | Integer | N | Template shortcut business form ID (required for BF type) |
| additionalProperty | Object | Y | |
| additionalProperty.kakaoTemplateCode | String | Y | Kakao template code (English, numbers, -, _) |



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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Modify AlimTalk Template

PUT {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "#{Name}, your order has been successfully placed.",
    "templateAd" : "Follow our channel to receive marketing messages and updates via KakaoTalk",
    "templateExtra" : "* Please note that real-time availability can lead to overlapping bookings. If we cannot accommodate your stay, your reservation will be canceled.\\n* Contact: 1234-1234",
    "templateTitle" : "123,450 KRW",
    "templateSubtitle" : "Approval Details",
    "templateHeader" : "Your order has been confirmed",
    "templateItem" : {
      "list" : [ {
        "title" : "item title",
        "description" : "item description"
      } ],
      "summary" : {
        "title" : "summary title",
        "description" : "summary description"
      }
    },
    "templateItemHighlight" : {
      "title" : "highlight title",
      "description" : "highlight description",
      "attachmentId" : "YaX2DA4Weab2",
      "imageUrl" : "https://example.com/thumbnail.jpg"
    },
    "templateRepresentLink" : {
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "attachmentId" : "YaX2DA4Weab2",
    "templateImageName" : "image.png",
    "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "securityFlag" : false,
    "categoryCode" : "999999",
    "buttons" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "button name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "Quick link name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ]
  },
  "additionalProperty" : {
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "#{Name}, your order has been successfully placed.",
    "templateAd" : "Follow our channel to receive marketing messages and updates via KakaoTalk",
    "templateExtra" : "* Please note that real-time availability can lead to overlapping bookings. If we cannot accommodate your stay, your reservation will be canceled.\\n* Contact: 1234-1234",
    "templateTitle" : "123,450 KRW",
    "templateSubtitle" : "Approval Details",
    "templateHeader" : "Your order has been confirmed",
    "templateItem" : {
      "list" : [ {
        "title" : "item title",
        "description" : "item description"
      } ],
      "summary" : {
        "title" : "summary title",
        "description" : "summary description"
      }
    },
    "templateItemHighlight" : {
      "title" : "highlight title",
      "description" : "highlight description",
      "attachmentId" : "YaX2DA4Weab2",
      "imageUrl" : "https://example.com/thumbnail.jpg"
    },
    "templateRepresentLink" : {
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "attachmentId" : "YaX2DA4Weab2",
    "templateImageName" : "image.png",
    "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "securityFlag" : false,
    "categoryCode" : "999999",
    "buttons" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "button name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "Quick link name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ]
  },
  "additionalProperty" : {
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}'
```

</details>
<span id="templateV1x0011DeleteAlimtalkTemplate"></span>

## Delete AlimTalk Template

Delete a template.

**Request**

```
DELETE /template/v1.0/ALIMTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Delete AlimTalk Template

DELETE {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0012InquireAlimtalkTemplate"></span>

## Inquire about AlimTalk Template (deprecated)

!!! danger "Unsupported API."
    * Refer to the [Inquire about Kakao Alimtalk Template](#templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesKakaoTemplateCodeInquiriesPost).

Inquire about an AlimTalk template.

**Request**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/inquiries
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "comment" : "sample inquiry"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| comment | String | Y | Inquiry |



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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Inquire about AlimTalk Template

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/inquiries
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "comment" : "sample inquiry"
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/inquiries" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "comment" : "sample inquiry"
}'
```

</details>
<span id="templateV1x0013InquireAlimtalkTemplateWithFile"></span>

## Inquiry AlimTalk Template (file attached) (deprecated)

!!! danger "Unsupported API."
    * Refer to the [Inquire Kakao AlimTalk Template](#templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesKakaoTemplateCodeInquiriesDoWithFilePost).

Please attach a file when inquiring about an Alimtalk template.

**Request**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/inquiries/do-with-file
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Inquire about AlimTalk Template (File Attached)

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/inquiries/do-with-file
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/inquiries/do-with-file" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0014ReadAlimtalkTemplateModifications"></span>

## View Modified AlimTalk Template Lists (deprecated)

!!! danger "Unsupported API."
    * Refer to the [View AlimTalk Template's Kakao Template Lists](#templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesGet).

View modified AlimTalk template lists.

**Request**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}/modifications
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |
| limit | Query  | Integer | N | If limit is not set, default is 50 (maximum 1,000) |
| offset | Query | Integer | N | If offset is not set, default is 0 |



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
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "template name",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "sender" : {
      "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
      "senderProfileId" : "@nhnCloud",
      "senderProfileType" : "GROUP"
    },
    "additionalProperty" : {
      "templateCode" : "templateCode",
      "kakaoTemplateCode" : "kakaoTemplateCode",
      "comments" : [ {
        "id" : 1,
        "content" : "sample inquiry content",
        "userName" : "user name",
        "createdAt" : "2024-10-29T06:00:01.000+09:00",
        "attachments" : [ {
          "originalFileName" : "file name example",
          "filePath" : "/path/to/file"
        } ],
        "status" : "REQ"
      } ],
      "status" : "APR",
      "block" : false,
      "dormant" : false,
      "activated" : false
    },
    "content" : {
      "templateMessageType" : "BA",
      "templateEmphasizeType" : "NONE",
      "templateContent" : "#{Name}, your order has been successfully placed.",
      "templateAd" : "Follow our channel to receive marketing messages and updates via KakaoTalk",
      "templateExtra" : "* Please note that real-time availability can lead to overlapping bookings. If we cannot accommodate your stay, your reservation will be canceled.\\n* Contact: 1234-1234",
      "templateTitle" : "123,450 KRW",
      "templateSubtitle" : "Approval Details",
      "templateHeader" : "Your order has been confirmed",
      "templateItem" : {
        "list" : [ {
          "title" : "item title",
          "description" : "item description"
        } ],
        "summary" : {
          "title" : "summary title",
          "description" : "summary description"
        }
      },
      "templateItemHighlight" : {
        "title" : "highlight title",
        "description" : "highlight description",
        "attachmentId" : "YaX2DA4Weab2",
        "imageUrl" : "https://example.com/thumbnail.jpg"
      },
      "templateRepresentLink" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "attachmentId" : "YaX2DA4Weab2",
      "templateImageName" : "image.png",
      "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
      "securityFlag" : false,
      "categoryCode" : "999999",
      "buttons" : [ {
        "ordering" : 1,
        "type" : "WL",
        "name" : "button name",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ],
      "quickReplies" : [ {
        "ordering" : 1,
        "type" : "WL",
        "name" : "Quick link name",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ]
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | Total counts |
| templates | Array |  |
| templates[].templateId | String | Template ID issued when registering a template |
| templates[].templateName | String | Template name |
| templates[].categoryId | String | Category ID |
| templates[].messageChannel | String | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | Sent content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array | |
| templates[].templateLanguage | String | Template type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| templates[].sender | Object | |
| templates[].sender.senderKey | String | Sender profile sender key |
| templates[].sender.senderProfileId | String | KakaoTalk channel name |
| templates[].sender.senderProfileType | String | Sender profile type<br>[GROUP, NORMAL] |
| templates[].additionalProperty | Object | |
| templates[].additionalProperty.templateCode | String | Template code (English, numbers, -, _) |
| templates[].additionalProperty.kakaoTemplateCode | String | Kakao template code |
| templates[].additionalProperty.comments | Array | Template inquiry list |
| templates[].additionalProperty.status | String | REG: Request, REQ: Under review, APR: Approved, REJ: Rejected<br>[REG, REQ, APR, REJ] |
| templates[].additionalProperty.block | Boolean | Template block status |
| templates[].additionalProperty.dormant | Boolean | Template dormancy status|
| templates[].additionalProperty.activated | Boolean | Template activation status |
| templates[].content | Object |  |
| templates[].content.templateMessageType | String | Template message type (BA: basic, EX: additional information, AD: channel addition, MI: composite, default: BA) |
| templates[].content.templateEmphasizeType | String | Template highlight type (NONE: basic, TEXT: highlight, IMAGE: image, ITEM_LIST: item list, default: NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| templates[].content.templateContent | String | Template body |
| templates[].content.templateAd | String | Channel addition notification message (template message type: channel addition, fixed value if composite) |
| templates[].content.templateExtra | String | Template additional information (required if template message type is [additional information/complex]), cannot use substitution variables, can include URLs |
| templates[].content.templateTitle | String | Template title (up to 50 characters, Android: 2 lines, truncation after 23 characters, iOS: 2 lines, truncation after 27 characters) |
| templates[].content.templateSubtitle | String | Template subtitle (up to 50 characters, Android: 18 characters or more, truncation after 21 characters) |
| templates[].content.templateHeader | String | Template header, variable input possible |
| templates[].content.templateItem | Object | |
| templates[].content.templateItem.list | Array | |
| templates[].content.templateItem.summary | Object | |
| templates[].content.templateItem.summary.title | String | Summary title |
| templates[].content.templateItem.summary.description | String | Summary description (only variables, currency units, numbers, commas, and periods are allowed) |
| templates[].content.templateItemHighlight | Object | |
| templates[].content.templateItemHighlight.title | String | Item highlight title (up to 30 characters, 21 characters if a thumbnail image is present) |
| templates[].content.templateItemHighlight.description | String | Item highlight description (up to 19 characters, 13 characters if a thumbnail image is present) |
| templates[].content.templateItemHighlight.attachmentId | String | Template attachment ID |
| templates[].content.templateItemHighlight.imageUrl | String | Thumbnail image address |
| templates[].content.templateRepresentLink | Object |  |
| templates[].content.templateRepresentLink.linkMo | String | Primary link mobile web Link |
| templates[].content.templateRepresentLink.linkPc | String | Primary link PC web link |
| templates[].content.templateRepresentLink.schemeIos | String | Primary link iOS app link |
| templates[].content.templateRepresentLink.schemeAndroid | String | Primary link Android app link |
| templates[].content.attachmentId | String | Template attachment file ID |
| templates[].content.templateImageName | String | Template image name |
| templates[].content.templateImageUrl | String | Template image link |
| templates[].content.securityFlag | Boolean | Template security status (default: false) |
| templates[].content.categoryCode | String | Template category code (refer to the template category query API, default: 999999) |
| templates[].content.buttons | Array | Template button |
| templates[].content.quickReplies | Array | Template shortcut |
| templates[].createdDateTime | String | Created at |
| templates[].updatedDateTime | String | Modified at |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View Modified AlimTalk Template List

GET {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/modifications
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/modifications" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>

<span id="templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesGet"></span>

## View AlimTalk Template's Kakao Template List

View the Kakao template list for an AlimTalk template.

**Request**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates
```

**Request parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | Access token |
| templateId | Path | String | Y | Template ID |
| limit | Query | Integer | N | If limit is not set, default is 20 (maximum 1,000) |
| offset | Query | Integer | N | If offset is not set, default is 0 |



**Request body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.



**Response body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "templates" : [ {
    "kakaoTemplateCode" : "kakaoTemplateCode",
    "kakaoTemplateName" : "template name",
    "content" : {
      "templateMessageType" : "BA",
      "templateEmphasizeType" : "NONE",
      "templateContent" : "#{Name}, your order has been successfully placed.",
      "templateAd" : "Follow our channel to receive marketing messages and updates via KakaoTalk",
      "templateExtra" : "* Please note that real-time availability can lead to overlapping bookings. If we cannot accommodate your stay, your reservation will be canceled.\\n* Contact: 1234-1234",
      "templateTitle" : "123,450 KRW",
      "templateSubtitle" : "Approval Details",
      "templateHeader" : "Your order has been confirmed",
      "templateItem" : {
        "list" : [ {
          "title" : "item title",
          "description" : "item description"
        } ],
        "summary" : {
          "title" : "summary title",
          "description" : "summary description"
        }
      },
      "templateItemHighlight" : {
        "title" : "highlight title",
        "description" : "highlight description",
        "attachmentId" : "YaX2DA4Weab2",
        "imageUrl" : "https://example.com/thumbnail.jpg"
      },
      "templateRepresentLink" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "attachmentId" : "YaX2DA4Weab2",
      "templateImageName" : "image.png",
      "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
      "securityFlag" : false,
      "categoryCode" : "999999",
      "buttons" : [ {
        "ordering" : 1,
        "type" : "WL",
        "name" : "button name",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ],
      "quickReplies" : [ {
        "ordering" : 1,
        "type" : "WL",
        "name" : "Quick link name",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ]
    },
    "reviewStatus" : "APPROVED",
    "comments" : [ {
      "id" : 1,
      "content" : "sample inquiry content",
      "userName" : "user name",
      "createdAt" : "2024-10-29T06:00:01.000+09:00",
      "attachments" : [ {
        "originalFileName" : "file name example",
        "filePath" : "/path/to/file"
      } ],
      "status" : "REQ"
    } ],
    "block" : false,
    "dormant" : false,
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description                                                                                                                       |
| - | - |--------------------------------------------------------------------------------------------------------------------------|
| header | Object |                                                                                                                          |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true                                                                                        |
| header.resultCode | Integer | The result code of the request.<br>Default: 0                                                                                                  |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS                                                                                           |
| totalCount | Integer | Total counts                                                                                                                     |
| templates | Array |                                                                                                                          |
| templates[].kakaoTemplateCode | String | Kakao Template Code |
| templates[].kakaoTemplateName | String | Template Name |
| templates[].content | Object | |
| templates[].content.templateMessageType | String | Template Message Type (BA: Basic, EX: Additional Information, AD: Channel Addition, MI: Composite, default: BA) |
| templates[].content.templateEmphasizeType | String | Template Emphasize Type (NONE: Basic, TEXT: Emphasize, IMAGE: Image, ITEM_LIST: Item List, default: NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| templates[].content.templateContent | String | Template Body |
| templates[].content.templateAd | String | Channel Addition Notification Message (Template Message Type: Channel Addition, Fixed Value for Composite) |
| templates[].content.templateExtra | String | Template additional information (required when the template message type is [Additional Information Type/Composite Type]), substitution variables are not allowed, URLs can be included |
| templates[].content.templateTitle | String | Template title (up to 50 characters, Android: 2 lines, 23 or more characters are truncated, iOS: 2 lines, 27 or more characters are truncated) |
| templates[].content.templateSubtitle | String | Template additional text (up to 50 characters, Android: 18 or more characters are truncated, iOS: 21 or more characters are truncated) |
| templates[].content.templateHeader | String | Template header, variables can be entered |
| templates[].content.templateItem | Object | |
| templates[].content.templateItem.list | Array | |
| templates[].content.templateItem.summary | Object | |
| templates[].content.templateItem.summary.title | String | Summary title |
| templates[].content.templateItem.summary.description | String | Summary description (only variables, currency units, numbers, commas, and periods are allowed) |
| templates[].content.templateItemHighlight | Object | |
| templates[].content.templateItemHighlight.title | String | Item highlight title (up to 30 characters, 21 characters if a thumbnail image is present) |
| templates[].content.templateItemHighlight.description | String | Item highlight description (up to 19 characters, 13 characters if a thumbnail image is present) |
| templates[].content.templateItemHighlight.attachmentId | String | Template attachment ID |
| templates[].content.templateItemHighlight.imageUrl | String | Thumbnail image URL                                                                                                               |
| templates[].content.templateRepresentLink | Object |                                                                                                                          |
| templates[].content.templateRepresentLink.linkMo | String | Primary link mobile web pink |
| templates[].content.templateRepresentLink.linkPc | String | Primary link PC web link |
| templates[].content.templateRepresentLink.schemeIos | String | Primary link iOS app link |
| templates[].content.templateRepresentLink.schemeAndroid | String | Primary link Android app link |
| templates[].content.attachmentId | String | Template attachment file ID |
| templates[].content.templateImageName | String | Template image name |
| templates[].content.templateImageUrl | String | Template image link |
| templates[].content.securityFlag | Boolean | Template security status (default: false) |
| templates[].content.categoryCode | String | Template category code (refer to the template category query API, default: 999999) |
| templates[].content.buttons | Array | Template button |
| templates[].content.quickReplies | Array | Template shorcut |
| templates[].reviewStatus | String | REGISTERED: Request, REQUESTED: Reviewing, APPROVED: Approved, REJECTED: Rejected<br>[REGISTERED, REQUESTED, APPROVED, REJECTED] |
| templates[].comments | Array | List of Template Comments                                                                                                               |
| templates[].block | Boolean | Template block status                                                                                                                |
| templates[].dormant | Boolean | Template dormancy status                                                                                                                |
| templates[].createdDateTime | String | Created at                                                                                                                |
| templates[].updatedDateTime | String | Modified at                                                                                                               |



**Request example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View AlimTalk Template's Kakao Template List

GET {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/kakao-templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/kakao-templates" \
-H "X-NC-APP-KEY: {appKey}"  \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
<span id="templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesKakaoTemplateCodeInquiriesDoWithFilePost"></span>

## Inquire about Kakao AlimTalk Template (Attach File)

When inquiring about KakaoTalk AlimTalk templates, please attach the file.

**Request**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates/{kakaoTemplateCode}/inquiries/do-with-file
```

**Request parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | Access token |
| templateId | Path | String | Y | Template ID |
| kakaoTemplateCode | Path | String | Y | Kakao template code |

**Request body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| comment | String | Y | Inquiry details |
| file | Binary | Y | Inquiry files |

### 응답 본문

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
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Inquire about Kakao AlimTalk Template (Attach File)

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/kakao-templates/{{kakaoTemplateCode}}/inquiries/do-with-file
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
Content-Type: multipart/form-data; boundary=boundary

--boundary
Content-Disposition: form-data; name="comment"

comment_example
--boundary
Content-Disposition: form-data; name="file"; filename="file.txt"
Content-Type: text/plain

< /path/to/file.txt
--boundary--
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/kakao-templates/${kakaoTemplateCode}/inquiries/do-with-file" \
-H "X-NC-APP-KEY: {appKey}"  \
-H "X-NHN-Authorization: Bearer {accessToken}"  \
-F "comment=comment_example" \
-F "file=@/path/to/file.txt"
```

</details>
<span id="templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesKakaoTemplateCodeInquiriesPost"></span>

## Inquire about Kakao AlimTalk Template

Inquire about a Kakao AlimTalk template.

**Request**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates/{kakaoTemplateCode}/inquiries
```

**Request parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | Access token |
| templateId | Path | String | Y | Template ID |
| kakaoTemplateCode | Path | String | Y | Kakao template coe |



**Request body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "comment" : "sample inquiry content"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| comment | String | Y | Inquiry details |



**Response body**

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
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Inquire about Kakao AlimTalk Template

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/kakao-templates/{{kakaoTemplateCode}}/inquiries
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "comment" : "sample inquiry content"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/kakao-templates/${kakaoTemplateCode}/inquiries" \
-H "X-NC-APP-KEY: {appKey}"  \
-H "X-NHN-Authorization: Bearer {accessToken}"  \
-d '{
  "comment" : "sample inquiry content"
}'
```

</details>

<span id="templateV1x0015ReadAlimtalkTemplateCategories"></span>

## View AimTalk Template Category List

View an AlimTalk template category list.

**Request**

```
GET /template/v1.0/ALIMTALK/template-categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |



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
  "categories" : [ {
    "name" : "purchase",
    "subCategories" : [ {
      "code" : "002001",
      "name" : "purchased",
      "groupName" : "purchase",
      "inclusion" : "Applicable to 'Order Confirmed' and 'Purchase Completed' templates.",
      "exclusion" : "Templates with booking or reservation details will be categorized as 'Bookings' instead of 'Purchased'."
    } ]
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| categories | Array |  |
| categories[].name | String | Main category name |
| categories[].subCategories | Array | Subcategories |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View AlimTalk Template Category List

GET {{endpoint}}/template/v1.0/ALIMTALK/template-categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/template-categories" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>

<span id="templateV1x0021CreateEmailTemplate"></span>

## Register Email Template

Register a template.

**Request**

```
POST /template/v1.0/EMAIL/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] monitoring notification",
    "body" : "Hello. Your product arrived today.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | Y | Template name |
| categoryId | String | N | Category ID |
| messagePurpose | String | N | Sent content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | Template type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N | |
| sender.senderMailAddress | String | Y | Sender email address |
| content | Object | Y | |
| content.title | String | N | Template email title |
| content.body | String | N | Template email body |
| content.attachmentIds | Array | N | Template attachment ID |



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "templateId" : "A9z0A9z0"
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| templateId | String | Template ID issued when registering a template |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Register Email Template

POST {{endpoint}}/template/v1.0/EMAIL/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] monitoring notification",
    "body" : "Hello. Your product arrived today.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/EMAIL/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] monitoring notification",
    "body" : "Hello. Your product arrived today.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>
<span id="templateV1x0022ReadEmailTemplate"></span>

## View Email Template Details

View template details.

**Request**

```
GET /template/v1.0/EMAIL/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



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
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "template name",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "sender" : {
      "senderMailAddress" : "abcde@nhn.com"
    },
    "content" : {
      "title" : "[NHN Cloud Email][##env##] monitoring notification",
      "body" : "Hello. Your product arrived today.",
      "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| template | Object |  |
| template.templateId | String | Template ID issued when registering a template |
| template.templateName | String | Template name |
| template.categoryId | String | Category ID |
| template.messageChannel | String | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | Sent content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array | |
| template.templateLanguage | String | Template type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object | |
| template.sender.senderMailAddress | String | Sender email address |
| template.content | Object | |
| template.content.title | String | Template email subject |
| template.content.body | String | Template email body |
| template.content.attachmentIds | Array | template attachment ID |
| template.createdDateTime | String | Created at |
| template.updatedDateTime | String | Modified at |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View Email Template Details

GET {{endpoint}}/template/v1.0/EMAIL/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/EMAIL/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0022ReadEmailTemplateList"></span>

## View Email Template List

View a template list.

**Request**

```
GET /template/v1.0/EMAIL/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateName | Query  | String | N | Template name (LIKE search) |
| limit | Query | Integer | N | If limit is not set, default is 20 (maximum 1,000) |
| offset | Query | Integer | N | If offset is not set, default is 0 |



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
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "Delivered",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | Total counts |
| templates | Array |  |
| templates[].templateId | String | Template ID issued when registering a template |
| templates[].templateName | String | Template name |
| templates[].categoryId | String | Category ID |
| templates[].messageChannel | String | Message channel <br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | Sender content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | Created at |
| templates[].updatedDateTime | String | Modified at |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View Email Template List

GET {{endpoint}}/template/v1.0/EMAIL/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/EMAIL/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0023UpdateEmailTemplate"></span>

## Modify Email Template

Modify a template.

**Request**

```
PUT /template/v1.0/EMAIL/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] monitoring alarm",
    "body" : "Hello. Your product arrived today.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | Y | Template name |
| messagePurpose | String | N | Sender content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | Template type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N | |
| sender.senderMailAddress | String | Y | Sender email address |
| content | Object | Y | |
| content.title | String | N | Template email title |
| content.body | String | N | Template email body |
| content.attachmentIds | Array | N | Template attachment ID |



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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Modify Email Template

PUT {{endpoint}}/template/v1.0/EMAIL/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] monitoring alarm",
    "body" : "Hello. Your product arrived today.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/EMAIL/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] monitoring alarm",
    "body" : "Hello. Your product arrived today.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>
<span id="templateV1x0024DeleteEmailTemplate"></span>

## Delete Email Template

Delete a template.

**Request**

```
DELETE /template/v1.0/EMAIL/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Delete Email Template

DELETE {{endpoint}}/template/v1.0/EMAIL/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/EMAIL/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0025CreateRcsTemplate"></span>

## Register RCS Template

Register a template.

**Request**

```
POST /template/v1.0/RCS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday Service Hours",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience. :)",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "title",
      "description" : "body",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "main title",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "title 1",
      "title2" : "title 2",
      "title3" : "title 3",
      "description1" : "body 1",
      "description2" : "body 2",
      "description3" : "body 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "schedule title",
                "description" : "schedule description"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "schedule title",
              "description" : "schedule description"
            }
          }
        }
      }
    } ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | Y | Template name |
| categoryId | String | N | Category ID |
| messagePurpose | String | N | Sent content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | Template type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | Y | |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chat room (chatbot) ID |
| content | Object | Y | |
| content.messageType | String | N | RCS Message type<br>[SMS, LMS, MMS, RBC_TEMPLATE] |
| content.title | String | N | Message title |
| content.body | String | N | Message body |
| content.smsType | String | N | SMS type<br>[STANDALONE] |
| content.lmsType | String | N | LMS type<br>[STANDALONE, FORMAT_BASIC, FORMAT_TITLE_HIGHLIGHT, FORMAT_PARAGRAPH] |
| content.mmsType | String | N | MMS type (required for MMS transmission)<br>[HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL] |
| content.messagebaseId | String | N | RCS Biz center template ID |
| content.unsubscribePhoneNumber | String | N | Unsubscribe number (required for advertising transmission) |
| content.cards | Array | N | RCS card |
| content.cards[].title | String | N | title |
| content.cards[].description | String | N | body |
| content.cards[].attachmentId | String | N | Image attachment file ID |
| content.cards[].mTitle | String | N | Main Title |
| content.cards[].mTitleMedia | String | N | Main title logo file ID |
| content.cards[].title1 | String | N | Title 1 |
| content.cards[].title2 | String | N | Title 2 |
| content.cards[].title3 | String | N | Title 3 |
| content.cards[].description1 | String | N | Body 1 |
| content.cards[].description2 | String | N | Body 2 |
| content.cards[].description3 | String | N | Body 3 |
| content.cards[].buttons | Array | N | |
| content.buttons | Array | N | RCS button list |
| content.buttons[].buttonType | String | N | An action object with the same name as the buttonType value is included as buttonJson.<br>Button types: Open chat room (COMPOSE), Copy (CLIPBOARD), Make a phone call (DIALER), Show map (MAP_SHOW), Search map (MAP_QUERY), Share current location (MAP_SHARE), Connect URL (URL), Register schedule (CALENDAR)<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | N | |
| content.buttons[].buttonJson.action | Object | N | Button action |



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "templateId" : "A9z0A9z0"
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| templateId | String | Template ID issued when registering a template |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Register RCS Template

POST {{endpoint}}/template/v1.0/RCS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday Service Hours",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience. :)",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "title",
      "description" : "body",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "main title",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "title 1",
      "title2" : "title 2",
      "title3" : "title 3",
      "description1" : "body 1",
      "description2" : "body 2",
      "description3" : "body 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "schedule title",
                "description" : "schedule description"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "schedule title",
              "description" : "schedule description"
            }
          }
        }
      }
    } ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/RCS/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday Service Hours",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience. :)",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "title",
      "description" : "body",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "main title",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "title 1",
      "title2" : "title 2",
      "title3" : "title 3",
      "description1" : "body 1",
      "description2" : "body 2",
      "description3" : "body 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "schedule title",
                "description" : "schedule description"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "schedule title",
              "description" : "schedule description"
            }
          }
        }
      }
    } ]
  }
}'
```

</details>
<span id="templateV1x0026ReadRcsTemplateList"></span>

## View RCS Template List

View a template list.

**Request**

```
GET /template/v1.0/RCS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateName | Query  | String | N | Template name (LIKE search) |
| limit | Query | Integer | N | If limit is not set, default is 20 (maximum 1,000) |
| offset | Query | Integer | N | If offset is not set, default is 0 |



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
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "Delivered",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | Total counts |
| templates | Array |  |
| templates[].templateId | String | Template ID issued when registering a template |
| templates[].templateName | String | Template name |
| templates[].categoryId | String | Category ID |
| templates[].messageChannel | String | Message channel <br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | Sender content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | Created at |
| templates[].updatedDateTime | String | Modified at |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View RCS Template List

GET {{endpoint}}/template/v1.0/RCS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/RCS/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0027ReadRcsTemplate"></span>

## View RCS Template Details

View template details.

**Request**

```
GET /template/v1.0/RCS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



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
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "template name",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "sender" : {
      "brandId" : "AR.lj0eOjEI7Y",
      "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
    },
    "content" : {
      "messageType" : "SMS",
      "title" : "Holiday Service Hours",
      "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience. :)",
      "smsType" : "STANDALONE",
      "lmsType" : "HORIZONTAL",
      "mmsType" : "HORIZONTAL",
      "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
      "messagebaseformId" : "SS000000",
      "unsubscribePhoneNumber" : "08012341234",
      "cards" : [ {
        "title" : "title",
        "description" : "body",
        "attachmentId" : "20240814125609swLmoZTsGr0",
        "mTitle" : "main title",
        "mTitleMedia" : "LT-messagebase.common-2k8ydI",
        "title1" : "title 1",
        "title2" : "title 2",
        "title3" : "title 3",
        "description1" : "body 1",
        "description2" : "body 2",
        "description3" : "body 3",
        "buttons" : [ {
          "buttonType" : "CALENDAR",
          "buttonJson" : {
            "action" : {
              "displayText" : "register schedule",
              "calendarAction" : {
                "createCalendarEvent" : {
                  "startTime" : "2024-01-01T00:00:00.000+09:00",
                  "endTime" : "2024-01-01T00:00:00.000+09:00",
                  "title" : "schedule title",
                  "description" : "schedule description"
                }
              }
            }
          }
        } ]
      } ],
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "schedule title",
                "description" : "schedule description"
              }
            }
          }
        }
      } ]
    },
    "additionalProperty" : {
      "status" : "SUCCESS",
      "approvedDateTime" : "2024-10-29T06:00:01.000+09:00"
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| template | Object |  |
| template.templateId | String | Template ID issued when registering a template |
| template.templateName | String | Template name |
| template.categoryId | String | Category ID |
| template.messageChannel | String | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | Sent content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array | |
| template.templateLanguage | String | Template type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object | |
| template.sender.brandId | String | Brand ID |
| template.sender.chatbotId | String | Chat room (chatbot) ID |
| template.content | Object | |
| template.content.messageType | String | RCS Message type<br>[SMS, LMS, MMS, RBC_TEMPLATE] |
| template.content.title | String | Message title |
| template.content.body | String | Message body |
| template.content.smsType | String | SMS type<br>[STANDALONE] |
| template.content.lmsType | String | LMS type<br>[STANDALONE, FORMAT_BASIC, FORMAT_TITLE_HIGHLIGHT, FORMAT_PARAGRAPH] |
| template.content.mmsType | String | MMS type (required for MMS sending)<br>[HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL] |
| template.content.messagebaseId | String | RCS Biz center template ID |
| template.content.messagebaseformId | String | messageBase format specified by RCS Biz Center<br><br>[SS000000 (basic), SL000000 (basic), OL00000001 (lms format basic), OL00000002 (lms format title emphasis), OL00000003 (lms format paragraph), SMwThT00 (mms vertical), SMwThM00 (mms horizontal), CMwMhM0200 (mms slide medium (2)), CMwMhM0300 (mms slide medium (3)), CMwMhM0400 (mms slide medium (4)), CMwMhM0500 (mms slide medium (5)), CMwMhM0600 (mms slide medium (6)), CMwShS0200 (mms slide small (2)), CMwShS0300 (mms slide small (3)), CMwShS0400 (mms slide small type (4)), CMwShS0500 (mms slide small type (5)), CMwShS0600 (mms slide small type (6)), CLI00001 (item detail type), ITTBNV (thumbnail type (vertical)), ITTBNH (thumbnail type (horizontal)), ITHIMS (image emphasis type (1:1)), ITHIMV (image emphasis type (3:4)), ITSNSS (sns type), ITSNSH (sns type (middle button)), ITHITS (image & title emphasis type (1:1)), ITHITV (image & title emphasis type (3:4)), ITCRM2 (slide type (2)), ITCRM3 (slide type (3)), ITCRM4 (slide type (4)), ITCRM5 (slide type (5)), ITCRM6 (slide type (6)), CLT00001 (item emphasis type) desc), CLT00002 (item emphasis table), TATA001C (title free style free), TATA001D (title free style cell), TATA001F (title free style desc), FF005C (title selection free), FF005D (specification cell), FF004C (specification desc), FF004D (cancellation cell), GG003C (cancellation desc), GG003D (guidance cell), GG002C (guidance desc), GG002D (authentication cell), GG001C (authentication desc), GG001D (membership registration cell), GG000F (membership registration desc), EE001C (reservation cell), EE001D (reservation desc), CC003C (delivery cell), CC003D (delivery desc), FF002C (deposit cell), FF002D (deposit desc), FF001C (approval cell), FF001D (approval desc), CC002C (order cell), CC002D (order desc), CC001C (shipping cell), CC001D (shipping desc), FF003C (withdrawal cell), FF003D (withdrawal desc), CLL00001 (lms statement a), CLL00002 (lms paragraph type), CLL00003 (lms title emphasis type), CLL00004 (lms basic type), CLL00005 (lms statement b), CLL00006 (lms statement c)]
| template.content.unsubscribePhoneNumber | String | Opt-out number (required when sending advertisements) |
| template.content.cards | Array | RCS card |
| template.content.cards[].title | String | Title |
| template.content.cards[].description | String | Body |
| template.content.cards[].attachmentId | String | Image attachment file ID |
| template.content.cards[].mTitle | String | Main Title |
| template.content.cards[].mTitleMedia | String | Main title logo file ID|
| template.content.cards[].title1 | String | Title 1 |
| template.content.cards[].title2 | String | Title 2 |
| template.content.cards[].title3 | String | Title 3 |
| template.content.cards[].description1 | String | Body 1 |
| template.content.cards[].description2 | String | Body 2 |
| template.content.cards[].description3 | String | Body 3 |
| template.content.cards[].buttons | Array |  |
| template.content.buttons | Array | RCS button list |
| template.content.buttons[].buttonType | String | An Action object with the same name as the buttonType value is included as buttonJson.<br>Button types: Open a chat room (COMPOSE), Copy (CLIPBOARD), Make a phone call (DIALER), Show a map (MAP_SHOW), Search a map (MAP_QUERY), Share the current location (MAP_SHARE), Connect to a URL (URL), Register a schedule (CALENDAR)<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| template.content.buttons[].buttonJson | Object | |
| template.content.buttons[].buttonJson.action | Object | Button action |
| template.additionalProperty | Object |  |
| template.additionalProperty.status | String | Template status<br>- SAVE: Saved<br>- APPROVE_WAIT: Pending Approval<br>- INSPECTION_START: Review in Progress<br>- INSPECTION_FINISH: Review Completed<br>- APPROVE: Approved<br>- REJECT: Rejected<br>- MODIFY_APPROVE_WAIT: Modification Pending Approval<br>- MODIFY_INSPECTION_START: Modification Review in Progress<br>- MODIFY_INSPECTION_FINISH: Modification Review Completed<br>- MODIFY_REJECT: Modification Rejected<br><br>[SAVE, APPROVE_WAIT, INSPECTION_START, INSPECTION_FINISH, APPROVE, REJECT, MODIFY_APPROVE_WAIT, MODIFY_INSPECTION_START, MODIFY_INSPECTION_FINISH, MODIFY_REJECT] |
| template.additionalProperty.approvedDateTime | String | Approved at |
| template.createdDateTime | String | Created at |
| template.updatedDateTime | String | Modified at |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View RCS Template Details

GET {{endpoint}}/template/v1.0/RCS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/RCS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0028UpdateRcsTemplate"></span>

## Modify RCS Template

Modify a template.

**Request**

```
PUT /template/v1.0/RCS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday Service Hours",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience. :)",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "title",
      "description" : "body",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "main title",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "title 1",
      "title2" : "title 2",
      "title3" : "title 3",
      "description1" : "body 1",
      "description2" : "body 2",
      "description3" : "body 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "schedule title",
                "description" : "schedule description"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "schedule title",
              "description" : "schedule description"
            }
          }
        }
      }
    } ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | Y | Template name |
| messagePurpose | String | N | Sender content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | Template type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N | |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chat room (chatbot) ID |
| content | Object | Y | | |
| content.messageType | String | N | RCS Message type<br>[SMS, LMS, MMS, RBC_TEMPLATE] |
| content.title | String | N | Message title |
| content.body | String | N | Message body |
| content.smsType | String | N | SMS type<br>[STANDALONE] |
| content.lmsType | String | N | LMS type<br>[STANDALONE, FORMAT_BASIC, FORMAT_TITLE_HIGHLIGHT, FORMAT_PARAGRAPH] |
| content.mmsType | String | N | MMS type (required for MMS transmission)<br>[HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL] |
| content.messagebaseId | String | N | RCS Biz center template ID |
| content.unsubscribePhoneNumber | String | N | Opt-out Number (required for advertising transmission) |
| content.cards | Array | N | RCS card |
| content.cards[].title | String | N | Title |
| content.cards[].description | String | N | Body |
| content.cards[].attachmentId | String | N | Image attachment file ID |
| content.cards[].mTitle | String | N | Main Title |
| content.cards[].mTitleMedia | String | N | Main title logo file ID |
| content.cards[].title1 | String | N | Title 1 |
| content.cards[].title2 | String | N | Title 2 |
| content.cards[].title3 | String | N | Title 3 |
| content.cards[].description1 | String | N | Body 1 |
| content.cards[].description2 | String | N | Body 2 |
| content.cards[].description3 | String | N | Body 3 |
| content.cards[].buttons | Array | N |  |
| content.buttons | Array | N | RCS button list |
| content.buttons[].buttonType | String | N | an Action object with the same name as the buttonType value is included as buttonJson.<br>Button types: Open a chat room (COMPOSE), Copy (CLIPBOARD), Make a phone call (DIALER), Show a map (MAP_SHOW), Search a map (MAP_QUERY), Share the current location (MAP_SHARE), Connect to a URL (URL), Register a schedule (CALENDAR)<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| template.content.buttons[].buttonJson | Object | |
| template.content.buttons[].buttonJson.action | Object | Button action



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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Modify RCS Template

PUT {{endpoint}}/template/v1.0/RCS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday Service Hours",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience. :)",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "title",
      "description" : "body",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "main title",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "title 1",
      "title2" : "title 2",
      "title3" : "title 3",
      "description1" : "body 1",
      "description2" : "body 2",
      "description3" : "body 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "schedule title",
                "description" : "schedule description"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "schedule title",
              "description" : "schedule description"
            }
          }
        }
      }
    } ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/RCS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday Service Hours",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience. :)",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "title",
      "description" : "body",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "main title",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "title 1",
      "title2" : "title 2",
      "title3" : "title 3",
      "description1" : "body 1",
      "description2" : "body 2",
      "description3" : "body 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "schedule title",
                "description" : "schedule description"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "schedule title",
              "description" : "schedule description"
            }
          }
        }
      }
    } ]
  }
}'
```

</details>
<span id="templateV1x0029DeleteRcsTemplate"></span>

## Delete RCS Template

Delete an RCS template.

**Request**

```
DELETE /template/v1.0/RCS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Delete RCS Template

DELETE {{endpoint}}/template/v1.0/RCS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/RCS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0030CreatePushTemplate"></span>

## Register Push Template

register a template.

**Request**

```
POST /template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "main number",
    "unsubscribeGuide" : "menu > settings",
    "title" : "title",
    "body" : "contents",
    "richMessage" : {
      "buttons" : [ {
        "name" : "button name",
        "submitName" : "send button name",
        "buttonType" : "button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "link upon clicking button",
        "hint" : "button hint"
      } ],
      "media" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "location of large icon, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "group key, a feature to group multiple messages together, supported on Android only",
        "description" : "group description"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | Y | Template name |
| categoryId | String | N | Category ID |
| messagePurpose | String | N | Sent Content Type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | Template Type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| content | Object | Y | Push message content |



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "templateId" : "A9z0A9z0"
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| templateId | String | Template ID issued when registering a template |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Register Push Template

POST {{endpoint}}/template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "main number",
    "unsubscribeGuide" : "menu > settings",
    "title" : "title",
    "body" : "contents",
    "richMessage" : {
      "buttons" : [ {
        "name" : "button name",
        "submitName" : "send button name",
        "buttonType" : "button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "link upon clicking button",
        "hint" : "button hint"
      } ],
      "media" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "location of large icon, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "group key, a feature to group multiple messages together, supported on Android only",
        "description" : "group description"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/PUSH/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "main number",
    "unsubscribeGuide" : "menu > settings",
    "title" : "title",
    "body" : "contents",
    "richMessage" : {
      "buttons" : [ {
        "name" : "button name",
        "submitName" : "send button name",
        "buttonType" : "button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "link upon clicking button",
        "hint" : "button hint"
      } ],
      "media" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "location of large icon, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "group key, a feature to group multiple messages together, supported on Android only",
        "description" : "group description"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}'
```

</details>
<span id="templateV1x0031ReadPushTemplateList"></span>

## View Push Template List

View a template list.

**Request**

```
GET /template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateName | Query  | String | N | Template name (LIKE search) |
| limit | Query | Integer | N | If limit is not set, default is 20 (maximum 1,000) |
| offset | Query | Integer | N | If offset is not set, default is 0 |



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
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "Delivered",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | Total counts |
| templates | Array |  |
| templates[].templateId | String | When registering a template, the issued template ID |
| templates[].templateName | String | Template name |
| templates[].categoryId | String | Category ID |
| templates[].messageChannel | String | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | Message type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | Created at |
| templates[].updatedDateTime | String | Modified at |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View Push Template List

GET {{endpoint}}/template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/PUSH/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0032ReadPushTemplate"></span>

## View Push Template Details

View template details.

**Request**

```
GET /template/v1.0/PUSH/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



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
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "template name",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "content" : {
      "unsubscribePhoneNumber" : "main number",
      "unsubscribeGuide" : "menu > settings",
      "title" : "title",
      "body" : "contents",
      "richMessage" : {
        "buttons" : [ {
          "name" : "button name",
          "submitName" : "send button name",
          "buttonType" : "button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
          "link" : "link upon clicking button",
          "hint" : "button hint"
        } ],
        "media" : {
          "sourceType" : "media location, REMOTE, LOCAL",
          "source" : "address of the media location, URL, LOCAL_RESOURCE",
          "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
          "extension" : "media file extensions, jpg, png",
          "expandable" : true
        },
        "androidMedia" : {
          "sourceType" : "media location, REMOTE, LOCAL",
          "source" : "address of the media location, URL, LOCAL_RESOURCE",
          "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
          "extension" : "media file extensions, jpg, png",
          "expandable" : true
        },
        "iosMedia" : {
          "sourceType" : "media location, REMOTE, LOCAL",
          "source" : "address of the media location, URL, LOCAL_RESOURCE",
          "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
          "extension" : "media file extensions, jpg, png",
          "expandable" : true
        },
        "largeIcon" : {
          "sourceType" : "location of large icon, REMOTE, LOCAL",
          "source" : "address of the media location, URL, LOCAL_RESOURCE"
        },
        "group" : {
          "key" : "group key, a feature to group multiple messages together, supported on Android only",
          "description" : "group description"
        }
      },
      "style" : {
        "useHtmlStyle" : true
      },
      "customKey" : "customValue"
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| template | Object |  |
| template.templateId | String | Template ID issued when registering a template |
| template.templateName | String | Template name |
| template.categoryId | String | Category ID |
| template.messageChannel | String | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | Sender content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array | |
| template.templateLanguage | String | Template type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.content | Object | Push message content |
| template.createdDateTime | String | Created at |
| template.updatedDateTime | String | Modified at |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View Push Template Details

GET {{endpoint}}/template/v1.0/PUSH/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/PUSH/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0033UpdatePushTemplate"></span>

## Modify Push Template

Modify a template.

**Request**

```
PUT /template/v1.0/PUSH/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "main number",
    "unsubscribeGuide" : "menu > settings",
    "title" : "title",
    "body" : "contents",
    "richMessage" : {
      "buttons" : [ {
        "name" : "button name",
        "submitName" : "send button name",
        "buttonType" : "button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "link upon clicking button",
        "hint" : "button hint"
      } ],
      "media" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "location of large icon, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "group key, a feature to group multiple messages together, supported on Android only",
        "description" : "group description"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | Y | Template name |
| messagePurpose | String | N | Sender content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | Template type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| content | Object | Y | Push message content |



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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Modify Push Template

PUT {{endpoint}}/template/v1.0/PUSH/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "main number",
    "unsubscribeGuide" : "menu > settings",
    "title" : "title",
    "body" : "contents",
    "richMessage" : {
      "buttons" : [ {
        "name" : "button name",
        "submitName" : "send button name",
        "buttonType" : "button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "link upon clicking button",
        "hint" : "button hint"
      } ],
      "media" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "location of large icon, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "group key, a feature to group multiple messages together, supported on Android only",
        "description" : "group description"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/PUSH/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "main number",
    "unsubscribeGuide" : "menu > settings",
    "title" : "title",
    "body" : "contents",
    "richMessage" : {
      "buttons" : [ {
        "name" : "button name",
        "submitName" : "send button name",
        "buttonType" : "button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "link upon clicking button",
        "hint" : "button hint"
      } ],
      "media" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "media location, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "media file extensions, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "location of large icon, REMOTE, LOCAL",
        "source" : "address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "group key, a feature to group multiple messages together, supported on Android only",
        "description" : "group description"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}'
```

</details>
<span id="templateV1x0034DeletePushTemplate"></span>

## Delete Push Template

Delete a template.

**Request**

```
DELETE /template/v1.0/PUSH/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| templateId | Path  | String | Y | Template ID |



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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### DeletePush Template

DELETE {{endpoint}}/template/v1.0/PUSH/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/PUSH/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0035ReadTemplateParameters"></span>

## Retrieve Template Parameter

Retrieve the list of parameters included in the template.

**Request**

```
GET /template/v1.0/{messageChannel}/templates/{templateId}/parameters
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messageChannel | Path  | String | Y | Message channel.<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| templateId | Path  | String | Y | Template ID |



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
  "templateParameter" : {
    "validateTimestamp" : "",
    "timestamp" : "",
    "validateFailDomainList" : [ {
      "domain" : "",
      "verifyYn" : "",
      "spfYn" : "",
      "dkimVerifyYn" : "",
      "dmarcYn" : ""
    } ]
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| templateParameter | Object | Template parameter result JSON |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve Template Parameter

GET {{endpoint}}/template/v1.0/{{messageChannel}}/templates/{{templateId}}/parameters
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/${messageChannel}/templates/${templateId}/parameters" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>