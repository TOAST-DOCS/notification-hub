<h1>API v1.0 사용 가이드</h1>

**Notification > Notification Hub > API v1.0 사용 가이드**

<span id="basic-information"></span>

## Notification Hub API 공통 정보

### 주의 사항
* Notification Hub v1.0 API는 현재 알파(alpha) 상태로, API는 변경될 수 있으며, 변경 시 사전 공지 없이 변경될 수 있습니다.
* 알파 버전의 API는 안정화되지 않았으며, 실험적인 기능이 추가되거나 제거될 수 있습니다.
* Notification Hub가 GA(General Availability) 상태로 전환 후 공식 버전으로 변경됩니다.
* 변경 가능한 부분은 이 문서에서 설명하는 API 엔드포인트, 인증, 요청 제한, 요청, 응답, 필드 등 모든 항목이 포함됩니다.

<span id="endpoint"></span>

### API 엔드포인트

| 리전     | 엔드포인트 |
|--------| ----- |
| Global | https://notification-hub.api.nhncloudservice.com |

* Notification Hub는 리전 구분 없이 Global 엔드포인트를 사용합니다.


<span id="authorization"></span>

### 인증 및 권한

```
X-NHN-Authorization: {accessToken}
```

* 인증 토큰을 발급 받아 Notification Hub API 호출 시 **X-NHN-Authorization** 요청 헤더에 인증 토큰을 설정합니다.

#### 인증 토큰 발급 예시

##### IntelliJ HTTP

```http
POST https://oauth.api.gov-nhncloudservice.com/oauth2/token/create
Content-Type: application/x-www-form-urlencoded
Authorization: Basic {{oauthAuthorization}}
```

##### cURL

```curl
curl -X POST "https://oauth.api.gov-nhncloudservice.com/oauth2/token/create" \
     -H "Content-Type: application/x-www-form-urlencoded" \
     -H "Authorization: Basic {{oauthAuthorization}}"
```

* **oauthAuthorization**은 **User Access Key ID**와 **Secret Access Key**를 **USER_ACCESS_KEY_ID:SECRET_ACCESS_KEY**로 합쳐 Base64 인코딩한 값입니다.
* **User Access Key ID**와 **Secret Access Key**는 로그인 후 **오른쪽 상단의 메일 주소** > **API 보안 설정**에서 생성 및 관리할 수 있습니다.
* 인증 토큰 발급에 대한 자세한 내용은 **사용자 가이드** > **NHN Cloud** > **Public API** > **API 인증** > **인증 토큰** 항목을 확인 부탁드립니다.

<span id="date-time-format"></span>

### 날짜와 시간 형식

