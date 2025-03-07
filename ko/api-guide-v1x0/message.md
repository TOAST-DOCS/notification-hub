<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>메시지</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 메시지**

<span id="free-form-message-sending-request"></span>

## 자유 양식 메시지 발송 요청

요청 본문에 메시지 내용을 입력해 메시지를 발송 요청합니다.

각 메시지 채널로 메시지를 발송하기 위해서는 각 메시지 채널의 발신 정보가 등록되어야 있어야 합니다. 발신 정보 등록은 **Notification Hub 콘솔** > **발신 정보** 탭에서 진행할 수 있습니다. 메시지 채널의 발신 정보에 대한 자세한 설명은 **Notification** > **Notification Hub** > **이용 정책 및 사전 설정 안내**에서 확인할 수 있습니다.

<!-- !!! tip "알아두기"-->
<!-- API를 사용할 때 사용자가 알아 두면 좋을 참고 사항이나 추가 정보를 제공할 때 사용합니다.-->

<!-- !!! warning "주의"-->
<!--API를 사용할 때 따르지 않을 경우 서비스의 비정상 또는 비효율적 동작이 발생할 수 있는 주의 사항을 표기할 때 사용합니다.-->

**요청**

```
POST /message/v1.0/{messageChannel}/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| messageChannel | Path | String | Y | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| messagePurpose | Path | String | Y | 메시지 목적<br>NORMAL, AD, AUTH |

**공통 요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

메시지 채널에 따른 요청 본문의 자세한 내용은 아래 **메시지 채널별 상세 요청 본문**을 확인 부탁드립니다.

```json
{
  "statsKeyId": "통계_아이디",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "...": "메시지_채널에_따라_다른_형식"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "test"
        }
      ]
    }
  ],
  "content": {
    "...": "메시지_채널에_따라_다른_형식"
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 이름 | 타입 | 필수  | 설명                                                                                                                                    |
| --- | --- |-----|---------------------------------------------------------------------------------------------------------------------------------------|
| statsKeyId | String | N   | 통계 키 아이디                                                                                                                              |
| scheduledDateTime | DateTime(ISO 8601) | N   | 예약 발송 일시(예: 2024-10-29T06:29:00+09:00)                                                                                                |
| confirmBeforeSend | Boolean | N   | 발송 전 확인 여부(기본값 false)                                                                                                                 |
| sender | Object | Y | 발신자, 푸시 외 다른 메시지 채널은 필수                                                                                                               |
| recipients | Object Array | Y   | 수신자 배열                                                                                                                                |
| recipients[].contacts | Object Array | Y   | 수신자의 연락처 배열                                                                                                                           |
| recipients[].contacts[].contactType | String | Y   | 연락처 유형<br>PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_FCM, TOKEN_APNS, TOKEN_ADM, TOKEN_APNS_SANDBOX, TOKEN_APNS_VOIP, TOKEN_APNS_VOIP_SANDBOX |
| recipients[].contacts[].contact | String | Y   | 연락처                                                                                                                                   |
| recipients[].contacts[].clientReference | String         | N | 사용자 커스텀 필드                        |
| content | Object | Y   | 메시지 내용                                                                                                                                |

* 메시지 채널에 따라 **sender**, **content** 필드는 서로 다른 형식을 가집니다.
* 메시지 채널에 따라 **recipients[].contacts.contactType**, **recipients[].contacts.contact** 필드에 입력할 수 있는 값이 달라집니다.
* 예약 발송의 경우 **scheduledDateTime**를 설정합니다. 발송이 시작되기 전의 예약 발송은 요청 취소가 가능합니다. 요청 취소 API를 호출하거나 **Notification Hub 콘솔** > **발송 조회**에서 취소할 수 있습니다.
* 승인 후 발송의 경우 **confirmBeforeSend**를 **true**로 설정합니다. 승인 후 발송인 메시지는 **Notification Hub 콘솔** > **발송 조회**에서 승인을 하면 발송이 진행됩니다.
* 예약 발송과 승인 후 발송은 동시에 설정할 수 없습니다.

### 메시지 채널별 sender 필드

| 메시지 채널 | 필드 | 설명 |
| --- | --- | --- |
| SMS | sender.senderPhoneNumber | 발신자 번호 |
| RCS | sender.brandId | 브랜드 아이디 |
| RCS | sender.chatbotId | 대화방 아이디 |
| EMAIL | sender.senderMailAddress | 발신자 이메일 주소 |
| ALIMTALK, FRIENDTALK | sender.senderKey | 발신 키 |
| ALIMTALK | sender.senderProfileType | 발신 프로필 유형<br>GROUP, NORMAL |

* 알림톡(ALIMTALK)은 발신 키(senderKey)와 발신 프로필 유형(senderProfileType)을 필수로 입력해야 합니다.
* 친구톡(FRIENDTALK)은 NORMAL(일반) 발신 프로필 유형만 사용할 수 있습니다. GROUP(그룹) 발신 프로필 유형의 발신 키를 사용하면 발송에 실패합니다.
* 발신자 프로필 유형은 **GROUP(그룹)**과 **NORMAL(일반)**이 있습니다. **GROUP**은 그룹 발신자 프로필, **NORMAL**은 일반 발신자 프로필입니다.

**응답 본문**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "messageId": "메시지_아이디"
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 이름 | 타입 | 설명 |
| --- | --- | --- |
| header.isSuccessful | Boolean | API 요청 성공 여부 |
| header.resultCode | Integer | 결과 코드 |
| header.resultMessage | String | 결과 메시지 |
| messageId | String | 요청 성공한 메시지 아이디 |

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 자유 양식 메시지 발송
POST {{endpoint}}/message/v1.0/PUSH/free-form-messages/{messagePurpose}
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
          "contact": "01012345678",
          "clientReference": "test"
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
curl -X POST "${ENDPOINT}/message/v1.0/PUSH/free-form-messages/${MESSAGE_PURPOSE}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
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
    }'
```

</details>

<span id="free-form-message-request-body"></span>

## 메시지 채널별 자유 양식 메시지 발송 요청 본문 예시

<span id="free-form-message-request-body-sms"></span>

### SMS

```json
{
  "statsKeyId": "통계_키_아이디",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "test"
        }
      ]
    }
  ],
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

| 이름 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- |
| sender | Object | Y | 발신자, 푸시 외 다른 메시지 채널은 필수 |
| sender.senderPhoneNumber | String | N | 발신자 번호 |
| content | Object | Y | 메시지 내용 |
| content.messageType | String | Y | 메시지 타입<br>SMS(단문), LMS(장문), MMS(미디어 장문) |
| content.title | String | Y | 제목 |
| content.body | String | Y | 내용 |
| content.attachmentIds | String Array | N | 첨부 파일 아이디 |


<span id="free-form-message-request-body-rcs-sms-standalone"></span>

### RCS - SMS Standalone

```json
{
  "statsKeyId": "통계_키_아이디",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "브랜드_아이디",
    "chatbotId": "대화방_아이디"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "test"
        }
      ]
    }
  ],
  "content": {
    "messageType": "SMS",
    "unsubscribePhoneNumber": "08012341234",
    "smsType": "STANDALONE",
    "cards": [
        {
          "description":"안녕하세요. NHN Cloud Notification Hub 입니다.",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"홈페이지로 이동\"}}"
            }
          ]
        }
    ]
  },
  "options": {
    "expiryOption": 1,
    "groupId":"groupId"
  }
}
```


| 이름 | 타입 | 필수 | 설명                                                                                                                                                                     |
| --- | --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| sender | Object | Y | 발신자                                                                                                                                                               |
| sender.brandId | String | Y | 브랜드 아이디                                                                                                                                                  |
| sender.chatbotId | String | Y | 대화방 아이디                                                                                                                                                |
| content | Object | Y | 메시지 내용                                                                                                                                                          |
| content.messageType | String | Y | RCS 내 메시지 유형, SMS, LMS, MMS, RBC_TEMPLATE                                                                                                          |
| content.unsubscribePhoneNumber | String | N | 080 수신 거부 번호, 발송 목적이 광고인 경우 필수                                                                                                     |
| content.smsType | String | Y | SMS 타입, 메시지 유형이 SMS인 경우 필수, STANDALONE(스탠다드)                                                                                                      |
| content.cards | Object Array | Y | 카드                                                                                                                                                   |
| content.cards[].title | String | N | 제목                                                                                                                                                 |
| content.cards[].description | String | Y | 내용                                                                                                                                           |
| content.cards[].buttons | Object Array | N | 버튼                                                                                                                                         |
| content.cards[].buttons[].buttonType | String | Y | 버튼 타입<br>COMPOSE(대화방 열기), CLIPBOARD(복사하기), DIALER(전화 걸기), MAP_SHOW(지도 보여주기), MAP_QUERY(지도 검색하기), MAP_SHARE(현재 위치 공유하기), URL(URL 연결하기), CALENDAR(일정 등록하기) |
| content.cards[].buttons[].buttonJson | String | Y | 버튼 Json, 버튼 타입에 맞는 포맷 확인                                                                                                       |
| options | Object | N | 발송 옵션                                                                                                                                                           |
| options.expiryOption | Integer | N | 디바이스로의 전송 시도에 대한 타임아웃 (1: 1일, 2: 40초, 3: 3분, 4: 1시간)                                                                                      |
| options.groupId | String | N | RCS BizCenter 통계 연동을 위한 그룹 아이디                                                                                                                       |

<span id="free-form-message-request-body-rcs-lms-standalone"></span>

### RCS - LMS Standalone

