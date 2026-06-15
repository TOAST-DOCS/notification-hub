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

## Free-form message sending requests

Request that a message be sent by entering the message content in the request body.

In order to send messages to each message channel, the sender information for each message channel must be registered. You can register the sender information in the **Notification Hub console** > **Sender Information** tab. For a detailed description of outgoing information for message channels, see **Notification** > **Notification Hub** > **Service Policy & Precondition**.

```
POST /message/v1.0/SMS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | App Key |
| X-NHN-Authorization | Header | String | O | Access Token |
| messagePurpose | Path | String | O | Message purpose.<br>[AD, AUTH, NORMAL] |

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
| statsKeyId | String | X | Statistics key ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| sender | Object | X | |
| sender.senderPhoneNumber | String | O | Sender number |
| recipients | Array | X | | |
| recipients[].contacts | Array | X | | |
| recipients[].templateParameters | Object | X | Template parameters. Consist of key (Key, placeholder) and value (Value) pairs.<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | X | ID generated upon successful bulk recipient list and file upload |
| content | Object | X | |
| content.messageType | String | O | Sent message type (SMS, LMS, MMS)<br>[Short message service (SMS), long message service (LMS), and media long message service (MMS)] |
| content.title | String | X | Message title |
| content.body | String | O | Message body |
| content.attachmentIds | Array | X | Up to 3 attachment IDs |

* The **sender** and **content** fields have different formats depending on the message channel.
* The values ​​you can enter in the **recipients[].contact.contactType** and **recipients[].contact.contact** fields vary depending on the message channel.
* For scheduled delivery, set **scheduledDateTime**. You can cancel a scheduled delivery request before it begins. You can do so by calling the Cancel Request API or by going to **Notification Hub Console** > **Delivery Result**.
* For approved delivery, set **confirmBeforeSend** to **true**. After approval, the sender's message will be sent once you approve it in **Notification Hub Console** > **Delivery Result**.
* You cannot set both scheduled and approved delivery at the same time.

<a id="sender-fields-by-message-channel"></a>

### Sender Fields by Message Channel

| Message Channel | Field | Description |
| --- | --- | --- |
| SMS | sender.senderPhoneNumber | Sender Number |
| RCS | sender.brandId | Brand ID |
| RCS | sender.chatbotId | Chatbot ID |
| EMAIL | sender.senderMailAddress | Sender Email Address |
| ALIMTALK | sender.senderKey | Sender Key |
| ALIMTALK | sender.senderProfileType | Sender Profile Type<br>GROUP, NORMAL |

* AlimTalk requires a senderKey and senderProfileType to be entered.
* AlimTalk must be sent with a template. Free-form message sending is not supported.
* There are two sender profile types: GROUP and NORMAL. **GROUP**is a group sender profile and **NORMAL**is a normal sender profile.


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

<span id="messageV1x0003EmailFreeFormMessages"></span>

<a id="request-to-send-a-free-form-message---email"></a>

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
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | Access token |
| messagePurpose | Path  | String | O | Message purpose<br>NORMAL, AD, AUTH |



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
| statsKeyId | String | X | Statistics key ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| sender | Object | X | |
| sender.senderMailAddress | String | O | Sender email address |
| recipients | Array | X | | |
| recipients[].contacts | Array | X | | |
| recipients[].templateParameters | Object | X | Template parameters. Consist of key (Key, placeholder) and value (Value) pairs.<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | X | ID generated upon successful bulk recipient list and file upload |
| content | Object | X | |
| content.title | String | O | Template Email Title |
| content.body | String | O | Template Email Body |
| content.attachmentIds | Array | X | Template Attachment ID |



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

<a id="request-to-send-a-free-form-message---rcs"></a>

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
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | Access token |
| messagePurpose | Path  | String | O | Message purpose<br>NORMAL, AD, AUTH |



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
| statsKeyId | String | X | Statistics key ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | O | Whether to send after confirmation |
| sender | Object | X | |
| sender.brandId | String | O | Brand ID |
| sender.chatbotId | String | O | Chatbot ID |
| recipients | Array | X | | |
| recipients[].contacts | Array | X | | |
| recipients[].templateParameters | Object | X | Template parameters. Consist of key (Key, placeholder) and value (Value) pairs.<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | X | ID generated upon successful bulk recipient list and file upload |
| content | Object | X | |
| content.messageType | String | X | RCS message type <br>[Short message service (SMS), long message service (LMS), media long message service (MMS), and RBC_TEMPLATE (RCS Biz Center template)] |
| content.title | String | X | (Use deprecated, content.cards[].title) Message title |
| content.body | String | X | (Use deprecated, content.cards[].description) Message body |
| content.smsType | String | X | SMS type<br>[STANDALONE (standalone), UNIFIED_STANDALONE (unified standalone)] |
| content.lmsType | String | X | LMS type<br>[STANDALONE (standalone), FORMAT_BASIC (basic format), FORMAT_TITLE_HIGHLIGHT (title highlight format), FORMAT_PARAGRAPH (paragraph format), UNIFIED_STANDALONE (unified standalone)] |
| content.mmsType | String | X | MMS type (required when sending MMS)<br>[HORIZONTAL (horizontal), VERTICAL (vertical), CAROUSEL_MEDIUM (carousel medium), CAROUSEL_SMALL (carousel small), UNIFIED_HORIZONTAL (unified horizontal), UNIFIED_VERTICAL (unified vertical)] |
| content.messagebaseId | String | X | RCS Biz Center Template ID |
| content.unsubscribePhoneNumber | String | X | Unsubscribe Number (required for advertisements) |
| content.cards | Array | X | RCS Card |
| content.cards[].title | String | X | Title |
| content.cards[].description | String | X | Body |
| content.cards[].attachmentId | String | X | Attachment File ID<br>※ If a GIF image is attached to an Integrated MMS Card, it cannot be received on iOS devices. | |
| content.cards[].mTitle | String | X | Main Title |
| content.cards[].mTitleMedia | String | X | Main Title Logo File ID |
| content.cards[].title1 | String | X | Title 1 |
| content.cards[].title2 | String | X | Title 2 |
| content.cards[].title3 | String | X | Title 3 |
| content.cards[].description1 | String | X | Body 1 |
| content.cards[].description2 | String | X | Body 2 |
| content.cards[].description3 | String | X | Body 3 |
| content.cards[].buttons | Array | X | Button |
| content.cards[].buttons[].buttonType | String | X | Button type<br>COMPOSE (Open chat room), CLIPBOARD (Copy), DIALER (Make a call), MAP_SHOW (Show map), MAP_QUERY (Search map), MAP_SHARE (Share current location), URL (Connect URL), CALENDAR (Add to calendar)<br><br>※ If a CLIPBOARD (Copy) button is used in an integrated message type, it cannot be received on iOS devices.<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.cards[].buttons[].buttonJson | Object | X | Button JSON, check format for each button type |
| content.buttons | Array | X | (Use deprecated, content.cards[].buttons) RCS button list |
| content.buttons[].buttonType | String | X | An Action object with the same name as the buttonType value is included as buttonJson.<br>Button Types: Open Chat Room (COMPOSE), Copy (CLIPBOARD), Make a Call (DIALER), Show Map (MAP_SHOW), Search Map (MAP_QUERY), Share Current Location (MAP_SHARE), Connect to URL (URL), Register Schedule (CALENDAR)<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | X | |
| content.buttons[].buttonJson.action | Object | X | Button Action |
| options | Object | X | | |
| options.expiryOption | Integer | X | The time the carrier attempts to send to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour)<br>Default: 1 |
| options.groupId | String | X | Group ID for RCS Biz Center statistics integration |



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

<a id="request-to-send-a-free-form-message---push"></a>

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
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | Access token |
| messagePurpose | Path  | String | O | Message purpose<br>NORMAL, AD, AUTH |



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
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Only IMAGE supported in Android",
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
| statsKeyId | String | X | Statistics key ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| recipients | Array | X | |
| recipients[].contacts | Array | X | | |
| recipients[].templateParameters | Object | X | Template parameters. Consist of key (Key, placeholder) and value (Value) pairs.<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | X | ID generated upon successful bulk recipient list and file upload |
| content | Object | X | Push message content |



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
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Only IMAGE supported in Android",
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
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Only IMAGE supported in Android",
        "extension" : "Media file extension, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "Media location, REMOTE, LOCAL",
        "source" : "Address of where the media is located, URL, LOCAL_RESOURCE",
        "mediaType" : "Media type, IMAGE, GIF, VIDEO, AUDIO. Only IMAGE supported in Android",
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

<a id="request-template-message-sending"></a>

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
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | Access token |
| messageChannel | Path  | String | O | Message channel.<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| messagePurpose | Path  | String | O | Message purpose<br>NORMAL, AD, AUTH |



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
| statsKeyId | String | X | Statistics key ID |
| templateId | String | X | Template ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| templateParameters | Object | X | Template parameters. It consists of a pair of key (Key, placeholder) and value (Value).<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| recipients | Array | X | | |
| recipients[].contacts | Array | X | |
| recipients[].templateParameters | Object | X | Template parameters. It consists of a pair of keys (key, placeholder) and values ​​(value).<br><br>You cannot specify template parameters for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | X | ID generated when bulk recipient list and file upload are successful |



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

<a id="send-alimtalk-template-message"></a>

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
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | Access token |
| messagePurpose | Path  | String | O | Message purpose<br>NORMAL, AD, AUTH |



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
| statsKeyId | String | X | Statistics key ID |
| sender | Object | X | |
| sender.senderKey | String | O | Sender profile sender key |
| templateId | String | O | Template ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| templateParameters | Object | X | Template parameters. It consists of a pair of key (Key, placeholder) and value (Value).<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| recipients | Array | X | | |
| recipients[].contacts | Array | X | | |
| recipients[].templateParameters | Object | X | Template parameter. It consists of a pair of key (key, placeholder) and value (value).<br><br>You cannot specify template parameters for each recipient in group sending.<br><br>Template parameters set for each recipient take precedence over message template parameters.<br><br> |
| id | String | X | ID generated upon successful bulk recipient list and file upload |



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

<span id="messageV1x0008EmailTemplateMessages"></span>

<a id="send-email-template-message"></a>

## Send Email Template Message

Sends a message using a registered template.<br>
If no template has been registered, register a template first before sending.<br>
<br>
The recipient configuration must be set by selecting one of the following: single recipient, bulk recipients, or group query.<br>
* Single recipient (recipient)<br>
* Bulk/group recipients (id)<br>
  <br>
  For scheduled sending, set 'scheduledDateTime'.<br>
  For send after confirmation, set 'confirmBeforeSend' to true.<br>


**Request**

```
POST /message/v1.0/EMAIL/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| messagePurpose | Path | Enum | O | Message purpose. |



