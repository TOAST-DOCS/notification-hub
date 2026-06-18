<!-- pre-align:aligned sig=8780bb7cdba0 -->

<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>Template</h1>

**Notification > Notification Hub > API v1.0 User Guide > Template**



<span id="templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesGet"></span>

## List Kakao Templates for an Alim Talk Template

Retrieves a list of Kakao templates for an Alim Talk template.

**Request**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| templateId | Path | String | O | Template ID |
| limit | Query | Number | X | If not set, defaults to 20 (maximum: 1000) |
| offset | Query | Number | X | If not set, defaults to 0 |



**Request Body**

This API does not require a request body.



**Response Body**

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
    "kakaoTemplateName" : "Template name",
    "content" : {
      "templateMessageType" : "BA",
      "templateEmphasizeType" : "NONE",
      "templateContent" : "Your order for #{name} has been completed.",
      "templateAd" : "Add this channel to receive marketing messages and more from this channel via KakaoTalk",
      "templateExtra" : "* Due to the nature of real-time reservations, duplicate bookings may occur, and your reservation may be canceled if check-in is unavailable.\\n* Inquiries: 1234-1234",
      "templateTitle" : "123,450 KRW",
      "templateSubtitle" : "Approval details",
      "templateHeader" : "Your order has been placed.",
      "templateItem" : {
        "list" : [ {
          "title" : "Item title",
          "description" : "Item description"
        } ],
        "summary" : {
          "title" : "Summary title",
          "description" : "Summary description"
        }
      },
      "templateItemHighlight" : {
        "title" : "Highlight title",
        "description" : "Highlight description",
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
        "name" : "Button name",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ],
      "quickReplies" : [ {
        "ordering" : 1,
        "type" : "WL",
        "name" : "Quick reply name",
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
      "content" : "Sample inquiry content",
      "userName" : "Username",
      "createdAt" : "2024-10-29T06:00:01.000+09:00",
      "attachments" : [ {
        "originalFileName" : "Sample filename",
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

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | O | Total count |
| templates | Array | O |  |
| templates[].kakaoTemplateCode | String | O | Kakao template code |
| templates[].kakaoTemplateName | String | O | Template name |
| templates[].content | Object | O |  |
| templates[].content.templateMessageType | String | X | Types of template message (BA: Basic, EX: Extra Information, AD: Ad Included, MI: Mixed Purposes, default: BA) |
| templates[].content.templateEmphasizeType | String | O | Template emphasis type<br>[NONE (no emphasis), TEXT (text emphasis), IMAGE (image emphasis), ITEM_LIST (item list emphasis)] |
| templates[].content.templateContent | String | X | Template body |
| templates[].content.templateAd | String | X | Channel add guide message (fixed value when the template message type is Ad Included or Mixed Purposes) |
| templates[].content.templateExtra | String | X | Template extra information (required when the template message type is Extra Information or Mixed Purposes); placeholder variables not allowed, URLs allowed |
| templates[].content.templateTitle | String | X | Template title (No more than 50 characters, Android: To be abbreviated if it exceeds 2 lines with more than 23 characters, iOS: To be abbreviated if it exceeds 2 lines with more than 27 characters) |
| templates[].content.templateSubtitle | String | X | Auxiliary template phrase (No more than 50 characters, Android: To be abbreviated if it exceeds 18 characters, iOS: To be abbreviated if it exceeds 21 characters) |
| templates[].content.templateHeader | String | X | Template header; variables allowed |
| templates[].content.templateItem | Object | X |  |
| templates[].content.templateItem.list | Array | O |  |
| templates[].content.templateItem.list[].title | String | O | Item title |
| templates[].content.templateItem.list[].description | String | O | Item description |
| templates[].content.templateItem.summary | Object | X |  |
| templates[].content.templateItem.summary.title | String | O | Summary title |
| templates[].content.templateItem.summary.description | String | O | Summary description (only variables, currency units, numbers, commas, and periods are allowed) |
| templates[].content.templateItemHighlight | Object | X |  |
| templates[].content.templateItemHighlight.title | String | O | Item highlight title (up to 30 characters; up to 21 characters if a thumbnail image is present) |
| templates[].content.templateItemHighlight.description | String | O | Item highlight description (up to 19 characters; up to 13 characters if a thumbnail image is present) |
| templates[].content.templateItemHighlight.attachmentId | String | X | Template attachment file ID |
| templates[].content.templateItemHighlight.imageUrl | String | X | Thumbnail image URL |
| templates[].content.templateRepresentLink | Object | X |  |
| templates[].content.templateRepresentLink.linkMo | String | X | Representative link mobile web URL |
| templates[].content.templateRepresentLink.linkPc | String | X | Representative link PC web URL |
| templates[].content.templateRepresentLink.schemeIos | String | X | Representative link iOS app link |
| templates[].content.templateRepresentLink.schemeAndroid | String | X | Representative link Android app link |
| templates[].content.attachmentId | String | X | Template attachment file ID |
| templates[].content.templateImageName | String | X | Template image name |
| templates[].content.templateImageUrl | String | X | Template image URL |
| templates[].content.securityFlag | Boolean | X | Whether the template is secured (default: false) |
| templates[].content.categoryCode | String | X | Template category code (see the List Template Categories API; default: 999999) |
| templates[].content.buttons | Array | X | Template buttons |
| templates[].content.buttons[].ordering | Integer | O | Template button order |
| templates[].content.buttons[].type | String | O | Template button type<br>[WL (Web link), AL (App link), DS (Delivery search), BK (Bot keyword), MD (Message delivery), BC (Bot for Consultation), BT (Bot Transfer), AC (Add channel), BF (Business form), P1 (Image secure transmission plugin), P2 (Personal information use plugin), P3 (One-click payment plugin), TN (Call)] |
| templates[].content.buttons[].name | String | O | Template button name |
| templates[].content.buttons[].linkMo | String | X | Template button mobile web URL |
| templates[].content.buttons[].linkPc | String | X | Template button PC web URL |
| templates[].content.buttons[].schemeIos | String | X | Template button iOS app link |
| templates[].content.buttons[].schemeAndroid | String | X | Template button Android app link |
| templates[].content.buttons[].bizFormId | Integer | X | Template button business form ID (required for BF type) |
| templates[].content.quickReplies | Array | X | Template quick replies |
| templates[].content.quickReplies[].ordering | Integer | O | Template quick reply order |
| templates[].content.quickReplies[].type | String | O | Template quick reply type<br>[WL (Web link), AL (App link), BK (Bot keyword), BC (Bot for Consultation), BT (Bot Transfer), BF (Business form)] |
| templates[].content.quickReplies[].name | String | O | Template quick reply name |
| templates[].content.quickReplies[].linkMo | String | X | Template quick reply mobile web URL |
| templates[].content.quickReplies[].linkPc | String | X | Template quick reply PC web URL |
| templates[].content.quickReplies[].schemeIos | String | X | Template quick reply iOS app link |
| templates[].content.quickReplies[].schemeAndroid | String | X | Template quick reply Android app link |
| templates[].content.quickReplies[].bizFormId | Integer | X | Template quick reply business form ID (required for BF type) |
| templates[].reviewStatus | String | O | REGISTERED: Submitted, REQUESTED: Under review, APPROVED: Approved, REJECTED: Rejected<br>[REGISTERED, REQUESTED, APPROVED, REJECTED] |
| templates[].comments | Array | O | Template inquiry list |
| templates[].comments[].id | Integer | O | Inquiry ID |
| templates[].comments[].content | String | X | Inquiry content |
| templates[].comments[].userName | String | O | Author |
| templates[].comments[].createdAt | String | O | Inquiry creation time |
| templates[].comments[].attachments | Array | O | Inquiry attachments |
| templates[].comments[].attachments[].originalFileName | String | O | Attachment file name |
| templates[].comments[].attachments[].filePath | String | O | Attachment file path |
| templates[].comments[].status | String | O | Inquiry status (REQ: Requested, INQ: Inquiry, APR: Approved, REJ: Rejected, REP: Replied)<br>[REQ, INQ, APR, REJ, REP] |
| templates[].block | Boolean | O | Whether the template is blocked |
| templates[].dormant | Boolean | O | Whether the template is dormant |
| templates[].createdDateTime | String | O | Template creation time |
| templates[].updatedDateTime | String | O | Template last modified time |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List Kakao templates for an Alim Talk template

GET {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/kakao-templates
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/kakao-templates"
```

</details>

<span id="templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesKakaoTemplateCodeInquiriesDoWithFilePost"></span>

<a id="submit-an-alimtalk-template-inquiry-with-file-attachment"></a>

## Submit an AlimTalk Template Inquiry with File Attachment

Submits an inquiry for a Kakao AlimTalk template with a file attachment.

**Request**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates/{kakaoTemplateCode}/inquiries/do-with-file
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| templateId | Path | String | O | Template ID |
| kakaoTemplateCode | Path | String | O | Kakao template code |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->

| Path | Type | Required | Description |
| - | - | - | - |
| file | Array | O | Inquiry file |
| comment | String | O | Inquiry content |



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
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



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Submit an AlimTalk Template Inquiry with File Attachment

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/kakao-templates/{{kakaoTemplateCode}}/inquiries/do-with-file
comment=comment_example
file=@/path/to/file.txt
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/kakao-templates/${kakaoTemplateCode}/inquiries/do-with-file" \
-F "comment=comment_example" \
-F "file=@/path/to/file.txt"
```

</details>

<span id="templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesKakaoTemplateCodeInquiriesPost"></span>

<a id="submit-an-alimtalk-template-inquiry"></a>

## Submit an AlimTalk Template Inquiry

Submits an inquiry for a Kakao AlimTalk template.

**Request**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates/{kakaoTemplateCode}/inquiries
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| templateId | Path | String | O | Template ID |
| kakaoTemplateCode | Path | String | O | Kakao template code |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->


```
{
  "comment" : "Sample inquiry content"
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| comment | String | O | Inquiry content |



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
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



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Submit an AlimTalk Template Inquiry

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/kakao-templates/{{kakaoTemplateCode}}/inquiries
{
  "comment" : "Sample inquiry content"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/kakao-templates/${kakaoTemplateCode}/inquiries" \
-d '{
  "comment" : "Sample inquiry content"
}'
```

</details>

<span id="templateV1x0001CreateSmsTemplate"></span>

<a id="register-sms-template"></a>

## Register an SMS Template

Registers a template.

**Request**

```
POST /template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |



**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


```
{
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "명절 운영시간 공지",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다. 방문해주세요^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | O | Template name |
| categoryId | String | X | Category ID |
| messagePurpose | String | X | Message content type<br>Default: NORMAL<br>[NORMAL (general), AD (advertising), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| sender | Object | O |  |
| sender.senderPhoneNumber | String | O | Sender number |
| content | Object | O |  |
| content.messageType | String | O | Message type (SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| content.title | String | X | Message title |
| content.body | String | O | Message body |
| content.attachmentIds | Array | X | Up to 3 attachment IDs |
| content.imageLayoutId | String | X | Image layout ID |



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| templateId | String | O | Template ID issued upon template registration |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Register an SMS Template

POST {{endpoint}}/template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "명절 운영시간 공지",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다. 방문해주세요^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/SMS/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "명절 운영시간 공지",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다. 방문해주세요^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}'
```

</details>

<span id="templateV1x0002ReadSmsTemplateList"></span>

<a id="list-sms-templates"></a>

## List SMS Templates

Retrieves a list of templates.

**Request**

```
GET /template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateName | Query | String | X | Template name (LIKE search) |
| limit | Query | Number | X | If limit is not set, the default value is 20. (Maximum 1,000) |
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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | O | Total count |
| templates | Array | O |  |
| templates[].templateId | String | O | Template ID issued when registering the template. |
| templates[].templateName | String | O | Template name |
| templates[].categoryId | String | O | Category ID |
| templates[].messageChannel | String | O | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| templates[].messagePurposes | Array | O |  |
| templates[].createdDateTime | String | O | Template creation time |
| templates[].updatedDateTime | String | O | Template modification time |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List SMS Templates

GET {{endpoint}}/template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/SMS/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0003ReadSmsTemplate"></span>

<a id="get-sms-template-details"></a>

## Get SMS Template Details

Retrieves the details of a template.

**Request**

```
GET /template/v1.0/SMS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



**Request body**

This API does not require a request body.



**Response body**

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "템플릿 이름",
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
      "title" : "명절 운영시간 공지",
      "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다. 방문해주세요^^",
      "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
      "imageLayoutId" : "YaX2DA4Weab1"
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | X |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| template | Object | X |  |
| template.templateId | String | O | Template ID issued when the template was registered |
| template.templateName | String | X | Template name |
| template.categoryId | String | X | Category ID |
| template.messageChannel | String | X | Message channel<br>[SMS(SMS), ALIMTALK(Alim Talk), EMAIL(Email), RCS(RCS), PUSH(Push)] |
| template.messagePurpose | String | X | Message content type<br>Default: NORMAL<br>[NORMAL(General), AD(Advertising), AUTH(Authentication)] |
| template.messagePurposes | Array | X |  |
| template.templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT(Plain text), FREEMARKER(FreeMarker template)] |
| template.sender | Object | X |  |
| template.sender.senderPhoneNumber | String | O | Sender number |
| template.content | Object | X |  |
| template.content.messageType | String | O | Message type (SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| template.content.title | String | X | Message title |
| template.content.body | String | O | Message body |
| template.content.attachmentIds | Array | X | Up to 3 attachment file IDs |
| template.content.imageLayoutId | String | X | Image layout ID |
| template.createdDateTime | String | X | Template creation date and time |
| template.updatedDateTime | String | X | Template last modified date and time |



**Request examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Get SMS Template Details

GET {{endpoint}}/template/v1.0/SMS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/SMS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0004UpdateSmsTemplate"></span>

<a id="update-sms-template"></a>

## Modify SMS Template

Modifies a template.

**Request**

```
PUT /template/v1.0/SMS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


```
{
  "templateName" : "Template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday hours notice",
    "body" : "Hello. Your order has arrived today. Please come visit us^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | O | Template name |
| messagePurpose | String | X | Message content type<br>Default: NORMAL<br>[NORMAL (general), AD (advertising), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| sender | Object | X |  |
| sender.senderPhoneNumber | String | O | Sender number |
| content | Object | O |  |
| content.messageType | String | O | Message type (SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| content.title | String | X | Message title |
| content.body | String | O | Message body |
| content.attachmentIds | Array | X | Up to 3 attachment IDs |
| content.imageLayoutId | String | X | Image layout ID |



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
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



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Modify SMS Template

PUT {{endpoint}}/template/v1.0/SMS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "Template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday hours notice",
    "body" : "Hello. Your order has arrived today. Please come visit us^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/SMS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "Template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday hours notice",
    "body" : "Hello. Your order has arrived today. Please come visit us^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}'
```

</details>

<span id="templateV1x0005DeleteSmsTemplate"></span>

<a id="delete-sms-template"></a>

## Delete SMS Template

Deletes a template.

**Request**

```
DELETE /template/v1.0/SMS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0006CreateAlimtalkTemplate"></span>

<a id="register-alimtalk-template"></a>

## Register Alim Talk Template

Registers a template.

**Request**

```
POST /template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | App key |
| X-NHN-Authorization | Header | String | O | Access token |



**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


```
{
  "templateName" : "템플릿 이름",
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
    "templateContent" : "#{이름}님의 주문이 완료되었습니다.",
    "templateAd" : "채널 추가하고 이 채널의 마케팅 메시지 등을 카카오톡으로 받기",
    "templateExtra" : "* 실시간 예약 특성상 중복 예약이 발생할 수 있으며, 입실이 불가할 경우 예약이 취소될 수 있습니다.\\n* 문의전화: 1234-1234",
    "templateTitle" : "123,450원",
    "templateSubtitle" : "승인 내역",
    "templateHeader" : "주문이 체결되었습니다.",
    "templateItem" : {
      "list" : [ {
        "title" : "아이템 타이틀",
        "description" : "아이템 설명"
      } ],
      "summary" : {
        "title" : "요약 타이틀",
        "description" : "요약 설명"
      }
    },
    "templateItemHighlight" : {
      "title" : "하이라이트 타이틀",
      "description" : "하이라이트 설명",
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
      "name" : "버튼 이름",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "바로연결 이름",
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

<!--Describes the fields of the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | O | Template name |
| categoryId | String | X | Category ID |
| messagePurpose | String | X | Message content type<br>Default: NORMAL<br>[NORMAL (General), AD (Advertising), AUTH (Authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (Plain text), FREEMARKER (FreeMarker template)] |
| sender | Object | X |  |
| sender.senderKey | String | X | Sender profile sender key |
| sender.senderProfileType | String | X | Sender profile type<br>[GROUP, NORMAL] |
| content | Object | O |  |
| content.templateMessageType | String | X | Template message type (BA: Basic, EX: Extra information, AD: Ad included, MI: Mixed, default: BA) |
| content.templateEmphasizeType | String | O | Template emphasis type<br>[NONE (No emphasis), TEXT (Text emphasis), IMAGE (Image emphasis), ITEM_LIST (Item list emphasis)] |
| content.templateContent | String | X | Template body |
| content.templateAd | String | X | Channel add guide message (fixed value when template message type is Ad Included or Mixed) |
| content.templateExtra | String | X | Template extra information (required when template message type is [Extra information/Mixed]); substitution variables not allowed, URLs allowed |
| content.templateTitle | String | X | Template title (No more than 50 characters, Android: To be abbreviated if it exceeds 2 lines with more than 23 characters, iOS: To be abbreviated if it exceeds 2 lines with more than 27 characters) |
| content.templateSubtitle | String | X | Template subtitle (No more than 50 characters, Android: abbreviated if more than 18 characters, iOS: abbreviated if more than 21 characters) |
| content.templateHeader | String | X | Template header; variables can be entered |
| content.templateItem | Object | X |  |
| content.templateItem.list | Array | O |  |
| content.templateItem.list[].title | String | O | Item title |
| content.templateItem.list[].description | String | O | Item description |
| content.templateItem.summary | Object | X |  |
| content.templateItem.summary.title | String | O | Summary title |
| content.templateItem.summary.description | String | O | Summary description (only variables, currency units, numbers, commas, and periods are allowed) |
| content.templateItemHighlight | Object | X |  |
| content.templateItemHighlight.title | String | O | Item highlight title (up to 30 characters; up to 21 characters if a thumbnail image is present) |
| content.templateItemHighlight.description | String | O | Item highlight description (up to 19 characters; up to 13 characters if a thumbnail image is present) |
| content.templateItemHighlight.attachmentId | String | X | Template attachment file ID |
| content.templateItemHighlight.imageUrl | String | X | Thumbnail image URL |
| content.templateRepresentLink | Object | X |  |
| content.templateRepresentLink.linkMo | String | X | Representative link mobile web URL |
| content.templateRepresentLink.linkPc | String | X | Representative link PC web URL |
| content.templateRepresentLink.schemeIos | String | X | Representative link iOS app link |
| content.templateRepresentLink.schemeAndroid | String | X | Representative link Android app link |
| content.attachmentId | String | X | Template attachment file ID |
| content.templateImageName | String | X | Template image name |
| content.templateImageUrl | String | X | Template image URL |
| content.securityFlag | Boolean | X | Whether the template is security-enabled (default: false) |
| content.categoryCode | String | X | Template category code (see the Get Template Category API; default: 999999) |
| content.buttons | Array | X | Template buttons |
| content.buttons[].ordering | Integer | O | Template button order |
| content.buttons[].type | String | O | Template button type<br>[WL (Web link), AL (App link), DS (Delivery search), BK (Bot keyword), MD (Message delivery), BC (Bot for Consultation), BT (Bot Transfer), AC (Add channel), BF (Business form), P1 (Image secure transmission plugin), P2 (Personal information use plugin), P3 (One-click payment plugin), TN (Phone call)] |
| content.buttons[].name | String | O | Template button name |
| content.buttons[].linkMo | String | X | Template button mobile web URL |
| content.buttons[].linkPc | String | X | Template button PC web URL |
| content.buttons[].schemeIos | String | X | Template button iOS app link |
| content.buttons[].schemeAndroid | String | X | Template button Android app link |
| content.buttons[].bizFormId | Integer | X | Template button business form ID (required for BF type) |
| content.quickReplies | Array | X | Template quick replies |
| content.quickReplies[].ordering | Integer | O | Template quick reply order |
| content.quickReplies[].type | String | O | Template quick reply type<br>[WL (Web link), AL (App link), BK (Bot keyword), BC (Bot for Consultation), BT (Bot Transfer), BF (Business form)] |
| content.quickReplies[].name | String | O | Template quick reply name |
| content.quickReplies[].linkMo | String | X | Template quick reply mobile web URL |
| content.quickReplies[].linkPc | String | X | Template quick reply PC web URL |
| content.quickReplies[].schemeIos | String | X | Template quick reply iOS app link |
| content.quickReplies[].schemeAndroid | String | X | Template quick reply Android app link |
| content.quickReplies[].bizFormId | Integer | X | Template quick reply business form ID (required for BF type) |
| additionalProperty | Object | O |  |
| additionalProperty.templateCode | String | O | Template code (letters, numbers, -, _) |
| additionalProperty.kakaoTemplateCode | String | X | KakaoTalk template code |



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields of the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| templateId | String | O | Template ID issued when the template is registered |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Register Alim Talk Template

POST {{endpoint}}/template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "템플릿 이름",
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
    "templateContent" : "#{이름}님의 주문이 완료되었습니다.",
    "templateAd" : "채널 추가하고 이 채널의 마케팅 메시지 등을 카카오톡으로 받기",
    "templateExtra" : "* 실시간 예약 특성상 중복 예약이 발생할 수 있으며, 입실이 불가할 경우 예약이 취소될 수 있습니다.\\n* 문의전화: 1234-1234",
    "templateTitle" : "123,450원",
    "templateSubtitle" : "승인 내역",
    "templateHeader" : "주문이 체결되었습니다.",
    "templateItem" : {
      "list" : [ {
        "title" : "아이템 타이틀",
        "description" : "아이템 설명"
      } ],
      "summary" : {
        "title" : "요약 타이틀",
        "description" : "요약 설명"
      }
    },
    "templateItemHighlight" : {
      "title" : "하이라이트 타이틀",
      "description" : "하이라이트 설명",
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
      "name" : "버튼 이름",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "바로연결 이름",
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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "템플릿 이름",
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
    "templateContent" : "#{이름}님의 주문이 완료되었습니다.",
    "templateAd" : "채널 추가하고 이 채널의 마케팅 메시지 등을 카카오톡으로 받기",
    "templateExtra" : "* 실시간 예약 특성상 중복 예약이 발생할 수 있으며, 입실이 불가할 경우 예약이 취소될 수 있습니다.\\n* 문의전화: 1234-1234",
    "templateTitle" : "123,450원",
    "templateSubtitle" : "승인 내역",
    "templateHeader" : "주문이 체결되었습니다.",
    "templateItem" : {
      "list" : [ {
        "title" : "아이템 타이틀",
        "description" : "아이템 설명"
      } ],
      "summary" : {
        "title" : "요약 타이틀",
        "description" : "요약 설명"
      }
    },
    "templateItemHighlight" : {
      "title" : "하이라이트 타이틀",
      "description" : "하이라이트 설명",
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
      "name" : "버튼 이름",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "바로연결 이름",
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

<a id="list-alimtalk-templates"></a>

## List AlimTalk Templates

Retrieves a list of templates.

**Request**

```
GET /template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateName | Query | String | X | Template name (LIKE search) |
| senderKey | Query | String | X | Sender key |
| templateStatus | Query | String | X | Template status |
| limit | Query | Number | X | If limit is not set, the default value is 20. (Maximum 1,000) |
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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | O | Total count |
| templates | Array | O |  |
| templates[].templateId | String | O | Template ID issued when registering the template. |
| templates[].templateName | String | O | Template name |
| templates[].categoryId | String | O | Category ID |
| templates[].messageChannel | String | O | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| templates[].messagePurposes | Array | O |  |
| templates[].createdDateTime | String | O | Template creation time |
| templates[].updatedDateTime | String | O | Template modification time |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List AlimTalk Templates

GET {{endpoint}}/template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0008ReadAlimtalkSenderTemplates"></span>

<a id="list-templates-by-alimtalk-sender"></a>

## List Templates by AlimTalk Sender

Retrieves a list of templates associated with a sender (including templates for groups that the sender belongs to).

**Request**

```
GET /template/v1.0/ALIMTALK/senders/{senderKey}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| senderKey | Path | String | O | Sender key |
| templateName | Query | String | X | Template name (LIKE search) |
| templateStatus | Query | String | X | Template status |
| limit | Query | Number | X | If limit is not set, the default value is 20. (Maximum 1,000) |
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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | O | Total count |
| templates | Array | O |  |
| templates[].templateId | String | O | Template ID issued when registering the template. |
| templates[].templateName | String | O | Template name |
| templates[].categoryId | String | O | Category ID |
| templates[].messageChannel | String | O | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| templates[].messagePurposes | Array | O |  |
| templates[].createdDateTime | String | O | Template creation time |
| templates[].updatedDateTime | String | O | Template modification time |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List Templates by AlimTalk Sender

GET {{endpoint}}/template/v1.0/ALIMTALK/senders/{{senderKey}}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/senders/${senderKey}/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0009ReadAlimtalkTemplate"></span>

<a id="get-alimtalk-template-details"></a>

## Get Alim Talk Template Details

Retrieves the details of a template.

**Request**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | App key |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



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
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "템플릿 이름",
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
      "kakaoTemplateCode" : "templateCode",
      "templateCode" : "templateCode",
      "comments" : [ {
        "id" : 1,
        "content" : "문의 내용 예시",
        "userName" : "사용자 이름",
        "createdAt" : "2024-10-29T06:00:01.000+09:00",
        "attachments" : [ {
          "originalFileName" : "파일명 예시",
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
      "templateContent" : "#{이름}님의 주문이 완료되었습니다.",
      "templateAd" : "채널 추가하고 이 채널의 마케팅 메시지 등을 카카오톡으로 받기",
      "templateExtra" : "* 실시간 예약 특성상 중복 예약이 발생할 수 있으며, 입실이 불가할 경우 예약이 취소될 수 있습니다.\\n* 문의전화: 1234-1234",
      "templateTitle" : "123,450원",
      "templateSubtitle" : "승인 내역",
      "templateHeader" : "주문이 체결되었습니다.",
      "templateItem" : {
        "list" : [ {
          "title" : "아이템 타이틀",
          "description" : "아이템 설명"
        } ],
        "summary" : {
          "title" : "요약 타이틀",
          "description" : "요약 설명"
        }
      },
      "templateItemHighlight" : {
        "title" : "하이라이트 타이틀",
        "description" : "하이라이트 설명",
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
        "name" : "버튼 이름",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ],
      "quickReplies" : [ {
        "ordering" : 1,
        "type" : "WL",
        "name" : "바로연결 이름",
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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| template | Object | O |  |
| template.templateId | String | O | Template ID issued when the template was registered |
| template.templateName | String | O | Template name |
| template.categoryId | String | O | Category ID |
| template.messageChannel | String | O | Message channel<br>[SMS(SMS), ALIMTALK(Alim Talk), EMAIL(Email), RCS(RCS), PUSH(Push)] |
| template.messagePurpose | String | O | Message content type<br>Default: NORMAL<br>[NORMAL(General), AD(Advertising), AUTH(Authentication)] |
| template.messagePurposes | Array | O |  |
| template.templateLanguage | String | O | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT(Plain text), FREEMARKER(FreeMarker template)] |
| template.sender | Object | O |  |
| template.sender.senderKey | String | O | Sender profile sender key |
| template.sender.senderProfileId | String | O | KakaoTalk channel name |
| template.sender.senderProfileType | String | O | Sender profile type<br>[GROUP, NORMAL] |
| template.additionalProperty | Object | O |  |
| template.additionalProperty.kakaoTemplateCode | String | O | Kakao template code |
| template.additionalProperty.templateCode | String | O | Template code (letters, numbers, -, _) |
| template.additionalProperty.comments | Array | O | Template inquiry list |
| template.additionalProperty.comments[].id | Integer | O | Inquiry ID |
| template.additionalProperty.comments[].content | String | X | Inquiry content |
| template.additionalProperty.comments[].userName | String | O | Author |
| template.additionalProperty.comments[].createdAt | String | O | Inquiry creation time |
| template.additionalProperty.comments[].attachments | Array | O | Inquiry attachments |
| template.additionalProperty.comments[].attachments[].originalFileName | String | O | Attachment file name |
| template.additionalProperty.comments[].attachments[].filePath | String | O | Attachment file path |
| template.additionalProperty.comments[].status | String | O | Inquiry status (REQ: Request, INQ: Inquiry, APR: Approved, REJ: Rejected, REP: Reply)<br>[REQ, INQ, APR, REJ, REP] |
| template.additionalProperty.status | String | X | REGISTERED: Requested, REQUESTED: Under review, APPROVED: Approved, REJECTED: Rejected<br>[REGISTERED, REQUESTED, APPROVED, REJECTED] |
| template.additionalProperty.block | Boolean | O | Whether the template is blocked<br>Default: false |
| template.additionalProperty.dormant | Boolean | O | Whether the template is dormant<br>Default: false |
| template.content | Object | O |  |
| template.content.templateMessageType | String | X | Template message type (BA: Basic, EX: Extra information, AD: Channel add, MI: Mixed, default: BA) |
| template.content.templateEmphasizeType | String | O | Template emphasis type<br>[NONE(No emphasis), TEXT(Text emphasis), IMAGE(Image emphasis), ITEM_LIST(Item list emphasis)] |
| template.content.templateContent | String | X | Template body |
| template.content.templateAd | String | X | Channel add guide message (fixed value when template message type is Channel add or Mixed) |
| template.content.templateExtra | String | X | Template extra information (required when template message type is Extra information or Mixed); placeholders cannot be used; URLs can be included |
| template.content.templateTitle | String | X | Template title (No more than 50 characters, Android: To be abbreviated if it exceeds 2 lines with more than 23 characters, iOS: To be abbreviated if it exceeds 2 lines with more than 27 characters) |
| template.content.templateSubtitle | String | X | Template subtitle (No more than 50 characters, Android: To be abbreviated if it exceeds 18 characters, iOS: To be abbreviated if it exceeds 21 characters) |
| template.content.templateHeader | String | X | Template header; variables can be entered |
| template.content.templateItem | Object | X |  |
| template.content.templateItem.list | Array | O |  |
| template.content.templateItem.list[].title | String | O | Item title |
| template.content.templateItem.list[].description | String | O | Item description |
| template.content.templateItem.summary | Object | X |  |
| template.content.templateItem.summary.title | String | O | Summary title |
| template.content.templateItem.summary.description | String | O | Summary description (only variables, currency units, numbers, commas, and periods can be used) |
| template.content.templateItemHighlight | Object | X |  |
| template.content.templateItemHighlight.title | String | O | Item highlight title (No more than 30 characters; 21 characters if a thumbnail image is present) |
| template.content.templateItemHighlight.description | String | O | Item highlight description (No more than 19 characters; 13 characters if a thumbnail image is present) |
| template.content.templateItemHighlight.attachmentId | String | X | Template attachment file ID |
| template.content.templateItemHighlight.imageUrl | String | X | Thumbnail image URL |
| template.content.templateRepresentLink | Object | X |  |
| template.content.templateRepresentLink.linkMo | String | X | Representative link mobile web URL |
| template.content.templateRepresentLink.linkPc | String | X | Representative link PC web URL |
| template.content.templateRepresentLink.schemeIos | String | X | Representative link iOS app link |
| template.content.templateRepresentLink.schemeAndroid | String | X | Representative link Android app link |
| template.content.attachmentId | String | X | Template attachment file ID |
| template.content.templateImageName | String | X | Template image name |
| template.content.templateImageUrl | String | X | Template image URL |
| template.content.securityFlag | Boolean | X | Whether the template has security enabled (default: false) |
| template.content.categoryCode | String | X | Template category code (see the Get Template Categories API; default: 999999) |
| template.content.buttons | Array | X | Template buttons |
| template.content.buttons[].ordering | Integer | O | Template button order |
| template.content.buttons[].type | String | O | Template button type<br>[WL(Web link), AL(App link), DS(Delivery search), BK(Bot keyword), MD(Message delivery), BC(Bot for Consultation), BT(Bot Transfer), AC(Add channel), BF(Business form), P1(Image secure transmission plugin), P2(Personal information use plugin), P3(One-click payment plugin), TN(Call)] |
| template.content.buttons[].name | String | O | Template button name |
| template.content.buttons[].linkMo | String | X | Template button mobile web URL |
| template.content.buttons[].linkPc | String | X | Template button PC web URL |
| template.content.buttons[].schemeIos | String | X | Template button iOS app link |
| template.content.buttons[].schemeAndroid | String | X | Template button Android app link |
| template.content.buttons[].bizFormId | Integer | X | Template button business form ID (required for BF type) |
| template.content.quickReplies | Array | X | Template quick replies |
| template.content.quickReplies[].ordering | Integer | O | Template quick reply order |
| template.content.quickReplies[].type | String | O | Template quick reply type<br>[WL(Web link), AL(App link), BK(Bot keyword), BC(Bot for Consultation), BT(Bot Transfer), BF(Business form)] |
| template.content.quickReplies[].name | String | O | Template quick reply name |
| template.content.quickReplies[].linkMo | String | X | Template quick reply mobile web URL |
| template.content.quickReplies[].linkPc | String | X | Template quick reply PC web URL |
| template.content.quickReplies[].schemeIos | String | X | Template quick reply iOS app link |
| template.content.quickReplies[].schemeAndroid | String | X | Template quick reply Android app link |
| template.content.quickReplies[].bizFormId | Integer | X | Template quick reply business form ID (required for BF type) |
| template.createdDateTime | String | O | Template creation time |
| template.updatedDateTime | String | O | Template last modified time |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Get Alim Talk Template Details

GET {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0010UpdateAlimtalkTemplate"></span>

<a id="update-alimtalk-template"></a>

## Update AlimTalk Template

Updates a template.

**Request**

```
PUT /template/v1.0/ALIMTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->


```
{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "Your order #{name} has been completed.",
    "templateAd" : "Add the channel to receive marketing messages and more from this channel on KakaoTalk",
    "templateExtra" : "* Due to the nature of real-time reservations, duplicate reservations may occur and reservations may be cancelled if check-in is unavailable.\\n* Inquiry: 1234-1234",
    "templateTitle" : "123,450 KRW",
    "templateSubtitle" : "Approval details",
    "templateHeader" : "Your order has been placed.",
    "templateItem" : {
      "list" : [ {
        "title" : "Item title",
        "description" : "Item description"
      } ],
      "summary" : {
        "title" : "Summary title",
        "description" : "Summary description"
      }
    },
    "templateItemHighlight" : {
      "title" : "Highlight title",
      "description" : "Highlight description",
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
      "name" : "Button name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "Quick reply name",
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

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | O | Template name |
| messagePurpose | String | O | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| content | Object | O |  |
| content.templateMessageType | String | X | Template message type (BA: basic, EX: additional info, AD: channel add, MI: mixed, default: BA) |
| content.templateEmphasizeType | String | O | Template emphasis type<br>[NONE (no emphasis), TEXT (text emphasis), IMAGE (image emphasis), ITEM_LIST (item list emphasis)] |
| content.templateContent | String | X | Template body |
| content.templateAd | String | X | Channel add guide message (fixed value when template message type is channel add or mixed) |
| content.templateExtra | String | X | Template additional information (required when template message type is additional info or mixed). Substitution variables cannot be used. URLs can be included. |
| content.templateTitle | String | X | Template title (up to 50 characters; Android: 2 lines, truncated at 23+ characters; iOS: 2 lines, truncated at 27+ characters) |
| content.templateSubtitle | String | X | Template subtitle (up to 50 characters; Android: truncated at 18+ characters; iOS: truncated at 21+ characters) |
| content.templateHeader | String | X | Template header. Variables can be entered. |
| content.templateItem | Object | X |  |
| content.templateItem.list | Array | O |  |
| content.templateItem.list[].title | String | O | Item title |
| content.templateItem.list[].description | String | O | Item description |
| content.templateItem.summary | Object | X |  |
| content.templateItem.summary.title | String | O | Summary title |
| content.templateItem.summary.description | String | O | Summary description (only variables, currency units, numbers, commas, and periods are allowed) |
| content.templateItemHighlight | Object | X |  |
| content.templateItemHighlight.title | String | O | Item highlight title (up to 30 characters; 21 characters when a thumbnail image is present) |
| content.templateItemHighlight.description | String | O | Item highlight description (up to 19 characters; 13 characters when a thumbnail image is present) |
| content.templateItemHighlight.attachmentId | String | X | Template attachment file ID |
| content.templateItemHighlight.imageUrl | String | X | Thumbnail image URL |
| content.templateRepresentLink | Object | X |  |
| content.templateRepresentLink.linkMo | String | X | Representative link - mobile web URL |
| content.templateRepresentLink.linkPc | String | X | Representative link - PC web URL |
| content.templateRepresentLink.schemeIos | String | X | Representative link - iOS app URL |
| content.templateRepresentLink.schemeAndroid | String | X | Representative link - Android app URL |
| content.attachmentId | String | X | Template attachment file ID |
| content.templateImageName | String | X | Template image name |
| content.templateImageUrl | String | X | Template image URL |
| content.securityFlag | Boolean | X | Whether the template has security enabled (default: false) |
| content.categoryCode | String | X | Template category code (see the List AlimTalk Template Categories API, default: 999999) |
| content.buttons | Array | X | Template buttons |
| content.buttons[].ordering | Integer | O | Template button order |
| content.buttons[].type | String | O | Template button type<br>[WL (web link), AL (app link), DS (delivery tracking), BK (bot keyword), MD (message forwarding), BC (consult chat switch), BT (bot switch), AC (channel add), BF (business form), P1 (image security transfer plugin), P2 (personal information usage plugin), P3 (one-click payment plugin), TN (call)] |
| content.buttons[].name | String | O | Template button name |
| content.buttons[].linkMo | String | X | Template button mobile web URL |
| content.buttons[].linkPc | String | X | Template button PC web URL |
| content.buttons[].schemeIos | String | X | Template button iOS app URL |
| content.buttons[].schemeAndroid | String | X | Template button Android app URL |
| content.buttons[].bizFormId | Integer | X | Template button business form ID (required when type is BF) |
| content.quickReplies | Array | X | Quick replies |
| content.quickReplies[].ordering | Integer | O | Quick reply order |
| content.quickReplies[].type | String | O | Quick reply type<br>[WL (web link), AL (app link), BK (bot keyword), BC (consult chat switch), BT (bot switch), BF (business form)] |
| content.quickReplies[].name | String | O | Quick reply name |
| content.quickReplies[].linkMo | String | X | Quick reply mobile web URL |
| content.quickReplies[].linkPc | String | X | Quick reply PC web URL |
| content.quickReplies[].schemeIos | String | X | Quick reply iOS app URL |
| content.quickReplies[].schemeAndroid | String | X | Quick reply Android app URL |
| content.quickReplies[].bizFormId | Integer | X | Quick reply business form ID (required when type is BF) |
| additionalProperty | Object | O |  |
| additionalProperty.kakaoTemplateCode | String | O | Kakao template code (letters, numbers, -, _) |



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
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



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Update AlimTalk Template

PUT {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "Your order #{name} has been completed.",
    "templateAd" : "Add the channel to receive marketing messages and more from this channel on KakaoTalk",
    "templateExtra" : "* Due to the nature of real-time reservations, duplicate reservations may occur and reservations may be cancelled if check-in is unavailable.\\n* Inquiry: 1234-1234",
    "templateTitle" : "123,450 KRW",
    "templateSubtitle" : "Approval details",
    "templateHeader" : "Your order has been placed.",
    "templateItem" : {
      "list" : [ {
        "title" : "Item title",
        "description" : "Item description"
      } ],
      "summary" : {
        "title" : "Summary title",
        "description" : "Summary description"
      }
    },
    "templateItemHighlight" : {
      "title" : "Highlight title",
      "description" : "Highlight description",
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
      "name" : "Button name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "Quick reply name",
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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "Your order #{name} has been completed.",
    "templateAd" : "Add the channel to receive marketing messages and more from this channel on KakaoTalk",
    "templateExtra" : "* Due to the nature of real-time reservations, duplicate reservations may occur and reservations may be cancelled if check-in is unavailable.\\n* Inquiry: 1234-1234",
    "templateTitle" : "123,450 KRW",
    "templateSubtitle" : "Approval details",
    "templateHeader" : "Your order has been placed.",
    "templateItem" : {
      "list" : [ {
        "title" : "Item title",
        "description" : "Item description"
      } ],
      "summary" : {
        "title" : "Summary title",
        "description" : "Summary description"
      }
    },
    "templateItemHighlight" : {
      "title" : "Highlight title",
      "description" : "Highlight description",
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
      "name" : "Button name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "Quick reply name",
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

<a id="delete-alimtalk-template"></a>

## Delete AlimTalk Template

Deletes a template.

**Request**

```
DELETE /template/v1.0/ALIMTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0012InquireAlimtalkTemplate"></span>

<a id="submit-an-alimtalk-template-inquiry---deprecated"></a>

## Submit an AlimTalk Template Inquiry - Deprecated

!!! danger This API is no longer supported.
* See [Submit an AlimTalk Template Inquiry](#templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesKakaoTemplateCodeInquiriesPost).

Submits an inquiry for a Kakao AlimTalk template.


**Request**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/inquiries
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->


```
{
  "comment" : "Sample inquiry content"
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| comment | String | O | Inquiry content |



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->




**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Submit an AlimTalk Template Inquiry - Deprecated

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/inquiries
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "comment" : "Sample inquiry content"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/inquiries" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "comment" : "Sample inquiry content"
}'
```

</details>

<span id="templateV1x0013InquireAlimtalkTemplateWithFile"></span>

<a id="submit-an-alimtalk-template-inquiry-with-file-attachment---deprecated"></a>

## Submit an AlimTalk Template Inquiry with File Attachment - Deprecated

!!! danger This API is no longer supported.
* See [Submit an AlimTalk Template Inquiry](#templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesKakaoTemplateCodeInquiriesPost).

Submits an inquiry for a Kakao AlimTalk template with a file attachment.


**Request**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/inquiries/do-with-file
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->

| Path | Type | Required | Description |
| - | - | - | - |
| file | Array | O | Inquiry file |
| comment | String | O | Inquiry content |



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->




**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Submit an AlimTalk Template Inquiry with File Attachment - Deprecated

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/inquiries/do-with-file
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
comment=comment_example
file=@/path/to/file.txt
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/inquiries/do-with-file" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-F "comment=comment_example" \
-F "file=@/path/to/file.txt"
```

</details>

<span id="templateV1x0014ReadAlimtalkTemplateModifications"></span>

<a id="list-alimtalk-template-updates"></a>

## List AlimTalk Template Updates

Retrieves a list of AlimTalk template updates.

**Request**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}/modifications
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |
| limit | Query | Number | X | If limit is not set, the default value is 50. (Maximum 1,000) |
| offset | Query | Number | X | If offset is not set, the default value is 0. |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->

This API does not require a request body.



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->




**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List AlimTalk Template Updates

GET {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/modifications
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/modifications" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0015ReadAlimtalkTemplateCategories"></span>

<a id="list-alimtalk-template-categories"></a>

## List AlimTalk Template Categories

Retrieves a list of AlimTalk template categories.

**Request**

```
GET /template/v1.0/ALIMTALK/template-categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |



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
  "categories" : [ {
    "name" : "Purchase",
    "subCategories" : [ {
      "code" : "002001",
      "name" : "Purchase completed",
      "groupName" : "Purchase",
      "inclusion" : "Targets are order completed and purchase completed templates.",
      "exclusion" : "Templates related to schedules containing reservation or reservation numbers are excluded from purchase completed and classified as reservation."
    } ]
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
| categories | Array | O |  |
| categories[].name | String | O | Main category name |
| categories[].subCategories | Array | X | Subcategories |
| categories[].subCategories[].code | String | O | Category code |
| categories[].subCategories[].name | String | O | Subcategory name |
| categories[].subCategories[].groupName | String | O | Main category name |
| categories[].subCategories[].inclusion | String | O | Inclusion description |
| categories[].subCategories[].exclusion | String | O | Exclusion description |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List AlimTalk Template Categories

GET {{endpoint}}/template/v1.0/ALIMTALK/template-categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/template-categories" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0021CreateEmailTemplate"></span>

<a id="register-email-template"></a>

## Register Email Template

Registers a template.

**Request**

```
POST /template/v1.0/EMAIL/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |



**Request Body**

```
{
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] 모니터링 알림",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | O | Template name |
| categoryId | String | X | Category ID |
| messagePurpose | String | X | Message content type<br>Default: NORMAL<br>[NORMAL (general), AD (advertising), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| sender | Object | O |  |
| sender.senderMailAddress | String | O | Sender email address |
| content | Object | O |  |
| content.title | String | X | Template email subject |
| content.body | String | X | Template email body |
| content.attachmentIds | Array | X | Template attachment file IDs |



**Response Body**

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

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| templateId | String | O | Template ID issued when the template is registered |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Register Email Template

POST {{endpoint}}/template/v1.0/EMAIL/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] 모니터링 알림",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/EMAIL/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] 모니터링 알림",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>

<span id="templateV1x0022ReadEmailTemplate"></span>

<a id="get-email-template-details"></a>

## Get Email Template Details

Retrieves the details of a template.

**Request**

```
GET /template/v1.0/EMAIL/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



**Request Body**

This API does not require a request body.



**Response Body**

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "템플릿 이름",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "sender" : {
      "senderMailAddress" : "abcde@nhn.com"
    },
    "content" : {
      "title" : "[NHN Cloud Email][##env##] 모니터링 알림",
      "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다.",
      "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | X |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| template | Object | X |  |
| template.templateId | String | O | Template ID issued when the template was registered |
| template.templateName | String | X | Template name |
| template.categoryId | String | X | Category ID |
| template.messageChannel | String | X | Message channel<br>[SMS(SMS), ALIMTALK(Alim Talk), EMAIL(Email), RCS(RCS), PUSH(Push)] |
| template.messagePurpose | String | X | Message content type<br>Default: NORMAL<br>[NORMAL(General), AD(Advertising), AUTH(Authentication)] |
| template.messagePurposes | Array | X |  |
| template.templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT(Plain text), FREEMARKER(FreeMarker template)] |
| template.sender | Object | X |  |
| template.sender.senderMailAddress | String | O | Sender email address |
| template.content | Object | X |  |
| template.content.title | String | X | Template email subject |
| template.content.body | String | X | Template email body |
| template.content.attachmentIds | Array | X | Template attachment file IDs |
| template.createdDateTime | String | X | Template creation date and time |
| template.updatedDateTime | String | X | Template last modified date and time |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Get Email Template Details

GET {{endpoint}}/template/v1.0/EMAIL/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/EMAIL/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0022ReadEmailTemplateList"></span>

<a id="list-email-templates"></a>

## List Email Templates

Retrieves a list of templates.

**Request**

```
GET /template/v1.0/EMAIL/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateName | Query | String | X | Template name (LIKE search) |
| limit | Query | Number | X | If limit is not set, the default value is 20. (Maximum 1,000) |
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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | O | Total count |
| templates | Array | O |  |
| templates[].templateId | String | O | Template ID issued when registering the template. |
| templates[].templateName | String | O | Template name |
| templates[].categoryId | String | O | Category ID |
| templates[].messageChannel | String | O | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| templates[].messagePurposes | Array | O |  |
| templates[].createdDateTime | String | O | Template creation time |
| templates[].updatedDateTime | String | O | Template modification time |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List Email Templates

GET {{endpoint}}/template/v1.0/EMAIL/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/EMAIL/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0023UpdateEmailTemplate"></span>

<a id="update-email-template"></a>

## Modify an Email Template

Modifies a template.

**Request**

```
PUT /template/v1.0/EMAIL/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


```
{
  "templateName" : "Template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] Monitoring notification",
    "body" : "Hello. Your ordered product has arrived today.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | O | Template name |
| messagePurpose | String | X | Message content type<br>Default: NORMAL<br>[NORMAL (general), AD (advertising), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| sender | Object | O |  |
| sender.senderMailAddress | String | O | Sender email address |
| content | Object | O |  |
| content.title | String | X | Template email subject |
| content.body | String | X | Template email body |
| content.attachmentIds | Array | X | Template attachment file IDs |



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
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



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Modify an Email Template

PUT {{endpoint}}/template/v1.0/EMAIL/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "Template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] Monitoring notification",
    "body" : "Hello. Your ordered product has arrived today.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/EMAIL/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "Template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] Monitoring notification",
    "body" : "Hello. Your ordered product has arrived today.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>

<span id="templateV1x0024DeleteEmailTemplate"></span>

<a id="delete-email-template"></a>

## Delete Email Template

Deletes a template.

**Request**

```
DELETE /template/v1.0/EMAIL/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0025CreateRcsTemplate"></span>

<a id="register-rcs-template"></a>

## Register RCS Template

Registers a template.

**Request**

```
POST /template/v1.0/RCS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | App key |
| X-NHN-Authorization | Header | String | O | Access token |



**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


```
{
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "명절 운영시간 공지",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다. 방문해주세요^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "제목",
      "description" : "본문",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "메인 타이틀",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "제목 1",
      "title2" : "제목 2",
      "title3" : "제목 3",
      "description1" : "본문 1",
      "description2" : "본문 2",
      "description3" : "본문 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "일정 등록하기",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "일정 제목",
                "description" : "일정 설명"
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
          "displayText" : "일정 등록하기",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "일정 제목",
              "description" : "일정 설명"
            }
          }
        }
      }
    } ]
  }
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | O | Template name |
| categoryId | String | X | Category ID |
| messagePurpose | String | X | Message content type<br>Default: NORMAL<br>[NORMAL (general), AD (advertising), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| sender | Object | O |  |
| sender.brandId | String | O | Brand ID |
| sender.chatbotId | String | O | Chat room (chatbot) ID |
| content | Object | O |  |
| content.messageType | String | X | RCS message type<br>[SMS (short message), LMS (long message), MMS (multimedia message), RBC_TEMPLATE (RCS Biz Center template)] |
| content.title | String | X | (Deprecated, use content.cards[].title) Message title |
| content.body | String | X | (Deprecated, use content.cards[].description) Message body |
| content.smsType | String | X | SMS type<br>[STANDALONE (standalone), UNIFIED_STANDALONE (unified standalone)] |
| content.lmsType | String | X | LMS type<br>[STANDALONE (standalone), FORMAT_BASIC (basic format), FORMAT_TITLE_HIGHLIGHT (title highlight format), FORMAT_PARAGRAPH (paragraph format), UNIFIED_STANDALONE (unified standalone)] |
| content.mmsType | String | X | MMS type (required when sending MMS)<br>[HORIZONTAL (horizontal), VERTICAL (vertical), CAROUSEL_MEDIUM (carousel medium), CAROUSEL_SMALL (carousel small), UNIFIED_HORIZONTAL (unified horizontal), UNIFIED_VERTICAL (unified vertical)] |
| content.messagebaseId | String | X | RCS Biz Center template ID |
| content.unsubscribePhoneNumber | String | X | Opt-out phone number (required when sending advertising messages) |
| content.cards | Array | X | RCS cards |
| content.cards[].title | String | X | Title |
| content.cards[].description | String | X | Body |
| content.cards[].attachmentId | String | X | Attachment file ID<br>※ If a GIF image is attached to a unified MMS card, it cannot be received on iOS devices. |
| content.cards[].mTitle | String | X | Main title |
| content.cards[].mTitleMedia | String | X | Main title logo file ID |
| content.cards[].title1 | String | X | Title 1 |
| content.cards[].title2 | String | X | Title 2 |
| content.cards[].title3 | String | X | Title 3 |
| content.cards[].description1 | String | X | Body 1 |
| content.cards[].description2 | String | X | Body 2 |
| content.cards[].description3 | String | X | Body 3 |
| content.cards[].buttons | Array | X | RCS button list |
| content.cards[].buttons[].buttonType | String | X | COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make a call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share current location), URL (link to URL), CALENDAR (add event)<br>※ If a CLIPBOARD (copy) button is used with a unified message type, it cannot be received on iOS devices.<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.cards[].buttons[].buttonJson | Object | X |  |
| content.cards[].buttons[].buttonJson.action | Object | X | Button action |
| content.buttons | Array | X | (Deprecated, use content.cards[].buttons) RCS button list |
| content.buttons[].buttonType | String | X | COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make a call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share current location), URL (link to URL), CALENDAR (add event)<br>※ If a CLIPBOARD (copy) button is used with a unified message type, it cannot be received on iOS devices.<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | X |  |
| content.buttons[].buttonJson.action | Object | X | Button action |



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| templateId | String | O | Template ID issued when the template is registered |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Register RCS Template

POST {{endpoint}}/template/v1.0/RCS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "명절 운영시간 공지",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다. 방문해주세요^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "제목",
      "description" : "본문",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "메인 타이틀",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "제목 1",
      "title2" : "제목 2",
      "title3" : "제목 3",
      "description1" : "본문 1",
      "description2" : "본문 2",
      "description3" : "본문 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "일정 등록하기",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "일정 제목",
                "description" : "일정 설명"
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
          "displayText" : "일정 등록하기",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "일정 제목",
              "description" : "일정 설명"
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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "명절 운영시간 공지",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다. 방문해주세요^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "제목",
      "description" : "본문",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "메인 타이틀",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "제목 1",
      "title2" : "제목 2",
      "title3" : "제목 3",
      "description1" : "본문 1",
      "description2" : "본문 2",
      "description3" : "본문 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "일정 등록하기",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "일정 제목",
                "description" : "일정 설명"
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
          "displayText" : "일정 등록하기",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "일정 제목",
              "description" : "일정 설명"
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

<a id="list-rcs-templates"></a>

## List RCS Templates

Retrieves a list of templates.

**Request**

```
GET /template/v1.0/RCS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateName | Query | String | X | Template name (LIKE search) |
| limit | Query | Number | X | If limit is not set, the default value is 20. (Maximum 1,000) |
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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | O | Total count |
| templates | Array | O |  |
| templates[].templateId | String | O | Template ID issued when registering the template. |
| templates[].templateName | String | O | Template name |
| templates[].categoryId | String | O | Category ID |
| templates[].messageChannel | String | O | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| templates[].messagePurposes | Array | O |  |
| templates[].createdDateTime | String | O | Template creation time |
| templates[].updatedDateTime | String | O | Template modification time |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List RCS Templates

GET {{endpoint}}/template/v1.0/RCS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/RCS/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0027ReadRcsTemplate"></span>

<a id="get-rcs-template-details"></a>

## Get RCS Template Details

Retrieves the details of a template.

**Request**

```
GET /template/v1.0/RCS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



**Request Body**

This API does not require a request body.



**Response Body**

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "Template name",
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
      "title" : "Holiday hours notice",
      "body" : "Hello. Your order has arrived today. Please come visit us^^",
      "smsType" : "STANDALONE",
      "lmsType" : "HORIZONTAL",
      "mmsType" : "HORIZONTAL",
      "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
      "messagebaseformId" : "SS000000",
      "unsubscribePhoneNumber" : "08012341234",
      "cards" : [ {
        "title" : "Title",
        "description" : "Body",
        "attachmentId" : "20240814125609swLmoZTsGr0",
        "mTitle" : "Main title",
        "mTitleMedia" : "LT-messagebase.common-2k8ydI",
        "title1" : "Title 1",
        "title2" : "Title 2",
        "title3" : "Title 3",
        "description1" : "Body 1",
        "description2" : "Body 2",
        "description3" : "Body 3",
        "buttons" : [ {
          "buttonType" : "CALENDAR",
          "buttonJson" : {
            "action" : {
              "displayText" : "Add event",
              "calendarAction" : {
                "createCalendarEvent" : {
                  "startTime" : "2024-01-01T00:00:00.000+09:00",
                  "endTime" : "2024-01-01T00:00:00.000+09:00",
                  "title" : "Event title",
                  "description" : "Event description"
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
            "displayText" : "Add event",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "Event title",
                "description" : "Event description"
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

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | X |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| template | Object | X |  |
| template.templateId | String | O | Template ID issued when the template was registered |
| template.templateName | String | X | Template name |
| template.categoryId | String | X | Category ID |
| template.messageChannel | String | X | Message channel<br>[SMS(SMS), ALIMTALK(Alim Talk), EMAIL(Email), RCS(RCS), PUSH(Push)] |
| template.messagePurpose | String | X | Message content type<br>Default: NORMAL<br>[NORMAL(General), AD(Advertising), AUTH(Authentication)] |
| template.messagePurposes | Array | X |  |
| template.templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT(Plain text), FREEMARKER(FreeMarker template)] |
| template.sender | Object | X |  |
| template.sender.brandId | String | O | Brand ID |
| template.sender.chatbotId | String | O | Chat room (chatbot) ID |
| template.content | Object | X |  |
| template.content.messageType | String | X | RCS message type<br>[SMS(Short message), LMS(Long message), MMS(Multimedia message), RBC_TEMPLATE(RCS Biz Center template)] |
| template.content.title | String | X | Message title |
| template.content.body | String | X | Message body |
| template.content.smsType | String | X | SMS type<br>[STANDALONE(Standalone), UNIFIED_STANDALONE(Unified standalone)] |
| template.content.lmsType | String | X | LMS type<br>[STANDALONE(Standalone), FORMAT_BASIC(Basic format), FORMAT_TITLE_HIGHLIGHT(Title highlight format), FORMAT_PARAGRAPH(Paragraph format), UNIFIED_STANDALONE(Unified standalone)] |
| template.content.mmsType | String | X | MMS type (required for MMS sending)<br>[HORIZONTAL(Horizontal), VERTICAL(Vertical), CAROUSEL_MEDIUM(Carousel medium), CAROUSEL_SMALL(Carousel small), UNIFIED_HORIZONTAL(Unified horizontal), UNIFIED_VERTICAL(Unified vertical)] |
| template.content.messagebaseId | String | X | RCS Biz Center template ID |
| template.content.messagebaseformId | String | X | messageBase form designated by RCS Biz Center<br>- SS000000 (SMS basic)<br>- SL000000 (LMS basic)<br>- OL00000001 (LMS Format basic)<br>- OL00000002 (LMS Format title highlight)<br>- OL00000003 (LMS Format paragraph)<br>- SMwThT00 (MMS vertical)<br>- SMwThM00 (MMS horizontal)<br>- CMwMhM0200 (MMS slide medium (2))<br>- CMwMhM0300 (MMS slide medium (3))<br>- CMwMhM0400 (MMS slide medium (4))<br>- CMwMhM0500 (MMS slide medium (5))<br>- CMwMhM0600 (MMS slide medium (6))<br>- CMwShS0200 (MMS slide small (2))<br>- CMwShS0300 (MMS slide small (3))<br>- CMwShS0400 (MMS slide small (4))<br>- CMwShS0500 (MMS slide small (5))<br>- CMwShS0600 (MMS slide small (6))<br>- CLI00001 (Item detail)<br>- CLI00002 (Image highlight (1:1))<br>- CLI00003 (Image highlight (3:4))<br>- CLI00004 (Image & title highlight (1:1))<br>- CLI00005 (Image & title highlight (3:4))<br>- CLI00006 (Thumbnail (horizontal))<br>- CLI00007 (Thumbnail (vertical))<br>- CLI00008 (SNS (bottom button))<br>- CLI00009 (SNS (middle button))<br>- ITTBNV (Thumbnail (vertical))<br>- ITTBNH (Thumbnail (horizontal))<br>- ITHIMS (Image highlight (1:1))<br>- ITHIMV (Image highlight (3:4))<br>- ITSNSS (SNS)<br>- ITSNSH (SNS (middle button))<br>- ITHITS (Image & title highlight (1:1))<br>- ITHITV (Image & title highlight (3:4))<br>- ITCRM2 (Slide (2))<br>- ITCRM3 (Slide (3))<br>- ITCRM4 (Slide (4))<br>- ITCRM5 (Slide (5))<br>- ITCRM6 (Slide (6))<br>- CLT00001 (Item highlight DESC)<br>- CLT00002 (Item highlight TABLE)<br>- TATA001F (Title free-form FREE)<br>- TATA001C (Title free-form CELL)<br>- TATA001D (Title free-form DESC)<br>- GG000F (Title selection FREE)<br>- FF005C (Statement CELL)<br>- FF005D (Statement DESC)<br>- FF004C (Cancellation CELL)<br>- FF004D (Cancellation DESC)<br>- GG003C (Notice CELL)<br>- GG003D (Notice DESC)<br>- GG002C (Authentication CELL)<br>- GG002D (Authentication DESC)<br>- GG001C (Membership registration CELL)<br>- GG001D (Membership registration DESC)<br>- EE001C (Reservation CELL)<br>- EE001D (Reservation DESC)<br>- CC003C (Delivery CELL)<br>- CC003D (Delivery DESC)<br>- FF002C (Deposit CELL)<br>- FF002D (Deposit DESC)<br>- FF001C (Approval CELL)<br>- FF001D (Approval DESC)<br>- CC002C (Order CELL)<br>- CC002D (Order DESC)<br>- CC001C (Shipment CELL)<br>- CC001D (Shipment DESC)<br>- FF003C (Withdrawal CELL)<br>- FF003D (Withdrawal DESC)<br>- CLL00001 (LMS statement A)<br>- CLL00002 (LMS paragraph)<br>- CLL00003 (LMS title highlight)<br>- CLL00004 (LMS basic)<br>- CLL00005 (LMS statement B)<br>- CLL00006 (LMS statement C)<br>- RPSSAXX001 (Unified SMS card)<br>- RPLSAXX001 (Unified LMS card)<br>- RPMSMMX001 (Unified MMS card M)<br>- RPMSMTX001 (Unified MMS card T)<br>- RPISMMX001 (Unified image template M)<br>- RPISMTX001 (Unified image template T)<br>- RPTDXXX001 (Unified informational template)<br>- RPTFXXX001 (Unified free template)<br><br>[SS000000, SL000000, OL00000001, OL00000002, OL00000003, SMwThT00, SMwThM00, CMwMhM0200, CMwMhM0300, CMwMhM0400, CMwMhM0500, CMwMhM0600, CMwShS0200, CMwShS0300, CMwShS0400, CMwShS0500, CMwShS0600, CLI00001, CLI00002, CLI00003, CLI00004, CLI00005, CLI00006, CLI00007, CLI00008, CLI00009, ITTBNV, ITTBNH, ITHIMS, ITHIMV, ITSNSS, ITSNSH, ITHITS, ITHITV, ITCRM2, ITCRM3, ITCRM4, ITCRM5, ITCRM6, CLT00001, CLT00002, TATA001C, TATA001D, TATA001F, FF005C, FF005D, FF004C, FF004D, GG003C, GG003D, GG002C, GG002D, GG001C, GG001D, GG000F, EE001C, EE001D, CC003C, CC003D, FF002C, FF002D, FF001C, FF001D, CC002C, CC002D, CC001C, CC001D, FF003C, FF003D, CLL00001, CLL00002, CLL00003, CLL00004, CLL00005, CLL00006, RPSSAXX001, RPLSAXX001, RPMSMMX001, RPMSMTX001, RPISMMX001, RPISMTX001, RPTDXXX001, RPTFXXX001] |
| template.content.unsubscribePhoneNumber | String | X | Unsubscribe number (required for advertising messages) |
| template.content.cards | Array | X | RCS cards |
| template.content.cards[].title | String | X | Title |
| template.content.cards[].description | String | X | Body |
| template.content.cards[].attachmentId | String | X | Attachment file ID<br>※ If a GIF image is attached in a unified MMS card, it cannot be received on iOS devices. |
| template.content.cards[].mTitle | String | X | Main title |
| template.content.cards[].mTitleMedia | String | X | Main title logo file ID |
| template.content.cards[].title1 | String | X | Title 1 |
| template.content.cards[].title2 | String | X | Title 2 |
| template.content.cards[].title3 | String | X | Title 3 |
| template.content.cards[].description1 | String | X | Body 1 |
| template.content.cards[].description2 | String | X | Body 2 |
| template.content.cards[].description3 | String | X | Body 3 |
| template.content.cards[].buttons | Array | X | RCS button list |
| template.content.cards[].buttons[].buttonType | String | X | COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make a call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share current location), URL (link to URL), CALENDAR (add event)<br>※ If the CLIPBOARD (copy) button is used with a unified message type, it cannot be received on iOS devices.<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| template.content.cards[].buttons[].buttonJson | Object | X |  |
| template.content.cards[].buttons[].buttonJson.action | Object | X | Button action |
| template.content.buttons | Array | X | RCS button list |
| template.content.buttons[].buttonType | String | X | COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make a call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share current location), URL (link to URL), CALENDAR (add event)<br>※ If the CLIPBOARD (copy) button is used with a unified message type, it cannot be received on iOS devices.<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| template.content.buttons[].buttonJson | Object | X |  |
| template.content.buttons[].buttonJson.action | Object | X | Button action |
| template.additionalProperty | Object | X |  |
| template.additionalProperty.status | String | X | Template status<br>- SAVE: Saved<br>- APPROVE_WAIT: Pending approval<br>- INSPECTION_START: Inspection started<br>- INSPECTION_FINISH: Inspection completed<br>- APPROVE: Approved<br>- REJECT: Rejected<br>- MODIFY_APPROVE_WAIT: Pending modification approval<br>- MODIFY_INSPECTION_START: Modification inspection started<br>- MODIFY_INSPECTION_FINISH: Modification inspection completed<br>- MODIFY_REJECT: Modification rejected<br><br>[SAVE, APPROVE_WAIT, INSPECTION_START, INSPECTION_FINISH, APPROVE, REJECT, MODIFY_APPROVE_WAIT, MODIFY_INSPECTION_START, MODIFY_INSPECTION_FINISH, MODIFY_REJECT] |
| template.additionalProperty.approvedDateTime | String | X | Template approval date and time |
| template.createdDateTime | String | X | Template creation date and time |
| template.updatedDateTime | String | X | Template last modified date and time |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Get RCS Template Details

GET {{endpoint}}/template/v1.0/RCS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/RCS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0028UpdateRcsTemplate"></span>

<a id="update-rcs-template"></a>

## Modify RCS Template

Modifies a template.

**Request**

```
PUT /template/v1.0/RCS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | App key |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


```
{
  "templateName" : "템플릿 이름",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "명절 운영시간 공지",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다. 방문해주세요^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "제목",
      "description" : "본문",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "메인 타이틀",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "제목 1",
      "title2" : "제목 2",
      "title3" : "제목 3",
      "description1" : "본문 1",
      "description2" : "본문 2",
      "description3" : "본문 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "일정 등록하기",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "일정 제목",
                "description" : "일정 설명"
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
          "displayText" : "일정 등록하기",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "일정 제목",
              "description" : "일정 설명"
            }
          }
        }
      }
    } ]
  }
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | O | Template name |
| messagePurpose | String | X | Message content type<br>Default: NORMAL<br>[NORMAL (general), AD (advertising), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| sender | Object | X |  |
| sender.brandId | String | O | Brand ID |
| sender.chatbotId | String | O | Chat room (chatbot) ID |
| content | Object | O |  |
| content.messageType | String | X | RCS message type<br>[SMS (short message), LMS (long message), MMS (multimedia message), RBC_TEMPLATE (RCS Biz Center template)] |
| content.title | String | X | (Deprecated, use content.cards[].title) Message title |
| content.body | String | X | (Deprecated, use content.cards[].description) Message body |
| content.smsType | String | X | SMS type<br>[STANDALONE, UNIFIED_STANDALONE] |
| content.lmsType | String | X | LMS type<br>[STANDALONE, FORMAT_BASIC, FORMAT_TITLE_HIGHLIGHT, FORMAT_PARAGRAPH, UNIFIED_STANDALONE] |
| content.mmsType | String | X | MMS type (required when sending MMS)<br>[HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL, UNIFIED_HORIZONTAL, UNIFIED_VERTICAL] |
| content.messagebaseId | String | X | RCS Biz Center template ID |
| content.unsubscribePhoneNumber | String | X | Opt-out phone number (required when sending advertising messages) |
| content.cards | Array | X | RCS cards |
| content.cards[].title | String | X | Title |
| content.cards[].description | String | X | Body |
| content.cards[].attachmentId | String | X | Attachment file ID<br>※ If a GIF image is attached to a unified MMS card, it cannot be received on iOS devices. |
| content.cards[].mTitle | String | X | Main title |
| content.cards[].mTitleMedia | String | X | Main title logo file ID |
| content.cards[].title1 | String | X | Title 1 |
| content.cards[].title2 | String | X | Title 2 |
| content.cards[].title3 | String | X | Title 3 |
| content.cards[].description1 | String | X | Body 1 |
| content.cards[].description2 | String | X | Body 2 |
| content.cards[].description3 | String | X | Body 3 |
| content.cards[].buttons | Array | X | RCS button list |
| content.cards[].buttons[].buttonType | String | X | COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make a call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share current location), URL (link to URL), CALENDAR (add event)<br>※ If the CLIPBOARD (copy) button is used with a unified message type, it cannot be received on iOS devices.<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.cards[].buttons[].buttonJson | Object | X |  |
| content.cards[].buttons[].buttonJson.action | Object | X | Button action |
| content.buttons | Array | X | (Deprecated, use content.cards[].buttons) RCS button list |
| content.buttons[].buttonType | String | X | COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make a call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share current location), URL (link to URL), CALENDAR (add event)<br>※ If the CLIPBOARD (copy) button is used with a unified message type, it cannot be received on iOS devices.<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | X |  |
| content.buttons[].buttonJson.action | Object | X | Button action |



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
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



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Modify RCS Template

PUT {{endpoint}}/template/v1.0/RCS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "템플릿 이름",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "명절 운영시간 공지",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다. 방문해주세요^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "제목",
      "description" : "본문",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "메인 타이틀",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "제목 1",
      "title2" : "제목 2",
      "title3" : "제목 3",
      "description1" : "본문 1",
      "description2" : "본문 2",
      "description3" : "본문 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "일정 등록하기",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "일정 제목",
                "description" : "일정 설명"
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
          "displayText" : "일정 등록하기",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "일정 제목",
              "description" : "일정 설명"
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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "템플릿 이름",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "명절 운영시간 공지",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다. 방문해주세요^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "제목",
      "description" : "본문",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "메인 타이틀",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "제목 1",
      "title2" : "제목 2",
      "title3" : "제목 3",
      "description1" : "본문 1",
      "description2" : "본문 2",
      "description3" : "본문 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "일정 등록하기",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "일정 제목",
                "description" : "일정 설명"
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
          "displayText" : "일정 등록하기",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "일정 제목",
              "description" : "일정 설명"
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

<a id="delete-rcs-template"></a>

## Delete RCS Template

Deletes a template.

**Request**

```
DELETE /template/v1.0/RCS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0030CreatePushTemplate"></span>

<a id="register-push-template"></a>

## Register a Push Template

Registers a template.

**Request**

```
POST /template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |



**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


```
{
  "templateName" : "Template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "Representative number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Body",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Submit button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link connected when the button is pressed",
        "hint" : "Hint for the button"
      } ],
      "media" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Location of the large icon, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, used to group multiple messages together; supported on Android only",
        "description" : "Description of the group"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | O | Template name |
| categoryId | String | X | Category ID |
| messagePurpose | String | X | Message content type<br>Default: NORMAL<br>[NORMAL (general), AD (advertising), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| content | Object | O | Push message content |



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| templateId | String | O | Template ID issued when the template is registered |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Register a Push template

POST {{endpoint}}/template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "Template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "Representative number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Body",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Submit button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link connected when the button is pressed",
        "hint" : "Hint for the button"
      } ],
      "media" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Location of the large icon, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, used to group multiple messages together; supported on Android only",
        "description" : "Description of the group"
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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "Template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "Representative number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Body",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Submit button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link connected when the button is pressed",
        "hint" : "Hint for the button"
      } ],
      "media" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Location of the large icon, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, used to group multiple messages together; supported on Android only",
        "description" : "Description of the group"
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

<a id="list-push-templates"></a>

## List Push Templates

Retrieves a list of templates.

**Request**

```
GET /template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateName | Query | String | X | Template name (LIKE search) |
| limit | Query | Number | X | If limit is not set, the default value is 20. (Maximum 1,000) |
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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | O | Total count |
| templates | Array | O |  |
| templates[].templateId | String | O | Template ID issued when registering the template. |
| templates[].templateName | String | O | Template name |
| templates[].categoryId | String | O | Category ID |
| templates[].messageChannel | String | O | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| templates[].messagePurposes | Array | O |  |
| templates[].createdDateTime | String | O | Template creation time |
| templates[].updatedDateTime | String | O | Template modification time |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List Push Templates

GET {{endpoint}}/template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/PUSH/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0032ReadPushTemplate"></span>

<a id="get-push-template-details"></a>

## Get Push Template Details

Retrieves the details of a template.

**Request**

```
GET /template/v1.0/PUSH/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



**Request Body**

This API does not require a request body.



**Response Body**

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "Template name",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "content" : {
      "unsubscribePhoneNumber" : "Representative number",
      "unsubscribeGuide" : "Menu > Settings",
      "title" : "Title",
      "body" : "Body",
      "richMessage" : {
        "buttons" : [ {
          "name" : "Button name",
          "submitName" : "Submit button name",
          "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
          "link" : "Link connected when the button is tapped",
          "hint" : "Hint for the button"
        } ],
        "media" : {
          "sourceType" : "Location of the media, REMOTE, LOCAL",
          "source" : "Address of the media location, URL, LOCAL_RESOURCE",
          "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
          "extension" : "Extension of the media file, jpg, png",
          "expandable" : true
        },
        "androidMedia" : {
          "sourceType" : "Location of the media, REMOTE, LOCAL",
          "source" : "Address of the media location, URL, LOCAL_RESOURCE",
          "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
          "extension" : "Extension of the media file, jpg, png",
          "expandable" : true
        },
        "iosMedia" : {
          "sourceType" : "Location of the media, REMOTE, LOCAL",
          "source" : "Address of the media location, URL, LOCAL_RESOURCE",
          "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
          "extension" : "Extension of the media file, jpg, png",
          "expandable" : true
        },
        "largeIcon" : {
          "sourceType" : "Location of the large icon, REMOTE, LOCAL",
          "source" : "Address of the media location, URL, LOCAL_RESOURCE"
        },
        "group" : {
          "key" : "Group key, a feature that groups multiple messages together, supported on Android only",
          "description" : "Description of the group"
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

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| template | Object | O |  |
| template.templateId | String | O | Template ID issued when the template was registered |
| template.templateName | String | O | Template name |
| template.categoryId | String | O | Category ID |
| template.messageChannel | String | O | Message channel<br>[SMS(SMS), ALIMTALK(Alim Talk), EMAIL(Email), RCS(RCS), PUSH(Push)] |
| template.messagePurpose | String | O | Message content type<br>Default: NORMAL<br>[NORMAL(General), AD(Advertising), AUTH(Authentication)] |
| template.messagePurposes | Array | O |  |
| template.templateLanguage | String | O | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT(Plain text), FREEMARKER(FreeMarker template)] |
| template.content | Object | O | Push message content |
| template.createdDateTime | String | O | Time the template was created |
| template.updatedDateTime | String | O | Time the template was last modified |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Get Push Template Details

GET {{endpoint}}/template/v1.0/PUSH/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/PUSH/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0033UpdatePushTemplate"></span>

<a id="update-push-template"></a>

## Modify Push Template

Modifies a template.

**Request**

```
PUT /template/v1.0/PUSH/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



**Request Body**

<!--If this API does not require a request body, enter "This API does not require a request body."-->


```
{
  "templateName" : "Template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "Representative number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Body",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Send button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link connected when the button is pressed",
        "hint" : "Hint for the button"
      } ],
      "media" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Large icon location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key — groups multiple messages together; supported on Android only",
        "description" : "Description of the group"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | O | Template name |
| messagePurpose | String | X | Message content type<br>Default: NORMAL<br>[NORMAL (general), AD (advertising), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| content | Object | O | Push message content |



**Response Body**

<!--If this API does not return a response body, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
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



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Modify Push Template

PUT {{endpoint}}/template/v1.0/PUSH/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "Template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "Representative number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Body",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Send button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link connected when the button is pressed",
        "hint" : "Hint for the button"
      } ],
      "media" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Large icon location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key — groups multiple messages together; supported on Android only",
        "description" : "Description of the group"
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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "Template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "Representative number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Body",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Send button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link connected when the button is pressed",
        "hint" : "Hint for the button"
      } ],
      "media" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Large icon location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key — groups multiple messages together; supported on Android only",
        "description" : "Description of the group"
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

<a id="delete-push-template"></a>

## Delete Push Template

Deletes a template.

**Request**

```
DELETE /template/v1.0/PUSH/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| templateId | Path | String | O | Template ID |



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



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Delete Push Template

DELETE {{endpoint}}/template/v1.0/PUSH/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/PUSH/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0035ReadTemplateParameters"></span>

<a id="retrieve-template-parameters"></a>

## Retrieve Template Parameters

Retrieves the list of parameters included in the template.

**Request**

```
GET /template/v1.0/{messageChannel}/templates/{templateId}/parameters
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| messageChannel | Path | Enum | O | Message channel. |
| templateId | Path | String | O | Template ID |



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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| templateParameter | Object | X | Template parameter result JSON |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve template parameterss

GET {{endpoint}}/template/v1.0/{{messageChannel}}/templates/{{templateId}}/parameters
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/${messageChannel}/templates/${templateId}/parameters" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
