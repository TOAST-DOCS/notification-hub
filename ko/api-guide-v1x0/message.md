<!-- pre-align:aligned sig=65b610526e63 -->

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

<a id="free-form-message-sending-request---sms"></a>

## 자유 양식 메시지 발송 요청 - SMS

SMS에 대한 자유 양식 메시지 발송을 요청합니다. 메시지 내용을 요청 본문에 입력한 뒤 발송을 요청합니다.

각 메시지 채널로 메시지를 발송하기 위해서는 각 메시지 채널의 발신 정보가 등록되어 있어야 합니다. 발신 정보 등록은 **Notification Hub 콘솔** > **발신 정보 탭**에서 진행할 수 있습니다. 메시지 채널의 발신 정보에 대한 자세한 설명은 **Notification** > **Notification Hub** > **이용 정책 및 사전 설정 안내**에서 확인할 수 있습니다.


**요청**

```
POST /message/v1.0/SMS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| messagePurpose | Path | Enum | O | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | X | 통계 키 아이디 |
| scheduledDateTime | String | X | 예약 발송 시간 |
| confirmBeforeSend | Boolean | X | 확인 후 발송 여부 |
| sender | Object | X |  |
| sender.senderPhoneNumber | String | O | 발신 번호 |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 연락처입니다. 수신자를 지정하지 않고 연락처를 직접 입력하여 메시지를 발송할 수 있습니다. |
| recipients[].contacts[].clientReference | String | X | 수신자 별로 부여할 수 있는 사용자 지정 필드 입니다 |
| recipients[].templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| id | String | X | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| content | Object | X |  |
| content.messageType | String | O | 발송 메시지 유형(SMS, LMS, MMS)<br>[SMS(단문 메시지), LMS(장문 메시지), MMS(멀티미디어 메시지)] |
| content.title | String | X | 메시지 제목 |
| content.body | String | O | 메시지 본문 |
| content.attachmentIds | Array | X | 첨부 파일 아이디 최대 3개 |

* 메시지 채널에 따라 **sender**, **content** 필드는 서로 다른 형식을 가집니다.
* 메시지 채널에 따라 **recipients[].contact.contactType**, **recipients[].contact.contact** 필드에 입력할 수 있는 값이 달라집니다.
* 예약 발송의 경우 **scheduledDateTime**를 설정합니다. 발송이 시작되기 전의 예약 발송은 요청 취소가 가능합니다. 요청 취소 API를 호출하거나 **Notification Hub 콘솔** > **발송 조회**에서 취소할 수 있습니다.
* 승인 후 발송의 경우 **confirmBeforeSend**를 **true**로 설정합니다. 승인 후 발송인 메시지는 **Notification Hub 콘솔** > **발송 조회**에서 승인을 하면 발송이 진행됩니다.
* 예약 발송과 승인 후 발송은 동시에 설정할 수 없습니다.

<a id="sender-fields-by-message-channel"></a>

### 메시지 채널별 sender 필드

| 메시지 채널 | 필드 | 설명 |
| --- | --- | --- |
| SMS | sender.senderPhoneNumber | 발신자 번호 |
| RCS | sender.brandId | 브랜드 아이디 |
| RCS | sender.chatbotId | 대화방 아이디 |
| EMAIL | sender.senderMailAddress | 발신자 이메일 주소 |
| ALIMTALK | sender.senderKey | 발신 키 |
| ALIMTALK | sender.senderProfileType | 발신 프로필 유형<br>GROUP, NORMAL |

* 알림톡(ALIMTALK)은 발신 키(senderKey)와 발신 프로필 유형(senderProfileType)을 필수로 입력해야 합니다.
* 알림톡(ALIMTALK)은 발송 시 템플릿이 반드시 필요합니다. 자유 양식 메시지 발송을 지원하지 않습니다.
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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | O | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



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
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/SMS/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  }
}'
```

</details>

<span id="messageV1x0002BrandmessageFreeFormMessages"></span>

<a id="free-form-message-sending-request---brand-message-brandmessage"></a>

## 자유 양식 메시지 발송 요청 - 브랜드 메시지(BRANDMESSAGE)

브랜드 메시지(BRANDMESSAGE)에 대한 자유 양식 메시지 발송을 요청합니다.

브랜드 메시지는 카카오톡 친구톡 업그레이드 상품으로, 기존 친구톡보다 더 다양한 메시지 유형을 지원합니다.
- TEXT: 텍스트형
- IMAGE: 이미지형
- WIDE_IMAGE: 와이드 이미지형
- WIDE_ITEM_LIST: 와이드 아이템리스트형
- CAROUSEL_FEED: 캐러셀 피드형
- CAROUSEL_COMMERCE: 캐러셀 커머스형
- COMMERCE: 커머스형
- PREMIUM_VIDEO: 프리미엄 비디오형


**요청**