**Request body**

<!--If no request body is required, enter "This API does not require a request body."-->


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
| templateParameters | Object | X | Template parameters. Consists of key (substitution variable) and value pairs.<br><br>Recipient-specific template parameters cannot be specified for group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | Contact type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | Contact. Messages can be sent by entering a contact directly without specifying a recipient. |
| recipients[].contacts[].clientReference | String | X | A user-defined field that can be assigned per recipient. |
| recipients[].templateParameters | Object | X | Template parameters. Consists of key (substitution variable) and value pairs.<br><br>Recipient-specific template parameters cannot be specified for group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | X | ID generated when bulk recipient list and file upload are successful |



**Response body**

<!--If no response body is returned, enter "This API does not return a response body."-->

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



**Request example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send email template message

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
| messagePurpose | Path  | String | O | Message purpose<br>NORMAL, AD, AUTH |



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
| statsKeyId | String | X | Statistics key ID |
| sender | Object | X | |
| sender.chatbotId | String | X | Chatbot ID |
| content | Object | X | |
| content.unsubscribePhoneNumber | String | X | Unsubscribe phone number |
| templateId | String | O | Template ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| templateParameters | Object | X | Template parameters. Consists of key (key, placeholder) and value (value) pairs.<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| recipients | Array | X | |
| recipients[].contacts | Array | X | |
| recipients[].templateParameters | Object | X | Template parameters. They consist of key (placeholder) and value (value) pairs.<br><br>You cannot specify template parameters for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | X | ID generated upon successful bulk recipient list and file upload |
| options | Object | X | | |
| options.expiryOption | Integer | X | Time the carrier attempts to send to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour)<br>Default: 1 |
| options.groupId | String | X | Group ID for RCS Biz Center statistics integration |



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