* 날짜와 시간은 **ISO 8601 확장 형식**을 사용합니다.
    * [ISO 8601 - 날짜와 시간 표기법](https://ko.wikipedia.org/wiki/ISO_8601)
* 사용 가능한 **ISO 8601** 형식은 다음과 같습니다.
    * YYYY-MM-DDThh:mm+hh:mm
    * YYYY-MM-DDThh:mmZ
    * YYYY-MM-DDThh:mm:ss+hh:mm
    * YYYY-MM-DDThh:mm:ssZ
    * YYYY-MM-DDThh:mm:ss.sss+hh:mm
    * YYYY-MM-DDThh:mm:ss.sssZ
* **T**는 날짜와 시간을 구분하는 구분자입니다.
* **+hh:mm** 또는 **Z**는 표준 시간대 지정자(Time Zone Designator) 를 나타냅니다.
* Notification Hub API 및 기능에서 초와 밀리초 단위는 사용되지 않습니다.
* API 응답에서 날짜와 시간은 **YYYY-MM-DDThh:mm:ss.sss+09:000** 형식으로 표기합니다.

<span id="response"></span>

### 응답 공통 정보

<span id="succeed-response"></span>

#### 실패 응답 본문

성공 응답의 HTTP 상태 코드는 **200 OK**입니다.

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

<span id="failed-response"></span>

#### 실패 응답 본문

실패 응답의 HTTP 상태 코드는 **4xx**와 **5xx**입니다.

```json
{
    "header": {
        "isSuccessful": false,
        "resultCode": 400629,
        "resultMessage": "실패에 대한 정보를 담고 있습니다."
    }
}
```

| 이름 | 타입 | 설명 |
| --- | --- | --- |
| header.isSuccessful | Boolean | API 호출 성공 여부입니다. |
| header.resultCode | Number | 결과 코드입니다. 성공은 0, 실패는 400000 이상의 값을 가집니다. |
| header.resultMessage | String | 결과 메시지입니다. 실패에 대한 정보를 담고 있습니다. |

* **resultCode** 앞자리 3자리는 HTTP 상태 코드와 동일하며, 뒷자리 3자리는 상세 코드입니다.
* 결과 메시지는 결과 메시지는 언제든지 변경될 수 있습니다. 결과 메시지를 비즈니스 로직에 사용하는 것은 권장하지 않습니다.
* 결과 메시지는 **Accept-Language** 요청 헤더에 따라 한국어, 영어, 일본어로 제공됩니다..
* API 호출 시 **X-NC-ALWAYS-200-OK** 요청 헤더에 값을 **true**로 설정하면, 실패 응답에도 HTTP 상태 코드 **200 OK**로 응답합니다.

<span id="rate-limit"></span>

### 요청 수 제한
* Notification Hub에서는 특정 클라이언트가 과도한 리소스 점유를 막고 서비스의 안정성을 보장하기 위해 API 요청 수를 제한합니다.
* API 요청 수는 초당 요청 수. 300RPS(Requests Per Second)으로 제한됩니다.

#### 주의 사항
* 요청 수 계산은 클라이언트, 서버간 시간 차이, 네트워크 지연에 따라 다르게 측정되어 계산된 값이 다를 수 있습니다.
* 300RPS가 넘으면 서버는 HTTP 상태 코드 429(Too Many Requests) 응답으로 클라이언트의 요청을 거부합니다.
* 클라이언트는 요청이 거부되면 바로 재시도하는 경우, 서버의 요청 거부가 유지될 수 있습니다.
* 클라이언트는 요청이 거부되면 지수 백오프(Exponential Backoff) 처럼 재시도 간격을 늘려가며 호출하는 것을 권장합니다.

<span id="example-guide"></span>

**요청 예시**
* 본 API 가이드 문서에서 API를 호출하는 예시를 IntelliJ HTTP, cURL로 제공합니다.
* IntelliJ HTTP는 IntelliJ IDEA의 HTTP 클라이언트 플러그인으로 JetBrains IDEs 또는 명령줄에서 실행할 수 있습니다.
  * [JetBrains - IntelliJ HTTP Client](https://www.jetbrains.com/help/idea/http-client-in-product-code-editor.html)
    * IntelliJ HTTP Client 사용 방법, 문법에 대한 가이드 문서입니다.
  * [JetBrains Marketplace - IntelliJ HTP Client](https://plugins.jetbrains.com/plugin/13121-http-client)
    * IntelliJ HTTP Client 플러그인 링크입니다.
  * [JetBrains - IntelliJ HTTP Cient CLI](https://blog.jetbrains.com/idea/2022/12/http-client-cli-run-requests-and-tests-on-ci/)
    * IntelliJ가 없는 환경에서 IntelliJ HTTP(*.http) 파일을 실행시키는 CLI에 대한 소개 문서입니다.
  * [Docker - IntelliJ HTTP Cliemt Image](https://hub.docker.com/r/jetbrains/intellij-http-client)
    * IntelliJ HTTP Client 도커 이미지 링크입니다.

---

<span id="post-free-form-message"></span>

## 전문 메시지 발송 요청

요청 본문에 메시지 내용을 입력해 메시지를 발송 요청합니다.

각 메시지 채널로 메시지를 발송하기 위해서는 각 메시지 채널의 발신 정보가 등록되어야 있어야 합니다. 발신 정보 등록은 **Notification Hub 콘솔** > **발신 정보** 탭에서 진행할 수 있습니다. 메시지 채널의 발신 정보에 대한 자세한 설명은 **사용자 가이드** > **Notification Hub** > **사용 전 준비 및 제한 사항**에서 확인할 수 있습니다.

<!-- !!! tip "알아두기"-->
<!-- API를 사용할 때 사용자가 알아 두면 좋을 참고 사항이나 추가 정보를 제공할 때 사용합니다.-->

<!-- !!! warning "주의"-->
<!--API를 사용할 때 따르지 않을 경우 서비스의 비정상 또는 비효율적 동작이 발생할 수 있는 주의 사항을 표기할 때 사용합니다.-->

**요청**

```
POST /message/v1.0/{{messageChannel}}/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| messageChannel | Path | String | Y | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| messagePurpose | Path | String | Y | 메시지 목적<br>NORMAL, AD, AUTH |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |

**공통 요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

메시지 채널에 따른 요청 본문의 자세한 내용은 아래 **메시지 채널별 상세 요청 본문**을 확인 부탁드립니다.

```json
{
  "statsKeyId": "통계_아이디",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "...": "..."
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
    "...": "..."
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 이름 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- |
| statsKeyId | String | N | 통계 키 아이디 |
| scheduledDateTime | DateTime(ISO 8601) | N | 예약 발송 일시(예: 2024-10-29T06:29:00+09:00) |
| confirmBeforeSend | Boolean | N | 발송 전 확인 여부(기본값 false) |
| sender | Object | N | 발신자, 푸시 외 다른 메시지 채널은 필수 |
| recipients | Array | Y | 수신자 배열 |
| recipients[].contacts | Array | Y | 수신자의 연락처 배열 |
| recipients[].contacts[].contactType | String | Y | 연락처 유형 |
| recipients[].contacts[].contact | String | Y | 연락처 |
| content | Object | Y | 메시지 내용 |

* 메시지 채널에 따라 다른 **sender**, **content** 필드 형식을 가집니다.
* 메시지 채널에 따라 **recipients.contact.contactType**, **recipients.contact.contact** 필드에 입력할 수 있는 값이 달라집니다.
* 예약 발송의 경우 **scheduledDateTime**를 설정합니다. 발송이 시작되기 전의 예약 발송은 요청 취소가 가능합니다. 요청 취소 API를 호출하거나 **Notification Hub 콘솔** > **발송 조회**에서 취소할 수 있습니다.
* 승인 후 발송의 경우 **confirmBeforeSend**를 **true**로 설정합니다. 승인 후 발송인 메시지는 **Notification Hub 콘솔** > **발송 조회**에서 승인을 하면 발송이 진행됩니다.
* 예약 발송과 승인 후 발송은 동시에 설정할 수 없습니다.

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
| header.resultCode | Number | 결과 코드 |
| header.resultMessage | String | 결과 메시지 |
| messageId | String | 요청 성공한 메시지 아이디 |

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 전문 메시지 발송
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
````

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "https://api.example.com/message/v1.0/PUSH/free-form-messages/{messagePurpose}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}" \
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

<span id="free-form-by-message-channel"></span>

## 메시지 채널별 상세 요청 본문

<span id="free-form-by-sms"></span>

### SMS 요청 본문 예시

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
          "contact": "01012345678"
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


| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| sender | Body | Object | N | 발신자, 푸시 외 다른 메시지 채널은 필수 |
| sender.senderPhoneNumber | Body | Object | N | 발신자 번호 |
| content | Body | Object | Y | 메시지 내용 |
| content.messageType | Body | String | Y | SMS, LMS, MMS |
| content.title | Body | Object | Y | 제목 |
| content.body | Body | Object | Y | 내용 |
| content.attachmentIds | Body | Object | Y | 첨부 파일 아이디 |


<span id="free-form-by-rcs"></span>

### RCS 요청 본문 예시

```json
{
  "statsKeyId": "통계_키_아이디",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "브랜드_이이디",
    "chatbotId": "대화방_아이디"
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
    "unsubscribePhoneNumber": "08012341234",
    "title": "[NHN Cloud Notification Hub] 공지사항",
    "body": "안녕하세요. NHN Cloud Notification Hub 입니다.",
    "mmsType": "HORIZONTAL",
    "messagebaseId": "44o4SUjpqnjDuUcH+uHvPg==",
    "cards": [
        {
          "title":"testTitle",
          "description":"testBody",
          "media":"fileId",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"홈페이지로 이동\"}}"
            },
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"홈페이지로 이동\"}}"
            }
          ]
        }
    ],
    "buttons": [
        {
            "buttonType": "URL",
            "buttonJson": "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"홈페이지로 이동\"}}"
        }
    ]
  }
}
```


| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| sender | Body | Object | N | 발신자 |
| sender.brandId | Body | Object | N | 브랜드 아이디 |
| sender.chatbotId | Body | Object | N | 대화방 아이디 |
| content | Body | Object | Y | 메시지 내용 |
| content.messageType | Body | String | Y | RCS 내 메시지 유형, SMS, LMS, MMS, RCS_TEMPLATE |
| content.unsubscribePhoneNumber | Body | String | Y | 080 수신 거부 번호, 발송 목적이 광고인 경우 필수 |
| content.title | Body | Object | Y | 제목 |
| content.body | Body | Object | Y | 내용 |
| content.mmsType | Body | Object | N | MMS 타입, 메시지 유형이 MMS인 경우 필수, HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMAL |
| content.messagebaseId | Body | Object | N | 메시지 유형이 RCS_TEMPLATE인 경우 필수, RCS Biz Center에 등록된 템플릿 아이디 |
| content.cards | Body | Array | Y | 카드 |
| content.cards[].title | Body | String | Y | 제목 |
| content.cards[].description | Body | String | Y | 내용 |
| content.cards[].media | Body | String | Y | 첨부파일 ID |
| content.cards[].buttons | Body | Array<Object> | Y | 버튼 |
| content.cards[].button.buttonType | Body | String | Y | 버튼 타입<br>대화방 열기(COMPOSE), 복사하기(CLIPBOARD), 전화 걸기(DIALER), 지도 보여주기(MAP_SHOW), 지도 검색하기(MAP_QUERY), 현재 |
| content.cards[].button.buttonJson | Body | String | Y | 버튼 Json | 버튼 타입에 맞는 포맷 확인 |
| content.buttons | Body | Array<Object> | Y | 버튼 |
| content.buttons[].buttonType | Body | String | Y | 버튼 타입<br><ul><li>대화방 열기(COMPOSE)</li><li>복사하기(CLIPBOARD)</li><li>전화 걸기(DIALER)</li><li>지도 보여주기(MAP_SHOW)</li><li>지도 검색하기(MAP_QUERY)</li><li>현재 위치 공유하기(MAP_SHARE)</li><li>URL 연결하기(URL)</li><li>일정 등록하기(CALENDAR)</li><ul> |
| content.buttons[].buttonJson | Body | String | Y | 버튼 Json |
| content.attachmentIds | Body | Body | Array<String> | Y | 첨부 파일 아이디 배열 |


<span id="free-form-by-friendtalk"></span>

### 친구톡 요청 본문 예시 - 텍스트형

* 알림톡은 템플릿 등록 후 승인을 받은 상태에서 발송 가능하기 때문에 템플릿, 플로우 메시지 발송만 가능합니다.
* 알림톡의 **sender**, **content** 필드는 **템플릿 메시지 발송**의 **요청 본문**을 확인하세요.
* 친구톡(FRIENDTALK)은 NORMAL(일반) 발신프로필 유형만 사용할 수 있습니다. GROUP(그룹) 발신프로필 유형의 발신 키를 사용하면 발송에 실패합니다.

```json
{
    "statsKeyId": "통계_키_아이디",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "발신프로필_발신키"
    },
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
        "description": "쿠폰_상제_설명",
        "linkMo": "모바일_링크",
        "linkPc": "PC_링크",
        "schemeIos": "iOS_앱_링크",
        "schemeAndroid": "Android_앱_링크"
      }
    }
}
```


| 이름 | 구분 | 타입 | 필수 | 설명                                                            |
| --- | --- | --- |----|---------------------------------------------------------------|
| sender | Body | Object | Y  | 발신자                                                           |
| sender.senderKey | Body | Object | Y  | 발신프로필_발신키                                                     |
| content | Body | Object | Y  | 메시지 내용                                                        |
| content.messageType | Body | String | Y  | 메시지 유형                                                        |
| content.content | Body | String | Y  | 내용                                                            |
| content.buttons                   | Body | Array  | N  | 버튼                                                                                                                                                        |
| content.buttons[].type            | Body | String | Y  | 버튼 타입<br>WL(웹 링크), AL(앱 링크), BK(봇 키워드), MD(메시지 전달), BF(비즈니스폼)                                                                                             |
| content.buttons[].name            | Body | String | Y  | 버튼 이름                                                                                                                                                     |
| content.buttons[].linkMo          | Body | String | N  | 링크 모바일, 버튼 타입이 WL이면 필수                                                                                                                                    |
| content.buttons[].linkPc          | Body | String | N  | 링크 PC                                                                                                                                                     |
| content.buttons[].schemeIos       | Body | String | N  | iOS 앱 링크                                                                                                                                                  |
| content.buttons[].schemeAndroid   | Body | String | N  | Android 앱 링크                                                                                                                                              |
| content.buttons[].bizFormKey      | Body | String | N  | 비즈폼 키, 버튼 타입이 BF이면 필수                                                                                                                                     |
| content.coupon | Body | Object | N  | 쿠폰                                                            |
| content.coupon.title | Body | String | Y  | 제목, 경우 5가지 형식으로 제한됨<br>"${숫자}원 할인 쿠폰" 숫자는 1 이상 99,999,999 이하<br>"${숫자}% 할인 쿠폰" 숫자는 1 이상 100 이하<br>"배송비 할인 쿠폰"<br><br>"${7자 이내} 무료 쿠폰"<br>"${7자 이내} UP 쿠폰"                                                          |
| content.coupon.description | Body | String | Y  | 쿠폰 상세 설명 (일반 텍스트, 이미지형, 캐러셀 피드형 최대 12자 / 와이드 이미지형, 와이드 아이템 리스트형 최대 18자) |
| content.coupon.linkMo | Body | String | N  | 링크 모바일                                                        |
| content.coupon.linkPc | Body | String | N  | 링크 PC                                                         |
| content.coupon.schemeIos | Body | String | N  | iOS 앱 링크                                            |
| content.coupon.schemeAndroid | Body | String | N  | Android 앱 링크                         |

## * 친구톡 요청 본문 예시 - 이미지형 / 와이드 이미지형

* 친구톡(FRIENDTALK)은 NORMAL(일반) 발신프로필 유형만 사용할 수 있습니다. GROUP(그룹) 발신프로필 유형의 발신 키를 사용하면 발송에 실패합니다.

```json
{
    "statsKeyId": "통계_키_아이디",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "발신프로필_발신키"
    },
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
        "description": "쿠폰_상제_설명",
        "linkMo": "모바일_링크",
        "linkPc": "PC_링크",
        "schemeIos": "iOS_앱_링크",
        "schemeAndroid": "Android_앱_링크"
      }
    }
}
```

| 이름 | 구분   | 타입     | 필수 | 설명                                                            |
| --- |------|--------|----|---------------------------------------------------------------|
| sender | Body | Object | Y  | 발신자                                                           |
| sender.senderKey | Body | Object | Y  | 발신프로필_발신키                                                     |
| content | Body | Object | Y  | 메시지 내용                                                        |
| content.messageType | Body | String | Y  | 메시지 유형                                                        |
| content.content | Body | String | Y  | 내용                                                            |
| content.attachmentId | Body  | String  | Y  | 첨부 파일 아이디 |
| content.imageLink | Body | String | N  | 이미지 링크 |
| content.buttons                   | Body | Array  | N  | 버튼                                                                                                                                                        |
| content.buttons[].type            | Body | String | Y  | 버튼 타입<br>WL(웹 링크), AL(앱 링크), BK(봇 키워드), MD(메시지 전달), BF(비즈니스폼)                                                                                             |
| content.buttons[].name            | Body | String | Y  | 버튼 이름                                                                                                                                                     |
| content.buttons[].linkMo          | Body | String | N  | 링크 모바일, 버튼 타입이 WL이면 필수                                                                                                                                    |
| content.buttons[].linkPc          | Body | String | N  | 링크 PC                                                                                                                                                     |
| content.buttons[].schemeIos       | Body | String | N  | iOS 앱 링크                                                                                                                                                  |
| content.buttons[].schemeAndroid   | Body | String | N  | Android 앱 링크                                                                                                                                              |
| content.buttons[].bizFormKey      | Body | String | N  | 비즈폼 키, 버튼 타입이 BF이면 필수                                                                                                                                     |
| content.coupon | Body | Object | N  | 쿠폰                                                            |
| content.coupon.title | Body | String | Y  | 제목, 경우 5가지 형식으로 제한됨<br>"${숫자}원 할인 쿠폰" 숫자는 1 이상 99,999,999 이하<br>"${숫자}% 할인 쿠폰" 숫자는 1 이상 100 이하<br>"배송비 할인 쿠폰"<br><br>"${7자 이내} 무료 쿠폰"<br>"${7자 이내} UP 쿠폰"                                                          |
| content.coupon.description | Body | String | Y  | 쿠폰 상세 설명 (일반 텍스트, 이미지형, 캐러셀 피드형 최대 12자 / 와이드 이미지형, 와이드 아이템 리스트형 최대 18자) |
| content.coupon.linkMo | Body | String | N  | 링크 모바일                                                        |
| content.coupon.linkPc | Body | String | N  | 링크 PC                                                         |
| content.coupon.schemeIos | Body | String | N  | iOS 앱 링크                                            |
| content.coupon.schemeAndroid | Body | String | N  | Android 앱 링크                         |

## * 친구톡 요청 본문 예시 - 와이드 아이템리스트형

* 친구톡(FRIENDTALK)은 NORMAL(일반) 발신프로필 유형만 사용할 수 있습니다. GROUP(그룹) 발신프로필 유형의 발신 키를 사용하면 발송에 실패합니다.

```json
{
    "statsKeyId": "통계_키_아이디",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "발신프로필_발신키"
    },
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
        "description": "쿠폰_상제_설명",
        "linkMo": "모바일_링크",
        "linkPc": "PC_링크",
        "schemeIos": "iOS_앱_링크",
        "schemeAndroid": "Android_앱_링크"
      }
    }
}
```

| 이름                                | 구분   | 타입     | 필수 | 설명                                                                                                                                                        |
|-----------------------------------|------|--------|----|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| sender                            | Body | Object | Y  | 발신자                                                                                                                                                       |
| sender.senderKey                  | Body | Object | Y  | 발신프로필_발신키                                                                                                                                                 |
| content                           | Body | Object | Y  | 메시지 내용                                                                                                                                                    |
| content.messageType               | Body | String | Y  | 메시지 유형                                                                                                                                                    |
| content.buttons                   | Body | Array  | N  | 버튼                                                                                                                                                        |
| content.buttons[].type            | Body | String | Y  | 버튼 타입<br>WL(웹 링크), AL(앱 링크), BK(봇 키워드), MD(메시지 전달), BF(비즈니스폼)                                                                                             |
| content.buttons[].name            | Body | String | Y  | 버튼 이름                                                                                                                                                     |
| content.buttons[].linkMo          | Body | String | N  | 링크 모바일, 버튼 타입이 WL이면 필수                                                                                                                                    |
| content.buttons[].linkPc          | Body | String | N  | 링크 PC                                                                                                                                                     |
| content.buttons[].schemeIos       | Body | String | N  | iOS 앱 링크                                                                                                                                                  |
| content.buttons[].schemeAndroid   | Body | String | N  | Android 앱 링크                                                                                                                                              |
| content.buttons[].bizFormKey      | Body | String | N  | 비즈폼 키, 버튼 타입이 BF이면 필수                                                                                                                                     |
| content.header                    | Body | String | Y  | 헤더                                                                                                                                                        |
| content.item                      | Body | Object | Y  | 와이드 아이템                                                                                                                                                   |
| content.item.list                 | Body | Array  | Y  | 와이드 아이템 리스트(최소 3개, 최대 4개)                                                                                                                                 |
| content.item.list[].title         | Body | String | Y  | 아이템 제목(첫 번째 아이템의 경우 최대 25자, 2~4번째 아이템의 경우 최대 30자)                                                                                                         |
| content.item.list[].attachmentId  | Body | String | Y  | 첨부 파일 아이디                                                                                                                                                 |
| content.item.list[].linkMo        | Body | String | Y  | 모바일 웹 링크                                                                                                                                                  |
| content.item.list[].linkPc        | Body | String | Y  | PC 웹 링크                                                                                                                                                   |
| content.item.list[].schemeIos     | Body | String | Y  | IOS 앱 링크                                                                                                                                                  |
| content.item.list[].schemeAndroid | Body | String | Y  | 안드로이 앱 링크                                                                                                                                                 |
| content.coupon                    | Body | Object | N  | 쿠폰                                                                                                                                                        |
| content.coupon.title              | Body | String | Y  | 제목, 경우 5가지 형식으로 제한됨<br>"${숫자}원 할인 쿠폰" 숫자는 1 이상 99,999,999 이하<br>"${숫자}% 할인 쿠폰" 숫자는 1 이상 100 이하<br>"배송비 할인 쿠폰"<br><br>"${7자 이내} 무료 쿠폰"<br>"${7자 이내} UP 쿠폰" |
| content.coupon.description        | Body | String | Y  | 쿠폰 상세 설명 (일반 텍스트, 이미지형, 캐러셀 피드형 최대 12자 / 와이드 이미지형, 와이드 아이템 리스트형 최대 18자)                                                                                   |
| content.coupon.linkMo             | Body | String | N  | 링크 모바일                                                                                                                                                    |
| content.coupon.linkPc             | Body | String | N  | 링크 PC                                                                                                                                                     |
| content.coupon.schemeIos          | Body | String | N  | iOS 앱 링크                                                                                                                                                  |
| content.coupon.schemeAndroid      | Body | String | N  | Android 앱 링크                                                                                                                                              |

## * 친구톡 요청 본문 예시 - 캐러셀 피드형

* 친구톡(FRIENDTALK)은 NORMAL(일반) 발신프로필 유형만 사용할 수 있습니다. GROUP(그룹) 발신프로필 유형의 발신 키를 사용하면 발송에 실패합니다.

```json
{
    "statsKeyId": "통계_키_아이디",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "발신프로필_발신키"
    },
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
                "description": "쿠폰_상제_설명",
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
                "description": "쿠폰_상제_설명",
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

| 이름                                                         | 구분   | 타입     | 필수 | 설명                                                                                                                                                       |
|------------------------------------------------------------|------|--------|----|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| sender                                                     | Body | Object | Y  | 발신자                                                                                                                                                      |
| sender.senderKey                                           | Body | Object | Y  | 발신프로필_발신키                                                                                                                                                |
| content                                                    | Body | Object | Y  | 메시지 내용                                                                                                                                                   |
| content.messageType                                        | Body | String | Y  | 메시지 유형                                                                                                                                                   |
| content.carousel                                           | Body | Object | Y  | 캐러셀                                                                                                                                                      |
| content.carousel.list                                      | Body | Array  | Y  | 캐러셀 리스트(최소 2개, 최대 10개)                                                                                                                                   |
| content.carousel.list[].header                             | Body | String | Y  | 캐러셀 아이템 제목(최대 20자), 캐러셀 피드형에서만 사용 가능                                                                                                                     |
| content.carousel.list[].message                            | Body | String | Y  | 캐러셀 아이템 메시지(최대 180자), 캐러셀 피드형에서만 사용 가능                                                                                                                   |
| content.carousel.list[].attachment                         | Body | Object | N  | 캐러셀 아이템 이미지, 버튼 정보                                                                                                                                       |
| content.carousel.list[].attachment.buttons                 | Body | Array  | N  | 버튼 리스트 (최대 2개)                                                                                                                                           |
| content.carousel.list[].attachment.buttons[].type          | Body | String | Y  | 버튼 타입<br>WL(웹 링크), AL(앱 링크), BK(봇 키워드), MD(메시지 전달), BF(비즈니스폼)                                                                                            |
| content.carousel.list[].attachment.buttons[].name          | Body | String | Y  | 버튼 이름                                                                                                                                                    |
| content.carousel.list[].attachment.buttons[].linkMo        | Body | String | N  | 링크 모바일, 버튼 타입이 WL이면 필수                                                                                                                                   |
| content.carousel.list[].attachment.buttons[].linkPc        | Body | String | N  | 링크 PC                                                                                                                                                    |
| content.carousel.list[].attachment.buttons[].schemeIos     | Body | String | N  | iOS 앱 링크                                                                                                                                                 |
| content.carousel.list[].attachment.buttons[].schemeAndroid | Body | String | N  | Android 앱 링크                                                                                                                                             |
| content.carousel.list[].attachment.image                   | Body | Object | Y  | 캐러셀 이미지                                                                                                                                                  |
| content.carousel.list[].attachment.image.attachmentId      | Body | String | Y  | 첨부 파일 id                                                                                                                                                 |
| content.carousel.list[].attachment.image.imageLink         | Body | String | N  | 이미지 링크 URL                                                                                                                                               |
| content.carousel.list[].attachment.coupon                  | Body | Object | N  | 쿠폰                                                                                                                                                       |
| content.carousel.list[].attachment.coupon.title            | Body | String | Y  | 제목, 경우 5가지 형식으로 제한됨<br>"${숫자}원 할인 쿠폰" 숫자는 1 이상 99,999,999 이하<br>"${숫자}% 할인 쿠폰" 숫자는 1 이상 100 이하<br>"배송비 할인 쿠폰"<br><br>"${7자 이내} 무료 쿠폰"<br>"${7자 이내} UP 쿠폰" |
| content.carousel.list[].attachment.coupon.description      | Body | String | Y  | 쿠폰 상세 설명 (일반 텍스트, 이미지형, 캐러셀 피드형 최대 12자 / 와이드 이미지형, 와이드 아이템 리스트형 최대 18자)                                                                                  |
| content.carousel.list[].attachment.coupon.linkMo           | Body | String | N  | 링크 모바일                                                                                                                                                   |
| content.carousel.list[].attachment.coupon.linkPc           | Body | String | N  | 링크 PC                                                                                                                                                    |
| content.carousel.list[].attachment.coupon.schemeIos        | Body | String | N  | iOS 앱 링크                                                                                                                                                 |
| content.carousel.list[].attachment.coupon.schemeAndroid    | Body | String | N  | Android 앱 링크                                                                                                                                             |
| content.carousel.tail                                      | Body | Object | N  | 캐러셀 더보기 버튼 정보                                                                                                                                           |
| content.carousel.tail.linkMo                               | Body | String | Y  | 모바일 웹 링크                                                                                                                                           |
| content.carousel.tail.linkPc                               | Body | String | N  | 모바일 웹 링크                                                                                                                                           |
| content.carousel.tail.schemeIos                            | Body | String | N  | 모바일 웹 링크                                                                                                                                           |
| content.carousel.tail.schemeAndroid                        | Body | String | N  | 모바일 웹 링크                                                                                                                                           |

<span id="free-form-by-email"></span>

### Email 요청 본문 예시

```json
{
  "sender": {
    "senderMailAddress": "sender@example.com"
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
    "title": "[NHN Cloud Notification Hub] 공지사항",
    "body": "안녕하세요. NHN Cloud Notification Hub 입니다.",
    "attachmentIds": [
      "첨부_파일_아이디"
    ]
  }
}
```

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| sender | Body | Object | N | 발신자, 푸시 외 다른 메시지 채널은 필수 |
| sender.senderMailAddress | Body | Object | N | 발신자 이메일 주소 |
| content | Body | Object | Y | 메시지 내용 |
| content.title | Body | Object | Y | 제목 |
| content.body | Body | Object | Y | 내용 |
| content.attachmentIds | Body | Object | Y | 첨부 파일 아이디 |

* 발신자 이메일 주소의 도메인은 소유 인증이 완료되어야 합니다.
* 첨부 파일은 **최대 10개**까지 업로드 가능하며, **30MB 이하의 파일**만 가능합니다.
* 첨부 파일의 **총합은 30MB**를 넘어갈 수 없습니다.
* 최대 **30MB**까지 첨부 가능하지만 수신하는 이메일 시스템(gmail.com, naver.com 등)의 첨부 파일 제한 정책에 따라 **제한 초과**로 거부되거나 스팸 판정률이 높아질 수 있으므로 **10MB 이내로 첨부**할 것을 권장합니다.

<span id="free-form-by-push"></span>

### 푸시 요청 본문 예시

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

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| content | Body | Object | Y | 메시지 내용 |
| content.unsubscribePhoneNumber | Body | String | 푸시 메시지 수신 거부를 위한 대표 번호 |
| content.unsubscribeGuide | Body | String | 푸시 메시지 수신 거부를 위한 안내 |
| content.title | Body | String | Y | 제목 |
| content.body | Body | String | Y | 내용 |
| content.style.useHtmlStyle | Body | Boolean | Y | HTML 스타일 사용(Android에서만 가능) |
| content.richMessage | Body | Object| 리치 메시지 |
| content.richMessage | Body | Optional, Object | N | 리치 메시지 사용시 필요 |
| content.richMessage.buttons | Body | Optional, Object Array | N |  리치 메시지에 추가되는 버튼, 최대 3개까지 가능 |
| content.richMessage.button.name | Body | Required, String | 버튼 이름 |
| content.richMessage.button.buttonType | Body | Required, String | 버튼 타입, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS |
| content.richMessage.button.link | Body | Required, String | 버튼을 눌렀을때, 연결되는 링크 |
| content.richMessage.button.hint | Body | Required, String | 버튼에대한 힌트 |
| content.richMessage.media | Body | Optional, Object | N |  리치 메시지에 추가되는 미디어 |
| content.richMessage.media.source | Body | Required, String | 미디어의 위치한 곳의 주소, URL, LOCAL_RESOURCE 가능 |
| content.richMessage.media.mediaType | Body | Optional, String | N |  미디어의 타입, IMAGE, GIF, VEDIO, AUDIO. Android에서는 IMAGE만 지원 |
| content.richMessage.media.expandable | Body | Required, Boolean | N | Android에서 미디어를 클릭 시 펼침 기능 사용 여부 |
| content.richMessage.androidMedia | Body | Optional, Object | N |  Android 기기에 사용되는 미디어. 형식은 media와 동일 |
| content.richMessage.iosMedia | Body | Optional, Object | N |  iOS 기기에 사용되는 미디어. 형식은 media와 동일 |
| content.richMessage.largeIcon | Body | Optional, Object | N |  리치 메시지에 추가되는 큰 아이콘, Android에서만 지원 |
| content.richMessage.largeIcon.source | Body | Required, String | Y | 미디어의 위치한 곳의 주소 |
| content.richMessage.group | Body | Optional, Object | N |  여러 개의 메시지를 그룹 단위로 묶는 기능, Android에서만 지원 |
| content.richMessage.group.key | Body | String | Y |  그룹의 키 |
| content.richMessage.group.description | Body | String | Y |  그룹에대한 설명 |
| content.customKey | Body | Object, Array, String | N | 사용자 정의 키와 값 |

* 푸시는 **sender** 필드가 필요 없습니다.
* 푸시는 사용자가 정의한 키와 값을 추가해 **content** 필드를 작성할 수 있습니다.


<span id="post-template-message"></span>

### 템플릿 메시지 발송 요청

**요청**

```
POST /message/v1.0/{{messageChannel}}/template-messages/{messagePurpose}
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
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
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 이름 | 구분 | 타입             | 필수 | 설명 |
| --- | --- |----------------| --- | --- |
| statsKeyId | Body | String         | N | 통계 키 아이디 |
| scheduledDateTime | Body | DateTime(ISO 8601) | N | 예약 발송 일시(예: 2024-10-29T06:29:00+09:00) |
| confirmBeforeSend | Body | Boolean        | N | 발송 전 확인 여부(기본값 false) |
| templateId | Body | String         | Y | 템플릿 아이디 |
| templateParameters | Body | Object         | N | 템플릿 파라미터 |
| recipients | Body | Array          | Y | 수신자 배열 |
| recipients[].contacts | Body | Array          | Y | 수신자의 연락처 배열 |
| recipients[].contacts[].contactType | Body | String         | Y | 연락처 유형 |
| recipients[].contacts[].contact | Body | String         | Y | 연락처 |
| recipients[].templateParameters | Body | Object         | N | 템플릿 파라미터 |

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
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "{endpoint}/message/v1.0/SMS/template-messages/NORMAL" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}" \
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

<span id="post-flow-message"></span>

### 플로우 메시지 발송 요청

**요청**

```
POST /message/v1.0/flow-messages/{messagePurpose}
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| messagePurpose | Path | String | Y | 메시지 목적<br>NORMAL, AD, AUTH |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |

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
          "contact": "01012345679"
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

<!--요청 본문의 필드를 설명합니다.-->

| 이름                 | 구분 | 타입             | 필수 | 설명                                     |
|--------------------| --- |----------------| --- |----------------------------------------|
| statsKeyId         | Body | String         | N | 통계 키 아이디                               |
| scheduledDateTime  | Body | DateTime(ISO 8601) | N | 예약 발송 일시(예: 2024-10-29T06:29:00+09:00) |
| confirmBeforeSend  | Body | Boolean        | N | 발송 전 확인 여부(기본값 false)                  |
| flowId             | Body | String         | Y | 템플릿 아이디                                |
| templateParameters | Body | Object         | N | 메시지 공통 템플릿 파라미터                        |
| recipients         | Body | Array          | Y | 수신자 배열                                 |
| recipients[].contacts | Body | Array          | Y | 수신자의 연락처 배열                            |
| recipients[].contacts[].contactType | Body | String         | Y | 연락처 유형                                 |
| recipients[].contacts[].contact | Body | String         | Y | 연락처                                    |
| recipients[].templateParameters | Body | Object         | N | 수신자 별 템플릿 파라미터                         |

* 플로우 메시지 발송도 템플릿 메시지 발송과 동일하게 템플릿 파라미터를 사용합니다.
* 수신자의 연락처는 플로우에서 사용하는 메시지 채널에 필요한 연락처가 모두 포함되어야 합니다.


<span id="get-contact-delivery-results"></span>

### 연락처별 수신 결과 목록 조회

발송 요청된 메시지의 발송과 수신 결과를 수신자의 연락처 단위로 조회합니다.

예를 들어, 이메일과 전화번호를 가진 수신자 10명에게 이메일, SMS 템플릿으로 구성된 플로우 메시지 2개를 발송하는 경우, 연락처 별 수신 결과 목록을 조회하면 40개의 항목이 조회됩니다. (연락처 2개 X 수신자 10명 X 플로우 메시지 2개 = 연락처 별 수신 결과 40개)
다양한 검색 조건으로 연락처 별 수신 결과를 조회할 수 있습니다.

<!-- !!! tip "알아두기"-->
<!-- API를 사용할 때 사용자가 알아 두면 좋을 참고 사항이나 추가 정보를 제공할 때 사용합니다.-->

<!-- !!! warning "주의"-->
<!--API를 사용할 때 따르지 않을 경우 서비스의 비정상 또는 비효율적 동작이 발생할 수 있는 주의 사항을 표기할 때 사용합니다.-->

**요청**

```
GET /message/v1.0/contact-delivery-results
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| messageId | Query | String | Y | 메시지 아이디 |
| templateId | Query | String | N | 템플릿 아이디 |
| flowId | Query | String | N | 플로우 아이디 |
| statsKeyId | Query | String | N | 통계 키 아이디 |
| sender | Query | String | N | 발신자 |
| contact | Query | String | N | 연락처 |
| messageChannel | Query | String | N | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| messagePurpose | Query | String | N | 메시지 목적 |
| status | Query | String | N | 상태 |
| scheduled | Query | Boolean | N | 예약 발송 여부 |
| confirmBeforeSend | Query | Boolean | N | 발송 전 확인 여부 |
| createdDateTime | Query | DateTime(ISO 8601) | N | 생성 일시 |
| limit | Query | Number | N | 조회 개수 |
| offset | Query | Number | N | 조회 시작 위치 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다

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
| header.resultCode | Number | 결과 코드 |
| header.resultMessage | String | 결과 메시지 |
| contactDeliveryResults | Array<Object> | 연락처 별 수신 결과 목록 |
| contactDeliveryResults.messageId | String| 메시지의 아이디 |
| contactDeliveryResults.recipientIndex | Number| 수신자 인덱스|
| contactDeliveryResults.contactIndex | Number| 연락처 인덱스|
| contactDeliveryResults.contactType | String| 연락처 타입 |
| contactDeliveryResults.contact | String| 연락처|
| contactDeliveryResults.sender | Object| 발신자|
| contactDeliveryResults.sender.senderKey | String| 발신프로필 발신키, 알림톡과 친구톡만 표시|
| contactDeliveryResults.sender.senderProfileId | String| 발신 프로필 아이디, 알림톡과 친구톡만 표시 |
| contactDeliveryResults.sender.senderProfileType | String| 발신 프로필 타입, 알림톡과 친구톡만 표시|
| contactDeliveryResults.sender.senderPhoneNumber | String| 발신자 전화번호, SMS만 표시|
| contactDeliveryResults.sender.senderMailAddress | String| 발신자 이메일 주소, 이메일만 표시|
| contactDeliveryResults.sender.brandId | String| 브랜드 아이디, RCS만 표시 |
| contactDeliveryResults.sender.chatbotId | String| 대화방 아이디, RCS만 표시 |
| contactDeliveryResults.templateId | String| 템플릿의 아이디, 템플릿 메시지만 표시|
| contactDeliveryResults.flowId | String| 플로우의 아이디, 템플릿 메시지만 표시|
| contactDeliveryResults.statsKeyId | String| 통계 키의 아이디|
| contactDeliveryResults.messageChannel | String| 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| contactDeliveryResults.messagePurpose | String| 메시지 목적 |
| contactDeliveryResults.confirmBeforeSend | Boolean | 승인 후 발송 사용 여부|
| contactDeliveryResults.confirmedDateTime | DateTime(ISO 86091) | 승인 일시(예: 2024-10-29T06:09:00+09:00)|
| contactDeliveryResults.scheduled | Boolean | 예약 발송 여부 |
| contactDeliveryResults.scheduledDateTime | DateTime(ISO 86091) | 예약 발송 일시 |
| contactDeliveryResults.status | String| 상태 |
| contactDeliveryResults.resultCode | String| 결과 코드|
| contactDeliveryResults.resultMessage | String| 결과 메시지 |
| contactDeliveryResults.templateParameters | Object| 템플릿 파라미터 |
| contactDeliveryResults.additionalProperty | Object| 추가 속성, 알림톡, RCS만 제공|
| contactDeliveryResults.createdDateTime | DateTime(ISO 86091) | 생성 일시(예: 2024-10-29T06:09:00+09:00)|
| contactDeliveryResults.sentDateTime | DateTime(ISO 86091) | 발송 일시, 발송 이벤트가 수집되기 전까지 값은 null|
| contactDeliveryResults.deliveredDateTime | DateTime(ISO 86091) | 수신 일시, 수신 이벤트가 수집되기 전까지 값은 null|
| contactDeliveryResults.openedDateTime | DateTime(ISO 86091) | 열람 일시, 열람 이벤트가 수집되기 전까지 값은 null, 푸시와 이메일만 제공 |
| contactDeliveryResults.updatedDateTime | DateTime(ISO 86091) | 마지막 업데이트 일시|
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
curl -X GET "{endpoint}/message/v1.0/contact-delivery-results" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}"
```

</details>



<span id="post-message-do-cancel"></span>

### 메시지 요청 취소

발송 전 예약 메시지, 승인 후 발송 메시지의 발송 요청을 취소합니다. 요청 취소된 메시지는 연락처별 수신 결과 조회에서 조회할 수 있습니다.

**요청**

```
POST /message/v1.0/messages/{messageId}/do-cancel
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
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

---

## 템플릿

<span id="post-template"></span>

### 템플릿 생성

**요청**

```
POST /template/v1.0/{messageChannel}/templates
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
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

#### sender 필드

| 메시지 채널 | 필드 | 비고 |
| --- | --- | --- |
| SMS | sender.senderPhoneNumber | 발신자 번호 |
| RCS | sender.brandId | 브랜드 아이디 |
| RCS | sender.chatbotId | 대화방 아이디 |
| EMAIL | sender.senderMailAddress | 발신자 이메일 주소 |
| ALIMTALK, FRIENDTALK | sender.senderKey | 발신키 |
| ALIMTALK | sender.senderProfileType | 발신프로필 유형<br>GROUP, NORMAL |

* 알림톡(ALIMTALK)은 발신 키(senderKey)와 발신프로필 유형(senderProfileType)을 필수로 입력해야 합니다.
* 친구톡(FRIENDTALK)은 NORMAL(일반) 발신프로필 유형만 사용할 수 있습니다. GROUP(그룹) 발신프로필 유형의 발신 키를 사용하면 발송에 실패합니다.
* 발신자 프로필 유형은 **GROUP(그룹)**과 **NORMAL(일반)**이 있습니다. **GROUP**은 그룹 발신자 프로필, **NORMAL**은 일반 발신자 프로필입니다.

### 알림톡 템플릿 요청 본문

* 알림톡은 발송을 위해서 템플릿 등록이 필수 입니다.
* 알림톡 템플릿을 등록하면 카카오비즈니스의 검수와 승인 과정을 거치고 승인 완료 후에 사용할 수 있습니다.
* 알림톡 템플릿은 검수와 승인 과정에서 카카오비즈니스 검수 담당자와 문의를 주고 받을 수 있습니다.
  * [카카오톡채널 관리자센터](https://center-pf.kakao.com)
  * 알림톡 템플릿은 **문의하기**, **파일 첨부 문의하기**, **템플릿 수정 내역 조회** API를 추가로 제공합니다.

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
curl -X POST "{endpoint}/template/v1.0/{messageChannel}/templates" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}" \
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
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
```

**요청 파라미터**

| 이름           | 구분 | 타입 | 필수 | 설명                        |
|--------------| --- | --- | --- |---------------------------|
| appKey       | Header | String | Y | 앱키                        |
| accessToken  | Header | String | Y | 인증 토큰                     |
| templateName | Query | String | N | 템플릿 이름, 접두사(Prefix) 검색 가능 |
| limit        | Query | Number | N | 조회 개수(기본값: 20)            |
| offset       | Query | Number | N | 조회 시작 위치(기본값: 0)          |

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
curl -X GET "{endpoint}/template/v1.0/{messageChannel}/templates" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}"
```

</details>

<span id="get-template"></span>

### 템플릿 조회

**요청**

```
GET /template/v1.0/{messageChannel}/templates/{templateId}
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
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
curl -X GET "{endpoint}/template/v1.0/{messageChannel}/templates/{templateId}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}"
```

</details>

<span id="put-template"></span>

### 템플릿 수정

**요청**

```
PUT /template/v1.0/{messageChannel}/templates/{templateId}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
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
curl -X PUT "{endpoint}/template/v1.0/{messageChannel}/templates/{templateId}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}" \
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
curl -X DELETE "{endpoint}/template/v1.0/{messageChannel}/templates/{templateId}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}"
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
curl -X POST "{endpoint}/template/v1.0/ALIMTALK/templates/{templateId}/inquiries" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}" \
     -d '{
        "comment": "문의 내용"
      }'
```

</details>

### 알림톡 템플릿 파일 첨부 문의하기

**요청**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/inquiries/do-with-file
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
curl -X POST "{endpoint}/template/v1.0/ALIMTALK/templates/{templateId}/inquiries/do-with-file?fileName=attachment.xlsx" \
     -H "Content-Type: multipart/form-data" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}" \
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

| 이름 | 타입 | 필수 | 설명                |
| --- | --- | --- |-------------------|
| templateCode         | String  | 필수      | 템플릿 코드(최대 20자) |
| templateName         | String  | 필수      | 템플릿명(최대 150자) |
| templateContent      | String  | 필수      | 템플릿 본문(최대 1000자) |
| templateMessageType  | String  | 선택      | 템플릿 메시지 유형<br>BA: 기본형, EX: 부가 정보형, AD: 채널 추가형, MI: 복합형 (기본값: BA) |
| templateEmphasizeType| String  | 선택      | 템플릿 강조 표시 타입<br>NONE: 기본, TEXT: 강조 표시, IMAGE: 이미지형, ITEM_LIST: 아이템리스트형 (기본값: NONE)<br>- TEXT 선택 시: templateTitle, templateSubtitle 필수<br>- IMAGE 선택 시: templateImageName, templateImageUrl 필수<br>- ITEM_LIST 선택 시: 이미지, 헤더, 아이템 하이라이트, 아이템 리스트 중 1개 이상 필수 |
| templateExtra        | String  | 조건부 필수 | 템플릿 부가 정보<br>템플릿 메시지 유형이 부가 정보형 또는 복합형일 경우 필수 |
| templateTitle        | String  | 선택      | 템플릿 제목(최대 50자)<br>Android: 2줄, 23자 이상일 때 말줄임 처리<br>iOS: 2줄, 27자 이상일 때 말줄임 처리 |
| templateSubtitle     | String  | 선택      | 템플릿 보조 문구(최대 50자)<br>Android: 18자 이상일 때 말줄임 처리<br>iOS: 21자 이상일 때 말줄임 처리 |
| templateHeader       | String  | 선택      | 템플릿 헤더(최대 16자) |
| templateItem         | Object  | 선택      | 아이템 |
| templateItem.list    | Array    | 선택      | 아이템 리스트(최소 2개, 최대 10개) |
| templateItem.list.title | String | 선택   | 타이틀(최대 6자) |
| templateItem.list.description | String | 선택 | 디스크립션(최대 23자) |
| templateItem.summary | Object  | 선택      | 아이템 요약 정보 |
| templateItem.summary.title | String | 선택 | 타이틀(최대 6자) |
| templateItem.summary.description | String | 선택 | 디스크립션(변수 및 화폐 단위, 숫자, 쉼표, 마침표만 사용 가능, 최대 14자) |
| templateItemHighlight | Object | 선택      | 아이템 하이라이트 |
| templateItemHighlight.title | String | 선택 | 타이틀(최대 30자, 섬네일 이미지가 있을 경우 21자) |
| templateItemHighlight.description | String | 선택 | 디스크립션(최대 19자, 섬네일 이미지가 있을 경우 13자) |
| templateItemHighlight.imageUrl | String | 선택 | 섬네일 이미지 주소 |
| templateRepresentLink | Object | 선택     | 대표 링크 |
| templateRepresentLink.linkMo | String | 선택 | 모바일 웹 링크(최대 500자) |
| templateRepresentLink.linkPc | String | 선택 | PC 웹 링크(최대 500자) |
| templateRepresentLink.schemeIos | String | 선택 | iOS 앱 링크(최대 500자) |
| templateRepresentLink.schemeAndroid | String | 선택 | 안드로이드 앱 링크(최대 500자) |
| templateImageName   | String  | 선택      | 이미지명(업로드한 파일명) |
| templateImageUrl    | String  | 선택      | 이미지 URL |
| securityFlag        | Boolean | 선택      | 보안 템플릿 여부<br>OTP 등 보안 메시지일 경우 설정<br>발신 당시 메인 디바이스 외 다른 디바이스에 메시지 텍스트 미노출 (기본값: false) |
| categoryCode        | String  | 선택      | 템플릿 카테고리 코드 (템플릿 카테고리 조회 API 참고, 기본값: 999999)<br>카테고리 기타일 경우 최하위 우선순위로 심사 |
| buttons             | Array    | 선택      | 버튼 리스트(최대 5개) |
| buttons.ordering    | Integer | 선택      | 버튼 순서(1~5) |
| buttons.type        | String  | 선택      | 버튼 타입<br>WL: 웹 링크, AL: 앱 링크, DS: 배송 조회, BK: 봇 키워드, MD: 메시지 전달, BC: 상담톡 전환, BT: 봇 전환, AC: 채널 추가, BF: 비즈니스폼, P1: 이미지 보안 전송 플러그인 ID, P2: 개인정보이용 플러그인 ID, P3: 원클릭 결제 플러그인 ID |
| buttons.name        | String  | 조건부 필수 | 버튼 이름 (버튼이 있는 경우 필수, 최대 14자) |
| buttons.linkMo      | String  | 조건부 필수 | 모바일 웹 링크 (WL 타입일 경우 필수 필드, 최대 500자) |
| buttons.linkPc      | String  | 선택      | PC 웹 링크 (WL 타입일 경우 선택 필드, 최대 500자) |
| buttons.schemeIos   | String  | 조건부 필수 | iOS 앱 링크 (AL 타입일 경우 필수 필드, 최대 500자) |
| buttons.schemeAndroid | String | 조건부 필수 | 안드로이드 앱 링크 (AL 타입일 경우 필수 필드, 최대 500자) |
| buttons.bizFormId   | Integer | 조건부 필수 | 비즈니스폼 ID (BF 타입일 경우 필수) |
| buttons.pluginId    | String  | 선택      | 플러그인 ID (최대 24자) |
| quickReplies        | Array    | 선택      | 바로연결 리스트 (최대 5개) |
| quickReplies.ordering | Integer | 조건부 필수 | 바로연결 순서 (바로연결이 있는 경우 필수) |
| quickReplies.type   | String  | 선택      | 바로연결 타입<br>WL: 웹 링크, AL: 앱 링크, BK: 봇 키워드, BC: 상담톡 전환, BT: 봇 전환, BF: 비즈니스폼 |
| quickReplies.name   | String  | 조건부 필수 | 바로연결 이름 (바로연결이 있는 경우 필수, 최대 14자) |
| quickReplies.linkMo | String  | 조건부 필수 | 모바일 웹 링크 (WL 타입일 경우 필수 필드, 최대 500자) |
| quickReplies.linkPc | String  | 선택      | PC 웹 링크 (WL 타입일 경우 선택 필드, 최대 500자) |
| quickReplies.schemeIos | String | 조건부 필수 | iOS 앱 링크 (AL 타입일 경우 필수 필드, 최대 500자) |
| quickReplies.schemeAndroid | String | 조건부 필수 | 안드로이드 앱 링크 (AL 타입일 경우 필수 필드, 최대 500자) |
| quickReplies.bizFormId | Integer | 조건부 필수 | 비즈니스폼 ID (BF 타입일 경우 필수) |

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
curl -X GET "{endpoint}/template/v1.0/ALIMTALK/templates/{templateId}/modifications" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}"
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
curl -X POST "{endpoint}/template/v1.0/{messageChannel}/categories" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}"
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
curl -X GET "{endpoint}/template/v1.0/{messageChannel}/categories" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}"
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

| 이름                      | 타입            | 필수 | 설명                |
|-------------------------|---------------| --- |-------------------|
| categories.[]categoryId | String        | 필수 | 카테고리 아이디 |
| categories.[]categoryName            | String        | 필수 | 카테고리 이름 |
| categories.[]parentCategoryId        | String        | 선택 | 상위 카테고리 아이디 |
| categories.[]messageChannel          | String        | 필수 | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| categories.[]categories              | Array<Object> | 선택 | 하위 카테고리 목록 |
| categories.[]templates               | Array<Object>         | 선택 | 템플릿 목록 |
| categories.[]templates.[]templateId  | String        | 필수 | 템플릿 아이디 |
| categories.[]templates.[]templateName| String        | 필수 | 템플릿 이름 |

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
curl -X GET "{endpoint}/template/v1.0/{messageChannel}/category-tree" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}"
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
curl -X GET "{endpoint}/template/v1.0/{messageChannel}/categories/{categoryId}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}"
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
curl -X PUT "{endpoint}/template/v1.0/{messageChannel}/categories/{categoryId}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}" \
     -d '{
         "parentCategoryId": "상위_카테고리_아이디",
         "name": "카테고리_이름"
     }'
```

</details>

### 템플릿 카테고리에 템플릿 추가

**요청**

```
POST /template/v1.0/{messageChannel}/categories/{categoryId}/templates
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
curl -X POST "{endpoint}/template/v1.0/{messageChannel}/categories/{categoryId}/templates" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}" \
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
curl -X DELETE "{endpoint}/template/v1.0/{messageChannel}/categories/{categoryId}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}"
```

</details>

---

## 플로우

<span id="post-flow"></span>

### 플로우 생성

**요청**

```
POST /flow/v1.0/flows
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |

**요청 본문**

```json
{
  "flowName": "플로우_이름",
  "description": "플로우_설명",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "이메일_템플릿_아이디",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "알림톡_템플릿_아이디",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_템플릿_아이디",
            "nextSteps": []
          }
        ]
      }
    ]
  }
}
```

* 위 예시는 이메일, 알림톡, SMS 템플릿을 사용하는 플로우를 생성하는 예시입니다.
* 한번 사용된 메시지 채널은 다음 단계에서 사용할 수 없습니다.
* 한 단계는 여러 개의 다음 단계를 가질 수 있습니다.
* 순서 없이 동시 발송을 원하는 겨우 첫 번째 단계인 **steps**에 모든 메시지 채널을 추가합니다.

**응답 본문**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "flowId": "플로우_아이디"
}
```