```json
{
  "statsKeyId": "통계_키_아이디",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "브랜드_아이디",
    "chatbotId": "대화방_아이디"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "test"
        }
      ]
    }
  ],
  "content": {
    "messageType": "LMS",
    "unsubscribePhoneNumber": "08012341234",
    "lmsType": "STANDALONE",
    "cards": [
        {
          "title":"[NHN Cloud] 공지사항",
          "description":"안녕하세요. NHN Cloud Notification Hub 입니다.",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"홈페이지로 이동\"}}"
            }
          ]
        }
    ]
  },
  "options": {
    "expiryOption": 1,
    "groupId":"groupId"
  }
}
```

| 이름 | 타입 | 필수 | 설명                                                                                                                                                                     |
| --- | --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| sender | Object | Y | 발신자                                                                                                                                                               |
| sender.brandId | String | Y | 브랜드 아이디                                                                                                                                                  |
| sender.chatbotId | String | Y | 대화방 아이디                                                                                                                                                |
| content | Object | Y | 메시지 내용                                                                                                                                                          |
| content.messageType | String | Y | RCS 내 메시지 유형, SMS, LMS, MMS, RBC_TEMPLATE                                                                                                          |
| content.unsubscribePhoneNumber | String | N | 080 수신 거부 번호, 발송 목적이 광고인 경우 필수                                                                                                     |
| content.lmsType | String | Y | LMS 타입, 메시지 유형이 LMS인 경우 필수, STANDALONE(스탠다드), FORMAT_BASIC(포맷 기본형), FORMAT_TITLE_HIGHLIGHT(포맷 타이틀 강조형), FORMAT_PARAGRAPH(포맷 문단형)           |
| content.cards | Object Array | Y | 카드                                                                                                                                                   |
| content.cards[].title | String | N | 제목                                                                                                                                                 |
| content.cards[].description | String | Y | 내용                                                                                                                                           |
| content.cards[].buttons | Object Array | N | 버튼                                                                                                                                         |
| content.cards[].buttons[].buttonType | String | Y | 버튼 타입<br>COMPOSE(대화방 열기), CLIPBOARD(복사하기), DIALER(전화 걸기), MAP_SHOW(지도 보여주기), MAP_QUERY(지도 검색하기), MAP_SHARE(현재 위치 공유하기), URL(URL 연결하기), CALENDAR(일정 등록하기) |
| content.cards[].buttons[].buttonJson | String | Y | 버튼 Json, 버튼 타입에 맞는 포맷 확인                                                                                                       |
| options | Object | N | 발송 옵션                                                                                                                                                           |
| options.expiryOption | Integer | N | 디바이스로의 전송 시도에 대한 타임아웃 (1: 1일, 2: 40초, 3: 3분, 4: 1시간)                                                                                      |
| options.groupId | String | N | RCS BizCenter 통계 연동을 위한 그룹 아이디                                                                                                                        |

<span id="free-form-message-request-body-rcs-lms-format-basic"></span>

### RCS - LMS 포맷 기본형 및 포맷 타이틀 강조형
* mTitleMedia 아이콘 파일 ID 목록
  * 프로모션: LT-messagebase.common-DdWk6s
  * 쿠폰: LT-messagebase.common-5Weq00
  * 이벤트: LT-messagebase.common-jUAJX2
  * 예약: LT-messagebase.common-2Yxt2H
  * 영수증: LT-messagebase.common-2k8ydI
  * 알림: LT-messagebase.common-YCVd02

```json
{
  "statsKeyId": "통계_키_아이디",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "브랜드_아이디",
    "chatbotId": "대화방_아이디"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "test"
        }
      ]
    }
  ],
  "content": {
    "messageType": "LMS",
    "unsubscribePhoneNumber": "08012341234",
    "lmsType": "FORMAT_BASIC",
    "cards": [
        {
          "mTitle":"[NHN Cloud] 공지사항",
          "mTitleMedia":"LT-messagebase.common-DdWk6s",
          "title":"공지 1",
          "description":"안녕하세요. NHN Cloud Notification Hub 입니다.",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"홈페이지로 이동\"}}"
            }
          ]
        }
    ]
  },
  "options": {
    "expiryOption": 1,
    "groupId":"groupId"
  }
}
```

| 이름 | 타입 | 필수 | 설명                                                                                                                                                                     |
| --- | --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| sender | Object | Y | 발신자                                                                                                                                                               |
| sender.brandId | String | Y | 브랜드 아이디                                                                                                                                                  |
| sender.chatbotId | String | Y | 대화방 아이디                                                                                                                                                |
| content | Object | Y | 메시지 내용                                                                                                                                                          |
| content.messageType | String | Y | RCS 내 메시지 유형, SMS, LMS, MMS, RBC_TEMPLATE                                                                                                          |
| content.unsubscribePhoneNumber | String | N | 080 수신 거부 번호, 발송 목적이 광고인 경우 필수                                                                                                     |
| content.lmsType | String | Y | LMS 타입, 메시지 유형이 LMS인 경우 필수, STANDALONE(스탠다드), FORMAT_BASIC(포맷 기본형), FORMAT_TITLE_HIGHLIGHT(포맷 타이틀 강조형), FORMAT_PARAGRAPH(포맷 문단형)           |
| content.cards | Object Array | Y | 카드                                                                                                                                                   |
| content.cards[].mTitle | String | Y | 메인 타이틀                                                                                                                                           |
| content.cards[].mTitleMedia | String | N | 메인 타이틀 아이콘                                                                                                                              |
| content.cards[].title | String | N | 제목                                                                                                                                                 |
| content.cards[].description | String | Y | 내용                                                                                                                                           |
| content.cards[].buttons | Object Array | N | 버튼                                                                                                                                         |
| content.cards[].buttons[].buttonType | String | Y | 버튼 타입<br>COMPOSE(대화방 열기), CLIPBOARD(복사하기), DIALER(전화 걸기), MAP_SHOW(지도 보여주기), MAP_QUERY(지도 검색하기), MAP_SHARE(현재 위치 공유하기), URL(URL 연결하기), CALENDAR(일정 등록하기) |
| content.cards[].buttons[].buttonJson | String | Y | 버튼 Json, 버튼 타입에 맞는 포맷 확인                                                                                                       |
| options | Object | N | 발송 옵션                                                                                                                                                           |
| options.expiryOption | Integer | N | 디바이스로의 전송 시도에 대한 타임아웃 (1: 1일, 2: 40초, 3: 3분, 4: 1시간)                                                                                      |
| options.groupId | String | N | RCS BizCenter 통계 연동을 위한 그룹 아이디                                                                                                                        |

### RCS - LMS 포맷 문단형 타입
* mTitleMedia 아이콘 파일 ID 목록
  * 프로모션: LT-messagebase.common-DdWk6s
  * 쿠폰: LT-messagebase.common-5Weq00
  * 이벤트: LT-messagebase.common-jUAJX2
  * 예약: LT-messagebase.common-2Yxt2H
  * 영수증: LT-messagebase.common-2k8ydI
  * 알림: LT-messagebase.common-YCVd02

```json
{
  "statsKeyId": "통계_키_아이디",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "브랜드_아이디",
    "chatbotId": "대화방_아이디"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "test"
        }
      ]
    }
  ],
  "content": {
    "messageType": "LMS",
    "unsubscribePhoneNumber": "08012341234",
    "lmsType": "FORMAT_PARAGRAPH",
    "cards": [
        {
          "mTitle":"[NHN Cloud] 공지사항",
          "mTitleMedia":"LT-messagebase.common-DdWk6s",
          "title1":"공지 1",
          "description1":"안녕하세요. NHN Cloud Notification Hub 입니다.",
          "title2":"공지 2",
          "description2":"안녕하세요. NHN Cloud Notification Hub 입니다.",
          "title3":"공지 3",
          "description3":"안녕하세요. NHN Cloud Notification Hub 입니다.",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"공지1 버튼\"}}"
            },
            {},
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"공지2 버튼\"}}"
            },
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"공지2 버튼\"}}"
            },
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"공지3 버튼\"}}"
            },
          ]
        }
    ]
  },
  "options": {
    "expiryOption": 1,
    "groupId":"groupId"
  }
}
```

| 이름 | 타입 | 필수 | 설명                                                                                                                                                                     |
| --- | --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| sender | Object | Y | 발신자                                                                                                                                                               |
| sender.brandId | String | Y | 브랜드 아이디                                                                                                                                                  |
| sender.chatbotId | String | Y | 대화방 아이디                                                                                                                                                |
| content | Object | Y | 메시지 내용                                                                                                                                                          |
| content.messageType | String | Y | RCS 내 메시지 유형, SMS, LMS, MMS, RBC_TEMPLATE                                                                                                          |
| content.unsubscribePhoneNumber | String | N | 080 수신 거부 번호, 발송 목적이 광고인 경우 필수                                                                                                     |
| content.lmsType | String | Y | LMS 타입, 메시지 유형이 LMS인 경우 필수, STANDALONE(스탠다드), FORMAT_BASIC(포맷 기본형), FORMAT_TITLE_HIGHLIGHT(포맷 타이틀 강조형), FORMAT_PARAGRAPH(포맷 문단형)           |
| content.cards | Object Array | Y | 카드                                                                                                                                                   |
| content.cards[].mTitle | String | Y | 메인 타이틀                                                                                                                                           |
| content.cards[].mTitleMedia | String | N | 메인 타이틀 아이콘                                                                                                                                |
| content.cards[].title1 | String | N | 제목 (문단 1)                                                                                                                                        |
| content.cards[].description1 | String | Y | 내용 (문단 1)                                                                                                                                  |
| content.cards[].title2 | String | N | 제목 (문단 2)                                                                                                                                        |
| content.cards[].description2 | String | Y | 내용 (문단 2)                                                                                                                                  |
| content.cards[].title3 | String | N | 제목 (문단 3)                                                                                                                                        |
| content.cards[].description3 | String | Y | 내용 (문단 3)                                                                                                                                  |
| content.cards[].buttons | Object Array | N | 버튼                                                                                                                                         |
| content.cards[].buttons[].buttonType | String | Y | 버튼 타입<br>COMPOSE(대화방 열기), CLIPBOARD(복사하기), DIALER(전화 걸기), MAP_SHOW(지도 보여주기), MAP_QUERY(지도 검색하기), MAP_SHARE(현재 위치 공유하기), URL(URL 연결하기), CALENDAR(일정 등록하기) |
| content.cards[].buttons[].buttonJson | String | Y | 버튼 Json, 버튼 타입에 맞는 포맷 확인                                                                                                       |
| options | Object | N | 발송 옵션                                                                                                                                                           |
| options.expiryOption | Integer | N | 디바이스로의 전송 시도에 대한 타임아웃 (1: 1일, 2: 40초, 3: 3분, 4: 1시간)                                                                                      |
| options.groupId | String | N | RCS BizCenter 통계 연동을 위한 그룹 아이디                                                                                                                        |



