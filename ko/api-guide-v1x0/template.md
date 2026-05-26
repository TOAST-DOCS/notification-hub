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

## List Kakao Templates for AlimTalk Template

Retrieves a list of Kakao templates for an AlimTalk template.

**Request**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| templateId | Path | String | O | Template ID |
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
    "kakaoTemplateCode" : "kakaoTemplateCode",
    "kakaoTemplateName" : "template name",
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
    "reviewStatus" : "APPROVED",
    "comments" : [ {
      "id" : 1,
      "content" : "Sample inquiry content",
      "userName" : "Username",
      "createdAt" : "2024-10-29T06:00:01.000+09:00",
      "attachments" : [ {
        "originalFileName" : "Sample file name",
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

<!--Describes the fields in the response body.-->

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
| templates[].content.templateMessageType | String | X | Template message type (BA: basic, EX: additional info, AD: channel add, MI: mixed, default: BA) |
| templates[].content.templateEmphasizeType | String | O | Template emphasis type<br>[NONE (no emphasis), TEXT (text emphasis), IMAGE (image emphasis), ITEM_LIST (item list emphasis)] |
| templates[].content.templateContent | String | X | Template body |
| templates[].content.templateAd | String | X | Channel add guide message (fixed value when template message type is channel add or mixed) |
| templates[].content.templateExtra | String | X | Template additional information (required when template message type is additional info or mixed). Substitution variables cannot be used. URLs can be included. |
| templates[].content.templateTitle | String | X | Template title (up to 50 characters; Android: 2 lines, truncated at 23+ characters; iOS: 2 lines, truncated at 27+ characters) |
| templates[].content.templateSubtitle | String | X | Template subtitle (up to 50 characters; Android: truncated at 18+ characters; iOS: truncated at 21+ characters) |
| templates[].content.templateHeader | String | X | Template header. Variables can be entered. |
| templates[].content.templateItem | Object | X |  |
| templates[].content.templateItem.list | Array | O |  |
| templates[].content.templateItem.list[].title | String | O | Item title |
| templates[].content.templateItem.list[].description | String | O | Item description |
| templates[].content.templateItem.summary | Object | X |  |
| templates[].content.templateItem.summary.title | String | O | Summary title |
| templates[].content.templateItem.summary.description | String | O | Summary description (only variables, currency units, numbers, commas, and periods are allowed) |
| templates[].content.templateItemHighlight | Object | X |  |
| templates[].content.templateItemHighlight.title | String | O | Item highlight title (up to 30 characters; 21 characters when a thumbnail image is present) |
| templates[].content.templateItemHighlight.description | String | O | Item highlight description (up to 19 characters; 13 characters when a thumbnail image is present) |
| templates[].content.templateItemHighlight.attachmentId | String | X | Template attachment file ID |
| templates[].content.templateItemHighlight.imageUrl | String | X | Thumbnail image URL |
| templates[].content.templateRepresentLink | Object | X |  |
| templates[].content.templateRepresentLink.linkMo | String | X | Representative link - mobile web URL |
| templates[].content.templateRepresentLink.linkPc | String | X | Representative link - PC web URL |
| templates[].content.templateRepresentLink.schemeIos | String | X | Representative link - iOS app URL |
| templates[].content.templateRepresentLink.schemeAndroid | String | X | Representative link - Android app URL |
| templates[].content.attachmentId | String | X | Template attachment file ID |
| templates[].content.templateImageName | String | X | Template image name |
| templates[].content.templateImageUrl | String | X | Template image URL |
| templates[].content.securityFlag | Boolean | X | Whether the template has security enabled (default: false) |
| templates[].content.categoryCode | String | X | Template category code (see the List AlimTalk Template Categories API, default: 999999) |
| templates[].content.buttons | Array | X | Template buttons |
| templates[].content.buttons[].ordering | Integer | O | Template button order |
| templates[].content.buttons[].type | String | O | Template button type<br>[WL (web link), AL (app link), DS (delivery tracking), BK (bot keyword), MD (message forwarding), BC (consult chat switch), BT (bot switch), AC (channel add), BF (business form), P1 (image security transfer plugin), P2 (personal information usage plugin), P3 (one-click payment plugin), TN (call)] |
| templates[].content.buttons[].name | String | O | Template button name |
| templates[].content.buttons[].linkMo | String | X | Template button mobile web URL |
| templates[].content.buttons[].linkPc | String | X | Template button PC web URL |
| templates[].content.buttons[].schemeIos | String | X | Template button iOS app URL |
| templates[].content.buttons[].schemeAndroid | String | X | Template button Android app URL |
| templates[].content.buttons[].bizFormId | Integer | X | Template button business form ID (required when type is BF) |
| templates[].content.quickReplies | Array | X | Quick replies |
| templates[].content.quickReplies[].ordering | Integer | O | Quick reply order |
| templates[].content.quickReplies[].type | String | O | Quick reply type<br>[WL (web link), AL (app link), BK (bot keyword), BC (consult chat switch), BT (bot switch), BF (business form)] |
| templates[].content.quickReplies[].name | String | O | Quick reply name |
| templates[].content.quickReplies[].linkMo | String | X | Quick reply mobile web URL |
| templates[].content.quickReplies[].linkPc | String | X | Quick reply PC web URL |
| templates[].content.quickReplies[].schemeIos | String | X | Quick reply iOS app URL |
| templates[].content.quickReplies[].schemeAndroid | String | X | Quick reply Android app URL |
| templates[].content.quickReplies[].bizFormId | Integer | X | Quick reply business form ID (required when type is BF) |
| templates[].reviewStatus | String | O | REGISTERED: submitted, REQUESTED: under review, APPROVED: approved, REJECTED: rejected<br>[REGISTERED, REQUESTED, APPROVED, REJECTED] |
| templates[].comments | Array | O | Template inquiry list |
| templates[].comments[].id | Integer | O | Inquiry ID |
| templates[].comments[].content | String | X | Inquiry content |
| templates[].comments[].userName | String | O | Author |
| templates[].comments[].createdAt | String | O | Inquiry creation time |
| templates[].comments[].attachments | Array | O | Inquiry attachments |
| templates[].comments[].attachments[].originalFileName | String | O | Attachment file name |
| templates[].comments[].attachments[].filePath | String | O | Attachment file path |
| templates[].comments[].status | String | O | Inquiry status (REQ: submitted, INQ: inquired, APR: approved, REJ: rejected, REP: replied)<br>[REQ, INQ, APR, REJ, REP] |
| templates[].block | Boolean | O | Whether the template is blocked |
| templates[].dormant | Boolean | O | Whether the template is dormant |
| templates[].createdDateTime | String | O | Template creation time |
| templates[].updatedDateTime | String | O | Template modification time |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List Kakao Templates for AlimTalk Template

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

## Register SMS Template

Registers a template.

**Request**

```
POST /template/v1.0/SMS/templates
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
    "title" : "Holiday service hours notice",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience.",
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
| messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| sender | Object | O |  |
| sender.senderPhoneNumber | String | O | Sender phone number |
| content | Object | O |  |
| content.messageType | String | O | Message type (SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| content.title | String | X | Message title |
| content.body | String | O | Message body |
| content.attachmentIds | Array | X | Up to 3 attachment IDs |
| content.imageLayoutId | String | X | Image layout ID |



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

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
| templateId | String | O | Template ID issued when registering the template. |



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
    "title" : "Holiday service hours notice",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience.",
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
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday service hours notice",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}'
```

</details>

<span id="templateV1x0002ReadSmsTemplateList"></span>

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

## Get SMS Template Details

Retrieves template details.

**Request**

```
GET /template/v1.0/SMS/templates/{templateId}
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
      "title" : "Holiday service hours notice",
      "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience.",
      "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
      "imageLayoutId" : "YaX2DA4Weab1"
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | X |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| template | Object | X |  |
| template.templateId | String | O | Template ID issued when registering the template. |
| template.templateName | String | X | Template name |
| template.categoryId | String | X | Category ID |
| template.messageChannel | String | X | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| template.messagePurposes | Array | X |  |
| template.templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| template.sender | Object | X |  |
| template.sender.senderPhoneNumber | String | O | Sender phone number |
| template.content | Object | X |  |
| template.content.messageType | String | O | Message type (SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| template.content.title | String | X | Message title |
| template.content.body | String | O | Message body |
| template.content.attachmentIds | Array | X | Up to 3 attachment IDs |
| template.content.imageLayoutId | String | X | Image layout ID |
| template.createdDateTime | String | X | Template creation time |
| template.updatedDateTime | String | X | Template modification time |



**Request Example**


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

## Update SMS Template

Updates a template.

**Request**

```
PUT /template/v1.0/SMS/templates/{templateId}
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
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday service hours notice",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | O | Template name |
| messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| sender | Object | X |  |
| sender.senderPhoneNumber | String | O | Sender phone number |
| content | Object | O |  |
| content.messageType | String | O | Message type (SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| content.title | String | X | Message title |
| content.body | String | O | Message body |
| content.attachmentIds | Array | X | Up to 3 attachment IDs |
| content.imageLayoutId | String | X | Image layout ID |



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
### Update SMS Template

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
    "title" : "Holiday service hours notice",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience.",
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
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday service hours notice",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}'
```

</details>

<span id="templateV1x0005DeleteSmsTemplate"></span>

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

## Register AlimTalk Template

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
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->


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
    "templateCode" : "templateCode",
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | O | Template name |
| categoryId | String | X | Category ID |
| messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| sender | Object | X |  |
| sender.senderKey | String | X | Sender profile sender key |
| sender.senderProfileType | String | X | Sender profile type<br>[GROUP, NORMAL] |
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
| additionalProperty.templateCode | String | O | Template code (letters, numbers, -, _) |
| additionalProperty.kakaoTemplateCode | String | X | Kakao template code |



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

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
| templateId | String | O | Template ID issued when registering the template. |



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
    "templateCode" : "templateCode",
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}'
```

</details>

<span id="templateV1x0007ReadAlimtalkTemplateList"></span>

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

## Get AlimTalk Template Details

Retrieves template details.

**Request**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}
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
      "kakaoTemplateCode" : "templateCode",
      "templateCode" : "templateCode",
      "comments" : [ {
        "id" : 1,
        "content" : "Sample inquiry content",
        "userName" : "Username",
        "createdAt" : "2024-10-29T06:00:01.000+09:00",
        "attachments" : [ {
          "originalFileName" : "Sample file name",
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
| template.templateId | String | O | Template ID issued when registering the template. |
| template.templateName | String | O | Template name |
| template.categoryId | String | O | Category ID |
| template.messageChannel | String | O | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | O | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| template.messagePurposes | Array | O |  |
| template.templateLanguage | String | O | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
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
| template.additionalProperty.comments[].status | String | O | Inquiry status (REQ: submitted, INQ: inquired, APR: approved, REJ: rejected, REP: replied)<br>[REQ, INQ, APR, REJ, REP] |
| template.additionalProperty.status | String | X | REGISTERED: submitted, REQUESTED: under review, APPROVED: approved, REJECTED: rejected<br>[REGISTERED, REQUESTED, APPROVED, REJECTED] |
| template.additionalProperty.block | Boolean | O | Whether the template is blocked<br>Default: false |
| template.additionalProperty.dormant | Boolean | O | Whether the template is dormant<br>Default: false |
| template.content | Object | O |  |
| template.content.templateMessageType | String | X | Template message type (BA: basic, EX: additional info, AD: channel add, MI: mixed, default: BA) |
| template.content.templateEmphasizeType | String | O | Template emphasis type<br>[NONE (no emphasis), TEXT (text emphasis), IMAGE (image emphasis), ITEM_LIST (item list emphasis)] |
| template.content.templateContent | String | X | Template body |
| template.content.templateAd | String | X | Channel add guide message (fixed value when template message type is channel add or mixed) |
| template.content.templateExtra | String | X | Template additional information (required when template message type is additional info or mixed). Substitution variables cannot be used. URLs can be included. |
| template.content.templateTitle | String | X | Template title (up to 50 characters; Android: 2 lines, truncated at 23+ characters; iOS: 2 lines, truncated at 27+ characters) |
| template.content.templateSubtitle | String | X | Template subtitle (up to 50 characters; Android: truncated at 18+ characters; iOS: truncated at 21+ characters) |
| template.content.templateHeader | String | X | Template header. Variables can be entered. |
| template.content.templateItem | Object | X |  |
| template.content.templateItem.list | Array | O |  |
| template.content.templateItem.list[].title | String | O | Item title |
| template.content.templateItem.list[].description | String | O | Item description |
| template.content.templateItem.summary | Object | X |  |
| template.content.templateItem.summary.title | String | O | Summary title |
| template.content.templateItem.summary.description | String | O | Summary description (only variables, currency units, numbers, commas, and periods are allowed) |
| template.content.templateItemHighlight | Object | X |  |
| template.content.templateItemHighlight.title | String | O | Item highlight title (up to 30 characters; 21 characters when a thumbnail image is present) |
| template.content.templateItemHighlight.description | String | O | Item highlight description (up to 19 characters; 13 characters when a thumbnail image is present) |
| template.content.templateItemHighlight.attachmentId | String | X | Template attachment file ID |
| template.content.templateItemHighlight.imageUrl | String | X | Thumbnail image URL |
| template.content.templateRepresentLink | Object | X |  |
| template.content.templateRepresentLink.linkMo | String | X | Representative link - mobile web URL |
| template.content.templateRepresentLink.linkPc | String | X | Representative link - PC web URL |
| template.content.templateRepresentLink.schemeIos | String | X | Representative link - iOS app URL |
| template.content.templateRepresentLink.schemeAndroid | String | X | Representative link - Android app URL |
| template.content.attachmentId | String | X | Template attachment file ID |
| template.content.templateImageName | String | X | Template image name |
| template.content.templateImageUrl | String | X | Template image URL |
| template.content.securityFlag | Boolean | X | Whether the template has security enabled (default: false) |
| template.content.categoryCode | String | X | Template category code (see the List AlimTalk Template Categories API, default: 999999) |
| template.content.buttons | Array | X | Template buttons |
| template.content.buttons[].ordering | Integer | O | Template button order |
| template.content.buttons[].type | String | O | Template button type<br>[WL (web link), AL (app link), DS (delivery tracking), BK (bot keyword), MD (message forwarding), BC (consult chat switch), BT (bot switch), AC (channel add), BF (business form), P1 (image security transfer plugin), P2 (personal information usage plugin), P3 (one-click payment plugin), TN (call)] |
| template.content.buttons[].name | String | O | Template button name |
| template.content.buttons[].linkMo | String | X | Template button mobile web URL |
| template.content.buttons[].linkPc | String | X | Template button PC web URL |
| template.content.buttons[].schemeIos | String | X | Template button iOS app URL |
| template.content.buttons[].schemeAndroid | String | X | Template button Android app URL |
| template.content.buttons[].bizFormId | Integer | X | Template button business form ID (required when type is BF) |
| template.content.quickReplies | Array | X | Quick replies |
| template.content.quickReplies[].ordering | Integer | O | Quick reply order |
| template.content.quickReplies[].type | String | O | Quick reply type<br>[WL (web link), AL (app link), BK (bot keyword), BC (consult chat switch), BT (bot switch), BF (business form)] |
| template.content.quickReplies[].name | String | O | Quick reply name |
| template.content.quickReplies[].linkMo | String | X | Quick reply mobile web URL |
| template.content.quickReplies[].linkPc | String | X | Quick reply PC web URL |
| template.content.quickReplies[].schemeIos | String | X | Quick reply iOS app URL |
| template.content.quickReplies[].schemeAndroid | String | X | Quick reply Android app URL |
| template.content.quickReplies[].bizFormId | Integer | X | Quick reply business form ID (required when type is BF) |
| template.createdDateTime | String | O | Template creation time |
| template.updatedDateTime | String | O | Template modification time |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Get AlimTalk Template Details

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

## Register Email Template

Registers a template.

**Request**

```
POST /template/v1.0/EMAIL/templates
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
    "title" : "[NHN Cloud Email][##env##] Monitoring alert",
    "body" : "Hello, your item has arrived and is ready for pickup.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | O | Template name |
| categoryId | String | X | Category ID |
| messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| sender | Object | O |  |
| sender.senderMailAddress | String | O | Sender email address |
| content | Object | O |  |
| content.title | String | X | Template email subject |
| content.body | String | X | Template email body |
| content.attachmentIds | Array | X | Template attachment file IDs |



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

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
| templateId | String | O | Template ID issued when registering the template. |



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
    "title" : "[NHN Cloud Email][##env##] Monitoring alert",
    "body" : "Hello, your item has arrived and is ready for pickup.",
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
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] Monitoring alert",
    "body" : "Hello, your item has arrived and is ready for pickup.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>

<span id="templateV1x0022ReadEmailTemplate"></span>

## Get Email Template Details

Retrieves template details.

**Request**

```
GET /template/v1.0/EMAIL/templates/{templateId}
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
      "title" : "[NHN Cloud Email][##env##] Monitoring alert",
      "body" : "Hello, your item has arrived and is ready for pickup.",
      "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | X |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| template | Object | X |  |
| template.templateId | String | O | Template ID issued when registering the template. |
| template.templateName | String | X | Template name |
| template.categoryId | String | X | Category ID |
| template.messageChannel | String | X | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| template.messagePurposes | Array | X |  |
| template.templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| template.sender | Object | X |  |
| template.sender.senderMailAddress | String | O | Sender email address |
| template.content | Object | X |  |
| template.content.title | String | X | Template email subject |
| template.content.body | String | X | Template email body |
| template.content.attachmentIds | Array | X | Template attachment file IDs |
| template.createdDateTime | String | X | Template creation time |
| template.updatedDateTime | String | X | Template modification time |



**Request Example**


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

## Update Email Template

Updates a template.

**Request**

```
PUT /template/v1.0/EMAIL/templates/{templateId}
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
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] Monitoring alert",
    "body" : "Hello, your item has arrived and is ready for pickup.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateName | String | O | Template name |
| messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| sender | Object | O |  |
| sender.senderMailAddress | String | O | Sender email address |
| content | Object | O |  |
| content.title | String | X | Template email subject |
| content.body | String | X | Template email body |
| content.attachmentIds | Array | X | Template attachment file IDs |



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
### Update Email Template

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
    "title" : "[NHN Cloud Email][##env##] Monitoring alert",
    "body" : "Hello, your item has arrived and is ready for pickup.",
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
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] Monitoring alert",
    "body" : "Hello, your item has arrived and is ready for pickup.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>

<span id="templateV1x0024DeleteEmailTemplate"></span>

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

## Register RCS Template

Registers a template.

**Request**

```
POST /template/v1.0/RCS/templates
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
    "title" : "Holiday service hours notice",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience.",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
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
            "displayText" : "Register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "Schedule title",
                "description" : "Schedule description"
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
          "displayText" : "Register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "Schedule title",
              "description" : "Schedule description"
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
| messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
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
| content.unsubscribePhoneNumber | String | X | Unsubscribe phone number (required when sending advertisements) |
| content.cards | Array | X | RCS cards |
| content.cards[].title | String | X | Title |
| content.cards[].description | String | X | Body |
| content.cards[].attachmentId | String | X | Attachment file ID<br>※ Attaching a GIF image in a unified MMS card is not receivable on iOS devices. |
| content.cards[].mTitle | String | X | Main title |
| content.cards[].mTitleMedia | String | X | Main title logo file ID |
| content.cards[].title1 | String | X | Title 1 |
| content.cards[].title2 | String | X | Title 2 |
| content.cards[].title3 | String | X | Title 3 |
| content.cards[].description1 | String | X | Body 1 |
| content.cards[].description2 | String | X | Body 2 |
| content.cards[].description3 | String | X | Body 3 |
| content.cards[].buttons | Array | X | RCS button list |
| content.cards[].buttons[].buttonType | String | X | COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share location), URL (open URL), CALENDAR (add calendar) |
| content.cards[].buttons[].buttonJson | Object | X |  |
| content.cards[].buttons[].buttonJson.action | Object | X | Button action |
| content.buttons | Array | X | (Deprecated, use content.cards[].buttons) RCS button list |
| content.buttons[].buttonType | String | X | COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share location), URL (open URL), CALENDAR (add calendar)<br>※ For unified MMS, only COMPOSE and CLIPBOARD are supported. |
| content.buttons[].buttonJson | Object | X |  |
| content.buttons[].buttonJson.action | Object | X | Button action |



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

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
| templateId | String | O | Template ID issued when registering the template. |



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
    "title" : "Holiday service hours notice",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience.",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
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
            "displayText" : "Register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "Schedule title",
                "description" : "Schedule description"
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
          "displayText" : "Register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "Schedule title",
              "description" : "Schedule description"
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
    "title" : "Holiday service hours notice",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience.",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
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
            "displayText" : "Register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "Schedule title",
                "description" : "Schedule description"
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
          "displayText" : "Register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "Schedule title",
              "description" : "Schedule description"
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

## Get RCS Template Details

Retrieves template details.

**Request**

```
GET /template/v1.0/RCS/templates/{templateId}
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
      "title" : "Holiday service hours notice",
      "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience.",
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
              "displayText" : "Register schedule",
              "calendarAction" : {
                "createCalendarEvent" : {
                  "startTime" : "2024-01-01T00:00:00.000+09:00",
                  "endTime" : "2024-01-01T00:00:00.000+09:00",
                  "title" : "Schedule title",
                  "description" : "Schedule description"
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
            "displayText" : "Register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "Schedule title",
                "description" : "Schedule description"
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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | X |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| template | Object | X |  |
| template.templateId | String | O | Template ID issued when registering the template. |
| template.templateName | String | X | Template name |
| template.categoryId | String | X | Category ID |
| template.messageChannel | String | X | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| template.messagePurposes | Array | X |  |
| template.templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| template.sender | Object | X |  |
| template.sender.brandId | String | O | Brand ID |
| template.sender.chatbotId | String | O | Chat room (chatbot) ID |
| template.content | Object | X |  |
| template.content.messageType | String | X | RCS message type<br>[SMS (short message), LMS (long message), MMS (multimedia message), RBC_TEMPLATE (RCS Biz Center template)] |
| template.content.title | String | X | Message title |
| template.content.body | String | X | Message body |
| template.content.smsType | String | X | SMS type<br>[STANDALONE (standalone), UNIFIED_STANDALONE (unified standalone)] |
| template.content.lmsType | String | X | LMS type<br>[STANDALONE (standalone), FORMAT_BASIC (basic format), FORMAT_TITLE_HIGHLIGHT (title highlight format), FORMAT_PARAGRAPH (paragraph format), UNIFIED_STANDALONE (unified standalone)] |
| template.content.mmsType | String | X | MMS type (required when sending MMS)<br>[HORIZONTAL (horizontal), VERTICAL (vertical), CAROUSEL_MEDIUM (carousel medium), CAROUSEL_SMALL (carousel small), UNIFIED_HORIZONTAL (unified horizontal), UNIFIED_VERTICAL (unified vertical)] |
| template.content.messagebaseId | String | X | RCS Biz Center template ID |
| template.content.messagebaseformId | String | X | messageBase format specified by RCS Biz Center<br>- SS000000 (SMS basic)<br>- SL000000 (LMS basic)<br>- OL00000001 (LMS Format basic)<br>- OL00000002 (LMS Format title highlight)<br>- MM000000 (MMS basic) |
| template.content.unsubscribePhoneNumber | String | X | Unsubscribe phone number (required when sending advertisements) |
| template.content.cards | Array | X | RCS cards |
| template.content.cards[].title | String | X | Title |
| template.content.cards[].description | String | X | Body |
| template.content.cards[].attachmentId | String | X | Attachment file ID<br>※ Attaching a GIF image in a unified MMS card is not receivable on iOS devices. |
| template.content.cards[].mTitle | String | X | Main title |
| template.content.cards[].mTitleMedia | String | X | Main title logo file ID |
| template.content.cards[].title1 | String | X | Title 1 |
| template.content.cards[].title2 | String | X | Title 2 |
| template.content.cards[].title3 | String | X | Title 3 |
| template.content.cards[].description1 | String | X | Body 1 |
| template.content.cards[].description2 | String | X | Body 2 |
| template.content.cards[].description3 | String | X | Body 3 |
| template.content.cards[].buttons | Array | X | RCS button list |
| template.content.cards[].buttons[].buttonType | String | X | COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share location), URL (open URL), CALENDAR (add calendar) |
| template.content.cards[].buttons[].buttonJson | Object | X |  |
| template.content.cards[].buttons[].buttonJson.action | Object | X | Button action |
| template.content.buttons | Array | X | RCS button list |
| template.content.buttons[].buttonType | String | X | COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share location), URL (open URL), CALENDAR (add calendar) |
| template.content.buttons[].buttonJson | Object | X |  |
| template.content.buttons[].buttonJson.action | Object | X | Button action |
| template.additionalProperty | Object | X |  |
| template.additionalProperty.status | String | X | Template status<br>- SAVE: saved<br>- APPROVE_WAIT: pending approval<br>- INSPECTION_START: inspection started<br>- INSPECTION_FINISH: inspection completed<br>- APPROVE: approved<br>- REJECT: rejected<br>- MODIFY: modification requested |
| template.additionalProperty.approvedDateTime | String | X | Template approval time |
| template.createdDateTime | String | X | Template creation time |
| template.updatedDateTime | String | X | Template modification time |



**Request Example**


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

## Update RCS Template

Updates a template.

**Request**

```
PUT /template/v1.0/RCS/templates/{templateId}
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
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday service hours notice",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience.",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
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
            "displayText" : "Register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "Schedule title",
                "description" : "Schedule description"
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
          "displayText" : "Register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "Schedule title",
              "description" : "Schedule description"
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
| messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| sender | Object | X |  |
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
| content.unsubscribePhoneNumber | String | X | Unsubscribe phone number (required when sending advertisements) |
| content.cards | Array | X | RCS cards |
| content.cards[].title | String | X | Title |
| content.cards[].description | String | X | Body |
| content.cards[].attachmentId | String | X | Attachment file ID<br>※ Attaching a GIF image in a unified MMS card is not receivable on iOS devices. |
| content.cards[].mTitle | String | X | Main title |
| content.cards[].mTitleMedia | String | X | Main title logo file ID |
| content.cards[].title1 | String | X | Title 1 |
| content.cards[].title2 | String | X | Title 2 |
| content.cards[].title3 | String | X | Title 3 |
| content.cards[].description1 | String | X | Body 1 |
| content.cards[].description2 | String | X | Body 2 |
| content.cards[].description3 | String | X | Body 3 |
| content.cards[].buttons | Array | X | RCS button list |
| content.cards[].buttons[].buttonType | String | X | COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share location), URL (open URL), CALENDAR (add calendar) |
| content.cards[].buttons[].buttonJson | Object | X |  |
| content.cards[].buttons[].buttonJson.action | Object | X | Button action |
| content.buttons | Array | X | (Deprecated, use content.cards[].buttons) RCS button list |
| content.buttons[].buttonType | String | X | COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share location), URL (open URL), CALENDAR (add calendar)<br>※ For unified MMS, only COMPOSE and CLIPBOARD are supported. |
| content.buttons[].buttonJson | Object | X |  |
| content.buttons[].buttonJson.action | Object | X | Button action |



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
### Update RCS Template

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
    "title" : "Holiday service hours notice",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience.",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
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
            "displayText" : "Register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "Schedule title",
                "description" : "Schedule description"
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
          "displayText" : "Register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "Schedule title",
              "description" : "Schedule description"
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
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "Holiday service hours notice",
    "body" : "Hello, your item has arrived and is ready for pickup. Please visit us at your convenience.",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
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
            "displayText" : "Register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "Schedule title",
                "description" : "Schedule description"
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
          "displayText" : "Register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "Schedule title",
              "description" : "Schedule description"
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

## Register Push Template

Registers a template.

**Request**

```
POST /template/v1.0/PUSH/templates
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


```
{
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "Main number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Content",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Send button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link when button is clicked",
        "hint" : "Button hint"
      } ],
      "media" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Large icon location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, a feature to group multiple messages together, supported on Android only",
        "description" : "Group description"
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
| messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| content | Object | O | Push message content |



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

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
| templateId | String | O | Template ID issued when registering the template. |



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
    "unsubscribePhoneNumber" : "Main number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Content",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Send button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link when button is clicked",
        "hint" : "Button hint"
      } ],
      "media" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Large icon location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, a feature to group multiple messages together, supported on Android only",
        "description" : "Group description"
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
  "templateName" : "template name",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "Main number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Content",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Send button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link when button is clicked",
        "hint" : "Button hint"
      } ],
      "media" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Large icon location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, a feature to group multiple messages together, supported on Android only",
        "description" : "Group description"
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

