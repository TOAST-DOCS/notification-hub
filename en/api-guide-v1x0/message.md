<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Message</h1>

**Notification > Notification Hub > API v1.0 User Guide > Messages**

<span id="free-form-message-sending-request"></span>

## Free-form message sending requests

Request that a message be sent by entering the message content in the request body.

In order to send messages to each message channel, the sender information for each message channel must be registered. You can register the sender information in the **Notification Hub console** > **Sender Information** tab. For a detailed description of outgoing information for message channels, see **Notification** > **Notification Hub** > **Guide to Usage Policies and Preparations**.

<!-- !!! tip "알아두기"-->
<!-- API를 사용할 때 사용자가 알아 두면 좋을 참고 사항이나 추가 정보를 제공할 때 사용합니다.-->

<!-- !!! warning "주의"-->
<!--API를 사용할 때 따르지 않을 경우 서비스의 비정상 또는 비효율적 동작이 발생할 수 있는 주의 사항을 표기할 때 사용합니다.-->

**Request**

```
POST /message/v1.0/{messageChannel}/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| messageChannel | Path | String | Y | Message channels<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| messagePurpose | Path | String | Y | Message purpose<br>NORMAL, AD, AUTH |

**Common request bodies**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

For more information on the body of the request depending on the message channel, please see **Detailed request body by message channel** below.

```json
{
  "statsKeyId": "Statistics_Id",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "...": "Different_formats_for_different_message_channels"
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
    "...": "Different_formats_for_different_message_channels"
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Name | Type | Required  | Description                                                                                                                                    |
| --- | --- |-----|---------------------------------------------------------------------------------------------------------------------------------------|
| statsKeyId | String | N   | Statistics Key ID                                                                                                                              |
| scheduledDateTime | DateTime(ISO 8601) | N   | Scheduled send date (e.g., 2024-10-29T06:29:00+09:00)                                                                                                |
| confirmBeforeSend | Boolean | N   | Whether to verify before sending (default false)                                                                                                                 |
| sender | Object | Y/N | Sender, Push, and other message channels are required                                                                                                               |
| recipients | Object Array | Y   | Receiver Array                                                                                                                                |
| recipients[].contacts | Object Array | Y   | Arrange the recipient's contacts                                                                                                                           |
| recipients[].contacts[].contactType | String | Y   | Contact types<br>phone_number, email_address, token_fcm, token_apns, token_adm, token_apns_sandbox, token_apns_voip, token_apns_voip_sandbox |
| recipients[].contacts[].contact | String | Y   | Contact                                                                                                                                   |
| content | Object | Y   | Message content                                                                                                                                |

* Depending on the message channel, the **sender** and **content** fields have different formats.
* The message channel determines the values you can enter in the **recipients** **[].contact.contactType**, **recipients[].contact.contact** fields.
* For scheduled sending, set **the scheduledDateTime**. Scheduled dispatches can be canceled before the dispatch starts. You can cancel the request by calling the cancel request API or **from the** **Notification Hub console** > **View dispatch**.
* For post-approval sending, set **confirmBeforeSend** **to true**. After approval, sender messages will be sent when you approve **them in the** **Notification Hub console** > **Delivery Result**.
* You can't set up a scheduled sending and a post-approval sending at the same time.

### SENDER field per message channel

| Message channels | Field | Description |
| --- | --- | --- |
| SMS | sender.senderPhoneNumber | Caller ID |
| RCS | sender.brandId | Brand ID |
| RCS | sender.chatbotId | Room ID |
| EMAIL | sender.senderMailAddress | Sender email address |
| ALIMTALK, FRIENDTALK | sender.senderKey | Sender key |
| ALIMTALK | sender.senderProfileType | Outgoing profile types<br>GROUP, NORMAL |

* AlimTalk requires a senderKey and senderProfileType to be entered.
* FriendTalk can only use the NORMAL sender profile type. If you use a sending key with the GROUP sender profile type, the sending will fail.
* There are two sender profile types: GROUP and NORMAL. **GROUP**is a group sender profile and **NORMAL**is a normal sender profile.

**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "messageId": "Message_Id"
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Name | Type | Description |
| --- | --- | --- |
| header.isSuccessful | Boolean | API request success |
| header.resultCode | Integer | Result code |
| header.resultMessage | String | Result message |
| messageId | String | Message ID of the successful request |

**Request example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send a free-form message
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
    "body": "Hello. NHN Cloud's new product Notification Hub has been released."
  }
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/message/v1.0/PUSH/free-form-messages/${MESSAGE_PURPOSE}" \
     -H "Content-Type: application/json" \
     -h "x-nc-app-key: ${app_key}" \
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
            "body": "Hello. NHN Cloud's new product Notification Hub has been released."
        }
    }'
