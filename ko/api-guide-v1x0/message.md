<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>메시지</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 메시지**



<span id="messageV1x0001SmsFreeFormMessages"></span>

## 자유 양식 메시지 발송 요청 - SMS

SMS에 대한 자유 양식 메시지를 발송요청 합니다. 요청 본문에 메시지 내용을 입력해 메시지를 발송 요청합니다.

각 메시지 채널로 메시지를 발송하기 위해서는 각 메시지 채널의 발신 정보가 등록되어야 있어야 합니다. 발신 정보 등록은 **Notification Hub 콘솔** > **발신 정보 탭**에서 진행할 수 있습니다. 메시지 채널의 발신 정보에 대한 자세한 설명은 **Notification** > **Notification Hub** > **이용 정책 및 사전 설정 안내**에서 확인할 수 있습니다.


**요청**

```
POST /message/v1.0/SMS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messagePurpose | Path  | String | Y | 메시지 목적입니다. |

요청 파라미터 밑에 추가될 추가 설명 입니다.


**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.197+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "content" : {
    "messageType" : "SMS",
    "title" : "명절 운영시간 공지",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다. 방문해주세요^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  },
  "dryRun" : false
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | N | 통계 키 아이디 |
| scheduledDateTime | String | N | 예약 발송 시간 |
| confirmBeforeSend | Boolean | N | 확인 후 발송 여부 |
| sender | Object | N | No description |
| sender.senderPhoneNumber | String | Y | 발신 번호 |
| recipients | Array | N | No description |
| recipients[].contacts | Array | N | No description |
| recipients[].templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| id | String | N | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| content | Object | N | No description |
| content.messageType | String | Y | 발송 메시지 유형(SMS, LMS, MMS)<br>설정 가능한 값: [SMS, LMS, MMS] |
| content.title | String | N | 메시지 제목 |
| content.body | String | Y | 메시지 본문 |
| content.attachmentIds | Array | N | 첨부 파일 아이디 최대 3개<br>기본값: [] |
| dryRun | Boolean | N | 발송을 시뮬레이션 모드로 실행합니다. 실제 발송은 하지 않습니다.<br>연락처 별 수신 결과 상태는 발송 실패(SEND_FAILED)로 설정됩니다.<br><br>기본값: false |

* 메시지 채널에 따라 **sender**, **content** 필드는 서로 다른 형식을 가집니다.
* 메시지 채널에 따라 **recipients[].contact.contactType**, **recipients[].contact.contact** 필드에 입력할 수 있는 값이 달라집니다.
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
* 알림톡(ALIMTALK)은 발송 시 템플릿이 반드시 필요합니다. 자유 양식 메시지 발송을 지원하지 않습니다.
* 친구톡(FRIENDTALK)은 NORMAL(일반) 발신 프로필 유형만 사용할 수 있습니다. GROUP(그룹) 발신 프로필 유형의 발신 키를 사용하면 발송에 실패합니다.
* 발신자 프로필 유형은 **GROUP(그룹)**과 **NORMAL(일반)**이 있습니다. **GROUP**은 그룹 발신자 프로필, **NORMAL**은 일반 발신자 프로필입니다.


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
| header | Object | No description |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |

응답 밑에 추가될 추가 설명 입니다.


**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 자유 양식 메시지 발송 요청 - SMS

POST {{endpoint}}/message/v1.0/SMS/free-form-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.197+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "content" : {
    "messageType" : "SMS",
    "title" : "명절 운영시간 공지",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다. 방문해주세요^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  },
  "dryRun" : false
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/SMS/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.197+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "content" : {
    "messageType" : "SMS",
    "title" : "명절 운영시간 공지",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다. 방문해주세요^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  },
  "dryRun" : false
}'
```

</details>
<span id="messageV1x0002FriendtalkFreeFormMessages"></span>

## 자유 양식 메시지 발송 요청 - 친구톡(FRIENDTALK)

친구톡(FRIENDTALK)에 대한 자유 양식 메시지를 발송요청 합니다.


**요청**