```
POST /message/v1.0/BRANDMESSAGE/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| messagePurpose | Path | Enum | O | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
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
    "chatBubbleType" : "TEXT",
    "adult" : false,
    "content" : null,
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "image" : {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    },
    "video" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailAttachmentId" : "20230131070811m2fDe1rXx80",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    },
    "buttons" : [ {
      "type" : "WL",
      "name" : "버튼명",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123",
      "chatExtra" : "extra_info",
      "chatEvent" : "event_name"
    } ],
    "header" : "헤더",
    "item" : {
      "list" : [ {
        "title" : "아이템 제목",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "carousel" : {
      "head" : {
        "header" : "인트로 헤더",
        "content" : null,
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "additionalContent" : "가격 정보",
        "buttons" : [ {
          "type" : "WL",
          "name" : "버튼명",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android",
          "bizFormKey" : "bizFormKey123",
          "chatExtra" : "extra_info",
          "chatEvent" : "event_name"
        } ],
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg",
          "imageLink" : "https://www.example.com"
        },
        "commerce" : {
          "title" : "상품 제목",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "coupon" : {
          "title" : "5000원 할인 쿠폰",
          "description" : "첫 구매 고객 전용",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "commerce" : {
      "title" : "상품 제목",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "coupon" : {
      "title" : "5000원 할인 쿠폰",
      "description" : "첫 구매 고객 전용",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "additionalContent" : "가격 정보"
  },
  "options" : {
    "audienceType" : "CUSTOMER",
    "targeting" : "M",
    "pushAlarm" : true,
    "unsubscribePhoneNumber" : "0801111234",
    "unsubscribeAuthNumber" : "1234"
  },
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| sender | Object | X |  |
| sender.senderKey | String | O | 발신 키(40자). 그룹 발신 키는 사용 불가 |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 연락처입니다. 수신자를 지정하지 않고 연락처를 직접 입력하여 메시지를 발송할 수 있습니다. |
| recipients[].contacts[].clientReference | String | X | 수신자 별로 부여할 수 있는 사용자 지정 필드 입니다 |
| recipients[].templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| id | String | X | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| content | Object | X |  |
| content.chatBubbleType | String | X | 메시지 말풍선 타입. TEXT: 텍스트형, IMAGE: 이미지형, WIDE: 와이드 이미지형, WIDE_ITEM_LIST: 와이드 아이템리스트형, CAROUSEL_FEED: 캐러셀 피드형, CAROUSEL_COMMERCE: 캐러셀 커머스형, COMMERCE: 커머스형, PREMIUM_VIDEO: 프리미엄 비디오형<br>[TEXT, IMAGE, WIDE, WIDE_ITEM_LIST, CAROUSEL_FEED, CAROUSEL_COMMERCE, COMMERCE, PREMIUM_VIDEO] |
| content.adult | Boolean | X | 성인용 메시지 여부(default: false). 성인용 설정 시 성인 인증을 완료한 수신자에게만 노출<br>기본값: false |
| content.content | String | X | 메시지 본문. TEXT: 필수(최대 1,300자, 줄바꿈 최대 99개), IMAGE: 필수(최대 1,300자), WIDE: 필수(최대 76자, 줄바꿈 최대 5개), PREMIUM_VIDEO: 선택(최대 76자, 줄바꿈 최대 5개). WIDE_ITEM_LIST/CAROUSEL_FEED/CAROUSEL_COMMERCE: 사용 불가. URL 입력 가능 |
| content.attachmentId | String | X | 첨부 파일 아이디. IMAGE/WIDE: attachmentId 또는 image.imageUrl 중 하나 필수 |
| content.image | Object | X |  |
| content.image.attachmentId | String | X | 첨부 파일 아이디. imageUrl과 택1 |
| content.image.imageUrl | String | X | 이미지 URL. attachmentId와 택1 |
| content.image.imageLink | String | X | 이미지 클릭 시 이동할 URL(http/https). 선택. 미설정 시 카카오톡 이미지 뷰어 사용 |
| content.video | Object | X |  |
| content.video.videoUrl | String | O | 카카오TV 동영상 URL(https://tv.kakao.com/으로 시작). PREMIUM_VIDEO 타입 필수 |
| content.video.thumbnailAttachmentId | String | X | 썸네일 이미지 첨부 파일 아이디. thumbnailUrl과 택1. 일반 이미지 업로드 API로 등록한 이미지만 사용 가능 |
| content.video.thumbnailUrl | String | X | 동영상 썸네일 이미지 URL. thumbnailAttachmentId와 택1. 일반 이미지 업로드 API로 등록한 이미지만 사용 가능. 미설정 시 카카오TV 기본 썸네일 사용 |
| content.buttons | Array | X | 메시지 버튼 목록. TEXT/IMAGE: 최대 5개(쿠폰 적용 시 최대 4개), WIDE/WIDE_ITEM_LIST: 최대 2개, PREMIUM_VIDEO: 최대 1개, COMMERCE: 필수(최소 1개, 최대 2개). CAROUSEL_FEED/CAROUSEL_COMMERCE: 캐러셀 아이템 내 attachment.buttons 사용 |
| content.buttons[].type | String | O | 버튼 타입. WL: 웹 링크, AL: 앱 링크, BK: 봇 키워드, MD: 메시지 전달, BC: 상담톡 전환, BT: 챗봇 전환, BF: 비즈니스폼, AC: 채널 추가<br>[WL, AL, BK, MD, BC, BT, BF, AC] |
| content.buttons[].name | String | X | 버튼 이름. TEXT/IMAGE: 최대 14자, 그 외: 최대 8자. AC 타입: 값 없이 전송. BF 타입: "설문 참여하기", "신청하기", "응모하기" 중 택1 |
| content.buttons[].linkMo | String | X | 모바일 웹 링크(http/https). WL 타입 필수, AL 타입 선택(schemeIos/schemeAndroid 중 하나와 함께 입력 시 필요) |
| content.buttons[].linkPc | String | X | PC 웹 링크(http/https). WL/AL 타입 선택 |
| content.buttons[].schemeIos | String | X | iOS 앱 링크. AL 타입: linkMo, schemeAndroid, schemeIos 중 2개 이상 필수 |
| content.buttons[].schemeAndroid | String | X | 안드로이드 앱 링크. AL 타입: linkMo, schemeAndroid, schemeIos 중 2개 이상 필수 |
| content.buttons[].bizFormKey | String | X | 비즈니스폼 키. BF 타입 필수 |
| content.buttons[].chatExtra | String | X | BC(상담톡 전환), BT(챗봇 전환) 타입 버튼의 메타 정보 |
| content.buttons[].chatEvent | String | X | BT(챗봇 전환) 타입 버튼의 봇 이벤트명 |
| content.header | String | X | 메시지 제목. WIDE_ITEM_LIST: 필수(최대 20자), PREMIUM_VIDEO: 선택(최대 20자). 그 외 타입: 사용 불가 |
| content.item | Object | X |  |
| content.item.list | Array | O | 아이템 목록. 최소 3개, 최대 4개 |
| content.item.list[].title | String | X | 아이템 제목(줄바꿈 최대 1개). 첫 번째 아이템: 선택(최대 25자), 2~4번째 아이템: 필수(최대 30자) |
| content.item.list[].image | Object | O |  |
| content.item.list[].image.attachmentId | String | X | 첨부 파일 아이디. imageUrl과 택1 |
| content.item.list[].image.imageUrl | String | X | 이미지 URL. attachmentId와 택1 |
| content.item.list[].linkMo | String | O | 아이템 클릭 시 이동할 모바일 웹 링크(http/https). 필수 |
| content.item.list[].linkPc | String | X | 아이템 클릭 시 이동할 PC 웹 링크(http/https). 선택 |
| content.item.list[].schemeIos | String | X | 아이템 클릭 시 실행할 iOS 앱 링크. 선택 |
| content.item.list[].schemeAndroid | String | X | 아이템 클릭 시 실행할 안드로이드 앱 링크. 선택 |
| content.carousel | Object | X |  |
| content.carousel.head | Object | X |  |
| content.carousel.head.header | String | O | 인트로 헤더. head 사용 시 필수(최대 20자) |
| content.carousel.head.content | String | O | 인트로 내용. head 사용 시 필수(최대 50자) |
| content.carousel.head.image | Object | O |  |
| content.carousel.head.image.attachmentId | String | X | 첨부 파일 아이디. imageUrl과 택1 |
| content.carousel.head.image.imageUrl | String | X | 이미지 URL. attachmentId와 택1 |
| content.carousel.head.linkMo | String | X | 인트로 클릭 시 이동할 모바일 웹 링크. 다른 링크(linkPc/schemeIos/schemeAndroid) 입력 시 필수 |
| content.carousel.head.linkPc | String | X | 인트로 클릭 시 이동할 PC 웹 링크. 선택 |
| content.carousel.head.schemeIos | String | X | 인트로 클릭 시 실행할 iOS 앱 링크. 선택 |
| content.carousel.head.schemeAndroid | String | X | 인트로 클릭 시 실행할 안드로이드 앱 링크. 선택 |
| content.carousel.list | Array | O | 캐러셀 아이템 목록. head 사용 시 1~5개, 미사용 시 2~6개 |
| content.carousel.list[].header | String | X | 캐러셀 아이템 제목. CAROUSEL_FEED: 필수(최대 20자). CAROUSEL_COMMERCE: 사용 불가 |
| content.carousel.list[].message | String | X | 캐러셀 아이템 메시지. CAROUSEL_FEED: 필수(최대 180자). CAROUSEL_COMMERCE: 사용 불가 |
| content.carousel.list[].additionalContent | String | X | 부가 콘텐츠. CAROUSEL_COMMERCE: 선택(최대 34자). CAROUSEL_FEED: 사용 불가 |
| content.carousel.list[].buttons | Array | O | 캐러셀 아이템 버튼. 최소 1개, 최대 2개 필수. AC 버튼은 마지막 위치 |
| content.carousel.list[].buttons[].type | String | O | 버튼 타입. WL: 웹 링크, AL: 앱 링크, BK: 봇 키워드, MD: 메시지 전달, BC: 상담톡 전환, BT: 챗봇 전환, BF: 비즈니스폼, AC: 채널 추가<br>[WL, AL, BK, MD, BC, BT, BF, AC] |
| content.carousel.list[].buttons[].name | String | X | 버튼 이름. TEXT/IMAGE: 최대 14자, 그 외: 최대 8자. AC 타입: 값 없이 전송. BF 타입: "설문 참여하기", "신청하기", "응모하기" 중 택1 |
| content.carousel.list[].buttons[].linkMo | String | X | 모바일 웹 링크(http/https). WL 타입 필수, AL 타입 선택(schemeIos/schemeAndroid 중 하나와 함께 입력 시 필요) |
| content.carousel.list[].buttons[].linkPc | String | X | PC 웹 링크(http/https). WL/AL 타입 선택 |
| content.carousel.list[].buttons[].schemeIos | String | X | iOS 앱 링크. AL 타입: linkMo, schemeAndroid, schemeIos 중 2개 이상 필수 |
| content.carousel.list[].buttons[].schemeAndroid | String | X | 안드로이드 앱 링크. AL 타입: linkMo, schemeAndroid, schemeIos 중 2개 이상 필수 |
| content.carousel.list[].buttons[].bizFormKey | String | X | 비즈니스폼 키. BF 타입 필수 |
| content.carousel.list[].buttons[].chatExtra | String | X | BC(상담톡 전환), BT(챗봇 전환) 타입 버튼의 메타 정보 |
| content.carousel.list[].buttons[].chatEvent | String | X | BT(챗봇 전환) 타입 버튼의 봇 이벤트명 |
| content.carousel.list[].image | Object | O |  |
| content.carousel.list[].image.attachmentId | String | X | 첨부 파일 아이디. imageUrl과 택1 |
| content.carousel.list[].image.imageUrl | String | X | 이미지 URL. attachmentId와 택1 |
| content.carousel.list[].image.imageLink | String | X | 이미지 클릭 시 이동할 URL(http/https). 선택. 미설정 시 카카오톡 이미지 뷰어 사용 |
| content.carousel.list[].commerce | Object | X |  |
| content.carousel.list[].commerce.title | String | O | 상품 제목(최대 30자). 필수 |
| content.carousel.list[].commerce.regularPrice | Integer | O | 정상 가격(0~99,999,999). 필수 |
| content.carousel.list[].commerce.discountPrice | Integer | X | 할인 후 가격(0~99,999,999). 선택. 사용 시 discountRate 또는 discountFixed 중 하나 필수 |
| content.carousel.list[].commerce.discountRate | Integer | X | 할인율(0~100). discountPrice 존재 시 discountFixed와 택1 |
| content.carousel.list[].commerce.discountFixed | Integer | X | 정액 할인 가격(0~999,999). discountPrice 존재 시 discountRate와 택1 |
| content.carousel.list[].coupon | Object | X |  |
| content.carousel.list[].coupon.title | String | O | 쿠폰 제목. 필수. 형식: "{N}원 할인 쿠폰"(N: 1~99,999,999), "{N}% 할인 쿠폰"(N: 1~100), "배송비 할인 쿠폰", "{상품명} 무료 쿠폰"(상품명 최대 7자), "{상품명} UP 쿠폰"(상품명 최대 7자) 중 택1 |
| content.carousel.list[].coupon.description | String | O | 쿠폰 상세 설명. 필수. TEXT/IMAGE/COMMERCE: 최대 12자, WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO: 최대 18자 |
| content.carousel.list[].coupon.linkMo | String | X | 쿠폰 클릭 시 이동할 모바일 웹 링크(http/https). 채널 쿠폰 URL이 아닌 경우 필수 |
| content.carousel.list[].coupon.linkPc | String | X | 쿠폰 클릭 시 이동할 PC 웹 링크. 선택 |
| content.carousel.list[].coupon.schemeIos | String | X | 쿠폰 클릭 시 실행할 iOS 앱 링크. 채널 쿠폰 URL(alimtalk=coupon://) 사용 시 schemeAndroid와 함께 하나 이상 필수 |
| content.carousel.list[].coupon.schemeAndroid | String | X | 쿠폰 클릭 시 실행할 안드로이드 앱 링크. 채널 쿠폰 URL(alimtalk=coupon://) 사용 시 schemeIos와 함께 하나 이상 필수 |
| content.carousel.tail | Object | X |  |
| content.carousel.tail.linkMo | String | O | 더보기 버튼 클릭 시 이동할 모바일 웹 링크(http/https). tail 사용 시 필수 |
| content.carousel.tail.linkPc | String | X | 더보기 버튼 클릭 시 이동할 PC 웹 링크. 선택 |
| content.carousel.tail.schemeIos | String | X | 더보기 버튼 클릭 시 실행할 iOS 앱 링크. 선택 |
| content.carousel.tail.schemeAndroid | String | X | 더보기 버튼 클릭 시 실행할 안드로이드 앱 링크. 선택 |
| content.commerce | Object | X |  |
| content.commerce.title | String | O | 상품 제목(최대 30자). 필수 |
| content.commerce.regularPrice | Integer | O | 정상 가격(0~99,999,999). 필수 |
| content.commerce.discountPrice | Integer | X | 할인 후 가격(0~99,999,999). 선택. 사용 시 discountRate 또는 discountFixed 중 하나 필수 |
| content.commerce.discountRate | Integer | X | 할인율(0~100). discountPrice 존재 시 discountFixed와 택1 |
| content.commerce.discountFixed | Integer | X | 정액 할인 가격(0~999,999). discountPrice 존재 시 discountRate와 택1 |
| content.coupon | Object | X |  |
| content.coupon.title | String | O | 쿠폰 제목. 필수. 형식: "{N}원 할인 쿠폰"(N: 1~99,999,999), "{N}% 할인 쿠폰"(N: 1~100), "배송비 할인 쿠폰", "{상품명} 무료 쿠폰"(상품명 최대 7자), "{상품명} UP 쿠폰"(상품명 최대 7자) 중 택1 |
| content.coupon.description | String | O | 쿠폰 상세 설명. 필수. TEXT/IMAGE/COMMERCE: 최대 12자, WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO: 최대 18자 |
| content.coupon.linkMo | String | X | 쿠폰 클릭 시 이동할 모바일 웹 링크(http/https). 채널 쿠폰 URL이 아닌 경우 필수 |
| content.coupon.linkPc | String | X | 쿠폰 클릭 시 이동할 PC 웹 링크. 선택 |
| content.coupon.schemeIos | String | X | 쿠폰 클릭 시 실행할 iOS 앱 링크. 채널 쿠폰 URL(alimtalk=coupon://) 사용 시 schemeAndroid와 함께 하나 이상 필수 |
| content.coupon.schemeAndroid | String | X | 쿠폰 클릭 시 실행할 안드로이드 앱 링크. 채널 쿠폰 URL(alimtalk=coupon://) 사용 시 schemeIos와 함께 하나 이상 필수 |
| content.additionalContent | String | X | 부가 콘텐츠. COMMERCE 타입에서만 사용(선택, 최대 34자). CAROUSEL_COMMERCE는 캐러셀 아이템 내 additionalContent 사용 |
| options | Object | X |  |
| options.audienceType | String | X | 발송 대상 타입. CUSTOMER: 고객, FRIEND: 친구<br>[CUSTOMER, FRIEND] |
| options.targeting | String | X | 메시지 대상 타입. M: 마케팅 수신 동의 유저, N: 친구가 아닌 마케팅 수신 동의 유저, O: 친구인 유저. M/N 사용 시 발신 프로필에 마케팅 수신 동의 활성화 및 080 수신거부 번호 필요<br>[M, N, O] |
| options.pushAlarm | Boolean | X | 메시지 푸시 알람 발송 여부(default: true)<br>기본값: true |
| options.unsubscribePhoneNumber | String | X | 080 무료수신거부 전화번호. targeting이 M/N인 경우 필요. 형식: 080-XXX-XXXX, 080-XXXX-XXXX, 080XXXXXXX, 080XXXXXXXX. 생략 시 발신 프로필에 등록된 값이 자동 적용 |
| options.unsubscribeAuthNumber | String | X | 수신거부 인증번호(숫자, 최대 9자). 필수 아님. unsubscribePhoneNumber 없이 단독 입력 불가. 생략 시 발신 프로필에 등록된 값이 자동 적용 |
| statsKeyId | String | X | 통계 키 아이디 |
| scheduledDateTime | String | X | 예약 발송 시간 |
| confirmBeforeSend | Boolean | X | 확인 후 발송 여부 |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | O | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 자유 양식 메시지 발송 요청 - 브랜드 메시지(BRANDMESSAGE)

POST {{endpoint}}/message/v1.0/BRANDMESSAGE/free-form-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
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
    "chatBubbleType" : "TEXT",
    "adult" : false,
    "content" : null,
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "image" : {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    },
    "video" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailAttachmentId" : "20230131070811m2fDe1rXx80",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    },
    "buttons" : [ {
      "type" : "WL",
      "name" : "버튼명",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123",
      "chatExtra" : "extra_info",
      "chatEvent" : "event_name"
    } ],
    "header" : "헤더",
    "item" : {
      "list" : [ {
        "title" : "아이템 제목",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "carousel" : {
      "head" : {
        "header" : "인트로 헤더",
        "content" : null,
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "additionalContent" : "가격 정보",
        "buttons" : [ {
          "type" : "WL",
          "name" : "버튼명",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android",
          "bizFormKey" : "bizFormKey123",
          "chatExtra" : "extra_info",
          "chatEvent" : "event_name"
        } ],
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg",
          "imageLink" : "https://www.example.com"
        },
        "commerce" : {
          "title" : "상품 제목",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "coupon" : {
          "title" : "5000원 할인 쿠폰",
          "description" : "첫 구매 고객 전용",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "commerce" : {
      "title" : "상품 제목",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "coupon" : {
      "title" : "5000원 할인 쿠폰",
      "description" : "첫 구매 고객 전용",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "additionalContent" : "가격 정보"
  },
  "options" : {
    "audienceType" : "CUSTOMER",
    "targeting" : "M",
    "pushAlarm" : true,
    "unsubscribePhoneNumber" : "0801111234",
    "unsubscribeAuthNumber" : "1234"
  },
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/BRANDMESSAGE/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
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
    "chatBubbleType" : "TEXT",
    "adult" : false,
    "content" : null,
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "image" : {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    },
    "video" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailAttachmentId" : "20230131070811m2fDe1rXx80",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    },
    "buttons" : [ {
      "type" : "WL",
      "name" : "버튼명",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123",
      "chatExtra" : "extra_info",
      "chatEvent" : "event_name"
    } ],
    "header" : "헤더",
    "item" : {
      "list" : [ {
        "title" : "아이템 제목",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "carousel" : {
      "head" : {
        "header" : "인트로 헤더",
        "content" : null,
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "additionalContent" : "가격 정보",
        "buttons" : [ {
          "type" : "WL",
          "name" : "버튼명",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android",
          "bizFormKey" : "bizFormKey123",
          "chatExtra" : "extra_info",
          "chatEvent" : "event_name"
        } ],
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg",
          "imageLink" : "https://www.example.com"
        },
        "commerce" : {
          "title" : "상품 제목",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "coupon" : {
          "title" : "5000원 할인 쿠폰",
          "description" : "첫 구매 고객 전용",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "commerce" : {
      "title" : "상품 제목",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "coupon" : {
      "title" : "5000원 할인 쿠폰",
      "description" : "첫 구매 고객 전용",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "additionalContent" : "가격 정보"
  },
  "options" : {
    "audienceType" : "CUSTOMER",
    "targeting" : "M",
    "pushAlarm" : true,
    "unsubscribePhoneNumber" : "0801111234",
    "unsubscribeAuthNumber" : "1234"
  },
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false
}'
```

