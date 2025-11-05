<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>템플릿</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 템플릿**



<span id="templateV1x0001CreateSmsTemplate"></span>

## SMS 템플릿 등록

템플릿을 등록합니다.

**요청**

```
POST /template/v1.0/SMS/templates
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

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateName | String | Y | 템플릿 이름 |
| categoryId | String | N | 카테고리 아이디 |
| messagePurpose | String | N | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | Y |  |
| sender.senderPhoneNumber | String | Y | 발신 번호 |
| content | Object | Y |  |
| content.messageType | String | Y | 발송 메시지 유형(SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| content.title | String | N | 메시지 제목 |
| content.body | String | Y | 메시지 본문 |
| content.attachmentIds | Array | N | 첨부 파일 아이디 최대 3개 |
| content.imageLayoutId | String | N | 이미지 레이아웃 아이디 |



**응답 본문**

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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMS 템플릿 등록

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

## SMS 템플릿 리스트 조회

템플릿 리스트를 조회합니다.

**요청**

```
GET /template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateName | Query  | String | N | 템플릿 이름(LIKE 검색) |
| limit | Query  | Integer | N | limit 설정하지 않으면 default 20(최대 1000) |
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
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "배송 완료",
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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | N| 총 건수 |
| templates | Array | N|  |
| templates[].templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | N| 템플릿명 |
| templates[].categoryId | String | N| 카테고리 아이디 |
| templates[].messageChannel | String | N| 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | N| 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array | N|  |
| templates[].createdDateTime | String | N| 템플릿 생성 시각 |
| templates[].updatedDateTime | String | N| 템플릿 수정된 시각 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMS 템플릿 리스트 조회

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

## SMS 템플릿 상세 조회

템플릿을 상세 조회합니다.

**요청**

```
GET /template/v1.0/SMS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



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

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| template | Object | N|  |
| template.templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |
| template.templateName | String | N| 템플릿 이름 |
| template.categoryId | String | N| 카테고리 아이디 |
| template.messageChannel | String | N| 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | N| 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array | N|  |
| template.templateLanguage | String | N| 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object | N|  |
| template.sender.senderPhoneNumber | String | N| 발신 번호 |
| template.content | Object | N|  |
| template.content.messageType | String | N| 발송 메시지 유형(SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| template.content.title | String | N| 메시지 제목 |
| template.content.body | String | N| 메시지 본문 |
| template.content.attachmentIds | Array | N| 첨부 파일 아이디 최대 3개 |
| template.content.imageLayoutId | String | N| 이미지 레이아웃 아이디 |
| template.createdDateTime | String | N| 템플릿 생성 시각 |
| template.updatedDateTime | String | N| 템플릿 수정된 시각 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMS 템플릿 상세 조회

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

## SMS 템플릿 수정

템플릿을 수정합니다.

**요청**

```
PUT /template/v1.0/SMS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "템플릿 이름",
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

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateName | String | Y | 템플릿 이름 |
| messagePurpose | String | N | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.senderPhoneNumber | String | Y | 발신 번호 |
| content | Object | Y |  |
| content.messageType | String | Y | 발송 메시지 유형(SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| content.title | String | N | 메시지 제목 |
| content.body | String | Y | 메시지 본문 |
| content.attachmentIds | Array | N | 첨부 파일 아이디 최대 3개 |
| content.imageLayoutId | String | N | 이미지 레이아웃 아이디 |



**응답 본문**

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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMS 템플릿 수정

PUT {{endpoint}}/template/v1.0/SMS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "템플릿 이름",
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
curl -X PUT "${endpoint}/template/v1.0/SMS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "템플릿 이름",
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
<span id="templateV1x0005DeleteSmsTemplate"></span>

## SMS 템플릿 삭제

템플릿을 삭제합니다.

**요청**

```
DELETE /template/v1.0/SMS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



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
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMS 템플릿 삭제

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

## 알림톡 템플릿 등록

템플릿을 등록합니다.

**요청**

```
POST /template/v1.0/ALIMTALK/templates
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
    "kakaoTemplateCode" : "kakaoTemplateCode",
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
    "status" : "APR",
    "templateModificationStatus" : "APR",
    "block" : false,
    "dormant" : false
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateName | String | Y | 템플릿 이름 |
| categoryId | String | N | 카테고리 아이디 |
| messagePurpose | String | N | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.senderKey | String | N | 발신프로필 발신키 |
| sender.senderProfileType | String | N | 발신프로필 타입<br>[GROUP, NORMAL] |
| content | Object | Y |  |
| content.templateMessageType | String | N | 템플릿 메시지 유형(BA: 기본형, EX: 부가 정보형, AD: 채널 추가형, MI: 복합형, default: BA) |
| content.templateEmphasizeType | String | N | 템플릿 강조 표시 타입(NONE : 기본, TEXT : 강조 표시, IMAGE: 이미지형, ITEM_LIST: 아이템리스트형, default : NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| content.templateContent | String | N | 템플릿 본문 |
| content.templateAd | String | N | 채널 추가 안내 메시지(템플릿 메시지 유형: 채널 추가형, 복합형일 경우 고정값) |
| content.templateExtra | String | N | 템플릿 부가 정보(템플릿 메시지 유형이 [부가 정보형/복합형]일 경우 필수), 치환 변수 사용 불가, URL 포함 가능 |
| content.templateTitle | String | N | 템플릿 제목(최대 50자, Android: 2줄, 23자 이상 말줄임 처리, iOS : 2줄, 27자 이상 말줄임 처리) |
| content.templateSubtitle | String | N | 템플릿 보조 문구(최대 50자, Android: 18자 이상 말줄임 처리, iOS : 21자 이상 말줄임 처리) |
| content.templateHeader | String | N | 템플릿 헤더, 변수 입력 가능 |
| content.templateItem | Object | N |  |
| content.templateItem.list | Array | N |  |
| content.templateItem.list[].title | String | N | 아이템 타이틀 |
| content.templateItem.list[].description | String | N | 아이템 설명 |
| content.templateItem.summary | Object | N |  |
| content.templateItem.summary.title | String | N | 요약 타이틀 |
| content.templateItem.summary.description | String | N | 요약 설명(변수 및 화폐 단위, 숫자, 쉼표, 마침표만 사용 가능) |
| content.templateItemHighlight | Object | N |  |
| content.templateItemHighlight.title | String | N | 아이템 하이라이트 타이틀(최대 30자, 섬네일 이미지가 있을 경우, 21자) |
| content.templateItemHighlight.description | String | N | 아이템 하이라이트 설명(최대 19자, 섬네일 이미지가 있을 경우, 13자) |
| content.templateItemHighlight.attachmentId | String | N | 템플릿 첨부 파일 ID |
| content.templateItemHighlight.imageUrl | String | N | 섬네일 이미지 주소 |
| content.templateRepresentLink | Object | N |  |
| content.templateRepresentLink.linkMo | String | N | 대표 링크 모바일 웹 링크 |
| content.templateRepresentLink.linkPc | String | N | 대표 링크 PC 웹 링크 |
| content.templateRepresentLink.schemeIos | String | N | 대표 링크 iOS 앱 링크 |
| content.templateRepresentLink.schemeAndroid | String | N | 대표 링크 안드로이드 앱 링크 |
| content.attachmentId | String | N | 템플릿 첨부 파일 ID |
| content.templateImageName | String | N | 템플릿 이미지 이름 |
| content.templateImageUrl | String | N | 템플릿 이미지 링크 |
| content.securityFlag | Boolean | N | 템플릿 보안 여부(default: false) |
| content.categoryCode | String | N | 템플릿 카테고리 코드(템플릿 카테고리 조회 API 참고, default: 999999) |
| content.buttons | Array | N | 템플릿 버튼 |
| content.buttons[].ordering | Integer | N | 템플릿 버튼 순서 |
| content.buttons[].type | String | N | 템플릿 버튼 타입(WL: 웹 링크, AL: 앱 링크, DS: 배송 조회, BK: 봇 키워드, MD: 메시지 전달, BC: 상담톡 전환, BT: 봇 전환, AC: 채널 추가, BF: 비지니스폼, P1: 이미지 보안 전송 플러그인 ID, P2: 개인정보이용 플러그인 ID, P3: 원클릭 결제 플러그인 ID, TN: 전화하기)<br>[WL, AL, DS, BK, MD, BC, BT, AC, BF, P1, P2, P3, TN] |
| content.buttons[].name | String | N | 템플릿 버튼 이름 |
| content.buttons[].linkMo | String | N | 템플릿 버튼 모바일 웹 링크 |
| content.buttons[].linkPc | String | N | 템플릿 버튼 PC 웹 링크 |
| content.buttons[].schemeIos | String | N | 템플릿 버튼 iOS 앱 링크 |
| content.buttons[].schemeAndroid | String | N | 템플릿 버튼 안드로이드 앱 링크 |
| content.buttons[].bizFormId | Integer | N | 템플릿 버튼 비즈니스폼 ID(BF 타입일 경우, 필수) |
| content.quickReplies | Array | N | 템플릿 바로 연결 |
| content.quickReplies[].ordering | Integer | N | 템플릿 바로연결 순서 |
| content.quickReplies[].type | String | N | 템플릿 바로연결 타입(WL: 웹 링크, AL: 앱 링크, BK: 봇 키워드, BC: 상담톡 전환, BT: 봇 전환, BF: 비지니스폼)<br>[WL, AL, BK, BC, BT, BF] |
| content.quickReplies[].name | String | N | 템플릿 바로연결 이름 |
| content.quickReplies[].linkMo | String | N | 템플릿 바로연결 모바일 웹 링크 |
| content.quickReplies[].linkPc | String | N | 템플릿 바로연결 PC 웹 링크 |
| content.quickReplies[].schemeIos | String | N | 템플릿 바로연결 iOS 앱 링크 |
| content.quickReplies[].schemeAndroid | String | N | 템플릿 바로연결 안드로이드 앱 링크 |
| content.quickReplies[].bizFormId | Integer | N | 템플릿 바로연결 비즈니스폼 ID(BF 타입일 경우, 필수) |
| additionalProperty | Object | N |  |
| additionalProperty.templateCode | String | N | 템플릿 코드(영문, 숫자, -, _) |
| additionalProperty.kakaoTemplateCode | String | N | 카카오 템플릿 코드 |
| additionalProperty.comments | Array | N | 템플릿 문의 리스트 |
| additionalProperty.comments[].id | Integer | Y | 문의 아이디 |
| additionalProperty.comments[].content | String | N | 문의 내용 |
| additionalProperty.comments[].userName | String | Y | 작성자 |
| additionalProperty.comments[].createdAt | String | Y | 문의 생성 시각 |
| additionalProperty.comments[].attachments | Array | N | 문의 첨부 파일 |
| additionalProperty.comments[].status | String | Y | 문의 상태(REQ: 요청, INQ:문의, APR:승인, REJ:반려, REP: 답변)<br>[REQ, INQ, APR, REJ, REP] |
| additionalProperty.status | String | N | REG:요청, REQ:검수 중, APR:승인, REJ: 반려<br>[REG, REQ, APR, REJ] |
| additionalProperty.templateModificationStatus | String | N | REG:요청, REQ:검수 중, APR:승인, REJ: 반려<br>[REG, REQ, APR, REJ] |
| additionalProperty.block | Boolean | N | 템플릿 차단 여부 |
| additionalProperty.dormant | Boolean | N | 템플릿 휴면 여부 |



**응답 본문**

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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 등록

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
    "kakaoTemplateCode" : "kakaoTemplateCode",
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
    "status" : "APR",
    "templateModificationStatus" : "APR",
    "block" : false,
    "dormant" : false
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
    "kakaoTemplateCode" : "kakaoTemplateCode",
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
    "status" : "APR",
    "templateModificationStatus" : "APR",
    "block" : false,
    "dormant" : false
  }
}'
```

</details>
<span id="templateV1x0007ReadAlimtalkTemplateList"></span>

## 알림톡 템플릿 리스트 조회

템플릿 리스트를 조회합니다.

**요청**

```
GET /template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateName | Query  | String | N | 템플릿 이름(LIKE 검색) |
| senderKey | Query  | String | N | 발신키 |
| templateStatus | Query  | String | N | 템플릿 상태 |
| limit | Query  | Integer | N | limit 설정하지 않으면 default 20(최대 1000) |
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
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "배송 완료",
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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | N| 총 건수 |
| templates | Array | N|  |
| templates[].templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | N| 템플릿명 |
| templates[].categoryId | String | N| 카테고리 아이디 |
| templates[].messageChannel | String | N| 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | N| 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array | N|  |
| templates[].createdDateTime | String | N| 템플릿 생성 시각 |
| templates[].updatedDateTime | String | N| 템플릿 수정된 시각 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 리스트 조회

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

