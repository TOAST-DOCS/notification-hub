<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>연락처별 수신 결과</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 연락처별 수신 결과**



<span id="contactDeliveryResultV1x0001ReadContactDeliveryResults"></span>

## 연락처별 수신 결과 목록 조회

발송 요청된 메시지의 발송과 수신 결과를 수신자의 연락처 단위로 조회합니다.

예를 들어, 이메일과 전화번호를 가진 수신자 10명에게 이메일, SMS 템플릿으로 구성된 플로우 메시지 2개를 발송하는 경우, 연락처별 수신 결과 목록을 조회하면 40개의 항목이 조회됩니다. (연락처 2개 X 수신자 10명 X 플로우 메시지 2개 = 연락처별 수신 결과 40개)
다양한 검색 조건으로 연락처별 수신 결과를 조회할 수 있습니다.


**요청**

```
GET /message/v1.0/contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageId | Query  | String | N | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |
| templateId | Query  | String | N | 템플릿 아이디입니다. |
| flowId | Query  | String | N | 플로우 아이디입니다. |
| statsKeyId | Query  | String | N | 통계 키 아이디입니다. |
| sender | Query  | String | N | 발신자 정보입니다. |
| contact | Query  | String | N | 연락처입니다. |
| messageChannel | Query  | String | N | 메시지 채널입니다. |
| messagePurpose | Query  | String | N | 메시지 목적입니다. |
| statuses | Query  | String | N | 메시지 상태 입니다. 발송 결과로 볼 수 있습니다.<br> 메시지 발송 요청을 받으면 메시지 상태가 REQUESTED로 설정됩니다.<br>  |
| scheduled | Query  | Boolean | N | 예약 발송 여부입니다. |
| confirmBeforeSend | Query  | Boolean | N | 승인 후 발송 여부입니다. |
| createdDateTimeFrom | Query  | Date | N | 요청 시작 일시입니다. 기본값은 7일 전입니다. |
| createdDateTimeTo | Query  | Date | N | 요청 종료 일시입니다. 기본값은 현재 일시입니다. |
| limit | Query  | Integer | N | 조회할 메시지 수입니다. 기본값은 10입니다. |
| offset | Query  | Integer | N | 조회할 메시지의 시작 위치입니다. 기본값은 0입니다. |

* **createdDateTimeFrom**과 **createdDateTimeTo**의 최대 조회 기간은 7일입니다.


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
  "contactDeliveryResults" : [ {
    "messageId" : "메시지의 아이디",
    "recipientIndex" : 0,
    "contactIndex" : 0,
    "contactType" : "PHONE_NUMBER",
    "contact" : "01012345678",
    "sender" : {
      "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
      "senderProfileId" : "@nhnCloud",
      "senderProfileType" : "GROUP",
      "senderPhoneNumber" : "01012341234",
      "senderMailAddress" : "abcde@nhn.com",
      "brandId" : "AR.lj0eOjEI7Y",
      "chatbotId" : "01012341234"
    },
    "templateId" : "템플릿의 아이디",
    "flowId" : "플로우의 아이디",
    "statsKeyId" : "통계 키의 아이디",
    "clientReference" : "사용자 지정 필드",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "confirmBeforeSend" : false,
    "confirmedDateTime" : "2025-03-21T16:08:26.150+09:00",
    "scheduled" : false,
    "scheduledDateTime" : "2025-03-21T16:08:26.150+09:00",
    "status" : "REQUESTED",
    "resultCode" : "5.0.0",
    "resultMessage" : "Success",
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    },
    "additionalProperty" : { },
    "createdDateTime" : "2025-03-21T16:08:26.152+09:00",
    "sentDateTime" : "2025-03-21T16:08:26.152+09:00",
    "deliveredDateTime" : "2025-03-21T16:08:26.152+09:00",
    "openedDateTime" : "2025-03-21T16:08:26.152+09:00",
    "updatedDateTime" : "2025-03-21T16:08:26.152+09:00"
  } ],
  "totalCount" : 1
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| contactDeliveryResults | Array | 메시지 발송 결과입니다. |
| contactDeliveryResults[].messageId | String | 메시지 ID |
| contactDeliveryResults[].recipientIndex | Integer | 수신자 인덱스입니다. |
| contactDeliveryResults[].contactIndex | Integer | 연락처 인덱스입니다. |
| contactDeliveryResults[].contactType | Object | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| contactDeliveryResults[].contact | String | 연락처입니다. |
| contactDeliveryResults[].sender | Object |  |
| contactDeliveryResults[].sender.senderKey | String | 발신프로필 발신키 |
| contactDeliveryResults[].sender.senderProfileId | String | 카카오톡 채널명 |
| contactDeliveryResults[].sender.senderProfileType | String | 발신프로필 타입<br>[GROUP, NORMAL] |
| contactDeliveryResults[].sender.senderPhoneNumber | String | 발신 번호 |
| contactDeliveryResults[].sender.senderMailAddress | String | 발신 메일 주소 |
| contactDeliveryResults[].sender.brandId | String | 브랜드 아이디 |
| contactDeliveryResults[].sender.chatbotId | String | 대화방(챗봇) 아이디 |
| contactDeliveryResults[].templateId | String | 템플릿 ID |
| contactDeliveryResults[].flowId | String | 플로우 ID |
| contactDeliveryResults[].statsKeyId | String | 통계 키 아이디 |
| contactDeliveryResults[].clientReference | String | 사용자 지정 필드 |
| contactDeliveryResults[].messageChannel | Object | 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| contactDeliveryResults[].messagePurpose | Object | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>[NORMAL, AD, AUTH] |
| contactDeliveryResults[].confirmBeforeSend | Boolean | 확인 후 발송 여부입니다. |
| contactDeliveryResults[].confirmedDateTime | String | 메시지 발송 확인 시각입니다. |
| contactDeliveryResults[].scheduled | Boolean | 예약 발송 여부입니다. |
| contactDeliveryResults[].scheduledDateTime | String | 예약 발송 시각입니다. |
| contactDeliveryResults[].status | Object | 발송/수신 상태입니다.<br>[REQUESTED, CONFIRM_WAITED, WAITED, SCHEDULED, IN_PROGRESS, SENT, SEND_FAILED, DELIVERED, OPENED, DELIVERY_FAILED, CANCELED] |
| contactDeliveryResults[].resultCode | String | 발송 결과 코드입니다. 메시지 채널에 따라 값이 다릅니다. |
| contactDeliveryResults[].resultMessage | String | 발송 결과 메시지입니다. |
| contactDeliveryResults[].templateParameters | Object | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| contactDeliveryResults[].additionalProperty | Object |  |
| contactDeliveryResults[].createdDateTime | String | 메시지가 생성된 시각입니다. |
| contactDeliveryResults[].sentDateTime | String | 메시지가 발송된 시각입니다. |
| contactDeliveryResults[].deliveredDateTime | String | 메시지가 수신된 시각입니다. |
| contactDeliveryResults[].openedDateTime | String | 메시지가 열람된 시각입니다. |
| contactDeliveryResults[].updatedDateTime | String | 메시지가 수정된 시각입니다. |
| totalCount | Integer | 조회된 메시지 발송 결과의 총 개수입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 연락처별 수신 결과 목록 조회

GET {{endpoint}}/message/v1.0/contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/message/v1.0/contact-delivery-results" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="contactDeliveryResultV1x0002ReadFinalContactDeliveryResults"></span>

## 최종 발송 상태 메시지 목록 조회

발송 과정이 끝난 메시지 결과 목록을 조회합니다.<br>
최종 발송 상태에는 "SEND_FAILED(발송 실패)", "DELIVERED(수신 성공)", "DELIVERY_FAILED(수신 실패)", "CANCELED(취소)"가 있습니다.


**요청**

```
GET /message/v1.0/final-contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageId | Query  | String | N | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |
| templateId | Query  | String | N | 템플릿 아이디입니다. |
| flowId | Query  | String | N | 플로우 아이디입니다. |
| statsKeyId | Query  | String | N | 통계 키 아이디입니다. |
| sender | Query  | String | N | 발신자 정보입니다. |
| contact | Query  | String | N | 연락처입니다. |
| messageChannel | Query  | String | N | 메시지 채널입니다. |
| messagePurpose | Query  | String | N | 메시지 목적입니다. |
| scheduled | Query  | Boolean | N | 예약 발송 여부입니다. |
| confirmBeforeSend | Query  | Boolean | N | 승인 후 발송 여부입니다. |
| updatedDateTimeFrom | Query  | Date | N | 발송 상태 업데이트 시작 일시입니다. 기본값은 7일 전입니다. |
| updatedDateTimeTo | Query  | Date | N | 발송 상태 업데이트 종료 일시입니다. 기본값은 현재 일시입니다. |
| limit | Query  | Integer | N | 조회할 메시지 수입니다. 기본값은 10입니다. |
| offset | Query  | Integer | N | 조회할 메시지의 시작 위치입니다. 기본값은 0입니다. |



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
  "contactDeliveryResults" : [ {
    "messageId" : "메시지의 아이디",
    "recipientIndex" : 0,
    "contactIndex" : 0,
    "contactType" : "PHONE_NUMBER",
    "contact" : "01012345678",
    "sender" : {
      "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
      "senderProfileId" : "@nhnCloud",
      "senderProfileType" : "GROUP",
      "senderPhoneNumber" : "01012341234",
      "senderMailAddress" : "abcde@nhn.com",
      "brandId" : "AR.lj0eOjEI7Y",
      "chatbotId" : "01012341234"
    },
    "templateId" : "템플릿의 아이디",
    "flowId" : "플로우의 아이디",
    "statsKeyId" : "통계 키의 아이디",
    "clientReference" : "사용자 지정 필드",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "confirmBeforeSend" : false,
    "confirmedDateTime" : "2025-03-21T16:08:26.242+09:00",
    "scheduled" : false,
    "scheduledDateTime" : "2025-03-21T16:08:26.242+09:00",
    "status" : "REQUESTED",
    "resultCode" : "5.0.0",
    "resultMessage" : "Success",
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    },
    "additionalProperty" : { },
    "createdDateTime" : "2025-03-21T16:08:26.243+09:00",
    "sentDateTime" : "2025-03-21T16:08:26.243+09:00",
    "deliveredDateTime" : "2025-03-21T16:08:26.243+09:00",
    "openedDateTime" : "2025-03-21T16:08:26.243+09:00",
    "updatedDateTime" : "2025-03-21T16:08:26.243+09:00"
  } ],
  "totalCount" : 1
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| contactDeliveryResults | Array | 메시지 발송 결과입니다. |
| contactDeliveryResults[].messageId | String | 메시지 ID |
| contactDeliveryResults[].recipientIndex | Integer | 수신자 인덱스입니다. |
| contactDeliveryResults[].contactIndex | Integer | 연락처 인덱스입니다. |
| contactDeliveryResults[].contactType | Object | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| contactDeliveryResults[].contact | String | 연락처입니다. |
| contactDeliveryResults[].sender | Object |  |
| contactDeliveryResults[].sender.senderKey | String | 발신프로필 발신키 |
| contactDeliveryResults[].sender.senderProfileId | String | 카카오톡 채널명 |
| contactDeliveryResults[].sender.senderProfileType | String | 발신프로필 타입<br>[GROUP, NORMAL] |
| contactDeliveryResults[].sender.senderPhoneNumber | String | 발신 번호 |
| contactDeliveryResults[].sender.senderMailAddress | String | 발신 메일 주소 |
| contactDeliveryResults[].sender.brandId | String | 브랜드 아이디 |
| contactDeliveryResults[].sender.chatbotId | String | 대화방(챗봇) 아이디 |
| contactDeliveryResults[].templateId | String | 템플릿 ID |
| contactDeliveryResults[].flowId | String | 플로우 ID |
| contactDeliveryResults[].statsKeyId | String | 통계 키 아이디 |
| contactDeliveryResults[].clientReference | String | 사용자 지정 필드 |
| contactDeliveryResults[].messageChannel | Object | 메시지 채널<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| contactDeliveryResults[].messagePurpose | Object | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>[NORMAL, AD, AUTH] |
| contactDeliveryResults[].confirmBeforeSend | Boolean | 확인 후 발송 여부입니다. |
| contactDeliveryResults[].confirmedDateTime | String | 메시지 발송 확인 시각입니다. |
| contactDeliveryResults[].scheduled | Boolean | 예약 발송 여부입니다. |
| contactDeliveryResults[].scheduledDateTime | String | 예약 발송 시각입니다. |
| contactDeliveryResults[].status | Object | 발송/수신 상태입니다.<br>[REQUESTED, CONFIRM_WAITED, WAITED, SCHEDULED, IN_PROGRESS, SENT, SEND_FAILED, DELIVERED, OPENED, DELIVERY_FAILED, CANCELED] |
| contactDeliveryResults[].resultCode | String | 발송 결과 코드입니다. 메시지 채널에 따라 값이 다릅니다. |
| contactDeliveryResults[].resultMessage | String | 발송 결과 메시지입니다. |
| contactDeliveryResults[].templateParameters | Object | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| contactDeliveryResults[].additionalProperty | Object |  |
| contactDeliveryResults[].createdDateTime | String | 메시지가 생성된 시각입니다. |
| contactDeliveryResults[].sentDateTime | String | 메시지가 발송된 시각입니다. |
| contactDeliveryResults[].deliveredDateTime | String | 메시지가 수신된 시각입니다. |
| contactDeliveryResults[].openedDateTime | String | 메시지가 열람된 시각입니다. |
| contactDeliveryResults[].updatedDateTime | String | 메시지가 수정된 시각입니다. |
| totalCount | Integer | 조회된 메시지 발송 결과의 총 개수입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 최종 발송 상태 메시지 목록 조회

GET {{endpoint}}/message/v1.0/final-contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/message/v1.0/final-contact-delivery-results" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>