<a id="send-sms-template-message"></a>

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
| messagePurpose | Path  | String | O | Message purpose<br>NORMAL, AD, AUTH |



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
| statsKeyId | String | X | Statistics key ID |
| templateId | String | X | Template ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| templateParameters | Object | X | Template parameters. Consist of key (placeholder) and value (value) pairs.<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| content | Object | X | | | | content.imageLayoutId | String | X | Image layout ID |
| content.imageLayoutName | String | X | Image layout name |
| recipients | Array | X | | |
| recipients[].contacts | Array | O | | |
| recipients[].templateParameters | Object | X | Template parameters. They consist of key (key, placeholder) and value (value) pairs.<br><br>You cannot specify template parameters for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | X | ID generated upon successful bulk recipient list and file upload |



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

<a id="send-flow-message"></a>

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
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | Access token |
| messagePurpose | Path  | String | O | Message purpose<br>NORMAL, AD, AUTH |



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
| statsKeyId | String | X | Statistics key ID |
| flowId | String | X | Flow ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| templateParameters | Object | X | Template parameters. It consists of a pair of key (Key, placeholder) and value (Value).<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| recipients | Array | X | | | | recipients[].contacts | Array | X | | |
| recipients[].templateParameters | Object | X | Template parameters. It consists of a pair of keys (keys, placeholders) and values ​​(values).<br><br>You cannot specify template parameters for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| id | String | X | ID generated upon successful bulk recipient list and file upload |
| flow | Object | X | |
| flow.steps | Array | O | | |
| flow.steps[].messageChannel | String | O | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| flow.steps[].sender | Object | X | Sender information. Sender information may be configured differently depending on the message channel.<br> |
| flow.steps[].content | Object | X | Message content. Message content may be configured differently depending on the message channel.<br> |
| flow.steps[].options | Object | X | Sending options. Sending options can be configured differently depending on the message channel.<br> |
| flow.steps[].nextSteps | Array | X | The next step. If there is no next step, message sending will end.<br> |



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