### RCS - MMS 가로형, 세로형

```json
{
  "statsKeyId": "통계_키_아이디",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "브랜드_아이디",
    "chatbotId": "대화방_아이디"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "test"
        }
      ]
    }
  ],
  "content": {
    "messageType": "MMS",
    "unsubscribePhoneNumber": "08012341234",
    "mmsType": "HORIZONTAL",
    "cards": [
        {
          "title":"[NHN Cloud] 공지사항",
          "description":"안녕하세요. NHN Cloud Notification Hub 입니다.",
          "attachmentId":"첨부 파일 아이디",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"홈페이지로 이동\"}}"
            }
          ]
        }
    ]
  },
  "options": {
    "expiryOption": 1,
    "groupId":"groupId"
  }
}
```


| 이름 | 타입 | 필수 | 설명                                                                                                                                                                     |
| --- | --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| sender | Object | Y | 발신자                                                                                                                                                               |
| sender.brandId | String | Y | 브랜드 아이디                                                                                                                                                  |
| sender.chatbotId | String | Y | 대화방 아이디                                                                                                                                                |
| content | Object | Y | 메시지 내용                                                                                                                                                          |
| content.messageType | String | Y | RCS 내 메시지 유형, SMS, LMS, MMS, RBC_TEMPLATE                                                                                                          |
| content.unsubscribePhoneNumber | String | N | 080 수신 거부 번호, 발송 목적이 광고인 경우 필수                                                                                                     |
| content.mmsType | String | Y | MMS 타입, 메시지 유형이 MMS인 경우 필수, HORIZONTAL(가로형), VERTICAL(세로형), CAROUSEL_MEDIUM(캐러셀 중간), CAROUSEL_SMALL(캐러셀 작게)                                  |
| content.cards | Object Array | Y | 카드                                                                                                                                                   |
| content.cards[].title | String | N | 제목                                                                                                                                                 |
| content.cards[].description | String | Y | 내용                                                                                                                                           |
| content.cards[].attachmentId | String | Y | 첨부 파일 아이디                                                                                                                                           |
| content.cards[].buttons | Object Array | N | 버튼                                                                                                                                         |
| content.cards[].buttons[].buttonType | String | Y | 버튼 타입<br>COMPOSE(대화방 열기), CLIPBOARD(복사하기), DIALER(전화 걸기), MAP_SHOW(지도 보여주기), MAP_QUERY(지도 검색하기), MAP_SHARE(현재 위치 공유하기), URL(URL 연결하기), CALENDAR(일정 등록하기) |
| content.cards[].buttons[].buttonJson | String | Y | 버튼 Json, 버튼 타입에 맞는 포맷 확인                                                                                                       |
| options | Object | N | 발송 옵션                                                                                                                                                           |
| options.expiryOption | Integer | N | 디바이스로의 전송 시도에 대한 타임아웃 (1: 1일, 2: 40초, 3: 3분, 4: 1시간)                                                                                      |
| options.groupId | String | N | RCS BizCenter 통계 연동을 위한 그룹 아이디                                                                                                                        |

### RCS - MMS 캐러셀

```json
{
  "statsKeyId": "통계_키_아이디",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "브랜드_아이디",
    "chatbotId": "대화방_아이디"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "test"
        }
      ]
    }
  ],
  "content": {
    "messageType": "MMS",
    "unsubscribePhoneNumber": "08012341234",
    "mmsType": "CAROUSEL_MEDIUM",
    "cards": [
        {
          "title":"[NHN Cloud] 공지사항",
          "description":"안녕하세요. NHN Cloud Notification Hub 입니다.",
          "attachmentId":"첨부 파일 아이디",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"홈페이지로 이동\"}}"
            }
          ]
        },
        {
          "title":"[NHN Cloud] 공지사항",
          "description":"안녕하세요. NHN Cloud Notification Hub 입니다.",
          "attachmentId":"첨부 파일 아이디",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"홈페이지로 이동\"}}"
            }
          ]
        },
        {
          "title":"[NHN Cloud] 공지사항",
          "description":"안녕하세요. NHN Cloud Notification Hub 입니다.",
          "attachmentId":"첨부 파일 아이디",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"홈페이지로 이동\"}}"
            }
          ]
        }
    ]
  },
  "options": {
    "expiryOption": 1,
    "groupId":"groupId"
  }
}
```


| 이름 | 타입 | 필수 | 설명                                                                                                                                                                     |
| --- | --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| sender | Object | Y | 발신자                                                                                                                                                               |
| sender.brandId | String | Y | 브랜드 아이디                                                                                                                                                  |
| sender.chatbotId | String | Y | 대화방 아이디                                                                                                                                                |
| content | Object | Y | 메시지 내용                                                                                                                                                          |
| content.messageType | String | Y | RCS 내 메시지 유형, SMS, LMS, MMS, RBC_TEMPLATE                                                                                                          |
| content.unsubscribePhoneNumber | String | N | 080 수신 거부 번호, 발송 목적이 광고인 경우 필수                                                                                                     |
| content.mmsType | String | Y | MMS 타입, 메시지 유형이 MMS인 경우 필수, HORIZONTAL(가로형), VERTICAL(세로형), CAROUSEL_MEDIUM(캐러셀 중간), CAROUSEL_SMALL(캐러셀 작게)                                  |
| content.cards | Object Array | Y | 카드                                                                                                                                                   |
| content.cards[].title | String | N | 제목                                                                                                                                                 |
| content.cards[].description | String | Y | 내용                                                                                                                                           |
| content.cards[].attachmentId | String | Y | 첨부 파일 아이디                                                                                                                                           |
| content.cards[].buttons | Object Array | N | 버튼                                                                                                                                         |
| content.cards[].buttons[].buttonType | String | Y | 버튼 타입<br>COMPOSE(대화방 열기), CLIPBOARD(복사하기), DIALER(전화 걸기), MAP_SHOW(지도 보여주기), MAP_QUERY(지도 검색하기), MAP_SHARE(현재 위치 공유하기), URL(URL 연결하기), CALENDAR(일정 등록하기) |
| content.cards[].buttons[].buttonJson | String | Y | 버튼 Json, 버튼 타입에 맞는 포맷 확인                                                                                                       |
| options | Object | N | 발송 옵션                                                                                                                                                           |
| options.expiryOption | Integer | N | 디바이스로의 전송 시도에 대한 타임아웃 (1: 1일, 2: 40초, 3: 3분, 4: 1시간)                                                                                      |
| options.groupId | String | N | RCS BizCenter 통계 연동을 위한 그룹 아이디                                                                                                                        |


<span id="free-form-message-request-body-friendtalk-text"></span>

### 친구톡 - 텍스트형

* 알림톡은 템플릿 등록 후 승인을 받은 상태에서 발송 가능하기 때문에 템플릿, 플로우 메시지 발송만 가능합니다.
* 알림톡의 **sender**, **content** 필드는 **템플릿 메시지 발송**의 **요청 본문**을 확인하세요.
* 친구톡(FRIENDTALK)은 NORMAL(일반) 발신 프로필 유형만 사용할 수 있습니다. GROUP(그룹) 발신 프로필 유형의 발신 키를 사용하면 발송에 실패합니다.

```json
{
    "statsKeyId": "통계_키_아이디",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "발신 프로필_발신키"
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
      "messageType": "TEXT",
      "content": "발송_내용",
      "buttons": [
        {
          "type": "WL",
          "name": "버튼_이름",
          "linkMo": "모바일_링크",
          "linkPc": "PC_링크",
          "schemeIos": "iOS_앱_링크",
          "schemeAndroid": "Android_앱_링크",
          "bizFormKey": "비즈폼_키"
        }
      ],
      "coupon": {
        "title": "쿠폰_제목",
        "description": "쿠폰_상세_설명",
        "linkMo": "모바일_링크",
        "linkPc": "PC_링크",
        "schemeIos": "iOS_앱_링크",
        "schemeAndroid": "Android_앱_링크"
      }
    }
}
```


