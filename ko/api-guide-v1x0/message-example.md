<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>메시지 - 발송 요청 본문 예시</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 메시지 - 발송 요청 본문 예시**


<span id="sms"></span>

## SMS

<span id="sms-sms"></span>

### SMS(단문)

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
          "clientReference": "클라이언트_레퍼런스"
        }
      ]
    }
  ],
  "content": {
    "messageType": "SMS",
    "body": "안녕하세요. NHN Cloud Notification Hub 입니다.",
  }
}
```

| 이름 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- |
| sender | Object | Y | 발신자 |
| sender.senderPhoneNumber | String | Y | 발신자 번호 |
| content | Object | Y | 메시지 내용 |
| content.messageType | String | Y | SMS |
| content.body | String | Y | 내용 |

### LMS(장문)

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
          "clientReference": "클라이언트_레퍼런스"
        }
      ]
    }
  ],
  "content": {
    "messageType": "LMS",
    "title": "[NHN Cloud Notification Hub] 공지사항",
    "body": "안녕하세요. NHN Cloud Notification Hub 입니다."
  }
}
```

| 이름 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- |
| sender | Object | Y | 발신자 |
| sender.senderPhoneNumber | String | Y | 발신자 번호 |
| content | Object | Y | 메시지 내용 |
| content.messageType | String | Y | LMS |
| content.title | String | Y | 제목 |
| content.body | String | Y | 내용 |

### MMS(미디어 장문)

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
          "clientReference": "클라이언트_레퍼런스"
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
| sender | Object | Y | 발신자 |
| sender.senderPhoneNumber | String | Y | 발신자 번호 |
| content | Object | Y | 메시지 내용 |
| content.messageType | String | Y | MMS |
| content.body | String | Y | 내용 |
| content.attachmentIds | String Array | Y | 첨부 파일 아이디<br>첨부 이미지 제한 사항.<br>지원 코덱: .jpg, .jpeg<br>첨부 이미지 개수: 3개 이하.<br>첨부 이미지 사이즈: 1개당 300KB 이하. 단, 첨부한 이미지의 개수가 3개일 경우 합산 800KB 이하.<br>첨부 이미지 해상도: 1000*1000 이하. |


<span id="rcs"></span>

## RCS

<span id="rcs-sms"></span>

### SMS

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
          "clientReference": "클라이언트_레퍼런스"
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
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "홈페이지로 이동"
                }
              }
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


| 이름 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | 
| sender | Object | Y | 발신자 |
| sender.brandId | String | Y | 브랜드 아이디 |
| sender.chatbotId | String | Y | 대화방 아이디 |
| content | Object | Y | 메시지 내용 |
| content.messageType | String | Y | RCS 내 메시지 유형, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 수신 거부 번호, 발송 목적이 광고인 경우 필수 |
| content.smsType | String | Y | SMS 타입, 메시지 유형이 SMS인 경우 필수, STANDALONE(스탠다드) |
| content.cards | Object Array | Y | 카드 |
| content.cards[].title | String | N | 제목 |
| content.cards[].description | String | Y | 내용 |
| content.cards[].buttons | Object Array | N | 버튼 |
| content.cards[].buttons[].buttonType | String | Y | 버튼 타입<br>COMPOSE(대화방 열기), CLIPBOARD(복사하기), DIALER(전화 걸기), MAP_SHOW(지도 보여주기), MAP_QUERY(지도 검색하기), MAP_SHARE(현재 위치 공유하기), URL(URL 연결하기), CALENDAR(일정 등록하기) |
| content.cards[].buttons[].buttonJson | Object | Y | 버튼 Json, 버튼 타입에 맞는 포맷 확인 |
| options | Object | N | 발송 옵션 |
| options.expiryOption | Integer | N | RCS 메시지 수신 대기 만료 기간 설정값(1: 1일, 2: 40초, 3: 3분, 4: 1시간) |
| options.groupId | String | N | RCS Biz Center 통계 연동을 위한 group ID [가이드](../console-guide/send-a-message/#RCS) (최대 20 Byte) |

<span id="free-form-message-request-body-rcs-lms-standalone"></span>

### LMS 스탠다드

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
          "clientReference": "클라이언트_레퍼런스"
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
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "홈페이지로 이동"
                }
              }
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

