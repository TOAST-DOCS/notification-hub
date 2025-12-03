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

## Free-form message sending requests

Request that a message be sent by entering the message content in the request body.

In order to send messages to each message channel, the sender information for each message channel must be registered. You can register the sender information in the **Notification Hub console** > **Sender Information** tab. For a detailed description of outgoing information for message channels, see **Notification** > **Notification Hub** > **Guide to Usage Policies and Preparations**.

```
POST /message/v1.0/SMS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | App Key |
| X-NHN-Authorization | Header | String | Y | Access Token |
| messagePurpose | Path | String | Y | Message purpose.<br>[AD, AUTH, NORMAL] |

The additional description that will be added under the request parameter.


**Request Body**

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
    "title" : "Notice for Holiday Operating Hours",
    "body" : "Hello. Your product arrived today. Please visit us^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | N | Statistics key ID |
| scheduledDateTime | String | N | Scheduled sending time |
| confirmBeforeSend | Boolean | N | Whether to send after confirmation |
| sender | Object | N | |
| sender.senderPhoneNumber | String | Y | Sender number |
| recipients | Array | N | | |
| recipients[].contacts | Array | N | | |
| recipients[].templateParameters | Object | N | Template parameters. Consist of key (Key, placeholder) and value (Value) pairs.<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | N | ID generated upon successful bulk recipient list and file upload |
| content | Object | N | |
| content.messageType | String | Y | Sent message type (SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| content.title | String | N | Message title |
| content.body | String | Y | Message body |
| content.attachmentIds | Array | N | Up to 3 attachment IDs |

* The **sender** and **content** fields have different formats depending on the message channel.
* The values ​​you can enter in the **recipients[].contact.contactType** and **recipients[].contact.contact** fields vary depending on the message channel.
* For scheduled delivery, set **scheduledDateTime**. You can cancel a scheduled delivery request before it begins. You can do so by calling the Cancel Request API or by going to **Notification Hub Console** > **Send Tracking**.
* For approved delivery, set **confirmBeforeSend** to **true**. After approval, the sender's message will be sent once you approve it in **Notification Hub Console** > **Send Tracking**.
* You cannot set both scheduled and approved delivery at the same time.

### Sender Fields by Message Channel

| Message Channel | Field | Description |
| --- | --- | --- |
| SMS | sender.senderPhoneNumber | Sender Number |
| RCS | sender.brandId | Brand ID |
| RCS | sender.chatbotId | Chatbot ID |
| EMAIL | sender.senderMailAddress | Sender Email Address |
| ALIMTALK, FRIENDTALK | sender.senderKey | Sender Key |
| ALIMTALK | sender.senderProfileType | Sender Profile Type<br>GROUP, NORMAL |

* Alimtalk requires the sender key (senderKey) and sender profile type (senderProfileType).
* Alimtalk requires a template for sending. Free-form messages are not supported.
* FriendTalk only supports the NORMAL sender profile type. Sending will fail if a sender key from the GROUP sender profile type is used. * There are two types of sender profiles: **GROUP** and **NORMAL**. **GROUP** is a group sender profile, and **NORMAL** is a general sender profile.


**Request Body**

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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful. <br>Default: true |
| header.resultCode | Integer | The result code of the request. <br>Default: 0 |
| header.resultMessage | String | The result message of the request. <br>Default: SUCCESS |
| messageId | String | The message ID. This value is generated when a message sending request is received. |

An additional description to be added to the response.


**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Free-form message sending requests - SMS

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
    "title" : "Notice for Holiday Operating Hours",
    "body" : "Hello. Your product arrived today. Please visit us^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
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
    "title" : "Notice for Holiday Operating Hours",
    "body" : "Hello. Your product arrived today. Please visit us^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>
<span id="messageV1x0002FriendtalkFreeFormMessages"></span>

## Request a Free-Form Message - FriendTalk

Request a free-form message for FriendTalk.


**Request**

```
POST /message/v1.0/FRIENDTALK/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messagePurpose | Path  | String | Y | Message purpose<br>NORMAL, AD, AUTH |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
    "header" : "Header",
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
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | N | Statistics key ID |
| scheduledDateTime | String | N | Scheduled sending time |
| confirmBeforeSend | Boolean | N | Whether to send after confirmation |
| sender | Object | N | |
| sender.senderKey | String | Y | Sender profile sender key |
| recipients | Array | N | | |
| recipients[].contacts | Array | N | | |
| recipients[].templateParameters | Object | N | Template parameters. Consist of key (Key, placeholder) and value (Value) pairs.<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | N | ID generated upon successful bulk recipient list and file upload |
| content | Object | N | |
| content.messageType | String | N | Template message type (TEXT: text type, IMAGE: image type, WIDE_IMAGE: wide image type, WIDE_ITEMLIST: wide item list type, CAROUSEL_FEED: carousel feed type, default: TEXT) |
| content.content | String | N | Template body |
| content.attachmentId | String | N | Attachment ID |
| content.imageUrl | String | N | Template image URL |
| content.imageLink | String | N | Template image link |
| content.buttons | Array | N | Template button |
| content.buttons[].type | String | N | Template button type (WL: web link, AL: app link, BK: bot keyword, MD: message forwarding, BF: business form)<br>[WL, AL, BK, MD, BF] |
| content.buttons[].name | String | N | Template button name |
| content.buttons[].linkMo | String | N | Template button mobile web link |
| content.buttons[].linkPc | String | N | Template button PC web link |
| content.buttons[].schemeIos | String | N | Template button iOS app link |
| content.buttons[].schemeAndroid | String | N | Template button Android app link |
| content.buttons[].bizFormKey | String | N | Bizform key for BF (Business Form) type buttons |
| content.header | String | N | Header (required when using wide item list message type, maximum 25 characters) |
| content.item | Object | N | | |
| content.item.list | Array | N | | |
| content.item.list[].title | String | N | Item Title: 25 characters for the first item, 30 characters for the 2nd to 4th items |
| content.item.list[].attachmentId | String | N | Attachment ID |
| content.item.list[].imageUrl | String | N | Item Image URL |
| content.item.list[].linkMo | String | N | Main Link: Mobile Web Link |
| content.item.list[].linkPc | String | N | Main Link: PC Web Link |
| content.item.list[].schemeIos | String | N | Main Link: iOS App Link |
| content.item.list[].schemeAndroid | String | N | Main Link: Android App Link |
| content.carousel | Object | N | | |
| content.carousel.list | Array | N | | |
| content.carousel.list[].header | String | N | Carousel Item Title |
| content.carousel.list[].message | String | N | Carousel item message |
| content.carousel.list[].attachment | Object | N | |
| content.carousel.list[].attachment.buttons | Array | N | |
| content.carousel.list[].attachment.image | Object | N | |
| content.carousel.list[].attachment.image.attachmentId | String | N | Attachment ID |
| content.carousel.list[].attachment.image.imageUrl | String | N | Carousel item image URL |
| content.carousel.list[].attachment.image.imageLink | String | N | Carousel item image link |
| content.carousel.tail | Object | N | | |
| content.carousel.tail.linkMo | String | N | Main link Mobile web link |
| content.carousel.tail.linkPc | String | N | Main Link PC Web Link |
| content.carousel.tail.schemeIos | String | N | Main Link iOS App Link |
| content.carousel.tail.schemeAndroid | String | N | Main Link Android App Link |
| content.coupon | Object | N | | |
| content.coupon.title | String | N | Coupon Name |
| content.coupon.description | String | N | Coupon Detailed Description (plain text, up to 12 characters for image types / up to 18 characters for wide image types and wide item list types) |
| content.coupon.linkMo | String | N | Main Link Mobile Web Link |
| content.coupon.linkPc | String | N | Main Link PC Web Link |
| content.coupon.schemeIos | String | N | Main Link iOS App Link |
| content.coupon.schemeAndroid | String | N | Representative Link Android App Link |