| 이름 | 타입 | 필수 | 설명                                                            |
| --- | --- |----|---------------------------------------------------------------|
| sender | Object | Y  | 발신자                                                           |
| sender.senderKey | Object | Y  | 발신 프로필_발신키                                                     |
| content | Object | Y  | 메시지 내용                                                        |
| content.messageType | String | Y  | 메시지 유형                                                        |
| content.content | String | Y  | 내용                                                            |
| content.buttons                   | Object Array  | N  | 버튼                                                                                                                                                        |
| content.buttons[].type            | String | Y  | 버튼 타입<br>WL(웹 링크), AL(앱 링크), BK(봇 키워드), MD(메시지 전달), BF(비즈니스폼)                                                                                             |
| content.buttons[].name            | String | Y  | 버튼 이름                                                                                                                                                     |
| content.buttons[].linkMo          | String | N  | 링크 모바일, 버튼 타입이 WL이면 필수                                                                                                                                    |
| content.buttons[].linkPc          | String | N  | 링크 PC                                                                                                                                                     |
| content.buttons[].schemeIos       | String | N  | iOS 앱 링크                                                                                                                                                  |
| content.buttons[].schemeAndroid   | String | N  | Android 앱 링크                                                                                                                                              |
| content.buttons[].bizFormKey      | String | N  | 비즈폼 키, 버튼 타입이 BF이면 필수                                                                                                                                     |
| content.coupon | Object | N  | 쿠폰                                                            |
| content.coupon.title | String | Y  | 제목, 경우 5가지 형식으로 제한됨<br>"${숫자}원 할인 쿠폰" 숫자는 1 이상 99,999,999 이하<br>"${숫자}% 할인 쿠폰" 숫자는 1 이상 100 이하<br>"배송비 할인 쿠폰"<br><br>"${7자 이내} 무료 쿠폰"<br>"${7자 이내} UP 쿠폰"                                                          |
| content.coupon.description | String | Y  | 쿠폰 상세 설명 (일반 텍스트, 이미지형, 캐러셀 피드형 최대 12자 / 와이드 이미지형, 와이드 아이템 리스트형 최대 18자) |
| content.coupon.linkMo | String | N  | 링크 모바일                                                        |
| content.coupon.linkPc | String | N  | 링크 PC                                                         |
| content.coupon.schemeIos | String | N  | iOS 앱 링크                                            |
| content.coupon.schemeAndroid | String | N  | Android 앱 링크                         |

<span id="free-form-message-request-body-friendtalk-image"></span>

### 친구톡 - 이미지형 / 와이드 이미지형

* 친구톡(FRIENDTALK)은 NORMAL(일반) 발신 프로필 유형만 사용할 수 있습니다. GROUP(그룹) 발신 프로필 유형의 발신 키를 사용하면 발송에 실패합니다.

```json
{
    "statsKeyId": "통계_키_아이디",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "발신 프로필_발신키"
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
      "messageType": "WIDE_IMAGE",
      "content": "발송_내용",
      "attachmentId": "첨부_파일_ID",
      "imageLink": "이미지_링크_URL",
      "buttons": [
        {
          "type": "WL",
          "name": "버튼_이름",
          "linkMo": "모바일_링크",
          "linkPc": "PC_링크",
          "schemeIos": "iOS_앱_링크",
          "schemeAndroid": "Android_앱_링크",
          "bizFormKey": "비즈폼_키"
        }
      ],
      "coupon": {
        "title": "쿠폰_제목",
        "description": "쿠폰_상세_설명",
        "linkMo": "모바일_링크",
        "linkPc": "PC_링크",
        "schemeIos": "iOS_앱_링크",
        "schemeAndroid": "Android_앱_링크"
      }
    }
}
```

| 이름 | 타입            | 필수 | 설명                                                            |
| --- |---------------|----|---------------------------------------------------------------|
| sender | Object        | Y  | 발신자                                                           |
| sender.senderKey | Object        | Y  | 발신 프로필_발신 키                                                     |
| content | Object        | Y  | 메시지 내용                                                        |
| content.messageType | String        | Y  | 메시지 유형                                                        |
| content.content | String        | Y  | 내용                                                            |
| content.attachmentId | String        | Y  | 첨부 파일 아이디 |
| content.imageLink | String        | N  | 이미지 링크 |
| content.buttons                   | Object Array | N  | 버튼                                                                                                                                                        |
| content.buttons[].type            | String        | Y  | 버튼 타입<br>WL(웹 링크), AL(앱 링크), BK(봇 키워드), MD(메시지 전달), BF(비즈니스폼)                                                                                             |
| content.buttons[].name            | String        | Y  | 버튼 이름                                                                                                                                                     |
| content.buttons[].linkMo          | String        | N  | 링크 모바일, 버튼 타입이 WL이면 필수                                                                                                                                    |
| content.buttons[].linkPc          | String        | N  | 링크 PC                                                                                                                                                     |
| content.buttons[].schemeIos       | String        | N  | iOS 앱 링크                                                                                                                                                  |
| content.buttons[].schemeAndroid   | String        | N  | Android 앱 링크                                                                                                                                              |
| content.buttons[].bizFormKey      | String        | N  | 비즈폼 키, 버튼 타입이 BF이면 필수                                                                                                                                     |
| content.coupon | Object        | N  | 쿠폰                                                            |
| content.coupon.title | String        | Y  | 제목, 경우 5가지 형식으로 제한됨<br>"${숫자}원 할인 쿠폰" 숫자는 1 이상 99,999,999 이하<br>"${숫자}% 할인 쿠폰" 숫자는 1 이상 100 이하<br>"배송비 할인 쿠폰"<br><br>"${7자 이내} 무료 쿠폰"<br>"${7자 이내} UP 쿠폰"                                                          |
| content.coupon.description | String        | Y  | 쿠폰 상세 설명 (일반 텍스트, 이미지형, 캐러셀 피드형 최대 12자 / 와이드 이미지형, 와이드 아이템 리스트형 최대 18자) |
| content.coupon.linkMo | String        | N  | 링크 모바일                                                        |
| content.coupon.linkPc | String        | N  | 링크 PC                                                         |
| content.coupon.schemeIos | String        | N  | iOS 앱 링크                                            |
| content.coupon.schemeAndroid | String        | N  | Android 앱 링크                         |

<span id="free-form-message-request-body-friendtalk-wide-itemlist"></span>

### 친구톡 - 와이드 아이템리스트형

* 친구톡(FRIENDTALK)은 NORMAL(일반) 발신 프로필 유형만 사용할 수 있습니다. GROUP(그룹) 발신 프로필 유형의 발신 키를 사용하면 발송에 실패합니다.

```json
{
    "statsKeyId": "통계_키_아이디",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "발신 프로필_발신 키"
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
      "messageType": "WIDE_ITEMLIST",
      "buttons": [
        {
          "type": "WL",
          "name": "버튼_이름",
          "linkMo": "모바일_링크",
          "linkPc": "PC_링크",
          "schemeIos": "iOS_앱_링크",
          "schemeAndroid": "Android_앱_링크",
          "bizFormKey": "비즈폼_키"
        }
      ],
      "header": "헤더",
      "item": {
          "list": [{
            "title": "아이템_제목",
            "attachmentId": "첨부_파일_아이디",
            "linkMo": "모바일_링크",
            "linkPc": "PC_링크",
            "schemeIos": "iOS_앱_링크",
            "schemeAndroid": "Android_앱_링크"
          },
          {
            "title": "아이템_제목",
            "attachmentId": "첨부_파일_아이디",
            "linkMo": "모바일_링크",
            "linkPc": "PC_링크",
            "schemeIos": "iOS_앱_링크",
            "schemeAndroid": "Android_앱_링크"
          },
          {
          "title": "아이템_제목",
          "attachmentId": "첨부_파일_아이디",
          "linkMo": "모바일_링크",
          "linkPc": "PC_링크",
          "schemeIos": "iOS_앱_링크",
          "schemeAndroid": "Android_앱_링크"
          }
        ]
      },
      "coupon": {
        "title": "쿠폰_제목",
        "description": "쿠폰_상세_설명",
        "linkMo": "모바일_링크",
        "linkPc": "PC_링크",
        "schemeIos": "iOS_앱_링크",
        "schemeAndroid": "Android_앱_링크"
      }
    }
}
```

| 이름                                | 타입            | 필수 | 설명                                                                                                                                                        |
|-----------------------------------|---------------|----|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| sender                            | Object        | Y  | 발신자                                                                                                                                                       |
| sender.senderKey                  | Object        | Y  | 발신 프로필_발신 키                                                                                                                                                 |
| content                           | Object        | Y  | 메시지 내용                                                                                                                                                    |
| content.messageType               | String        | Y  | 메시지 유형                                                                                                                                                    |
| content.buttons                   | Object Array | N  | 버튼                                                                                                                                                        |
| content.buttons[].type            | String        | Y  | 버튼 타입<br>WL(웹 링크), AL(앱 링크), BK(봇 키워드), MD(메시지 전달), BF(비즈니스폼)                                                                                             |
| content.buttons[].name            | String        | Y  | 버튼 이름                                                                                                                                                     |
| content.buttons[].linkMo          | String        | N  | 링크 모바일, 버튼 타입이 WL이면 필수                                                                                                                                    |
| content.buttons[].linkPc          | String        | N  | 링크 PC                                                                                                                                                     |
| content.buttons[].schemeIos       | String        | N  | iOS 앱 링크                                                                                                                                                  |
| content.buttons[].schemeAndroid   | String        | N  | Android 앱 링크                                                                                                                                              |
| content.buttons[].bizFormKey      | String        | N  | 비즈폼 키, 버튼 타입이 BF이면 필수                                                                                                                                     |
| content.header                    | String        | Y  | 헤더                                                                                                                                                        |
| content.item                      | Object        | Y  | 와이드 아이템                                                                                                                                                   |
| content.item.list                 | Object Array | Y  | 와이드 아이템 리스트(최소 3개, 최대 4개)                                                                                                                                 |
| content.item.list[].title         | String        | Y  | 아이템 제목(첫 번째 아이템의 경우 최대 25자, 2~4번째 아이템의 경우 최대 30자)                                                                                                         |
| content.item.list[].attachmentId  | String        | Y  | 첨부 파일 아이디                                                                                                                                                 |
| content.item.list[].linkMo        | String        | Y  | 모바일 웹 링크                                                                                                                                                  |
| content.item.list[].linkPc        | String        | Y  | PC 웹 링크                                                                                                                                                   |
| content.item.list[].schemeIos     | String        | Y  | iOS 앱 링크                                                                                                                                                  |
| content.item.list[].schemeAndroid | String        | Y  | Android 앱 링크                                                                                                                                                 |
| content.coupon                    | Object        | N  | 쿠폰                                                                                                                                                        |
| content.coupon.title              | String        | Y  | 제목, 경우 5가지 형식으로 제한됨<br>"${숫자}원 할인 쿠폰" 숫자는 1 이상 99,999,999 이하<br>"${숫자}% 할인 쿠폰" 숫자는 1 이상 100 이하<br>"배송비 할인 쿠폰"<br><br>"${7자 이내} 무료 쿠폰"<br>"${7자 이내} UP 쿠폰" |
| content.coupon.description        | String        | Y  | 쿠폰 상세 설명 (일반 텍스트, 이미지형, 캐러셀 피드형 최대 12자 / 와이드 이미지형, 와이드 아이템 리스트형 최대 18자)                                                                                   |
| content.coupon.linkMo             | String        | N  | 링크 모바일                                                                                                                                                    |
| content.coupon.linkPc             | String        | N  | 링크 PC                                                                                                                                                     |
| content.coupon.schemeIos          | String        | N  | iOS 앱 링크                                                                                                                                                  |
| content.coupon.schemeAndroid      | String        | N  | Android 앱 링크                                                                                                                                              |