```

</details>

<span id="free-form-message-request-body"></span>

## Example of a Free-Form Message Request Body for Each Message Channel

<span id="free-form-message-request-body-sms"></span>

### SMS

```json
{
  "statsKeyId": "Statistics_Key_Id",
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
    "title": "[NHN Cloud Notification Hub] Announcement",
    "body": "Hello. This is NHN Cloud Notification Hub",
    "attachmentIds": [
      "Attachment_File_Ids"
    ]
  }
}
```

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| sender | Object | Y | Sender, Push, and other message channels are required |
| sender.senderPhoneNumber | String | N | Caller ID |
| content | Object | Y | Message content |
| content.messageType | String | Y | Message type<br>SMS (short message), LMS (long message), MMS (media long message) |
| content.title | String | Y | Title |
| content.body | String | Y | Content |
| content.attachmentIds | String Array | N | Attachment ID |


<span id="free-form-message-request-body-rcs-sms-standalone"></span>

### RCS - SMS

```json
{
  "statsKeyId": "Statistics_Key_Id",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "Brand_Id",
    "chatbotId": "Chatbot_Id"
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
    "smsType": "STANDALONE",
    "cards": [
        {
          "description":"Hello, this is NHN Cloud Notification Hub.",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Go to Homepage"
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


| Name | Type | Required | Description |
| --- | --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------|
| sender | Object | Y | Sender |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chat room ID |
| content | Object | Y | Message content |
| content.messageType | String | Y | Message type in RCS, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 unsubscribe number, required if the sending purpose is advertising |
| content.smsType | String | Y | SMS type, required if the message type is SMS, STANDALONE (standard) |
| content.cards | Object Array | Y | Card |
| content.cards[].title | String | N | Title |
| content.cards[].description | String | Y | Content |
| content.cards[].buttons | Object Array | N | Button |
| content.cards[].buttons[].buttonType | String | Y | Button Type<br>COMPOSE (Open a chat room), CLIPBOARD (Copy), DIALER (Make a call), MAP_SHOW (Show a map), MAP_QUERY (Search a map), MAP_SHARE (Share your current location), URL (Connect to a URL), CALENDAR (Register a schedule) |
| content.cards[].buttons[].buttonJson | Object | Y | Button Json, check the format for the button type |
| options | Object | N | Sending Options |
| options.expiryOption | Integer | N | Timeout for attempts to send to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour) |
| options.groupId | String | N | Group ID for RCS BizCenter statistics integration |

<span id="free-form-message-request-body-rcs-lms-standalone"></span>

### RCS - LMS Standard

```json
{
  "statsKeyId": "Statistics_Key_ID",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "Brand_ID",
    "chatbotId": "Chat room_ID"
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
          "title":"[NHN Cloud] Notice",
          "description":"Hello, this is NHN Cloud Notification Hub.",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Go to Homepage"
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

| Name | Type | Required | Description |
| --- | --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------|
| sender | Object | Y | Sender |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chatroom ID |
| content | Object | Y | Message content |
| content.messageType | String | Y | Message type in RCS, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 unsubscribe number, required if the purpose of sending is advertising |
| content.lmsType | String | Y | LMS type, required if the message type is LMS, STANDALONE (Standard), FORMAT_BASIC (Basic format), FORMAT_TITLE_HIGHLIGHT (Highlighted title format), FORMAT_PARAGRAPH (Paragraph format) |
| content.cards | Object Array | Y | Card |
| content.cards[].title | String | N | Title |
| content.cards[].description | String | Y | Content |
| content.cards[].buttons | Object Array | N | Button |
| content.cards[].buttons[].buttonType | String | Y | Button Type<br>COMPOSE (Open Chat), CLIPBOARD (Copy), DIALER (Make a Call), MAP_SHOW (Show Map), MAP_QUERY (Search Map), MAP_SHARE (Share Current Location), URL (Connect URL), CALENDAR (Register Schedule) |
| content.cards[].buttons[].buttonJson | Object | Y | Button Json, Check the format for the button type |
| options | Object | N | Sending Options |
| options.expiryOption | Integer | N | Timeout for device transmission attempts (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour) |
| options.groupId | String | N | Group ID for RCS BizCenter statistics integration |

<span id="free-form-message-request-body-rcs-lms-format-basic"></span>

### RCS - LMS Format Basic and Format Title Emphasis
  * List of mTitleMedia Icon File IDs
  * Promotion: LT-messagebase.common-DdWk6s
  * Coupon: LT-messagebase.common-5Weq00
  * Event: LT-messagebase.common-jUAJX2
  * Reservation: LT-messagebase.common-2Yxt2H
  * Receipt: LT-messagebase.common-2k8ydI
  * Notification: LT-messagebase.common-YCVd02

```json
{
  "statsKeyId": "Statistics_Key_ID",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "Brand_ID",
    "chatbotId": "Chat room_ID"
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
          "mTitle":"[NHN Cloud] Notice",
          "mTitleMedia":"LT-messagebase.common-DdWk6s",
          "title":"Notice 1",
          "description":"Hello, this is NHN Cloud Notification Hub.",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Go to Homepage"
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

| Name | Type | Required | Description |
| --- | --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------|
| sender | Object | Y | Sender |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chatroom ID |
| content | Object | Y | Message content |
| content.messageType | String | Y | Message type in RCS, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 unsubscribe number, required if the purpose of sending is advertising |
| content.lmsType | String | Y | LMS type, required if the message type is LMS, STANDALONE (Standard), FORMAT_BASIC (Basic format), FORMAT_TITLE_HIGHLIGHT (Highlighted title format), FORMAT_PARAGRAPH (Paragraph format) |
| content.cards | Object Array | Y | Card |
| content.cards[].mTitle | String | Y | Main Title |
| content.cards[].mTitleMedia | String | N | Main Title Icon |
| content.cards[].title | String | N | Title |
| content.cards[].description | String | Y | Content |
| content.cards[].buttons | Object Array | N | Button |
| content.cards[].buttons[].buttonType | String | Y | Button Type<br>COMPOSE (Open Chat Room), CLIPBOARD (Copy), DIALER (Make a Call), MAP_SHOW (Show Map), MAP_QUERY (Search Map), MAP_SHARE (Share Current Location), URL (Connect URL), CALENDAR (Register Schedule) |
| content.cards[].buttons[].buttonJson | Object | Y | Button Json, check the format for the button type |
| options | Object | N | Sending Options |
| options.expiryOption | Integer | N | Timeout for sending to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour) |
| options.groupId | String | N | Group ID for RCS BizCenter statistics integration |

### RCS - LMS Format Paragraph Type
  * List of mTitleMedia Icon File IDs
  * Promotion: LT-messagebase.common-DdWk6s
  * Coupon: LT-messagebase.common-5Weq00
  * Event: LT-messagebase.common-jUAJX2
  * Reservation: LT-messagebase.common-2Yxt2H
  * Receipt: LT-messagebase.common-2k8ydI
  * Notification: LT-messagebase.common-YCVd02

```json
{
  "statsKeyId": "Statistics_Key_ID",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "Brand_ID",
    "chatbotId": "Chat room_ID"
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
          "mTitle":"[NHN Cloud] Notice",
          "mTitleMedia":"LT-messagebase.common-DdWk6s",
          "title1":"Notice 1",
          "description1":"Hello, this is NHN Cloud Notification Hub.",
          "title2":"Notice 2",
          "description2":"Hello, this is NHN Cloud Notification Hub.",
          "title3":"Notice 3",
          "description3":"Hello, this is NHN Cloud Notification Hub.",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Notice1 button"
                }
              }
            },
            {},
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Notice2 button"
                }
              }
            },
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Notice2 button"
                }
              }
            },
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Notice3 button"
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

| Name | Type | Required | Description |
| --- | --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------|
| sender | Object | Y | Sender |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chatroom ID |
| content | Object | Y | Message content |
| content.messageType | String | Y | Message type in RCS, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 unsubscribe number, required if the purpose of sending is advertising |
| content.lmsType | String | Y | LMS type, required if the message type is LMS, STANDALONE (Standard), FORMAT_BASIC (Basic format), FORMAT_TITLE_HIGHLIGHT (Highlighted title format), FORMAT_PARAGRAPH (Paragraph format) |
| content.cards | Object Array | Y | Card |
| content.cards[].mTitle | String | Y | Main Title |
| content.cards[].mTitleMedia | String | N | Main Title Icon |
| content.cards[].title1 | String | N | Title (Paragraph 1) |
| content.cards[].description1 | String | Y | Content (Paragraph 1) |
| content.cards[].title2 | String | N | Title (Paragraph 2) |
| content.cards[].description2 | String | Y | Content (Paragraph 2) |
| content.cards[].title3 | String | N | Title (Paragraph 3) |
| content.cards[].description3 | String | Y | Content (Paragraph 3) |
| content.cards[].buttons | Object Array | N | Button |
| content.cards[].buttons[].buttonType | String | Y | Button Type<br>COMPOSE (Open Chat), CLIPBOARD (Copy), DIALER (Make a Call), MAP_SHOW (Show Map), MAP_QUERY (Search Map), MAP_SHARE (Share Current Location), URL (Connect URL), CALENDAR (Register Schedule) |
| content.cards[].buttons[].buttonJson | Object | Y | Button JSON, check the format for the button type |
| options | Object | N | Sending Options |
| options.expiryOption | Integer | N | Timeout for sending attempts to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour) |
| options.groupId | String | N | Group ID for RCS BizCenter statistics integration |

### RCS - MMS Landscape, Portrait

```json
{
  "statsKeyId": "Statistics_Key_ID",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "Brand_ID",
    "chatbotId": "Chat room_ID"
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
          "title":"[NHN Cloud] Notice",
          "description":"Hello, this is NHN Cloud Notification Hub.",
          "attachmentId":"Attachment ID",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Go to Homepage"
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


| Name | Type | Required | Description |
| --- | --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------|
| sender | Object | Y | Sender |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chatroom ID |
| content | Object | Y | Message content |
| content.messageType | String | Y | Message type in RCS, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 Unsubscribe Number, Required if sending purpose is advertising |
| content.mmsType | String | Y | MMS Type, Required if message type is MMS, HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL |
| content.cards | Object Array | Y | Card |
| content.cards[].title | String | N | Title |
| content.cards[].description | String | Y | Content |
| content.cards[].attachmentId | String | Y | Attachment ID |
| content.cards[].buttons | Object Array | N | Button |
| content.cards[].buttons[].buttonType | String | Y | Button Type<br>COMPOSE (Open Chat), CLIPBOARD (Copy), DIALER (Make a Call), MAP_SHOW (Show Map), MAP_QUERY (Search Map), MAP_SHARE (Share Current Location), URL (Connect URL), CALENDAR (Register Schedule) |
| content.cards[].buttons[].buttonJson | Object | Y | Button Json, Check the format for the button type |
| options | Object | N | Sending Options |
| options.expiryOption | Integer | N | Timeout for transmission attempts to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour) |
| options.groupId | String | N | Group ID for RCS BizCenter statistics integration |

### RCS - MMS Carousel

```json
{
  "statsKeyId": "Statistics_Key_ID",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "Brand_ID",
    "chatbotId": "Chat room_ID"
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
          "title":"[NHN Cloud] Notice",
          "description":"Hello, this is NHN Cloud Notification Hub.",
          "attachmentId":"Attachment ID",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Go to Homepage"
                }
              }
            }
          ]
        },
        {
          "title":"[NHN Cloud] Notice",
          "description":"Hello, this is NHN Cloud Notification Hub.",
          "attachmentId":"Attachment ID",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Go to Homepage"
                }
              }
            }
          ]
        },
        {
          "title":"[NHN Cloud] Notice",
          "description":"Hello, this is NHN Cloud Notification Hub.",
          "attachmentId":"Attachment ID",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Go to Homepage"
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


| Name | Type | Required | Description |
| --- | --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------|
| sender | Object | Y | Sender |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chatroom ID |
| content | Object | Y | Message content |
| content.messageType | String | Y | Message type in RCS, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 Unsubscribe Number, Required if sending purpose is advertising |
| content.mmsType | String | Y | MMS Type, Required if message type is MMS, HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL |
| content.cards | Object Array | Y | Card |
| content.cards[].title | String | N | Title |
| content.cards[].description | String | Y | Content |
| content.cards[].attachmentId | String | Y | Attachment ID |
| content.cards[].buttons | Object Array | N | Button |
| content.cards[].buttons[].buttonType | String | Y | Button Type<br>COMPOSE (Open Chat), CLIPBOARD (Copy), DIALER (Make a Call), MAP_SHOW (Show Map), MAP_QUERY (Search Map), MAP_SHARE (Share Current Location), URL (Connect URL), CALENDAR (Register Schedule) |
| content.cards[].buttons[].buttonJson | Object | Y | Button Json, Check the format for the button type |
| options | Object | N | Sending Options |
| options.expiryOption | Integer | N | Timeout for transmission attempts to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour) |
| options.groupId | String | N | Group ID for RCS BizCenter statistics integration |


<span id="free-form-message-request-body-friendtalk-text"></span>

### FriendTalk - Text

* AlimTalk can only send templates and flow messages because it can only be sent after registering and approving templates.
* The **sender** and **content** fields in AlimTalk can be found in the **request body** of the **template message send**.
* FriendTalk can only use the NORMAL sender profile type. If you use a sending key with the GROUP sender profile type, the sending will fail.

```json
{
    "statsKeyId": "Statistics_Key_Id",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "senderProfile_SenderKey"
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
      "content": "sending_content",
      "buttons": [
        {
          "type": "WL",
          "name": "Button_name",
          "linkMo": "Mobile_link",
          "linkPc": "PC_link",
          "schemeIos": "iOS_app_link",
          "schemeAndroid": "Android_app_link",
          "bizFormKey": "BizForm_Key"
        }
      ],
      "coupon": {
        "title": "Coupon_Title",
        "description": "Coupon_Description",
        "linkMo": "Mobile_Link",
        "linkPc": "PC_link",
        "schemeIos": "iOS_App_Link",
        "schemeAndroid": "Android_app_link"
      }
    }
}
```


| Name | Type | Required | Description                                                            |
| --- | --- |----|---------------------------------------------------------------|
| sender | Object | Y  | Sender                                                           |
| sender.senderKey | Object | Y  | Outgoing profile_outgoing_key                                                     |
| content | Object | Y  | Message content                                                        |
| content.messageType | String | Y  | Message types                                                        |
| content.content | String | Y  | Content                                                            |
| content.buttons                   | Object Array  | N  | Button                                                                                                                                                        |
| content.buttons[].type            | String | Y  | Button type<br>WL (Web Link), AL (App Link), BK (Bot Keyword), MD (Message Delivery), BF (Business Form)                                                                                             |
| content.buttons[].name            | String | Y  | Button name                                                                                                                                                     |
| content.buttons[].linkMo          | String | N  | Link mobile, required if button type is WL                                                                                                                                    |
| content.buttons[].linkPc          | String | N  | Link PC                                                                                                                                                     |
| content.buttons[].schemeIos       | String | N  | iOS app link                                                                                                                                                  |
| content.buttons[].schemeAndroid   | String | N  | Android app link                                                                                                                                              |
| content.buttons[].bizFormKey      | String | N  | Bizform key, required if button type is BF                                                                                                                                     |
| content.coupon | Object | N  | Coupons                                                            |
| content.coupon.title | String | Y  | Title, if limited to 5 formats<br>"${number}One discount coupon" number is 1 or greater than or equal to 99,999,999<br>"${number}% off coupon" number is at least 1 and no more than 100<br>"Shipping discount coupon"<br><br>"${7 characters or less} free coupon"<br>"${7 characters or less} UP coupon"                                                          |
| content.coupon.description | String | Y  | Coupon description (up to 12 characters for plain text, image, carousel feed / up to 18 characters for wide image, wide item list) |
| content.coupon.linkMo | String | N  | Link Mobile                                                        |
| content.coupon.linkPc | String | N  | Link PC                                                         |
| content.coupon.schemeIos | String | N  | iOS app link                                            |
| content.coupon.schemeAndroid | String | N  | Android app link                         |

<span id="free-form-message-request-body-friendtalk-image"></span>

### FriendTalk - Image / Wide Image

* FriendTalk can only use the NORMAL sender profile type. If you use a sending key with the GROUP sender profile type, the sending will fail.

```json
{
    "statsKeyId": "Statistics_Key_Id",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "senderProfile_SenderKey"
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
      "content": "Send_Content",
      "attachmentId": "Attachment_File_ID",
      "imageLink": "image_link_URL",
      "buttons": [
        {
          "type": "WL",
          "name": "Button_name",
          "linkMo": "Mobile_link",
          "linkPc": "PC_link",
          "schemeIos": "iOS_app_link",
          "schemeAndroid": "Android_app_link",
          "bizFormKey": "BizForm_Key"
        }
      ],
      "coupon": {
        "title": "Coupon_Title",
        "description": "Coupon_Description",
        "linkMo": "Mobile_Link",
        "linkPc": "PC_link",
        "schemeIos": "iOS_App_Link",
        "schemeAndroid": "Android_app_link"
      }
    }
}
```

| Name | Type            | Required | Description                                                            |
| --- |---------------|----|---------------------------------------------------------------|
| sender | Object        | Y  | Sender                                                           |
| sender.senderKey | Object        | Y  | Outgoing profile_outgoing_key                                                     |
| content | Object        | Y  | Message content                                                        |
| content.messageType | String        | Y  | Message types                                                        |
| content.content | String        | Y  | Content                                                            |
| content.attachmentId | String        | Y  | Attachment ID |
| content.imageLink | String        | N  | Image link |
| content.buttons                   | Object Array | N  | Button                                                                                                                                                        |
| content.buttons[].type            | String        | Y  | Button type<br>WL (Web Link), AL (App Link), BK (Bot Keyword), MD (Message Delivery), BF (Business Form)                                                                                             |
| content.buttons[].name            | String        | Y  | Button name                                                                                                                                                     |
| content.buttons[].linkMo          | String        | N  | Link mobile, required if button type is WL                                                                                                                                    |
| content.buttons[].linkPc          | String        | N  | Link PC                                                                                                                                                     |
| content.buttons[].schemeIos       | String        | N  | iOS app link                                                                                                                                                  |
| content.buttons[].schemeAndroid   | String        | N  | Android app link                                                                                                                                              |
| content.buttons[].bizFormKey      | String        | N  | Bizform key, required if button type is BF                                                                                                                                     |
| content.coupon | Object        | N  | Coupons                                                            |
| content.coupon.title | String        | Y  | Title, if limited to 5 formats<br>"${number}One discount coupon" number is 1 or greater than or equal to 99,999,999<br>"${number}% off coupon" number is at least 1 and no more than 100<br>"Shipping discount coupon"<br><br>"${7 characters or less} free coupon"<br>"${7 characters or less} UP coupon"                                                          |
| content.coupon.description | String        | Y  | Coupon description (up to 12 characters for plain text, image, carousel feed / up to 18 characters for wide image, wide item list) |
| content.coupon.linkMo | String        | N  | Link Mobile                                                        |
| content.coupon.linkPc | String        | N  | Link PC                                                         |
| content.coupon.schemeIos | String        | N  | iOS app link                                            |
| content.coupon.schemeAndroid | String        | N  | Android app link                         |

<span id="free-form-message-request-body-friendtalk-wide-itemlist"></span>

### FriendTalk - Wide Itemized

* FriendTalk can only use the NORMAL sender profile type. If you use a sending key with the GROUP sender profile type, the sending will fail.

```json
{
    "statsKeyId": "Statistics_Key_Id",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "senderProfile_SenderKey"
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
          "name": "Button_Name",
          "linkMo": "Mobile_link",
          "linkPc": "PC_link",
          "schemeIos": "iOS_app_link",
          "schemeAndroid": "Android_app_link",
          "bizFormKey": "BizForm_Key"
        }
      ],
      "header": "Header",
      "item": {
          "list": [{
            "title": "Item_Title",
            "attachmentId": "Attachment_File_Id",
            "linkMo": "Mobile_Link",
            "linkPc": "PC_Link",
            "schemeIos": "iOS_App_Link",
            "schemeAndroid": "Android_app_link"
          },
          {
            "title": "Item_Title",
            "attachmentId": "Attachment_File_Id",
            "linkMo": "Mobile_Link",
            "linkPc": "PC_link",
            "schemeIos": "iOS_App_Link",
            "schemeAndroid": "Android_app_link"
          },
          {
          "title": "Item_Title",
          "attachmentId": "Attachment_File_Id",
          "linkMo": "Mobile_Link",
          "linkPc": "PC_link",
          "schemeIos": "iOS_App_Link",
          "schemeAndroid": "Android_app_link"
          }
        ]
      },
      "coupon": {
        "title": "Coupon_Title",
        "description": "Coupon_Title_Description",
        "linkMo": "Mobile_Link",
        "linkPc": "PC_link",
        "schemeIos": "iOS_App_Link",
        "schemeAndroid": "Android_app_link"
      }
    }
}
```

| Name                                | Type            | Required | Description                                                                                                                                                        |
|-----------------------------------|---------------|----|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| sender                            | Object        | Y  | Sender                                                                                                                                                       |
| sender.senderKey                  | Object        | Y  | Outgoing profile_outgoing_key                                                                                                                                                 |
| content                           | Object        | Y  | Message content                                                                                                                                                    |
| content.messageType               | String        | Y  | Message types                                                                                                                                                    |
| content.buttons                   | Object Array | N  | Button                                                                                                                                                        |
| content.buttons[].type            | String        | Y  | Button type<br>WL (Web Link), AL (App Link), BK (Bot Keyword), MD (Message Delivery), BF (Business Form)                                                                                             |
| content.buttons[].name            | String        | Y  | Button name                                                                                                                                                     |
| content.buttons[].linkMo          | String        | N  | Link mobile, required if button type is WL                                                                                                                                    |
| content.buttons[].linkPc          | String        | N  | Link PC                                                                                                                                                     |
| content.buttons[].schemeIos       | String        | N  | iOS app link                                                                                                                                                  |
| content.buttons[].schemeAndroid   | String        | N  | Android app link                                                                                                                                              |
| content.buttons[].bizFormKey      | String        | N  | Bizform key, required if button type is BF                                                                                                                                     |
| content.header                    | String        | Y  | Header                                                                                                                                                        |
| content.item                      | Object        | Y  | Wide item                                                                                                                                                   |
| content.item.list                 | Object Array | Y  | Wide item list (at lease 3, up to 4)                                                                                                                                 |
| content.item.list[].title         | String        | Y  | Item title (up to 25 characters for the first item, up to 30 characters for items 2-4)                                                                                                         |
| content.item.list[].attachmentId  | String        | Y  | Attachment ID                                                                                                                                                 |
| content.item.list[].linkMo        | String        | Y  | Mobile web link                                                                                                                                                  |
| content.item.list[].linkPc        | String        | Y  | PC web link                                                                                                                                                   |
| content.item.list[].schemeIos     | String        | Y  | iOS app link                                                                                                                                                  |
| content.item.list[].schemeAndroid | String        | Y  | Android app links                                                                                                                                                 |
| content.coupon                    | Object        | N  | Coupons                                                                                                                                                        |
| content.coupon.title              | String        | Y  | Title, if limited to 5 formats<br>"${number}One discount coupon" number is 1 or greater than or equal to 99,999,999<br>"${number}% off coupon" number is at least 1 and no more than 100<br>"Shipping discount coupon"<br><br>"${7 characters or less} free coupon"<br>"${7 characters or less} UP coupon" |
| content.coupon.description        | String        | Y  | Coupon description (up to 12 characters for plain text, image, carousel feed / up to 18 characters for wide image, wide item list)                                                                                   |
| content.coupon.linkMo             | String        | N  | Link Mobile                                                                                                                                                    |
| content.coupon.linkPc             | String        | N  | Link PC                                                                                                                                                     |
| content.coupon.schemeIos          | String        | N  | iOS app link                                                                                                                                                  |
| content.coupon.schemeAndroid      | String        | N  | Android app link                                                                                                                                              |

<span id="free-form-message-request-body-friendtalk-carousel"></span>

### FriendTalk - Carousel Feed

* FriendTalk can only use the NORMAL sender profile type. If you use a sending key with the GROUP sender profile type, the sending will fail.

```json
{
    "statsKeyId": "Statistics_Key_Id",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "senderProfile_SenderKey"
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
            "header": "Carousel_Item_Title",
            "message": "Carousel_item_message",
            "attachment": {
              "buttons": [
                {
                  "type": "WL",
                  "name": "button_name",
                  "linkMo": "Mobile_link",
                  "linkPc": "PC_link",
                  "schemeIos": "iOS_app_link",
                  "schemeAndroid": "Android_app_link"
                }
              ],
              "image": {
                "attachmentId": "Attachment_File_Id",
                "imageLink": "Image_Link_URL"
              },
              "coupon": {
                "title": "Coupon_Title",
                "description": "Coupon_Description",
                "linkMo": "Mobile link",
                "linkPc": "PC_link",
                "schemeIos": "iOS_App_Link",
                "schemeAndroid": "Android_app_link"
              }
            }
          },
          {
            "header": "Carousel_item_header",
            "message": "Carousel_item_message",
            "attachment": {
              "buttons": [
                {
                  "type": "WL",
                  "name": "button_name",
                  "linkMo": "Mobile_link",
                  "linkPc": "PC_link",
                  "schemeIos": "iOS_app_link",
                  "schemeAndroid": "Android_app_link"
                }
              ],
              "image": {
                "attachmentId": "Attachment_File_Id",
                "imageLink": "Image_Link_URL"
              },
              "coupon": {
                "title": "Coupon_Title",
                "description": "Coupon_Description",
                "linkMo": "Mobile link",
                "linkPc": "PC_link",
                "schemeIos": "iOS_App_Link",
                "schemeAndroid": "Android_app_link"
              }
            }
          }
        ],
        "tail": {
          "linkMo": "Mobile_link",
          "linkPc": "PC_link",
          "schemeAndroid": "Android_app_link",
          "schemeIos": "iOS_app_link"
        }
      }
    }
}
```

| Name                                                         | Type            | Required | Description                                                                                                                                                       |
|------------------------------------------------------------|---------------|----|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| sender                                                     | Object        | Y  | Sender                                                                                                                                                      |
| sender.senderKey                                           | Object        | Y  | Outgoing profile_outgoing_key                                                                                                                                                |
| content                                                    | Object        | Y  | Message content                                                                                                                                                   |
| content.messageType                                        | String        | Y  | Message types                                                                                                                                                   |
| content.carousel                                           | Object        | Y  | Carousel                                                                                                                                                      |
| content.carousel.list                                      | Object Array | Y  | Carousel lists (minimum 2, maximum 10)                                                                                                                                   |
| content.carousel.list[].header                             | String        | Y  | Carousel item title (up to 20 characters), only available for carousel feeds                                                                                                                     |
| content.carousel.list[].message                            | String        | Y  | Carousel item message (up to 180 characters), only available in carousel feeds                                                                                                                   |
| content.carousel.list[].attachment                         | Object        | N  | Carousel item images, button information                                                                                                                                       |
| content.carousel.list[].attachment.buttons                 | Object Array | N  | Button list (up to 2)                                                                                                                                           |
| content.carousel.list[].attachment.buttons[].type          | String        | Y  | Button type<br>WL (Web Link), AL (App Link), BK (Bot Keyword), MD (Message Delivery), BF (Business Form)                                                                                            |
| content.carousel.list[].attachment.buttons[].name          | String        | Y  | Button name                                                                                                                                                    |
| content.carousel.list[].attachment.buttons[].linkMo        | String        | N  | Link mobile, required if button type is WL                                                                                                                                   |
| content.carousel.list[].attachment.buttons[].linkPc        | String        | N  | Link PC                                                                                                                                                    |
| content.carousel.list[].attachment.buttons[].schemeIos     | String        | N  | iOS app link                                                                                                                                                 |
| content.carousel.list[].attachment.buttons[].schemeAndroid | String        | N  | Android app link                                                                                                                                             |
| content.carousel.list[].attachment.image                   | Object        | Y  | Carousel images                                                                                                                                                  |
| content.carousel.list[].attachment.image.attachmentId      | String        | Y  | Attachment ID                                                                                                                                                 |
| content.carousel.list[].attachment.image.imageLink         | String        | N  | Image link URL                                                                                                                                               |
| content.carousel.list[].attachment.coupon                  | Object        | N  | Coupons                                                                                                                                                       |
| content.carousel.list[].attachment.coupon.title            | String        | Y  | Title, if limited to 5 formats<br>"${number}One discount coupon" number is 1 or greater than or equal to 99,999,999<br>"${number}% off coupon" number is at least 1 and no more than 100<br>"Shipping discount coupon"<br><br>"${7 characters or less} free coupon"<br>"${7 characters or less} UP coupon" |
| content.carousel.list[].attachment.coupon.description      | String        | Y  | Coupon description (up to 12 characters for plain text, image, carousel feed / up to 18 characters for wide image, wide item list)                                                                                  |
| content.carousel.list[].attachment.coupon.linkMo           | String        | N  | Link Mobile                                                                                                                                                   |
| content.carousel.list[].attachment.coupon.linkPc           | String        | N  | Link PC                                                                                                                                                    |
| content.carousel.list[].attachment.coupon.schemeIos        | String        | N  | iOS app link                                                                                                                                                 |
| content.carousel.list[].attachment.coupon.schemeAndroid    | String        | N  | Android app link                                                                                                                                             |
| content.carousel.tail                                      | Object        | N  | About the carousel more button                                                                                                                                           |
| content.carousel.tail.linkMo                               | String        | Y  | Mobile web link                                                                                                                                           |
| content.carousel.tail.linkPc                               | String        | N  | Mobile web link                                                                                                                                           |
| content.carousel.tail.schemeIos                            | String        | N  | Mobile web link                                                                                                                                           |
| content.carousel.tail.schemeAndroid                        | String        | N  | Mobile web link                                                                                                                                           |

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
    "title": "[NHN Cloud Notification Hub] Announcement",
    "body": "Hello. This is NHN Cloud Notification Hub",
    "attachmentIds": [
      "Attachment_File_Ids"
    ]
  }
}
```