**Request Body**

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

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| messageId | String | The message ID. This value is generated when a message sending request is received. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Request to send a free-form message - FriendTalk

POST {{endpoint}}/message/v1.0/FRIENDTALK/free-form-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
  }
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
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
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
    "header" : "Header",
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
  }
}'
```

</details>
<span id="messageV1x0003EmailFreeFormMessages"></span>

## Request to Send a Free-Form Message - EMAIL

Request a free-form message to be sent to EMAIL.


**Request**

```
POST /message/v1.0/EMAIL/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messagePurpose | Path  | String | Y | Message purpose<br>NORMAL, AD, AUTH |



**Request Body**

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
    "title" : "[NHN Cloud Email][##env##] Monitoring notification",
    "body" : "Hello. Your product arrived today.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | N | Statistics key ID |
| scheduledDateTime | String | N | Scheduled sending time |
| confirmBeforeSend | Boolean | N | Whether to send after confirmation |
| sender | Object | N | |
| sender.senderMailAddress | String | Y | Sender email address |
| recipients | Array | N | | |
| recipients[].contacts | Array | N | | |
| recipients[].templateParameters | Object | N | Template parameters. Consist of key (Key, placeholder) and value (Value) pairs.<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | N | ID generated upon successful bulk recipient list and file upload |
| content | Object | N | |
| content.title | String | Y | Template Email Title |
| content.body | String | Y | Template Email Body |
| content.attachmentIds | Array | N | Template Attachment ID |