<span id="free-form-message-request-body-friendtalk-carousel"></span>

### 친구톡 - 캐러셀 피드형

* 친구톡(FRIENDTALK)은 NORMAL(일반) 발신 프로필 유형만 사용할 수 있습니다. GROUP(그룹) 발신 프로필 유형의 발신 키를 사용하면 발송에 실패합니다.

```json
{
    "statsKeyId": "통계_키_아이디",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "발신 프로필_발신 키"
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
      "messageType": "CAROUSEL_FEED",
      "carousel": {
        "list": [
          {
            "header": "캐러셀_아이템_제목",
            "message": "캐러셀_아이템_메시지",
            "attachment": {
              "buttons": [
                {
                  "type": "WL",
                  "name": "버튼_이름",
                  "linkMo": "모바일_링크",
                  "linkPc": "PC_링크",
                  "schemeIos": "iOS_앱_링크",
                  "schemeAndroid": "Android_앱_링크"
                }
              ],
              "image": {
                "attachmentId": "첨부_파일_아이디",
                "imageLink": "이미지_링크_URL"
              },
              "coupon": {
                "title": "쿠폰_제목",
                "description": "쿠폰_상세_설명",
                "linkMo": "모바일_링크",
                "linkPc": "PC_링크",
                "schemeIos": "iOS_앱_링크",
                "schemeAndroid": "Android_앱_링크"
              }
            }
          },
          {
            "header": "캐러셀_아이템_제목",
            "message": "캐러셀_아이템_메시지",
            "attachment": {
              "buttons": [
                {
                  "type": "WL",
                  "name": "버튼_이름",
                  "linkMo": "모바일_링크",
                  "linkPc": "PC_링크",
                  "schemeIos": "iOS_앱_링크",
                  "schemeAndroid": "Android_앱_링크"
                }
              ],
              "image": {
                "attachmentId": "첨부_파일_아이디",
                "imageLink": "이미지_링크_URL"
              },
              "coupon": {
                "title": "쿠폰_제목",
                "description": "쿠폰_상세_설명",
                "linkMo": "모바일_링크",
                "linkPc": "PC_링크",
                "schemeIos": "iOS_앱_링크",
                "schemeAndroid": "Android_앱_링크"
              }
            }
          }
        ],
        "tail": {
          "linkMo": "모바일_링크",
          "linkPc": "PC_링크",
          "schemeAndroid": "Android_앱_링크",
          "schemeIos": "iOS_앱_링크"
        }
      }
    }
}
```

| 이름                                                         | 타입            | 필수 | 설명                                                                                                                                                       |
|------------------------------------------------------------|---------------|----|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| sender                                                     | Object        | Y  | 발신자                                                                                                                                                      |
| sender.senderKey                                           | Object        | Y  | 발신 프로필_발신 키                                                                                                                                                |
| content                                                    | Object        | Y  | 메시지 내용                                                                                                                                                   |
| content.messageType                                        | String        | Y  | 메시지 유형                                                                                                                                                   |
| content.carousel                                           | Object        | Y  | 캐러셀                                                                                                                                                      |
| content.carousel.list                                      | Object Array | Y  | 캐러셀 리스트(최소 2개, 최대 10개)                                                                                                                                   |
| content.carousel.list[].header                             | String        | Y  | 캐러셀 아이템 제목(최대 20자), 캐러셀 피드형에서만 사용 가능                                                                                                                     |
| content.carousel.list[].message                            | String        | Y  | 캐러셀 아이템 메시지(최대 180자), 캐러셀 피드형에서만 사용 가능                                                                                                                   |
| content.carousel.list[].attachment                         | Object        | N  | 캐러셀 아이템 이미지, 버튼 정보                                                                                                                                       |
| content.carousel.list[].attachment.buttons                 | Object Array | N  | 버튼 리스트 (최대 2개)                                                                                                                                           |
| content.carousel.list[].attachment.buttons[].type          | String        | Y  | 버튼 타입<br>WL(웹 링크), AL(앱 링크), BK(봇 키워드), MD(메시지 전달), BF(비즈니스폼)                                                                                            |
| content.carousel.list[].attachment.buttons[].name          | String        | Y  | 버튼 이름                                                                                                                                                    |
| content.carousel.list[].attachment.buttons[].linkMo        | String        | N  | 링크 모바일, 버튼 타입이 WL이면 필수                                                                                                                                   |
| content.carousel.list[].attachment.buttons[].linkPc        | String        | N  | 링크 PC                                                                                                                                                    |
| content.carousel.list[].attachment.buttons[].schemeIos     | String        | N  | iOS 앱 링크                                                                                                                                                 |
| content.carousel.list[].attachment.buttons[].schemeAndroid | String        | N  | Android 앱 링크                                                                                                                                             |
| content.carousel.list[].attachment.image                   | Object        | Y  | 캐러셀 이미지                                                                                                                                                  |
| content.carousel.list[].attachment.image.attachmentId      | String        | Y  | 첨부 파일 id                                                                                                                                                 |
| content.carousel.list[].attachment.image.imageLink         | String        | N  | 이미지 링크 URL                                                                                                                                               |
| content.carousel.list[].attachment.coupon                  | Object        | N  | 쿠폰                                                                                                                                                       |
| content.carousel.list[].attachment.coupon.title            | String        | Y  | 제목, 경우 5가지 형식으로 제한됨<br>"${숫자}원 할인 쿠폰" 숫자는 1 이상 99,999,999 이하<br>"${숫자}% 할인 쿠폰" 숫자는 1 이상 100 이하<br>"배송비 할인 쿠폰"<br><br>"${7자 이내} 무료 쿠폰"<br>"${7자 이내} UP 쿠폰" |
| content.carousel.list[].attachment.coupon.description      | String        | Y  | 쿠폰 상세 설명 (일반 텍스트, 이미지형, 캐러셀 피드형 최대 12자 / 와이드 이미지형, 와이드 아이템 리스트형 최대 18자)                                                                                  |
| content.carousel.list[].attachment.coupon.linkMo           | String        | N  | 링크 모바일                                                                                                                                                   |
| content.carousel.list[].attachment.coupon.linkPc           | String        | N  | 링크 PC                                                                                                                                                    |
| content.carousel.list[].attachment.coupon.schemeIos        | String        | N  | iOS 앱 링크                                                                                                                                                 |
| content.carousel.list[].attachment.coupon.schemeAndroid    | String        | N  | Android 앱 링크                                                                                                                                             |
| content.carousel.tail                                      | Object        | N  | 캐러셀 더보기 버튼 정보                                                                                                                                           |
| content.carousel.tail.linkMo                               | String        | Y  | 모바일 웹 링크                                                                                                                                           |
| content.carousel.tail.linkPc                               | String        | N  | 모바일 웹 링크                                                                                                                                           |
| content.carousel.tail.schemeIos                            | String        | N  | 모바일 웹 링크                                                                                                                                           |
| content.carousel.tail.schemeAndroid                        | String        | N  | 모바일 웹 링크                                                                                                                                           |

<span id="free-form-message-request-body-email"></span>

### Email

```json
{
  "sender": {
    "senderMailAddress": "sender@example.com"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "EMAIL_ADDRESS",
          "contact": "recipient@example.com"
        }
      ]
    }
  ],
  "content": {
    "title": "[NHN Cloud Notification Hub] 공지사항",
    "body": "안녕하세요. NHN Cloud Notification Hub 입니다.",
    "attachmentIds": [
      "첨부_파일_아이디"
    ]
  }
}
```

| 이름 | 타입            | 필수 | 설명 |
| --- |---------------|----| --- |
| sender | Object        | N  | 발신자, 푸시 외 다른 메시지 채널은 필수 |
| sender.senderMailAddress | Object        | N  | 발신자 이메일 주소 |
| content | Object        | Y  | 메시지 내용 |
| content.title | Object        | Y  | 제목 |
| content.Object | Y             | 내용 |
| content.attachmentIds | String Array | N  | 첨부 파일 아이디 |