```
POST /message/v1.0/FRIENDTALK/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messagePurpose | Path  | String | Y | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.260+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
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
  "dryRun" : false
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | N | 통계 키 아이디 |
| scheduledDateTime | String | N | 예약 발송 시간 |
| confirmBeforeSend | Boolean | N | 확인 후 발송 여부 |
| sender | Object | N | No description |
| sender.senderKey | String | Y | 발신프로필 발신키 |
| recipients | Array | N | No description |
| recipients[].contacts | Array | N | No description |
| recipients[].templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| id | String | N | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| content | Object | N | No description |
| content.messageType | String | N | 템플릿 메시지 유형(TEXT: 텍스트형, IMAGE: 이미지형, WIDE_IMAGE: 와이드 이미지형, WIDE_ITEMLIST: 와이드아이템리스트형, CAROUSEL_FEED: 캐러셀피드형, default: TEXT) |
| content.content | String | N | 템플릿 본문 |
| content.attachmentId | String | N | 첨부 파일 아이디 |
| content.imageUrl | String | N | 템플릿 이미지 URL |
| content.imageLink | String | N | 템플릿 이미지 링크 |
| content.buttons | Array | N | 템플릿 버튼<br>기본값: [] |
| content.buttons[].type | String | N | 템플릿 버튼 타입(WL: 웹 링크, AL: 앱 링크, BK: 봇 키워드, MD: 메시지 전달, BF: 비지니스폼)<br>설정 가능한 값: [WL, AL, BK, MD, BF] |
| content.buttons[].name | String | N | 템플릿 버튼 이름 |
| content.buttons[].linkMo | String | N | 템플릿 버튼 모바일 웹 링크 |
| content.buttons[].linkPc | String | N | 템플릿 버튼 PC 웹 링크 |
| content.buttons[].schemeIos | String | N | 템플릿 버튼 iOS 앱 링크 |
| content.buttons[].schemeAndroid | String | N | 템플릿 버튼 안드로이드 앱 링크 |
| content.buttons[].bizFormKey | String | N | BF(비즈니스 폼) 타입 버튼 시, 비즈폼 키 |
| content.header | String | N | 헤더(와이드 아이템리스트 메시지 타입 사용 시, 필수, 최대 25자) |
| content.item | Object | N | No description |
| content.item.list | Array | N | No description<br>기본값: [] |
| content.item.list[].title | String | N | 아이템 타이틀 첫번째 아이템 25자, 2~4번째 30자 |
| content.item.list[].attachmentId | String | N | 첨부 파일 아이디 |
| content.item.list[].imageUrl | String | N | 아이템 이미지 URL |
| content.item.list[].linkMo | String | N | 대표 링크 모바일 웹 링크 |
| content.item.list[].linkPc | String | N | 대표 링크 PC 웹 링크 |
| content.item.list[].schemeIos | String | N | 대표 링크 iOS 앱 링크 |
| content.item.list[].schemeAndroid | String | N | 대표 링크 안드로이드 앱 링크 |
| content.carousel | Object | N | No description |
| content.carousel.list | Array | N | No description<br>기본값: [] |
| content.carousel.list[].header | String | N | 캐러셀 아이템 제목 |
| content.carousel.list[].message | String | N | 캐러셀 아이템 메시지 |
| content.carousel.list[].attachment | Object | N | No description |
| content.carousel.list[].attachment.buttons | Array | N | No description<br>기본값: [] |
| content.carousel.list[].attachment.image | Object | N | No description |
| content.carousel.list[].attachment.image.attachmentId | String | N | 첨부 파일 아이디 |
| content.carousel.list[].attachment.image.imageUrl | String | N | 캐러셀 아이템 이미지 URL |
| content.carousel.list[].attachment.image.imageLink | String | N | 캐러셀 아이템 이미지 링크 |
| content.carousel.tail | Object | N | No description |
| content.carousel.tail.linkMo | String | N | 대표 링크 모바일 웹 링크 |
| content.carousel.tail.linkPc | String | N | 대표 링크 PC 웹 링크 |
| content.carousel.tail.schemeIos | String | N | 대표 링크 iOS 앱 링크 |
| content.carousel.tail.schemeAndroid | String | N | 대표 링크 안드로이드 앱 링크 |
| content.coupon | Object | N | No description |
| content.coupon.title | String | N | 쿠폰 이름 |
| content.coupon.description | String | N | 쿠폰 상세 설명 (일반 텍스트, 이미지형 최대 12자 / 와이드 이미지형, 와이드 아이템리스트형 최대 18자) |
| content.coupon.linkMo | String | N | 대표 링크 모바일 웹 링크 |
| content.coupon.linkPc | String | N | 대표 링크 PC 웹 링크 |
| content.coupon.schemeIos | String | N | 대표 링크 iOS 앱 링크 |
| content.coupon.schemeAndroid | String | N | 대표 링크 안드로이드 앱 링크 |
| dryRun | Boolean | N | 발송을 시뮬레이션 모드로 실행합니다. 실제 발송은 하지 않습니다.<br>연락처 별 수신 결과 상태는 발송 실패(SEND_FAILED)로 설정됩니다.<br><br>기본값: false |



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
| header | Object | No description |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 자유 양식 메시지 발송 요청 - 친구톡(FRIENDTALK)

POST {{endpoint}}/message/v1.0/FRIENDTALK/free-form-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.260+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
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
  "dryRun" : false
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/FRIENDTALK/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.260+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
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
  "dryRun" : false
}'
```

