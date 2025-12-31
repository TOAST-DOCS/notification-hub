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
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateName | String | Y | 템플릿 이름 |
| categoryId | String | N | 카테고리 아이디 |
| messagePurpose | String | N | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.senderPhoneNumber | String | N | 발신 번호 |
| content | Object | Y |  |
| content.messageType | String | N | 발송 메시지 유형(SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| content.title | String | N | 메시지 제목 |
| content.body | String | N | 메시지 본문 |
| content.attachmentIds | Array | N | 첨부 파일 아이디 최대 3개 |



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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |



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
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | 총 건수 |
| templates | Array |  |
| templates[].templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | 템플릿명 |
| templates[].categoryId | String | 카테고리 아이디 |
| templates[].messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | 템플릿 생성 시각 |
| templates[].updatedDateTime | String | 템플릿 수정된 시각 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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
      "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| template | Object |  |
| template.templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |
| template.templateName | String | 템플릿 이름 |
| template.categoryId | String | 카테고리 아이디 |
| template.messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array |  |
| template.templateLanguage | String | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object |  |
| template.sender.senderPhoneNumber | String | 발신 번호 |
| template.content | Object |  |
| template.content.messageType | String | 발송 메시지 유형(SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| template.content.title | String | 메시지 제목 |
| template.content.body | String | 메시지 본문 |
| template.content.attachmentIds | Array | 첨부 파일 아이디 최대 3개 |
| template.createdDateTime | String | 템플릿 생성 시각 |
| template.updatedDateTime | String | 템플릿 수정된 시각 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateName | String | Y | 템플릿 이름 |
| messagePurpose | String | N | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.senderPhoneNumber | String | N | 발신 번호 |
| content | Object | Y |  |
| content.messageType | String | N | 발송 메시지 유형(SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| content.title | String | N | 메시지 제목 |
| content.body | String | N | 메시지 본문 |
| content.attachmentIds | Array | N | 첨부 파일 아이디 최대 3개 |



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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



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
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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
| messagePurpose | String | N | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
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
| content.buttons[].type | String | N | 템플릿 버튼 타입(WL: 웹 링크, AL: 앱 링크, DS: 배송 조회, BK: 봇 키워드, MD: 메시지 전달, BC: 상담톡 전환, BT: 봇 전환, AC: 채널 추가, BF: 비지니스폼, P1: 이미지 보안 전송 플러그인 ID, P2: 개인정보이용 플러그인 ID, P3: 원클릭 결제 플러그인 ID)<br>[WL, AL, DS, BK, MD, BC, BT, AC, BF, P1, P2, P3] |
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | 총 건수 |
| templates | Array |  |
| templates[].templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | 템플릿명 |
| templates[].categoryId | String | 카테고리 아이디 |
| templates[].messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | 템플릿 생성 시각 |
| templates[].updatedDateTime | String | 템플릿 수정된 시각 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | 총 건수 |
| templates | Array |  |
| templates[].templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | 템플릿명 |
| templates[].categoryId | String | 카테고리 아이디 |
| templates[].messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | 템플릿 생성 시각 |
| templates[].updatedDateTime | String | 템플릿 수정된 시각 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| template | Object |  |
| template.templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |
| template.templateName | String | 템플릿 이름 |
| template.categoryId | String | 카테고리 아이디 |
| template.messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array |  |
| template.templateLanguage | String | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object |  |
| template.sender.senderKey | String | 발신프로필 발신키 |
| template.sender.senderProfileId | String | 카카오톡 채널명 |
| template.sender.senderProfileType | String | 발신프로필 타입<br>[GROUP, NORMAL] |
| template.additionalProperty | Object |  |
| template.additionalProperty.templateCode | String | 템플릿 코드(영문, 숫자, -, _) |
| template.additionalProperty.kakaoTemplateCode | String | 카카오 템플릿 코드 |
| template.additionalProperty.comments | Array | 템플릿 문의 리스트 |
| template.additionalProperty.comments[].id | Integer | 문의 아이디 |
| template.additionalProperty.comments[].content | String | 문의 내용 |
| template.additionalProperty.comments[].userName | String | 작성자 |
| template.additionalProperty.comments[].createdAt | String | 문의 생성 시각 |
| template.additionalProperty.comments[].attachments | Array | 문의 첨부 파일 |
| template.additionalProperty.comments[].status | String | 문의 상태(REQ: 요청, INQ:문의, APR:승인, REJ:반려, REP: 답변)<br>[REQ, INQ, APR, REJ, REP] |
| template.additionalProperty.status | String | REG:요청, REQ:검수 중, APR:승인, REJ: 반려<br>[REG, REQ, APR, REJ] |
| template.additionalProperty.templateModificationStatus | String | REG:요청, REQ:검수 중, APR:승인, REJ: 반려<br>[REG, REQ, APR, REJ] |
| template.additionalProperty.block | Boolean | 템플릿 차단 여부 |
| template.additionalProperty.dormant | Boolean | 템플릿 휴면 여부 |
| template.content | Object |  |
| template.content.templateMessageType | String | 템플릿 메시지 유형(BA: 기본형, EX: 부가 정보형, AD: 채널 추가형, MI: 복합형, default: BA) |
| template.content.templateEmphasizeType | String | 템플릿 강조 표시 타입(NONE : 기본, TEXT : 강조 표시, IMAGE: 이미지형, ITEM_LIST: 아이템리스트형, default : NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| template.content.templateContent | String | 템플릿 본문 |
| template.content.templateAd | String | 채널 추가 안내 메시지(템플릿 메시지 유형: 채널 추가형, 복합형일 경우 고정값) |
| template.content.templateExtra | String | 템플릿 부가 정보(템플릿 메시지 유형이 [부가 정보형/복합형]일 경우 필수), 치환 변수 사용 불가, URL 포함 가능 |
| template.content.templateTitle | String | 템플릿 제목(최대 50자, Android: 2줄, 23자 이상 말줄임 처리, iOS : 2줄, 27자 이상 말줄임 처리) |
| template.content.templateSubtitle | String | 템플릿 보조 문구(최대 50자, Android: 18자 이상 말줄임 처리, iOS : 21자 이상 말줄임 처리) |
| template.content.templateHeader | String | 템플릿 헤더, 변수 입력 가능 |
| template.content.templateItem | Object |  |
| template.content.templateItem.list | Array |  |
| template.content.templateItem.list[].title | String | 아이템 타이틀 |
| template.content.templateItem.list[].description | String | 아이템 설명 |
| template.content.templateItem.summary | Object |  |
| template.content.templateItem.summary.title | String | 요약 타이틀 |
| template.content.templateItem.summary.description | String | 요약 설명(변수 및 화폐 단위, 숫자, 쉼표, 마침표만 사용 가능) |
| template.content.templateItemHighlight | Object |  |
| template.content.templateItemHighlight.title | String | 아이템 하이라이트 타이틀(최대 30자, 섬네일 이미지가 있을 경우, 21자) |
| template.content.templateItemHighlight.description | String | 아이템 하이라이트 설명(최대 19자, 섬네일 이미지가 있을 경우, 13자) |
| template.content.templateItemHighlight.attachmentId | String | 템플릿 첨부 파일 ID |
| template.content.templateItemHighlight.imageUrl | String | 섬네일 이미지 주소 |
| template.content.templateRepresentLink | Object |  |
| template.content.templateRepresentLink.linkMo | String | 대표 링크 모바일 웹 링크 |
| template.content.templateRepresentLink.linkPc | String | 대표 링크 PC 웹 링크 |
| template.content.templateRepresentLink.schemeIos | String | 대표 링크 iOS 앱 링크 |
| template.content.templateRepresentLink.schemeAndroid | String | 대표 링크 안드로이드 앱 링크 |
| template.content.attachmentId | String | 템플릿 첨부 파일 ID |
| template.content.templateImageName | String | 템플릿 이미지 이름 |
| template.content.templateImageUrl | String | 템플릿 이미지 링크 |
| template.content.securityFlag | Boolean | 템플릿 보안 여부(default: false) |
| template.content.categoryCode | String | 템플릿 카테고리 코드(템플릿 카테고리 조회 API 참고, default: 999999) |
| template.content.buttons | Array | 템플릿 버튼 |
| template.content.buttons[].ordering | Integer | 템플릿 버튼 순서 |
| template.content.buttons[].type | String | 템플릿 버튼 타입(WL: 웹 링크, AL: 앱 링크, DS: 배송 조회, BK: 봇 키워드, MD: 메시지 전달, BC: 상담톡 전환, BT: 봇 전환, AC: 채널 추가, BF: 비지니스폼, P1: 이미지 보안 전송 플러그인 ID, P2: 개인정보이용 플러그인 ID, P3: 원클릭 결제 플러그인 ID)<br>[WL, AL, DS, BK, MD, BC, BT, AC, BF, P1, P2, P3] |
| template.content.buttons[].name | String | 템플릿 버튼 이름 |
| template.content.buttons[].linkMo | String | 템플릿 버튼 모바일 웹 링크 |
| template.content.buttons[].linkPc | String | 템플릿 버튼 PC 웹 링크 |
| template.content.buttons[].schemeIos | String | 템플릿 버튼 iOS 앱 링크 |
| template.content.buttons[].schemeAndroid | String | 템플릿 버튼 안드로이드 앱 링크 |
| template.content.buttons[].bizFormId | Integer | 템플릿 버튼 비즈니스폼 ID(BF 타입일 경우, 필수) |
| template.content.quickReplies | Array | 템플릿 바로 연결 |
| template.content.quickReplies[].ordering | Integer | 템플릿 바로연결 순서 |
| template.content.quickReplies[].type | String | 템플릿 바로연결 타입(WL: 웹 링크, AL: 앱 링크, BK: 봇 키워드, BC: 상담톡 전환, BT: 봇 전환, BF: 비지니스폼)<br>[WL, AL, BK, BC, BT, BF] |
| template.content.quickReplies[].name | String | 템플릿 바로연결 이름 |
| template.content.quickReplies[].linkMo | String | 템플릿 바로연결 모바일 웹 링크 |
| template.content.quickReplies[].linkPc | String | 템플릿 바로연결 PC 웹 링크 |
| template.content.quickReplies[].schemeIos | String | 템플릿 바로연결 iOS 앱 링크 |
| template.content.quickReplies[].schemeAndroid | String | 템플릿 바로연결 안드로이드 앱 링크 |
| template.content.quickReplies[].bizFormId | Integer | 템플릿 바로연결 비즈니스폼 ID(BF 타입일 경우, 필수) |
| template.createdDateTime | String | 템플릿 생성 시각 |
| template.updatedDateTime | String | 템플릿 수정된 시각 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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
| messagePurpose | String | N | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
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
| content.buttons[].type | String | N | 템플릿 버튼 타입(WL: 웹 링크, AL: 앱 링크, DS: 배송 조회, BK: 봇 키워드, MD: 메시지 전달, BC: 상담톡 전환, BT: 봇 전환, AC: 채널 추가, BF: 비지니스폼, P1: 이미지 보안 전송 플러그인 ID, P2: 개인정보이용 플러그인 ID, P3: 원클릭 결제 플러그인 ID)<br>[WL, AL, DS, BK, MD, BC, BT, AC, BF, P1, P2, P3] |
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 문의하기(파일 첨부)

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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | 총 건수 |
| templates | Array |  |
| templates[].templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | 템플릿 이름 |
| templates[].categoryId | String | 카테고리 아이디 |
| templates[].messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].templateLanguage | String | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| templates[].sender | Object |  |
| templates[].sender.senderKey | String | 발신프로필 발신키 |
| templates[].sender.senderProfileId | String | 카카오톡 채널명 |
| templates[].sender.senderProfileType | String | 발신프로필 타입<br>[GROUP, NORMAL] |
| templates[].additionalProperty | Object |  |
| templates[].additionalProperty.templateCode | String | 템플릿 코드(영문, 숫자, -, _) |
| templates[].additionalProperty.kakaoTemplateCode | String | 카카오 템플릿 코드 |
| templates[].additionalProperty.comments | Array | 템플릿 문의 리스트 |
| templates[].additionalProperty.status | String | REG:요청, REQ:검수 중, APR:승인, REJ: 반려<br>[REG, REQ, APR, REJ] |
| templates[].additionalProperty.block | Boolean | 템플릿 차단 여부 |
| templates[].additionalProperty.dormant | Boolean | 템플릿 휴면 여부 |
| templates[].additionalProperty.activated | Boolean | 활성화 여부 |
| templates[].content | Object |  |
| templates[].content.templateMessageType | String | 템플릿 메시지 유형(BA: 기본형, EX: 부가 정보형, AD: 채널 추가형, MI: 복합형, default: BA) |
| templates[].content.templateEmphasizeType | String | 템플릿 강조 표시 타입(NONE : 기본, TEXT : 강조 표시, IMAGE: 이미지형, ITEM_LIST: 아이템리스트형, default : NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| templates[].content.templateContent | String | 템플릿 본문 |
| templates[].content.templateAd | String | 채널 추가 안내 메시지(템플릿 메시지 유형: 채널 추가형, 복합형일 경우 고정값) |
| templates[].content.templateExtra | String | 템플릿 부가 정보(템플릿 메시지 유형이 [부가 정보형/복합형]일 경우 필수), 치환 변수 사용 불가, URL 포함 가능 |
| templates[].content.templateTitle | String | 템플릿 제목(최대 50자, Android: 2줄, 23자 이상 말줄임 처리, iOS : 2줄, 27자 이상 말줄임 처리) |
| templates[].content.templateSubtitle | String | 템플릿 보조 문구(최대 50자, Android: 18자 이상 말줄임 처리, iOS : 21자 이상 말줄임 처리) |
| templates[].content.templateHeader | String | 템플릿 헤더, 변수 입력 가능 |
| templates[].content.templateItem | Object |  |
| templates[].content.templateItem.list | Array |  |
| templates[].content.templateItem.summary | Object |  |
| templates[].content.templateItem.summary.title | String | 요약 타이틀 |
| templates[].content.templateItem.summary.description | String | 요약 설명(변수 및 화폐 단위, 숫자, 쉼표, 마침표만 사용 가능) |
| templates[].content.templateItemHighlight | Object |  |
| templates[].content.templateItemHighlight.title | String | 아이템 하이라이트 타이틀(최대 30자, 섬네일 이미지가 있을 경우, 21자) |
| templates[].content.templateItemHighlight.description | String | 아이템 하이라이트 설명(최대 19자, 섬네일 이미지가 있을 경우, 13자) |
| templates[].content.templateItemHighlight.attachmentId | String | 템플릿 첨부 파일 ID |
| templates[].content.templateItemHighlight.imageUrl | String | 섬네일 이미지 주소 |
| templates[].content.templateRepresentLink | Object |  |
| templates[].content.templateRepresentLink.linkMo | String | 대표 링크 모바일 웹 링크 |
| templates[].content.templateRepresentLink.linkPc | String | 대표 링크 PC 웹 링크 |
| templates[].content.templateRepresentLink.schemeIos | String | 대표 링크 iOS 앱 링크 |
| templates[].content.templateRepresentLink.schemeAndroid | String | 대표 링크 안드로이드 앱 링크 |
| templates[].content.attachmentId | String | 템플릿 첨부 파일 ID |
| templates[].content.templateImageName | String | 템플릿 이미지 이름 |
| templates[].content.templateImageUrl | String | 템플릿 이미지 링크 |
| templates[].content.securityFlag | Boolean | 템플릿 보안 여부(default: false) |
| templates[].content.categoryCode | String | 템플릿 카테고리 코드(템플릿 카테고리 조회 API 참고, default: 999999) |
| templates[].content.buttons | Array | 템플릿 버튼 |
| templates[].content.quickReplies | Array | 템플릿 바로 연결 |
| templates[].createdDateTime | String | 템플릿 생성 시각 |
| templates[].updatedDateTime | String | 템플릿 수정된 시각 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| categories | Array |  |
| categories[].name | String | 대분류 카테고리 이름 |
| categories[].subCategories | Array | 서브 카테고리 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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
| messagePurpose | String | N | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| template | Object |  |
| template.templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |
| template.templateName | String | 템플릿 이름 |
| template.categoryId | String | 카테고리 아이디 |
| template.messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array |  |
| template.templateLanguage | String | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object |  |
| template.sender.senderMailAddress | String | 발신 메일 주소 |
| template.content | Object |  |
| template.content.title | String | 템플릿 메일 제목 |
| template.content.body | String | 템플릿 메일 본문 |
| template.content.attachmentIds | Array | 템플릿 첨부 파일 ID |
| template.createdDateTime | String | 템플릿 생성 시각 |
| template.updatedDateTime | String | 템플릿 수정된 시각 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | 총 건수 |
| templates | Array |  |
| templates[].templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | 템플릿명 |
| templates[].categoryId | String | 카테고리 아이디 |
| templates[].messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | 템플릿 생성 시각 |
| templates[].updatedDateTime | String | 템플릿 수정된 시각 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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
| messagePurpose | String | N | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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
| messagePurpose | String | N | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | Y |  |
| sender.brandId | String | Y | 브랜드 아이디 |
| sender.chatbotId | String | Y | 대화방(챗봇) 아이디 |
| content | Object | Y |  |
| content.messageType | String | N | RCS 발송 메시지 유형<br>[SMS, LMS, MMS, RBC_TEMPLATE] |
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | 총 건수 |
| templates | Array |  |
| templates[].templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | 템플릿명 |
| templates[].categoryId | String | 카테고리 아이디 |
| templates[].messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | 템플릿 생성 시각 |
| templates[].updatedDateTime | String | 템플릿 수정된 시각 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| template | Object |  |
| template.templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |
| template.templateName | String | 템플릿 이름 |
| template.categoryId | String | 카테고리 아이디 |
| template.messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array |  |
| template.templateLanguage | String | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object |  |
| template.sender.brandId | String | 브랜드 아이디 |
| template.sender.chatbotId | String | 대화방(챗봇) 아이디 |
| template.content | Object |  |
| template.content.messageType | String | RCS 발송 메시지 유형<br>[SMS, LMS, MMS, RBC_TEMPLATE] |
| template.content.title | String | 메시지 제목 |
| template.content.body | String | 메시지 본문 |
| template.content.smsType | String | SMS 타입<br>[STANDALONE] |
| template.content.lmsType | String | LMS 타입<br>[STANDALONE, FORMAT_BASIC, FORMAT_TITLE_HIGHLIGHT, FORMAT_PARAGRAPH] |
| template.content.mmsType | String | MMS 타입(MMS 발송일 경우 필수)<br>[HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL] |
| template.content.messagebaseId | String | RCS Biz Center 템플릿 아이디 |
| template.content.messagebaseformId | String | RCS Biz Center 에서 지정한 messageBase 양식<br><br>[SS000000(기본형), SL000000(기본형), OL00000001(LMS Format 기본형), OL00000002(LMS Format 타이틀 강조형), OL00000003(LMS Format 문단형), SMwThT00(MMS 세로형), SMwThM00(MMS 가로형), CMwMhM0200(MMS 슬라이드 중간형(2)), CMwMhM0300(MMS 슬라이드 중간형(3)), CMwMhM0400(MMS 슬라이드 중간형(4)), CMwMhM0500(MMS 슬라이드 중간형(5)), CMwMhM0600(MMS 슬라이드 중간형(6)), CMwShS0200(MMS 슬라이드 작은형(2)), CMwShS0300(MMS 슬라이드 작은형(3)), CMwShS0400(MMS 슬라이드 작은형(4)), CMwShS0500(MMS 슬라이드 작은형(5)), CMwShS0600(MMS 슬라이드 작은형(6)), CLI00001(아이템 상세형), ITTBNV(썸네일형(세로)), ITTBNH(썸네일형(가로)), ITHIMS(이미지 강조형(1:1)), ITHIMV(이미지 강조형(3:4)), ITSNSS(SNS형), ITSNSH(SNS형(중간버튼)), ITHITS(이미지 & 타이틀 강조형(1:1)), ITHITV(이미지 & 타이틀 강조형(3:4)), ITCRM2(슬라이드 형(2)), ITCRM3(슬라이드 형(3)), ITCRM4(슬라이드 형(4)), ITCRM5(슬라이드 형(5)), ITCRM6(슬라이드 형(6)), CLT00001(아이템 강조형 DESC), CLT00002(아이템 강조형 TABLE), TATA001C(타이틀 자유형 FREE), TATA001D(타이틀 자유형 CELL), TATA001F(타이틀 자유형 DESC), FF005C(타이틀 선택형 FREE), FF005D(명세서 CELL), FF004C(명세서 DESC), FF004D(취소 CELL), GG003C(취소 DESC), GG003D(안내 CELL), GG002C(안내 DESC), GG002D(인증 CELL), GG001C(인증 DESC), GG001D(회원 가입 CELL), GG000F(회원 가입 DESC), EE001C(예약 CELL), EE001D(예약 DESC), CC003C(배송 CELL), CC003D(배송 DESC), FF002C(입금 CELL), FF002D(입금 DESC), FF001C(승인 CELL), FF001D(승인 DESC), CC002C(주문 CELL), CC002D(주문 DESC), CC001C(출고 CELL), CC001D(출고 DESC), FF003C(출금 CELL), FF003D(출금 DESC), CLL00001(LMS 명세서 A), CLL00002(LMS 문단형), CLL00003(LMS 타이들 강조형), CLL00004(LMS 기본형), CLL00005(LMS 명세서 B), CLL00006(LMS 명세서 C)] |
| template.content.unsubscribePhoneNumber | String | 수신 거부 번호(광고 발송일 경우 필수) |
| template.content.cards | Array | RCS 카드 |
| template.content.cards[].title | String | 제목 |
| template.content.cards[].description | String | 본문 |
| template.content.cards[].attachmentId | String | 이미지 첨부 파일 아이디 |
| template.content.cards[].mTitle | String | 메인 타이틀 |
| template.content.cards[].mTitleMedia | String | 메인 타이틀 로고 파일 ID |
| template.content.cards[].title1 | String | 제목 1 |
| template.content.cards[].title2 | String | 제목 2 |
| template.content.cards[].title3 | String | 제목 3 |
| template.content.cards[].description1 | String | 본문 1 |
| template.content.cards[].description2 | String | 본문 2 |
| template.content.cards[].description3 | String | 본문 3 |
| template.content.cards[].buttons | Array |  |
| template.content.buttons | Array | RCS 버튼 리스트 |
| template.content.buttons[].buttonType | String | buttonType 값과 동일한 이름을 가진 Action 객체가 buttonJson으로 포함됨.<br>버튼 타입 대화방 열기(COMPOSE), 복사하기(CLIPBOARD), 전화 걸기(DIALER), 지도 보여주기(MAP_SHOW), 지도 검색하기(MAP_QUERY), 현재 위치 공유하기(MAP_SHARE), URL 연결하기(URL), 일정 등록하기(CALENDAR)<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| template.content.buttons[].buttonJson | Object |  |
| template.content.buttons[].buttonJson.action | Object | 버튼 액션 |
| template.additionalProperty | Object |  |
| template.additionalProperty.status | String | 템플릿 상태<br>- SAVE: 저장<br>- APPROVE_WAIT: 승인 대기<br>- INSPECTION_START: 검수 시작<br>- INSPECTION_FINISH: 검수 완료<br>- APPROVE: 승인<br>- REJECT: 거부<br>- MODIFY_APPROVE_WAIT: 수정 승인 대기<br>- MODIFY_INSPECTION_START: 수정 검수 시작<br>- MODIFY_INSPECTION_FINISH: 수정 검수 완료<br>- MODIFY_REJECT: 수정 거부<br><br>[SAVE, APPROVE_WAIT, INSPECTION_START, INSPECTION_FINISH, APPROVE, REJECT, MODIFY_APPROVE_WAIT, MODIFY_INSPECTION_START, MODIFY_INSPECTION_FINISH, MODIFY_REJECT] |
| template.additionalProperty.approvedDateTime | String | 템플릿 승인 시각 |
| template.createdDateTime | String | 템플릿 생성 시각 |
| template.updatedDateTime | String | 템플릿 수정된 시각 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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
| messagePurpose | String | N | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.brandId | String | Y | 브랜드 아이디 |
| sender.chatbotId | String | Y | 대화방(챗봇) 아이디 |
| content | Object | Y |  |
| content.messageType | String | N | RCS 발송 메시지 유형<br>[SMS, LMS, MMS, RBC_TEMPLATE] |
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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
| messagePurpose | String | N | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | 총 건수 |
| templates | Array |  |
| templates[].templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |
| templates[].templateName | String | 템플릿명 |
| templates[].categoryId | String | 카테고리 아이디 |
| templates[].messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | 템플릿 생성 시각 |
| templates[].updatedDateTime | String | 템플릿 수정된 시각 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| template | Object |  |
| template.templateId | String | 템플릿 등록 시, 발급된 템플릿 아이디 |
| template.templateName | String | 템플릿 이름 |
| template.categoryId | String | 카테고리 아이디 |
| template.messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array |  |
| template.templateLanguage | String | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.content | Object | 푸시 메시지 내용 |
| template.createdDateTime | String | 템플릿 생성 시각 |
| template.updatedDateTime | String | 템플릿 수정된 시각 |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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
| messagePurpose | String | N | 발송 내용 유형<br>기본값: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | 템플릿 타입<br>기본값: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
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
| messageChannel | Path  | String | Y | 메시지 채널입니다.<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| templateParameter | Object | 템플릿 파라미터 결과 JSON |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>