**Request Body**

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

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| messageId | String | The message ID. This value is generated when a message sending request is received. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Request to Send a Free-Form Message - EMAIL

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
    "body" : "Hello. Your product arrived today.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
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
    "body" : "Hello. Your product arrived today.",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>
<span id="messageV1x0004RcsFreeFormMessages"></span>

## Request to Send a Free-Form Message - RCS

Request to send a free-form message to RCS.


**Request**

```
POST /message/v1.0/RCS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messagePurpose | Path  | String | Y | Message purpose<br>NORMAL, AD, AUTH |



**Request Body**

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
    "title": "Notice of Holiday Operating Hours",
    "body": "Hi, your product arrived today. Please visit us^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "Title",
      "description" : "Body",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "Main Title",
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
            "displayText" : "Register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "Schedule title",
                "description" : "Schedule description"
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
          "displayText" : "Register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "Schedule title",
              "description" : "Schedule description"
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

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | N | Statistics key ID |
| scheduledDateTime | String | N | Scheduled sending time |
| confirmBeforeSend | Boolean | N | Whether to send after confirmation |
| sender | Object | N | |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chatbot ID |
| recipients | Array | N | | |
| recipients[].contacts | Array | N | | |
| recipients[].templateParameters | Object | N | Template parameters. Consist of key (Key, placeholder) and value (Value) pairs.<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | N | ID generated upon successful bulk recipient list and file upload |
| content | Object | N | |
| content.messageType | String | N | RCS message type <br>[SMS, LMS, MMS, RBC_TEMPLATE] |
| content.title | String | N | Message title |
| content.body | String | N | Message body |
| content.smsType | String | N | SMS type <br>[STANDALONE] |
| content.lmsType | String | N | LMS type <br>[STANDALONE, FORMAT_BASIC, FORMAT_TITLE_HIGHLIGHT, FORMAT_PARAGRAPH] |
| content.mmsType | String | N | MMS type (required for MMS transmission) <br>[HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL] |
| content.messagebaseId | String | N | RCS Biz Center Template ID |
| content.unsubscribePhoneNumber | String | N | Unsubscribe Number (required for advertisements) |
| content.cards | Array | N | RCS Card |
| content.cards[].title | String | N | Title |
| content.cards[].description | String | N | Body |
| content.cards[].attachmentId | String | N | Image Attachment File ID |
| content.cards[].mTitle | String | N | Main Title |
| content.cards[].mTitleMedia | String | N | Main Title Logo File ID |
| content.cards[].title1 | String | N | Title 1 |
| content.cards[].title2 | String | N | Title 2 |
| content.cards[].title3 | String | N | Title 3 |
| content.cards[].description1 | String | N | Body 1 |
| content.cards[].description2 | String | N | Body 2 |
| content.cards[].description3 | String | N | Body 3 |
| content.cards[].buttons | Array | N | |
| content.buttons | Array | N | RCS Button List |
| content.buttons[].buttonType | String | N | An Action object with the same name as the buttonType value is included as buttonJson.<br>Button Types: Open Chat Room (COMPOSE), Copy (CLIPBOARD), Make a Call (DIALER), Show Map (MAP_SHOW), Search Map (MAP_QUERY), Share Current Location (MAP_SHARE), Connect to URL (URL), Register Schedule (CALENDAR)<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | N | |
| content.buttons[].buttonJson.action | Object | N | Button Action |
| options | Object | N | | |
| options.expiryOption | Integer | N | The time the carrier attempts to send to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour)<br>Default: 1 |
| options.groupId | String | N | Group ID for RCS Biz Center statistics integration |



**Request Body**

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

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| messageId | String | The message ID. This value is generated when a message sending request is received. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Request to a Send Free-Form Message - RCS

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
    "title" : "Notice for Holiday Operating Hours",
    "body" : "Hello. Your product arrived today. Please visit us^^",
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
            "displayText" : "Register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "Schedule title",
                "description" : "Schedule description"
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
          "displayText" : "Register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "Schedule title",
              "description" : "Schedule description"
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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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
    "title" : "Notice for Holiday Operating Hours",
    "body" : "Hello. Your product arrived today. Please visit us^^",
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
            "displayText" : "Register schedule",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "Schedule title",
                "description" : "Schedule description"
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
          "displayText" : "Register schedule",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "Schedule title",
              "description" : "Schedule description"
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

## Request to Send a Free-Form Message - PUSH

Request to send a free-form message for PUSH.


**Request**

```
POST /message/v1.0/PUSH/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messagePurpose | Path  | String | Y | Message purpose<br>NORMAL, AD, AUTH |