</details>
<span id="messageV1x0003EmailFreeFormMessages"></span>

## 자유 양식 메시지 발송 요청 - 이메일(EMAIL)

이메일(EMAIL)에 대한 자유 양식 메시지를 발송요청 합니다.


**요청**

```
POST /message/v1.0/EMAIL/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messagePurpose | Path  | String | Y | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.275+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "content" : {
    "title" : "[NHN Cloud Email][##env##] 모니터링 알림",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  },
  "dryRun" : false
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | N | 통계 키 아이디 |
| scheduledDateTime | String | N | 예약 발송 시간 |
| confirmBeforeSend | Boolean | N | 확인 후 발송 여부 |
| sender | Object | N | No description |
| sender.senderMailAddress | String | Y | 발신 메일 주소 |
| recipients | Array | N | No description |
| recipients[].contacts | Array | N | No description |
| recipients[].templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| id | String | N | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| content | Object | N | No description |
| content.title | String | Y | 템플릿 메일 제목 |
| content.body | String | Y | 템플릿 메일 본문 |
| content.attachmentIds | Array | N | 템플릿 첨부파일 ID<br>기본값: [] |
| dryRun | Boolean | N | 발송을 시뮬레이션 모드로 실행합니다. 실제 발송은 하지 않습니다.<br>연락처 별 수신 결과 상태는 발송 실패(SEND_FAILED)로 설정됩니다.<br><br>기본값: false |



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
| header | Object | No description |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 자유 양식 메시지 발송 요청 - 이메일(EMAIL)

POST {{endpoint}}/message/v1.0/EMAIL/free-form-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.275+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "content" : {
    "title" : "[NHN Cloud Email][##env##] 모니터링 알림",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  },
  "dryRun" : false
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/EMAIL/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.275+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "content" : {
    "title" : "[NHN Cloud Email][##env##] 모니터링 알림",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  },
  "dryRun" : false
}'
```

</details>
<span id="messageV1x0004RcsFreeFormMessages"></span>

## 자유 양식 메시지 발송 요청 - RCS

RCS에 대한 자유 양식 메시지를 발송요청 합니다.


**요청**