</details>

<span id="messageV1x0003EmailFreeFormMessages"></span>

<a id="request-to-send-a-free-form-message---email"></a>

## 자유 양식 메시지 발송 요청 - 이메일(EMAIL)

이메일(EMAIL)에 대한 자유 양식 메시지 발송을 요청합니다.


**요청**

```
POST /message/v1.0/EMAIL/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| messagePurpose | Path | Enum | O | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "EMAIL_ADDRESS",
      "contact" : "recipient@example.com",
      "clientReference" : "1234:abcd:011-asd"
    } ]
  } ],
  "id" : "alpha123",
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
| statsKeyId | String | X | 통계 키 아이디 |
| scheduledDateTime | String | X | 예약 발송 시간 |
| confirmBeforeSend | Boolean | X | 확인 후 발송 여부 |
| sender | Object | X |  |
| sender.senderMailAddress | String | O | 발신 메일 주소 |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 연락처입니다. 수신자를 지정하지 않고 연락처를 직접 입력하여 메시지를 발송할 수 있습니다. |
| recipients[].contacts[].clientReference | String | X | 수신자 별로 부여할 수 있는 사용자 지정 필드 입니다 |
| recipients[].templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| id | String | X | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| content | Object | X |  |
| content.title | String | O | 템플릿 메일 제목 |
| content.body | String | O | 템플릿 메일 본문 |
| content.attachmentIds | Array | X | 템플릿 첨부 파일 ID |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | O | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



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
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "EMAIL_ADDRESS",
      "contact" : "recipient@example.com",
      "clientReference" : "1234:abcd:011-asd"
    } ]
  } ],
  "id" : "alpha123",
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
curl -X POST "${endpoint}/message/v1.0/EMAIL/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "EMAIL_ADDRESS",
      "contact" : "recipient@example.com",
      "clientReference" : "1234:abcd:011-asd"
    } ]
  } ],
  "id" : "alpha123",
  "content" : {
    "title" : "[NHN Cloud Email][##env##] 모니터링 알림",
    "body" : "안녕하세요. 금일 고객님 상품 입고 되었습니다.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>

<span id="messageV1x0004RcsFreeFormMessages"></span>

<a id="request-to-send-a-free-form-message---rcs"></a>

## 자유 양식 메시지 발송 요청 - RCS

RCS에 대한 자유 양식 메시지 발송을 요청합니다.


**요청**

```
POST /message/v1.0/RCS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| messagePurpose | Path | Enum | O | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | X | 통계 키 아이디 |
| scheduledDateTime | String | X | 예약 발송 시간 |
| confirmBeforeSend | Boolean | X | 확인 후 발송 여부 |
| sender | Object | O |  |
| sender.brandId | String | O | 브랜드 아이디 |
| sender.chatbotId | String | O | 대화방(챗봇) 아이디 |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 연락처입니다. 수신자를 지정하지 않고 연락처를 직접 입력하여 메시지를 발송할 수 있습니다. |
| recipients[].contacts[].clientReference | String | X | 수신자 별로 부여할 수 있는 사용자 지정 필드 입니다 |
| recipients[].templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| id | String | X | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| content | Object | X |  |
| content.messageType | String | X | RCS 발송 메시지 유형<br>[SMS(단문 메시지), LMS(장문 메시지), MMS(멀티미디어 메시지), RBC_TEMPLATE(RCS Biz Center 템플릿)] |
| content.title | String | X | (Deprecated, content.cards[].title 사용) 메시지 제목 |
| content.body | String | X | (Deprecated, content.cards[].description 사용) 메시지 본문 |
| content.smsType | String | X | SMS 타입<br>[STANDALONE(독립형), UNIFIED_STANDALONE(통합 독립형)] |
| content.lmsType | String | X | LMS 타입<br>[STANDALONE(독립형), FORMAT_BASIC(기본 형식), FORMAT_TITLE_HIGHLIGHT(제목 강조 형식), FORMAT_PARAGRAPH(문단 형식), UNIFIED_STANDALONE(통합 독립형)] |
| content.mmsType | String | X | MMS 타입(MMS 발송일 경우 필수)<br>[HORIZONTAL(가로형), VERTICAL(세로형), CAROUSEL_MEDIUM(캐러셀 중간형), CAROUSEL_SMALL(캐러셀 소형), UNIFIED_HORIZONTAL(통합 가로형), UNIFIED_VERTICAL(통합 세로형)] |
| content.messagebaseId | String | X | RCS Biz Center 템플릿 아이디 |
| content.unsubscribePhoneNumber | String | X | 수신 거부 번호(광고 발송일 경우 필수) |
| content.cards | Array | X | RCS 카드 |
| content.cards[].title | String | X | 제목 |
| content.cards[].description | String | X | 본문 |
| content.cards[].attachmentId | String | X | 첨부 파일 아이디<br>※ 통합 MMS 카드에서 GIF 이미지를 첨부하면 iOS 기기에서는 수신이 불가능합니다. |
| content.cards[].mTitle | String | X | 메인 타이틀 |
| content.cards[].mTitleMedia | String | X | 메인 타이틀 로고 파일 ID |
| content.cards[].title1 | String | X | 제목 1 |
| content.cards[].title2 | String | X | 제목 2 |
| content.cards[].title3 | String | X | 제목 3 |
| content.cards[].description1 | String | X | 본문 1 |
| content.cards[].description2 | String | X | 본문 2 |
| content.cards[].description3 | String | X | 본문 3 |
| content.cards[].buttons | Array | X | RCS 버튼 리스트 |
| content.cards[].buttons[].buttonType | String | X | COMPOSE(대화방 열기), CLIPBOARD(복사하기), DIALER(전화 걸기), MAP_SHOW(지도 보여주기), MAP_QUERY(지도 검색하기), MAP_SHARE(현재 위치 공유하기), URL(URL 연결하기), CALENDAR(일정 등록하기)<br>※ 통합 메시지 유형에 CLIPBOARD(복사하기) 버튼을 사용하면 iOS 기기에서는 수신이 불가능합니다.<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.cards[].buttons[].buttonJson | Object | X |  |
| content.cards[].buttons[].buttonJson.action | Object | X | 버튼 액션 |
| content.buttons | Array | X | (Deprecated, content.cards[].buttons 사용) RCS 버튼 리스트 |
| content.buttons[].buttonType | String | X | COMPOSE(대화방 열기), CLIPBOARD(복사하기), DIALER(전화 걸기), MAP_SHOW(지도 보여주기), MAP_QUERY(지도 검색하기), MAP_SHARE(현재 위치 공유하기), URL(URL 연결하기), CALENDAR(일정 등록하기)<br>※ 통합 메시지 유형에 CLIPBOARD(복사하기) 버튼을 사용하면 iOS 기기에서는 수신이 불가능합니다.<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | X |  |
| content.buttons[].buttonJson.action | Object | X | 버튼 액션 |
| options | Object | X |  |
| options.expiryOption | Integer | X | 통신사에서 디바이스로 발송 시도하는 시간(1: 1일, 2: 40초, 3: 3분, 4: 1시간)<br>기본값: 1 |
| options.groupId | String | X | RCS Biz Center 통계 연동을 위한 group ID [가이드](../console-guide/send-a-message/#RCS) (최대 20 Byte) |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | O | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



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
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/RCS/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  }
}'
```

</details>

<span id="messageV1x0005PushFreeFormMessages"></span>

<a id="request-to-send-a-free-form-message---push"></a>

## 자유 양식 메시지 발송 요청 - PUSH

PUSH에 대한 자유 양식 메시지 발송을 요청합니다.


**요청**

```
POST /message/v1.0/PUSH/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| messagePurpose | Path | Enum | O | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "TOKEN_FCM",
      "contact" : "TOKEN_FCM",
      "clientReference" : "1234:abcd:011-asd"
    } ]
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
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | X | 통계 키 아이디 |
| scheduledDateTime | String | X | 예약 발송 시간 |
| confirmBeforeSend | Boolean | X | 확인 후 발송 여부 |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 연락처입니다. 수신자를 지정하지 않고 연락처를 직접 입력하여 메시지를 발송할 수 있습니다. |
| recipients[].contacts[].clientReference | String | X | 수신자 별로 부여할 수 있는 사용자 지정 필드 입니다 |
| recipients[].templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| id | String | X | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| content | Object | X | 푸시 메시지 내용 |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | O | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



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
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "TOKEN_FCM",
      "contact" : "TOKEN_FCM",
      "clientReference" : "1234:abcd:011-asd"
    } ]
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
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/PUSH/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "TOKEN_FCM",
      "contact" : "TOKEN_FCM",
      "clientReference" : "1234:abcd:011-asd"
    } ]
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
  }
}'
```

</details>

<span id="messageV1x0006TemplateMessages"></span>

<a id="request-template-message-sending"></a>

## 템플릿 메시지 발송 요청

등록한 템플릿을 이용해 메시지를 발송합니다.<br>
등록한 템플릿이 없을 경우 템플릿을 먼저 등록한 뒤 발송합니다.<br>
<br>
수신 대상 설정은 단건 수신자, 대량 수신자, 그룹 쿼리 중 하나를 선택해 설정해야 합니다.<br>
* 단건 수신자(recipient)<br>
* 대량/그룹 수신자(id)<br>
  <br>
  예약 발송의 경우 'scheduledDateTime'을 설정합니다.<br>
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
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| messageChannel | Path | Enum | O | 메시지 채널입니다. |
| messagePurpose | Path | Enum | O | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  "id" : "alpha123"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | X | 통계 키 아이디 |
| templateId | String | X | 템플릿 ID |
| scheduledDateTime | String | X | 예약 발송 시간 |
| confirmBeforeSend | Boolean | X | 확인 후 발송 여부 |
| templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 연락처입니다. 수신자를 지정하지 않고 연락처를 직접 입력하여 메시지를 발송할 수 있습니다. |
| recipients[].contacts[].clientReference | String | X | 수신자 별로 부여할 수 있는 사용자 지정 필드 입니다 |
| recipients[].templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| id | String | X | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | O | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



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
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  "id" : "alpha123"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/${messageChannel}/template-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  "id" : "alpha123"
}'
```