**Request Body**

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
    "unsubscribePhoneNumber" : "Main Number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Content",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button Name",
        "submitName" : "Send button name",
        "buttonType" : "Button Type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "When you press the button, the link is connected",
        "hint" : "Hint for button"
      } ],
      "media" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Location of large icon, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, feature to group multiple messages, supported only on Android",
        "description" : "Description for group"
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

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | N | Statistics key ID |
| scheduledDateTime | String | N | Scheduled sending time |
| confirmBeforeSend | Boolean | N | Whether to send after confirmation |
| recipients | Array | N | |
| recipients[].contacts | Array | N | | |
| recipients[].templateParameters | Object | N | Template parameters. Consist of key (Key, placeholder) and value (Value) pairs.<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | N | ID generated upon successful bulk recipient list and file upload |
| content | Object | N | Push message content |



**Request Body**

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

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| messageId | String | The message ID. This value is generated when a message sending request is received. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Request to Send a Free-Form Message - PUSH

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
    "unsubscribePhoneNumber" : "Main Number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Content",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button Name",
        "submitName" : "Send button name",
        "buttonType" : "Button Type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "When you press the button, the link is connected",
        "hint" : "Hint for button"
      } ],
      "media" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Location of large icon, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, feature to group multiple messages, supported only on Android",
        "description" : "Description for group"
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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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
    "unsubscribePhoneNumber" : "Main Number",
    "unsubscribeGuide" : "Menu > Settings",
    "title" : "Title",
    "body" : "Content",
    "richMessage" : {
      "buttons" : [ {
        "name" : "Button Name",
        "submitName" : "Send button name",
        "buttonType" : "Button Type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "When you press the button, the link is connected",
        "hint" : "Hint for button"
      } ],
      "media" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "Location of large icon, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "Group key, feature to group multiple messages, supported only on Android",
        "description" : "Description for group"
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

## Request Template Message Sending

Send a message using a registered template.<br>
If no template is registered, register a template first and then send the message.<br>
<br>
The recipient settings must be set to one of the following: Single Recipient, Bulk Recipient, or Group Query.<br>
* Single Recipient (recipient)<br>
* Bulk/Group Recipient (id)<br>
<br>
For scheduled sending, set 'scheduledDateTime'.<br>
For confirmation-based sending, set 'confirmBeforeSend' to true.<br>


**Request**

```
POST /message/v1.0/{messageChannel}/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messageChannel | Path  | String | Y | Message channel.<br>[SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH] |
| messagePurpose | Path  | String | Y | Message purpose<br>NORMAL, AD, AUTH |



**Request Body**

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

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | N | Statistics key ID |
| templateId | String | N | Template ID |
| scheduledDateTime | String | N | Scheduled sending time |
| confirmBeforeSend | Boolean | N | Whether to send after confirmation |
| templateParameters | Object | N | Template parameters. It consists of a pair of key (Key, placeholder) and value (Value).<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| recipients | Array | N | | |
| recipients[].contacts | Array | N | |
| recipients[].templateParameters | Object | N | Template parameters. It consists of a pair of keys (key, placeholder) and values ​​(value).<br><br>You cannot specify template parameters for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | N | ID generated when bulk recipient list and file upload are successful |



**Request Body**

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

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| messageId | String | The message ID. This value is generated when a message sending request is received. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Request to Send a Template Message

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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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

## Send AlimTalk Template Message

Sends a message using a registered template.<br>
If no template has been registered, register a template first and then send.<br>
<br>
You must select one of the following recipients: Single Recipient, Bulk Recipient, or Group Query.<br>
* Single Recipient (recipient)<br>
* Bulk/Group Recipient (id)<br>
<br>
For scheduled delivery, set 'scheduledDateTime'.<br>
For confirmation-based delivery, set 'confirmBeforeSend' to true.<br>


**Request**

```
POST /message/v1.0/ALIMTALK/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messagePurpose | Path  | String | Y | Message purpose<br>NORMAL, AD, AUTH |



**Request Body**

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

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | N | Statistics key ID |
| sender | Object | N | |
| sender.senderKey | String | Y | Sender profile sender key |
| templateId | String | N | Template ID |
| scheduledDateTime | String | N | Scheduled sending time |
| confirmBeforeSend | Boolean | N | Whether to send after confirmation |
| templateParameters | Object | N | Template parameters. It consists of a pair of key (Key, placeholder) and value (Value).<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| recipients | Array | N | | |
| recipients[].contacts | Array | N | | |
| recipients[].templateParameters | Object | N | Template parameter. It consists of a pair of key (key, placeholder) and value (value).<br><br>You cannot specify template parameters for each recipient in group sending.<br><br>Template parameters set for each recipient take precedence over message template parameters.<br><br> |
| id | String | N | ID generated upon successful bulk recipient list and file upload |



**Request Body**

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

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| messageId | String | The message ID. This value is generated when a message sending request is received. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send an AlimTalk Template Message

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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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
<span id="messageV1x0008RcsTemplateMessages"></span>

## Send RCS Template Message

Sends a message using a registered template.<br>
If no template is registered, register a template first and then send.<br>
<br>
The recipient settings must be set to one of the following: Single Recipient, Bulk Recipient, or Group Query.<br>
* Single Recipient (recipient)<br>
* Bulk/Group Recipient (id)<br>
<br>
For scheduled sending, set 'scheduledDateTime'.<br>
For confirmation-based sending, set 'confirmBeforeSend' to true.<br>


**Request**

```
POST /message/v1.0/RCS/template-messages/{messagePurpose}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| messagePurpose | Path  | String | Y | Message purpose<br>NORMAL, AD, AUTH |



**Request Body**

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

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | N | Statistics key ID |
| sender | Object | N | |
| sender.chatbotId | String | N | Chatbot ID |
| content | Object | N | |
| content.unsubscribePhoneNumber | String | N | Unsubscribe phone number |
| templateId | String | N | Template ID |
| scheduledDateTime | String | N | Scheduled sending time |
| confirmBeforeSend | Boolean | N | Whether to send after confirmation |
| templateParameters | Object | N | Template parameters. Consists of key (key, placeholder) and value (value) pairs.<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| recipients | Array | N | |
| recipients[].contacts | Array | N | |
| recipients[].templateParameters | Object | N | Template parameters. They consist of key (placeholder) and value (value) pairs.<br><br>You cannot specify template parameters for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | N | ID generated upon successful bulk recipient list and file upload |
| options | Object | N | | |
| options.expiryOption | Integer | N | Time the carrier attempts to send to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour)<br>Default: 1 |
| options.groupId | String | N | Group ID for RCS Biz Center statistics integration |



**Request Body**

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

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| messageId | String | The message ID. This value is generated when a message sending request is received. |



**Request Example**


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

## Send SMS Template Message

Sends a message using the registered template.<br>
If no template has been registered, register a template first and then send.<br>
<br>
The recipient settings must be set to either a single recipient, a bulk recipient, or a group query.<br>
* Single recipient (recipient)<br>
* Bulk/group recipient (id)<br>
  <br>
  For scheduled sending, set 'scheduledDateTime'.<br>
  For confirmation-based sending, set 'confirmBeforeSend' to true.<br>

When sending an MMS template with an image layout, keep the following in mind:
* **Required template parameters**: `cardNumber` and `scratchNumber` must be included.
    * `cardNumber`: Used to generate a barcode and must be a 16-digit number.
    * `scratchNumber`: No restrictions. * **Image Layout Override**: You can override the image layout set in the template by including `content.imageLayoutId` or `content.imageLayoutName` in the request body.
    * You must use only one of `content.imageLayoutId` and `content.imageLayoutName`.
    * If neither field is included, the default image layout associated with the template will be used.


**Request**

```
POST /message/v1.0/SMS/template-messages/{messagePurpose}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| messagePurpose | Path  | String | Y | Message purpose<br>NORMAL, AD, AUTH |



**Request Body**

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
    "imageLayoutName" : "2025-promotion-layout"
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
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | N | Statistics key ID |
| templateId | String | N | Template ID |
| scheduledDateTime | String | N | Scheduled sending time |
| confirmBeforeSend | Boolean | N | Whether to send after confirmation |
| templateParameters | Object | N | Template parameters. Consist of key (placeholder) and value (value) pairs.<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| content | Object | N | | | | content.imageLayoutId | String | N | Image layout ID |
| content.imageLayoutName | String | N | Image layout name |
| recipients | Array | N | | |
| recipients[].contacts | Array | Y | | |
| recipients[].templateParameters | Object | N | Template parameters. They consist of key (key, placeholder) and value (value) pairs.<br><br>You cannot specify template parameters for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | N | ID generated upon successful bulk recipient list and file upload |
| dryRun | Boolean | N | Sending is executed in simulation mode. No actual sending occurs.<br>The reception result status for each contact is set to SEND_FAILED.<br><br>Default: false |



**Request Body**

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

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| messageId | String | The message ID. This value is generated when a message sending request is received. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send a SMS Template Message

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
    "imageLayoutName" : "2025-promotion-layout"
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
    "imageLayoutName" : "2025-promotion-layout"
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
}'
```

</details>
<span id="messageV1x0009FlowMessages"></span>

## Send Flow Message

Send a message using a registered flow.<br>
If you haven't registered a flow, you must register one and send it.<br>
<br>
The recipient settings must be set to either a single recipient, bulk recipient, or group query.<br>
* Single recipient (recipient)<br>
* Bulk/group recipient (id)<br>
<br>
For scheduled delivery, set 'scheduledDateTime'.<br>
For confirmation-based delivery, set 'confirmBeforeSend' to true.<br>


**Request**

```
POST /message/v1.0/flow-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messagePurpose | Path  | String | Y | Message purpose<br>NORMAL, AD, AUTH |



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

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | N | Statistics key ID |
| flowId | String | N | Flow ID |
| scheduledDateTime | String | N | Scheduled sending time |
| confirmBeforeSend | Boolean | N | Whether to send after confirmation |
| templateParameters | Object | N | Template parameters. It consists of a pair of key (Key, placeholder) and value (Value).<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| recipients | Array | N | | | | recipients[].contacts | Array | N | | |
| recipients[].templateParameters | Object | N | Template parameters. It consists of a pair of keys (keys, placeholders) and values ​​(values).<br><br>You cannot specify template parameters for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | N | ID generated upon successful bulk recipient list and file upload |
| flow | Object | N | |
| flow.steps | Array | Y | | |
| flow.steps[].messageChannel | String | Y | Message channel<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| flow.steps[].sender | Object | N | Sender information. Sender information may be configured differently depending on the message channel.<br> |
| flow.steps[].content | Object | N | Message content. Message content may be configured differently depending on the message channel.<br> |
| flow.steps[].options | Object | N | Sending options. Sending options can be configured differently depending on the message channel.<br> |
| flow.steps[].nextSteps | Array | N | The next step. If there is no next step, message sending will end.<br> |