```
POST /message/v1.0/RCS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messagePurpose | Path  | String | Y | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.284+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
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
  },
  "options" : {
    "expiryOption" : 1,
    "groupId" : "20240814125609swLmoZTsGr0"
  },
  "dryRun" : false
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | N | 통계 키 아이디 |
| scheduledDateTime | String | N | 예약 발송 시간 |
| confirmBeforeSend | Boolean | N | 확인 후 발송 여부 |
| sender | Object | N | No description |
| sender.brandId | String | Y | 브랜드 아이디 |
| sender.chatbotId | String | Y | 대화방(챗봇) 아이디 |
| recipients | Array | N | No description |
| recipients[].contacts | Array | N | No description |
| recipients[].templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| id | String | N | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| content | Object | N | No description |
| content.messageType | Object | N | No description |
| content.title | String | N | 메시지 제목 |
| content.body | String | N | 메시지 본문 |
| content.smsType | Object | N | No description |
| content.lmsType | Object | N | No description |
| content.mmsType | Object | N | No description |
| content.messagebaseId | String | N | RCS biz센터 템플릿 아이디 |
| content.unsubscribePhoneNumber | String | N | 수신 거부 번호 (광고 발송일 경우 필수) |
| content.cards | Array | N | RCS 카드<br>기본값: [] |
| content.cards[].title | String | N | 제목 |
| content.cards[].description | String | N | 본문 |
| content.cards[].attachmentId | String | N | 이미지 첨부파일 아이디 |
| content.cards[].mTitle | String | N | 메인 타이틀 |
| content.cards[].mTitleMedia | String | N | 메인 타이틀 로고 파일 ID |
| content.cards[].title1 | String | N | 제목 1 |
| content.cards[].title2 | String | N | 제목 2 |
| content.cards[].title3 | String | N | 제목 3 |
| content.cards[].description1 | String | N | 본문 1 |
| content.cards[].description2 | String | N | 본문 2 |
| content.cards[].description3 | String | N | 본문 3 |
| content.cards[].buttons | Array | N | No description<br>기본값: [] |
| content.buttons | Array | N | RCS 버튼 리스트<br>기본값: [] |
| content.buttons[].buttonType | String | N | buttonType값과 동일한 이름을 가진 Action 객체가 buttonJson으로 포함됨.<br>버튼 타입 대화방 열기(COMPOSE), 복사하기(CLIPBOARD), 전화 걸기(DIALER), 지도 보여주기(MAP_SHOW), 지도 검색하기(MAP_QUERY), 현재 위치 공유하기(MAP_SHARE), URL 연결하기(URL), 일정 등록하기(CALENDAR)<br><br>설정 가능한 값: [COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | N | No description |
| content.buttons[].buttonJson.action | Object | N | No description |
| options | Object | N | No description |
| options.expiryOption | Integer | N | 통신사에서 디바이스로 발송 시도하는 시간 (1: 1일, 2: 40초, 3: 3분, 4: 1시간)<br>기본값: 1 |
| options.groupId | String | N | RCS BizCenter 통계 연동을 위한 group ID |
| dryRun | Boolean | N | 발송을 시뮬레이션 모드로 실행합니다. 실제 발송은 하지 않습니다.<br>연락처 별 수신 결과 상태는 발송 실패(SEND_FAILED)로 설정됩니다.<br><br>기본값: false |



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
| header | Object | No description |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 자유 양식 메시지 발송 요청 - RCS

POST {{endpoint}}/message/v1.0/RCS/free-form-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.284+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
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
  },
  "options" : {
    "expiryOption" : 1,
    "groupId" : "20240814125609swLmoZTsGr0"
  },
  "dryRun" : false
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/RCS/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.284+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
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
  },
  "options" : {
    "expiryOption" : 1,
    "groupId" : "20240814125609swLmoZTsGr0"
  },
  "dryRun" : false
}'
```

</details>
<span id="messageV1x0005PushFreeFormMessages"></span>

## 자유 양식 메시지 발송 요청 - PUSH

PUSH에 대한 자유 양식 메시지를 발송요청 합니다.


**요청**