<a id="send-an-instant-flow-message"></a>

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
| messagePurpose | Path  | String | O | Message purpose<br>NORMAL, AD, AUTH |



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
      "templateId" : "Tj3nE8dq",
      "nextSteps" : [ ]
    } ]
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| statsKeyId | String | X | Statistics key ID |
| scheduledDateTime | String | X | Scheduled sending time |
| confirmBeforeSend | Boolean | X | Whether to send after confirmation |
| templateParameters | Object | X | Template parameters. It consists of a pair of key (Key, placeholder) and value (Value).<br><br>Template parameters cannot be specified for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| recipients | Array | O | | |
| recipients[].contacts | Array | X | |
| recipients[].templateParameters | Object | X | Template parameters. It consists of a pair of key (key, placeholder) and value (value).<br><br>You cannot specify template parameters for each recipient in group sending.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| instantFlow | Object | O | |
| instantFlow.steps | Array | O | |
| instantFlow.steps[].messageChannel | String | O | Message Channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| instantFlow.steps[].sender | Object | X | Sender information. Sender information can be configured differently depending on the message channel.<br> |
| instantFlow.steps[].content | Object | X | Message content. Message content can be configured differently depending on the message channel.<br> |
| instantFlow.steps[].options | Object | X | Sending options. Sending options can be configured differently depending on the message channel.<br> |
| instantFlow.steps[].templateId | String | X | Template ID. If a template ID is set, the sender information (sender) and message content (content) will not be applied to the request.<br>If a template ID is not set in an instant flow message, the sender information (sender) and message content (content) are required.<br> |
| instantFlow.steps[].nextSteps | Array | X | The next step. If there is no next step, message sending will end. |



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
