<!-- pre-align:aligned sig=65b610526e63 -->

<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>Message</h1>

**Notification > Notification Hub > API v1.0 User Guide > Message**



<span id="messageV1x0001SmsFreeFormMessages"></span>

## Free-Form Message Sending Request - SMS

Requests a free-form message sending for SMS. Enter the message content in the request body and then request sending.

In order to send messages to each message channel, the sender information for each message channel must be registered. You can register the sender information in the **Notification Hub console** > **Sender Information** tab. For a detailed description of sender information for message channels, see **Notification** > **Notification Hub** > **Guide to Usage Policies and Preparations**.


**Request**

```
POST /message/v1.0/SMS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | App key |
| X-NHN-Authorization | Header | String | O | Access token |
| messagePurpose | Path | Enum | O | Message purpose |



**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


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
    "title" : "Holiday hours notice",
    "body" : "Hello. Your ordered product has arrived today. Please come visit us^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | X | Statistics key ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| sender | Object | X |  |
| sender.senderPhoneNumber | String | O | Sender phone number |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | Contact type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | Contact. You can send a message by entering a contact directly without specifying a recipient. |
| recipients[].contacts[].clientReference | String | X | A custom field that can be assigned per recipient |
| recipients[].templateParameters | Object | X | Template parameters. Consists of key-value pairs where the key is a placeholder.<br><br>In group sending, template parameters cannot be specified per recipient.<br><br>Template parameters set on a recipient take precedence over message template parameters.<br><br> |
| id | String | X | ID generated when a bulk recipient list or file upload succeeds |
| content | Object | X |  |
| content.messageType | String | O | Message type to send (SMS, LMS, MMS)<br>[SMS (short message), LMS (long message), MMS (multimedia message)] |
| content.title | String | X | Message title |
| content.body | String | O | Message body |
| content.attachmentIds | Array | X | Up to 3 attachment IDs |

* The **sender** and **content** fields have different formats depending on the message channel.
* The values that can be entered in the **recipients[].contact.contactType** and **recipients[].contact.contact** fields vary depending on the message channel.
* For scheduled sending, set **scheduledDateTime**. Scheduled dispatches can be canceled before the dispatch starts. You can cancel the request by calling the cancel request API or from the **Notification Hub console** > **Delivery Result**.
* For post-approval sending, set **confirmBeforeSend** to **true**. After approval, sender messages will be sent when you approve them in the **Notification Hub console** > **Delivery Result**.
* Scheduled sending and post-approval sending cannot be configured at the same time.

<a id="sender-fields-by-message-channel"></a>

### Sender Fields by Message Channel

| Message Channel | Field | Description |
| --- | --- | --- |
| SMS | sender.senderPhoneNumber | Sender phone number |
| RCS | sender.brandId | Brand ID |
| RCS | sender.chatbotId | Chatbot ID |
| EMAIL | sender.senderMailAddress | Sender email address |
| ALIMTALK | sender.senderKey | Sender key |
| ALIMTALK | sender.senderProfileType | Sender profile type<br>GROUP, NORMAL |

* AlimTalk (ALIMTALK) requires a sender key (senderKey) and sender profile type (senderProfileType) to be entered.
* AlimTalk (ALIMTALK) requires a template when sending messages. Free-form message sending is not supported.
* Sender profile types are **GROUP** and **NORMAL**. **GROUP** is a group sender profile, and **NORMAL** is a standard sender profile.


**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| messageId | String | O | Message ID. A value generated when a message sending request is received. |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Free-form message sending request - SMS

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
    "title" : "Holiday hours notice",
    "body" : "Hello. Your ordered product has arrived today. Please come visit us^^",
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
    "title" : "Holiday hours notice",
    "body" : "Hello. Your ordered product has arrived today. Please come visit us^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>

<span id="messageV1x0002BrandmessageFreeFormMessages"></span>

## Free-Form Message Sending Request - Brand Message (BRANDMESSAGE)

Requests free-form message sending for Brand Message (BRANDMESSAGE).

Brand Message is an upgraded version of KakaoTalk Friend Talk that supports a wider variety of message types than the standard Friend Talk.
- TEXT: Text type
- IMAGE: Image type
- WIDE_IMAGE: Wide image type
- WIDE_ITEM_LIST: Wide item list type
- CAROUSEL_FEED: Carousel feed type
- CAROUSEL_COMMERCE: Carousel commerce type
- COMMERCE: Commerce type
- PREMIUM_VIDEO: Premium video type

**Request**

```
POST /message/v1.0/BRANDMESSAGE/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| messagePurpose | Path | Enum | O | Message purpose. |