```
POST /message/v1.0/PUSH/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messagePurpose | Path  | String | Y | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.295+09:00",
  "confirmBeforeSend" : false,
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
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
  "dryRun" : false
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | N | 통계 키 아이디 |
| scheduledDateTime | String | N | 예약 발송 시간 |
| confirmBeforeSend | Boolean | N | 확인 후 발송 여부 |
| recipients | Array | N | No description |
| recipients[].contacts | Array | N | No description |
| recipients[].templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| id | String | N | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| content | Object | N | No description |
| dryRun | Boolean | N | 발송을 시뮬레이션 모드로 실행합니다. 실제 발송은 하지 않습니다.<br>연락처 별 수신 결과 상태는 발송 실패(SEND_FAILED)로 설정됩니다.<br><br>기본값: false |



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
| header | Object | No description |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 자유 양식 메시지 발송 요청 - PUSH

POST {{endpoint}}/message/v1.0/PUSH/free-form-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.295+09:00",
  "confirmBeforeSend" : false,
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
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
  "dryRun" : false
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/PUSH/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.295+09:00",
  "confirmBeforeSend" : false,
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
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
  "dryRun" : false
}'
```

</details>
<span id="messageV1x0006TemplateMessages"></span>

## 템플릿 메시지 발송 요청

등록한 템플릿을 이용해 메시지를 발송합니다.<br>
템플릿을 등록하지 않았다면, 템플릿을 등록하고 발송해야 합니다.<br>
<br>
수신 대상 설정은 단건 수신자, 대량 수신자, 그룹 쿼리 중 하나를 선택해 설정해야 합니다.<br>
* 단건 수신자(recipient)<br>
* 대량/그룹 수신자(id)<br>
<br>
예약 발송의 경우 'scheduledDateTime'를 설정합니다.<br>
확인 후 발송의 경우 'confirmBeforeSend'를 true로 설정합니다.<br>


**요청**

```
POST /message/v1.0/{messageChannel}/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageChannel | Path  | String | Y | 메시지 채널입니다. |
| messagePurpose | Path  | String | Y | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.299+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "dryRun" : false
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | N | 통계 키 아이디 |
| templateId | String | N | 템플릿 ID |
| scheduledDateTime | String | N | 예약 발송 시간 |
| confirmBeforeSend | Boolean | N | 확인 후 발송 여부 |
| templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| recipients | Array | N | No description |
| recipients[].contacts | Array | N | No description |
| recipients[].templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| id | String | N | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| dryRun | Boolean | N | 발송을 시뮬레이션 모드로 실행합니다. 실제 발송은 하지 않습니다.<br>연락처 별 수신 결과 상태는 발송 실패(SEND_FAILED)로 설정됩니다.<br><br>기본값: false |



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
| header | Object | No description |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 메시지 발송 요청

POST {{endpoint}}/message/v1.0/{{messageChannel}}/template-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.299+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "dryRun" : false
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/${messageChannel}/template-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.299+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "dryRun" : false
}'
```

</details>
<span id="messageV1x0007AlimtalkTemplateMessages"></span>

## 알림톡 템플릿 메시지 발송

등록한 템플릿을 이용해 메시지를 발송합니다.<br>
템플릿을 등록하지 않았다면, 템플릿을 등록하고 발송해야 합니다.<br>
<br>
수신 대상 설정은 단건 수신자, 대량 수신자, 그룹 쿼리 중 하나를 선택해 설정해야 합니다.<br>
* 단건 수신자(recipient)<br>
* 대량/그룹 수신자(id)<br>
<br>
예약 발송의 경우 'scheduledDateTime'를 설정합니다.<br>
확인 후 발송의 경우 'confirmBeforeSend'를 true로 설정합니다.<br>


**요청**

```
POST /message/v1.0/ALIMTALK/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messagePurpose | Path  | String | Y | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "templateId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.305+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "dryRun" : false
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | N | 통계 키 아이디 |
| sender | Object | N | No description |
| sender.senderKey | String | Y | 발신프로필 발신키 |
| templateId | String | N | 템플릿 ID |
| scheduledDateTime | String | N | 예약 발송 시간 |
| confirmBeforeSend | Boolean | N | 확인 후 발송 여부 |
| templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| recipients | Array | N | No description |
| recipients[].contacts | Array | N | No description |
| recipients[].templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| id | String | N | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| dryRun | Boolean | N | 발송을 시뮬레이션 모드로 실행합니다. 실제 발송은 하지 않습니다.<br>연락처 별 수신 결과 상태는 발송 실패(SEND_FAILED)로 설정됩니다.<br><br>기본값: false |



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
| header | Object | No description |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 메시지 발송

POST {{endpoint}}/message/v1.0/ALIMTALK/template-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "statsKeyId" : "aA123456",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "templateId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.305+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "dryRun" : false
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/ALIMTALK/template-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "statsKeyId" : "aA123456",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "templateId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.305+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "dryRun" : false
}'
```

