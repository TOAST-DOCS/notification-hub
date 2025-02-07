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

| Name | Type | Required  | Description |
| --- | --- |-----| --- |
| statsKeyId | String | N   | Statistics Key ID |
| scheduledDateTime | DateTime(ISO 8601) | N   | Scheduled send date (e.g., 2024-10-29T06:29:00+09:00) |
| confirmBeforeSend | Boolean | N   | Whether to verify before sending (default false) |
| sender | Object | Y/N | Sender, Push, and other message channels are required |
| recipients | Object Array | Y   | Receiver Array |
| recipients[].contacts | Object Array | Y   | Arrange the recipient's contacts |
| recipients[].contacts[].contactType | String | Y   | Contact types |
| recipients[].contacts[].contact | String | Y   | Contact |
| content | Object | Y   | Message content |

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
### Send a professional message
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

## Example detailed request body by message channel

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


<span id="free-form-message-request-body-rcs"></span>

### RCS

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
    "title": "[NHN Cloud Notification Hub] Announcement",
    "body": "Hello. This is NHN Cloud Notification Hub",
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
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"Go to homepage\"}}"
            },
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"Go to homepage\"}}"
            }
          ]
        }
    ],
    "buttons": [
        {
            "buttonType": "URL",
            "buttonJson": "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"Go to homepage\"}}"
        }
    ]
  }
}
```


| Name | Type | Required | Description                                                                                                                                                       |
| --- | --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------| 
| sender | Object | Y | Sender                                                                                                                                                      |
| sender.brandId | Object | N | Brand ID                                                                                                                                                  |
| sender.chatbotId | Object | N | Room ID                                                                                                                                                  |
| content | Object | Y | Message content                                                                                                                                                   |
| content.messageType | String | Y | Message types in RCS, SMS, LMS, MMS, RCS_TEMPLATE                                                                                                                |
| content.unsubscribePhoneNumber | String | Y | 080 unsubscribe number, required if the purpose of the send is advertising                                                                                                                           |
| content.title | Object | Y | Title                                                                                                                                                       |
| content.Object | Y | Content |
| content.mmsType | Object | N | MMS type, required if message type is MMS, HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL, CAROUSEL_MIDDLE, CAROUSEL_SMALL                                                |
| content.messagebaseId | Object | N | Required if message type is RCS_TEMPLATE, template ID registered in RCS Biz Center                                                                                                 |
| content.cards | Object Array | Y | Card                                                                                                                                                       |
| content.cards[].title | String | Y | Title                                                                                                                                                       |
| content.cards[].description | String | Y | Content                                                                                                                                                       |
| content.cards[].media | String | Y | Attachment ID                                                                                                                                                  |
| content.cards[].buttons | Object Array | Y | Button                                                                                                                                                       |
| content.cards[].button.buttonType | String | Y | Button type<br>COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make a call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share current location), URL (link to URL), CALENDAR (add event) |
| content.cards[].button.buttonJson | String | Y | Button Json, check formatting for button type                                                                                                                                |
| content.buttons | Object Array | Y | Button |
| content.buttons[].buttonType | String | Y | Button type<br>COMPOSE (open chat room), CLIPBOARD (copy), DIALER (make a call), MAP_SHOW (show map), MAP_QUERY (search map), MAP_SHARE (share current location), URL (link to URL), CALENDAR (add event) |
| content.buttons[].buttonJson | String | Y | Button JSON-formatted string                                                                                                                                          |
| content.attachmentIds | String Array | N | Array of attachment IDs                                                                                                                                             |


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
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678"
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
* You can upload **up to 10**attachments, and they can be **no larger than 30 MB**.
* Attachments can't **total**more than **30 MB**.
* You can attach up to **30 MB**, but depending on the attachment limit policy of the receiving email system (gmail.com, naver.com, etc.), we recommend attachments that are **10 MB or less, as they may be rejected for **exceeding the limit** or result in a higher spam flagging rate.

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
  ]
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
  "flowId": "Template_Id",
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

| Name                 | Type             | Required | Description                                     |
|--------------------| ----------------| --- |----------------------------------------|
| statsKeyId         | String         | N | Statistics Key ID                               |
| scheduledDateTime  | DateTime(ISO 8601) | N | Scheduled send date (e.g., 2024-10-29T06:29:00+09:00) |
| confirmBeforeSend  | Boolean        | N | Whether to verify before sending (default false)                  |
| flowId             | String         | Y | Template ID                                |
| templateParameters | Object         | N | Message common template parameters                        |
| recipients         | Object Array          | Y | Receiver Array                                 |
| recipients[].contacts | Object Array          | Y | Arrange the recipient's contacts                            |
| recipients[].contacts[].contactType | String         | Y | Contact types                                 |
| recipients[].contacts[].contact | String         | Y | Contact                                    |
| recipients[].templateParameters | Object         | N | Recipient-specific template parameters                         |

* Sending flow messages uses the same template parameters as sending template messages.
* The recipient's contacts must contain all of the contacts required for the message channel used by the flow.

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
  "flowId": "Template_Id",
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
       "flowId": "Template_Id",
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