</details>

<span id="messageV1x0007AlimtalkTemplateMessages"></span>

<a id="send-alimtalk-template-message"></a>

## 알림톡 템플릿 메시지 발송

등록한 템플릿을 이용해 메시지를 발송합니다.<br>
등록한 템플릿이 없을 경우 템플릿을 먼저 등록한 뒤 발송합니다.<br>
<br>
수신 대상 설정은 단건 수신자, 대량 수신자, 그룹 쿼리 중 하나를 선택해 설정해야 합니다.<br>
* 단건 수신자(recipient)<br>
* 대량/그룹 수신자(id)<br>
  <br>
  예약 발송의 경우 'scheduledDateTime'을 설정합니다.<br>
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
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| messagePurpose | Path | Enum | O | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  "id" : "alpha123"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | X | 통계 키 아이디 |
| sender | Object | X |  |
| sender.senderKey | String | O | 발신프로필 발신키 |
| templateId | String | O | 템플릿 ID |
| scheduledDateTime | String | X | 예약 발송 시간 |
| confirmBeforeSend | Boolean | X | 확인 후 발송 여부 |
| templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 연락처입니다. 수신자를 지정하지 않고 연락처를 직접 입력하여 메시지를 발송할 수 있습니다. |
| recipients[].contacts[].clientReference | String | X | 수신자 별로 부여할 수 있는 사용자 지정 필드 입니다 |
| recipients[].templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| id | String | X | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | O | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



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
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  "id" : "alpha123"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/ALIMTALK/template-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  "id" : "alpha123"
}'
```

</details>

<span id="messageV1x0007BrandmessageTemplateMessages"></span>

<a id="send-a-brand-message-template-message"></a>

## 브랜드 메시지 템플릿 메시지 발송

등록한 템플릿을 이용해 브랜드 메시지를 발송합니다.<br>
등록한 템플릿이 없을 경우 템플릿을 먼저 등록한 뒤 발송합니다.<br>
<br>
수신 대상 설정은 단건 수신자, 대량 수신자, 그룹 쿼리 중 하나를 선택해 설정해야 합니다.<br>
* 단건 수신자(recipient)<br>
* 대량/그룹 수신자(id)<br>
  <br>
  예약 발송의 경우 'scheduledDateTime'을 설정합니다.<br>
  확인 후 발송의 경우 'confirmBeforeSend'를 true로 설정합니다.<br>


**요청**

```
POST /message/v1.0/BRANDMESSAGE/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| messagePurpose | Path | Enum | O | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
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
    },
    "imageParameters" : [ {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    } ],
    "videoParameter" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailAttachmentId" : "20230131070811m2fDe1rXx80",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    }
  } ],
  "id" : "alpha123",
  "templateId" : "aA123456",
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "options" : {
    "audienceType" : "CUSTOMER",
    "targeting" : "M",
    "pushAlarm" : true,
    "unsubscribePhoneNumber" : "0801111234",
    "unsubscribeAuthNumber" : "1234"
  },
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| sender | Object | X |  |
| sender.senderKey | String | O | 발신 키(40자). 그룹 발신 키는 사용 불가 |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 연락처입니다. 수신자를 지정하지 않고 연락처를 직접 입력하여 메시지를 발송할 수 있습니다. |
| recipients[].contacts[].clientReference | String | X | 수신자 별로 부여할 수 있는 사용자 지정 필드 입니다 |
| recipients[].templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| recipients[].imageParameters | Array | X | 수신자별 이미지 파라미터. 메시지 레벨의 이미지 파라미터를 오버라이딩합니다. |
| recipients[].imageParameters[].attachmentId | String | X | 첨부 파일 아이디. imageUrl과 택1 |
| recipients[].imageParameters[].imageUrl | String | X | 이미지 URL. attachmentId와 택1 |
| recipients[].imageParameters[].imageLink | String | X | 이미지 클릭 시 이동할 URL(http/https). 선택. 미설정 시 카카오톡 이미지 뷰어 사용 |
| recipients[].videoParameter | Object | X |  |
| recipients[].videoParameter.videoUrl | String | O | 카카오TV 동영상 URL(https://tv.kakao.com/으로 시작). PREMIUM_VIDEO 타입 필수 |
| recipients[].videoParameter.thumbnailAttachmentId | String | X | 썸네일 이미지 첨부 파일 아이디. thumbnailUrl과 택1. 일반 이미지 업로드 API로 등록한 이미지만 사용 가능 |
| recipients[].videoParameter.thumbnailUrl | String | X | 동영상 썸네일 이미지 URL. thumbnailAttachmentId와 택1. 일반 이미지 업로드 API로 등록한 이미지만 사용 가능. 미설정 시 카카오TV 기본 썸네일 사용 |
| id | String | X | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| templateId | String | X | 템플릿 ID |
| templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| options | Object | X |  |
| options.audienceType | String | X | 발송 대상 타입. CUSTOMER: 고객, FRIEND: 친구<br>[CUSTOMER, FRIEND] |
| options.targeting | String | X | 메시지 대상 타입. M: 마케팅 수신 동의 유저, N: 친구가 아닌 마케팅 수신 동의 유저, O: 친구인 유저. M/N 사용 시 발신 프로필에 마케팅 수신 동의 활성화 및 080 수신거부 번호 필요<br>[M, N, O] |
| options.pushAlarm | Boolean | X | 메시지 푸시 알람 발송 여부(default: true)<br>기본값: true |
| options.unsubscribePhoneNumber | String | X | 080 무료수신거부 전화번호. targeting이 M/N인 경우 필요. 형식: 080-XXX-XXXX, 080-XXXX-XXXX, 080XXXXXXX, 080XXXXXXXX. 생략 시 발신 프로필에 등록된 값이 자동 적용 |
| options.unsubscribeAuthNumber | String | X | 수신거부 인증번호(숫자, 최대 9자). 필수 아님. unsubscribePhoneNumber 없이 단독 입력 불가. 생략 시 발신 프로필에 등록된 값이 자동 적용 |
| statsKeyId | String | X | 통계 키 아이디 |
| scheduledDateTime | String | X | 예약 발송 시간 |
| confirmBeforeSend | Boolean | X | 확인 후 발송 여부 |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | O | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 브랜드 메시지 템플릿 메시지 발송

POST {{endpoint}}/message/v1.0/BRANDMESSAGE/template-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
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
    },
    "imageParameters" : [ {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    } ],
    "videoParameter" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailAttachmentId" : "20230131070811m2fDe1rXx80",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    }
  } ],
  "id" : "alpha123",
  "templateId" : "aA123456",
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "options" : {
    "audienceType" : "CUSTOMER",
    "targeting" : "M",
    "pushAlarm" : true,
    "unsubscribePhoneNumber" : "0801111234",
    "unsubscribeAuthNumber" : "1234"
  },
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/BRANDMESSAGE/template-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
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
    },
    "imageParameters" : [ {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    } ],
    "videoParameter" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailAttachmentId" : "20230131070811m2fDe1rXx80",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    }
  } ],
  "id" : "alpha123",
  "templateId" : "aA123456",
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "options" : {
    "audienceType" : "CUSTOMER",
    "targeting" : "M",
    "pushAlarm" : true,
    "unsubscribePhoneNumber" : "0801111234",
    "unsubscribeAuthNumber" : "1234"
  },
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false
}'
```

</details>

<span id="messageV1x0008EmailTemplateMessages"></span>

<a id="send-email-template-message"></a>

## 이메일 템플릿 메시지 발송

등록한 템플릿을 이용해 메시지를 발송합니다.<br>
등록한 템플릿이 없을 경우 템플릿을 먼저 등록한 뒤 발송합니다.<br>
<br>
수신 대상 설정은 단건 수신자, 대량 수신자, 그룹 쿼리 중 하나를 선택해 설정해야 합니다.<br>
* 단건 수신자(recipient)<br>
* 대량/그룹 수신자(id)<br>
  <br>
  예약 발송의 경우 'scheduledDateTime'을 설정합니다.<br>
  확인 후 발송의 경우 'confirmBeforeSend'를 true로 설정합니다.<br>


**요청**

```
POST /message/v1.0/EMAIL/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| messagePurpose | Path | Enum | O | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  "id" : "alpha123"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | X | 통계 키 아이디 |
| templateId | String | X | 템플릿 ID |
| scheduledDateTime | String | X | 예약 발송 시간 |
| confirmBeforeSend | Boolean | X | 확인 후 발송 여부 |
| templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 연락처입니다. 수신자를 지정하지 않고 연락처를 직접 입력하여 메시지를 발송할 수 있습니다. |
| recipients[].contacts[].clientReference | String | X | 수신자 별로 부여할 수 있는 사용자 지정 필드 입니다 |
| recipients[].templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| id | String | X | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | O | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 이메일 템플릿 메시지 발송