**Request Body**

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

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| messageId | String | The message ID. This value is generated when a message sending request is received. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send Flow Message

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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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

## Send an Instant Flow Message

When requesting a message, define a flow to send the message.<br>
<br>
When entering an instant flow, you can use a template to request a message or manually enter sender information and content.


**Request**

```
POST /message/v1.0/instant-flow-messages/{messagePurpose}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| messagePurpose | Path  | String | Y | Message purpose<br>NORMAL, AD, AUTH |



**Request Body**

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
        "title" : "Title",
        "body" : "Body"
      },
      "options" : {
        "expiryOption:" : 1,
        "groupId\"" : "groupId"
      },
      "templateId" : "Template_ID",
      "nextSteps" : [ ]
    } ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | N | Statistics key ID |
| scheduledDateTime | String | N | Scheduled sending time |
| confirmBeforeSend | Boolean | N | Whether to send after confirmation |
| templateParameters | Object | N | Template parameters. It consists of a pair of key (Key, placeholder) and value (Value).<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| recipients | Array | Y | | |
| recipients[].contacts | Array | N | |
| recipients[].templateParameters | Object | N | Template parameters. It consists of a pair of key (key, placeholder) and value (value).<br><br>You cannot specify template parameters for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| instantFlow | Object | Y | |
| instantFlow.steps | Array | Y | |
| instantFlow.steps[].messageChannel | String | Y | Message Channel<br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| instantFlow.steps[].sender | Object | N | Sender information. Sender information can be configured differently depending on the message channel.<br> |
| instantFlow.steps[].content | Object | N | Message content. Message content can be configured differently depending on the message channel.<br> |
| instantFlow.steps[].options | Object | N | Sending options. Sending options can be configured differently depending on the message channel.<br> |
| instantFlow.steps[].templateId | String | N | Template ID. If a template ID is set, the sender information (sender) and message content (content) will not be applied to the request.<br>If a template ID is not set in an instant flow message, the sender information (sender) and message content (content) are required.<br> |
| instantFlow.steps[].nextSteps | Array | N | The next step. If there is no next step, message sending will end. |



**Request Body**

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

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| messageId | String | The message ID. This value is generated when a message sending request is received. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send an Instant Flow Message

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
      "templateId" : "Template_ID",
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
      "templateId" : "Template_ID",
      "nextSteps" : [ ]
    } ]
  }
}'
```