## Get Push Template Details

Retrieves template details.

**Request**

```
GET /template/v1.0/PUSH/templates/{templateId}
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
      "unsubscribePhoneNumber" : "Main number",
      "unsubscribeGuide" : "Menu > Settings",
      "title" : "Title",
      "body" : "Content",
      "richMessage" : {
        "buttons" : [ {
          "name" : "Button name",
          "submitName" : "Send button name",
          "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
          "link" : "Link when button is clicked",
          "hint" : "Button hint"
        } ],
        "media" : {
          "sourceType" : "Media location, REMOTE, LOCAL",
          "source" : "Address of the media location, URL, LOCAL_RESOURCE",
          "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
          "extension" : "Media file extension, jpg, png",
          "expandable" : true
        },
        "androidMedia" : {
          "sourceType" : "Media location, REMOTE, LOCAL",
          "source" : "Address of the media location, URL, LOCAL_RESOURCE",
          "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
          "extension" : "Media file extension, jpg, png",
          "expandable" : true
        },
        "iosMedia" : {
          "sourceType" : "Media location, REMOTE, LOCAL",
          "source" : "Address of the media location, URL, LOCAL_RESOURCE",
          "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
          "extension" : "Media file extension, jpg, png",
          "expandable" : true
        },
        "largeIcon" : {
          "sourceType" : "Large icon location, REMOTE, LOCAL",
          "source" : "Address of the media location, URL, LOCAL_RESOURCE"
        },
        "group" : {
          "key" : "Group key, a feature to group multiple messages together, supported on Android only",
          "description" : "Group description"
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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| template | Object | O |  |
| template.templateId | String | O | Template ID issued when registering the template. |
| template.templateName | String | O | Template name |
| template.categoryId | String | O | Category ID |
| template.messageChannel | String | O | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | O | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| template.messagePurposes | Array | O |  |
| template.templateLanguage | String | O | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| template.content | Object | O | Push message content |
| template.createdDateTime | String | O | Template creation time |
| template.updatedDateTime | String | O | Template modification time |



**Request Example**


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

## Update Push Template

Updates a template.

**Request**

```
PUT /template/v1.0/PUSH/templates/{templateId}
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
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "Main number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Content",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Send button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link when button is clicked",
        "hint" : "Button hint"
      } ],
      "media" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Large icon location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, a feature to group multiple messages together, supported on Android only",
        "description" : "Group description"
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
| messagePurpose | String | X | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| templateLanguage | String | X | Template language type<br>Default: PLAIN_TEXT<br>[PLAIN_TEXT (plain text), FREEMARKER (FreeMarker template)] |
| content | Object | O | Push message content |



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
### Update Push Template

PUT {{endpoint}}/template/v1.0/PUSH/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "Main number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Content",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Send button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link when button is clicked",
        "hint" : "Button hint"
      } ],
      "media" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Large icon location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, a feature to group multiple messages together, supported on Android only",
        "description" : "Group description"
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
  "templateName" : "template name",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "Main number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Content",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Send button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link when button is clicked",
        "hint" : "Button hint"
      } ],
      "media" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE.",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Large icon location, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, a feature to group multiple messages together, supported on Android only",
        "description" : "Group description"
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