| Name | Type            | Required | Description |
| --- |---------------|----| --- |
| sender | Object        | N  | Sender, Push, and other message channels are required |
| sender.senderMailAddress | Object        | N  | Sender email address |
| content | Object        | Y  | Message content |
| content.title | Object        | Y  | Title |
| content.Object | Y             | Content |
| content.attachmentIds | String Array | N  | Attachment ID |

* The domain in the sender email address must be verified as owned.
* You can upload up to 10 attachments that are no larger than 30 MB.
* Attachments can't exceed a maximum of 30 MB in total.
* You can attach up to 30 MB, but depending on the attachment limit policy of the receiving email system (gmail.com, naver.com, etc.), we recommend attachments that are 10 MB or less, as they may be rejected for **exceeding the limit** or result in a higher spam flagging rate.
* **Only EMAIL_ADDRESS** is allowed in the **recipients[].contacts[].contactType** field. 
* In the **recipients[].contacts[].contact** field, enter the recipient email addresses.

<span id="free-form-message-request-body-push"></span>

### Push

```json
{
  "statsId": "Statistics_Id",
  "scheduledDateTime": "2024-10-29T06:29:00+09:00",
  "confirmBeforeSend": false,
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "TOKEN_FCM",
          "contact": "Token"
        }
      ]
    }
  ],
  "content": {
    "unsubscribePhoneNumber": "1234-1234",
    "unsubscribeGuide": "Settings > Menu",
    "style": {
      "useHtmlStyle": true
    },
    "title" : "<b>NHN Cloud </b> Notification",
    "body" : "<b>Launch event</b> <i>Check out the announcement</i>",
    "richMessage" : {
      "buttons" : [{
        "name" : "Button name",
        "submitName": "Submit button name",
        "buttonType" : "REPLY",
        "link" : "myapp://product_detail?product_id=1234",
        "hint" : "Hint for the button"
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
        "key" : "Key of the group",
        "description" : "Description of the group"
      }
    },
    "customKey" : "customValue"
  }
}
```

