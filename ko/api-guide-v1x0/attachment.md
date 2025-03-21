<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>첨부 파일</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 첨부 파일**



<span id="attachmentV1x0001UploadAttachments"></span>

## 첨부 파일 업로드

첨부 파일을 업로드합니다. FileType을 지정할 경우, 개별 상품에 대한 첨부 파일 업로드를 수행합니다.

**요청**

```
POST /attachment/v1.0/attachments
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.



**응답 본문**

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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| attachmentId | String | 첨부 파일 아이디입니다. |
| results | Array |  |
| results[].isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| results[].resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| results[].resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 첨부 파일 업로드

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

## 첨부 파일 목록 조회

첨부 파일의 목록을 반환합니다.

**요청**

```
GET /attachment/v1.0/attachments
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageChannel | Query  | V1x0MessageChannel | N | 메시지 채널 |
| fileType | Query  | V1x0FileType | N | 파일 유형 |
| fileName | Query  | String | N | 파일 이름 |
| limit | Query  | Integer | N | limit 설정하지 않으면 default 50(최대 1000) |
| offset | Query  | Integer | N | offset 설정하지 않으면 default 0 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.



**응답 본문**

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
    "createDateTime" : "2025-03-21T15:48:26.451+09:00",
    "expireDateTime" : "2025-03-21T15:48:26.451+09:00",
    "uploadedFileTypes" : [ "EMAIL_DEFAULT" ]
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | 총 첨부 파일 수 |
| attachments | Array | 첨부 파일 목록 |
| attachments[].attachmentId | String | 파일 업로드 성공 시 생성되는 파일 고유 ID |
| attachments[].fileName | String | 업로드 파일명 |
| attachments[].fileFormat | String | 파일 형식 |
| attachments[].fileSizeByte | Long | 첨부 파일의 사이즈 단위는 byte |
| attachments[].createDateTime | String | 파일 업로드 일시 |
| attachments[].expireDateTime | String | 파일 만료 일시 |
| attachments[].uploadedFileTypes | Array | 개별 상품에 업로드된 파일 유형 목록 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 첨부 파일 목록 조회

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

## 첨부 파일 단건 조회

첨부 파일 아이디로 첨부 파일을 조회합니다.


**요청**

```
GET /attachment/v1.0/attachments/{attachmentId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| attachmentId | Path  | String | Y | 첨부 파일 아이디 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.



**응답 본문**

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
    "createDateTime" : "2025-03-21T15:48:26.464+09:00",
    "expireDateTime" : "2025-03-21T15:48:26.464+09:00",
    "uploadedFileTypes" : [ "EMAIL_DEFAULT" ]
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| attachment | Object |  |
| attachment.attachmentId | String | 파일 업로드 성공 시 생성되는 파일 고유 ID |
| attachment.fileName | String | 업로드 파일명 |
| attachment.fileFormat | String | 파일 형식 |
| attachment.previewUrl | String | 파일 미리보기 URL - 만료 시간 존재(상세 조회 호출 시 생성) |
| attachment.fileSizeByte | Long | 첨부 파일의 사이즈 단위는 byte |
| attachment.createDateTime | String | 파일 업로드 일시 |
| attachment.expireDateTime | String | 파일 만료 일시 |
| attachment.uploadedFileTypes | Array | 개별 상품에 업로드된 파일 유형 목록 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 첨부 파일 단건 조회

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

## 업로드 전 첨부 파일 유효성 검사

업로드 할 첨부 파일의 유효성을 검사합니다. 파일 유형, 파일 포맷, 파일 크기, 해상도, 가로 길이, 세로 길이를 통해 설정한 파일 유형의 유효성을 검사합니다. 첨부 파일 업로드 전 파일 유형에 대한 유효성을 검사할 수 있습니다.


**요청**

```
POST /attachment/v1.0/attachments/do-validate
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.



**응답 본문**

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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| results | Array |  |
| results[].isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| results[].resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| results[].resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 업로드 전 첨부 파일 유효성 검사

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

## 업로드된 첨부 파일 유효성 검사

업로드된 첨부 파일에 대해 새로운 파일 유형의 유효성을 검사합니다. 파일 유형 수정 API 호출 전 파일 유형에 대한 유효성을 검사할 수 있습니다.


**요청**

```
POST /attachment/v1.0/attachments/{attachmentId}/do-validate
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| attachmentId | Path  | String | Y | 첨부 파일 아이디 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "fileTypes" : [ "EMAIL_DEFAULT" ]
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| fileTypes | Array | Y | 첨부 파일 유효성 검사를 위한 파일 유형 목록 |



**응답 본문**

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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| results | Array |  |
| results[].isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| results[].resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| results[].resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 업로드된 첨부 파일 유효성 검사

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

## 업로드된 첨부 파일의 파일 유형 수정

업로드된 첨부 파일의 파일 유형을 수정합니다.


**요청**

```
POST /attachment/v1.0/attachments/{attachmentId}/file-types
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| attachmentId | Path  | String | Y | 첨부 파일 아이디 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "fileTypes" : [ "EMAIL_DEFAULT", "SMS_DEFAULT", "EMAIL_TEMPLATE", "SMS_TEMPLATE" ]
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| fileTypes | Array | N | 개별 상품 첨부 파일 업로드 시 지정할 파일 유형 목록, 하나 이상 입력 가능. 템플릿 업로드간 사용시 EMAIL은 EMAIL_TEMPLATE, SMS는 SMS_TEMPLATE로 업로드 요청 필요 |



**응답 본문**

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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| results | Array | 다중 리소스 작업의 결과입니다. |
| results[].isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| results[].resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| results[].resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 업로드된 첨부 파일의 파일 유형 수정

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

## 첨부 파일 유형 목록 조회

지원 중인 첨부 파일 유형의 목록을 조회합니다. 메시지 채널을 설정하면 해당 메시지 채널에서 제공하는 파일 유형 목록을 조회할 수 있습니다.


**요청**

```
GET /attachment/v1.0/attachments/file-types
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageChannel | Query  | V1x0MessageChannel | N | 메시지 채널 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.



**응답 본문**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "fileTypes" : [ "EMAIL_DEFAULT", "SMS_DEFAULT" ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| fileTypes | Array | 파일 유형 목록 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 첨부 파일 유형 목록 조회

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