<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Message - Example of Sending Request Body</h1>

**Notification > Notification Hub > API v1.0 User Guide > Message - Example of Sending Request Body**


<span id="sms"></span>

## SMS

<span id="sms-sms"></span>

### SMS (Short)

```json
{
  "statsKeyId": "Statistics_Key_ID",
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
          "clientReference": "Client_Reference"
        }
      ]
    }
  ],
  "content": {
    "messageType": "SMS",
    "body": "Hi, this is NHN Cloud Notification Hub.",
  }
}
```

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| sender | Object | Y | Sender |
| sender.senderPhoneNumber | String | Y | Sender Number |
| content | Object | Y | Message Content |
| content.messageType | String | Y | SMS |
| content.body | String | Y | Content |

### LMS (Long)

```json
{
  "statsKeyId": "Statistics_Key_ID",
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
          "clientReference": "Client_Reference"
        }
      ]
    }
  ],
  "content": {
    "messageType": "LMS",
    "title": "[NHN Cloud Notification Hub] Notice",
    "body": "Hi, this is NHN Cloud Notification Hub."
  }
}
```

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| sender | Object | Y | Sender |
| sender.senderPhoneNumber | String | Y | Sender Number |
| content | Object | Y | Message Content |
| content.messageType | String | Y | LMS |
| content.title | String | Y | Title |
| content.body | String | Y | Content |

### MMS (Long Media)

```json
{
  "statsKeyId": "Statistics_Key_ID",
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
          "clientReference": "Client_Reference"
        }
      ]
    }
  ],
  "content": {
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub] Notice",
    "body": "Hi, this is NHN Cloud Notification Hub.",
    "attachmentIds": [
      "Attachment_ID"
    ]
  }
}
```

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| sender | Object | Y | Sender |
| sender.senderPhoneNumber | String | Y | Sender Number |
| content | Object | Y | Message Content |
| content.messageType | String | Y | MMS |
| content.body | String | Y | Content |
| content.attachmentIds | String Array | Y | Attachment File ID<br>Attached Image Restrictions.<br>Supported Codecs: .jpg, .jpeg<br>Number of Attached Images: 3 or less.<br>Attached Image Size: 300KB or less per image. However, if there are 3 attached images, the total size of the images must be 800KB or less.<br>Attached Image Resolution: 1,000*1,000 or less. |


<span id="rcs"></span>

## RCS

<span id="rcs-sms"></span>

### SMS