* 발신자 이메일 주소의 도메인은 소유 인증이 완료되어야 합니다.
* 첨부 파일은 30MB 이하로 최대 10개까지 업로드할 수 있습니다.
* 첨부 파일은 총합이 최대 30MB를 초과할 수 없습니다.
* 최대 30MB까지 첨부 가능하지만 수신하는 이메일 시스템(gmail.com, naver.com 등)의 첨부 파일 제한 정책에 따라 **제한 초과**로 거부되거나 스팸 판정률이 높아질 수 있으므로 10MB 이내로 첨부할 것을 권장합니다.
* **recipients[].contacts[].contactType** 필드에는 **EMAIL_ADDRESS**만 사용 가능합니다. 
* **recipients[].contacts[].contact** 필드에는 수신자 이메일 주소를 입력합니다.

<span id="free-form-message-request-body-push"></span>

### Push

```json
{
  "statsId": "통계_아이디",
  "scheduledDateTime": "2024-10-29T06:29:00+09:00",
  "confirmBeforeSend": false,
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "TOKEN_FCM",
          "contact": "토큰"
        }
      ]
    }
  ],
  "content": {
    "unsubscribePhoneNumber": "1234-1234",
    "unsubscribeGuide": "설정 > 메뉴",
    "style": {
      "useHtmlStyle": true
    },
    "title" : "<b>NHN Cloud </b> Notification",
    "body" : "<b>출시 이벤트</b> <i>공지 사항 확인</i>",
    "richMessage" : {
      "buttons" : [{
        "name" : "버튼 이름",
        "submitName": "전송 버튼 이름",
        "buttonType" : "REPLY",
        "link" : "myapp://product_detail?product_id=1234",
        "hint" : "버튼에대한 힌트"
      }
      ],
      "media" : {
        "source" : "URL",
        "mediaType" : "IMAGE",
        "expandable" : true
      },
      "androidMedia": {
        "source" : "URL",
        "mediaType" : "IMAGE",
        "expandable" : true
      },
      "iosMedia": {
        "source" : "URL",
        "mediaType" : "IMAGE",
        "expandable" : true
      },
      "largeIcon" : {
        "source" : "URL"
      },
      "group" : {
        "key" : "그룹의 키",
        "description" : "그룹에대한 설명"
      }
    },
    "customKey" : "customValue"
  }
}
```

| 이름 | 타입                    | 필수 | 설명 |
| --- |-----------------------| --- | --- |
| content | Object                | Y | 메시지 내용 |
| content.unsubscribePhoneNumber | String                | 푸시 메시지 수신 거부를 위한 대표 번호 |
| content.unsubscribeGuide | String                | 푸시 메시지 수신 거부를 위한 안내 |
| content.title | String                | Y | 제목 |
| content.String | Y                     | 내용 |
| content.style.useHtmlStyle | Boolean               | Y | HTML 스타일 사용(Android에서만 가능) |
| content.richMessage | Object                | 리치 메시지 |
| content.richMessage | Object                | N | 리치 메시지 사용시 필요 |
| content.richMessage.buttons | Object Array         | N |  리치 메시지에 추가되는 버튼, 최대 3개까지 가능 |
| content.richMessage.button.name | String                | 버튼 이름 |
| content.richMessage.button.buttonType | String                | 버튼 타입, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS |
| content.richMessage.button.link | String                | 버튼을 눌렀을때, 연결되는 링크 |
| content.richMessage.button.hint | String                | 버튼에대한 힌트 |
| content.richMessage.media | Object                | N |  리치 메시지에 추가되는 미디어 |
| content.richMessage.media.source | String                | 미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE 가능 |
| content.richMessage.media.mediaType | String                | N |  미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원 |
| content.richMessage.media.expandable | Boolean               | N | Android에서 미디어를 클릭 시 펼침 기능 사용 여부 |
| content.richMessage.androidMedia | Object                | N |  Android 기기에 사용되는 미디어. 형식은 media와 동일 |
| content.richMessage.iosMedia | Object                | N |  iOS 기기에 사용되는 미디어. 형식은 media와 동일 |
| content.richMessage.largeIcon | Object                | N |  리치 메시지에 추가되는 큰 아이콘, Android에서만 지원 |
| content.richMessage.largeIcon.source | String                | Y | 미디어의 위치한 곳의 주소 |
| content.richMessage.group | Object                | N |  여러 개의 메시지를 그룹 단위로 묶는 기능, Android에서만 지원 |
| content.richMessage.group.key | String                | Y |  그룹의 키 |
| content.richMessage.group.description | String                | Y |  그룹에대한 설명 |
| content.customKey | Object Array or String Array | N | 사용자 정의 키와 값 |

* 푸시는 **sender** 필드가 필요 없습니다.
* 푸시는 사용자가 정의한 키와 값을 추가해 **content** 필드를 작성할 수 있습니다.
* **recipients[].contacts[].contactType** 필드는 **TOKEN_FCM**, **TOKEN_APNS**, **TOKEN_ADM**, **TOKEN_APNS_SANDBOX**, **TOKEN_APNS_VOIP**, **TOKEN_APNS_VOIP_SANDBOX** 중 하나여야 합니다.
* **recipients[].contacts[].contact** 필드에는 **푸시 토큰**을 입력합니다.


<span id="template-message-sending-request"></span>

## 템플릿 메시지 발송 요청

**요청**

```
POST /message/v1.0/{messageChannel}/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| messageChannel | Path | String | Y | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| messagePurpose | Path | String | Y | 메시지 목적<br>NORMAL, AD, AUTH |

**요청 본문**

```json
{
  "statsKeyId": "통계_아이디",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "templateId": "템플릿_아이디",
  "templateParameters": {
    "key1": "value1",
    "key2": "value2",
    "key3": {
        "key4": "value4",
        "key5": "value5"
    }
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "test"
        }
      ],
      "templateParameters": {
        "key3": {
          "key4": "value4",
          "key5": "value5"
        },
        "key6": "value6"
      }
    }
  ],
  "sender": {
    "senderKey": "발신_키",
    "chatbotId": "대화방_아이디"
  },
  "content": {
    "unsubscribePhoneNumber": "08012341234"
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 이름                                      | 타입                 | 필수 | 설명                                                   |
|-----------------------------------------|--------------------|----|------------------------------------------------------|
| statsKeyId                              | String             | N  | 통계 키 아이디                                             |
| scheduledDateTime                       | DateTime(ISO 8601) | N  | 예약 발송 일시(예: 2024-10-29T06:29:00+09:00)               |
| confirmBeforeSend                       | Boolean            | N  | 발송 전 확인 여부(기본값 false)                                |
| templateId                              | String             | Y  | 템플릿 아이디                                              |
| templateParameters                      | Object             | N  | 템플릿 파라미터                                             |
| recipients                              | Object Array       | Y  | 수신자 배열                                               |
| recipients[].contacts                   | Object Array       | Y  | 수신자의 연락처 배열                                          |
| recipients[].contacts[].contactType     | String             | Y  | 연락처 유형                                               |
| recipients[].contacts[].contact         | String             | Y  | 연락처                                                  |
| recipients[].contacts[].clientReference | String             | N  | 사용자 커스텀 필드                                           |
| recipients[].templateParameters         | Object             | N  | 템플릿 파라미터                                             |
| sender                                  | Object             | N  | 발신자 정보                                               |
| sender.senderKey                        | String             | N  | 발신 키 (메시지 채널이 알림톡인 경우 필수)                            |
| sender.chatbotId                        | String             | N  | 대화방 아이디 (RCS Bizcenter 템플릿인 경우 필수)                   |
| content                                 | Object             | N  | 메시지 내용                                               |
| content.unsubscribePhoneNumber          | String             | N  | 080 수신 거부 번호 (광고 목적의 RCS Bizcenter 템플릿 발송 시 필수) |


* 템플릿 파라미터는 템플릿에 정의된 파라미터와 일치해야 합니다.
* 템플릿 파라미터는 공통 템플릿 파라미터, 수신자 템플릿 파라미터로 구분됩니다.
* 공통 템플릿 파라미터는 모든 수신자에게 동일하게 적용되는 파라미터입니다. 수신자 템플릿 파라미터는 수신자별로 다른 파라미터를 적용할 때 사용합니다.
* 수신자 템플릿 파라미터가 없는 경우 공통 템플릿 파라미터만 적용됩니다. 공통 템플릿 파라미터와 수신자 템플릿 파라미터가 중복되는 경우 수신자 템플릿 파라미터가 우선 적용됩니다.
* 템플릿 파라미터의 값의 타입은 문자열 또는 배열, 객체가 될 수 있습니다. 배열이나 객체 타입은 FREE_MARKER 템플릿에서 사용할 수 있습니다.

**응답 본문**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "messageId": "메시지_아이디"
}
```

<!--응답 본문의 필드를 설명합니다.-->

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 메시지 발송
POST {{endpoint}}/message/v1.0/SMS/template-messages/NORMAL
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "statsKeyId": "통계_아이디",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "templateId": "템플릿_아이디",
  "templateParameters": {
    "key1": "value1",
    "key2": "value2",
    "key3": {
        "key4": "value4",
        "key5": "value5"
    }
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "test"
        }
      ],
      "templateParameters": {
        "key3": {
          "key4": "value4",
          "key5": "value5"
        },
        "key6": "value6"
      }
    }
  ]
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/message/v1.0/SMS/template-messages/${MESSAGE_PURPOSE}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
        "statsKeyId": "통계_아이디",
        "scheduledDateTime": "2024-10-29T00:06:29+09:00",
        "confirmBeforeSend": false,
        "templateId": "템플릿_아이디",
        "templateParameters": {
            "key1": "value1",
            "key2": "value2",
            "key3": {
                "key4": "value4",
                "key5": "value5"
            }
        },
        "recipients": [
            {
            "contacts": [
                {
                "contactType": "PHONE_NUMBER",
                "contact": "01012345678"
                }
            ],
            "templateParameters": {
                "key3": {
                "key4": "value4",
                "key5": "value5"
                },
                "key6": "value6"
            }
            }
        ]
    }'
```