</details>
<span id="messageV1x0100MessageIdDoCancel"></span>

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
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messageId | Path  | String | Y | null |



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
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messageId | Path  | String | Y | null |



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


## Request to send an instant flow message
**Request**

```
POST /message/v1.0/instant-flow-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Required | Description |
| - | - | - | - | - |
| appKey | Header | String | Y | AppKey |
| accessToken | Header | String | Y | Authentication Token |
| messagePurpose | Path | String | Y | Message Purpose<br>NORMAL, AD, AUTH |

**Request Body**

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
          "brandId": "Brand_ID",
          "chatbotId": "Chat room_ID"
        },
        "content" : {
          "lmsType" : "STANDALONE",
          "cards" : [
            {
              "title" : "Title",
              "description" : "Body"
            }
          ]
        },
        "templateId" : "Template_ID",
        "nextSteps" : [ 
          {
            "messageChannel" : "SMS",
            "sender" : {
              "senderPhoneNumber" : "0123456789"
            },
            "content" : {
              "title" : "Title",
              "body" : "Body"
            },
            "templateId" : "Template_ID",
            "nextSteps" : [ ]
          } 
        ]
      } 
    ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | N | Statistics key ID |
| scheduledDateTime | DateTime (ISO 8601) | N | Scheduled sending time (e.g., 2024-10-29T06:29:00+09:00) |
| confirmBeforeSend | Boolean | N | Whether to confirm before sending (default: false)
| templateParameters | Object | N | Template parameters. Required if setting a template ID. |
| recipients[] | Array | Y | Recipient list |
| recipients[].contacts[] | Array | N | Recipient contact list. |
| recipients[].contacts[].contactType | String | Y | Contact Types<br>PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP |
| recipients[].contacts[].contact | String | Y | Contact information. You can send messages by directly entering contact information without specifying recipients. |
| recipients[].contacts[].clientReference | String | N | User custom field |
| recipients[].templateParameters | | N | Template parameters. Required if setting a template ID. |
| instantFlow | Object | Y | Instant flow. You can define it without creating a flow. |
| instantFlow.steps[] | Array | Y | Instant flow steps. (Refer to the instant flow step specifications for each message channel.) |

* A message channel that has been used once cannot be used in the next step.
* A step can have multiple subsequent steps.

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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | true |
| header.resultCode | Integer | 0 |
| header.resultMessage | String | SUCCESS |
| messageId | String | Message ID. This is the value generated when a message sending request is received. |

**Failure Response - Duplicate Recipient**

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 400004,
    "resultMessage" : "There are duplicate recipient addresses."
  },
  "duplicatedContacts" : [
    {
      "contactType": "PHONE_NUMBER",
      "contact": "0123456789"
    }
  ]
}
```