| Name | Type                    | Required | Description |
| --- |-----------------------| --- | --- |
| content | Object                | Y | Message content |
| content.unsubscribePhoneNumber | String                | Representative numbers for unsubscribing from push messages |
| content.unsubscribeGuide | String                | Instructions for unsubscribing from push messages |
| content.title | String                | Y | Title |
| content.String | Y                     | Content |
| content.style.useHtmlStyle | Boolean               | Y | Using HTML styles (Android only) |
| content.richMessage | Object                | Rich Messages |
| content.richMessage | Object                | N | Required when using Rich Messages |
| content.richMessage.buttons | Object Array         | N |  Buttons added to the rich message, up to a maximum of three |
| content.richMessage.button.name | String                | Button name |
| content.richMessage.button.buttonType | String                | Button type, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS |
| content.richMessage.button.link | String                | button, the link to the |
| content.richMessage.button.hint | String                | Hints for buttons |
| content.richMessage.media | Object                | N |  Media added to rich messages |
| content.richMessage.media.source | String                | The address, URL, and LOCAL_RESOURCE of where the media is located. |
| content.richMessage.media.mediaType | String                | N |  Type of media, IMAGE, GIF, VEDIO, AUDIO. Only IMAGE is supported on Android. |
| content.richMessage.media.expandable | Boolean               | N | Whether to enable expand on click media on Android |
| content.richMessage.androidMedia | Object                | N |  Media used on Android devices. Format is the same as media |
| content.richMessage.iosMedia | Object                | N |  The media used on iOS devices. The format is the same as media. |
| content.richMessage.largeIcon | Object                | N |  Large icons added to rich messages, only available on Android |
| content.richMessage.largeIcon.source | String                | Y | The address of where the media is located |
| content.richMessage.group | Object                | N |  Ability to group multiple messages together, only available on Android |
| content.richMessage.group.key | String                | Y |  Keys in a group |
| content.richMessage.group.description | String                | Y |  Description of the group |
| content.customKey | Object Array or String Array | N | Custom keys and values |