</details>


<span id="template-message-sending-request-rcs"></span>

### RCS 템플릿 메시지 발송 요청 본문 예시
```json
{
  "statsKeyId": "통계_아이디",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "templateId": "템플릿_아이디",
  "templateParameters": {
    "key1": "value1",
    "key2": "value2",
    "key3": {
        "key4": "value4",
        "key5": "value5"
    }
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "test"
        }
      ],
      "templateParameters": {
        "key3": {
          "key4": "value4",
          "key5": "value5"
        },
        "key6": "value6"
      }
    }
  ],
  "sender": {
    "brandId": "브랜드_아이디",
    "chatbotId": "대화방_아이디"
  },
  "content": {
    "unsubscribePhoneNumber": "08012341234"
  },
  "options": {
    "expiryOption": 1,
    "groupId":"groupId"
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 이름                                      | 타입                 | 필수 | 설명                                                   |
|-----------------------------------------|--------------------|----|------------------------------------------------------|
| statsKeyId                              | String             | N  | 통계 키 아이디                                             |
| scheduledDateTime                       | DateTime(ISO 8601) | N  | 예약 발송 일시(예: 2024-10-29T06:29:00+09:00)               |
| confirmBeforeSend                       | Boolean            | N  | 발송 전 확인 여부(기본값 false)                                |
| templateId                              | String             | Y  | 템플릿 아이디                                              |
| templateParameters                      | Object             | N  | 템플릿 파라미터                                             |
| recipients                              | Object Array       | Y  | 수신자 배열                                               |
| recipients[].contacts                   | Object Array       | Y  | 수신자의 연락처 배열                                          |
| recipients[].contacts[].contactType     | String             | Y  | 연락처 유형                                               |
| recipients[].contacts[].contact         | String             | Y  | 연락처                                                  |
| recipients[].contacts[].clientReference | String             | N  | 사용자 커스텀 필드                                           |
| recipients[].templateParameters         | Object             | N  | 템플릿 파라미터                                             |
| sender                                  | Object             | N  | 발신자 정보                                               |
| sender.chatbotId                        | String             | N  | 대화방 아이디 (RCS Bizcenter 템플릿인 경우 필수)               |
| content                                 | Object             | N  | 메시지 내용                                               |
| content.unsubscribePhoneNumber          | String             | N  | 080 수신 거부 번호 (광고 목적의 RCS Bizcenter 템플릿 발송 시 필수) |
| options                                 | Object             | N  | 발송 옵션                                                 |
| options.expiryOption                    | Integer            | N  | 디바이스로의 전송 시도에 대한 타임아웃 (1: 1일, 2: 40초, 3: 3분, 4: 1시간)  |
| options.groupId                         | String             | N  | RCS BizCenter 통계 연동을 위한 그룹 아이디                     |


<span id="flow-message-sending-request"></span>

## 플로우 메시지 발송 요청

**요청**

```
POST /message/v1.0/flow-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| messagePurpose | Path | String | Y | 메시지 목적<br>NORMAL, AD, AUTH |

**요청 본문**


```json
{
  "statsKeyId": "통계_아이디",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "flowId": "템플릿_아이디",
  "templateParameters": {
    "key1": "value1",
    "key2": "value2",
    "key3": {
        "key4": "value4",
        "key5": "value5"
    }
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "TOKEN_FCM",
          "contact": "token"
        },
        {
          "contactType": "EMAIL_ADDRESS",
          "contact": "recipient@example.com"
        },
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345679",
          "clientReference": "test"
        }
      ],
      "templateParameters": {
        "key3": {
          "key4": "value4",
          "key5": "value5"
        },
        "key6": "value6"
      }
    }
  ],
  "flow": {
    "steps": [
      {
        "messageChannel": "SMS",
        "nextSteps": [
          {
            "messageChannel": "RCS",
            "sender": {
              "chatbotId": "대화방_아이디"
            },
            "content": {
              "unsubscribePhoneNumber": "08012341234"
            }
          }
        ]
      }
    ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 이름                                      | 타입             | 필수 | 설명                                     |
|-----------------------------------------| ----------------|----|----------------------------------------|
| statsKeyId                              | String         | N  | 통계 키 아이디                               |
| scheduledDateTime                       | DateTime(ISO 8601) | N  | 예약 발송 일시(예: 2024-10-29T06:29:00+09:00) |
| confirmBeforeSend                       | Boolean        | N  | 발송 전 확인 여부(기본값 false)                  |
| flowId                                  | String         | Y  | 풀로우 아이디                                |
| templateParameters                      | Object         | N  | 메시지 공통 템플릿 파라미터                        |
| recipients                              | Object Array          | Y  | 수신자 배열                                 |
| recipients[].contacts                   | Object Array          | Y  | 수신자의 연락처 배열                            |
| recipients[].contacts[].contactType     | String         | Y  | 연락처 유형                                 |
| recipients[].contacts[].contact         | String         | Y  | 연락처                                    |
| recipients[].contacts[].clientReference | String         | N  | 사용자 커스텀 필드                        |
| recipients[].templateParameters         | Object         | N  | 수신자 별 템플릿 파라미터                         |
| flow                                    | Object | N  | 플로우 |
| flow.steps[]                            | Array | Y  | 플로우 단계 |
| flow.steps[].messageChannel             | String | Y  | 메시지 채널<br>SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH |
| flow.steps[].sender                     | Object | N  | 발신자 정보입니다. 발신자 정보는 메시지 채널에 따라 다르게 구성될 수 있습니다. |
| flow.steps[].content                    | Object | N  | 메시지 내용입니다. 메시지 내용은 메시지 채널에 따라 다르게 구성될 수 있습니다. |
| flow.steps[].nextSteps[]                | Array | N  | 다음 단계입니다. |

* 플로우 메시지 발송도 템플릿 메시지 발송과 동일하게 템플릿 파라미터를 사용합니다.
* 수신자의 연락처는 플로우에서 사용하는 메시지 채널에 필요한 연락처가 모두 포함되어야 합니다.
* 필수값이 필요한 템플릿을 사용하는 플로우인 경우 flow를 통해 필수값을 지정할 수 있습니다. 이때, flow의 구성은 발송하려는 flowId의 flow와 동일하게 구성해야 합니다.

**응답 본문**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "messageId": "메시지_아이디"
}
```

<!--응답 본문의 필드를 설명합니다.-->

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 메시지 발송
POST {{endpoint}}/message/v1.0/flow-messages/{{messagePurpose}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "statsKeyId": "통계_아이디",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "flowId": "플로우_아이디",
  "templateParameters": {
    "key1": "value1",
    "key2": "value2",
    "key3": {
        "key4": "value4",
        "key5": "value5"
    }
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "TOKEN_FCM",
          "contact": "token"
        },
        {
          "contactType": "EMAIL_ADDRESS",
          "contact": "recipient@example.com"
        }
      ],
        "templateParameters": {
          "key3": {
            "key4": "value4",
            "key5": "value5"
          },
          "key6": "value6"
        }
      }
    ]
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/message/v1.0/flow-messages/${MESSAGE_PURPOSE}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
       "statsKeyId": "통계_아이디",
       "scheduledDateTime": "2024-10-29T00:06:29+09:00",
       "confirmBeforeSend": false,
       "flowId": "플로우_아이디",
       "templateParameters": {
         "key1": "value1",
         "key2": "value2",
         "key3": {
           "key4": "value4",
           "key5": "value5"
         }
       },
       "recipients": [
         {
           "contacts": [
             {
               "contactType": "TOKEN_FCM",
               "contact": "token"
             },
             {
               "contactType": "EMAIL_ADDRESS",
               "contact": "recipient@example.com"
             }
           ],
           "templateParameters": {
             "key3": {
               "key4": "value4",
               "key5": "value5"
             },
             "key6": "value6"
           }
         }
       ]
     }'