**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send Instant Flow Message
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
        "title" : "Title",
        "body" : "Body"
      },
      "templateId" : "Template_ID",
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
            "title" : "Title",
            "body" : "Body"
          },
          "templateId" : "Template_ID",
          "nextSteps" : [ ]
        } ]
      }
     }'
```

</details>

<span id="instant-flow-message-sending-request-rcs-step"></span>

### Instant Flow Message Send Request Body RCS Step Example
* This is an example of instantFlow.steps for sending an instant flow consisting of only one RCS step.

```json
{
  "instantFlow" : {
    "steps" : [ 
      {
        "messageChannel" : "RCS",
        "sender" : {
          "brandId": "Brand_ID",
          "chatbotId": "Chat room_ID"
        },
        "content" : {
          "lmsType" : "STANDALONE",
          "cards" : [
            {
              "title" : "Title",
              "description" : "Body"
            }
          ]
        },
        "options": {
          "expiryOption": 1,
          "groupId":"groupId"
        },
        "templateId" : "Template_ID",
        "nextSteps" : [ ]
      } 
    ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Name | Type | Required | Description |
|-----------------------------------------| ----------------|----|-------------------------------------------|
| instantFlow.steps[] | Array | Y | Flow Step |
| instantFlow.steps[].messageChannel | String | Y | Message Channel<br>SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH |
| instantFlow.steps[].templateId | String | N | Template ID. If a template ID is set, the sender information (sender) and message content (content) will not be applied to the request.<br>If a template ID is not set in the instant flow message, the sender information (sender) and message content (content) are required.<br> |
| instantFlow.steps[].sender | Object | N | Sender information (refer to the example of the RCS body of a free-form message request) |
| instantFlow.steps[].content | Object | N | Message content (see example of a free-form message sending request RCS body) |
| instantFlow.steps[].options | Object | N | Sending options (see example of a free-form message sending request RCS body) |
| instantFlow.steps[].nextSteps[] | Object Array | N | Next step. |