| 이름 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- |
| sender | Object | Y | 발신자 |
| sender.brandId | String | Y | 브랜드 아이디 |
| sender.chatbotId | String | Y | 대화방 아이디 |
| content | Object | Y | 메시지 내용 |
| content.messageType | String | Y | RCS 내 메시지 유형, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 수신 거부 번호, 발송 목적이 광고인 경우 필수 |
| content.lmsType | String | Y | LMS 타입, 메시지 유형이 LMS인 경우 필수, STANDALONE(스탠다드), FORMAT_BASIC(포맷 기본형), FORMAT_TITLE_HIGHLIGHT(포맷 타이틀 강조형), FORMAT_PARAGRAPH(포맷 문단형) |
| content.cards | Object Array | Y | 카드 |
| content.cards[].title | String | N | 제목 |
| content.cards[].description | String | Y | 내용 |
| content.cards[].buttons | Object Array | N | 버튼 |
| content.cards[].buttons[].buttonType | String | Y | 버튼 타입<br>COMPOSE(대화방 열기), CLIPBOARD(복사하기), DIALER(전화 걸기), MAP_SHOW(지도 보여주기), MAP_QUERY(지도 검색하기), MAP_SHARE(현재 위치 공유하기), URL(URL 연결하기), CALENDAR(일정 등록하기) |
| content.cards[].buttons[].buttonJson | Object | Y | 버튼 Json, 버튼 타입에 맞는 포맷 확인 |
| options | Object | N | 발송 옵션 |
| options.expiryOption | Integer | N | RCS 메시지 수신 대기 만료 기간 설정값(1: 1일, 2: 40초, 3: 3분, 4: 1시간) |
| options.groupId | String | N | RCS Biz Center 통계 연동을 위한 group ID [가이드](../console-guide/send-a-message/#RCS) (최대 20 Byte) |

<span id="free-form-message-request-body-rcs-lms-format-basic"></span>

### LMS 포맷 기본형 및 포맷 타이틀 강조형
* mTitleMedia 아이콘 파일 ID 목록
  * 프로모션: LT-messagebase.common-jFBCKu
  * 쿠폰: LT-messagebase.common-LbshOv
  * 이벤트: LT-messagebase.common-aWdsJX
  * 예약: LT-messagebase.common-5eFcIF
  * 영수증: LT-messagebase.common-rJQ22U
  * 알림: LT-messagebase.common-j11Gtf

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
          "clientReference": "클라이언트_레퍼런스"
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
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "홈페이지로 이동"
                }
              }
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

| 이름 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | 
| sender | Object | Y | 발신자 |
| sender.brandId | String | Y | 브랜드 아이디 |
| sender.chatbotId | String | Y | 대화방 아이디 |
| content | Object | Y | 메시지 내용 |
| content.messageType | String | Y | RCS 내 메시지 유형, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 수신 거부 번호, 발송 목적이 광고인 경우 필수 |
| content.lmsType | String | Y | LMS 타입, 메시지 유형이 LMS인 경우 필수, STANDALONE(스탠다드), FORMAT_BASIC(포맷 기본형), FORMAT_TITLE_HIGHLIGHT(포맷 타이틀 강조형), FORMAT_PARAGRAPH(포맷 문단형) |
| content.cards | Object Array | Y | 카드 |
| content.cards[].mTitle | String | Y | 메인 타이틀 |
| content.cards[].mTitleMedia | String | N | 메인 타이틀 아이콘 |
| content.cards[].title | String | N | 제목 |
| content.cards[].description | String | Y | 내용 |
| content.cards[].buttons | Object Array | N | 버튼 |
| content.cards[].buttons[].buttonType | String | Y | 버튼 타입<br>COMPOSE(대화방 열기), CLIPBOARD(복사하기), DIALER(전화 걸기), MAP_SHOW(지도 보여주기), MAP_QUERY(지도 검색하기), MAP_SHARE(현재 위치 공유하기), URL(URL 연결하기), CALENDAR(일정 등록하기) |
| content.cards[].buttons[].buttonJson | Object | Y | 버튼 Json, 버튼 타입에 맞는 포맷 확인 |
| options | Object | N | 발송 옵션 |
| options.expiryOption | Integer | N | RCS 메시지 수신 대기 만료 기간 설정값(1: 1일, 2: 40초, 3: 3분, 4: 1시간) |
| options.groupId | String | N | RCS Biz Center 통계 연동을 위한 group ID [가이드](../console-guide/send-a-message/#RCS) (최대 20 Byte) |

### LMS 포맷 문단형 타입
* mTitleMedia 아이콘 파일 ID 목록
  * 프로모션: LT-messagebase.common-jFBCKu
  * 쿠폰: LT-messagebase.common-LbshOv
  * 이벤트: LT-messagebase.common-aWdsJX
  * 예약: LT-messagebase.common-5eFcIF
  * 영수증: LT-messagebase.common-rJQ22U
  * 알림: LT-messagebase.common-j11Gtf

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
          "clientReference": "클라이언트_레퍼런스"
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
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "공지1 버튼"
                }
              }
            },
            {},
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "공지2 버튼"
                }
              }
            },
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "공지2 버튼"
                }
              }
            },
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "공지3 버튼"
                }
              }
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