</details>
<span id="messageV1x0008RcsTemplateMessages"></span>

## RCS 템플릿 메시지 발송

등록한 템플릿을 이용해 메시지를 발송합니다.<br>
템플릿을 등록하지 않았다면, 템플릿을 등록하고 발송해야 합니다.<br>
<br>
수신 대상 설정은 단건 수신자, 대량 수신자, 그룹 쿼리 중 하나를 선택해 설정해야 합니다.<br>
* 단건 수신자(recipient)<br>
* 대량/그룹 수신자(id)<br>
<br>
예약 발송의 경우 'scheduledDateTime'를 설정합니다.<br>
확인 후 발송의 경우 'confirmBeforeSend'를 true로 설정합니다.<br>


**요청**

```
POST /message/v1.0/RCS/template-messages/{messagePurpose}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| messagePurpose | Path  | String | Y | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "sender" : {
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "unsubscribePhoneNumber" : "08012341234"
  },
  "templateId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.308+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "options" : {
    "expiryOption" : 1,
    "groupId" : "20240814125609swLmoZTsGr0"
  },
  "dryRun" : false
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | N | 통계 키 아이디 |
| sender | Object | N | No description |
| sender.chatbotId | String | N | 대화방(챗봇) 아이디 |
| content | Object | N | No description |
| content.unsubscribePhoneNumber | String | N | 수신거부 전화번호 |
| templateId | String | N | 템플릿 ID |
| scheduledDateTime | String | N | 예약 발송 시간 |
| confirmBeforeSend | Boolean | N | 확인 후 발송 여부 |
| templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| recipients | Array | N | No description |
| recipients[].contacts | Array | N | No description |
| recipients[].templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| id | String | N | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| options | Object | N | No description |
| options.expiryOption | Integer | N | 통신사에서 디바이스로 발송 시도하는 시간 (1: 1일, 2: 40초, 3: 3분, 4: 1시간)<br>기본값: 1 |
| options.groupId | String | N | RCS BizCenter 통계 연동을 위한 group ID |
| dryRun | Boolean | N | 발송을 시뮬레이션 모드로 실행합니다. 실제 발송은 하지 않습니다.<br>연락처 별 수신 결과 상태는 발송 실패(SEND_FAILED)로 설정됩니다.<br><br>기본값: false |



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
| header | Object | No description |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### RCS 템플릿 메시지 발송

POST {{endpoint}}/message/v1.0/RCS/template-messages/{{messagePurpose}}

{
  "statsKeyId" : "aA123456",
  "sender" : {
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "unsubscribePhoneNumber" : "08012341234"
  },
  "templateId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.308+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "options" : {
    "expiryOption" : 1,
    "groupId" : "20240814125609swLmoZTsGr0"
  },
  "dryRun" : false
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/RCS/template-messages/${messagePurpose}" \
-d '{
  "statsKeyId" : "aA123456",
  "sender" : {
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "unsubscribePhoneNumber" : "08012341234"
  },
  "templateId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.308+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "options" : {
    "expiryOption" : 1,
    "groupId" : "20240814125609swLmoZTsGr0"
  },
  "dryRun" : false
}'
```

</details>
<span id="messageV1x0009FlowMessages"></span>

## 플로우 메시지 발송

등록한 플로우를 이용해 메시지를 발송합니다.<br>
플로우를 등록하지 않았다면, 플로우를 등록하고 발송해야 합니다.<br>
<br>
수신 대상 설정은 단건 수신자, 대량 수신자, 그룹 쿼리 중 하나를 선택해 설정해야 합니다.<br>
* 단건 수신자(recipient)<br>
* 대량/그룹 수신자(id)<br>
<br>
예약 발송의 경우 'scheduledDateTime'를 설정합니다.<br>
확인 후 발송의 경우 'confirmBeforeSend'를 true로 설정합니다.<br>