## 알림톡 발신자와 관계된 템플릿 리스트 조회

발신자와 관계된 템플릿 리스트를 조회합니다.(발신자 또는 발신자가 포함된 그룹의 템플릿)

**요청**

```
GET /template/v1.0/ALIMTALK/senders/{senderKey}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| senderKey | Path  | String | Y | 발신키 |
| templateName | Query  | String | N | 템플릿 이름(LIKE 검색) |
| templateStatus | Query  | String | N | 템플릿 상태 |
| limit | Query  | Integer | N | limit 설정하지 않으면 default 20(최대 1000) |
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
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "배송 완료",
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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | N| 총 건수 |
| templates | Array | N|  |
| templates[].templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | N| 템플릿명 |
| templates[].categoryId | String | N| 카테고리 아이디 |
| templates[].messageChannel | String | N| 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | N| 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array | N|  |
| templates[].createdDateTime | String | N| 템플릿 생성 시각 |
| templates[].updatedDateTime | String | N| 템플릿 수정된 시각 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 발신자와 관계된 템플릿 리스트 조회

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

## 알림톡 템플릿 상세 조회

템플릿을 상세 조회합니다.

**요청**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



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
      "templateCode" : "templateCode",
      "kakaoTemplateCode" : "kakaoTemplateCode",
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
      "status" : "APR",
      "templateModificationStatus" : "APR",
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

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| template | Object | N|  |
| template.templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |
| template.templateName | String | N| 템플릿 이름 |
| template.categoryId | String | N| 카테고리 아이디 |
| template.messageChannel | String | N| 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | N| 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array | N|  |
| template.templateLanguage | String | N| 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object | N|  |
| template.sender.senderKey | String | N| 발신프로필 발신키 |
| template.sender.senderProfileId | String | N| 카카오톡 채널명 |
| template.sender.senderProfileType | String | N| 발신프로필 타입<br>[GROUP, NORMAL] |
| template.additionalProperty | Object | N|  |
| template.additionalProperty.templateCode | String | N| 템플릿 코드(영문, 숫자, -, _) |
| template.additionalProperty.kakaoTemplateCode | String | N| 카카오 템플릿 코드 |
| template.additionalProperty.comments | Array | N| 템플릿 문의 리스트 |
| template.additionalProperty.comments[].id | Integer | N| 문의 아이디 |
| template.additionalProperty.comments[].content | String | N| 문의 내용 |
| template.additionalProperty.comments[].userName | String | N| 작성자 |
| template.additionalProperty.comments[].createdAt | String | N| 문의 생성 시각 |
| template.additionalProperty.comments[].attachments | Array | N| 문의 첨부 파일 |
| template.additionalProperty.comments[].status | String | N| 문의 상태(REQ: 요청, INQ:문의, APR:승인, REJ:반려, REP: 답변)<br>[REQ, INQ, APR, REJ, REP] |
| template.additionalProperty.status | String | N| REG:요청, REQ:검수 중, APR:승인, REJ: 반려<br>[REG, REQ, APR, REJ] |
| template.additionalProperty.templateModificationStatus | String | N| REG:요청, REQ:검수 중, APR:승인, REJ: 반려<br>[REG, REQ, APR, REJ] |
| template.additionalProperty.block | Boolean | N| 템플릿 차단 여부 |
| template.additionalProperty.dormant | Boolean | N| 템플릿 휴면 여부 |
| template.content | Object | N|  |
| template.content.templateMessageType | String | N| 템플릿 메시지 유형(BA: 기본형, EX: 부가 정보형, AD: 채널 추가형, MI: 복합형, default: BA) |
| template.content.templateEmphasizeType | String | N| 템플릿 강조 표시 타입(NONE : 기본, TEXT : 강조 표시, IMAGE: 이미지형, ITEM_LIST: 아이템리스트형, default : NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| template.content.templateContent | String | N| 템플릿 본문 |
| template.content.templateAd | String | N| 채널 추가 안내 메시지(템플릿 메시지 유형: 채널 추가형, 복합형일 경우 고정값) |
| template.content.templateExtra | String | N| 템플릿 부가 정보(템플릿 메시지 유형이 [부가 정보형/복합형]일 경우 필수), 치환 변수 사용 불가, URL 포함 가능 |
| template.content.templateTitle | String | N| 템플릿 제목(최대 50자, Android: 2줄, 23자 이상 말줄임 처리, iOS : 2줄, 27자 이상 말줄임 처리) |
| template.content.templateSubtitle | String | N| 템플릿 보조 문구(최대 50자, Android: 18자 이상 말줄임 처리, iOS : 21자 이상 말줄임 처리) |
| template.content.templateHeader | String | N| 템플릿 헤더, 변수 입력 가능 |
| template.content.templateItem | Object | N|  |
| template.content.templateItem.list | Array | N|  |
| template.content.templateItem.list[].title | String | N| 아이템 타이틀 |
| template.content.templateItem.list[].description | String | N| 아이템 설명 |
| template.content.templateItem.summary | Object | N|  |
| template.content.templateItem.summary.title | String | N| 요약 타이틀 |
| template.content.templateItem.summary.description | String | N| 요약 설명(변수 및 화폐 단위, 숫자, 쉼표, 마침표만 사용 가능) |
| template.content.templateItemHighlight | Object | N|  |
| template.content.templateItemHighlight.title | String | N| 아이템 하이라이트 타이틀(최대 30자, 섬네일 이미지가 있을 경우, 21자) |
| template.content.templateItemHighlight.description | String | N| 아이템 하이라이트 설명(최대 19자, 섬네일 이미지가 있을 경우, 13자) |
| template.content.templateItemHighlight.attachmentId | String | N| 템플릿 첨부 파일 ID |
| template.content.templateItemHighlight.imageUrl | String | N| 섬네일 이미지 주소 |
| template.content.templateRepresentLink | Object | N|  |
| template.content.templateRepresentLink.linkMo | String | N| 대표 링크 모바일 웹 링크 |
| template.content.templateRepresentLink.linkPc | String | N| 대표 링크 PC 웹 링크 |
| template.content.templateRepresentLink.schemeIos | String | N| 대표 링크 iOS 앱 링크 |
| template.content.templateRepresentLink.schemeAndroid | String | N| 대표 링크 안드로이드 앱 링크 |
| template.content.attachmentId | String | N| 템플릿 첨부 파일 ID |
| template.content.templateImageName | String | N| 템플릿 이미지 이름 |
| template.content.templateImageUrl | String | N| 템플릿 이미지 링크 |
| template.content.securityFlag | Boolean | N| 템플릿 보안 여부(default: false) |
| template.content.categoryCode | String | N| 템플릿 카테고리 코드(템플릿 카테고리 조회 API 참고, default: 999999) |
| template.content.buttons | Array | N| 템플릿 버튼 |
| template.content.buttons[].ordering | Integer | N| 템플릿 버튼 순서 |
| template.content.buttons[].type | String | N| 템플릿 버튼 타입(WL: 웹 링크, AL: 앱 링크, DS: 배송 조회, BK: 봇 키워드, MD: 메시지 전달, BC: 상담톡 전환, BT: 봇 전환, AC: 채널 추가, BF: 비지니스폼, P1: 이미지 보안 전송 플러그인 ID, P2: 개인정보이용 플러그인 ID, P3: 원클릭 결제 플러그인 ID, TN: 전화하기)<br>[WL, AL, DS, BK, MD, BC, BT, AC, BF, P1, P2, P3, TN] |
| template.content.buttons[].name | String | N| 템플릿 버튼 이름 |
| template.content.buttons[].linkMo | String | N| 템플릿 버튼 모바일 웹 링크 |
| template.content.buttons[].linkPc | String | N| 템플릿 버튼 PC 웹 링크 |
| template.content.buttons[].schemeIos | String | N| 템플릿 버튼 iOS 앱 링크 |
| template.content.buttons[].schemeAndroid | String | N| 템플릿 버튼 안드로이드 앱 링크 |
| template.content.buttons[].bizFormId | Integer | N| 템플릿 버튼 비즈니스폼 ID(BF 타입일 경우, 필수) |
| template.content.quickReplies | Array | N| 템플릿 바로 연결 |
| template.content.quickReplies[].ordering | Integer | N| 템플릿 바로연결 순서 |
| template.content.quickReplies[].type | String | N| 템플릿 바로연결 타입(WL: 웹 링크, AL: 앱 링크, BK: 봇 키워드, BC: 상담톡 전환, BT: 봇 전환, BF: 비지니스폼)<br>[WL, AL, BK, BC, BT, BF] |
| template.content.quickReplies[].name | String | N| 템플릿 바로연결 이름 |
| template.content.quickReplies[].linkMo | String | N| 템플릿 바로연결 모바일 웹 링크 |
| template.content.quickReplies[].linkPc | String | N| 템플릿 바로연결 PC 웹 링크 |
| template.content.quickReplies[].schemeIos | String | N| 템플릿 바로연결 iOS 앱 링크 |
| template.content.quickReplies[].schemeAndroid | String | N| 템플릿 바로연결 안드로이드 앱 링크 |
| template.content.quickReplies[].bizFormId | Integer | N| 템플릿 바로연결 비즈니스폼 ID(BF 타입일 경우, 필수) |
| template.createdDateTime | String | N| 템플릿 생성 시각 |
| template.updatedDateTime | String | N| 템플릿 수정된 시각 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 상세 조회

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

## 알림톡 템플릿 수정

템플릿을 수정합니다.

**요청**

```
PUT /template/v1.0/ALIMTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "템플릿 이름",
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
    "templateCode" : "templateCode"
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateName | String | Y | 템플릿 이름 |
| messagePurpose | String | N | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.senderKey | String | N | 발신프로필 발신키 |
| sender.senderProfileType | String | N | 발신프로필 타입<br>[GROUP, NORMAL] |
| content | Object | Y |  |
| content.templateMessageType | String | N | 템플릿 메시지 유형(BA: 기본형, EX: 부가 정보형, AD: 채널 추가형, MI: 복합형, default: BA) |
| content.templateEmphasizeType | String | N | 템플릿 강조 표시 타입(NONE : 기본, TEXT : 강조 표시, IMAGE: 이미지형, ITEM_LIST: 아이템리스트형, default : NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| content.templateContent | String | N | 템플릿 본문 |
| content.templateAd | String | N | 채널 추가 안내 메시지(템플릿 메시지 유형: 채널 추가형, 복합형일 경우 고정값) |
| content.templateExtra | String | N | 템플릿 부가 정보(템플릿 메시지 유형이 [부가 정보형/복합형]일 경우 필수), 치환 변수 사용 불가, URL 포함 가능 |
| content.templateTitle | String | N | 템플릿 제목(최대 50자, Android: 2줄, 23자 이상 말줄임 처리, iOS : 2줄, 27자 이상 말줄임 처리) |
| content.templateSubtitle | String | N | 템플릿 보조 문구(최대 50자, Android: 18자 이상 말줄임 처리, iOS : 21자 이상 말줄임 처리) |
| content.templateHeader | String | N | 템플릿 헤더, 변수 입력 가능 |
| content.templateItem | Object | N |  |
| content.templateItem.list | Array | N |  |
| content.templateItem.list[].title | String | N | 아이템 타이틀 |
| content.templateItem.list[].description | String | N | 아이템 설명 |
| content.templateItem.summary | Object | N |  |
| content.templateItem.summary.title | String | N | 요약 타이틀 |
| content.templateItem.summary.description | String | N | 요약 설명(변수 및 화폐 단위, 숫자, 쉼표, 마침표만 사용 가능) |
| content.templateItemHighlight | Object | N |  |
| content.templateItemHighlight.title | String | N | 아이템 하이라이트 타이틀(최대 30자, 섬네일 이미지가 있을 경우, 21자) |
| content.templateItemHighlight.description | String | N | 아이템 하이라이트 설명(최대 19자, 섬네일 이미지가 있을 경우, 13자) |
| content.templateItemHighlight.attachmentId | String | N | 템플릿 첨부 파일 ID |
| content.templateItemHighlight.imageUrl | String | N | 섬네일 이미지 주소 |
| content.templateRepresentLink | Object | N |  |
| content.templateRepresentLink.linkMo | String | N | 대표 링크 모바일 웹 링크 |
| content.templateRepresentLink.linkPc | String | N | 대표 링크 PC 웹 링크 |
| content.templateRepresentLink.schemeIos | String | N | 대표 링크 iOS 앱 링크 |
| content.templateRepresentLink.schemeAndroid | String | N | 대표 링크 안드로이드 앱 링크 |
| content.attachmentId | String | N | 템플릿 첨부 파일 ID |
| content.templateImageName | String | N | 템플릿 이미지 이름 |
| content.templateImageUrl | String | N | 템플릿 이미지 링크 |
| content.securityFlag | Boolean | N | 템플릿 보안 여부(default: false) |
| content.categoryCode | String | N | 템플릿 카테고리 코드(템플릿 카테고리 조회 API 참고, default: 999999) |
| content.buttons | Array | N | 템플릿 버튼 |
| content.buttons[].ordering | Integer | N | 템플릿 버튼 순서 |
| content.buttons[].type | String | N | 템플릿 버튼 타입(WL: 웹 링크, AL: 앱 링크, DS: 배송 조회, BK: 봇 키워드, MD: 메시지 전달, BC: 상담톡 전환, BT: 봇 전환, AC: 채널 추가, BF: 비지니스폼, P1: 이미지 보안 전송 플러그인 ID, P2: 개인정보이용 플러그인 ID, P3: 원클릭 결제 플러그인 ID, TN: 전화하기)<br>[WL, AL, DS, BK, MD, BC, BT, AC, BF, P1, P2, P3, TN] |
| content.buttons[].name | String | N | 템플릿 버튼 이름 |
| content.buttons[].linkMo | String | N | 템플릿 버튼 모바일 웹 링크 |
| content.buttons[].linkPc | String | N | 템플릿 버튼 PC 웹 링크 |
| content.buttons[].schemeIos | String | N | 템플릿 버튼 iOS 앱 링크 |
| content.buttons[].schemeAndroid | String | N | 템플릿 버튼 안드로이드 앱 링크 |
| content.buttons[].bizFormId | Integer | N | 템플릿 버튼 비즈니스폼 ID(BF 타입일 경우, 필수) |
| content.quickReplies | Array | N | 템플릿 바로 연결 |
| content.quickReplies[].ordering | Integer | N | 템플릿 바로연결 순서 |
| content.quickReplies[].type | String | N | 템플릿 바로연결 타입(WL: 웹 링크, AL: 앱 링크, BK: 봇 키워드, BC: 상담톡 전환, BT: 봇 전환, BF: 비지니스폼)<br>[WL, AL, BK, BC, BT, BF] |
| content.quickReplies[].name | String | N | 템플릿 바로연결 이름 |
| content.quickReplies[].linkMo | String | N | 템플릿 바로연결 모바일 웹 링크 |
| content.quickReplies[].linkPc | String | N | 템플릿 바로연결 PC 웹 링크 |
| content.quickReplies[].schemeIos | String | N | 템플릿 바로연결 iOS 앱 링크 |
| content.quickReplies[].schemeAndroid | String | N | 템플릿 바로연결 안드로이드 앱 링크 |
| content.quickReplies[].bizFormId | Integer | N | 템플릿 바로연결 비즈니스폼 ID(BF 타입일 경우, 필수) |
| additionalProperty | Object | N |  |
| additionalProperty.templateCode | String | N | 템플릿 코드(영문, 숫자, -, _) |



**응답 본문**

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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 수정

PUT {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "템플릿 이름",
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
    "templateCode" : "templateCode"
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
  "templateName" : "템플릿 이름",
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
    "templateCode" : "templateCode"
  }
}'
```

</details>
<span id="templateV1x0011DeleteAlimtalkTemplate"></span>

## 알림톡 템플릿 삭제

템플릿을 삭제합니다.

**요청**

```
DELETE /template/v1.0/ALIMTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



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
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 삭제

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