| 이름 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | 
| sender | Object | Y | 발신자 |
| sender.brandId | String | Y | 브랜드 아이디 |
| sender.chatbotId | String | Y | 대화방 아이디 |
| content | Object | Y | 메시지 내용 |
| content.messageType | String | Y | RCS 내 메시지 유형, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 수신 거부 번호, 발송 목적이 광고인 경우 필수 |
| content.lmsType | String | Y | LMS 타입, 메시지 유형이 LMS인 경우 필수, STANDALONE(스탠다드), FORMAT_BASIC(포맷 기본형), FORMAT_TITLE_HIGHLIGHT(포맷 타이틀 강조형), FORMAT_PARAGRAPH(포맷 문단형) |
| content.cards | Object Array | Y | 카드 |
| content.cards[].mTitle | String | Y | 메인 타이틀 |
| content.cards[].mTitleMedia | String | N | 메인 타이틀 아이콘 |
| content.cards[].title1 | String | N | 제목(문단 1) |
| content.cards[].description1 | String | Y | 내용(문단 1) |
| content.cards[].title2 | String | N | 제목(문단 2) |
| content.cards[].description2 | String | Y | 내용(문단 2) |
| content.cards[].title3 | String | N | 제목(문단 3) |
| content.cards[].description3 | String | Y | 내용(문단 3) |
| content.cards[].buttons | Object Array | N | 버튼 |
| content.cards[].buttons[].buttonType | String | Y | 버튼 타입<br>COMPOSE(대화방 열기), CLIPBOARD(복사하기), DIALER(전화 걸기), MAP_SHOW(지도 보여주기), MAP_QUERY(지도 검색하기), MAP_SHARE(현재 위치 공유하기), URL(URL 연결하기), CALENDAR(일정 등록하기) |
| content.cards[].buttons[].buttonJson | Object | Y | 버튼 Json, 버튼 타입에 맞는 포맷 확인 |
| options | Object | N | 발송 옵션 |
| options.expiryOption | Integer | N | RCS 메시지 수신 대기 만료 기간 설정값(1: 1일, 2: 40초, 3: 3분, 4: 1시간) |
| options.groupId | String | N | RCS Biz Center 통계 연동을 위한 group ID [가이드](../console-guide/send-a-message/#RCS) (최대 20 Byte) |



### MMS 가로형, 세로형

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
          "clientReference": "클라이언트_레퍼런스"
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
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "홈페이지로 이동"
                }
              }
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


| 이름 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | 
| sender | Object | Y | 발신자 |
| sender.brandId | String | Y | 브랜드 아이디 |
| sender.chatbotId | String | Y | 대화방 아이디 |
| content | Object | Y | 메시지 내용 |
| content.messageType | String | Y | RCS 내 메시지 유형, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 수신 거부 번호, 발송 목적이 광고인 경우 필수 |
| content.mmsType | String | Y | MMS 타입, 메시지 유형이 MMS인 경우 필수, HORIZONTAL(가로형), VERTICAL(세로형), CAROUSEL_MEDIUM(캐러셀 중간), CAROUSEL_SMALL(캐러셀 작게) |
| content.cards | Object Array | Y | 카드 |
| content.cards[].title | String | N | 제목 |
| content.cards[].description | String | Y | 내용 |
| content.cards[].attachmentId | String | Y | 첨부 파일 아이디 |
| content.cards[].buttons | Object Array | N | 버튼 |
| content.cards[].buttons[].buttonType | String | Y | 버튼 타입<br>COMPOSE(대화방 열기), CLIPBOARD(복사하기), DIALER(전화 걸기), MAP_SHOW(지도 보여주기), MAP_QUERY(지도 검색하기), MAP_SHARE(현재 위치 공유하기), URL(URL 연결하기), CALENDAR(일정 등록하기) |
| content.cards[].buttons[].buttonJson | Object | Y | 버튼 Json, 버튼 타입에 맞는 포맷 확인 |
| options | Object | N | 발송 옵션 |
| options.expiryOption | Integer | N | RCS 메시지 수신 대기 만료 기간 설정값(1: 1일, 2: 40초, 3: 3분, 4: 1시간) |
| options.groupId | String | N | RCS Biz Center 통계 연동을 위한 group ID [가이드](../console-guide/send-a-message/#RCS) (최대 20 Byte) |

### MMS 캐러셀

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
          "clientReference": "클라이언트_레퍼런스"
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
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "홈페이지로 이동"
                }
              }
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
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "홈페이지로 이동"
                }
              }
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
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "홈페이지로 이동"
                }
              }
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