<!--응답 본문의 필드를 설명합니다.-->

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 생성
POST {{endpoint}}/flow/v1.0/flows
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "flowName": "플로우_이름",
  "description": "플로우_설명",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "이메일_템플릿_아이디",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "알림톡_템플릿_아이디",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_템플릿_아이디",
            "nextSteps": []
          }
        ]
      }
    ]
  }
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "{endpoint}/flow/v1.0/flows" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}" \
     -d '{
      "flowName": "플로우_이름",
      "description": "플로우_설명",
      "messagePurpose": "NORMAL",
      "steps": {
        "messageChannel": "EMAIL",
        "templateId": "이메일_템플릿_아이디",
        "nextSteps": [
          {
            "messageChannel": "ALIMTALK",
            "templateId": "알림톡_템플릿_아이디",
            "nextSteps": [
              {
                "messageChannel": "SMS",
                "templateId": "SMS_템플릿_아이디",
                "nextSteps": []
              }
            ]
          }
        ]
      }'
```

</details>

<span id="get-flows"></span>

### 플로우 목록 조회

**요청**

```
GET /flow/v1.0/flows
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명         |
| --- | --- | --- | --- |------------|
| appKey | Header | String | Y | 앱키         |
| accessToken | Header | String | Y | 인증 토큰      |
| flowId | Query | String | N | 플로우 아이디    |
| flowName | Query | String | N | 플로우 이름, 접두사(Prefix) 검색 가능 |
| limit | Query | Integer | N | 페이지당 조회 개수 |
| offset | Query | Integer | N | 페이지 오프셋    |

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
  "flows": [
    {
      "flowId": "플로우_아이디",
      "flowName": "플로우_이름",
      "description": "플로우_설명",
      "messagePurpose": "NORMAL",
      "steps": [
        {
          "messageChannel": "EMAIL",
          "templateId": "이메일_템플릿_아이디",
          "nextSteps": [
            {
              "messageChannel": "ALIMTALK",
              "templateId": "알림톡_템플릿_아이디",
              "nextSteps": [
                {
                  "messageChannel": "SMS",
                  "templateId": "SMS_템플릿_아이디",
                  "nextSteps": []
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 목록 조회
GET {{endpoint}}/flow/v1.0/flows
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "{endpoint}/flow/v1.0/flows" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}"
```

</details>

<span id="get-flow"></span>

### 플로우 조회

**요청**

```
GET /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| flowId | Path | String | Y | 플로우 아이디 |

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
  "flow": {
    "flowId": "플로우_아이디",
    "flowName": "플로우_이름",
    "description": "플로우_설명",
    "messagePurpose": "NORMAL",
    "steps": [
      {
        "messageChannel": "EMAIL",
        "templateId": "이메일_템플릿_아이디",
        "nextSteps": [
          {
            "messageChannel": "ALIMTALK",
            "templateId": "알림톡_템플릿_아이디",
            "nextSteps": [
              {
                "messageChannel": "SMS",
                "templateId": "SMS_템플릿_아이디",
                "nextSteps": []
              }
            ]
          }
        ]
      }
    ]
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 조회
GET {{endpoint}}/flow/v1.0/flows/플로우_아이디
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "{endpoint}/flow/v1.0/flows/플로우_아이디" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}"
```

</details>

<span id="put-flow"></span>

### 플로우 수정

**요청**

```
PUT /flow/v1.0/flows/{flowId}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| flowId | Path | String | Y | 플로우 아이디 |

**요청 본문**

```json
{
  "flowName": "플로우_이름",
  "description": "플로우_설명",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "이메일_템플릿_아이디",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "알림톡_템플릿_아이디",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_템플릿_아이디",
            "nextSteps": []
          }
        ]
      }
    ]
  }
}
```

* 플로우 수정은 플로우 생성과 동일한 요청 본문을 사용합니다.

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
### 플로우 수정
PUT {{endpoint}}/flow/v1.0/flows/{{flowId}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "flowName": "플로우_이름",
  "description": "플로우_설명",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "이메일_템플릿_아이디",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "알림톡_템플릿_아이디",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_템플릿_아이디",
            "nextSteps": []
          }
        ]
      }
    ]
  }
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X PUT "{endpoint}/flow/v1.0/flows/플로우_아이디" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}" \
     -d '{
      "flowName": "플로우_이름",
      "description": "플로우_설명",
      "messagePurpose": "NORMAL",
      "steps": {
        "messageChannel": "EMAIL",
        "templateId": "이메일_템플릿_아이디",
        "nextSteps": [
          {
            "messageChannel": "ALIMTALK",
            "templateId": "알림톡_템플릿_아이디",
            "nextSteps": [
              {
                "messageChannel": "SMS",
                "templateId": "SMS_템플릿_아이디",
                "nextSteps": []
              }
            ]
          }
        ]
      }'
}
```

</details>

<span id="delete-flow"></span>

### 플로우 삭제

**요청**

```
DELETE /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| flowId | Path | String | Y | 플로우 아이디 |

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
### 플로우 삭제
DELETE {{endpoint}}/flow/v1.0/flows/{{flowId}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X DELETE "{endpoint}/flow/v1.0/flows/플로우_아이디" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: {appKey}" \
     -H "X-NHN-Authorization: {accessToken}"
```

</details>