* Pushes don't require a **sender** field.
* Pushes can build **content** fields by adding user-defined keys and values.
* The **recipients[].contacts[].contactType** field must be one of the following: **TOKEN_FCM**, **TOKEN_APNS, TOKEN_ADM**, **TOKEN_APNS_SANDBOX**, **TOKEN_APNS_VOIP**, **TOKEN_APNS_VOIP_SANDBOX**.
* In the **recipients[].contacts[].contact** field, enter the **push token**.


<span id="template-message-sending-request"></span>

## Request to send a template message

**Request**

```
POST /message/v1.0/{messageChannel}/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| messageChannel | Path | String | Y | Message channels<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| messagePurpose | Path | String | Y | Message purpose<br>NORMAL, AD, AUTH |

**Request Body**

```json
{
  "statsKeyId": "Statistics_Id",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "templateId": "Template_Id",
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
  ],
  "sender": {
    "senderKey": "Outgoing_Key",
    "chatbotId": "Chat room_ID"
  },
  "content": {
    "unsubscribePhoneNumber": "08012341234"
  }
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Name | Type                 | Required | Description |
| --- |--------------------| --- | --- |
| statsKeyId | String             | N | Statistics Key ID |
| scheduledDateTime | DateTime(ISO 8601) | N | Scheduled send date (e.g., 2024-10-29T06:29:00+09:00) |
| confirmBeforeSend | Boolean            | N | Whether to verify before sending (default false) |
| templateId | String             | Y | Template ID |
| templateParameters | Object             | N | Template parameter |
| recipients | Object Array      | Y | Receiver Array |
| recipients[].contacts | Object Array              | Y | Arrange the recipient's contacts |
| recipients[].contacts[].contactType | String             | Y | Contact types |
| recipients[].contacts[].contact | String             | Y | Contact |
| recipients[].templateParameters | Object             | N | Template parameter |

