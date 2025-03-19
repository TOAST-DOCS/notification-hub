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
| sender.senderKey                        | String             | N  | 발신 키(메시지 채널이 알림톡인 경우 필수)                            |
| sender.chatbotId                        | String             | N  | 대화방 아이디(RCS Bizcenter 템플릿인 경우 필수)                   |
| content                                 | Object             | N  | 메시지 내용                                               |
| content.unsubscribePhoneNumber          | String             | N  | 080 수신 거부 번호(광고 목적의 RCS Bizcenter 템플릿 발송 시 필수) |


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
| sender                                  | Object             | N  | 발신자 정보                                               |
| sender.chatbotId                        | String             | N  | 대화방 아이디(RCS Bizcenter 템플릿인 경우 필수)               |
| content                                 | Object             | N  | 메시지 내용                                               |
| content.unsubscribePhoneNumber          | String             | N  | 080 수신 거부 번호(광고 목적의 RCS Bizcenter 템플릿 발송 시 필수) |
| options                                 | Object             | N  | 발송 옵션                                                 |
| options.expiryOption                    | Integer            | N  | 디바이스로의 전송 시도에 대한 타임아웃(1: 1일, 2: 40초, 3: 3분, 4: 1시간)  |
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
            },
            "options": {
              "expiryOption": 1,
              "groupId":"groupId"
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
| recipients[].templateParameters         | Object         | N  | 수신자별 템플릿 파라미터                         |
| flow                                    | Object | N  | 플로우(필수값이 필요한 템플릿을 사용하는 플로우인 경우 필수) |
| flow.steps[]                            | Array | Y  | 플로우 단계(메시지 채널별 flow steps 스펙 참고) |

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

### 플로우 메시지 발송 요청 본문 - RCS flow step
* RCS Step 1개로만 이루어진 플로우로 발송하는 경우에 대한 flow.steps 예시입니다.

```json
{
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
| flow.steps[].sender.chatbotId           | String         | N  | 대화방 아이디(RCS Bizcenter 템플릿인 경우 필수)    |
| flow.steps[].content                    | Object         | N  | 메시지 내용                                    |
| flow.steps[].content.unsubscribePhoneNumber | String     | N  | 080 수신 거부 번호(광고 목적의 RCS Bizcenter 템플릿 발송 시 필수) |
| flow.steps[].options                    | Object         | N  | 발송 옵션                                     |
| flow.steps[].options.expiryOption       | Integer        | N  | 디바이스로의 전송 시도에 대한 타임아웃(1: 1일, 2: 40초, 3: 3분, 4: 1시간)  |
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
| instantFlow.steps[] | Array | Y | 인스턴트 플로우 단계입니다.(메시지 채널별 인스턴트 플로우 단계 스펙 참고)|

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
* RCS Step 1개로만 이루어진 인스턴트 플로우 발송시의 instantFlow.steps 예시입니다.

```json
{
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
        "nextSteps" : [ ]
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
| instantFlow.steps[].templateId | String | N | 템플릿 아이디입니다. 템플릿 아이디를 설정한 경우, 요청 시 발신자 정보(sender)와 메시지 내용(content)이 적용되지 않습니다.<br>인스턴트 플로우 메시지에서 템플릿 아이디를 설정하지 않는 경우, 발신자 정보(sender)와 메시지 내용(content)이 반드시 필요합니다.<br> |
| instantFlow.steps[].sender                     | Object         | N  | 발신자 정보(자유 양식 메시지 발송 요청 RCS 본문 예시 참고) |
| instantFlow.steps[].content                    | Object         | N  | 메시지 내용(자유 양식 메시지 발송 요청 RCS 본문 예시 참고)  |
| instantFlow.steps[].options                    | Object         | N  | 발송 옵션(자유 양식 메시지 발송 요청 RCS 본문 예시 참고)  |
| instantFlow.steps[].nextSteps[]                | Object Array   | N  | 다음 단계입니다.                                |