**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->

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
      "name" : "Button name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123",
      "chatExtra" : "extra_info",
      "chatEvent" : "event_name"
    } ],
    "header" : "Header",
    "item" : {
      "list" : [ {
        "title" : "Item title",
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
        "header" : "Intro header",
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
        "additionalContent" : "Price information",
        "buttons" : [ {
          "type" : "WL",
          "name" : "Button name",
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
          "title" : "Product title",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "coupon" : {
          "title" : "5000 won discount coupon",
          "description" : "For first-time customers only",
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
      "title" : "Product title",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "coupon" : {
      "title" : "5000 won discount coupon",
      "description" : "For first-time customers only",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "additionalContent" : "Price information"
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

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| sender | Object | X |  |
| sender.senderKey | String | O | Sender key (40 characters). Group sender keys are not supported. |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | Contact type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | Contact. You can send a message by entering a contact directly without specifying a recipient. |
| recipients[].contacts[].clientReference | String | X | A custom field that can be assigned per recipient. |
| recipients[].templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>In group sending, template parameters cannot be specified per recipient.<br><br>Template parameters set on a recipient take precedence over message template parameters.<br><br> |
| id | String | X | ID generated when a bulk recipient list or file upload is successful. |
| content | Object | X |  |
| content.chatBubbleType | String | X | Message chat bubble type. TEXT: plain text, IMAGE: image, WIDE: wide image, WIDE_ITEM_LIST: wide item list, CAROUSEL_FEED: carousel feed, CAROUSEL_COMMERCE: carousel commerce, COMMERCE: commerce, PREMIUM_VIDEO: premium video<br>[TEXT, IMAGE, WIDE, WIDE_ITEM_LIST, CAROUSEL_FEED, CAROUSEL_COMMERCE, COMMERCE, PREMIUM_VIDEO] |
| content.adult | Boolean | X | Whether the message is for adults (default: false). When set to adult, only recipients who have completed adult verification can view it.<br>Default: false |
| content.content | String | X | Message body. TEXT: required (up to 1,300 characters, up to 99 line breaks), IMAGE: required (up to 1,300 characters), WIDE: required (up to 76 characters, up to 5 line breaks), PREMIUM_VIDEO: optional (up to 76 characters, up to 5 line breaks). Not available for WIDE_ITEM_LIST/CAROUSEL_FEED/CAROUSEL_COMMERCE. URLs can be entered. |
| content.attachmentId | String | X | Attachment ID. IMAGE/WIDE: either attachmentId or image.imageUrl is required. |
| content.image | Object | X |  |
| content.image.attachmentId | String | X | Attachment ID. Use either this or imageUrl. |
| content.image.imageUrl | String | X | Image URL. Use either this or attachmentId. |
| content.image.imageLink | String | X | URL to navigate to when the image is clicked (http/https). Optional. If not set, the KakaoTalk image viewer is used. |
| content.video | Object | X |  |
| content.video.videoUrl | String | O | KakaoTV video URL (must begin with https://tv.kakao.com/). Required for the PREMIUM_VIDEO type. |
| content.video.thumbnailAttachmentId | String | X | Thumbnail image attachment ID. Use either this or thumbnailUrl. Only images registered via the standard image upload API can be used. |
| content.video.thumbnailUrl | String | X | Video thumbnail image URL. Use either this or thumbnailAttachmentId. Only images registered via the standard image upload API can be used. If not set, the default KakaoTV thumbnail is used. |
| content.buttons | Array | X | List of message buttons. TEXT/IMAGE: up to 5 (up to 4 when a coupon is applied), WIDE/WIDE_ITEM_LIST: up to 2, PREMIUM_VIDEO: up to 1, COMMERCE: required (at least 1, up to 2). For CAROUSEL_FEED/CAROUSEL_COMMERCE, use attachment.buttons inside the carousel item. |
| content.buttons[].type | String | O | Button type. WL: Web Link, AL: App Link, BK: Bot Keyword, MD: Message Delivery, BC: Bot for Consultation, BT: Bot Transfer, BF: Business Form, AC: Add Channel<br>[WL, AL, BK, MD, BC, BT, BF, AC] |
| content.buttons[].name | String | X | Button name. TEXT/IMAGE: up to 14 characters, others: up to 8 characters. AC type: send without a value. BF type: choose one of "설문 참여하기", "신청하기", or "응모하기". |
| content.buttons[].linkMo | String | X | Mobile web link (http/https). Required for the WL type; optional for the AL type (required when entered together with schemeIos or schemeAndroid). |
| content.buttons[].linkPc | String | X | PC web link (http/https). Optional for WL/AL types. |
| content.buttons[].schemeIos | String | X | iOS app link. AL type: at least 2 of linkMo, schemeAndroid, and schemeIos are required. |
| content.buttons[].schemeAndroid | String | X | Android app link. AL type: at least 2 of linkMo, schemeAndroid, and schemeIos are required. |
| content.buttons[].bizFormKey | String | X | Business form key. Required for the BF type. |
| content.buttons[].chatExtra | String | X | Meta information for BC (Bot for Consultation) and BT (Bot Transfer) type buttons. |
| content.buttons[].chatEvent | String | X | Bot event name for BT (Bot Transfer) type buttons. |
| content.header | String | X | Message title. WIDE_ITEM_LIST: required (up to 20 characters), PREMIUM_VIDEO: optional (up to 20 characters). Not available for other types. |
| content.item | Object | X |  |
| content.item.list | Array | O | Item list. Minimum 3 items, maximum 4 items. |
| content.item.list[].title | String | X | Item title (up to 1 line break). First item: optional (up to 25 characters), items 2–4: required (up to 30 characters). |
| content.item.list[].image | Object | O |  |
| content.item.list[].image.attachmentId | String | X | Attachment ID. Use either this or imageUrl. |
| content.item.list[].image.imageUrl | String | X | Image URL. Use either this or attachmentId. |
| content.item.list[].linkMo | String | O | Mobile web link to navigate to when the item is clicked (http/https). Required. |
| content.item.list[].linkPc | String | X | PC web link to navigate to when the item is clicked (http/https). Optional. |
| content.item.list[].schemeIos | String | X | iOS app link to launch when the item is clicked. Optional. |
| content.item.list[].schemeAndroid | String | X | Android app link to launch when the item is clicked. Optional. |
| content.carousel | Object | X |  |
| content.carousel.head | Object | X |  |
| content.carousel.head.header | String | O | Intro header. Required when using head (up to 20 characters). |
| content.carousel.head.content | String | O | Intro content. Required when using head (up to 50 characters). |
| content.carousel.head.image | Object | O |  |
| content.carousel.head.image.attachmentId | String | X | Attachment ID. Use either this or imageUrl. |
| content.carousel.head.image.imageUrl | String | X | Image URL. Use either this or attachmentId. |
| content.carousel.head.linkMo | String | X | Mobile web link to navigate to when the intro is clicked. Required when any other link (linkPc/schemeIos/schemeAndroid) is entered. |
| content.carousel.head.linkPc | String | X | PC web link to navigate to when the intro is clicked. Optional. |
| content.carousel.head.schemeIos | String | X | iOS app link to launch when the intro is clicked. Optional. |
| content.carousel.head.schemeAndroid | String | X | Android app link to launch when the intro is clicked. Optional. |
| content.carousel.list | Array | O | List of carousel items. 1–5 items when head is used; 2–6 items when head is not used. |
| content.carousel.list[].header | String | X | Carousel item title. CAROUSEL_FEED: required (up to 20 characters). Not available for CAROUSEL_COMMERCE. |
| content.carousel.list[].message | String | X | Carousel item message. CAROUSEL_FEED: required (up to 180 characters). Not available for CAROUSEL_COMMERCE. |
| content.carousel.list[].additionalContent | String | X | Additional content. CAROUSEL_COMMERCE: optional (up to 34 characters). Not available for CAROUSEL_FEED. |
| content.carousel.list[].buttons | Array | O | Carousel item buttons. At least 1, up to 2 required. The AC button must be placed last. |
| content.carousel.list[].buttons[].type | String | O | Button type. WL: Web Link, AL: App Link, BK: Bot Keyword, MD: Message Delivery, BC: Bot for Consultation, BT: Bot Transfer, BF: Business Form, AC: Add Channel<br>[WL, AL, BK, MD, BC, BT, BF, AC] |
| content.carousel.list[].buttons[].name | String | X | Button name. TEXT/IMAGE: up to 14 characters, others: up to 8 characters. AC type: send without a value. BF type: choose one of "설문 참여하기", "신청하기", or "응모하기". |
| content.carousel.list[].buttons[].linkMo | String | X | Mobile web link (http/https). Required for the WL type; optional for the AL type (required when entered together with schemeIos or schemeAndroid). |
| content.carousel.list[].buttons[].linkPc | String | X | PC web link (http/https). Optional for WL/AL types. |
| content.carousel.list[].buttons[].schemeIos | String | X | iOS app link. AL type: at least 2 of linkMo, schemeAndroid, and schemeIos are required. |
| content.carousel.list[].buttons[].schemeAndroid | String | X | Android app link. AL type: at least 2 of linkMo, schemeAndroid, and schemeIos are required. |
| content.carousel.list[].buttons[].bizFormKey | String | X | Business form key. Required for the BF type. |
| content.carousel.list[].buttons[].chatExtra | String | X | Meta information for BC (Bot for Consultation) and BT (Bot Transfer) type buttons. |
| content.carousel.list[].buttons[].chatEvent | String | X | Bot event name for BT (Bot Transfer) type buttons. |
| content.carousel.list[].image | Object | O |  |
| content.carousel.list[].image.attachmentId | String | X | Attachment ID. Use either this or imageUrl. |
| content.carousel.list[].image.imageUrl | String | X | Image URL. Use either this or attachmentId. |
| content.carousel.list[].image.imageLink | String | X | URL to navigate to when the image is clicked (http/https). Optional. If not set, the KakaoTalk image viewer is used. |
| content.carousel.list[].commerce | Object | X |  |
| content.carousel.list[].commerce.title | String | O | Product title (up to 30 characters). Required. |
| content.carousel.list[].commerce.regularPrice | Integer | O | Regular price (0–99,999,999). Required. |
| content.carousel.list[].commerce.discountPrice | Integer | X | Discounted price (0–99,999,999). Optional. If used, either discountRate or discountFixed is required. |
| content.carousel.list[].commerce.discountRate | Integer | X | Discount rate (0–100). If discountPrice is set, use either this or discountFixed. |
| content.carousel.list[].commerce.discountFixed | Integer | X | Fixed discount amount (0–999,999). If discountPrice is set, use either this or discountRate. |
| content.carousel.list[].coupon | Object | X |  |
| content.carousel.list[].coupon.title | String | O | Coupon title. Required. Choose one of the following formats: "{N}KRW off coupon" (N: 1–99,999,999), "{N}% off coupon" (N: 1–100), "Shipping discount coupon", "{product name} Free coupon" (product name up to 7 characters), or "{product name} UP coupon" (product name up to 7 characters). |
| content.carousel.list[].coupon.description | String | O | Coupon description. Required. Up to 12 characters for TEXT/IMAGE/COMMERCE; up to 18 characters for WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO. |
| content.carousel.list[].coupon.linkMo | String | X | Mobile web link to navigate to when the coupon is clicked (http/https). Required if not using a channel coupon URL. |
| content.carousel.list[].coupon.linkPc | String | X | PC web link to navigate to when the coupon is clicked. Optional. |
| content.carousel.list[].coupon.schemeIos | String | X | iOS app link to launch when the coupon is clicked. At least one of schemeIos or schemeAndroid is required when using a channel coupon URL (alimtalk=coupon://). |
| content.carousel.list[].coupon.schemeAndroid | String | X | Android app link to launch when the coupon is clicked. At least one of schemeAndroid or schemeIos is required when using a channel coupon URL (alimtalk=coupon://). |
| content.carousel.tail | Object | X |  |
| content.carousel.tail.linkMo | String | O | Mobile web link to navigate to when the More button is clicked (http/https). Required when using tail. |
| content.carousel.tail.linkPc | String | X | PC web link to navigate to when the More button is clicked. Optional. |
| content.carousel.tail.schemeIos | String | X | iOS app link to launch when the More button is clicked. Optional. |
| content.carousel.tail.schemeAndroid | String | X | Android app link to launch when the More button is clicked. Optional. |
| content.commerce | Object | X |  |
| content.commerce.title | String | O | Product title (up to 30 characters). Required. |
| content.commerce.regularPrice | Integer | O | Regular price (0–99,999,999). Required. |
| content.commerce.discountPrice | Integer | X | Discounted price (0–99,999,999). Optional. If used, either discountRate or discountFixed is required. |
| content.commerce.discountRate | Integer | X | Discount rate (0–100). If discountPrice is set, use either this or discountFixed. |
| content.commerce.discountFixed | Integer | X | Fixed discount amount (0–999,999). If discountPrice is set, use either this or discountRate. |
| content.coupon | Object | X |  |
| content.coupon.title | String | O | Coupon title. Required. Choose one of the following formats: "{N}KRW off coupon" (N: 1–99,999,999), "{N}% off coupon" (N: 1–100), "Shipping discount coupon", "{product name} Free coupon" (product name up to 7 characters), or "{product name} UP coupon" (product name up to 7 characters). |
| content.coupon.description | String | O | Coupon description. Required. Up to 12 characters for TEXT/IMAGE/COMMERCE; up to 18 characters for WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO. |
| content.coupon.linkMo | String | X | Mobile web link to navigate to when the coupon is clicked (http/https). Required if not using a channel coupon URL. |
| content.coupon.linkPc | String | X | PC web link to navigate to when the coupon is clicked. Optional. |
| content.coupon.schemeIos | String | X | iOS app link to launch when the coupon is clicked. At least one of schemeIos or schemeAndroid is required when using a channel coupon URL (alimtalk=coupon://). |
| content.coupon.schemeAndroid | String | X | Android app link to launch when the coupon is clicked. At least one of schemeAndroid or schemeIos is required when using a channel coupon URL (alimtalk=coupon://). |
| content.additionalContent | String | X | Additional content. Available only for the COMMERCE type (optional, up to 34 characters). For CAROUSEL_COMMERCE, use additionalContent inside the carousel item. |
| options | Object | X |  |
| options.audienceType | String | X | Sending target type. CUSTOMER: customer, FRIEND: friend<br>[CUSTOMER, FRIEND] |
| options.targeting | String | X | Message target type. M: users who agreed to receive marketing messages, N: non-friend users who agreed to receive marketing messages, O: friend users. Using M/N requires the sending profile to have marketing consent enabled and an 080 opt-out number registered.<br>[M, N, O] |
| options.pushAlarm | Boolean | X | Whether to send a push notification for the message (default: true)<br>Default: true |
| options.unsubscribePhoneNumber | String | X | 080 toll-free opt-out phone number. Required when targeting is M/N. Formats: 080-XXX-XXXX, 080-XXXX-XXXX, 080XXXXXXX, 080XXXXXXXX. If omitted, the value registered in the sending profile is applied automatically. |
| options.unsubscribeAuthNumber | String | X | Opt-out authentication number (numeric, up to 9 characters). Not required. Cannot be entered alone without unsubscribePhoneNumber. If omitted, the value registered in the sending profile is applied automatically. |
| statsKeyId | String | X | Statistics key ID. |
| scheduledDateTime | String | X | Scheduled send time. |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation. |

**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| messageId | String | O | Message ID. This value is generated when a message delivery request is received. |

**Request Example**

<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http

### Free-form message sending request - Brand Message (BRANDMESSAGE)

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
      "name" : "Button name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123",
      "chatExtra" : "extra_info",
      "chatEvent" : "event_name"
    } ],
    "header" : "Header",
    "item" : {
      "list" : [ {
        "title" : "Item title",
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
        "header" : "Intro header",
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
        "additionalContent" : "Price information",
        "buttons" : [ {
          "type" : "WL",
          "name" : "Button name",
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
          "title" : "Product title",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "coupon" : {
          "title" : "5000 won discount coupon",
          "description" : "For first-time customers only",
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
      "title" : "Product title",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "coupon" : {
      "title" : "5000 won discount coupon",
      "description" : "For first-time customers only",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "additionalContent" : "Price information"
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
      "name" : "Button name",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123",
      "chatExtra" : "extra_info",
      "chatEvent" : "event_name"
    } ],
    "header" : "Header",
    "item" : {
      "list" : [ {
        "title" : "Item title",
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
        "header" : "Intro header",
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
        "additionalContent" : "Price information",
        "buttons" : [ {
          "type" : "WL",
          "name" : "Button name",
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
          "title" : "Product title",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "coupon" : {
          "title" : "5000 won discount coupon",
          "description" : "For first-time customers only",
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
      "title" : "Product title",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "coupon" : {
      "title" : "5000 won discount coupon",
      "description" : "For first-time customers only",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "additionalContent" : "Price information"
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

## Free-form message sending request - Email (EMAIL)

Requests free-form message sending for Email (EMAIL).


**Request**

```
POST /message/v1.0/EMAIL/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| messagePurpose | Path | Enum | O | Message purpose |



**Request body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


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
    "title" : "[NHN Cloud Email][##env##] Monitoring notification",
    "body" : "Hello. Your ordered product has arrived today.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | X | Statistics key ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| sender | Object | X |  |
| sender.senderMailAddress | String | O | Sender mail address |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | Contact type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | Contact. You can send a message by entering a contact directly without specifying a recipient. |
| recipients[].contacts[].clientReference | String | X | A user-defined field that can be assigned per recipient |
| recipients[].templateParameters | Object | X | Template parameters. Consists of key-value pairs where the key is a placeholder.<br><br>Template parameters cannot be specified per recipient in group sending.<br><br>Template parameters set on a recipient take precedence over message template parameters.<br><br> |
| id | String | X | ID generated upon successful bulk recipient list and file upload |
| content | Object | X |  |
| content.title | String | O | Template mail subject |
| content.body | String | O | Template mail body |
| content.attachmentIds | Array | X | Template attachment file IDs |



**Response body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| messageId | String | O | Message ID. A value generated when a message sending request is received. |



**Request examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Free-form message sending request - Email (EMAIL)

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
    "title" : "[NHN Cloud Email][##env##] Monitoring notification",
    "body" : "Hello. Your ordered product has arrived today.",
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
    "title" : "[NHN Cloud Email][##env##] Monitoring notification",
    "body" : "Hello. Your ordered product has arrived today.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>

<span id="messageV1x0004RcsFreeFormMessages"></span>

<a id="request-to-send-a-free-form-message---rcs"></a>

## Free-Form Message Sending Request - RCS

Requests free-form message sending for RCS.


**Request**

```
POST /message/v1.0/RCS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| messagePurpose | Path | Enum | O | Message purpose |



**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


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
    "title" : "Holiday hours notice",
    "body" : "Hello. Your order has arrived today. Please come visit us^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "Title",
      "description" : "Body",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "Main title",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "Title 1",
      "title2" : "Title 2",
      "title3" : "Title 3",
      "description1" : "Body 1",
      "description2" : "Body 2",
      "description3" : "Body 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "Add event",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "Event title",
                "description" : "Event description"
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
          "displayText" : "Add event",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "Event title",
              "description" : "Event description"
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

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | X | Statistics key ID |
| scheduledDateTime | String | X | Scheduled send time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| sender | Object | O |  |
| sender.brandId | String | O | Brand ID |
| sender.chatbotId | String | O | Chat room (chatbot) ID |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | Contact type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | Contact. You can send a message by entering a contact directly without specifying a recipient. |
| recipients[].contacts[].clientReference | String | X | A custom field that can be assigned per recipient |
| recipients[].templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>Template parameters cannot be specified per recipient in group sending.<br><br>Template parameters set on a recipient take precedence over message template parameters.<br><br> |
| id | String | X | ID generated when a bulk recipient list and file upload succeeds |
| content | Object | X |  |
| content.messageType | String | X | RCS message type<br>[SMS (short message), LMS (long message), MMS (multimedia message), RBC_TEMPLATE (RCS Biz Center template)] |
| content.title | String | X | (Deprecated, use content.cards[].title) Message title |
| content.body | String | X | (Deprecated, use content.cards[].description) Message body |
| content.smsType | String | X | SMS type<br>[STANDALONE, UNIFIED_STANDALONE] |
| content.lmsType | String | X | LMS type<br>[STANDALONE, FORMAT_BASIC, FORMAT_TITLE_HIGHLIGHT, FORMAT_PARAGRAPH, UNIFIED_STANDALONE] |
| content.mmsType | String | X | MMS type (required when sending MMS)<br>[HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL, UNIFIED_HORIZONTAL, UNIFIED_VERTICAL] |
| content.messagebaseId | String | X | RCS Biz Center template ID |
| content.unsubscribePhoneNumber | String | X | Opt-out number (required when sending advertising messages) |
| content.cards | Array | X | RCS cards |
| content.cards[].title | String | X | Title |
| content.cards[].description | String | X | Body |
| content.cards[].attachmentId | String | X | Attachment file ID<br>※ Attaching a GIF image to a unified MMS card is not supported on iOS devices. |
| content.cards[].mTitle | String | X | Main title |
| content.cards[].mTitleMedia | String | X | Main title logo file ID |
| content.cards[].title1 | String | X | Title 1 |
| content.cards[].title2 | String | X | Title 2 |
| content.cards[].title3 | String | X | Title 3 |
| content.cards[].description1 | String | X | Body 1 |
| content.cards[].description2 | String | X | Body 2 |
| content.cards[].description3 | String | X | Body 3 |
| content.cards[].buttons | Array | X | RCS button list |
| content.cards[].buttons[].buttonType | String | X | COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make a call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share current location), URL (link to URL), CALENDAR (add event)<br>※ Using the CLIPBOARD (copy) button with unified message types is not supported on iOS devices.<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.cards[].buttons[].buttonJson | Object | X |  |
| content.cards[].buttons[].buttonJson.action | Object | X | Button action |
| content.buttons | Array | X | (Deprecated, use content.cards[].buttons) RCS button list |
| content.buttons[].buttonType | String | X | COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make a call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share current location), URL (link to URL), CALENDAR (add event)<br>※ Using the CLIPBOARD (copy) button with unified message types is not supported on iOS devices.<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | X |  |
| content.buttons[].buttonJson.action | Object | X | Button action |
| options | Object | X |  |
| options.expiryOption | Integer | X | Duration during which the carrier attempts to deliver to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour)<br>Default: 1 |
| options.groupId | String | X | Group ID for RCS Biz Center statistics integration [Guide](../console-guide/send-a-message/#RCS) (up to 20 bytes) |



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| messageId | String | O | Message ID. This value is generated when a message send request is received. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Free-form message sending request - RCS

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
    "title" : "Holiday hours notice",
    "body" : "Hello. Your order has arrived today. Please come visit us^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "Title",
      "description" : "Body",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "Main title",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "Title 1",
      "title2" : "Title 2",
      "title3" : "Title 3",
      "description1" : "Body 1",
      "description2" : "Body 2",
      "description3" : "Body 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "Add event",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "Event title",
                "description" : "Event description"
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
          "displayText" : "Add event",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "Event title",
              "description" : "Event description"
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
    "title" : "Holiday hours notice",
    "body" : "Hello. Your order has arrived today. Please come visit us^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "Title",
      "description" : "Body",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "Main title",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "Title 1",
      "title2" : "Title 2",
      "title3" : "Title 3",
      "description1" : "Body 1",
      "description2" : "Body 2",
      "description3" : "Body 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "Add event",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "Event title",
                "description" : "Event description"
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
          "displayText" : "Add event",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "Event title",
              "description" : "Event description"
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

## Free-form message sending request - PUSH

Requests free-form message sending for PUSH.


**Request**

```
POST /message/v1.0/PUSH/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| messagePurpose | Path | Enum | O | Message purpose |



**Request body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


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
    "unsubscribePhoneNumber" : "Representative number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Body",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Submit button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link connected when the button is tapped",
        "hint" : "Hint for the button"
      } ],
      "media" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Location of the large icon, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, a feature that groups multiple messages together, supported on Android only",
        "description" : "Description of the group"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | X | Statistics key ID |
| scheduledDateTime | String | X | Scheduled send time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | Contact type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | Contact. You can send a message by entering a contact directly without specifying a recipient. |
| recipients[].contacts[].clientReference | String | X | A user-defined field that can be assigned per recipient |
| recipients[].templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>In bulk sending, template parameters cannot be specified per recipient.<br><br>Template parameters set for a recipient take precedence over message template parameters.<br><br> |
| id | String | X | ID generated when a bulk recipient list or file upload succeeds |
| content | Object | X | Push message content |



**Response body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| messageId | String | O | Message ID. This value is generated when a message sending request is received. |



**Request example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Free-form message sending request - PUSH

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
    "unsubscribePhoneNumber" : "Representative number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Body",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Submit button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link connected when the button is tapped",
        "hint" : "Hint for the button"
      } ],
      "media" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Location of the large icon, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, a feature that groups multiple messages together, supported on Android only",
        "description" : "Description of the group"
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
    "unsubscribePhoneNumber" : "Representative number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Body",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button name",
        "submitName" : "Submit button name",
        "buttonType" : "Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "Link connected when the button is tapped",
        "hint" : "Hint for the button"
      } ],
      "media" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Location of the media, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE",
        "mediaType" : "Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android.",
        "extension" : "Extension of the media file, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Location of the large icon, REMOTE, LOCAL",
        "source" : "Address of the media location, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, a feature that groups multiple messages together, supported on Android only",
        "description" : "Description of the group"
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

## Template Message Sending Request

Sends a message using a registered template.<br>
If no template is registered, register a template first before sending.<br>
<br>
You must configure the recipient settings by selecting one of the following: a single recipient, bulk recipients, or a group query.<br>
* Single recipient (recipient)<br>
* Bulk/group recipients (id)<br>
  <br>
  For scheduled sending, set `scheduledDateTime`.<br>
  For send after confirmation, set `confirmBeforeSend` to true.<br>


**Request**

```
POST /message/v1.0/{messageChannel}/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| messageChannel | Path | Enum | O | Message channel |
| messagePurpose | Path | Enum | O | Message purpose |



**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


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

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | X | Statistics key ID |
| templateId | String | X | Template ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>For group sending, you cannot specify template parameters per recipient.<br><br>Template parameters set on a recipient take precedence over message-level template parameters.<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | Contact type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | Contact. You can send a message by entering a contact directly without specifying a recipient. |
| recipients[].contacts[].clientReference | String | X | A user-defined field that can be assigned per recipient |
| recipients[].templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>For group sending, you cannot specify template parameters per recipient.<br><br>Template parameters set on a recipient take precedence over message-level template parameters.<br><br> |
| id | String | X | ID generated when a bulk recipient list or file upload succeeds |



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code for the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message for the request.<br>Default: SUCCESS |
| messageId | String | O | Message ID. A value generated when a message sending request is received. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Template message sending request

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

## Send Alim Talk Template Messages

Sends a message using a registered template.<br>
If no template has been registered, register a template first before sending.<br>
<br>
You must configure the recipient settings by selecting one of the following: a single recipient, bulk recipients, or a group query.<br>
* Single recipient (recipient)<br>
* Bulk/group recipients (id)<br>
  <br>
  For scheduled sending, set `scheduledDateTime`.<br>
  For send after confirmation, set `confirmBeforeSend` to true.<br>


**Request**

```
POST /message/v1.0/ALIMTALK/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | App key |
| X-NHN-Authorization | Header | String | O | Access token |
| messagePurpose | Path | Enum | O | Message purpose |



**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


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

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | X | Statistics key ID |
| sender | Object | X |  |
| sender.senderKey | String | O | Sender profile sender key |
| templateId | String | O | Template ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| templateParameters | Object | X | Template parameters. Consists of key-value pairs (key: placeholder, value: replacement).<br><br>Per-recipient template parameters cannot be specified for group sending.<br><br>Template parameters set on a recipient take precedence over message-level template parameters.<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | Contact type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | Contact. You can send a message by entering a contact directly without specifying a recipient. |
| recipients[].contacts[].clientReference | String | X | A user-defined field that can be assigned per recipient |
| recipients[].templateParameters | Object | X | Template parameters. Consists of key-value pairs (key: placeholder, value: replacement).<br><br>Per-recipient template parameters cannot be specified for group sending.<br><br>Template parameters set on a recipient take precedence over message-level template parameters.<br><br> |
| id | String | X | ID generated when a bulk recipient list or file is uploaded successfully |



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| messageId | String | O | Message ID. This value is generated when a message sending request is received. |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send Alim Talk Template Messages

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

## Send Brand Message Template Messages

Sends a brand message using a registered template.<br>
If no template has been registered, register a template first before sending.<br>
<br>
You must configure the recipient settings by selecting one of the following: a single recipient, bulk recipients, or a group query.<br>
* Single recipient (recipient)<br>
* Bulk/group recipients (id)<br>
  <br>
  For scheduled sending, set `scheduledDateTime`.<br>
  For send after confirmation, set `confirmBeforeSend` to true.<br>


**Request**

```
POST /message/v1.0/BRANDMESSAGE/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| messagePurpose | Path | Enum | O | Message purpose |



**Request Body**

<!--If this API does not require a request body, enter "This API does not require a request body."-->


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

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| sender | Object | X |  |
| sender.senderKey | String | O | Sender key (40 characters). Group sender keys are not supported. |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | Contact type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | Contact. You can send a message by entering a contact directly without specifying a recipient. |
| recipients[].contacts[].clientReference | String | X | A custom field that can be assigned to each recipient. |
| recipients[].templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>Per-recipient template parameters cannot be specified for group sending.<br><br>Template parameters set on a recipient take precedence over message-level template parameters.<br><br> |
| recipients[].imageParameters | Array | X | Per-recipient image parameters. Overrides message-level image parameters. |
| recipients[].imageParameters[].attachmentId | String | X | Attachment ID. Choose one of attachmentId or imageUrl. |
| recipients[].imageParameters[].imageUrl | String | X | Image URL. Choose one of imageUrl or attachmentId. |
| recipients[].imageParameters[].imageLink | String | X | URL to navigate to when the image is clicked (http/https). Optional. If not set, the KakaoTalk image viewer is used. |
| recipients[].videoParameter | Object | X |  |
| recipients[].videoParameter.videoUrl | String | O | KakaoTV video URL (must start with https://tv.kakao.com/). Required for the PREMIUM_VIDEO type. |
| recipients[].videoParameter.thumbnailAttachmentId | String | X | Thumbnail image attachment ID. Choose one of thumbnailAttachmentId or thumbnailUrl. Only images registered via the standard image upload API can be used. |
| recipients[].videoParameter.thumbnailUrl | String | X | Video thumbnail image URL. Choose one of thumbnailUrl or thumbnailAttachmentId. Only images registered via the standard image upload API can be used. If not set, the default KakaoTV thumbnail is used. |
| id | String | X | ID generated upon successful upload of a bulk recipient list or file. |
| templateId | String | X | Template ID |
| templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>Per-recipient template parameters cannot be specified for group sending.<br><br>Template parameters set on a recipient take precedence over message-level template parameters.<br><br> |
| options | Object | X |  |
| options.audienceType | String | X | Sending target type. CUSTOMER: customer, FRIEND: friend<br>[CUSTOMER, FRIEND] |
| options.targeting | String | X | Message target type. M: users who have consented to marketing, N: users who have consented to marketing but are not friends, O: users who are friends. When using M/N, marketing consent must be enabled on the sender profile and an 080 opt-out number is required.<br>[M, N, O] |
| options.pushAlarm | Boolean | X | Whether to send a push notification for the message (default: true)<br>Default: true |
| options.unsubscribePhoneNumber | String | X | 080 toll-free opt-out phone number. Required when targeting is M/N. Format: 080-XXX-XXXX, 080-XXXX-XXXX, 080XXXXXXX, 080XXXXXXXX. If omitted, the value registered on the sender profile is applied automatically. |
| options.unsubscribeAuthNumber | String | X | Opt-out authentication number (numeric, up to 9 digits). Optional. Cannot be entered alone without unsubscribePhoneNumber. If omitted, the value registered on the sender profile is applied automatically. |
| statsKeyId | String | X | Statistics key ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |



**Response Body**

<!--If this API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| messageId | String | O | Message ID. This value is generated when a message sending request is received. |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send brand message template messages

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

## Send Email Template Message

Sends a message using a registered template.<br>
If no template has been registered, register a template first before sending.<br>
<br>
You must configure the recipient by selecting one of the following: a single recipient, bulk recipients, or a group query.<br>
* Single recipient (recipient)<br>
* Bulk/group recipients (id)<br>
  <br>
  For scheduled sending, set `scheduledDateTime`.<br>
  For send after confirmation, set `confirmBeforeSend` to true.<br>


**Request**

```
POST /message/v1.0/EMAIL/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| messagePurpose | Path | Enum | O | Message purpose |



**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


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

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | X | Statistics key ID |
| templateId | String | X | Template ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>For group sending, you cannot specify template parameters per recipient.<br><br>Template parameters set on a recipient take priority over message-level template parameters.<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | Contact type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | Contact. You can send a message by entering a contact directly without specifying a recipient. |
| recipients[].contacts[].clientReference | String | X | A user-defined field that can be assigned per recipient |
| recipients[].templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>For group sending, you cannot specify template parameters per recipient.<br><br>Template parameters set on a recipient take priority over message-level template parameters.<br><br> |
| id | String | X | ID generated when a bulk recipient list and file upload succeed |



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| messageId | String | O | Message ID. This value is generated when a message sending request is received. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send Email Template Message

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

## Send RCS Template Message

Sends a message using a registered template.<br>
If no template has been registered, register a template first before sending.<br>
<br>
You must configure the recipient settings by selecting one of the following: single recipient, bulk recipients, or group query.<br>
* Single recipient (recipient)<br>
* Bulk/group recipients (id)<br>
  <br>
  For scheduled sending, set `scheduledDateTime`.<br>
  For send after confirmation, set `confirmBeforeSend` to true.<br>


**Request**

```
POST /message/v1.0/RCS/template-messages/{messagePurpose}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| messagePurpose | Path | Enum | O | Message purpose. |



**Request Body**

<!--If this API does not require a request body, enter "This API does not require a request body."-->


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

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | X | Statistics key ID |
| sender | Object | X |  |
| sender.chatbotId | String | X | Chat room (chatbot) ID |
| content | Object | X |  |
| content.unsubscribePhoneNumber | String | X | Opt-out phone number |
| templateId | String | X | Template ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>In group sending, you cannot specify template parameters per recipient.<br><br>Template parameters set on a recipient take priority over message-level template parameters.<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | Contact type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | Contact. You can send a message by entering a contact directly without specifying a recipient. |
| recipients[].contacts[].clientReference | String | X | A user-defined field that can be assigned per recipient. |
| recipients[].templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>In group sending, you cannot specify template parameters per recipient.<br><br>Template parameters set on a recipient take priority over message-level template parameters.<br><br> |
| id | String | X | ID generated when a bulk recipient list or file upload is successful |
| options | Object | X |  |
| options.expiryOption | Integer | X | Duration during which the carrier attempts delivery to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour)<br>Default: 1 |
| options.groupId | String | X | Group ID for RCS Biz Center statistics integration [Guide](../console-guide/send-a-message/#RCS) (maximum 20 bytes) |



**Response Body**

<!--If this API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| messageId | String | O | Message ID. This value is generated when a message send request is received. |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send RCS Template Message

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

## Send SMS Template Message

Sends a message using a registered template.
If no template has been registered, register a template first before sending.

You must configure the recipient settings by selecting one of the following: single recipient, bulk recipients, or group query.
* Single recipient (recipient)
* Bulk/group recipients (id)

For scheduled sending, set `scheduledDateTime`.
For send after confirmation, set `confirmBeforeSend` to true.

When sending an MMS template with an image layout linked, note the following:
* **Required template parameters**: You must include cardNumber and scratchNumber.
  * cardNumber: Used to generate a barcode. Must consist of exactly 16 digits.
  * scratchNumber: No specific constraints.
* **Image layout override**: You can override the image layout set in the template by including content.imageLayoutId or content.imageLayoutName in the request body.
  * Use only one of content.imageLayoutId or content.imageLayoutName.
  * If neither field is included, the default image layout linked when the template was created is used.


**Request**

```
POST /message/v1.0/SMS/template-messages/{messagePurpose}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| messagePurpose | Path | Enum | O | Message purpose. |



**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


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

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | X | Statistics key ID |
| templateId | String | X | Template ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>In group sending, you cannot specify template parameters per recipient.<br><br>Template parameters set on a recipient take precedence over message-level template parameters.<br><br> |
| content | Object | X |  |
| content.imageLayoutId | String | X | Image layout ID |
| content.imageLayoutName | String | X | Image layout name |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | Contact type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | Contact. You can send a message by entering a contact directly without specifying a recipient. |
| recipients[].contacts[].clientReference | String | X | A user-defined field that can be assigned per recipient |
| recipients[].templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>In group sending, you cannot specify template parameters per recipient.<br><br>Template parameters set on a recipient take precedence over message-level template parameters.<br><br> |
| id | String | X | ID generated when the bulk recipient list and file upload succeed |



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| messageId | String | O | Message ID. The value generated when a message sending request is received. |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send SMS Template Message

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

## Send a Flow Message

Sends a message using a registered flow.<br>
If you have not registered a flow, you must register one before sending.<br>
<br>
You must configure the recipient settings by choosing one of the following: a single recipient, bulk recipients, or a group query.<br>
* Single recipient (recipient)<br>
* Bulk/group recipients (id)<br>
  <br>
  For scheduled sending, set `scheduledDateTime`.<br>
  For send after confirmation, set `confirmBeforeSend` to `true`.<br>


**Request**

```
POST /message/v1.0/flow-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| messagePurpose | Path | Enum | O | Message purpose |



**Request Body**

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
        "title" : "Title",
        "body" : "Body"
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

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | X | Statistics key ID |
| flowId | String | X | Flow ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>In group sending, you cannot specify template parameters per recipient.<br><br>Template parameters set on a recipient take precedence over message template parameters.<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | Contact type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | Contact. You can send a message by entering the contact directly without specifying a recipient. |
| recipients[].contacts[].clientReference | String | X | A custom field that can be assigned per recipient |
| recipients[].templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>In group sending, you cannot specify template parameters per recipient.<br><br>Template parameters set on a recipient take precedence over message template parameters.<br><br> |
| id | String | X | ID generated when a bulk recipient list and file upload succeeds |
| flow | Object | X |  |
| flow.steps | Array | O |  |
| flow.steps[].messageChannel | String | O | Message channel<br>[SMS(SMS), ALIMTALK(Alim Talk), EMAIL(Email), RCS(RCS), PUSH(Push)] |
| flow.steps[].sender | Object | X | Sender information. Sender information may vary depending on the message channel.<br> |
| flow.steps[].content | Object | X | Message content. Message content may vary depending on the message channel.<br> |
| flow.steps[].options | Object | X | Sending options. Sending options may vary depending on the message channel.<br> |
| flow.steps[].nextSteps | Array | X | Next steps. If there are no next steps, message sending ends.<br> |



**Response Body**

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

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| messageId | String | O | Message ID. This value is generated when a message send request is received. |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send a flow message

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
        "title" : "Title",
        "body" : "Body"
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
        "title" : "Title",
        "body" : "Body"
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

## Send Instant Flow Messages

When requesting a message send, define a flow to send the message.<br>
<br>
When entering an instant flow, you can send a message using a template or by entering sender information and content directly.


**Request**

```
POST /message/v1.0/instant-flow-messages/{messagePurpose}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| messagePurpose | Path | Enum | O | Message purpose. |



**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->


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
        "title" : "Title",
        "body" : "Body"
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

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | X | Stats key ID |
| scheduledDateTime | String | X | Scheduled send time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>In group sending, you cannot specify template parameters per recipient.<br><br>Template parameters set on a recipient take precedence over message-level template parameters.<br><br> |
| recipients | Array | O |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | Contact type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | Contact. You can send a message by entering a contact directly without specifying a recipient. |
| recipients[].contacts[].clientReference | String | X | A user-defined field that can be assigned per recipient |
| recipients[].templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>In group sending, you cannot specify template parameters per recipient.<br><br>Template parameters set on a recipient take precedence over message-level template parameters.<br><br> |
| instantFlow | Object | O |  |
| instantFlow.steps | Array | O |  |
| instantFlow.steps[].messageChannel | String | O | Message channel<br>[SMS(SMS), ALIMTALK(Alim Talk), EMAIL(Email), RCS(RCS), PUSH(Push)] |
| instantFlow.steps[].sender | Object | X | Sender information. Sender information may vary depending on the message channel.<br> |
| instantFlow.steps[].content | Object | X | Message content. Message content may vary depending on the message channel.<br> |
| instantFlow.steps[].options | Object | X | Send options. Send options may vary depending on the message channel.<br> |
| instantFlow.steps[].templateId | String | X | Template ID. If a template ID is set, the sender information (sender) and message content (content) in the request are not applied.<br>If a template ID is not set in an instant flow message, sender information (sender) and message content (content) are required.<br> |
| instantFlow.steps[].nextSteps | Array | X | Next steps. If there are no next steps, the message send ends.<br> |



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| messageId | String | O | Message ID. This value is generated when a message send request is received. |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send Instant Flow Messages

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
        "title" : "Title",
        "body" : "Body"
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
        "title" : "Title",
        "body" : "Body"
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

## Cancel Sending Message

Enter the message ID you wish to cancel the message.<br>
You can cancel the message using the message ID received in response to the message you sent.<br>
All requests within the message will be canceled.<br>


**Request**

```
POST /message/v1.0/messages/{messageId}/do-cancel
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | Access token |
| messageId | Path  | String | O | null |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not request a request body.



**Request Body**

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

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Cancel Sending Message

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

<a id="confirm-message-delivery"></a>

## Confirm Message Delivery

After confirmation, check the message you requested to send.<br>


**Request**

```
POST /message/v1.0/messages/{messageId}/do-confirm
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | Access token |
| messageId | Path  | String | O | null |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.



**Response Body**

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

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Confirm Message Delivery

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