* Template parameters must match the parameters defined in the template.
* Template parameters are divided into common template parameters and recipient template parameters.
* Common template parameters are parameters that apply equally to all recipients. Recipient template parameters are used to apply parameters that are different for each recipient.
* If no recipient template parameters exist, only common template parameters are applied. If common template parameters and recipient template parameters overlap, the recipient template parameters take precedence.
* The value of a template parameter can be of type string, array, or object. The array or object types are available in the FREE_MARKER template.

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "messageId": "Message_Id"
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Sending a template message
POST {{endpoint}}/message/v1.0/SMS/template-messages/NORMAL
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "statsKeyId": "Statistics_Id",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "templateId": "Template_Id",
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
curl -X POST "${ENDPOINT}/message/v1.0/SMS/template-messages/${MESSAGE_PURPOSE}" \
     -H "Content-Type: application/json" \
     -h "x-nc-app-key: ${app_key}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
        "statsKeyId": "Statistics_Id",
        "scheduledDateTime": "2024-10-29T00:06:29+09:00",
        "confirmBeforeSend": false,
        "templateId": "Template_Id",
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

### Example of a Request Body for Sending an RCS Template Message
```json
{
  "statsKeyId": "Statistics_ID",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "templateId": "Template_ID",
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
    "brandId": "Brand_ID",
    "chatbotId": "Chat room_ID"
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

| Name | Type | Required | Description |
|-----------------------------------------|--------------------|----|------------------------------------------------------|
| sender | Object | N | Sender information |
| sender.chatbotId | String | N | Chat room ID (Required for RCS BizCenter templates) |
| content | Object | N | Message content |
| content.unsubscribePhoneNumber | String | N | 080 unsubscribe number (Required when sending RCS BizCenter templates for advertising purposes) |
| options | Object | N | Sending options |
| options.expiryOption | Integer | N | Timeout for sending attempts to devices (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour) |
| options.groupId | String | N | Group ID for RCS BizCenter statistics integration |


<span id="flow-message-sending-request"></span>

## Request to send a flow message

**Request**

```
POST /message/v1.0/flow-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| messagePurpose | Path | String | Y | Message purpose<br>NORMAL, AD, AUTH |

