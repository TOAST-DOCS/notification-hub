<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>연락처별 수신 결과</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 연락처별 수신 결과**

<span id="read-contact-delivery-results"></span>

### 연락처별 수신 결과 목록 조회

발송 요청된 메시지의 발송과 수신 결과를 수신자의 연락처 단위로 조회합니다.

예를 들어, 이메일과 전화번호를 가진 수신자 10명에게 이메일, SMS 템플릿으로 구성된 플로우 메시지 2개를 발송하는 경우, 연락처별 수신 결과 목록을 조회하면 40개의 항목이 조회됩니다. (연락처 2개 X 수신자 10명 X 플로우 메시지 2개 = 연락처 별 수신 결과 40개)
다양한 검색 조건으로 연락처 별 수신 결과를 조회할 수 있습니다.

<!-- !!! tip "알아두기"-->
<!-- API를 사용할 때 사용자가 알아 두면 좋을 참고 사항이나 추가 정보를 제공할 때 사용합니다.-->

<!-- !!! warning "주의"-->
<!--API를 사용할 때 따르지 않을 경우 서비스의 비정상 또는 비효율적 동작이 발생할 수 있는 주의 사항을 표기할 때 사용합니다.-->

**요청**

```
GET /message/v1.0/contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- |----| --- |
| appKey | Header | String | Y  | 앱키 |
| accessToken | Header | String | Y  | 인증 토큰 |
| createdDateTimeFrom | Query | DateTime(ISO 8601) | Y  | 생성 일시 시작 범위 |
| createdDateTimeTo | Query | DateTime(ISO 8601) | Y  | 생성 일시 종료 범위 |
| messageId | Query | String | N  | 메시지 아이디 |
| templateId | Query | String | N  | 템플릿 아이디 |
| flowId | Query | String | N  | 플로우 아이디 |
| statsKeyId | Query | String | N  | 통계 키 아이디 |
| sender | Query | String | N  | 발신자 |
| contact | Query | String | N  | 연락처 |
| messageChannel | Query | String | N  | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| messagePurpose | Query | String | N  | 메시지 목적 |
| status | Query | String | N  | 상태 |
| scheduled | Query | Boolean | N  | 예약 발송 여부 |
| confirmBeforeSend | Query | Boolean | N  | 발송 전 확인 여부 |
| limit | Query | Integer | N  | 조회 개수 |
| offset | Query | Integer | N  | 조회 시작 위치 |

* **createdDateTimeFrom**과 **createdDateTimeTo**의 최대 조회 기간은 7일입니다.

**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.

<!--요청 본문의 필드를 설명합니다.-->

**응답 본문**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->


```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "contactDeliveryResults": [
    {
      "messageId": "메시지의 아이디",
      "recipientIndex": 0,
      "contactIndex": 0,
      "contactType": "PHONE_NUMBER",
      "contact": "01012345678",
      "sender": {
        "senderKey": "발신_키",
        "senderProfileId": "@nhnCloud",
        "senderProfileType": "GROUP",
        "senderPhoneNumber": "01012341234",
        "senderMailAddress": "abcde@nhn.com",
        "brandId": "AR.lj0eOjEI7Y",
        "chatbotId": "01012341234"
      },
      "templateId": "템플릿의 아이디",
      "flowId": "플로우의 아이디",
      "statsKeyId": "통계 키의 아이디",
      "messageChannel": "SMS",
      "messagePurpose": "NORMAL",
      "confirmBeforeSend": false,
      "confirmedDateTime": "2023-01-01T00:00:00Z",
      "scheduled": false,
      "scheduledDateTime": "2024-10-26T07:52:12.728Z",
      "status": "REQUESTED",
      "resultCode": "5.0.0",
      "resultMessage": "Success",
      "templateParameters": {
        "key1": "value1",
        "key2": "value2"
      },
      "additionalProperty": {
        
      },
      "createdDateTime": "2023-01-01T00:00:00Z",
      "sentDateTime": "2023-01-01T00:00:00Z",
      "deliveredDateTime": "2023-01-01T00:00:00Z",
      "openedDateTime": "2023-01-01T00:00:00Z",
      "updatedDateTime": "2023-01-01T00:00:00Z"
    }
  ],
  "totalCount": 1
}
```



<!--응답 본문의 필드를 설명합니다.-->

| 이름 | 타입 | 설명 |
| --- | --- | --- |
| header.isSuccessful | Boolean | API 요청 성공 여부 |
| header.resultCode | Integer | 결과 코드 |
| header.resultMessage | String | 결과 메시지 |
| contactDeliveryResults | Object Array | 연락처별 수신 결과 목록 |
| contactDeliveryResults[].messageId | String| 메시지의 아이디 |
| contactDeliveryResults[].recipientIndex | Number| 수신자 인덱스|
| contactDeliveryResults[].contactIndex | Number| 연락처 인덱스|
| contactDeliveryResults[].contactType | String| 연락처 타입 |
| contactDeliveryResults[].contact | String| 연락처|
| contactDeliveryResults[].sender | Object| 발신자|
| contactDeliveryResults[].sender.senderKey | String| 발신 프로필 발신 키, 알림톡과 친구톡만 표시|
| contactDeliveryResults[].sender.senderProfileId | String| 발신 프로필 아이디, 알림톡과 친구톡만 표시 |
| contactDeliveryResults[].sender.senderProfileType | String| 발신 프로필 타입, 알림톡과 친구톡만 표시|
| contactDeliveryResults[].sender.senderPhoneNumber | String| 발신자 전화번호, SMS만 표시|
| contactDeliveryResults[].sender.senderMailAddress | String| 발신자 이메일 주소, 이메일만 표시|
| contactDeliveryResults[].sender.brandId | String| 브랜드 아이디, RCS만 표시 |
| contactDeliveryResults[].sender.chatbotId | String| 대화방 아이디, RCS만 표시 |
| contactDeliveryResults[].templateId | String| 템플릿의 아이디, 템플릿 메시지만 표시|
| contactDeliveryResults[].flowId | String| 플로우의 아이디, 템플릿 메시지만 표시|
| contactDeliveryResults[].statsKeyId | String| 통계 키의 아이디|
| contactDeliveryResults[].messageChannel | String| 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| contactDeliveryResults[].messagePurpose | String| 메시지 목적 |
| contactDeliveryResults[].confirmBeforeSend | Boolean | 승인 후 발송 사용 여부|
| contactDeliveryResults[].confirmedDateTime | DateTime(ISO 86091) | 승인 일시(예: 2024-10-29T06:09:00+09:00)|
| contactDeliveryResults[].scheduled | Boolean | 예약 발송 여부 |
| contactDeliveryResults[].scheduledDateTime | DateTime(ISO 86091) | 예약 발송 일시 |
| contactDeliveryResults[].status | String| 상태<br> 요청(REQUESTED), 요청 취소(CANCELED), 발송(SENT), 발송 실패(SEND_FAILED), 수신(DELIVERED), 수신 실패(DELIVERY_FAILED)  |
| contactDeliveryResults[].resultCode | String| 결과 코드|
| contactDeliveryResults[].resultMessage | String| 결과 메시지 |
| contactDeliveryResults[].templateParameters | Object| 템플릿 파라미터 |
| contactDeliveryResults[].additionalProperty | Object| 추가 속성, 알림톡, RCS만 제공|
| contactDeliveryResults[].createdDateTime | DateTime(ISO 86091) | 생성 일시(예: 2024-10-29T06:09:00+09:00)|
| contactDeliveryResults[].sentDateTime | DateTime(ISO 86091) | 발송 일시, 발송 이벤트가 수집되기 전까지 값은 null|
| contactDeliveryResults[].deliveredDateTime | DateTime(ISO 86091) | 수신 일시, 수신 이벤트가 수집되기 전까지 값은 null|
| contactDeliveryResults[].openedDateTime | DateTime(ISO 86091) | 열람 일시, 열람 이벤트가 수집되기 전까지 값은 null, 푸시와 이메일만 제공 |
| contactDeliveryResults[].updatedDateTime | DateTime(ISO 86091) | 마지막 업데이트 일시|
| totalCount | Number| 전체 개수|



**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 전문 메시지 발송
POST {{endpoint}}/message/v1.0/contact-delivery-results
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "confirmBeforeSend": false,
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678"
        }
      ]
    }
  ],
  "content": {
    "messageType": "SMS",
    "body": "안녕하세요. NHN Cloud의 신규 상품 Notification Hub가 출시 되었습니다."
  }
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/message/v1.0/contact-delivery-results" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