## 알림톡 템플릿 문의하기

알림톡 템플릿을 문의합니다.

**요청**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/inquiries
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "comment" : "문의 내용 예시"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| comment | String | Y | 문의 내용 |



**응답 본문**

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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 문의하기

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/inquiries
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "comment" : "문의 내용 예시"
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
  "comment" : "문의 내용 예시"
}'
```

</details>
<span id="templateV1x0013InquireAlimtalkTemplateWithFile"></span>

## 알림톡 템플릿 문의하기(파일 첨부)

알림톡 템플릿을 문의할 때 파일을 첨부해 문의합니다.

**요청**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/inquiries/do-with-file
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |
| attachments | Form  | List | Y | 문의 파일 |
| comment | Form  | String | Y | 문의 내용 |



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
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 문의하기(파일 첨부)

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/inquiries/do-with-file
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
comment=comment_example
attachments=@/path/to/file.txt
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/inquiries/do-with-file" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-F "comment=comment_example" \
-F "attachments=@/path/to/file.txt"
```

</details>
<span id="templateV1x0014ReadAlimtalkTemplateModifications"></span>

## 알림톡 템플릿 수정 리스트 조회

알림톡 템플릿 수정 리스트를 조회합니다.

**요청**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}/modifications
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |
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
  "totalCount" : 1,
  "templates" : [ {
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
      "templateCode" : "templateCode",
      "kakaoTemplateCode" : "kakaoTemplateCode",
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
      "status" : "APR",
      "block" : false,
      "dormant" : false,
      "activated" : false
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
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | N| 총 건수 |
| templates | Array | N|  |
| templates[].templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | N| 템플릿 이름 |
| templates[].categoryId | String | N| 카테고리 아이디 |
| templates[].messageChannel | String | N| 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | N| 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array | N|  |
| templates[].templateLanguage | String | N| 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| templates[].sender | Object | N|  |
| templates[].sender.senderKey | String | N| 발신프로필 발신키 |
| templates[].sender.senderProfileId | String | N| 카카오톡 채널명 |
| templates[].sender.senderProfileType | String | N| 발신프로필 타입<br>[GROUP, NORMAL] |
| templates[].additionalProperty | Object | N|  |
| templates[].additionalProperty.templateCode | String | N| 템플릿 코드(영문, 숫자, -, _) |
| templates[].additionalProperty.kakaoTemplateCode | String | N| 카카오 템플릿 코드 |
| templates[].additionalProperty.comments | Array | N| 템플릿 문의 리스트 |
| templates[].additionalProperty.status | String | N| REG:요청, REQ:검수 중, APR:승인, REJ: 반려<br>[REG, REQ, APR, REJ] |
| templates[].additionalProperty.block | Boolean | N| 템플릿 차단 여부 |
| templates[].additionalProperty.dormant | Boolean | N| 템플릿 휴면 여부 |
| templates[].additionalProperty.activated | Boolean | N| 활성화 여부 |
| templates[].content | Object | N|  |
| templates[].content.templateMessageType | String | N| 템플릿 메시지 유형(BA: 기본형, EX: 부가 정보형, AD: 채널 추가형, MI: 복합형, default: BA) |
| templates[].content.templateEmphasizeType | String | N| 템플릿 강조 표시 타입(NONE : 기본, TEXT : 강조 표시, IMAGE: 이미지형, ITEM_LIST: 아이템리스트형, default : NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| templates[].content.templateContent | String | N| 템플릿 본문 |
| templates[].content.templateAd | String | N| 채널 추가 안내 메시지(템플릿 메시지 유형: 채널 추가형, 복합형일 경우 고정값) |
| templates[].content.templateExtra | String | N| 템플릿 부가 정보(템플릿 메시지 유형이 [부가 정보형/복합형]일 경우 필수), 치환 변수 사용 불가, URL 포함 가능 |
| templates[].content.templateTitle | String | N| 템플릿 제목(최대 50자, Android: 2줄, 23자 이상 말줄임 처리, iOS : 2줄, 27자 이상 말줄임 처리) |
| templates[].content.templateSubtitle | String | N| 템플릿 보조 문구(최대 50자, Android: 18자 이상 말줄임 처리, iOS : 21자 이상 말줄임 처리) |
| templates[].content.templateHeader | String | N| 템플릿 헤더, 변수 입력 가능 |
| templates[].content.templateItem | Object | N|  |
| templates[].content.templateItem.list | Array | N|  |
| templates[].content.templateItem.summary | Object | N|  |
| templates[].content.templateItem.summary.title | String | N| 요약 타이틀 |
| templates[].content.templateItem.summary.description | String | N| 요약 설명(변수 및 화폐 단위, 숫자, 쉼표, 마침표만 사용 가능) |
| templates[].content.templateItemHighlight | Object | N|  |
| templates[].content.templateItemHighlight.title | String | N| 아이템 하이라이트 타이틀(최대 30자, 섬네일 이미지가 있을 경우, 21자) |
| templates[].content.templateItemHighlight.description | String | N| 아이템 하이라이트 설명(최대 19자, 섬네일 이미지가 있을 경우, 13자) |
| templates[].content.templateItemHighlight.attachmentId | String | N| 템플릿 첨부 파일 ID |
| templates[].content.templateItemHighlight.imageUrl | String | N| 섬네일 이미지 주소 |
| templates[].content.templateRepresentLink | Object | N|  |
| templates[].content.templateRepresentLink.linkMo | String | N| 대표 링크 모바일 웹 링크 |
| templates[].content.templateRepresentLink.linkPc | String | N| 대표 링크 PC 웹 링크 |
| templates[].content.templateRepresentLink.schemeIos | String | N| 대표 링크 iOS 앱 링크 |
| templates[].content.templateRepresentLink.schemeAndroid | String | N| 대표 링크 안드로이드 앱 링크 |
| templates[].content.attachmentId | String | N| 템플릿 첨부 파일 ID |
| templates[].content.templateImageName | String | N| 템플릿 이미지 이름 |
| templates[].content.templateImageUrl | String | N| 템플릿 이미지 링크 |
| templates[].content.securityFlag | Boolean | N| 템플릿 보안 여부(default: false) |
| templates[].content.categoryCode | String | N| 템플릿 카테고리 코드(템플릿 카테고리 조회 API 참고, default: 999999) |
| templates[].content.buttons | Array | N| 템플릿 버튼 |
| templates[].content.quickReplies | Array | N| 템플릿 바로 연결 |
| templates[].createdDateTime | String | N| 템플릿 생성 시각 |
| templates[].updatedDateTime | String | N| 템플릿 수정된 시각 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 수정 리스트 조회

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

## 알림톡 템플릿 카테고리 리스트 조회

알림톡 템플릿 카테고리 리스트를 조회합니다.

**요청**

```
GET /template/v1.0/ALIMTALK/template-categories
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
  "categories" : [ {
    "name" : "구매",
    "subCategories" : [ {
      "code" : "002001",
      "name" : "구매완료",
      "groupName" : "구매",
      "inclusion" : "주문완료, 구매완료 템플릿이 대상입니다.",
      "exclusion" : "일정관련 되어 예약, 예약번호가 있는 템플릿의 경우 구매완료에서 제외하고 예약으로 분류합니다."
    } ]
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| categories | Array | N|  |
| categories[].name | String | N| 대분류 카테고리 이름 |
| categories[].subCategories | Array | N| 서브 카테고리 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 카테고리 리스트 조회

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
<span id="templateV1x0016CreateFriendtalkTemplate"></span>

## 친구톡 템플릿 등록

템플릿을 등록합니다.

**요청**

```
POST /template/v1.0/FRIENDTALK/templates
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


```
{
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "content" : {
    "messageType" : "TEXT",
    "content" : null,
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "imageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "imageLink" : "https://www.naver.com",
    "buttons" : [ {
      "type" : "WL",
      "name" : "Button Name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123"
    } ],
    "header" : "헤더",
    "item" : {
      "list" : [ {
        "title" : "Item Title",
        "attachmentId" : "20230131070811m2fDe1rXx80",
        "imageUrl" : "https://example.com/image.jpg",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "carousel" : {
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "attachment" : {
          "buttons" : [ {
            "schemeAndroid" : "example://android",
            "name" : "Button Name",
            "linkMo" : "https://m.example.com",
            "schemeIos" : "example://ios",
            "linkPc" : "https://www.example.com",
            "type" : "WL",
            "bizFormKey" : "bizFormKey123",
            "target" : "out"
          } ],
          "image" : {
            "attachmentId" : "20230131070811m2fDe1rXx80",
            "imageUrl" : "https://example.com/image.jpg",
            "imageLink" : "https://www.example.com"
          }
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "coupon" : {
      "title" : "Coupon Title",
      "description" : "Coupon Description",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    }
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateName | String | Y | 템플릿 이름 |
| categoryId | String | N | 카테고리 아이디 |
| messagePurpose | String | N | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | Y |  |
| sender.senderKey | String | N | 발신프로필 발신키 |
| content | Object | N |  |
| content.messageType | String | N | 템플릿 메시지 유형(TEXT: 텍스트형, IMAGE: 이미지형, WIDE_IMAGE: 와이드 이미지형, WIDE_ITEMLIST: 와이드아이템리스트형, CAROUSEL_FEED: 캐러셀피드형, default: TEXT) |
| content.content | String | N | 템플릿 본문 |
| content.attachmentId | String | N | 첨부 파일 아이디 |
| content.imageUrl | String | N | 템플릿 이미지 URL |
| content.imageLink | String | N | 템플릿 이미지 링크 |
| content.buttons | Array | N | 템플릿 버튼 |
| content.buttons[].type | String | N | 템플릿 버튼 타입(WL: 웹 링크, AL: 앱 링크, BK: 봇 키워드, MD: 메시지 전달, BF: 비지니스폼)<br>[WL, AL, BK, MD, BF] |
| content.buttons[].name | String | N | 템플릿 버튼 이름 |
| content.buttons[].linkMo | String | N | 템플릿 버튼 모바일 웹 링크 |
| content.buttons[].linkPc | String | N | 템플릿 버튼 PC 웹 링크 |
| content.buttons[].schemeIos | String | N | 템플릿 버튼 iOS 앱 링크 |
| content.buttons[].schemeAndroid | String | N | 템플릿 버튼 안드로이드 앱 링크 |
| content.buttons[].bizFormKey | String | N | BF(비즈니스 폼) 타입 버튼 시, 비즈폼 키 |
| content.header | String | N | 헤더(와이드 아이템리스트 메시지 타입 사용 시, 필수, 최대 25자) |
| content.item | Object | N |  |
| content.item.list | Array | N |  |
| content.item.list[].title | String | N | 아이템 타이틀 첫번째 아이템 25자, 2~4번째 30자 |
| content.item.list[].attachmentId | String | N | 첨부 파일 아이디 |
| content.item.list[].imageUrl | String | N | 아이템 이미지 URL |
| content.item.list[].linkMo | String | N | 대표 링크 모바일 웹 링크 |
| content.item.list[].linkPc | String | N | 대표 링크 PC 웹 링크 |
| content.item.list[].schemeIos | String | N | 대표 링크 iOS 앱 링크 |
| content.item.list[].schemeAndroid | String | N | 대표 링크 안드로이드 앱 링크 |
| content.carousel | Object | N |  |
| content.carousel.list | Array | N |  |
| content.carousel.list[].header | String | N | 캐러셀 아이템 제목 |
| content.carousel.list[].message | String | N | 캐러셀 아이템 메시지 |
| content.carousel.list[].attachment | Object | N |  |
| content.carousel.list[].attachment.buttons | Array | N |  |
| content.carousel.list[].attachment.image | Object | N |  |
| content.carousel.list[].attachment.image.attachmentId | String | N | 첨부 파일 아이디 |
| content.carousel.list[].attachment.image.imageUrl | String | N | 캐러셀 아이템 이미지 URL |
| content.carousel.list[].attachment.image.imageLink | String | N | 캐러셀 아이템 이미지 링크 |
| content.carousel.tail | Object | N |  |
| content.carousel.tail.linkMo | String | N | 대표 링크 모바일 웹 링크 |
| content.carousel.tail.linkPc | String | N | 대표 링크 PC 웹 링크 |
| content.carousel.tail.schemeIos | String | N | 대표 링크 iOS 앱 링크 |
| content.carousel.tail.schemeAndroid | String | N | 대표 링크 안드로이드 앱 링크 |
| content.coupon | Object | N |  |
| content.coupon.title | String | N | 쿠폰 이름 |
| content.coupon.description | String | N | 쿠폰 상세 설명(일반 텍스트, 이미지형 최대 12자 / 와이드 이미지형, 와이드 아이템리스트형 최대 18자) |
| content.coupon.linkMo | String | N | 대표 링크 모바일 웹 링크 |
| content.coupon.linkPc | String | N | 대표 링크 PC 웹 링크 |
| content.coupon.schemeIos | String | N | 대표 링크 iOS 앱 링크 |
| content.coupon.schemeAndroid | String | N | 대표 링크 안드로이드 앱 링크 |



**응답 본문**

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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 친구톡 템플릿 등록

POST {{endpoint}}/template/v1.0/FRIENDTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "content" : {
    "messageType" : "TEXT",
    "content" : null,
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "imageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "imageLink" : "https://www.naver.com",
    "buttons" : [ {
      "type" : "WL",
      "name" : "Button Name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123"
    } ],
    "header" : "헤더",
    "item" : {
      "list" : [ {
        "title" : "Item Title",
        "attachmentId" : "20230131070811m2fDe1rXx80",
        "imageUrl" : "https://example.com/image.jpg",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "carousel" : {
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "attachment" : {
          "buttons" : [ {
            "schemeAndroid" : "example://android",
            "name" : "Button Name",
            "linkMo" : "https://m.example.com",
            "schemeIos" : "example://ios",
            "linkPc" : "https://www.example.com",
            "type" : "WL",
            "bizFormKey" : "bizFormKey123",
            "target" : "out"
          } ],
          "image" : {
            "attachmentId" : "20230131070811m2fDe1rXx80",
            "imageUrl" : "https://example.com/image.jpg",
            "imageLink" : "https://www.example.com"
          }
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "coupon" : {
      "title" : "Coupon Title",
      "description" : "Coupon Description",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    }
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/FRIENDTALK/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "content" : {
    "messageType" : "TEXT",
    "content" : null,
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "imageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "imageLink" : "https://www.naver.com",
    "buttons" : [ {
      "type" : "WL",
      "name" : "Button Name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123"
    } ],
    "header" : "헤더",
    "item" : {
      "list" : [ {
        "title" : "Item Title",
        "attachmentId" : "20230131070811m2fDe1rXx80",
        "imageUrl" : "https://example.com/image.jpg",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "carousel" : {
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "attachment" : {
          "buttons" : [ {
            "schemeAndroid" : "example://android",
            "name" : "Button Name",
            "linkMo" : "https://m.example.com",
            "schemeIos" : "example://ios",
            "linkPc" : "https://www.example.com",
            "type" : "WL",
            "bizFormKey" : "bizFormKey123",
            "target" : "out"
          } ],
          "image" : {
            "attachmentId" : "20230131070811m2fDe1rXx80",
            "imageUrl" : "https://example.com/image.jpg",
            "imageLink" : "https://www.example.com"
          }
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "coupon" : {
      "title" : "Coupon Title",
      "description" : "Coupon Description",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    }
  }
}'
```

</details>
<span id="templateV1x0017ReadFriendtalkTemplateList"></span>

## 친구톡 템플릿 리스트 조회

템플릿 리스트를 조회합니다.

**요청**

```
GET /template/v1.0/FRIENDTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateName | Query  | String | N | 템플릿 이름(LIKE 검색) |
| senderKey | Query  | String | N | 발신키 |
| limit | Query  | Integer | N | limit 설정하지 않으면 default 20(최대 1000) |
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
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "배송 완료",
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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | N| 총 건수 |
| templates | Array | N|  |
| templates[].templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | N| 템플릿명 |
| templates[].categoryId | String | N| 카테고리 아이디 |
| templates[].messageChannel | String | N| 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | N| 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array | N|  |
| templates[].createdDateTime | String | N| 템플릿 생성 시각 |
| templates[].updatedDateTime | String | N| 템플릿 수정된 시각 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 친구톡 템플릿 리스트 조회

GET {{endpoint}}/template/v1.0/FRIENDTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/FRIENDTALK/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
<span id="templateV1x0018ReadFriendtalkTemplate"></span>

## 친구톡 템플릿 상세 조회

템플릿을 상세 조회합니다.

**요청**

```
GET /template/v1.0/FRIENDTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



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
      "senderProfileId" : "@nhnCloud"
    },
    "content" : {
      "messageType" : "TEXT",
      "content" : null,
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
      "imageLink" : "https://www.naver.com",
      "buttons" : [ {
        "type" : "WL",
        "name" : "Button Name",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormKey" : "bizFormKey123"
      } ],
      "header" : "헤더",
      "item" : {
        "list" : [ {
          "title" : "Item Title",
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        } ]
      },
      "carousel" : {
        "list" : [ {
          "header" : "Carousel Header",
          "message" : "Carousel Message",
          "attachment" : {
            "buttons" : [ {
              "schemeAndroid" : "example://android",
              "name" : "Button Name",
              "linkMo" : "https://m.example.com",
              "schemeIos" : "example://ios",
              "linkPc" : "https://www.example.com",
              "type" : "WL",
              "bizFormKey" : "bizFormKey123",
              "target" : "out"
            } ],
            "image" : {
              "attachmentId" : "20230131070811m2fDe1rXx80",
              "imageUrl" : "https://example.com/image.jpg",
              "imageLink" : "https://www.example.com"
            }
          }
        } ],
        "tail" : {
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        }
      },
      "coupon" : {
        "title" : "Coupon Title",
        "description" : "Coupon Description",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| template | Object | N|  |
| template.templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |
| template.templateName | String | N| 템플릿 이름 |
| template.categoryId | String | N| 카테고리 아이디 |
| template.messageChannel | String | N| 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | N| 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array | N|  |
| template.templateLanguage | String | N| 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object | N|  |
| template.sender.senderKey | String | N| 발신프로필 발신키 |
| template.sender.senderProfileId | String | N| 카카오톡 채널명 |
| template.content | Object | N|  |
| template.content.messageType | String | N| 템플릿 메시지 유형(TEXT: 텍스트형, IMAGE: 이미지형, WIDE_IMAGE: 와이드 이미지형, WIDE_ITEMLIST: 와이드아이템리스트형, CAROUSEL_FEED: 캐러셀피드형, default: TEXT) |
| template.content.content | String | N| 템플릿 본문 |
| template.content.attachmentId | String | N| 첨부 파일 아이디 |
| template.content.imageUrl | String | N| 템플릿 이미지 URL |
| template.content.imageLink | String | N| 템플릿 이미지 링크 |
| template.content.buttons | Array | N| 템플릿 버튼 |
| template.content.buttons[].type | String | N| 템플릿 버튼 타입(WL: 웹 링크, AL: 앱 링크, BK: 봇 키워드, MD: 메시지 전달, BF: 비지니스폼)<br>[WL, AL, BK, MD, BF] |
| template.content.buttons[].name | String | N| 템플릿 버튼 이름 |
| template.content.buttons[].linkMo | String | N| 템플릿 버튼 모바일 웹 링크 |
| template.content.buttons[].linkPc | String | N| 템플릿 버튼 PC 웹 링크 |
| template.content.buttons[].schemeIos | String | N| 템플릿 버튼 iOS 앱 링크 |
| template.content.buttons[].schemeAndroid | String | N| 템플릿 버튼 안드로이드 앱 링크 |
| template.content.buttons[].bizFormKey | String | N| BF(비즈니스 폼) 타입 버튼 시, 비즈폼 키 |
| template.content.header | String | N| 헤더(와이드 아이템리스트 메시지 타입 사용 시, 필수, 최대 25자) |
| template.content.item | Object | N|  |
| template.content.item.list | Array | N|  |
| template.content.item.list[].title | String | N| 아이템 타이틀 첫번째 아이템 25자, 2~4번째 30자 |
| template.content.item.list[].attachmentId | String | N| 첨부 파일 아이디 |
| template.content.item.list[].imageUrl | String | N| 아이템 이미지 URL |
| template.content.item.list[].linkMo | String | N| 대표 링크 모바일 웹 링크 |
| template.content.item.list[].linkPc | String | N| 대표 링크 PC 웹 링크 |
| template.content.item.list[].schemeIos | String | N| 대표 링크 iOS 앱 링크 |
| template.content.item.list[].schemeAndroid | String | N| 대표 링크 안드로이드 앱 링크 |
| template.content.carousel | Object | N|  |
| template.content.carousel.list | Array | N|  |
| template.content.carousel.list[].header | String | N| 캐러셀 아이템 제목 |
| template.content.carousel.list[].message | String | N| 캐러셀 아이템 메시지 |
| template.content.carousel.list[].attachment | Object | N|  |
| template.content.carousel.list[].attachment.buttons | Array | N|  |
| template.content.carousel.list[].attachment.image | Object | N|  |
| template.content.carousel.list[].attachment.image.attachmentId | String | N| 첨부 파일 아이디 |
| template.content.carousel.list[].attachment.image.imageUrl | String | N| 캐러셀 아이템 이미지 URL |
| template.content.carousel.list[].attachment.image.imageLink | String | N| 캐러셀 아이템 이미지 링크 |
| template.content.carousel.tail | Object | N|  |
| template.content.carousel.tail.linkMo | String | N| 대표 링크 모바일 웹 링크 |
| template.content.carousel.tail.linkPc | String | N| 대표 링크 PC 웹 링크 |
| template.content.carousel.tail.schemeIos | String | N| 대표 링크 iOS 앱 링크 |
| template.content.carousel.tail.schemeAndroid | String | N| 대표 링크 안드로이드 앱 링크 |
| template.content.coupon | Object | N|  |
| template.content.coupon.title | String | N| 쿠폰 이름 |
| template.content.coupon.description | String | N| 쿠폰 상세 설명(일반 텍스트, 이미지형 최대 12자 / 와이드 이미지형, 와이드 아이템리스트형 최대 18자) |
| template.content.coupon.linkMo | String | N| 대표 링크 모바일 웹 링크 |
| template.content.coupon.linkPc | String | N| 대표 링크 PC 웹 링크 |
| template.content.coupon.schemeIos | String | N| 대표 링크 iOS 앱 링크 |
| template.content.coupon.schemeAndroid | String | N| 대표 링크 안드로이드 앱 링크 |
| template.createdDateTime | String | N| 템플릿 생성 시각 |
| template.updatedDateTime | String | N| 템플릿 수정된 시각 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 친구톡 템플릿 상세 조회

GET {{endpoint}}/template/v1.0/FRIENDTALK/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/FRIENDTALK/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
<span id="templateV1x0019UpdateFriendtalkTemplate"></span>

## 친구톡 템플릿 수정

템플릿을 수정합니다.

**요청**

```
PUT /template/v1.0/FRIENDTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "템플릿 이름",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "content" : {
    "messageType" : "TEXT",
    "content" : null,
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "imageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "imageLink" : "https://www.naver.com",
    "buttons" : [ {
      "type" : "WL",
      "name" : "Button Name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123"
    } ],
    "header" : "헤더",
    "item" : {
      "list" : [ {
        "title" : "Item Title",
        "attachmentId" : "20230131070811m2fDe1rXx80",
        "imageUrl" : "https://example.com/image.jpg",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "carousel" : {
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "attachment" : {
          "buttons" : [ {
            "schemeAndroid" : "example://android",
            "name" : "Button Name",
            "linkMo" : "https://m.example.com",
            "schemeIos" : "example://ios",
            "linkPc" : "https://www.example.com",
            "type" : "WL",
            "bizFormKey" : "bizFormKey123",
            "target" : "out"
          } ],
          "image" : {
            "attachmentId" : "20230131070811m2fDe1rXx80",
            "imageUrl" : "https://example.com/image.jpg",
            "imageLink" : "https://www.example.com"
          }
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "coupon" : {
      "title" : "Coupon Title",
      "description" : "Coupon Description",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    }
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateName | String | Y | 템플릿 이름 |
| messagePurpose | String | N | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.senderKey | String | N | 발신프로필 발신키 |
| content | Object | Y |  |
| content.messageType | String | N | 템플릿 메시지 유형(TEXT: 텍스트형, IMAGE: 이미지형, WIDE_IMAGE: 와이드 이미지형, WIDE_ITEMLIST: 와이드아이템리스트형, CAROUSEL_FEED: 캐러셀피드형, default: TEXT) |
| content.content | String | N | 템플릿 본문 |
| content.attachmentId | String | N | 첨부 파일 아이디 |
| content.imageUrl | String | N | 템플릿 이미지 URL |
| content.imageLink | String | N | 템플릿 이미지 링크 |
| content.buttons | Array | N | 템플릿 버튼 |
| content.buttons[].type | String | N | 템플릿 버튼 타입(WL: 웹 링크, AL: 앱 링크, BK: 봇 키워드, MD: 메시지 전달, BF: 비지니스폼)<br>[WL, AL, BK, MD, BF] |
| content.buttons[].name | String | N | 템플릿 버튼 이름 |
| content.buttons[].linkMo | String | N | 템플릿 버튼 모바일 웹 링크 |
| content.buttons[].linkPc | String | N | 템플릿 버튼 PC 웹 링크 |
| content.buttons[].schemeIos | String | N | 템플릿 버튼 iOS 앱 링크 |
| content.buttons[].schemeAndroid | String | N | 템플릿 버튼 안드로이드 앱 링크 |
| content.buttons[].bizFormKey | String | N | BF(비즈니스 폼) 타입 버튼 시, 비즈폼 키 |
| content.header | String | N | 헤더(와이드 아이템리스트 메시지 타입 사용 시, 필수, 최대 25자) |
| content.item | Object | N |  |
| content.item.list | Array | N |  |
| content.item.list[].title | String | N | 아이템 타이틀 첫번째 아이템 25자, 2~4번째 30자 |
| content.item.list[].attachmentId | String | N | 첨부 파일 아이디 |
| content.item.list[].imageUrl | String | N | 아이템 이미지 URL |
| content.item.list[].linkMo | String | N | 대표 링크 모바일 웹 링크 |
| content.item.list[].linkPc | String | N | 대표 링크 PC 웹 링크 |
| content.item.list[].schemeIos | String | N | 대표 링크 iOS 앱 링크 |
| content.item.list[].schemeAndroid | String | N | 대표 링크 안드로이드 앱 링크 |
| content.carousel | Object | N |  |
| content.carousel.list | Array | N |  |
| content.carousel.list[].header | String | N | 캐러셀 아이템 제목 |
| content.carousel.list[].message | String | N | 캐러셀 아이템 메시지 |
| content.carousel.list[].attachment | Object | N |  |
| content.carousel.list[].attachment.buttons | Array | N |  |
| content.carousel.list[].attachment.image | Object | N |  |
| content.carousel.list[].attachment.image.attachmentId | String | N | 첨부 파일 아이디 |
| content.carousel.list[].attachment.image.imageUrl | String | N | 캐러셀 아이템 이미지 URL |
| content.carousel.list[].attachment.image.imageLink | String | N | 캐러셀 아이템 이미지 링크 |
| content.carousel.tail | Object | N |  |
| content.carousel.tail.linkMo | String | N | 대표 링크 모바일 웹 링크 |
| content.carousel.tail.linkPc | String | N | 대표 링크 PC 웹 링크 |
| content.carousel.tail.schemeIos | String | N | 대표 링크 iOS 앱 링크 |
| content.carousel.tail.schemeAndroid | String | N | 대표 링크 안드로이드 앱 링크 |
| content.coupon | Object | N |  |
| content.coupon.title | String | N | 쿠폰 이름 |
| content.coupon.description | String | N | 쿠폰 상세 설명(일반 텍스트, 이미지형 최대 12자 / 와이드 이미지형, 와이드 아이템리스트형 최대 18자) |
| content.coupon.linkMo | String | N | 대표 링크 모바일 웹 링크 |
| content.coupon.linkPc | String | N | 대표 링크 PC 웹 링크 |
| content.coupon.schemeIos | String | N | 대표 링크 iOS 앱 링크 |
| content.coupon.schemeAndroid | String | N | 대표 링크 안드로이드 앱 링크 |



**응답 본문**

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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 친구톡 템플릿 수정

PUT {{endpoint}}/template/v1.0/FRIENDTALK/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "템플릿 이름",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "content" : {
    "messageType" : "TEXT",
    "content" : null,
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "imageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "imageLink" : "https://www.naver.com",
    "buttons" : [ {
      "type" : "WL",
      "name" : "Button Name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123"
    } ],
    "header" : "헤더",
    "item" : {
      "list" : [ {
        "title" : "Item Title",
        "attachmentId" : "20230131070811m2fDe1rXx80",
        "imageUrl" : "https://example.com/image.jpg",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "carousel" : {
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "attachment" : {
          "buttons" : [ {
            "schemeAndroid" : "example://android",
            "name" : "Button Name",
            "linkMo" : "https://m.example.com",
            "schemeIos" : "example://ios",
            "linkPc" : "https://www.example.com",
            "type" : "WL",
            "bizFormKey" : "bizFormKey123",
            "target" : "out"
          } ],
          "image" : {
            "attachmentId" : "20230131070811m2fDe1rXx80",
            "imageUrl" : "https://example.com/image.jpg",
            "imageLink" : "https://www.example.com"
          }
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "coupon" : {
      "title" : "Coupon Title",
      "description" : "Coupon Description",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    }
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/FRIENDTALK/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "템플릿 이름",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "content" : {
    "messageType" : "TEXT",
    "content" : null,
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "imageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "imageLink" : "https://www.naver.com",
    "buttons" : [ {
      "type" : "WL",
      "name" : "Button Name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123"
    } ],
    "header" : "헤더",
    "item" : {
      "list" : [ {
        "title" : "Item Title",
        "attachmentId" : "20230131070811m2fDe1rXx80",
        "imageUrl" : "https://example.com/image.jpg",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "carousel" : {
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "attachment" : {
          "buttons" : [ {
            "schemeAndroid" : "example://android",
            "name" : "Button Name",
            "linkMo" : "https://m.example.com",
            "schemeIos" : "example://ios",
            "linkPc" : "https://www.example.com",
            "type" : "WL",
            "bizFormKey" : "bizFormKey123",
            "target" : "out"
          } ],
          "image" : {
            "attachmentId" : "20230131070811m2fDe1rXx80",
            "imageUrl" : "https://example.com/image.jpg",
            "imageLink" : "https://www.example.com"
          }
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "coupon" : {
      "title" : "Coupon Title",
      "description" : "Coupon Description",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    }
  }
}'
```

</details>
<span id="templateV1x0020DeleteFriendtalkTemplate"></span>

## 친구톡 템플릿 삭제

템플릿을 삭제합니다.

**요청**

```
DELETE /template/v1.0/FRIENDTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



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
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 친구톡 템플릿 삭제

DELETE {{endpoint}}/template/v1.0/FRIENDTALK/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/FRIENDTALK/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
<span id="templateV1x0021CreateEmailTemplate"></span>

## Email 템플릿 등록

템플릿을 등록합니다.

**요청**

```
POST /template/v1.0/EMAIL/templates
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

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateName | String | Y | 템플릿 이름 |
| categoryId | String | N | 카테고리 아이디 |
| messagePurpose | String | N | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | Y |  |
| sender.senderMailAddress | String | Y | 발신 메일 주소 |
| content | Object | Y |  |
| content.title | String | N | 템플릿 메일 제목 |
| content.body | String | N | 템플릿 메일 본문 |
| content.attachmentIds | Array | N | 템플릿 첨부 파일 ID |



**응답 본문**

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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Email 템플릿 등록

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

## Email 템플릿 상세 조회

템플릿을 상세 조회합니다.

**요청**

```
GET /template/v1.0/EMAIL/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



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

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| template | Object | N|  |
| template.templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |
| template.templateName | String | N| 템플릿 이름 |
| template.categoryId | String | N| 카테고리 아이디 |
| template.messageChannel | String | N| 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | N| 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array | N|  |
| template.templateLanguage | String | N| 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object | N|  |
| template.sender.senderMailAddress | String | N| 발신 메일 주소 |
| template.content | Object | N|  |
| template.content.title | String | N| 템플릿 메일 제목 |
| template.content.body | String | N| 템플릿 메일 본문 |
| template.content.attachmentIds | Array | N| 템플릿 첨부 파일 ID |
| template.createdDateTime | String | N| 템플릿 생성 시각 |
| template.updatedDateTime | String | N| 템플릿 수정된 시각 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Email 템플릿 상세 조회

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

## Email 템플릿 리스트 조회

템플릿 리스트를 조회합니다.

**요청**

```
GET /template/v1.0/EMAIL/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateName | Query  | String | N | 템플릿 이름(LIKE 검색) |
| limit | Query  | Integer | N | limit 설정하지 않으면 default 20(최대 1000) |
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
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "배송 완료",
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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | N| 총 건수 |
| templates | Array | N|  |
| templates[].templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | N| 템플릿명 |
| templates[].categoryId | String | N| 카테고리 아이디 |
| templates[].messageChannel | String | N| 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | N| 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array | N|  |
| templates[].createdDateTime | String | N| 템플릿 생성 시각 |
| templates[].updatedDateTime | String | N| 템플릿 수정된 시각 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Email 템플릿 리스트 조회

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

## Email 템플릿 수정

템플릿을 수정합니다.

**요청**

```
PUT /template/v1.0/EMAIL/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "템플릿 이름",
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

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateName | String | Y | 템플릿 이름 |
| messagePurpose | String | N | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | Y |  |
| sender.senderMailAddress | String | Y | 발신 메일 주소 |
| content | Object | Y |  |
| content.title | String | N | 템플릿 메일 제목 |
| content.body | String | N | 템플릿 메일 본문 |
| content.attachmentIds | Array | N | 템플릿 첨부 파일 ID |



**응답 본문**

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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Email 템플릿 수정

PUT {{endpoint}}/template/v1.0/EMAIL/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "템플릿 이름",
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
curl -X PUT "${endpoint}/template/v1.0/EMAIL/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "템플릿 이름",
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
<span id="templateV1x0024DeleteEmailTemplate"></span>

## Email 템플릿 삭제

템플릿을 삭제합니다.

**요청**

```
DELETE /template/v1.0/EMAIL/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



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
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Email 템플릿 삭제

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

## RCS 템플릿 등록

템플릿을 등록합니다.

**요청**

```
POST /template/v1.0/RCS/templates
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

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateName | String | Y | 템플릿 이름 |
| categoryId | String | N | 카테고리 아이디 |
| messagePurpose | String | N | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | Y |  |
| sender.brandId | String | Y | 브랜드 아이디 |
| sender.chatbotId | String | Y | 대화방(챗봇) 아이디 |
| content | Object | Y |  |
| content.messageType | String | N | RCS 발송 메시지 유형(SMS, LMS, MMS, RBC_TEMPLATE)<br>[SMS, LMS, MMS, RBC_TEMPLATE] |
| content.title | String | N | 메시지 제목 |
| content.body | String | N | 메시지 본문 |
| content.smsType | String | N | SMS 타입<br>[STANDALONE] |
| content.lmsType | String | N | LMS 타입<br>[STANDALONE, FORMAT_BASIC, FORMAT_TITLE_HIGHLIGHT, FORMAT_PARAGRAPH] |
| content.mmsType | String | N | MMS 타입(MMS 발송일 경우 필수)<br>[HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL] |
| content.messagebaseId | String | N | RCS Biz Center 템플릿 아이디 |
| content.unsubscribePhoneNumber | String | N | 수신 거부 번호(광고 발송일 경우 필수) |
| content.cards | Array | N | RCS 카드 |
| content.cards[].title | String | N | 제목 |
| content.cards[].description | String | N | 본문 |
| content.cards[].attachmentId | String | N | 이미지 첨부 파일 아이디 |
| content.cards[].mTitle | String | N | 메인 타이틀 |
| content.cards[].mTitleMedia | String | N | 메인 타이틀 로고 파일 ID |
| content.cards[].title1 | String | N | 제목 1 |
| content.cards[].title2 | String | N | 제목 2 |
| content.cards[].title3 | String | N | 제목 3 |
| content.cards[].description1 | String | N | 본문 1 |
| content.cards[].description2 | String | N | 본문 2 |
| content.cards[].description3 | String | N | 본문 3 |
| content.cards[].buttons | Array | N |  |
| content.buttons | Array | N | RCS 버튼 리스트 |
| content.buttons[].buttonType | String | N | buttonType 값과 동일한 이름을 가진 Action 객체가 buttonJson으로 포함됨.<br>버튼 타입 대화방 열기(COMPOSE), 복사하기(CLIPBOARD), 전화 걸기(DIALER), 지도 보여주기(MAP_SHOW), 지도 검색하기(MAP_QUERY), 현재 위치 공유하기(MAP_SHARE), URL 연결하기(URL), 일정 등록하기(CALENDAR)<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | N |  |
| content.buttons[].buttonJson.action | Object | N | 버튼 액션 |



**응답 본문**

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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### RCS 템플릿 등록

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

## RCS 템플릿 리스트 조회

템플릿 리스트를 조회합니다.

**요청**

```
GET /template/v1.0/RCS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateName | Query  | String | N | 템플릿 이름(LIKE 검색) |
| limit | Query  | Integer | N | limit 설정하지 않으면 default 20(최대 1000) |
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
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "배송 완료",
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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | N| 총 건수 |
| templates | Array | N|  |
| templates[].templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | N| 템플릿명 |
| templates[].categoryId | String | N| 카테고리 아이디 |
| templates[].messageChannel | String | N| 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | N| 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array | N|  |
| templates[].createdDateTime | String | N| 템플릿 생성 시각 |
| templates[].updatedDateTime | String | N| 템플릿 수정된 시각 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### RCS 템플릿 리스트 조회

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

## RCS 템플릿 상세 조회

템플릿을 상세 조회합니다.

**요청**

```
GET /template/v1.0/RCS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



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
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "템플릿 이름",
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
      "title" : "명절 운영시간 공지",
      "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다. 방문해주세요^^",
      "smsType" : "STANDALONE",
      "lmsType" : "HORIZONTAL",
      "mmsType" : "HORIZONTAL",
      "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
      "messagebaseformId" : "SS000000",
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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| template | Object | N|  |
| template.templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |
| template.templateName | String | N| 템플릿 이름 |
| template.categoryId | String | N| 카테고리 아이디 |
| template.messageChannel | String | N| 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | N| 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array | N|  |
| template.templateLanguage | String | N| 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object | N|  |
| template.sender.brandId | String | N| 브랜드 아이디 |
| template.sender.chatbotId | String | N| 대화방(챗봇) 아이디 |
| template.content | Object | N|  |
| template.content.messageType | String | N| RCS 발송 메시지 유형(SMS, LMS, MMS, RBC_TEMPLATE)<br>[SMS, LMS, MMS, RBC_TEMPLATE] |
| template.content.title | String | N| 메시지 제목 |
| template.content.body | String | N| 메시지 본문 |
| template.content.smsType | String | N| SMS 타입<br>[STANDALONE] |
| template.content.lmsType | String | N| LMS 타입<br>[STANDALONE, FORMAT_BASIC, FORMAT_TITLE_HIGHLIGHT, FORMAT_PARAGRAPH] |
| template.content.mmsType | String | N| MMS 타입(MMS 발송일 경우 필수)<br>[HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL] |
| template.content.messagebaseId | String | N| RCS Biz Center 템플릿 아이디 |
| template.content.messagebaseformId | String | N| RCS Biz Center 에서 지정한 messageBase 양식<br>- SS000000(SMS 기본형)<br>- SL000000(LMS 기본형)<br>- OL00000001(LMS Format 기본형)<br>- OL00000002(LMS Format 타이틀 강조형)<br>- OL00000003(LMS Format 문단형)<br>- SMwThT00(MMS 세로형)<br>- SMwThM00(MMS 가로형)<br>- CMwMhM0200(MMS 슬라이드 중간형(2))<br>- CMwMhM0300(MMS 슬라이드 중간형(3))<br>- CMwMhM0400(MMS 슬라이드 중간형(4))<br>- CMwMhM0500(MMS 슬라이드 중간형(5))<br>- CMwMhM0600(MMS 슬라이드 중간형(6))<br>- CMwShS0200(MMS 슬라이드 작은형(2))<br>- CMwShS0300(MMS 슬라이드 작은형(3))<br>- CMwShS0400(MMS 슬라이드 작은형(4))<br>- CMwShS0500(MMS 슬라이드 작은형(5))<br>- CMwShS0600(MMS 슬라이드 작은형(6))<br>- CLI00001(아이템 상세형)<br>- CLI00002(이미지 강조형 (1:1))<br>- CLI00003(이미지 강조형 (3:4))<br>- CLI00004(이미지 & 타이틀 강조형 (1:1))<br>- CLI00005(이미지 & 타이틀 강조형 (3:4))<br>- CLI00006(썸네일형 (가로))<br>- CLI00007(썸네일형 (세로))<br>- CLI00008(SNS형 (하단버튼))<br>- CLI00009(SNS형 (중간버튼))<br>- ITTBNV(썸네일형(세로))<br>- ITTBNH(썸네일형(가로))<br>- ITHIMS(이미지 강조형(1:1))<br>- ITHIMV(이미지 강조형(3:4))<br>- ITSNSS(SNS형)<br>- ITSNSH(SNS형(중간버튼))<br>- ITHITS(이미지 & 타이틀 강조형(1:1))<br>- ITHITV(이미지 & 타이틀 강조형(3:4))<br>- ITCRM2(슬라이드 형(2))<br>- ITCRM3(슬라이드 형(3))<br>- ITCRM4(슬라이드 형(4))<br>- ITCRM5(슬라이드 형(5))<br>- ITCRM6(슬라이드 형(6))<br>- CLT00001(아이템 강조형 DESC)<br>- CLT00002(아이템 강조형 TABLE)<br>- TATA001F(타이틀 자유형 FREE)<br>- TATA001C(타이틀 자유형 CELL)<br>- TATA001D(타이틀 자유형 DESC)<br>- GG000F(타이틀 선택형 FREE)<br>- FF005C(명세서 CELL)<br>- FF005D(명세서 DESC)<br>- FF004C(취소 CELL)<br>- FF004D(취소 DESC)<br>- GG003C(안내 CELL)<br>- GG003D(안내 DESC)<br>- GG002C(인증 CELL)<br>- GG002D(인증 DESC)<br>- GG001C(회원 가입 CELL)<br>- GG001D(회원 가입 DESC)<br>- EE001C(예약 CELL)<br>- EE001D(예약 DESC)<br>- CC003C(배송 CELL)<br>- CC003D(배송 DESC)<br>- FF002C(입금 CELL)<br>- FF002D(입금 DESC)<br>- FF001C(승인 CELL)<br>- FF001D(승인 DESC)<br>- CC002C(주문 CELL)<br>- CC002D(주문 DESC)<br>- CC001C(출고 CELL)<br>- CC001D(출고 DESC)<br>- FF003C(출금 CELL)<br>- FF003D(출금 DESC)<br>- CLL00001(LMS 명세서 A)<br>- CLL00002(LMS 문단형)<br>- CLL00003(LMS 타이들 강조형)<br>- CLL00004(LMS 기본형)<br>- CLL00005(LMS 명세서 B)<br>- CLL00006(LMS 명세서 C)<br><br>[SS000000, SL000000, OL00000001, OL00000002, OL00000003, SMwThT00, SMwThM00, CMwMhM0200, CMwMhM0300, CMwMhM0400, CMwMhM0500, CMwMhM0600, CMwShS0200, CMwShS0300, CMwShS0400, CMwShS0500, CMwShS0600, CLI00001, CLI00002, CLI00003, CLI00004, CLI00005, CLI00006, CLI00007, CLI00008, CLI00009, ITTBNV, ITTBNH, ITHIMS, ITHIMV, ITSNSS, ITSNSH, ITHITS, ITHITV, ITCRM2, ITCRM3, ITCRM4, ITCRM5, ITCRM6, CLT00001, CLT00002, TATA001C, TATA001D, TATA001F, FF005C, FF005D, FF004C, FF004D, GG003C, GG003D, GG002C, GG002D, GG001C, GG001D, GG000F, EE001C, EE001D, CC003C, CC003D, FF002C, FF002D, FF001C, FF001D, CC002C, CC002D, CC001C, CC001D, FF003C, FF003D, CLL00001, CLL00002, CLL00003, CLL00004, CLL00005, CLL00006] |
| template.content.unsubscribePhoneNumber | String | N| 수신 거부 번호(광고 발송일 경우 필수) |
| template.content.cards | Array | N| RCS 카드 |
| template.content.cards[].title | String | N| 제목 |
| template.content.cards[].description | String | N| 본문 |
| template.content.cards[].attachmentId | String | N| 이미지 첨부 파일 아이디 |
| template.content.cards[].mTitle | String | N| 메인 타이틀 |
| template.content.cards[].mTitleMedia | String | N| 메인 타이틀 로고 파일 ID |
| template.content.cards[].title1 | String | N| 제목 1 |
| template.content.cards[].title2 | String | N| 제목 2 |
| template.content.cards[].title3 | String | N| 제목 3 |
| template.content.cards[].description1 | String | N| 본문 1 |
| template.content.cards[].description2 | String | N| 본문 2 |
| template.content.cards[].description3 | String | N| 본문 3 |
| template.content.cards[].buttons | Array | N|  |
| template.content.buttons | Array | N| RCS 버튼 리스트 |
| template.content.buttons[].buttonType | String | N| buttonType 값과 동일한 이름을 가진 Action 객체가 buttonJson으로 포함됨.<br>버튼 타입 대화방 열기(COMPOSE), 복사하기(CLIPBOARD), 전화 걸기(DIALER), 지도 보여주기(MAP_SHOW), 지도 검색하기(MAP_QUERY), 현재 위치 공유하기(MAP_SHARE), URL 연결하기(URL), 일정 등록하기(CALENDAR)<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| template.content.buttons[].buttonJson | Object | N|  |
| template.content.buttons[].buttonJson.action | Object | N| 버튼 액션 |
| template.additionalProperty | Object | N|  |
| template.additionalProperty.status | String | N| 템플릿 상태<br>- SAVE: 저장<br>- APPROVE_WAIT: 승인 대기<br>- INSPECTION_START: 검수 시작<br>- INSPECTION_FINISH: 검수 완료<br>- APPROVE: 승인<br>- REJECT: 거부<br>- MODIFY_APPROVE_WAIT: 수정 승인 대기<br>- MODIFY_INSPECTION_START: 수정 검수 시작<br>- MODIFY_INSPECTION_FINISH: 수정 검수 완료<br>- MODIFY_REJECT: 수정 거부<br><br>[SAVE, APPROVE_WAIT, INSPECTION_START, INSPECTION_FINISH, APPROVE, REJECT, MODIFY_APPROVE_WAIT, MODIFY_INSPECTION_START, MODIFY_INSPECTION_FINISH, MODIFY_REJECT] |
| template.additionalProperty.approvedDateTime | String | N| 템플릿 승인 시각 |
| template.createdDateTime | String | N| 템플릿 생성 시각 |
| template.updatedDateTime | String | N| 템플릿 수정된 시각 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### RCS 템플릿 상세 조회

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

## RCS 템플릿 수정

템플릿을 수정합니다.

**요청**

```
PUT /template/v1.0/RCS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


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

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateName | String | Y | 템플릿 이름 |
| messagePurpose | String | N | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.brandId | String | Y | 브랜드 아이디 |
| sender.chatbotId | String | Y | 대화방(챗봇) 아이디 |
| content | Object | Y |  |
| content.messageType | String | N | RCS 발송 메시지 유형(SMS, LMS, MMS, RBC_TEMPLATE)<br>[SMS, LMS, MMS, RBC_TEMPLATE] |
| content.title | String | N | 메시지 제목 |
| content.body | String | N | 메시지 본문 |
| content.smsType | String | N | SMS 타입<br>[STANDALONE] |
| content.lmsType | String | N | LMS 타입<br>[STANDALONE, FORMAT_BASIC, FORMAT_TITLE_HIGHLIGHT, FORMAT_PARAGRAPH] |
| content.mmsType | String | N | MMS 타입(MMS 발송일 경우 필수)<br>[HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL] |
| content.messagebaseId | String | N | RCS Biz Center 템플릿 아이디 |
| content.unsubscribePhoneNumber | String | N | 수신 거부 번호(광고 발송일 경우 필수) |
| content.cards | Array | N | RCS 카드 |
| content.cards[].title | String | N | 제목 |
| content.cards[].description | String | N | 본문 |
| content.cards[].attachmentId | String | N | 이미지 첨부 파일 아이디 |
| content.cards[].mTitle | String | N | 메인 타이틀 |
| content.cards[].mTitleMedia | String | N | 메인 타이틀 로고 파일 ID |
| content.cards[].title1 | String | N | 제목 1 |
| content.cards[].title2 | String | N | 제목 2 |
| content.cards[].title3 | String | N | 제목 3 |
| content.cards[].description1 | String | N | 본문 1 |
| content.cards[].description2 | String | N | 본문 2 |
| content.cards[].description3 | String | N | 본문 3 |
| content.cards[].buttons | Array | N |  |
| content.buttons | Array | N | RCS 버튼 리스트 |
| content.buttons[].buttonType | String | N | buttonType 값과 동일한 이름을 가진 Action 객체가 buttonJson으로 포함됨.<br>버튼 타입 대화방 열기(COMPOSE), 복사하기(CLIPBOARD), 전화 걸기(DIALER), 지도 보여주기(MAP_SHOW), 지도 검색하기(MAP_QUERY), 현재 위치 공유하기(MAP_SHARE), URL 연결하기(URL), 일정 등록하기(CALENDAR)<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | N |  |
| content.buttons[].buttonJson.action | Object | N | 버튼 액션 |



**응답 본문**

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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### RCS 템플릿 수정

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

## RCS 템플릿 삭제

템플릿을 삭제합니다.

**요청**

```
DELETE /template/v1.0/RCS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



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
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### RCS 템플릿 삭제

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

## Push 템플릿 등록

템플릿을 등록합니다.

**요청**

```
POST /template/v1.0/PUSH/templates
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


```
{
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "대표 번호",
    "unsubscribeGuide" : "매뉴 > 설정",
    "title" : "제목",
    "body" : "내용",
    "richMessage" : {
      "buttons" : [ {
        "name" : "버튼 이름",
        "submitName" : "전송 버튼 이름",
        "buttonType" : "버튼 타입, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "버튼을 눌렀을때, 연결되는 링크",
        "hint" : "버튼에대한 힌트"
      } ],
      "media" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "큰 아이콘의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "그룹의 키, 여러 개의 메시지를 그룹 단위로 묶는 기능, Android에서만 지원",
        "description" : "그룹에대한 설명"
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

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateName | String | Y | 템플릿 이름 |
| categoryId | String | N | 카테고리 아이디 |
| messagePurpose | String | N | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| content | Object | Y | 푸시 메시지 내용 |



**응답 본문**

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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Push 템플릿 등록

POST {{endpoint}}/template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "대표 번호",
    "unsubscribeGuide" : "매뉴 > 설정",
    "title" : "제목",
    "body" : "내용",
    "richMessage" : {
      "buttons" : [ {
        "name" : "버튼 이름",
        "submitName" : "전송 버튼 이름",
        "buttonType" : "버튼 타입, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "버튼을 눌렀을때, 연결되는 링크",
        "hint" : "버튼에대한 힌트"
      } ],
      "media" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "큰 아이콘의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "그룹의 키, 여러 개의 메시지를 그룹 단위로 묶는 기능, Android에서만 지원",
        "description" : "그룹에대한 설명"
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
  "templateName" : "템플릿 이름",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "대표 번호",
    "unsubscribeGuide" : "매뉴 > 설정",
    "title" : "제목",
    "body" : "내용",
    "richMessage" : {
      "buttons" : [ {
        "name" : "버튼 이름",
        "submitName" : "전송 버튼 이름",
        "buttonType" : "버튼 타입, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "버튼을 눌렀을때, 연결되는 링크",
        "hint" : "버튼에대한 힌트"
      } ],
      "media" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "큰 아이콘의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "그룹의 키, 여러 개의 메시지를 그룹 단위로 묶는 기능, Android에서만 지원",
        "description" : "그룹에대한 설명"
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

## Push 템플릿 리스트 조회

템플릿 리스트를 조회합니다.

**요청**

```
GET /template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateName | Query  | String | N | 템플릿 이름(LIKE 검색) |
| limit | Query  | Integer | N | limit 설정하지 않으면 default 20(최대 1000) |
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
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "배송 완료",
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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | N| 총 건수 |
| templates | Array | N|  |
| templates[].templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | N| 템플릿명 |
| templates[].categoryId | String | N| 카테고리 아이디 |
| templates[].messageChannel | String | N| 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | N| 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array | N|  |
| templates[].createdDateTime | String | N| 템플릿 생성 시각 |
| templates[].updatedDateTime | String | N| 템플릿 수정된 시각 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Push 템플릿 리스트 조회

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

## Push 템플릿 상세 조회

템플릿을 상세 조회합니다.

**요청**

```
GET /template/v1.0/PUSH/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



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
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "템플릿 이름",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "content" : {
      "unsubscribePhoneNumber" : "대표 번호",
      "unsubscribeGuide" : "매뉴 > 설정",
      "title" : "제목",
      "body" : "내용",
      "richMessage" : {
        "buttons" : [ {
          "name" : "버튼 이름",
          "submitName" : "전송 버튼 이름",
          "buttonType" : "버튼 타입, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
          "link" : "버튼을 눌렀을때, 연결되는 링크",
          "hint" : "버튼에대한 힌트"
        } ],
        "media" : {
          "sourceType" : "미디어의 위치, REMOTE, LOCAL",
          "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
          "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
          "extension" : "미디어 파일의 확장자, jpg, png",
          "expandable" : true
        },
        "androidMedia" : {
          "sourceType" : "미디어의 위치, REMOTE, LOCAL",
          "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
          "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
          "extension" : "미디어 파일의 확장자, jpg, png",
          "expandable" : true
        },
        "iosMedia" : {
          "sourceType" : "미디어의 위치, REMOTE, LOCAL",
          "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
          "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
          "extension" : "미디어 파일의 확장자, jpg, png",
          "expandable" : true
        },
        "largeIcon" : {
          "sourceType" : "큰 아이콘의 위치, REMOTE, LOCAL",
          "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE"
        },
        "group" : {
          "key" : "그룹의 키, 여러 개의 메시지를 그룹 단위로 묶는 기능, Android에서만 지원",
          "description" : "그룹에대한 설명"
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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| template | Object | N|  |
| template.templateId | String | N| 템플릿 등록 시, 발급된 템플릿 아이디 |
| template.templateName | String | N| 템플릿 이름 |
| template.categoryId | String | N| 카테고리 아이디 |
| template.messageChannel | String | N| 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | N| 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array | N|  |
| template.templateLanguage | String | N| 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.content | Object | N| 푸시 메시지 내용 |
| template.createdDateTime | String | N| 템플릿 생성 시각 |
| template.updatedDateTime | String | N| 템플릿 수정된 시각 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Push 템플릿 상세 조회

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

## Push 템플릿 수정

템플릿을 수정합니다.

**요청**

```
PUT /template/v1.0/PUSH/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateName" : "템플릿 이름",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "대표 번호",
    "unsubscribeGuide" : "매뉴 > 설정",
    "title" : "제목",
    "body" : "내용",
    "richMessage" : {
      "buttons" : [ {
        "name" : "버튼 이름",
        "submitName" : "전송 버튼 이름",
        "buttonType" : "버튼 타입, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "버튼을 눌렀을때, 연결되는 링크",
        "hint" : "버튼에대한 힌트"
      } ],
      "media" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "큰 아이콘의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "그룹의 키, 여러 개의 메시지를 그룹 단위로 묶는 기능, Android에서만 지원",
        "description" : "그룹에대한 설명"
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

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateName | String | Y | 템플릿 이름 |
| messagePurpose | String | N | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입 default: PLAIN_TEXT<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| content | Object | Y | 푸시 메시지 내용 |



**응답 본문**

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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Push 템플릿 수정

PUT {{endpoint}}/template/v1.0/PUSH/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "템플릿 이름",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "대표 번호",
    "unsubscribeGuide" : "매뉴 > 설정",
    "title" : "제목",
    "body" : "내용",
    "richMessage" : {
      "buttons" : [ {
        "name" : "버튼 이름",
        "submitName" : "전송 버튼 이름",
        "buttonType" : "버튼 타입, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "버튼을 눌렀을때, 연결되는 링크",
        "hint" : "버튼에대한 힌트"
      } ],
      "media" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "큰 아이콘의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "그룹의 키, 여러 개의 메시지를 그룹 단위로 묶는 기능, Android에서만 지원",
        "description" : "그룹에대한 설명"
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
  "templateName" : "템플릿 이름",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "대표 번호",
    "unsubscribeGuide" : "매뉴 > 설정",
    "title" : "제목",
    "body" : "내용",
    "richMessage" : {
      "buttons" : [ {
        "name" : "버튼 이름",
        "submitName" : "전송 버튼 이름",
        "buttonType" : "버튼 타입, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "버튼을 눌렀을때, 연결되는 링크",
        "hint" : "버튼에대한 힌트"
      } ],
      "media" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "미디어의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE",
        "mediaType" : "미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원",
        "extension" : "미디어 파일의 확장자, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "큰 아이콘의 위치, REMOTE, LOCAL",
        "source" : "미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "그룹의 키, 여러 개의 메시지를 그룹 단위로 묶는 기능, Android에서만 지원",
        "description" : "그룹에대한 설명"
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

## Push 템플릿 삭제

템플릿을 삭제합니다.

**요청**

```
DELETE /template/v1.0/PUSH/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| templateId | Path  | String | Y | 템플릿 아이디 |



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
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Push 템플릿 삭제

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

## 템플릿 파라미터 조회

템플릿이 포함하고 있는 파라미터 목록을 조회합니다.

**요청**

```
GET /template/v1.0/{messageChannel}/templates/{templateId}/parameters
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageChannel | Path  | String | Y | 메시지 채널입니다.<br>[SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH] |
| templateId | Path  | String | Y | 템플릿 아이디 |



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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| templateParameter | Object | N| 템플릿 파라미터 결과 JSON |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 파라미터 조회

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