**Request Body**


```json
{
  "statsKeyId": "Statistics_Id",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "flowId": "Flow_ID",
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
  ],
  "flow": {
    "steps": [
      {
        "messageChannel": "SMS",
        "nextSteps": [
          {
            "messageChannel": "RCS",
            "sender": {
              "chatbotId": "Chat room_ID"
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

| Name | Type | Required | Description |
|-----------------------------------------| ----------------|----|----------------------------------------|
| statsKeyId | String | N | Statistics key ID |
| scheduledDateTime | DateTime (ISO 8601) | N | Scheduled sending time (e.g., 2024-10-29T06:29:00+09:00) |
| confirmBeforeSend | Boolean | N | Confirmation before sending (default: false) |
| flowId | String | Y | Flow ID |
| templateParameters | Object | N | Message common template parameters |
| recipients | Object Array | Y | Recipient array |
| recipients[].contacts | Object Array | Y | Recipient contact array |
| recipients[].contacts[].contactType | String | Y | Contact type |
| recipients[].contacts[].contact | String | Y | Contacts |
| recipients[].contacts[].clientReference | String | N | User Custom Fields |
| recipients[].templateParameters | Object | N | Recipient-specific template parameters |
| flow | Object | N | Flow (required if the flow uses a template that requires mandatory values) |
| flow.steps[] | Array | Y | Flow steps (refer to the flow steps specification for each message channel) | |

* Sending flow messages uses the same template parameters as sending template messages.
* The recipient's contacts must contain all of the contacts required for the message channel used by the flow.
* If the flow uses a template that requires mandatory values, you can specify the required values ​​through the flow. The flow must be configured identically to the flow with the flowId you want to send.

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "messageId": "Message_Id"
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send a flow message
POST {{endpoint}}/message/v1.0/flow-messages/{{messagePurpose}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "statsKeyId": "Statistics_Id",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "flowId": "Flow_Id",
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
     -h "x-nc-app-key: ${app_key}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
       "statsKeyId": "Statistics_Id",
       "scheduledDateTime": "2024-10-29T00:06:29+09:00",
       "confirmBeforeSend": false,
       "flowId": "Flow_Id",
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

### Flow Message Transmission Request Body - RCS Flow Step
* This is an example of flow.steps for a flow consisting of only one RCS Step.

```json
{
  "flow": {
    "steps": [
      {
        "messageChannel": "RCS",
        "sender": {
          "chatbotId": "Chat room_ID"
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

| Name | Type | Required | Description |
|-----------------------------------------| ----------------|----|-------------------------------------------|
| flow.steps[] | Array | Y | Flow Step |
| flow.steps[].messageChannel | String | Y | Message Channel<br>SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH |
| flow.steps[].sender | Object | N | Sender Information |
| flow.steps[].sender.chatbotId | String | N | Chat Room ID (Required for RCS Bizcenter templates) |
| flow.steps[].content | Object | N | Message Content |
| flow.steps[].content.unsubscribePhoneNumber | String | N | 080 Unsubscribe Number (Required for RCS Bizcenter templates sent for advertising purposes) |
| flow.steps[].options | Object | N | Sending Options |
| flow.steps[].options.expiryOption | Integer | N | Timeout for transmission attempts to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour) |
| flow.steps[].options.groupId | String | N | Group ID for RCS BizCenter statistics integration |
| flow.steps[].nextSteps[] | Object Array | N | Next step. |

<span id="cancel-message-sending-request"></span>

## Cancel a message request

Cancel a sending request for a scheduled message before it is sent, or a sent message after it is approved. Canceled messages can be viewed in the Receipts by contact view.

**Request**

```
POST /message/v1.0/messages/{messageId}/do-cancel
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| messageId | Path | String | Y | Message ID |


**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.

**Response Body**

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

**Request example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Cancel a message request
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