POST {{endpoint}}/message/v1.0/EMAIL/template-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  "id" : "alpha123"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/EMAIL/template-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  "id" : "alpha123"
}'
```

</details>

<span id="messageV1x0008RcsTemplateMessages"></span>

<a id="send-rcs-template-message"></a>

## RCS 템플릿 메시지 발송

등록한 템플릿을 이용해 메시지를 발송합니다.<br>
등록한 템플릿이 없을 경우 템플릿을 먼저 등록한 뒤 발송합니다.<br>
<br>
수신 대상 설정은 단건 수신자, 대량 수신자, 그룹 쿼리 중 하나를 선택해 설정해야 합니다.<br>
* 단건 수신자(recipient)<br>
* 대량/그룹 수신자(id)<br>
  <br>
  예약 발송의 경우 'scheduledDateTime'을 설정합니다.<br>
  확인 후 발송의 경우 'confirmBeforeSend'를 true로 설정합니다.<br>


**요청**

```
POST /message/v1.0/RCS/template-messages/{messagePurpose}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| messagePurpose | Path | Enum | O | 메시지 목적입니다. |



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
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | X | 통계 키 아이디 |
| sender | Object | X |  |
| sender.chatbotId | String | X | 대화방(챗봇) 아이디 |
| content | Object | X |  |
| content.unsubscribePhoneNumber | String | X | 수신거부 전화번호 |
| templateId | String | X | 템플릿 ID |
| scheduledDateTime | String | X | 예약 발송 시간 |
| confirmBeforeSend | Boolean | X | 확인 후 발송 여부 |
| templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 연락처입니다. 수신자를 지정하지 않고 연락처를 직접 입력하여 메시지를 발송할 수 있습니다. |
| recipients[].contacts[].clientReference | String | X | 수신자 별로 부여할 수 있는 사용자 지정 필드 입니다 |
| recipients[].templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| id | String | X | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| options | Object | X |  |
| options.expiryOption | Integer | X | 통신사에서 디바이스로 발송 시도하는 시간(1: 1일, 2: 40초, 3: 3분, 4: 1시간)<br>기본값: 1 |
| options.groupId | String | X | RCS Biz Center 통계 연동을 위한 group ID [가이드](../console-guide/send-a-message/#RCS) (최대 20 Byte) |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | O | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



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
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  }
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
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  }
}'
```

</details>

<span id="messageV1x0008SmsTemplateMessages"></span>

<a id="send-sms-template-message"></a>

## SMS 템플릿 메시지 발송

등록한 템플릿을 이용해 메시지를 발송합니다.
등록한 템플릿이 없을 경우 템플릿을 먼저 등록한 뒤 발송합니다.

수신 대상 설정은 단건 수신자, 대량 수신자, 그룹 쿼리 중 하나를 선택해 설정해야 합니다.
* 단건 수신자(recipient)
* 대량/그룹 수신자(id)

예약 발송의 경우 'scheduledDateTime'을 설정합니다.
확인 후 발송의 경우 'confirmBeforeSend'를 true로 설정합니다.

이미지 레이아웃이 연동된 MMS 템플릿 발송 시 다음 사항을 유의해야 합니다.
* **필수 템플릿 파라미터**: cardNumber, scratchNumber를 반드시 포함해야 합니다.
  * cardNumber: 바코드 생성에 사용되며, 반드시 16자리 숫자로 구성되어야 합니다.
  * scratchNumber: 별도 제약 조건이 없습니다.
* **이미지 레이아웃 Override**: 요청 본문에 content.imageLayoutId 또는 content.imageLayoutName을 포함하여 템플릿에 설정된 이미지 레이아웃을 변경할 수 있습니다.
  * content.imageLayoutId와 content.imageLayoutName 중 하나만 사용해야 합니다.
  * 두 필드 모두 포함되지 않으면 템플릿 생성 시 연동한 기본 이미지 레이아웃이 사용됩니다.


**요청**

```
POST /message/v1.0/SMS/template-messages/{messagePurpose}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| messagePurpose | Path | Enum | O | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "content" : {
    "imageLayoutId" : "aA123456",
    "imageLayoutName" : "2025-프로모션-레이아웃"
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
  "id" : "alpha123"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | X | 통계 키 아이디 |
| templateId | String | X | 템플릿 ID |
| scheduledDateTime | String | X | 예약 발송 시간 |
| confirmBeforeSend | Boolean | X | 확인 후 발송 여부 |
| templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| content | Object | X |  |
| content.imageLayoutId | String | X | 이미지 레이아웃 아이디 |
| content.imageLayoutName | String | X | 이미지 레이아웃 이름 |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 연락처입니다. 수신자를 지정하지 않고 연락처를 직접 입력하여 메시지를 발송할 수 있습니다. |
| recipients[].contacts[].clientReference | String | X | 수신자 별로 부여할 수 있는 사용자 지정 필드 입니다 |
| recipients[].templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| id | String | X | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | O | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMS 템플릿 메시지 발송

POST {{endpoint}}/message/v1.0/SMS/template-messages/{{messagePurpose}}
{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "content" : {
    "imageLayoutId" : "aA123456",
    "imageLayoutName" : "2025-프로모션-레이아웃"
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
  "id" : "alpha123"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/SMS/template-messages/${messagePurpose}" \
-d '{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "content" : {
    "imageLayoutId" : "aA123456",
    "imageLayoutName" : "2025-프로모션-레이아웃"
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
  "id" : "alpha123"
}'
```

</details>

<span id="messageV1x0009FlowMessages"></span>

<a id="send-flow-message"></a>

## 플로우 메시지 발송

등록한 플로우를 이용해 메시지를 발송합니다.<br>
플로우를 등록하지 않았다면, 플로우를 등록하고 발송해야 합니다.<br>
<br>
수신 대상 설정은 단건 수신자, 대량 수신자, 그룹 쿼리 중 하나를 선택해 설정해야 합니다.<br>
* 단건 수신자(recipient)<br>
* 대량/그룹 수신자(id)<br>
  <br>
  예약 발송의 경우 'scheduledDateTime'을 설정합니다.<br>
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
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| messagePurpose | Path | Enum | O | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "flowId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | X | 통계 키 아이디 |
| flowId | String | X | 플로우 ID |
| scheduledDateTime | String | X | 예약 발송 시간 |
| confirmBeforeSend | Boolean | X | 확인 후 발송 여부 |
| templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 연락처입니다. 수신자를 지정하지 않고 연락처를 직접 입력하여 메시지를 발송할 수 있습니다. |
| recipients[].contacts[].clientReference | String | X | 수신자 별로 부여할 수 있는 사용자 지정 필드 입니다 |
| recipients[].templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| id | String | X | 대량 수신자 목록 및 파일 업로드 성공 시 생성되는 아이디 |
| flow | Object | X |  |
| flow.steps | Array | O |  |
| flow.steps[].messageChannel | String | O | 메시지 채널<br>[SMS(SMS), ALIMTALK(알림톡), EMAIL(이메일), RCS(RCS), PUSH(푸시)] |
| flow.steps[].sender | Object | X | 발신자 정보입니다. 발신자 정보는 메시지 채널에 따라 다르게 구성될 수 있습니다.<br> |
| flow.steps[].content | Object | X | 메시지 내용입니다. 메시지 내용은 메시지 채널에 따라 다르게 구성될 수 있습니다.<br> |
| flow.steps[].options | Object | X | 발송 옵션입니다. 발송 옵션은 메시지 채널에 따라 다르게 구성될 수 있습니다.<br> |
| flow.steps[].nextSteps | Array | X | 다음 단계입니다. 다음 단계가 없는 경우, 메시지 발송이 종료됩니다.<br> |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | O | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



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
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/flow-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "flowId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  }
}'
```

</details>

<span id="messageV1x0010InstantFlowMessages"></span>

<a id="send-an-instant-flow-message"></a>

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
| messagePurpose | Path | Enum | O | 메시지 목적입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
      "templateId" : "Tj3nE8dq",
      "nextSteps" : [ ]
    } ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| statsKeyId | String | X | 통계 키 아이디 |
| scheduledDateTime | String | X | 예약 발송 시간 |
| confirmBeforeSend | Boolean | X | 확인 후 발송 여부 |
| templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| recipients | Array | O |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 연락처 타입<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 연락처입니다. 수신자를 지정하지 않고 연락처를 직접 입력하여 메시지를 발송할 수 있습니다. |
| recipients[].contacts[].clientReference | String | X | 수신자 별로 부여할 수 있는 사용자 지정 필드 입니다 |
| recipients[].templateParameters | Object | X | 템플릿 파라미터입니다. 키(Key, 치환자)와 값(Value)의 쌍으로 구성되어 있습니다.<br><br>그룹 발송에서는 수신자별 템플릿 파라미터를 지정할 수 없습니다.<br><br>수신자에 설정되는 템플릿 파라미터는 메시지 템플릿 파라미터보다 우선시됩니다.<br><br> |
| instantFlow | Object | O |  |
| instantFlow.steps | Array | O |  |
| instantFlow.steps[].messageChannel | String | O | 메시지 채널<br>[SMS(SMS), ALIMTALK(알림톡), EMAIL(이메일), RCS(RCS), PUSH(푸시)] |
| instantFlow.steps[].sender | Object | X | 발신자 정보입니다. 발신자 정보는 메시지 채널에 따라 다르게 구성될 수 있습니다.<br> |
| instantFlow.steps[].content | Object | X | 메시지 내용입니다. 메시지 내용은 메시지 채널에 따라 다르게 구성될 수 있습니다.<br> |
| instantFlow.steps[].options | Object | X | 발송 옵션입니다. 발송 옵션은 메시지 채널에 따라 다르게 구성될 수 있습니다.<br> |
| instantFlow.steps[].templateId | String | X | 템플릿 아이디입니다. 템플릿 아이디를 설정한 경우, 요청 시 발신자 정보(sender)와 메시지 내용(content)가 적용되지 않습니다.<br>인스턴트 플로우 메시지에서 템플릿 아이디를 설정하지 않는 경우, 발신자 정보(sender)와 메시지 내용(content)이 반드시 필요합니다.<br> |
| instantFlow.steps[].nextSteps | Array | X | 다음 단계입니다. 다음 단계가 없는 경우, 메시지 발송이 종료됩니다.<br> |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| messageId | String | O | 메시지 아이디입니다. 메시지 발송 요청을 받으면 생성되는 값입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 인스턴트 플로우 메시지 발송

POST {{endpoint}}/message/v1.0/instant-flow-messages/{{messagePurpose}}
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
      "templateId" : "Tj3nE8dq",
      "nextSteps" : [ ]
    } ]
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/instant-flow-messages/${messagePurpose}" \
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
      "templateId" : "Tj3nE8dq",
      "nextSteps" : [ ]
    } ]
  }
}'
```

</details>

<span id="messageV1x0100MessageIdDoCancel"></span>

<a id="cancel-sending-message"></a>

## 메시지 발송 취소

발송 취소할 메시지 아이디를 입력해 발송 취소합니다.<br>
메시지 발송 시 응답 받은 메시지 아이디를 이용해 발송을 취소할 수 있습니다.<br>
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
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| messageId | Path | String | O |  |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="messageV1x0101MessageIdDoConfirm"></span>

<a id="confirm-message-delivery"></a>

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
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| messageId | Path | String | O |  |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

