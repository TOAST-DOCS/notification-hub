<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Template</h1>

**Notification > Notification Hub > API v1.0 User Guide > Template**

## Template

<span id="create-template"></span>

### Create a Template

**Request**

```
POST /template/v1.0/{messageChannel}/templates
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |

**Request Body**

```json
{
  "templateName": "Template_Name",
  "categoryId": "Template_Category_Id",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "content": {
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub] Announcement",
    "body": "Hello. This is NHN Cloud Notification Hub",
    "attachmentIds": [
      "Attachment_File_Ids"
    ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Name | Type | Required | Description                                |
| --- | --- | --- |-----------------------------------|
| templateName | String | Y | Template name                            |
| categoryId | String | Y | Template category ID                      |
| messagePurpose | String | Y | Message purpose                            |
| templateLanguage | String | Y | Template language<br>PLAIN_TEXT, FREE_MARKER |
| sender | Object | Y | Sender                               |
| content | Object | Y | Content                                |

* Template categories can be created using the Template Categories API.
* Select one of the following for the template language: PLAIN_TEXT, FREE_MARKER.
* If your template language is FREE_MARKER, you can use FREE_MARKER syntax in your template content.
* The **sender**, **content** fields are identical to the request body of the free-form message sending API.

#### Sender field per message channel

| Message channels | Field | Description                        |
| --- | --- |---------------------------|
| SMS | sender.senderPhoneNumber | Sender ID                    |
| RCS | sender.brandId | Brand ID                   |
| RCS | sender.chatbotId | Room ID                   |
| EMAIL | sender.senderMailAddress | Sender email address                |
| ALIMTALK, FRIENDTALK | sender.senderKey | Sender key                       |
| ALIMTALK | sender.senderProfileType | Sender profile type<br>GROUP, NORMAL |

* AlimTalk requires a senderKey and senderProfileType to be entered.
* FriendTalk can only use the NORMAL sender profile type. If you use a sending key with the GROUP sender profile type, the sending will fail.
* There are two sender profile types: GROUP and NORMAL. **GROUP** is a group sender profile and **NORMAL**is a normal sender profile.

### AlimTalk template details request body

* AlimTalk requires template registration to be sent.
* Once you register your AlimTalk template, it will be reviewed and approved by Kakao Business, and you can use it after approval.
* The AlimTalk template can be used to communicate with Kakao Business reviewers during the review and approval process.
    * [Go to KakaoTalk Channel Admin Center](https://center-pf.kakao.com)
    * AlimTalk Templates additionally provides APIs to **inquire about AlimTalk template, **inquire about AlimTalk template file attachment**, and **view AlimTalk template revision history**.

```json
{
  "templateName": "Template name",
  "categoryId": "Category_Id",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderKey": "sender_key",
    "senderProfileType": "GROUP"
  },
  "content": {
    "templateMessageType": "BA",
    "templateEmphasizeType": "NONE",
    "templateContent": "#{Name}'s order has been completed",
    "templateAd": "Add channel and receive marketing messages from this channel in KakaoTalk",
    "templateExtra": "* Due to the real-time nature of reservations, duplicate reservations may occur, and reservations may be canceled if the room is unavailable.\\n* Contact: 1234-1234",
    "templateTitle": "123,450won",
    "templateSubtitle": "Approval History",
    "templateHeader": "Your order has been fulfilled",
    "templateItem": {
      "list": [],
      "summary": {
        "title": "string",
        "description": "string"
      }
    },
    "templateItemHighlight": {
      "title": "string",
      "description": "string",
      "attachmentId": "YaX2DA4Weab2",
      "imageUrl": "string"
    },
    "templateRepresentLink": {
      "linkMo": "string",
      "linkPc": "string",
      "schemeIos": "string",
      "schemeAndroid": "string"
    },
    "attachmentId": "YaX2DA4Weab2",
    "templateImageName": "image.png",
    "templateImageUrl": "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "securityFlag": false,
    "categoryCode": "999999",
    "buttons": [],
    "quickReplies": []
  },
  "additionalProperty": {
    "templateCode": "templateCode",
    "kakaoTemplateCode": "kakaoTemplateCode",
    "comments": [],
    "status": "APR",
    "templateModificationStatus": "APR",
    "block": false,
    "dormant": false
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Name | Type | Required | Description |
| --- | --- | --- | --- |

<!--TODO: 요청 본문의 필드를 설명합니다.-->


**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "templateId": "template_id"
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Create a template
POST {{endpoint}}/template/v1.0/{{messageChannel}}/templates
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "templateName": "Template_Name",
  "categoryId": "Template_Category_Id",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "content": {
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub] Announcement",
    "body": "Hello. This is NHN Cloud Notification Hub",
    "attachmentIds": [
      "Attachment_File_Ids"
    ]
  }
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/templates" \
     -H "Content-Type: application/json" \
     -h "x-nc-app-key: ${app_key}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
        "templateName": "Template_Name",
        "categoryId": "Template_Category_Id",
        "messagePurpose": "NORMAL",
        "templateLanguage": "PLAIN_TEXT",
        "sender": {
          "senderPhoneNumber": "01012341234"
        },
        "content": {
          "messageType": "MMS",
          "title": "[NHN Cloud Notification Hub] Announcement",
          "body": "Hello. This is NHN Cloud Notification Hub",
          "attachmentIds": [
            "Attachment_File_Ids"
          ]
        }
      }'
```

</details>

<span id="get-templates"></span>

### View Templates

**Request**

```
GET /template/v1.0/{messageChannel}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name           | In | Type | Required | Description                                                 |
|--------------| --- | --- | --- |-------------------------------------------------------------------|
| appKey       | Header | String | Y | Appkey                                                             |
| accessToken  | Header | String | Y | Authentication Token                                                |
| templateName | Query | String | N | Searchable template names and prefixes                               |
| limit        | Query | Integer | N | Number of views (default: 20)                                       |
| offset       | Query | Integer | N | View start location (default: 0)                                    |

**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "templates": [
    {
      "templateId": "Template_Id",
      "templateName": "Template_Name",
      "categoryId": "Template_Category_Id",
      "messagePurpose": "NORMAL",
      "templateLanguage": "PLAIN_TEXT",
      "sender": {
        "senderPhoneNumber": "01012341234"
      },
      "content": {
        "messageType": "MMS",
        "title": "[NHN Cloud Notification Hub] Announcement",
        "body": "Hello. This is NHN Cloud Notification Hub",
        "attachmentIds": [
          "Attachment_File_Ids"
        ]
      },
      "createdDateTime": "2023-01-01T00:00:00Z",
      "updatedDateTime": "2023-01-01T00:00:00Z"
    }
  ],
  "totalCount": 1
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View templates
GET {{endpoint}}/template/v1.0/{{messageChannel}}/templates
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/templates" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

<span id="get-template"></span>

### View a Template

**Request**

```
GET /template/v1.0/{messageChannel}/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| templateId | Path | String | Y | Template ID |

**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "template": {
    "templateId": "Template_Id",
    "templateName": "Template_Name",
    "categoryId": "Template_Category_Id",
    "messagePurpose": "NORMAL",
    "templateLanguage": "PLAIN_TEXT",
    "sender": {
      "senderPhoneNumber": "01012341234"
    },
    "content": {
      "messageType": "MMS",
      "title": "[NHN Cloud Notification Hub] Announcement",
      "body": "Hello. This is NHN Cloud Notification Hub",
      "attachmentIds": [
        "Attachment_File_Ids"
      ]
    },
    "createdDateTime": "2023-01-01T00:00:00Z",
    "updatedDateTime": "2023-01-01T00:00:00Z"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View a template
GET {{endpoint}}/template/v1.0/{{messageChannel}}/templates/{templateId}
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/templates/${TEMPLATE_ID}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

<span id="put-template"></span>

### Modify Templates

**Request**

```
PUT /template/v1.0/{messageChannel}/templates/{templateId}
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| templateId | Path | String | Y | Template ID |

**Request Body**

```json
{
  "templateName": "Template_Name",
  "categoryId": "Template_Category_Id",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "content": {
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub] Announcement",
    "body": "Hello. This is NHN Cloud Notification Hub",
    "attachmentIds": [
      "Attachment_File_Ids"
    ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Modify a template
PUT {{endpoint}}/template/v1.0/{{messageChannel}}/templates/{templateId}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "templateName": "Template_Name",
  "categoryId": "Template_Category_Id",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "content": {
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub] Announcement",
    "body": "Hello. This is NHN Cloud Notification Hub",
    "attachmentIds": [
      "Attachment_File_Ids"
    ]
  }
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X PUT "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/templates/${TEMPLATE_ID}" \
     -H "Content-Type: application/json" \
     -h "x-nc-app-key: ${app_key}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
        "templateName": "Template_Name",
        "categoryId": "Template_Category_Id",
        "messagePurpose": "NORMAL",
        "templateLanguage": "PLAIN_TEXT",
        "sender": {
          "senderPhoneNumber": "01012341234"
        },
        "content": {
          "messageType": "MMS",
          "title": "[NHN Cloud Notification Hub] Announcement",
          "body": "Hello. This is NHN Cloud Notification Hub",
          "attachmentIds": [
            "Attachment_File_Ids"
          ]
        }
      }'
```

</details>

<span id="delete-template"></span>

### Delete a Template

**Request**

```
DELETE /template/v1.0/{messageChannel}/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| templateId | Path | String | Y | Template ID |

**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Delete a template
DELETE {{endpoint}}/template/v1.0/{{messageChannel}}/templates/{templateId}
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X DELETE "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/templates/${TEMPLATE_ID}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

### Contact us for AlimTalk templates

**Request**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/inquiries
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| templateId | Path | String | Y | Template ID |

**Request Body**

```json
{
  "comment": "Your comment"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Name | Type | Required | Description                |
| --- | --- | --- |-------------------|
| comment | String | Y | Inquiry content (maximum length: 500) |

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Inquire About Alimtalk Template
POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{templateId}/inquiries
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "comment": "Your inquiry"
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/template/v1.0/ALIMTALK/templates/${TEMPLATE_ID}/inquiries" \
     -H "Content-Type: application/json" \
     -h "x-nc-app-key: ${app_key}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
        "comment": "Your inquiry"
      }'
```

</details>

### Inquire About AlimTalk Template File Attachments

**Request**

```
POST /template/v1.0/ALIMTALK/templates/${TEMPLATE_ID}/inquiries/do-with-file
Content-Type: multipart/form-data
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| templateId | Path | String | Y | Template ID |
| comment | Query | String | Y | Inquiry content (maximum length: 500) |

**Request Body**

* File attachments are requested **with multipart/form-data**.
* **In form-data,**set the **file** data in the **file** field.

```
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="file"; filename="attachment.xlsx"
Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet

<File Data
------WebKitFormBoundary7MA4YWxkTrZu0gW--
```

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Alimtalk template file attachment inquiries
POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{templateId}/inquiries/do-with-file?fileName=attachment.xlsx
Content-Type: multipart/form-data
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

--boundary
Content-Disposition: form-data; name="file"; fileName="attachment.xlsx"
Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet


< ./file/attachment.xlsx
--boundary--.
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/template/v1.0/ALIMTALK/templates/${TEMPLATE_ID}/inquiries/do-with-file?fileName=attachment.xlsx" \
     -H "Content-Type: multipart/form-data" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -F "file=@./file/attachment.xlsx"
```

</details>

### View AlimTalk Template Revision History

**Request**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}/modifications
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| templateId | Path | String | Y | Template ID |

**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "templates": [
    {
      "templateId": "Template_Id",
      "templateName": "Template_Name",
      "categoryId": "Template_Category_Id",
      "messageChannel": "ALIMTALK",
      "messagePurpose": "NORMAL",
      "templateLanguage": "PLAIN_TEXT",
      "sender": {
        "senderKey": "Sender_Key",
        "senderProfileId": "Sender_Profile_Id",
        "senderProfileType": "GROUP"
      },
      "content": {
          "templateMessageType": "BA",
          "templateEmphasizeType": "NONE",
          "templateContent": "#{Name}'s order has been completed",
            "templateAd": "Add channel and receive marketing messages from this channel in KakaoTalk",
            "templateExtra": "* Due to the real-time nature of reservations, duplicate reservations may occur, and reservations may be canceled if the room is unavailable.\\n* Contact: 1234-1234",
            "templateTitle": "123,450won",
            "templateSubtitle": "Approval History",
            "templateHeader": "Your order has been fulfilled",
            "templateItem": {
              "list": [
                {
                "title": "Title",
                "description": "Description"
                }
              ],
              "summary": {
                "title": "Title",
                "description": "Description"
              }
            },
            "templateItemHighlight": {
              "title": "Title",
              "description": "Description",
              "attachmentId": "Highlight_image_attachment_id",
              "imageUrl": "highlight_image_link"
            },
            "templateRepresentLink": {
              "linkMo": "Mobile_link",
              "linkPc": "PC_link",
              "schemeIos": "iOS_link",
              "schemeAndroid": "Android_link"
            },
            "attachmentId": "Attachment_File_Id",
            "templateImageName": "Image_File_Name",
            "templateImageUrl": "Image_link",
            "securityFlag": false,
            "categoryCode": "999999",
            "buttons": [
              {
                "ordering": 1,
                "type": "WL",
                "name": "button_name",
                "linkMo": "Mobile_link",
                "linkPc": "PC_link",
                "schemeIos": "iOS_link",
                "schemeAndroid": "Android_link",
                "bizFormId": 1
              }
            ],
            "quickReplies": [
              {
                "ordering": 1,
                "type": "WL",
                "name": "Button_Name",
                "linkMo": "Mobile_link",
                "linkPc": "PC_link",
                "schemeIos": "iOS_link",
                "schemeAndroid": "Android_link",
                "bizFormId": 1
              }
            ]
      },
      "createdDateTime": "2023-01-01T00:00:00Z",
      "updatedDateTime": "2023-01-01T00:00:00Z"
    }
  ],
  "totalCount": 1
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Name | Type            | Description                |
| --- |---------------| ------------------|
| templateCode         | String        | Template code (up to 20 characters) |
| templateName         | String        | Template name (up to 150 characters) |
| templateContent      | String        | Template body (up to 1000 characters) |
| templateMessageType  | String        | Template message types<br>BA: Basic, EX: Enhanced, AD: Added Channel, MI: Mixed (Default: BA) |
| templateEmphasizeType| String        | Template highlighting type<br>NONE: Default, TEXT: Highlighted, IMAGE: Image, ITEM_LIST: Itemized (Default: NONE)<br>- When selecting TEXT: templateTitle, templateSubtitle required<br>- When selecting IMAGE: templateImageName, templateImageUrl required<br>- When selecting ITEM_LIST: At least one of image, header, item highlights, or item list. |
| templateExtra        | String        | Additional template information<br>Required if the template message type is Informational or Complex |
| templateTitle        | String        | Template title (up to 50 characters)<br>Android: Word wrap for 2 lines, 23 characters or more<br>iOS: Word wrap for 2 lines, 27 characters or more |
| templateSubtitle     | String        | Template secondary copy (up to 50 characters)<br>Android: Handling word truncation when more than 18 characters<br>iOS: Handling word reduction when more than 21 characters are used |
| templateHeader       | String        | Template header (up to 16 characters) |
| templateItem         | Object        | Item |
| templateItem.list    | Object Array | List of items (minimum 2, maximum 10) |
| templateItem.list.title | String        | Title (up to 6 characters) |
| templateItem.list.description | String        | Description (up to 23 characters) |
| templateItem.summary | Object        | Item summary information |
| templateItem.summary.title | String        | Title (up to 6 characters) |
| templateItem.summary.description | String        | Description (variables and monetary units, numbers, commas, and periods only, up to 14 characters) |
| templateItemHighlight | Object        | Item highlight |
| templateItemHighlight.title | String        | Title (up to 30 characters, 21 characters if you have a thumbnail image) |
| templateItemHighlight.description | String        | Description (up to 19 characters, 13 characters if you have a thumbnail image) |
| templateItemHighlight.imageUrl | String        | Thumbnail image address |
| templateRepresentLink | Object        | Representative links |
| templateRepresentLink.linkMo | String        | Mobile web link (up to 500 characters) |
| templateRepresentLink.linkPc | String        | PC web link (up to 500 characters) |
| templateRepresentLink.schemeIos | String        | iOS app link (up to 500 characters) |
| templateRepresentLink.schemeAndroid | String        | Android app link (up to 500 characters) |
| templateImageName   | String        | Image name (name of uploaded file) |
| templateImageUrl    | String        | Image URL |
| securityFlag        | Boolean       | Whether it is a security template<br>For secure messages, such as OTP, click Settings<br>Do not expose message text to devices other than the primary device at the time of sending (default: false) |
| categoryCode        | String        | Template Category Code (see Template Category Lookup API, default: 999999)<br>Lowest priority review for category Other |
| buttons             | Object Array | List of buttons (up to 5) |
| buttons[].ordering    | Integer       | Button sequence (1~5) |
| buttons[].type        | String        | Button type<br>WL: Web link, AL: App link, DS: Delivery tracking, BK: Bot keyword, MD: Message delivery, BC: Chat conversion, BT: Bot conversion, AC: Add channel, BF: Business form, P1: Secure image delivery plugin ID, P2: Privacy plugin ID, P3: One-click payment plugin ID |
| buttons[].name        | String        | Button name (required, if there's a button, up to 14 characters) |
| buttons[].linkMo      | String        | Mobile web link (required for the WL type, up to 500 characters) |
| buttons[].linkPc      | String        | PC web link (optional field if WL type, maximum 500 characters) |
| buttons[].schemeIos   | String        | iOS app link (required field if AL type, 500 characters max) |
| buttons[].schemeAndroid | String        | Android app link (required field if AL type, 500 characters max) |
| buttons[].bizFormId   | Integer       | Business form ID (required for BF type) |
| buttons[].pluginId    | String        | Plugin ID (up to 24 characters) |
| quickReplies        | Object Array         | Quick reply list (up to 5) |
| quickReplies[].ordering | Integer       | Quick reply order (required  when quick reply exists) |
| quickReplies[].type   | String        | Direct Connection Type<br>WL: web link, AL: app link, BK: bot keyword, BC: chat conversion, BT: bot conversion, BF: business form |
| quickReplies[].name   | String        | Quick reply name (required  when quick reply exists, up to 14 characters) |
| quickReplies[].linkMo | String        | Mobile web link (required for the WL type, up to 500 characters) |
| quickReplies[].linkPc | String        | PC web link (optional field if WL type, maximum 500 characters) |
| quickReplies[].schemeIos | String        | iOS app link (required field if AL type, 500 characters max) |
| quickReplies[].schemeAndroid | String        | Android app link (required field if AL type, 500 characters max) |
| quickReplies[].bizFormId | Integer       | Business form ID (required for BF type) |

* The templateAd value is fixed when registering the AD included (AD) or Mixed Purposes (MI) message type template.
* The Add Chanel button must be in the first when registering the AD included (AD) or Mixed Purposes (MI) message type template.
* null

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View AlimTalk template revision history
GET {{endpoint}}/template/v1.0/ALIMTALK/templates/{templateId}/modifications
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/template/v1.0/ALIMTALK/templates/${TEMPLATE_ID}/modifications" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

---

### Create a template category

**Request**

```
POST /template/v1.0/{messageChannel}/categories
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| messageChannel | Path | String | Y | Message channels<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |

**Request Body**

```json
{
  "parentCategoryId": "Parent_Category_Id",
  "name": "Category_Name"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Name | Type | Required | Description                |
| --- | --- | --- |-------------------|
| parentCategoryId | String | Optional | Parent Category ID |
| name | String | Required | Category name (up to 50 characters) |

* A top-level category is created by default. The top-level category **is ROOT**.
* New categories can be created from the top-level category down.

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "categoryId": "Category_Id"
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Create a category
POST {{endpoint}}/template/v1.0/{{messageChannel}}/categories
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "parentCategoryId": "Parent_Category_Id",
  "name": "Category_Name"
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories" \
     -H "Content-Type: application/json" \
     -h "x-nc-app-key: ${app_key}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
     -d '{
         "parentCategoryId": "Parent_Category_Id",
         "name": "Category_Name"
     }'
```

</details>

### View Category List

**Request**

```
GET /template/v1.0/{messageChannel}/categories
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| messageChannel | Path | String | Y | Message channels<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |

**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "categories": [
    { "categoryId": "category_id
      "categoryId": "Category_Id",
      "name": "Category name",
      "parentCategoryId": "Parent_Category_Id",
      "categoryIds": [
        "child_category_id"
      ],
      "templateIds": [
        "Template_Ids belonging to category"
      ]
    }
  ]
}
```

<!--TODO: categoryIds => childCategoryIds로 이름 변경 필요-->
<!--TODO: totalCount 추가 필요-->

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Get list of categories
GET {{endpoint}}/template/v1.0/{{messageChannel}}/categories
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

### View Category Tree

**Request**

```
GET /template/v1.0/{messageChannel}/category-tree
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description                                                     |
| --- | --- | --- | --- |--------------------------------------------------------|
| appKey | Header | String | Y | Appkey                                                     |
| accessToken | Header | String | Y | Authentication Token                                                  |
| messageChannel | Path | String | Y | Message channels<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH  |
| categoryTemplateName | Query | String | N | Searchable by category, template name, prefix, or single character wildcard                      |
| senderProfileType | Query | String | N | Sender profile type (GROUP, USER), Notification Chats and Friend Chats only                |
| senderKey | Query | String | N | Sender ID, Notification Chats and Friend Chats only                                   |

<!--TODO: status 필드가 없는데 필요한지 확인 필요-->

**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "categories": [
    {
      "categoryId": "ROOT",
      "categoryName": "Root Category",
      "parentCategoryId": null,
      "messageChannel": "SMS",
      "categories": [
        { "categoryName".
          "categoryId": "Category_Id",
          "categoryName": "category_name",
          "parentCategoryId": "ROOT",
          "messageChannel": "SMS",
          "categories": [
            { "categoryName".
              "categoryId": "Category_Id",
              "categoryName": "Category_Name",
              "parentCategoryId": "6XAeH2yo",
              "messageChannel": "SMS",
              "categories": [],
              "templates": [
                {
                  "templateId": "Template_Id",
                  "templateName": "template_name"
                },
                {
                  "templateId": "Template_Id",
                  "templateName": "Template_Name"
                }
              ]
            }
          ],
          "templates": []
        }
      ],
      "templates": []
    }
  ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Name                      | Type            | Description                |
|-------------------------|---------------|-------------------|
| categories.[]categoryId | String        | Category ID |
| categories.[]categoryName            | String        | Category name |
| categories.[]parentCategoryId        | String        | Parent Category ID |
| categories.[]messageChannel          | String        | Message channels<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| categories.[]categories              | Object Array | List of subcategories |
| categories.[]templates               | Object Array         | Template list |
| categories.[]templates.[]templateId  | String        | Template ID |
| categories.[]templates.[]templateName| String        | Template name |

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View category tree
GET {{endpoint}}/template/v1.0/{{messageChannel}}/category-tree
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/category-tree" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

### View Category

**Request**

```
GET /template/v1.0/{messageChannel}/categories/{categoryId}
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| messageChannel | Path | String | Y | Message channels<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| categoryId | Path | String | Y | Category ID |

**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "category": {
    "categoryId": "Category_Id",
    "categoryName": "Category_Name",
    "parentCategoryId": "Parent_Category_Id",
    "messageChannel": "SMS",
    "categoryIds": [
      "child_category_id"
    ],
    "templateIds": [
      "Category_belonging_template_id"
    ]
  }
}
```

<!--TODO: 카테고리 이름을 name or categoryName으로 할지 통일 필요, name으로 변경 필요-->

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**


<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Get categories by message channel
GET {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories/{categoryId}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

### Modify Categories

**Request**

```
PUT /template/v1.0/{messageChannel}/categories/{categoryId}
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| messageChannel | Path | String | Y | Message channels<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| categoryId | Path | String | Y | Category ID |

**Request Body**

```json
{
  "parentCategoryId": "Parent_Category_Id",
  "name": "Category_Name"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Name | Type | Required | Description                |
| --- | --- | --- |-------------------|
| parentCategoryId | String | Optional | Parent Category ID |
| name | String | Required | Category name (up to 50 characters) |

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Modify a category
PUT {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "parentCategoryId": "Parent_Category_Id",
  "name": "Category_Name"
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X PUT "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories/{categoryId}" \
     -H "Content-Type: application/json" \
     -h "x-nc-app-key: ${app_key}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
         "parentCategoryId": "Parent_Category_Id",
         "name": "Category_Name"
     }'
```

</details>

### Add a template to a template category

**Request**

```
POST /template/v1.0/${MESSAGE_CHANNEL}/categories/${CATEGORY_ID}/templates
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| messageChannel | Path | String | Y | Message channels<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |

**Request Body**

```json
{
  "templateId": "template_id"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Name | Type | Required | Description                |
| --- | --- | --- |-------------------|
| templateId | String | Required | Template ID |

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Add template to template category
POST {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}/templates
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "templateId": "template_id"
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories/${CATEGORY_ID}/templates" \
     -H "Content-Type: application/json" \
     -h "x-nc-app-key: ${app_key}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
         "templateId": "Template_Id"
     }'
```

</details>

### Delete a category

**Request**

```
DELETE /template/v1.0/{messageChannel}/categories/{categoryId}
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| messageChannel | Path | String | Y | Message channels<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| categoryId | Path | String | Y | Category ID |

**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->
This API does not require a request body.

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Delete category
DELETE {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X DELETE "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories/${CATEGORY_ID}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>