| 이름 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | 
| sender | Object | Y | 발신자 |
| sender.brandId | String | Y | 브랜드 아이디 |
| sender.chatbotId | String | Y | 대화방 아이디 |
| content | Object | Y | 메시지 내용 |
| content.messageType | String | Y | RCS 내 메시지 유형, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 수신 거부 번호, 발송 목적이 광고인 경우 필수 |
| content.mmsType | String | Y | MMS 타입, 메시지 유형이 MMS인 경우 필수, HORIZONTAL(가로형), VERTICAL(세로형), CAROUSEL_MEDIUM(캐러셀 중간), CAROUSEL_SMALL(캐러셀 작게) |
| content.cards | Object Array | Y | 카드 |
| content.cards[].title | String | N | 제목 |
| content.cards[].description | String | Y | 내용 |
| content.cards[].attachmentId | String | Y | 첨부 파일 아이디 |
| content.cards[].buttons | Object Array | N | 버튼 |
| content.cards[].buttons[].buttonType | String | Y | 버튼 타입<br>COMPOSE(대화방 열기), CLIPBOARD(복사하기), DIALER(전화 걸기), MAP_SHOW(지도 보여주기), MAP_QUERY(지도 검색하기), MAP_SHARE(현재 위치 공유하기), URL(URL 연결하기), CALENDAR(일정 등록하기) |
| content.cards[].buttons[].buttonJson | Object | Y | 버튼 Json, 버튼 타입에 맞는 포맷 확인 |
| options | Object | N | 발송 옵션 |
| options.expiryOption | Integer | N | RCS 메시지 수신 대기 만료 기간 설정값(1: 1일, 2: 40초, 3: 3분, 4: 1시간) |
| options.groupId | String | N | RCS Biz Center 통계 연동을 위한 group ID [가이드](../console-guide/send-a-message/#RCS) (최대 20 Byte) |

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

| 이름 | 타입 | 필수 | 설명 |
| --- |---------------| --- | --- |
| sender | Object | N | 발신자, 푸시 외 다른 메시지 채널은 필수 |
| sender.senderMailAddress | Object | N | 발신자 이메일 주소 |
| content | Object | Y | 메시지 내용 |
| content.title | Object | Y | 제목 |
| content.Object | Y | 내용 |
| content.attachmentIds | String Array | N | 첨부 파일 아이디 |

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

| 이름 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- |
| content | Object | Y | 메시지 내용 |
| content.unsubscribePhoneNumber | String | N | 푸시 메시지 수신 거부를 위한 대표 번호 |
| content.unsubscribeGuide | String | N | 푸시 메시지 수신 거부를 위한 안내 |
| content.title | String | Y | 제목 |
| content.body | String | Y | 내용 |
| content.style.useHtmlStyle | Boolean | Y | HTML 스타일 사용(Android에서만 가능) |
| content.richMessage | Object | N | 리치 메시지 사용 시 필요 |
| content.richMessage.buttons | Object Array | N | 리치 메시지에 추가되는 버튼, 최대 3개까지 가능 |
| content.richMessage.buttons.name | String | N | 버튼 이름 |
| content.richMessage.buttons.buttonType | String | N | 버튼 타입: REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS |
| content.richMessage.buttons.link | String | N | 버튼을 눌렀을 때 연결되는 링크 |
| content.richMessage.buttons.hint | String | N | 버튼에 대한 힌트 |
| content.richMessage.media | Object | N | 리치 메시지에 추가되는 미디어 |
| content.richMessage.media.source | String | N | 미디어의 주소 (URL, LOCAL_RESOURCE 가능) |
| content.richMessage.media.mediaType | String | N | 미디어 타입: IMAGE, GIF, VIDEO, AUDIO. Android는 IMAGE만 지원 |
| content.richMessage.media.expandable | Boolean | N | Android에서 미디어 클릭 시 펼침 기능 사용 여부 |
| content.richMessage.androidMedia | Object | N | Android 기기 전용 미디어. media 형식과 동일 |
| content.richMessage.iosMedia | Object | N | iOS 기기 전용 미디어. media 형식과 동일 |
| content.richMessage.largeIcon | Object | N | 리치 메시지에 추가되는 큰 아이콘, Android만 지원 |
| content.richMessage.largeIcon.source | String | Y | 아이콘의 주소 |
| content.richMessage.group | Object | N | 여러 메시지를 그룹으로 묶는 기능, Android만 지원 |
| content.richMessage.group.key | String | Y | 그룹 키 |
| content.richMessage.group.description | String | Y | 그룹 설명 |
| content.customKey | Object Array or String Array | N | 사용자 정의 키와 값 |

* 푸시는 **sender** 필드가 필요 없습니다.
* 푸시는 사용자가 정의한 키와 값을 추가해 **content** 필드를 작성할 수 있습니다.
* **recipients[].contacts[].contactType** 필드는 **TOKEN_FCM**, **TOKEN_APNS**, **TOKEN_ADM**, **TOKEN_APNS_SANDBOX**, **TOKEN_APNS_VOIP**, **TOKEN_APNS_VOIP_SANDBOX** 중 하나여야 합니다.
* **recipients[].contacts[].contact** 필드에는 **푸시 토큰**을 입력합니다.
