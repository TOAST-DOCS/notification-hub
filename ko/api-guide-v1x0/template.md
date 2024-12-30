<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>템플릿</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 템플릿**

## 템플릿

<span id="create-template"></span>

### 템플릿 생성

**요청**

```
POST /template/v1.0/{messageChannel}/templates
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |

**요청 본문**

```json
{
  "templateName": "템플릿_이름",
  "categoryId": "템플릿_카테고리_아이디",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "content": {
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub] 공지사항",
    "body": "안녕하세요. NHN Cloud Notification Hub 입니다.",
    "attachmentIds": [
      "첨부_파일_아이디"
    ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 이름 | 타입 | 필수 | 설명                                |
| --- | --- | --- |-----------------------------------|
| templateName | String | Y | 템플릿 이름                            |
| categoryId | String | Y | 템플릿 카테고리 아이디                      |
| messagePurpose | String | Y | 메시지 목적                            |
| templateLanguage | String | Y | 템플릿 언어<br>PLAIN_TEXT, FREE_MARKER |
| sender | Object | Y | 발신자                               |
| content | Object | Y | 내용                                |

* 템플릿 카테고리는 템플릿 카테고리 API를 이용해 생성할 수 있습니다.
* 템플릿 언어는 PLAIN_TEXT, FREE_MARKER 중 하나를 선택합니다.
* 템플릿 언어가 FREE_MARKER인 경우 템플릿 내용에 FREE_MARKER 문법을 사용할 수 있습니다.
* **sender**, **content** 필드는 전문 메시지 발송 API의 요청 본문과 동일합니다.

#### 메시지 채널별 sender 필드

| 메시지 채널 | 필드 | 설명                        |
| --- | --- |---------------------------|
| SMS | sender.senderPhoneNumber | 발신자 번호                    |
| RCS | sender.brandId | 브랜드 아이디                   |
| RCS | sender.chatbotId | 대화방 아이디                   |
| EMAIL | sender.senderMailAddress | 발신자 이메일 주소                |
| ALIMTALK, FRIENDTALK | sender.senderKey | 발신키                       |
| ALIMTALK | sender.senderProfileType | 발신 프로필 유형<br>GROUP, NORMAL |

* 알림톡(ALIMTALK)은 발신 키(senderKey)와 발신 프로필 유형(senderProfileType)을 필수로 입력해야 합니다.
* 친구톡(FRIENDTALK)은 NORMAL(일반) 발신 프로필 유형만 사용할 수 있습니다. GROUP(그룹) 발신 프로필 유형의 발신 키를 사용하면 발송에 실패합니다.
* 발신자 프로필 유형은 **GROUP(그룹)**과 **NORMAL(일반)**이 있습니다. **GROUP**은 그룹 발신자 프로필, **NORMAL**은 일반 발신자 프로필입니다.

### 알림톡 템플릿 상세 요청 본문

* 알림톡은 발송을 위해서 템플릿 등록이 필수 입니다.
* 알림톡 템플릿을 등록하면 카카오비즈니스의 검수와 승인 과정을 거치고 승인 완료 후에 사용할 수 있습니다.
* 알림톡 템플릿은 검수와 승인 과정에서 카카오비즈니스 검수 담당자와 문의를 주고 받을 수 있습니다.
    * [카카오톡채널 관리자센터 바로 가기](https://center-pf.kakao.com)
    * 알림톡 템플릿은 **알림톡 템플릿 문의하기**, **알림톡 템플릿 파일 첨부 문의하기**, **알림톡 템플릿 수정 내역 조회** API를 추가로 제공합니다.

```json
{
  "templateName": "템플릿 이름",
  "categoryId": "카테고리_아이디",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderKey": "발신_키",
    "senderProfileType": "GROUP"
  },
  "content": {
    "templateMessageType": "BA",
    "templateEmphasizeType": "NONE",
    "templateContent": "#{이름}님의 주문이 완료되었습니다.",
    "templateAd": "채널 추가하고 이 채널의 마케팅 메시지 등을 카카오톡으로 받기",
    "templateExtra": "* 실시간 예약 특성상 중복 예약이 발생할 수 있으며, 입실이 불가할 경우 예약이 취소될 수 있습니다.\\n* 문의전화: 1234-1234",
    "templateTitle": "123,450원",
    "templateSubtitle": "승인 내역",
    "templateHeader": "주문이 체결되었습니다.",
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

| 이름 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- |

<!--TODO: 요청 본문의 필드를 설명합니다.-->


**응답 본문**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "templateId": "템플릿_아이디"
}
```

<!--응답 본문의 필드를 설명합니다.-->

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 생성
POST {{endpoint}}/template/v1.0/{{messageChannel}}/templates
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "templateName": "템플릿_이름",
  "categoryId": "템플릿_카테고리_아이디",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "content": {
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub] 공지사항",
    "body": "안녕하세요. NHN Cloud Notification Hub 입니다.",
    "attachmentIds": [
      "첨부_파일_아이디"
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
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
        "templateName": "템플릿_이름",
        "categoryId": "템플릿_카테고리_아이디",
        "messagePurpose": "NORMAL",
        "templateLanguage": "PLAIN_TEXT",
        "sender": {
          "senderPhoneNumber": "01012341234"
        },
        "content": {
          "messageType": "MMS",
          "title": "[NHN Cloud Notification Hub] 공지사항",
          "body": "안녕하세요. NHN Cloud Notification Hub 입니다.",
          "attachmentIds": [
            "첨부_파일_아이디"
          ]
        }
      }'
```

</details>

<span id="get-templates"></span>

### 템플릿 목록 조회

**요청**

```
GET /template/v1.0/{messageChannel}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름           | 구분 | 타입 | 필수 | 설명                        |
|--------------| --- | --- | --- |---------------------------|
| appKey       | Header | String | Y | 앱키                        |
| accessToken  | Header | String | Y | 인증 토큰                     |
| templateName | Query | String | N | 템플릿 이름, 접두사(Prefix) 검색 가능 |
| limit        | Query | Integer | N | 조회 개수(기본값: 20)            |
| offset       | Query | Integer | N | 조회 시작 위치(기본값: 0)          |

**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.

**응답 본문**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "templates": [
    {
      "templateId": "템플릿_아이디",
      "templateName": "템플릿_이름",
      "categoryId": "템플릿_카테고리_아이디",
      "messagePurpose": "NORMAL",
      "templateLanguage": "PLAIN_TEXT",
      "sender": {
        "senderPhoneNumber": "01012341234"
      },
      "content": {
        "messageType": "MMS",
        "title": "[NHN Cloud Notification Hub] 공지사항",
        "body": "안녕하세요. NHN Cloud Notification Hub 입니다.",
        "attachmentIds": [
          "첨부_파일_아이디"
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

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 목록 조회
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

### 템플릿 조회

**요청**

```
GET /template/v1.0/{messageChannel}/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| templateId | Path | String | Y | 템플릿 아이디 |

**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.

**응답 본문**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "template": {
    "templateId": "템플릿_아이디",
    "templateName": "템플릿_이름",
    "categoryId": "템플릿_카테고리_아이디",
    "messagePurpose": "NORMAL",
    "templateLanguage": "PLAIN_TEXT",
    "sender": {
      "senderPhoneNumber": "01012341234"
    },
    "content": {
      "messageType": "MMS",
      "title": "[NHN Cloud Notification Hub] 공지사항",
      "body": "안녕하세요. NHN Cloud Notification Hub 입니다.",
      "attachmentIds": [
        "첨부_파일_아이디"
      ]
    },
    "createdDateTime": "2023-01-01T00:00:00Z",
    "updatedDateTime": "2023-01-01T00:00:00Z"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 조회
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

### 템플릿 수정

**요청**

```
PUT /template/v1.0/{messageChannel}/templates/{templateId}
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| templateId | Path | String | Y | 템플릿 아이디 |

**요청 본문**

```json
{
  "templateName": "템플릿_이름",
  "categoryId": "템플릿_카테고리_아이디",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "content": {
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub] 공지사항",
    "body": "안녕하세요. NHN Cloud Notification Hub 입니다.",
    "attachmentIds": [
      "첨부_파일_아이디"
    ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

**응답 본문**

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

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 수정
PUT {{endpoint}}/template/v1.0/{{messageChannel}}/templates/{templateId}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "templateName": "템플릿_이름",
  "categoryId": "템플릿_카테고리_아이디",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "content": {
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub] 공지사항",
    "body": "안녕하세요. NHN Cloud Notification Hub 입니다.",
    "attachmentIds": [
      "첨부_파일_아이디"
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
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
        "templateName": "템플릿_이름",
        "categoryId": "템플릿_카테고리_아이디",
        "messagePurpose": "NORMAL",
        "templateLanguage": "PLAIN_TEXT",
        "sender": {
          "senderPhoneNumber": "01012341234"
        },
        "content": {
          "messageType": "MMS",
          "title": "[NHN Cloud Notification Hub] 공지사항",
          "body": "안녕하세요. NHN Cloud Notification Hub 입니다.",
          "attachmentIds": [
            "첨부_파일_아이디"
          ]
        }
      }'
```

</details>

<span id="delete-template"></span>

### 템플릿 삭제

**요청**

```
DELETE /template/v1.0/{messageChannel}/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| templateId | Path | String | Y | 템플릿 아이디 |

**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.

**응답 본문**

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

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 삭제
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

### 알림톡 템플릿 문의하기

**요청**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/inquiries
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| templateId | Path | String | Y | 템플릿 아이디 |

**요청 본문**

```json
{
  "comment": "문의 내용"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 이름 | 타입 | 필수 | 설명                |
| --- | --- | --- |-------------------|
| comment | String | Y | 문의 내용(최대 길이: 500) |

**응답 본문**

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

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 문의하기
POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{templateId}/inquiries
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "comment": "문의 내용"
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/template/v1.0/ALIMTALK/templates/${TEMPLATE_ID}/inquiries" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
        "comment": "문의 내용"
      }'
```

</details>

### 알림톡 템플릿 파일 첨부 문의하기

**요청**

```
POST /template/v1.0/ALIMTALK/templates/${TEMPLATE_ID}/inquiries/do-with-file
Content-Type: multipart/form-data
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| templateId | Path | String | Y | 템플릿 아이디 |
| comment | Query | String | Y | 문의 내용(최대 길이: 500) |

**요청 본문**

* 파일 첨부는 **multipart/form-data**로 요청합니다.
* **form-data**에 **file** 필드에 파일 데이터를 설정합니다.

```
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="file"; filename="attachment.xlsx"
Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet

<파일 데이터>
------WebKitFormBoundary7MA4YWxkTrZu0gW--
```

**응답 본문**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 파일 첨부 문의하기
POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{templateId}/inquiries/do-with-file?fileName=attachment.xlsx
Content-Type: multipart/form-data
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

--boundary
Content-Disposition: form-data; name="file"; fileName="attachment.xlsx"
Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet


< ./file/attachment.xlsx
--boundary--
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

### 알림톡 템플릿 수정 내역 조회

**요청**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}/modifications
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| templateId | Path | String | Y | 템플릿 아이디 |

**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.

**응답 본문**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "templates": [
    {
      "templateId": "템플릿_아이디",
      "templateName": "템플릿_이름",
      "categoryId": "템플릿_카테고리_아이디",
      "messageChannel": "ALIMTALK",
      "messagePurpose": "NORMAL",
      "templateLanguage": "PLAIN_TEXT",
      "sender": {
        "senderKey": "발신자_키",
        "senderProfileId": "발신자_프로필_아이디",
        "senderProfileType": "GROUP"
      },
      "content": {
          "templateMessageType": "BA",
          "templateEmphasizeType": "NONE",
          "templateContent": "#{이름}님의 주문이 완료되었습니다.",
            "templateAd": "채널 추가하고 이 채널의 마케팅 메시지 등을 카카오톡으로 받기",
            "templateExtra": "* 실시간 예약 특성상 중복 예약이 발생할 수 있으며, 입실이 불가할 경우 예약이 취소될 수 있습니다.\\n* 문의전화: 1234-1234",
            "templateTitle": "123,450원",
            "templateSubtitle": "승인 내역",
            "templateHeader": "주문이 체결되었습니다.",
            "templateItem": {
              "list": [
                {
                "title": "제목",
                "description": "설명"
                }
              ],
              "summary": {
                "title": "제목",
                "description": "설명"
              }
            },
            "templateItemHighlight": {
              "title": "제목",
              "description": "설명",
              "attachmentId": "하이라이트_이미_첨부파일_아이디",
              "imageUrl": "하이라이트_이미지_링크"
            },
            "templateRepresentLink": {
              "linkMo": "모바일_링크",
              "linkPc": "PC_링크",
              "schemeIos": "iOS_링크",
              "schemeAndroid": "안드로이드_링크"
            },
            "attachmentId": "첨부_파일_아이디",
            "templateImageName": "이미지_파일_이름",
            "templateImageUrl": "이미지_링크",
            "securityFlag": false,
            "categoryCode": "999999",
            "buttons": [
              {
                "ordering": 1,
                "type": "WL",
                "name": "버튼_이름",
                "linkMo": "모바일_링크",
                "linkPc": "PC_링크",
                "schemeIos": "iOS_링크",
                "schemeAndroid": "안드로이드_링크",
                "bizFormId": 1
              }
            ],
            "quickReplies": [
              {
                "ordering": 1,
                "type": "WL",
                "name": "버튼_이름",
                "linkMo": "모바일_링크",
                "linkPc": "PC_링크",
                "schemeIos": "iOS_링크",
                "schemeAndroid": "안드로이드_링크",
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

| 이름 | 타입            | 설명                |
| --- |---------------| ------------------|
| templateCode         | String        | 템플릿 코드(최대 20자) |
| templateName         | String        | 템플릿명(최대 150자) |
| templateContent      | String        | 템플릿 본문(최대 1000자) |
| templateMessageType  | String        | 템플릿 메시지 유형<br>BA: 기본형, EX: 부가 정보형, AD: 채널 추가형, MI: 복합형 (기본값: BA) |
| templateEmphasizeType| String        | 템플릿 강조 표시 타입<br>NONE: 기본, TEXT: 강조 표시, IMAGE: 이미지형, ITEM_LIST: 아이템리스트형 (기본값: NONE)<br>- TEXT 선택 시: templateTitle, templateSubtitle 필수<br>- IMAGE 선택 시: templateImageName, templateImageUrl 필수<br>- ITEM_LIST 선택 시: 이미지, 헤더, 아이템 하이라이트, 아이템 리스트 중 1개 이상 필수 |
| templateExtra        | String        | 템플릿 부가 정보<br>템플릿 메시지 유형이 부가 정보형 또는 복합형일 경우 필수 |
| templateTitle        | String        | 템플릿 제목(최대 50자)<br>Android: 2줄, 23자 이상일 때 말줄임 처리<br>iOS: 2줄, 27자 이상일 때 말줄임 처리 |
| templateSubtitle     | String        | 템플릿 보조 문구(최대 50자)<br>Android: 18자 이상일 때 말줄임 처리<br>iOS: 21자 이상일 때 말줄임 처리 |
| templateHeader       | String        | 템플릿 헤더(최대 16자) |
| templateItem         | Object        | 아이템 |
| templateItem.list    | Object Array | 아이템 리스트(최소 2개, 최대 10개) |
| templateItem.list.title | String        | 타이틀(최대 6자) |
| templateItem.list.description | String        | 디스크립션(최대 23자) |
| templateItem.summary | Object        | 아이템 요약 정보 |
| templateItem.summary.title | String        | 타이틀(최대 6자) |
| templateItem.summary.description | String        | 디스크립션(변수 및 화폐 단위, 숫자, 쉼표, 마침표만 사용 가능, 최대 14자) |
| templateItemHighlight | Object        | 아이템 하이라이트 |
| templateItemHighlight.title | String        | 타이틀(최대 30자, 섬네일 이미지가 있을 경우 21자) |
| templateItemHighlight.description | String        | 디스크립션(최대 19자, 섬네일 이미지가 있을 경우 13자) |
| templateItemHighlight.imageUrl | String        | 섬네일 이미지 주소 |
| templateRepresentLink | Object        | 대표 링크 |
| templateRepresentLink.linkMo | String        | 모바일 웹 링크(최대 500자) |
| templateRepresentLink.linkPc | String        | PC 웹 링크(최대 500자) |
| templateRepresentLink.schemeIos | String        | iOS 앱 링크(최대 500자) |
| templateRepresentLink.schemeAndroid | String        | 안드로이드 앱 링크(최대 500자) |
| templateImageName   | String        | 이미지명(업로드한 파일명) |
| templateImageUrl    | String        | 이미지 URL |
| securityFlag        | Boolean       | 보안 템플릿 여부<br>OTP 등 보안 메시지일 경우 설정<br>발신 당시 메인 디바이스 외 다른 디바이스에 메시지 텍스트 미노출 (기본값: false) |
| categoryCode        | String        | 템플릿 카테고리 코드 (템플릿 카테고리 조회 API 참고, 기본값: 999999)<br>카테고리 기타일 경우 최하위 우선순위로 심사 |
| buttons             | Object Array | 버튼 리스트(최대 5개) |
| buttons[].ordering    | Integer       | 버튼 순서(1~5) |
| buttons[].type        | String        | 버튼 타입<br>WL: 웹 링크, AL: 앱 링크, DS: 배송 조회, BK: 봇 키워드, MD: 메시지 전달, BC: 상담톡 전환, BT: 봇 전환, AC: 채널 추가, BF: 비즈니스폼, P1: 이미지 보안 전송 플러그인 ID, P2: 개인정보이용 플러그인 ID, P3: 원클릭 결제 플러그인 ID |
| buttons[].name        | String        | 버튼 이름 (버튼이 있는 경우 필수, 최대 14자) |
| buttons[].linkMo      | String        | 모바일 웹 링크 (WL 타입일 경우 필수 필드, 최대 500자) |
| buttons[].linkPc      | String        | PC 웹 링크 (WL 타입일 경우 선택 필드, 최대 500자) |
| buttons[].schemeIos   | String        | iOS 앱 링크 (AL 타입일 경우 필수 필드, 최대 500자) |
| buttons[].schemeAndroid | String        | 안드로이드 앱 링크 (AL 타입일 경우 필수 필드, 최대 500자) |
| buttons[].bizFormId   | Integer       | 비즈니스폼 ID (BF 타입일 경우 필수) |
| buttons[].pluginId    | String        | 플러그인 ID (최대 24자) |
| quickReplies        | Object Array         | 바로연결 리스트 (최대 5개) |
| quickReplies[].ordering | Integer       | 바로연결 순서 (바로연결이 있는 경우 필수) |
| quickReplies[].type   | String        | 바로연결 타입<br>WL: 웹 링크, AL: 앱 링크, BK: 봇 키워드, BC: 상담톡 전환, BT: 봇 전환, BF: 비즈니스폼 |
| quickReplies[].name   | String        | 바로연결 이름 (바로연결이 있는 경우 필수, 최대 14자) |
| quickReplies[].linkMo | String        | 모바일 웹 링크 (WL 타입일 경우 필수 필드, 최대 500자) |
| quickReplies[].linkPc | String        | PC 웹 링크 (WL 타입일 경우 선택 필드, 최대 500자) |
| quickReplies[].schemeIos | String        | iOS 앱 링크 (AL 타입일 경우 필수 필드, 최대 500자) |
| quickReplies[].schemeAndroid | String        | 안드로이드 앱 링크 (AL 타입일 경우 필수 필드, 최대 500자) |
| quickReplies[].bizFormId | Integer       | 비즈니스폼 ID (BF 타입일 경우 필수) |

* 채널 추가형(AD) 또는 복합형(MI) 메시지 유형 템플릿 등록 시 templateAd 값이 고정됩니다.
* 채널 추가형(AD) 또는 복합형(MI) 메시지 유형 템플릿 등록 시 채널 추가(AC) 버튼이 첫 번째 순서에 위치해야 합니다.
* 채널 추가(AC) 버튼의 버튼명은 "채널 추가"로 고정하여 등록해야 합니다.

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 수정 내역 조회
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

### 템플릿 카테고리 생성

**요청**

```
POST /template/v1.0/{messageChannel}/categories
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| messageChannel | Path | String | Y | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |

**요청 본문**

```json
{
  "parentCategoryId": "상위_카테고리_아이디",
  "name": "카테고리_이름"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 이름 | 타입 | 필수 | 설명                |
| --- | --- | --- |-------------------|
| parentCategoryId | String | 선택 | 상위 카테고리 아이디 |
| name | String | 필수 | 카테고리 이름(최대 50자) |

* 최상위 카테고리는 기본적으로 생성되어 있습니다. 최상위 카테고리아이디는 **ROOT**입니다.
* 새로운 카테고리는 최상위 카테고리를 하위부터 생성할 수 있습니다.

**응답 본문**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "categoryId": "카테고리_아이디"
}
```

<!--응답 본문의 필드를 설명합니다.-->

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 카테고리 생성
POST {{endpoint}}/template/v1.0/{{messageChannel}}/categories
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "parentCategoryId": "상위_카테고리_아이디",
  "name": "카테고리_이름"
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
     -d '{
         "parentCategoryId": "상위_카테고리_아이디",
         "name": "카테고리_이름"
     }'
```

</details>

### 카테고리 목록 조회

**요청**

```
GET /template/v1.0/{messageChannel}/categories
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| messageChannel | Path | String | Y | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |

**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.

**응답 본문**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "categories": [
    {
      "categoryId": "카테고리_아이디",
      "name": "카테고리_이름",
      "parentCategoryId": "상위_카테고리_아이디",
      "categoryIds": [
        "하위_카테고리_아이디"
      ],
      "templateIds": [
        "카테고리에 속한 템플릿_아이디"
      ]
    }
  ]
}
```

<!--TODO: categoryIds => childCategoryIds로 이름 변경 필요-->
<!--TODO: totalCount 추가 필요-->

<!--응답 본문의 필드를 설명합니다.-->

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 카테고리 목록 조회
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

### 카테고리 트리 조회

**요청**

```
GET /template/v1.0/{messageChannel}/category-tree
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명                                                     |
| --- | --- | --- | --- |--------------------------------------------------------|
| appKey | Header | String | Y | 앱키                                                     |
| accessToken | Header | String | Y | 인증 토큰                                                  |
| messageChannel | Path | String | Y | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH  |
| categoryTemplateName | Query | String | N | 카테고리 또는 템플릿 이름, 접두사(Prefix) 검색 가능                      |
| senderProfileType | Query | String | N | 발신자 프로필 타입 (GROUP, USER), 알림톡과 친구톡만 해당됨                |
| senderKey | Query | String | N | 발신자 키, 알림톡과 친구톡만 해당됨                                   |

<!--TODO: status 필드가 없는데 필요한지 확인 필요-->

**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.

**응답 본문**

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
        {
          "categoryId": "카테고리_아이디",
          "categoryName": "카테고리_이름",
          "parentCategoryId": "ROOT",
          "messageChannel": "SMS",
          "categories": [
            {
              "categoryId": "카테고리_아이디",
              "categoryName": "카테고리_이름",
              "parentCategoryId": "6XAeH2yo",
              "messageChannel": "SMS",
              "categories": [],
              "templates": [
                {
                  "templateId": "템플릿_아이디",
                  "templateName": "템플릿_이름"
                },
                {
                  "templateId": "템플릿_아이디",
                  "templateName": "템플릿_이름"
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

| 이름                      | 타입            | 설명                |
|-------------------------|---------------|-------------------|
| categories.[]categoryId | String        | 카테고리 아이디 |
| categories.[]categoryName            | String        | 카테고리 이름 |
| categories.[]parentCategoryId        | String        | 상위 카테고리 아이디 |
| categories.[]messageChannel          | String        | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| categories.[]categories              | Object Array | 하위 카테고리 목록 |
| categories.[]templates               | Object Array         | 템플릿 목록 |
| categories.[]templates.[]templateId  | String        | 템플릿 아이디 |
| categories.[]templates.[]templateName| String        | 템플릿 이름 |

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 카테고리 트리 조회
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

### 카테고리 조회

**요청**

```
GET /template/v1.0/{messageChannel}/categories/{categoryId}
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| messageChannel | Path | String | Y | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| categoryId | Path | String | Y | 카테고리 아이디 |

**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.

**응답 본문**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "category": {
    "categoryId": "카테고리_아이디",
    "categoryName": "카테고리_이름",
    "parentCategoryId": "상위_카테고리_아이디",
    "messageChannel": "SMS",
    "categoryIds": [
      "하위_카테고리_아이디"
    ],
    "templateIds": [
      "카테고리에_속한_템플릿_아이디"
    ]
  }
}
```

<!--TODO: 카테고리 이름을 name or categoryName으로 할지 통일 필요, name으로 변경 필요-->

<!--응답 본문의 필드를 설명합니다.-->

**요청 예시**


<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 메시지 채널별 카테고리 조회
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

### 카테고리 수정

**요청**

```
PUT /template/v1.0/{messageChannel}/categories/{categoryId}
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| messageChannel | Path | String | Y | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| categoryId | Path | String | Y | 카테고리 아이디 |

**요청 본문**

```json
{
  "parentCategoryId": "상위_카테고리_아이디",
  "name": "카테고리_이름"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 이름 | 타입 | 필수 | 설명                |
| --- | --- | --- |-------------------|
| parentCategoryId | String | 선택 | 상위 카테고리 아이디 |
| name | String | 필수 | 카테고리 이름(최대 50자) |

**응답 본문**

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

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 카테고리 수정
PUT {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "parentCategoryId": "상위_카테고리_아이디",
  "name": "카테고리_이름"
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X PUT "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories/{categoryId}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
         "parentCategoryId": "상위_카테고리_아이디",
         "name": "카테고리_이름"
     }'
```

</details>

### 템플릿 카테고리에 템플릿 추가

**요청**

```
POST /template/v1.0/${MESSAGE_CHANNEL}/categories/${CATEGORY_ID}/templates
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| messageChannel | Path | String | Y | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |

**요청 본문**

```json
{
  "templateId": "템플릿_아이디"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 이름 | 타입 | 필수 | 설명                |
| --- | --- | --- |-------------------|
| templateId | String | 필수 | 템플릿 아이디 |

**응답 본문**

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

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 카테고리에 템플릿 추가
POST {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}/templates
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "templateId": "템플릿_아이디"
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories/${CATEGORY_ID}/templates" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
         "templateId": "템플릿_아이디"
     }'
```

</details>

### 카테고리 삭제

**요청**

```
DELETE /template/v1.0/{messageChannel}/categories/{categoryId}
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| messageChannel | Path | String | Y | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| categoryId | Path | String | Y | 카테고리 아이디 |

**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->
이 API는 요청 본문을 요구하지 않습니다.

**응답 본문**

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

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 카테고리 삭제
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


