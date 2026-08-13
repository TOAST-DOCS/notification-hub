<!-- pre-align:aligned sig=8c77b572b6aa -->

<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>Received Results by Contacts</h1>

**Notification > Notification Hub > API v1.0 User Guide > Received Results by Contacts**



<span id="contactDeliveryResultV1x0001ReadContactDeliveryResults"></span>

<a id="retrieve-a-list-of-received-results-by-contacts"></a>
## Retrieve a List of Received Results by Contacts { #retrieve-a-list-of-received-results-by-contacts }

Retrieve the sending and reception results of requested messages by recipient contact.

For example, if you send two flow messages consisting of an email and SMS template to 10 recipients with email addresses and phone numbers, 40 items will be displayed when viewing the reception results list by contact. (2 contacts X 10 recipients X 2 flow messages = 40 reception results per contact.)
You can retrieve reception results by contact using various retrieve conditions.


**Request**

```
GET /message/v1.0/contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | App Key |
| X-NHN-Authorization | Header | String | Y | Access Token |
| messageId | Query | String | N | Message ID. This value is generated when a message sending request is received. |
| templateId | Query | String | N | Template ID. |
| flowId | Query | String | N | Flow ID. |
| statsKeyId | Query | String | N | Statistics Key ID. |
| sender | Query | String | N | Sender information. |
| contact | Query | String | N | Contact information. |
| messageChannel | Query | Enum | X | Message channel.<br>[SMS(SMS), ALIMTALK(AlimTalk), BRANDMESSAGE(Brand Message), RCS(RCS), EMAIL(Email), PUSH(Push)] |
| messagePurpose | Query | Enum | X | The message purpose.<br>[NORMAL(Normal), AD(Ad), AUTH(Auth)] |
| statuses | Query | Enum | X | Message status. You can view it as a send result.<br> When a message sending request is received, the message status is set to REQUESTED.<br> <br>[REQUESTED(Requested), SCHEDULED(Scheduled), READY(Ready), CONFIRM_WAITED(Confirm Waited), WAITED(Waited), IN_PROGRESS(In Progress), SENT(Sent), SEND_FAILED(Send Failed), DELIVERED(Delivered), DELIVERY_FAILED(Delivery Failed), CANCELED(Canceled)] |
| scheduled | Query | Boolean | N | Whether to schedule sending. |
| confirmBeforeSend | Query | Boolean | N | Whether to send after approval. |
| createdDateTimeFrom | Query | DateTime | N | The request start date and time. The default is 7 days ago. |
| createdDateTimeTo | Query | DateTime | N | The request end date and time. The default is the current date and time. |
| limit | Query | Number | N | The number of messages to retrieve. The default is 10. |
| offset | Query | Number | N | The starting position of the messages to retrieve. The default is 0. |

* The maximum query period for **createdDateTimeFrom** and **createdDateTimeTo** is 7 days.


**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not request a request body.



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "contactDeliveryResults" : [ {
    "messageId" : "Message ID",
    "recipientIndex" : 0,
    "contactIndex" : 0,
    "contactType" : "PHONE_NUMBER",
    "contact" : "01012345678",
    "sender" : {
      "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
      "senderProfileId" : "@nhnCloud",
      "senderProfileType" : "GROUP",
      "senderPhoneNumber" : "01012341234",
      "senderMailAddress" : "abcde@nhn.com",
      "brandId" : "AR.lj0eOjEI7Y",
      "chatbotId" : "01012341234"
    },
    "templateId" : "Tj3nE8dq",
    "flowId" : "R2m9Kv0x",
    "statsKeyId" : "aA123456",
    "clientReference" : "Custom Field",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "options" : {
      "expiryOption" : 1,
      "groupId" : "20240814125609swLmoZTsGr0"
    },
    "confirmBeforeSend" : false,
    "confirmedDateTime" : "2024-10-29T06:00:01.000+09:00",
    "scheduled" : false,
    "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
    "status" : "REQUESTED",
    "resultCode" : "5.0.0",
    "resultMessage" : "Success",
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
      "thumbnailUrl" : "https://example.com/thumbnail.jpg"
    },
    "additionalProperty" : { },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "sentDateTime" : "2024-10-29T06:00:01.000+09:00",
    "deliveredDateTime" : "2024-10-29T06:00:01.000+09:00",
    "openedDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ],
  "totalCount" : 1
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | The result message of the request.<br>Default: SUCCESS |
| contactDeliveryResults | Array | O | The result of sending the message. |
| contactDeliveryResults[].messageId | String | O | The message ID. |
| contactDeliveryResults[].recipientIndex | Integer | O | The recipient index. |
| contactDeliveryResults[].contactIndex | Integer | O | The contact index. |
| contactDeliveryResults[].contactType | String | O | Contact Type<br>[PHONE_NUMBER(Phone number), EMAIL_ADDRESS(Email address), TOKEN_ADM(Amazon Device Messaging token), TOKEN_FCM(Firebase Cloud Messaging token), TOKEN_APNS(Apple Push Notification service token), TOKEN_APNS_SANDBOX(APNS Sandbox token), TOKEN_APNS_SANDBOX_VOIP(APNS Sandbox VoIP token), TOKEN_APNS_VOIP(APNS VoIP token)] |
| contactDeliveryResults[].contact | String | O | Contact information. |
| contactDeliveryResults[].sender | Object | X | Sender information by channel.<br>- ALIMTALK : senderKey, senderProfileId, senderProfileType<br>- SMS : senderPhoneNumber<br>- EMAIL : senderMailAddress<br>- RCS : brandId, chatbotId<br> |
| contactDeliveryResults[].sender.senderKey | String | X | Sender profile sender key |
| contactDeliveryResults[].sender.senderProfileId | String | X | KakaoTalk channel name |
| contactDeliveryResults[].sender.senderProfileType | String | X | Sender profile type<br>[GROUP (group sender profile), NORMAL (normal sender profile)] |
| contactDeliveryResults[].sender.senderPhoneNumber | String | X | Sender number |
| contactDeliveryResults[].sender.senderMailAddress | String | X | Sender email address |
| contactDeliveryResults[].sender.brandId | String | X | Brand ID |
| contactDeliveryResults[].sender.chatbotId | String | X | Chat room (chatbot) ID |
| contactDeliveryResults[].templateId | String | X | Template ID |
| contactDeliveryResults[].flowId | String | X | Flow ID |
| contactDeliveryResults[].statsKeyId | String | X | Statistics key ID |
| contactDeliveryResults[].clientReference | String | X | Custom field |
| contactDeliveryResults[].messageChannel | String | O | Message channel<br>[SMS(SMS), ALIMTALK(AlimTalk), BRANDMESSAGE(Brand Message), EMAIL(Email), RCS(RCS), PUSH(Push)] |
| contactDeliveryResults[].messagePurpose | String | O | Sent content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| contactDeliveryResults[].options | Object | X | Options by channel. |
| contactDeliveryResults[].options.expiryOption | Integer | X | (RCS) The time the carrier attempts to send to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour)<br>Default: 1 |
| contactDeliveryResults[].options.groupId | String | X | (RCS) Group ID for RCS Biz Center statistics integration [Guide](../console-guide/send-a-message/#RCS) (up to 20 bytes) |
| contactDeliveryResults[].confirmBeforeSend | Boolean | O | Whether to send after confirmation. |
| contactDeliveryResults[].confirmedDateTime | String | X | The time the message sending was confirmed. |
| contactDeliveryResults[].scheduled | Boolean | O | Whether to schedule sending. |
| contactDeliveryResults[].scheduledDateTime | String | X | Scheduled delivery time. |
| contactDeliveryResults[].status | String | O | Delivery/reception status. <br>[REQUESTED, CONFIRM_WAITED, WAITED, SCHEDULED, IN_PROGRESS, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED, CANCELED] |
| contactDeliveryResults[].resultCode | String | X | Delivery result code. The value varies depending on the message channel. |
| contactDeliveryResults[].resultMessage | String | X | Delivery result message. |
| contactDeliveryResults[].templateParameters | Object | X | Template parameters. It consists of a pair of keys (key, placeholder) and values ​​(value).<br><br>You cannot specify template parameters for each recipient in group delivery.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| contactDeliveryResults[].imageParameters | Array | X | Image parameters per recipient. Used only for Brand Message. |
| contactDeliveryResults[].imageParameters[].attachmentId | String | X | Attachment ID |
| contactDeliveryResults[].imageParameters[].imageUrl | String | X | Image URL |
| contactDeliveryResults[].imageParameters[].imageLink | String | X | URL to navigate to when the image is clicked |
| contactDeliveryResults[].videoParameter | Object | X | Video parameters per recipient. Used only for Brand Message. |
| contactDeliveryResults[].videoParameter.videoUrl | String | X | KakaoTV video URL |
| contactDeliveryResults[].videoParameter.thumbnailAttachmentId | String | X | Thumbnail image attachment ID |
| contactDeliveryResults[].videoParameter.thumbnailUrl | String | X | Video thumbnail image URL |
| contactDeliveryResults[].additionalProperty | Object | X | Additional properties of the message channel. |
| contactDeliveryResults[].createdDateTime | String | O | The time the message was created. |
| contactDeliveryResults[].sentDateTime | String | X | The time the message was sent. |
| contactDeliveryResults[].deliveredDateTime | String | X | The time the message was received. |
| contactDeliveryResults[].openedDateTime | String | X | The time the message was opened. |
| contactDeliveryResults[].updatedDateTime | String | X | The time the message was modified. |
| totalCount | Integer | O | The total number of message delivery results retrieved. |

**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve Received Results by Contacts

GET {{endpoint}}/message/v1.0/contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/message/v1.0/contact-delivery-results" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="contactDeliveryResultV1x0002ReadFinalContactDeliveryResults"></span>

<a id="retrieve-a-list-of-the-final-send-status-messages"></a>
## Retrieve a List of the Final Send Status Messages { #retrieve-a-list-of-the-final-send-status-messages }

View a list of message results after the sending process has completed.<br>
Final sending statuses include "SEND_FAILED (Delivery Failed)," "DELIVERED (Delivery Successful)," "DELIVERY_FAILED (Delivery Failed)," and "CANCELED (Canceled)."


**Request**

```
GET /message/v1.0/final-contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | App Key |
| X-NHN-Authorization | Header | String | Y | Access Token |
| messageId | Query | String | N | Message ID. This value is generated when a message sending request is received. |
| templateId | Query | String | N | Template ID. |
| flowId | Query | String | N | Flow ID. |
| statsKeyId | Query | String | N | Statistics Key ID. |
| sender | Query | String | N | Sender information. |
| contact | Query | String | N | Contact information. |
| messageChannel | Query | Enum | X | Message channel.<br>[SMS(SMS), ALIMTALK(AlimTalk), BRANDMESSAGE(Brand Message), RCS(RCS), EMAIL(Email), PUSH(Push)] |
| messagePurpose | Query | Enum | X | The message purpose.<br>[NORMAL(Normal), AD(Ad), AUTH(Auth)] |
| scheduled | Query | Boolean | N | Whether to schedule sending. |
| confirmBeforeSend | Query | Boolean | N | Whether to send after approval. |
| updatedDateTimeFrom | Query | DateTime | N | The start date and time of sending status updates. The default is 7 days ago. |
| updatedDateTimeTo | Query | DateTime | N | The end date and time of sending status updates. The default is the current date and time. |
| limit | Query | Number | N | The number of messages to retrieve. The default is 10. |
| offset | Query | Number | N | The starting position of the messages to retrieve. The default is 0. |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not request a request body.



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "contactDeliveryResults" : [ {
    "messageId" : "Message ID",
    "recipientIndex" : 0,
    "contactIndex" : 0,
    "contactType" : "PHONE_NUMBER",
    "contact" : "01012345678",
    "sender" : {
      "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
      "senderProfileId" : "@nhnCloud",
      "senderProfileType" : "GROUP",
      "senderPhoneNumber" : "01012341234",
      "senderMailAddress" : "abcde@nhn.com",
      "brandId" : "AR.lj0eOjEI7Y",
      "chatbotId" : "01012341234"
    },
    "templateId" : "Tj3nE8dq",
    "flowId" : "R2m9Kv0x",
    "statsKeyId" : "aA123456",
    "clientReference" : "Custom Field",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "options" : {
      "expiryOption" : 1,
      "groupId" : "20240814125609swLmoZTsGr0"
    },
    "confirmBeforeSend" : false,
    "confirmedDateTime" : "2024-10-29T06:00:01.000+09:00",
    "scheduled" : false,
    "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
    "status" : "REQUESTED",
    "resultCode" : "5.0.0",
    "resultMessage" : "Success",
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
      "thumbnailUrl" : "https://example.com/thumbnail.jpg"
    },
    "additionalProperty" : { },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "sentDateTime" : "2024-10-29T06:00:01.000+09:00",
    "deliveredDateTime" : "2024-10-29T06:00:01.000+09:00",
    "openedDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ],
  "totalCount" : 1
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | The result message of the request.<br>Default: SUCCESS |
| contactDeliveryResults | Array | O | The result of sending the message. |
| contactDeliveryResults[].messageId | String | O | The message ID. |
| contactDeliveryResults[].recipientIndex | Integer | O | The recipient index. |
| contactDeliveryResults[].contactIndex | Integer | O | The contact index. |
| contactDeliveryResults[].contactType | String | O | Contact Type<br>[PHONE_NUMBER(Phone number), EMAIL_ADDRESS(Email address), TOKEN_ADM(Amazon Device Messaging token), TOKEN_FCM(Firebase Cloud Messaging token), TOKEN_APNS(Apple Push Notification service token), TOKEN_APNS_SANDBOX(APNS Sandbox token), TOKEN_APNS_SANDBOX_VOIP(APNS Sandbox VoIP token), TOKEN_APNS_VOIP(APNS VoIP token)] |
| contactDeliveryResults[].contact | String | O | Contact information. |
| contactDeliveryResults[].sender | Object | X | Sender information by channel.<br>- ALIMTALK : senderKey, senderProfileId, senderProfileType<br>- SMS : senderPhoneNumber<br>- EMAIL : senderMailAddress<br>- RCS : brandId, chatbotId<br> |
| contactDeliveryResults[].sender.senderKey | String | X | Sender profile sender key |
| contactDeliveryResults[].sender.senderProfileId | String | X | KakaoTalk channel name |
| contactDeliveryResults[].sender.senderProfileType | String | X | Sender profile type<br>[GROUP (group sender profile), NORMAL (normal sender profile)] |
| contactDeliveryResults[].sender.senderPhoneNumber | String | X | Sender number |
| contactDeliveryResults[].sender.senderMailAddress | String | X | Sender email address |
| contactDeliveryResults[].sender.brandId | String | X | Brand ID |
| contactDeliveryResults[].sender.chatbotId | String | X | Chat room (chatbot) ID |
| contactDeliveryResults[].templateId | String | X | Template ID |
| contactDeliveryResults[].flowId | String | X | Flow ID |
| contactDeliveryResults[].statsKeyId | String | X | Statistics key ID |
| contactDeliveryResults[].clientReference | String | X | Custom field |
| contactDeliveryResults[].messageChannel | String | O | Message channel<br>[SMS(SMS), ALIMTALK(AlimTalk), BRANDMESSAGE(Brand Message), EMAIL(Email), RCS(RCS), PUSH(Push)] |
| contactDeliveryResults[].messagePurpose | String | O | Sent content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| contactDeliveryResults[].options | Object | X | Options by channel. |
| contactDeliveryResults[].options.expiryOption | Integer | X | (RCS) The time the carrier attempts to send to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour)<br>Default: 1 |
| contactDeliveryResults[].options.groupId | String | X | (RCS) Group ID for RCS Biz Center statistics integration [Guide](../console-guide/send-a-message/#RCS) (up to 20 bytes) |
| contactDeliveryResults[].confirmBeforeSend | Boolean | O | Whether to send after confirmation. |
| contactDeliveryResults[].confirmedDateTime | String | X | The time the message sending was confirmed. |
| contactDeliveryResults[].scheduled | Boolean | O | Whether to schedule sending. |
| contactDeliveryResults[].scheduledDateTime | String | X | Scheduled delivery time. |
| contactDeliveryResults[].status | String | O | Delivery/reception status. <br>[REQUESTED, CONFIRM_WAITED, WAITED, SCHEDULED, IN_PROGRESS, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED, CANCELED] |
| contactDeliveryResults[].resultCode | String | X | Delivery result code. The value varies depending on the message channel. |
| contactDeliveryResults[].resultMessage | String | X | Delivery result message. |
| contactDeliveryResults[].templateParameters | Object | X | Template parameters. It consists of a pair of keys (key, placeholder) and values ​​(value).<br><br>You cannot specify template parameters for each recipient in group delivery.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| contactDeliveryResults[].imageParameters | Array | X | Image parameters per recipient. Used only for Brand Message. |
| contactDeliveryResults[].imageParameters[].attachmentId | String | X | Attachment ID |
| contactDeliveryResults[].imageParameters[].imageUrl | String | X | Image URL |
| contactDeliveryResults[].imageParameters[].imageLink | String | X | URL to navigate to when the image is clicked |
| contactDeliveryResults[].videoParameter | Object | X | Video parameters per recipient. Used only for Brand Message. |
| contactDeliveryResults[].videoParameter.videoUrl | String | X | KakaoTV video URL |
| contactDeliveryResults[].videoParameter.thumbnailAttachmentId | String | X | Thumbnail image attachment ID |
| contactDeliveryResults[].videoParameter.thumbnailUrl | String | X | Video thumbnail image URL |
| contactDeliveryResults[].additionalProperty | Object | X | Additional properties of the message channel. |
| contactDeliveryResults[].createdDateTime | String | O | The time the message was created. |
| contactDeliveryResults[].sentDateTime | String | X | The time the message was sent. |
| contactDeliveryResults[].deliveredDateTime | String | X | The time the message was received. |
| contactDeliveryResults[].openedDateTime | String | X | The time the message was opened. |
| contactDeliveryResults[].updatedDateTime | String | X | The time the message was modified. |
| totalCount | Integer | O | The total number of message delivery results retrieved. |

**Request Example**

<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve a List of the Final Send Status Messages

GET {{endpoint}}/message/v1.0/final-contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/message/v1.0/final-contact-delivery-results" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>