```

</details>

<span id="flow-message-sending-request-rcs-step"></span>

### 플로우 메시지 발송 요청 본문 RCS Step 예시

```json
{
  "statsKeyId": "통계_아이디",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "flowId": "플로우_아이디",
  "templateParameters": {
    "key1": "value1",
    "key3": {
        "key4": "value4",
        "key5": "value5"
    }
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345679",
          "clientReference": "test"
        }
      ],
      "templateParameters": {
        "key3": {
          "key4": "value4",
          "key5": "value5"
        },
        "key6": "value6"
      }
    }
  ],
  "flow": {
    "steps": [
      {
        "messageChannel": "RCS",
        "sender": {
          "chatbotId": "대화방_아이디"
        },
        "content": {
          "unsubscribePhoneNumber": "08012341234"
        },
        "options": {
          "expiryOption": 1,
          "groupId":"groupId"
        },
        "nextSteps": []
      }
    ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 이름                                      | 타입             | 필수 | 설명                                     |
|-----------------------------------------| ----------------|----|-------------------------------------------|
| flow.steps[]                            | Array | Y  | 플로우 단계 |
| flow.steps[].messageChannel             | String | Y  | 메시지 채널<br>SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH |
| flow.steps[].sender                     | Object         | N  | 발신자 정보                                    |
| flow.steps[].sender.chatbotId           | String         | N  | 대화방 아이디 (RCS Bizcenter 템플릿인 경우 필수)    |
| flow.steps[].content                    | Object         | N  | 메시지 내용                                    |
| flow.steps[].content.unsubscribePhoneNumber | String     | N  | 080 수신 거부 번호 (광고 목적의 RCS Bizcenter 템플릿 발송 시 필수) |
| flow.steps[].options                    | Object         | N  | 발송 옵션                                     |
| flow.steps[].options.expiryOption       | Integer        | N  | 디바이스로의 전송 시도에 대한 타임아웃 (1: 1일, 2: 40초, 3: 3분, 4: 1시간)  |
| flow.steps[].options.groupId            | String         | N  | RCS BizCenter 통계 연동을 위한 그룹 아이디         |
| flow.steps[].nextSteps[]                | Object Array   | N  | 다음 단계입니다.                                |

<span id="cancel-message-sending-request"></span>

## 메시지 요청 취소

발송 전 예약 메시지, 승인 후 발송 메시지의 발송 요청을 취소합니다. 요청 취소된 메시지는 연락처별 수신 결과 조회에서 조회할 수 있습니다.

**요청**

```
POST /message/v1.0/messages/{messageId}/do-cancel
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| messageId | Path | String | Y | 메시지 아이디 |


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
### 메시지 요청 취소
POST {{endpoint}}/message/v1.0/messages/{{messageId}}/do-cancel
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/message/v1.0/messages/${MESSAGE_ID}/do-cancel" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>


## 인스턴트 플로우 메시지 발송 요청
**요청**

```
POST /message/v1.0/instant-flow-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| messagePurpose | Path | String | Y | 메시지 목적<br>NORMAL, AD, AUTH |

**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```json
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2021-01-01T00:00:00Z",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key": "value"
  },
  "recipients" : [ 
    {
      "contacts" : [ 
        {
          "contactType" : "PHONE_NUMBER",
          "contact" : "01012345678",
          "clientReference": "test"
        } 
      ],
      "templateParameters" : {
        "key": "value"
      }
    } 
  ],
  "instantFlow" : {
    "steps" : [ 
      {
        "messageChannel" : "RCS",
        "sender" : {
          "brandId": "브랜드_이이디",
          "chatbotId": "대화방_아이디"
        },
        "content" : {
          "lmsType" : "STANDALONE",
          "cards" : [
            {
              "title" : "제목",
              "description" : "본문"
            }
          ]
        },
        "templateId" : "템플릿_아이디",
        "nextSteps" : [ 
          {
            "messageChannel" : "SMS",
            "sender" : {
              "senderPhoneNumber" : "0123456789"
            },
            "content" : {
              "title" : "제목",
              "body" : "본문"
            },
            "templateId" : "템플릿_아이디",
            "nextSteps" : [ ]
          } 
        ]
      } 
    ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | N   | 통계 키 아이디                                                                                                                              |
| scheduledDateTime | DateTime(ISO 8601) | N   | 예약 발송 일시(예: 2024-10-29T06:29:00+09:00)                                                                                                |
| confirmBeforeSend | Boolean | N   | 발송 전 확인 여부(기본값 false)      
| templateParameters | Object | N | 템플릿 파라미터입니다. 템플릿 아이디를 설정하는 경우 필수입니다. |
| recipients[] | Array | Y | 수신자 목록록 |
| recipients[].contacts[] | Array | N | 수신자 연락처 목록입니다. |
| recipients[].contacts[].contactType | String | Y | 연락처 타입<br>PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP |
| recipients[].contacts[].contact | String | Y | 연락처 입니다. 수신자를 지정하지 않고 연락처를 직접 입력하여 메시지를 발송할 수 있습니다. |
| recipients[].contacts[].clientReference | String         | N | 사용자 커스텀 필드                        |
| recipients[].templateParameters |  | N | 템플릿 파라미터입니다. 템플릿 아이디를 설정하는 경우 필수입니다.  |
| instantFlow | Object | Y | 인스턴트 플로우입니다. 플로우 생성 없이 정의할 수 있습니다. |
| instantFlow.steps[] | Array | Y | 인스턴트 플로우 단계입니다. |
| instantFlow.steps[].messageChannel | String | Y | 메시지 채널<br>SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH |
| instantFlow.steps[].sender | Object | N | 발신자 정보입니다. 발신자 정보는 메시지 채널에 따라 다르게 구성될 수 있습니다.<br> |
| instantFlow.steps[].content | Object | N | 메시지 내용입니다. 메시지 내용은 메시지 채널에 따라 다르게 구성될 수 있습니다.<br> |
| instantFlow.steps[].templateId | String | N | 템플릿 아이디입니다. 템플릿 아이디를 설정한 경우, 요청 시 발신자 정보(sender)와 메시지 내용(content)가 적용되지 않습니다.<br>인스턴트 플로우 메시지에서 템플릿 아이디를 설정하지 않는 경우, 발신자 정보(sender)와 메시지 내용(content)이 반드시 필요합니다.<br> |
| instantFlow.steps[].nextSteps[] | Array | N | 다음 단계입니다. 다음 단계가 없는 경우, 메시지 발송이 종료됩니다. |

* 한번 사용된 메시지 채널은 다음 단계에서 사용할 수 없습니다.
* 한 단계는 여러 개의 다음 단계를 가질 수 있습니다.

**응답 본문**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "messageId" : "aA123456"
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | true |
| header.resultCode | Integer | 0 |
| header.resultMessage | String | SUCCESS |
| messageId | String | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |

**실패 응답 - 중복 수신자**

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 400004,
    "resultMessage" : "중복된 수신자 연락처가 있습니다."
  },
  "duplicatedContacts" : [
    {
      "contactType": "PHONE_NUMBER",
      "contact": "0123456789"
    }
  ]
}
```




**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 인스턴트 플로우 메시지 발송
POST {{endpoint}}/message/v1.0/instant-flow-messages/{{messagePurpose}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}

{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2021-01-01T00:00:00Z",
  "confirmBeforeSend" : false,
  "templateParameters" : "templateParameters" : {
    "key": "value"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678"
    } ],
    "templateParameters" : {
      "key": "value"
    }
  } ],
  "instantFlow" : {
    "steps" : [ {
      "messageChannel" : "SMS",
      "sender" : {
        "senderPhoneNumber" : "0123456789"
      },
      "content" : {
        "title" : "제목",
        "body" : "본문"
      },
      "templateId" : "템플릿_아이디",
      "nextSteps" : [ ]
    } ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${ENDPOINT}/message/v1.0/instant-flow-messages/{messagePurpose}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
     -d '{
      "statsKeyId" : "aA123456",
      "scheduledDateTime" : "2021-01-01T00:00:00Z",
      "confirmBeforeSend" : false,
      "templateParameters" : {
          "key": "value"
      },
      "recipients" : [ {
        "contacts" : [ {
          "contactType" : "PHONE_NUMBER",
          "contact" : "01012345678"
        } ],
        "templateParameters" : {
          "key": "value"
        }
      } ],
      "instantFlow" : {
        "steps" : [ {
          "messageChannel" : "SMS",
          "sender" : {
            "senderPhoneNumber" : "0123456789"
          },
          "content" : {
            "title" : "제목",
            "body" : "본문"
          },
          "templateId" : "템플릿_아이디",
          "nextSteps" : [ ]
        } ]
      }
     }'
```

</details>

<span id="instant-flow-message-sending-request-rcs-step"></span>

### 인스턴트 플로우 메시지 발송 요청 본문 RCS Step 예시

```json
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2021-01-01T00:00:00Z",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key": "value"
  },
  "recipients" : [ 
    {
      "contacts" : [ 
        {
          "contactType" : "PHONE_NUMBER",
          "contact" : "01012345678",
          "clientReference": "test"
        } 
      ],
      "templateParameters" : {
        "key": "value"
      }
    } 
  ],
  "instantFlow" : {
    "steps" : [ 
      {
        "messageChannel" : "RCS",
        "sender" : {
          "brandId": "브랜드_이이디",
          "chatbotId": "대화방_아이디"
        },
        "content" : {
          "lmsType" : "STANDALONE",
          "cards" : [
            {
              "title" : "제목",
              "description" : "본문"
            }
          ]
        },
        "options": {
          "expiryOption": 1,
          "groupId":"groupId"
        },
        "templateId" : "템플릿_아이디",
        "nextSteps" : [ 
          {
            "messageChannel" : "SMS",
            "sender" : {
              "senderPhoneNumber" : "0123456789"
            },
            "content" : {
              "title" : "제목",
              "body" : "본문"
            },
            "templateId" : "템플릿_아이디",
            "nextSteps" : [ ]
          } 
        ]
      } 
    ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 이름                                      | 타입             | 필수 | 설명                                     |
|-----------------------------------------| ----------------|----|-------------------------------------------|
| instantFlow.steps[]                            | Array          | Y  | 플로우 단계                                    |
| instantFlow.steps[].messageChannel             | String         | Y  | 메시지 채널<br>SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH |
| instantFlow.steps[].templateId | String | N | 템플릿 아이디입니다. 템플릿 아이디를 설정한 경우, 요청 시 발신자 정보(sender)와 메시지 내용(content)가 적용되지 않습니다.<br>인스턴트 플로우 메시지에서 템플릿 아이디를 설정하지 않는 경우, 발신자 정보(sender)와 메시지 내용(content)이 반드시 필요합니다.<br> |
| instantFlow.steps[].sender                     | Object         | N  | 발신자 정보 (자유 양식 메시지 발송 요청 RCS 본문 예시 참고) |
| instantFlow.steps[].content                    | Object         | N  | 메시지 내용(자유 양식 메시지 발송 요청 RCS 본문 예시 참고)  |
| instantFlow.steps[].options                    | Object         | N  | 발송 옵션(자유 양식 메시지 발송 요청 RCS 본문 예시 참고)  |
| instantFlow.steps[].nextSteps[]                | Object Array   | N  | 다음 단계입니다.                                |