**요청**

```
POST /message/v1.0/flow-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messagePurpose | Path  | String | Y | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "flowId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.312+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "flow" : {
    "steps" : [ {
      "messageChannel" : "SMS",
      "sender" : {
        "senderPhoneNumber" : "0123456789"
      },
      "content" : {
        "title" : "제목",
        "body" : "본문"
      },
      "options" : {
        "expiryOption:" : 1,
        "groupId\"" : "groupId"
      },
      "nextSteps" : [ {
        "messageChannel" : "RCS"
      } ]
    } ]
  },
  "dryRun" : false
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | N | 통계 키 아이디 |
| flowId | String | N | 플로우 ID |
| scheduledDateTime | String | N | 예약 발송 시간 |
| confirmBeforeSend | Boolean | N | 확인 후 발송 여부 |
| templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| recipients | Array | N | No description |
| recipients[].contacts | Array | N | No description |
| recipients[].templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| id | String | N | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| flow | Object | N | No description |
| flow.steps | Array | Y | No description |
| flow.steps[].messageChannel | Object | Y | No description |
| flow.steps[].sender | Object | N | 발신자 정보입니다. 발신자 정보는 메시지 채널에 따라 다르게 구성될 수 있습니다.<br> |
| flow.steps[].content | Object | N | 메시지 내용입니다. 메시지 내용은 메시지 채널에 따라 다르게 구성될 수 있습니다.<br> |
| flow.steps[].options | Object | N | 발송 옵션입니다. 발송 옵션은 메시지 채널에 따라 다르게 구성될 수 있습니다.<br> |
| flow.steps[].nextSteps | Array | N | 다음 단계입니다. 다음 단계가 없는 경우, 메시지 발송이 종료됩니다.<br> |
| dryRun | Boolean | N | 발송을 시뮬레이션 모드로 실행합니다. 실제 발송은 하지 않습니다.<br>연락처 별 수신 결과 상태는 발송 실패(SEND_FAILED)로 설정됩니다.<br><br>기본값: false |



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
| header | Object | No description |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 메시지 발송

POST {{endpoint}}/message/v1.0/flow-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "statsKeyId" : "aA123456",
  "flowId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.312+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "flow" : {
    "steps" : [ {
      "messageChannel" : "SMS",
      "sender" : {
        "senderPhoneNumber" : "0123456789"
      },
      "content" : {
        "title" : "제목",
        "body" : "본문"
      },
      "options" : {
        "expiryOption:" : 1,
        "groupId\"" : "groupId"
      },
      "nextSteps" : [ {
        "messageChannel" : "RCS"
      } ]
    } ]
  },
  "dryRun" : false
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/flow-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "statsKeyId" : "aA123456",
  "flowId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.312+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "flow" : {
    "steps" : [ {
      "messageChannel" : "SMS",
      "sender" : {
        "senderPhoneNumber" : "0123456789"
      },
      "content" : {
        "title" : "제목",
        "body" : "본문"
      },
      "options" : {
        "expiryOption:" : 1,
        "groupId\"" : "groupId"
      },
      "nextSteps" : [ {
        "messageChannel" : "RCS"
      } ]
    } ]
  },
  "dryRun" : false
}'
```

</details>
<span id="messageV1x0010InstantFlowMessages"></span>

## 인스턴트 플로우 메시지 발송

메시지 발송 요청 시 플로우를 정의해 메시지를 발송 요청합니다.<br>
<br>
인스턴트 플로우 입력 시 템플릿을 이용해 발송 요청하거나 직접 발신자 정보, 내용을 입력해 발송 요청할 수 있습니다.


**요청**