```json
{
  "statsKeyId": "Statistics_Key_ID",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "Brand_ID",
    "chatbotId": "Chat Room_ID"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "Client_Reference"
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
          "description":"Hi, this is NHN Cloud Notification Hub.",
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
| --- | --- | --- | --- |
| sender | Object | Y | Sender |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chat room ID |
| content | Object | Y | Message content |
| content.messageType | String | Y | Message type in RCS, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 opt-out number, required if the sending purpose is advertising |
| content.smsType | String | Y | SMS type, required if the message type is SMS, STANDALONE (standard) |
| content.cards | Object Array | Y | Card |
| content.cards[].title | String | N | Title |
| content.cards[].description | String | Y | Content |
| content.cards[].buttons | Object Array | N | Button |
| content.cards[].buttons[].buttonType | String | Y | Button Type<br>COMPOSE (Open Chat), CLIPBOARD (Copy), DIALER (Make a Call), MAP_SHOW (Show Map), MAP_QUERY (Search Map), MAP_SHARE (Share Current Location), URL (Connect URL), CALENDAR (Register Schedule) |
| content.cards[].buttons[].buttonJson | Object | Y | Button Json, check the format for the button type |
| options | Object | N | Sending Options |
| options.expiryOption | Integer | N | RCS message reception wait expiration period setting value (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour) |
| options.groupId | String | N | Group ID for RCS BizCenter statistics integration |

<span id="free-form-message-request-body-rcs-lms-standalone"></span>

### LMS Standard

```json
{
  "statsKeyId": "Statistics_Key_ID",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "Brand_ID",
    "chatbotId": "Chat Room_ID"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "Client_Reference"
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
          "description":"Hi, this is NHN Cloud Notification Hub.",
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
| --- | --- | --- | --- |
| sender | Object | Y | Sender |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chat room ID |
| content | Object | Y | Message content |
| content.messageType | String | Y | Message type in RCS, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 opt-out number, required if the sending purpose is advertising |
| content.lmsType | String | Y | LMS type, required if the message type is LMS, STANDALONE (Standard), FORMAT_BASIC (Basic format), FORMAT_TITLE_HIGHLIGHT (Highlighted title format), FORMAT_PARAGRAPH (Paragraph format) |
| content.cards | Object Array | Y | Card |
| content.cards[].title | String | N | Title |
| content.cards[].description | String | Y | Content |
| content.cards[].buttons | Object Array | N | Button |
| content.cards[].buttons[].buttonType | String | Y | Button Type<br>COMPOSE (Open Chat), CLIPBOARD (Copy), DIALER (Make a Call), MAP_SHOW (Show Map), MAP_QUERY (Search Map), MAP_SHARE (Share Current Location), URL (Connect URL), CALENDAR (Register Schedule) |
| content.cards[].buttons[].buttonJson | Object | Y | Button Json, Check the format for the button type |
| options | Object | N | Sending Options |
| options.expiryOption | Integer | N | RCS message reception wait expiration setting (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour) |
| options.groupId | String | N | Group ID for RCS BizCenter statistics integration |

<span id="free-form-message-request-body-rcs-lms-format-basic"></span>

### LMS Format Basic and Format Title Emphasis
  * List of mTitleMedia Icon File IDs
  * Promotion: LT-messagebase.common-jFBCKu
  * Coupon: LT-messagebase.common-LbshOv
  * Event: LT-messagebase.common-aWdsJX
  * Reservation: LT-messagebase.common-5eFcIF
  * Receipt: LT-messagebase.common-rJQ22U
  * Notification: LT-messagebase.common-j11Gtf

```json
{
  "statsKeyId": "Statistics+Key_ID",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "Brand_ID",
    "chatbotId": "Chat Room_ID"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "Client_Reference"
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
          "description":"Hi, this is NHN Cloud Notification Hub.",
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
| --- | --- | --- | --- |
| sender | Object | Y | Sender |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chat room ID |
| content | Object | Y | Message content |
| content.messageType | String | Y | Message type in RCS, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 opt-out number, required if the sending purpose is advertising |
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
| options.expiryOption | Integer | N | RCS message reception wait expiration period setting (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour) |
| options.groupId | String | N | Group ID for RCS BizCenter statistics integration |

### LMS Format Paragraph Type
* List of mTitleMedia Icon File IDs
* Promotion: LT-messagebase.common-jFBCKu
* Coupon: LT-messagebase.common-LbshOv
* Event: LT-messagebase.common-aWdsJX
* Reservation: LT-messagebase.common-5eFcIF
* Receipt: LT-messagebase.common-rJQ22U
* Notification: LT-messagebase.common-j11Gtf

```json
{
  "statsKeyId": "Statistics_Key_ID",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "Brand_ID",
    "chatbotId": "Chat Room_ID"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "Client_Reference"
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
          "description1":"Hi, this is NHN Cloud Notification Hub.",
          "title2":"Notice 2",
          "description2":"Hi, this is NHN Cloud Notification Hub.",
          "title3":"Notice 3",
          "description3":"Hi, this is NHN Cloud Notification Hub.",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Notice1 Button"
                }
              }
            },
            {},
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Notice2 Button"
                }
              }
            },
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Notice2 Button"
                }
              }
            },
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Notice3 Button"
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
| --- | --- | --- | --- |
| sender | Object | Y | Sender |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chat room ID |
| content | Object | Y | Message content |
| content.messageType | String | Y | Message type in RCS, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 opt-out number, required if the sending purpose is advertising |
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
| content.cards[].buttons[].buttonType | String | Y | Button Type<br>COMPOSE (Open Chat Room), CLIPBOARD (Copy), DIALER (Make a Call), MAP_SHOW (Show Map), MAP_QUERY (Search Map), MAP_SHARE (Share Current Location), URL (Connect URL), CALENDAR (Register Schedule) |
| content.cards[].buttons[].buttonJson | Object | Y | Button JSON, check the format for the button type |
| options | Object | N | Sending Options |
| options.expiryOption | Integer | N | RCS Message Reception Wait Expiration Period Setting (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour) |
| options.groupId | String | N | Group ID for RCS BizCenter Statistics Integration |

