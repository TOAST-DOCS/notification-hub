<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>Attachment</h1>

**Notification > Notification Hub > API v1.0 User Guide > Attachment**



<span id="attachmentV1x0001UploadAttachments"></span>

## Upload Attachments

Upload attachments. If specifying a FileType, you can upload the attachment for each product.

**Request**

```
POST /attachment/v1.0/attachments
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

| Path | Type | Required | Description |
| --- | --- | --- | --- |
| file | Binary | Y | File to upload |
| fileName | String |  Y | File name | 
| fileTypes | Array | N | File type to upload |


**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "attachmentId" : "20230131070811m2fDe1rXx80",
  "results" : [ {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the operation was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| attachmentId | String | Attachment ID. |
| results | Array |  |
| results[].isSuccessful | Boolean | Indicates whether the operation was successful.<br>Default: true |
| results[].resultCode | Integer | The result code of the request.<br>Default: 0 |
| results[].resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Upload Attachments

POST {{endpoint}}/attachment/v1.0/attachments
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/attachment/v1.0/attachments" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="attachmentV1x0002ReadAttachments"></span>

## Retrieve Attachment Lists

Retrieve attachment lists.

**Request**

```
GET /attachment/v1.0/attachments
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messageChannel | Query  | V1x0MessageChannel | N | Message channel |
| fileType | Query  | V1x0FileType | N | File type |
| fileName | Query  | String | N | File name |
| limit | Query  | Integer | N | If not set limit, default 50 (max. 1,000) |
| offset | Query  | Integer | N | If not set offset, default 0 |



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
  "totalCount" : 120,
  "attachments" : [ {
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "fileName" : "test.txt",
    "fileFormat" : "JPG",
    "fileSizeByte" : 21391,
    "createDateTime" : "2024-10-29T06:00:01.000+09:00",
    "expireDateTime" : "2024-10-29T06:00:01.000+09:00",
    "uploadedFileTypes" : [ "EMAIL_DEFAULT" ]
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the operation was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| totalCount | Integer | Total number of attachments |
| attachments | Array | List of attachments |
| attachments[].attachmentId | String | Unique file ID generated upon successful file upload |
| attachments[].fileName | String | Uploaded file name |
| attachments[].fileFormat | String | File format |
| attachments[].fileSizeByte | Long | Attachment file size in bytes |
| attachments[].createDateTime | String | File uploaded at |
| attachments[].expireDateTime | String | File expired at |
| attachments[].uploadedFileTypes | Array | List of file types uploaded to each product |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve Attachment Lists

GET {{endpoint}}/attachment/v1.0/attachments
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/attachment/v1.0/attachments" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="attachmentV1x0003ReadAttachment"></span>

## View Attachment Details

View attachments with attachment IDs.


**Request**

```
GET /attachment/v1.0/attachments/{attachmentId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| attachmentId | Path  | String | Y | Attachment ID |



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
  "attachment" : {
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "fileName" : "test.txt",
    "fileFormat" : "JPG",
    "previewUrl" : "https://www.example.com/preview/test.txt",
    "fileSizeByte" : 21391,
    "createDateTime" : "2024-10-29T06:00:01.000+09:00",
    "expireDateTime" : "2024-10-29T06:00:01.000+09:00",
    "uploadedFileTypes" : [ "EMAIL_DEFAULT" ]
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
| attachment | Object |  |
| attachment.attachmentId | String | Unique file ID generated upon successful file upload |
| attachment.fileName | String | Upload file name |
| attachment.fileFormat | String | File format |
| attachment.previewUrl | String | File preview URL - Expiration time exists (generated when calling detailed query) |
| attachment.fileSizeByte | Long | Attachment file size unit is byte |
| attachment.createDateTime | String | File uploaded at |
| attachment.expireDateTime | String | File expired at |
| attachment.uploadedFileTypes | Array | List of file types uploaded to each product |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View Attachment Details

GET {{endpoint}}/attachment/v1.0/attachments/{{attachmentId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/attachment/v1.0/attachments/${attachmentId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="attachmentV1x0004DoValidateAttachments"></span>

## Validate Attachments before Upload

Validates attachments before they are uploaded. The system checks the file type, format, size, resolution, and dimensions (width/height) to ensure they meet the defined criteria.


**Request**

```
POST /attachment/v1.0/attachments/do-validate
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
  "results" : [ {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the operation was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| results | Array |  |
| results[].isSuccessful | Boolean | Indicates whether the operation was successful.<br>Default: true |
| results[].resultCode | Integer | The result code of the request.<br>Default: 0 |
| results[].resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Validate Attachments before Upload

POST {{endpoint}}/attachment/v1.0/attachments/do-validate
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/attachment/v1.0/attachments/do-validate" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="attachmentV1x0005DoValidateAttachment"></span>

## Validate Attachments after Upload

Validates existing attachments against a new file type. This allows you to verify compatibility before calling the File Type Update API.


**Request**

```
POST /attachment/v1.0/attachments/{attachmentId}/do-validate
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| attachmentId | Path  | String | Y | Attachment ID |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "fileTypes" : [ "EMAIL_DEFAULT" ]
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| fileTypes | Array | Y | File type list for validating attachments |



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "results" : [ {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the operation was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| results | Array |  |
| results[].isSuccessful | Boolean | Indicates whether the operation was successful.<br>Default: true |
| results[].resultCode | Integer | The result code of the request.<br>Default: 0 |
| results[].resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Validate Attachments after Upload

POST {{endpoint}}/attachment/v1.0/attachments/{{attachmentId}}/do-validate
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "fileTypes" : [ "EMAIL_DEFAULT" ]
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/attachment/v1.0/attachments/${attachmentId}/do-validate" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "fileTypes" : [ "EMAIL_DEFAULT" ]
}'
```

</details>
<span id="attachmentV1x0006UpdateFileType"></span>

## Update Uploaded Attachment File Type

Updates the file type of an uploaded attachment.


**Request**

```
POST /attachment/v1.0/attachments/{attachmentId}/file-types
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| attachmentId | Path  | String | Y | Attachment ID |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "fileTypes" : [ "EMAIL_DEFAULT", "SMS_DEFAULT", "RCS_DEFAULT", "ALIMTALK_IMAGE", "ALIMTALK_ITEM_HIGHLIGHT_IMAGE" ]
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| fileTypes | Array | N | Product attachment file types. Multiple allowed. For templates, use EMAIL_TEMPLATE or SMS_TEMPLATE. |



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "results" : [ {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the operation was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| results | Array | The result of the multiple resource tasks. |
| results[].isSuccessful | Boolean | Indicates whether the operation was successful.<br>Default: true |
| results[].resultCode | Integer | The result code of the request.<br>Default: 0 |
| results[].resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Update Uploaded Attachment File Type

POST {{endpoint}}/attachment/v1.0/attachments/{{attachmentId}}/file-types
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "fileTypes" : [ "EMAIL_DEFAULT", "SMS_DEFAULT", "EMAIL_TEMPLATE", "SMS_TEMPLATE" ]
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/attachment/v1.0/attachments/${attachmentId}/file-types" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "fileTypes" : [ "EMAIL_DEFAULT", "SMS_DEFAULT", "EMAIL_TEMPLATE", "SMS_TEMPLATE" ]
}'
```

</details>
<span id="attachmentV1x0007ReadFileTypes"></span>

## List Attachment File Types

Views the list of supported attachment types. Select a message channel to see the specific file types available for that channel.


**Request**

```
GET /attachment/v1.0/attachments/file-types
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messageChannel | Query  | V1x0MessageChannel | N | Message channel |



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
  "fileTypes" : [ "EMAIL_DEFAULT", "SMS_DEFAULT", "RCS_DEFAULT", "ALIMTALK_IMAGE", "ALIMTALK_ITEM_HIGHLIGHT_IMAGE" ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the operation was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| fileTypes | Array | File type list |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve a List of Attachment File Types

GET {{endpoint}}/attachment/v1.0/attachments/file-types
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/attachment/v1.0/attachments/file-types" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>