```
POST /message/v1.0/instant-flow-messages/{messagePurpose}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| messagePurpose | Path  | String | Y | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.316+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
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
      "options" : {
        "expiryOption:" : 1,
        "groupId\"" : "groupId"
      },
      "templateId" : "템플릿_아이디",
      "nextSteps" : [ ]
    } ]
  },
  "dryRun" : false
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | N | 통계 키 아이디 |
| scheduledDateTime | String | N | 예약 발송 시간 |
| confirmBeforeSend | Boolean | N | 확인 후 발송 여부 |
| templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| recipients | Array | Y | No description |
| recipients[].contacts | Array | N | No description |
| recipients[].templateParameters | Object | N | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터 보다 우선 시 됩니다.<br><br> |
| instantFlow | Object | Y | No description |
| instantFlow.steps | Array | Y | No description |
| instantFlow.steps[].messageChannel | Object | Y | No description |
| instantFlow.steps[].sender | Object | N | 발신자 정보입니다. 발신자 정보는 메시지 채널에 따라 다르게 구성될 수 있습니다.<br> |
| instantFlow.steps[].content | Object | N | 메시지 내용입니다. 메시지 내용은 메시지 채널에 따라 다르게 구성될 수 있습니다.<br> |
| instantFlow.steps[].options | Object | N | 발송 옵션입니다. 발송 옵션은 메시지 채널에 따라 다르게 구성될 수 있습니다.<br> |
| instantFlow.steps[].templateId | String | N | 템플릿 아이디입니다. 템플릿 아이디를 설정한 경우, 요청 시 발신자 정보(sender)와 메시지 내용(content)가 적용되지 않습니다.<br>인스턴트 플로우 메시지에서 템플릿 아이디를 설정하지 않는 경우, 발신자 정보(sender)와 메시지 내용(content)이 반드시 필요합니다.<br> |
| instantFlow.steps[].nextSteps | Array | N | 다음 단계입니다. 다음 단계가 없는 경우, 메시지 발송이 종료됩니다. |
| dryRun | Boolean | N | 발송을 시뮬레이션 모드로 실행합니다. 실제 발송은 하지 않습니다.<br>연락처 별 수신 결과 상태는 발송 실패(SEND_FAILED)로 설정됩니다.<br><br>기본값: false |



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
| header | Object | No description |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 인스턴트 플로우 메시지 발송

POST {{endpoint}}/message/v1.0/instant-flow-messages/{{messagePurpose}}

{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.316+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
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
      "options" : {
        "expiryOption:" : 1,
        "groupId\"" : "groupId"
      },
      "templateId" : "템플릿_아이디",
      "nextSteps" : [ ]
    } ]
  },
  "dryRun" : false
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/instant-flow-messages/${messagePurpose}" \
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2025-03-21T10:44:43.316+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
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
      "options" : {
        "expiryOption:" : 1,
        "groupId\"" : "groupId"
      },
      "templateId" : "템플릿_아이디",
      "nextSteps" : [ ]
    } ]
  },
  "dryRun" : false
}'
```

</details>
<span id="messageV1x0100MessageIdDoCancel"></span>

## 메시지 발송 취소

발송 취소할 메시지 아이디를 입력해 발송 취소합니다.<br>
메시지 발송 시 응답받은 메시지 아이디를 이용해 발송을 취소할 수 있습니다.<br>
메시지 내 모든 요청은 취소됩니다.<br>


**요청**

```
POST /message/v1.0/messages/{messageId}/do-cancel
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageId | Path  | String | Y |  |



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
| header | Object | No description |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 메시지 발송 취소

POST {{endpoint}}/message/v1.0/messages/{{messageId}}/do-cancel
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/messages/${messageId}/do-cancel" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="messageV1x0101MessageIdDoConfirm"></span>

## 메시지 발송 확인

확인 후 발송 요청한 메시지를 확인합니다.<br>


**요청**

```
POST /message/v1.0/messages/{messageId}/do-confirm
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageId | Path  | String | Y |  |



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
| header | Object | No description |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 메시지 발송 확인

POST {{endpoint}}/message/v1.0/messages/{{messageId}}/do-confirm
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/messages/${messageId}/do-confirm" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>