### MMS Horizontal, Vertical

```json
{
  "statsKeyId": "Statistics_Key_ID",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "Brand_ID",
    "chatbotId": "Chat Room_ID"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "Client_Reference"
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
          "description":"Hi, this is NHN Cloud Notification Hub.",
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
| --- | --- | --- | --- |
| sender | Object | Y | Sender |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chat room ID |
| content | Object | Y | Message content |
| content.messageType | String | Y | Message type in RCS, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 opt-out number, required if the sending purpose is advertising |
| content.mmsType | String | Y | MMS type, required if the message type is MMS, HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL |
| content.cards | Object Array | Y | Cards |
| content.cards[].title | String | N | Title |
| content.cards[].description | String | Y | Content |
| content.cards[].attachmentId | String | Y | Attachment ID |
| content.cards[].buttons | Object Array | N | Button |
| content.cards[].buttons[].buttonType | String | Y | Button Type<br>COMPOSE (Open Chat), CLIPBOARD (Copy), DIALER (Make a Call), MAP_SHOW (Show Map), MAP_QUERY (Search Map), MAP_SHARE (Share Current Location), URL (Connect URL), CALENDAR (Register Schedule) |
| content.cards[].buttons[].buttonJson | Object | Y | Button Json, Check the format for the button type |
| options | Object | N | Sending Options |
| options.expiryOption | Integer | N | RCS message reception wait expiration period setting (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour) |
| options.groupId | String | N | Group ID for RCS BizCenter statistics integration |

### MMS Carousel

```json
{
  "statsKeyId": "Statistics_Key_ID",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "Brand_ID",
    "chatbotId": "Chat Room_ID"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678",
          "clientReference": "Client_Reference"
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
          "description":"Hi, this is NHN Cloud Notification Hub.",
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
          "description":"Hi, this is NHN Cloud Notification Hub.",
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
          "description":"Hi, this is NHN Cloud Notification Hub.",
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
| --- | --- | --- | --- |
| sender | Object | Y | Sender |
| sender.brandId | String | Y | Brand ID |
| sender.chatbotId | String | Y | Chat room ID |
| content | Object | Y | Message content |
| content.messageType | String | Y | Message type in RCS, SMS, LMS, MMS, RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080 opt-out number, required if the sending purpose is advertising |
| content.mmsType | String | Y | MMS type, required if the message type is MMS, HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL |
| content.cards | Object Array | Y | Cards |
| content.cards[].title | String | N | Title |
| content.cards[].description | String | Y | Content |
| content.cards[].attachmentId | String | Y | Attachment ID |
| content.cards[].buttons | Object Array | N | Button |
| content.cards[].buttons[].buttonType | String | Y | Button Type<br>COMPOSE (Open Chat), CLIPBOARD (Copy), DIALER (Make a Call), MAP_SHOW (Show Map), MAP_QUERY (Search Map), MAP_SHARE (Share Current Location), URL (Connect URL), CALENDAR (Register Schedule) |
| content.cards[].buttons[].buttonJson | Object | Y | Button Json, Check the format for the button type |
| options | Object | N | Sending Options |
| options.expiryOption | Integer | N | RCS message reception wait expiration period setting (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour) |
| options.groupId | String | N | Group ID for RCS BizCenter statistics integration |


<span id="free-form-message-request-body-friendtalk-text"></span>

## FriendTalk

### Text Type

* Since AlimTalk can only be sent after template registration and approval, only template and flow messages can be sent.
* For AlimTalk's' **sender** and **content** fields, refer to the **request body** in **Sending a template message**.
* FRIENDTALK only supports the NORMAL sending profile type. Sending will fail if a sender key from the GROUP sending profile type is used.

```json
{
    "statsKeyId": "Statistics_Key_ID",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "Outgoing Profile_Outgoing Key"
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
      "content": "Delivery_Contents",
      "buttons": [
        {
        "type": "WL",
        "name": "Button_Name",
        "linkMo": "Mobile_Link",
        "linkPc": "PC_Link",
        "schemeIos": "iOS_App_Link",
        "schemeAndroid": "Android_App_Link",
        "bizFormKey": "BizForm_Key"
        }
      ],
      "coupon": {
        "title": "Coupon Title",
        "description": "Coupon Detail Description",
        "linkMo": "Mobile Link",
        "linkPc": "PC Link",
        "schemeIos": "iOS App Link",
        "schemeAndroid": "Android App Link"
      }
    }
}
```


| Name | Type | Required | Description |
| --- | --- |----|--------------------------------------------------------------|
| sender | Object | Y | Sender |
| sender.senderKey | Object | Y | Sender Profile_SenderKey |
| content | Object | Y | Message Content |
| content.messageType | String | Y | Message Type |
| content.content | String | Y | Content |
| content.buttons | Object Array | N | Button |
| content.buttons[].type | String | Y | Button Type <br>WL (Web Link), AL (App Link), BK (Bot Keyword), MD (Message Delivery), BF (Business Form) |
| content.buttons[].name | String | Y | Button Name |
| content.buttons[].linkMo | String | N | Link Mobile, Required if button type is WL |
| content.buttons[].linkPc | String | N | Link PC |
| content.buttons[].schemeIos | String | N | iOS app link |
| content.buttons[].schemeAndroid | String | N | Android app link |
| content.buttons[].bizFormKey | String | N | BizForm key, required if button type is BF |
| content.coupon | Object | N | Coupon |
| content.coupon.title | String | Y | Title, limited to 5 formats<br>"${number} won discount coupon" must be between 1 and 99,999,999<br>"${number}% discount coupon" must be between 1 and 100<br>"Shipping discount coupon"<br><br>"${7 characters or less} free coupon"<br>"${7 characters or less} UP coupon" |
| content.coupon.description | String | Y | Coupon Description (up to 12 characters for plain text, image, and carousel feeds / up to 18 characters for wide image and wide item list types) |
| content.coupon.linkMo | String | N | Mobile Link |
| content.coupon.linkPc | String | N | PC Link |
| content.coupon.schemeIos | String | N | iOS App Link |
| content.coupon.schemeAndroid | String | N | Android App Link |

<span id="free-form-message-request-body-friendtalk-image"></span>

### Image / Wide Image Type

* FRIENDTALK only supports the NORMAL sending profile type. Sending messages using a GROUP sending profile type key will fail.

```json
{
    "statsKeyId": "Statistics_Key_ID",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "Outgoing Profile_Outgoing Key"
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
      "content": "Delivery_Contents",
      "attachmentId": "Attachment_File_ID",
      "imageLink": "Image_Link_URL",
      "buttons": [
        {
        "type": "WL",
        "name": "Button_Name",
        "linkMo": "Mobile_Link",
        "linkPc": "PC_Link",
        "schemeIos": "iOS_App_Link",
        "schemeAndroid": "Android_App_Link",
        "bizFormKey": "BizForm_Key"
        }
      ],
      "coupon": {
        "title": "Coupon Title",
        "description": "Coupon Detail Description",
        "linkMo": "Mobile Link",
        "linkPc": "PC Link",
        "schemeIos": "iOS App Link",
        "schemeAndroid": "Android App Link"
      }
    }
}
```

| Name | Type | Required | Description |
| --- |---------------|----|---------------------------------------------------------------|
| sender | Object | Y | Sender |
| sender.senderKey | Object | Y | Sender Profile_SenderKey |
| content | Object | Y | Message Content |
| content.messageType | String | Y | Message Type |
| content.content | String | Y | Content |
| content.attachmentId | String | Y | Attachment ID |
| content.imageLink | String | N | Image Link |
| content.buttons | Object Array | N | Button |
| content.buttons[].type | String | Y | Button Type <br>WL (Web Link), AL (App Link), BK (Bot Keyword), MD (Message Forwarding), BF (Business Form) |
| content.buttons[].name | String | Y | Button Name |
| content.buttons[].linkMo | String | N | Link Mobile, required if button type is WL |
| content.buttons[].linkPc | String | N | Link PC |
| content.buttons[].schemeIos | String | N | iOS app link |
| content.buttons[].schemeAndroid | String | N | Android app link |
| content.buttons[].bizFormKey | String | N | BizForm key, required if button type is BF |
| content.coupon | Object | N | Coupon |
| content.coupon.title | String | Y | Title, limited to 5 formats<br>"${number} won discount coupon" must be between 1 and 99,999,999<br>"${number}% discount coupon" must be between 1 and 100<br>"Shipping discount coupon"<br><br>"${7 characters or less} free coupon"<br>"${7 characters or less} UP coupon" |
| content.coupon.description | String | Y | Coupon detailed description (up to 12 characters for plain text, image, and carousel feed / up to 18 characters for wide image and wide item list) |
| content.coupon.linkMo | String | N | Link mobile |
| content.coupon.linkPc | String | N | Link PC |
| content.coupon.schemeIos | String | N | iOS app link |
| content.coupon.schemeAndroid | String | N | Android app link |

<span id="free-form-message-request-body-friendtalk-wide-itemlist"></span>

### Wide Item List

* FRIENDTALK only supports the NORMAL sender profile type. Sending will fail if a sender key from the GROUP sender profile type is used.

```json
{
    "statsKeyId": "Statistics_Key_ID",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "Outgoing Profile_Outgoing Key"
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
          "linkMo": "Mobile_Link",
          "linkPc": "PC_Link",
          "schemeIos": "iOS_App_Link",
          "schemeAndroid": "Android_App_Link",
          "bizFormKey": "BizForm_Key"
        }
      ],
      "header": "Header",
      "item": {
          "list": [{
            "title": "Item_Title",
            "attachmentId": "Attachment_ID",
            "linkMo": "Mobile_Link",
            "linkPc": "PC_Link",
            "schemeIos": "iOS_App_Link",
            "schemeAndroid": "Android_App_Link"
          },
          {
            "title": "Item_Title",
            "attachmentId": "Attachment_ID",
            "linkMo": "Mobile_Link",
            "linkPc": "PC_Link",
            "schemeIos": "iOS_App_Link",
            "schemeAndroid": "Android_App_Link"
          },
          {
          "title": "Item_Title",
          "attachmentId": "Attachment_ID",
          "linkMo": "Mobile_Link",
          "linkPc": "PC_Link",
          "schemeIos": "iOS_App_Link",
          "schemeAndroid": "Android_App_Link"
          }
        ]
      },
      "coupon": {
        "title": "Coupon_Title",
        "description": "Coupon_Details",
        "linkMo": "Mobile_Link",
        "linkPc": "PC_Link",
        "schemeIos": "iOS_App_Link",
        "schemeAndroid": "Android_App_Link"
      }
    }
}
```

| Name | Type | Required | Description |
|----------------------------------|---------------|----|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| sender | Object | Y | Sender |
| sender.senderKey | Object | Y | Sender Profile_Sender Key |
| content | Object | Y | Message Content |
| content.messageType | String | Y | Message Type |
| content.buttons | Object Array | N | Button |
| content.buttons[].type | String | Y | Button Type <br>WL (Web Link), AL (App Link), BK (Bot Keyword), MD (Message Delivery), BF (Business Form) |
| content.buttons[].name | String | Y | Button Name |
| content.buttons[].linkMo | String | N | Link Mobile, Required if button type is WL |
| content.buttons[].linkPc | String | N | PC Link |
| content.buttons[].schemeIos | String | N | iOS app Link |
| content.buttons[].schemeAndroid | String | N | Android app Link |
| content.buttons[].bizFormKey | String | N | BizForm Key, required if button type is BF |
| content.header | String | Y | Header |
| content.item | Object | Y | Wide Item |
| content.item.list | Object Array | Y | Wide Item List (Minimum 3, Maximum 4) |
| content.item.list[].title | String | Y | Item Title (Maximum 25 characters for the first item, Maximum 30 characters for items 2-4) |
| content.item.list[].attachmentId | String | Y | Attachment ID |
| content.item.list[].linkMo | String | Y | Mobile Web Link |
| content.item.list[].linkPc | String | Y | PC web link |
| content.item.list[].schemeIos | String | Y | iOS app link |
| content.item.list[].schemeAndroid | String | Y | Android app link |
| content.coupon | Object | N | Coupon |
| content.coupon.title | String | Y | Title, limited to 5 formats<br>"${number} won discount coupon" The number must be between 1 and 99,999,999<br>"${number}% discount coupon" The number must be between 1 and 100<br>"Shipping discount coupon"<br><br>"${7 characters or less} free coupon"<br>"${7 characters or less} UP coupon" |
| content.coupon.description | String | Y | Coupon Description (up to 12 characters for plain text, image, and carousel feeds / up to 18 characters for wide image and wide item list types) |
| content.coupon.linkMo | String | N | Mobile Link |
| content.coupon.linkPc | String | N | PC Link |
| content.coupon.schemeIos | String | N | iOS App Link |
| content.coupon.schemeAndroid | String | N | Android App Link |

<span id="free-form-message-request-body-friendtalk-carousel"></span>

### Carousel Feed

* FRIENDTALK only supports the NORMAL sending profile type. Sending messages using a GROUP sending profile type key will fail.

```json
{
    "statsKeyId": "Statistics_Key_ID",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "Outgoing Profile_Outgoing Key"
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
            "message": "Carousel_Item_Message",
            "attachment": {
              "buttons": [
                {
                  "type": "WL",
                  "name": "Button_Name",
                  "linkMo": "Mobile_Link",
                  "linkPc": "PC_Link",
                  "schemeIos": "iOS_App_Link",
                  "schemeAndroid": "Android_App_Link"
                }
              ],
              "image": {
                "attachmentId": "Attachment_ID",
                "imageLink": "Image_Link__URL"
              },
              "coupon": {
                "title": "Coupon_Title",
                "description": "Coupon_Details",
                "linkMo": "Mobile_Link",
                "linkPc": "PC_Link",
                "schemeIos": "iOS_App_Link",
                "schemeAndroid": "Android_App_Link"
              }
            }
          },
          {
            "header": "Carousel_Item_Title",
            "message": "Carousel_Item_Message",
            "attachment": {
              "buttons": [
                {
                  "type": "WL",
                  "name": "Button_Name",
                  "linkMo": "Mobile_Link",
                  "linkPc": "PC_Link",
                  "schemeIos": "iOS_App_Link",
                  "schemeAndroid": "Android_App_Link"
                }
              ],
              "image": {
                "attachmentId": "Attachment_ID",
                "imageLink": "Image_Link_URL"
              },
              "coupon": {
                "title": "Coupon_Title",
                "description": "Coupon_Details",
                "linkMo": "Mobile_Link",
                "linkPc": "PC_Link",
                "schemeIos": "iOS_App_Link",
                "schemeAndroid": "Android_App_Link"
              }
            }
          }
        ],
        "tail": {
          "linkMo": "Mobile_Link",
          "linkPc": "PC_Link",
          "schemeAndroid": "Android_App_Link",
          "schemeIos": "iOS_App_Link"
        }
      }
    }
}
```

| Name | Type | Required | Description |
|------------------------------------------------------------|---------------|----|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| sender | Object | Y | Sender |
| sender.senderKey | Object | Y | SenderProfile_SenderKey |
| content | Object | Y | Message Content |
| content.messageType | String | Y | Message Type |
| content.carousel | Object | Y | Carousel |
| content.carousel.list | Object Array | Y | Carousel List (Minimum 2, Maximum 10) |
| content.carousel.list[].header | String | Y | Carousel Item Title (Maximum 20 characters), Only Available in Carousel Feed Type |
| content.carousel.list[].message | String | Y | Carousel Item Message (Maximum 180 characters), Only Available in Carousel Feed Type |
| content.carousel.list[].attachment | Object | N | Carousel item image, button information |
| content.carousel.list[].attachment.buttons | Object Array | N | Button list (up to 2) |
| content.carousel.list[].attachment.buttons[].type | String | Y | Button type <br>WL (Web Link), AL (App Link), BK (Bot Keyword), MD (Message Delivery), BF (Business Form) |
| content.carousel.list[].attachment.buttons[].name | String | Y | Button name |
| content.carousel.list[].attachment.buttons[].linkMo | String | N | Link mobile, required if button type is WL |
| content.carousel.list[].attachment.buttons[].linkPc | String | N | Link PC |
| content.carousel.list[].attachment.buttons[].schemeIos | String | N | iOS app link |
| content.carousel.list[].attachment.buttons[].schemeAndroid | String | N | Android app link |
| content.carousel.list[].attachment.image | Object | Y | Carousel image |
| content.carousel.list[].attachment.image.attachmentId | String | Y | Attachment id |
| content.carousel.list[].attachment.image.imageLink | String | N | Image link URL |
| content.carousel.list[].attachment.coupon | Object | N | Coupon |
| content.carousel.list[].attachment.coupon.title | String | Y | Title, limited to 5 formats<br>"${number} won discount coupon" The number must be 1 to 99,999,999<br>"${number}% discount coupon" The number must be 1 to 100<br>"Shipping discount coupon"<br><br>"${7 characters or less} free coupon"<br>"${7 characters or less} UP coupon" |
| content.carousel.list[].attachment.coupon.description | String | Y | Coupon detailed description (up to 12 characters for plain text, image, and carousel feed / up to 18 characters for wide image and wide item list) |
| content.carousel.list[].attachment.coupon.linkMo | String | N | Link mobile |
| content.carousel.list[].attachment.coupon.linkPc | String | N | Link PC |
| content.carousel.list[].attachment.coupon.schemeIos | String | N | iOS app link |
| content.carousel.list[].attachment.coupon.schemeAndroid | String | N | Android app link |
| content.carousel.tail | Object | N | Carousel Show More Button Information |
| content.carousel.tail.linkMo | String | Y | Mobile web link |
| content.carousel.tail.linkPc | String | N | Mobile web link |
| content.carousel.tail.schemeIos | String | N | Mobile web link |
| content.carousel.tail.schemeAndroid | String | N | Mobile web link |

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
    "title": "[NHN Cloud Notification Hub] Notice",
    "body": "Hi, this is NHN Cloud Notification Hub.",
    "attachmentIds": [
      "Attachment_ID"
    ]
  }
}
```

| Name | Type | Required | Description |
| --- |--------------| --- | --- |
| sender | Object | N | Sender, required for message channels other than push |
| sender.senderMailAddress | Object | N | Sender email address |
| content | Object | Y | Message content |
| content.title | Object | Y | Title |
| content.Object | Y | Content |
| content.attachmentIds | String Array | N | Attachment ID |

* The domain of the sender's email address must be verified.
* Up to 10 attachments can be uploaded, each with a maximum size of 30MB.
* The total size of attachments cannot exceed 30MB. * You can attach up to 30MB, but depending on the attachment limit policy of the receiving email system (e.g., gmail.com, naver.com), it may be rejected as **exceeding the limit** or may increase the spam rating, so we recommend keeping attachments under 10MB.
* Only **EMAIL_ADDRESS** can be used in the **recipients[].contacts[].contactType** field.
* Enter the recipient's email address in the **recipients[].contacts[].contact** field.

<span id="free-form-message-request-body-push"></span>

### Push

```json
{
  "statsId": "Statistics_ID",
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
    "body" : "<b>Launch Event</b> <i>Check Notices</i>",
    "richMessage" : {
      "buttons" : [{
        "name" : "Button Name",
        "submitName": "Name of Send Button",
        "buttonType" : "REPLY",
        "link" : "myapp://product_detail?product_id=1234",
        "hint" : "Hint for Button"
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
        "key" : "Group Key",
        "description" : "Description for Group"
      }
    },
    "customKey" : "customValue"
  }
}
```

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| content | Object | Y | Message content |
| content.unsubscribePhoneNumber | String | N | Representative number for unsubscribing from push messages |
| content.unsubscribeGuide | String | N | Guide for unsubscribing from push messages |
| content.title | String | Y | Title |
| content.body | String | Y | Content |
| content.style.useHtmlStyle | Boolean | Y | Use HTML style (Android only) |
| content.richMessage | Object | N | Required when using rich messages |
| content.richMessage.buttons | Object Array | N | Buttons added to rich messages, up to 3 allowed |
| content.richMessage.buttons.name | String | N | Button name |
| content.richMessage.buttons.buttonType | String | N | Button types: REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS |
| content.richMessage.buttons.link | String | N | Link to link to when the button is clicked |
| content.richMessage.buttons.hint | String | N | Hint for the button |
| content.richMessage.media | Object | N | Media added to the rich message |
| content.richMessage.media.source | String | N | Address of the media (can be URL or LOCAL_RESOURCE) |
| content.richMessage.media.mediaType | String | N | Media types: IMAGE, GIF, VIDEO, AUDIO. Android only supports IMAGE |
| content.richMessage.media.expandable | Boolean | N | Whether to use the expand function when clicking the media on Android |
| content.richMessage.androidMedia | Object | N | Media for Android devices only. Same as the media type |
| content.richMessage.iosMedia | Object | N | Media for iOS devices only. Same as the media format |
| content.richMessage.largeIcon | Object | N | Large icon added to a rich message, supported only by Android |
| content.richMessage.largeIcon.source | String | Y | Icon address |
| content.richMessage.group | Object | N | Ability to group multiple messages, supported only by Android |
| content.richMessage.group.key | String | Y | Group key |
| content.richMessage.group.description | String | Y | Group description |
| content.customKey | Object Array or String Array | N | Custom key and value |

* Push does not require a **sender** field.
* Push can create a **content** field by adding user-defined keys and values. * The **recipients[].contacts[].contactType** field must be one of **TOKEN_FCM**, **TOKEN_APNS**, **TOKEN_ADM**, **TOKEN_APNS_SANDBOX**, **TOKEN_APNS_VOIP**, or **TOKEN_APNS_VOIP_SANDBOX**.
* Enter **push token** in the **recipients[].contacts[].contact** field.