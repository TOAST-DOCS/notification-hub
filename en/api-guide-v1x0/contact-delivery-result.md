<!-- pre-align:aligned sig=5e0edaf20f7a -->

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

## List Received Results by Contacts

Retrieves the sending and received results of requested messages by each recipient's contact.

For example, if you send 2 flow messages composed of email and SMS templates to 10 recipients who each have an email address and a phone number, retrieving the list of received results by contacts returns 40 items. (2 contacts × 10 recipients × 2 flow messages = 40 received results by contacts)
You can retrieve received results by contacts using various search criteria.


**Request**

```
GET /message/v1.0/contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| messageId | Query | String | X | Message ID. A value generated when a message sending request is received. |
| templateId | Query | String | X | Template ID. |
| flowId | Query | String | X | Flow ID. |
| statsKeyId | Query | String | X | Statistics key ID. |
| sender | Query | String | X | Sender information. |
| contact | Query | String | X | Contact. |
| messageChannel | Query | Enum | X | Message channel. |
| messagePurpose | Query | Enum | X | Message purpose. |
| statuses | Query | Enum | X | Message status. Can be viewed as a sending result.<br> When a message sending request is received, the message status is set to REQUESTED.<br> |
| scheduled | Query | Boolean | X | Whether the message is scheduled for delivery. |
| confirmBeforeSend | Query | Boolean | X | Whether to send after confirmation. |
| createdDateTimeFrom | Query | DateTime | X | Request start date and time. The default value is 7 days ago. |
| createdDateTimeTo | Query | DateTime | X | Request end date and time. The default value is the current date and time. |
| limit | Query | Number | X | Number of messages to retrieve. The default value is 10. |
| offset | Query | Number | X | Starting position of messages to retrieve. The default value is 0. |

* The maximum retrieval period for **createdDateTimeFrom** and **createdDateTimeTo** is 7 days.


**Request Body**

<!--If the API does not require a request body, enter "This API does not require a request body."-->

This API does not require a request body.



**Response Body**

<!--If the API does not return a response body, enter "This API does not return a response body."-->

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
    "clientReference" : "User-defined field",
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

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| contactDeliveryResults | Array | O | Message sending results. |
| contactDeliveryResults[].messageId | String | O | Message ID |
| contactDeliveryResults[].recipientIndex | Integer | O | Recipient index. |
| contactDeliveryResults[].contactIndex | Integer | O | Contact index. |
| contactDeliveryResults[].contactType | String | O | Contact type<br>[PHONE_NUMBER (phone number), EMAIL_ADDRESS (email address), TOKEN_ADM (Amazon Device Messaging token), TOKEN_FCM (Firebase Cloud Messaging token), TOKEN_APNS (Apple Push Notification service token), TOKEN_APNS_SANDBOX (APNS Sandbox token), TOKEN_APNS_SANDBOX_VOIP (APNS Sandbox VoIP token), TOKEN_APNS_VOIP (APNS VoIP token)] |
| contactDeliveryResults[].contact | String | O | Contact. |
| contactDeliveryResults[].sender | Object | X |  |
| contactDeliveryResults[].sender.senderKey | String | X | Sender profile sender key |
| contactDeliveryResults[].sender.senderProfileId | String | X | KakaoTalk channel name |
| contactDeliveryResults[].sender.senderProfileType | String | X | Sender profile type<br>[GROUP (group sender profile), NORMAL (standard sender profile)] |
| contactDeliveryResults[].sender.senderPhoneNumber | String | X | Sender phone number |
| contactDeliveryResults[].sender.senderMailAddress | String | X | Sender email address |
| contactDeliveryResults[].sender.brandId | String | X | Brand ID |
| contactDeliveryResults[].sender.chatbotId | String | X | Chat room (chatbot) ID |
| contactDeliveryResults[].templateId | String | X | Template ID |
| contactDeliveryResults[].flowId | String | X | Flow ID |
| contactDeliveryResults[].statsKeyId | String | X | Statistics key ID |
| contactDeliveryResults[].clientReference | String | X | User-defined field |
| contactDeliveryResults[].messageChannel | String | O | Message channel<br>[SMS (SMS), ALIMTALK (Alim Talk), EMAIL (email), RCS (RCS), PUSH (push)] |
| contactDeliveryResults[].messagePurpose | String | O | Message content type<br>Default: NORMAL<br>[NORMAL (general), AD (advertising), AUTH (authentication)] |
| contactDeliveryResults[].options | Object | X |  |
| contactDeliveryResults[].options.expiryOption | Integer | X | (RCS) Time that the carrier attempts to deliver the message to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour)<br>Default: 1 |
| contactDeliveryResults[].options.groupId | String | X | (RCS) Group ID for RCS Biz Center statistics integration [Guide](../console-guide/send-a-message/#RCS) (up to 20 bytes) |
| contactDeliveryResults[].confirmBeforeSend | Boolean | O | Whether to send after confirmation. |
| contactDeliveryResults[].confirmedDateTime | String | X | Date and time when the message sending was confirmed. |
| contactDeliveryResults[].scheduled | Boolean | O | Whether the message is scheduled for delivery. |
| contactDeliveryResults[].scheduledDateTime | String | X | Scheduled delivery date and time. |
| contactDeliveryResults[].status | String | O | Sending/received status<br>[REQUESTED (requested), CONFIRM_WAITED (pending confirmation), WAITED (waiting), SCHEDULED (scheduled), IN_PROGRESS (sending), SENT (sent), SEND_FAILED (send failed), DELIVERED (delivered), DELIVERY_FAILED (delivery failed), CANCELED (canceled)] |
| contactDeliveryResults[].resultCode | String | X | Sending result code. The value varies by message channel. |
| contactDeliveryResults[].resultMessage | String | X | Sending result message. |
| contactDeliveryResults[].templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>In group sending, you cannot specify template parameters per recipient.<br><br>Template parameters set for a recipient take precedence over message template parameters.<br><br> |
| contactDeliveryResults[].additionalProperty | Object | X |  |
| contactDeliveryResults[].createdDateTime | String | O | Date and time when the message was created. |
| contactDeliveryResults[].sentDateTime | String | X | Date and time when the message was sent. |
| contactDeliveryResults[].deliveredDateTime | String | X | Date and time when the message was delivered. |
| contactDeliveryResults[].openedDateTime | String | X | Date and time when the message was opened. |
| contactDeliveryResults[].updatedDateTime | String | X | Date and time when the message was last updated. |
| totalCount | Integer | O | Total number of message sending results retrieved. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List received results by contacts

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

## List Final Delivery Status Messages

Retrieves a list of message results for which the delivery process has ended.<br>
The final delivery statuses are "SEND_FAILED", "DELIVERED", "DELIVERY_FAILED", and "CANCELED".


**Request**

```
GET /message/v1.0/final-contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | Type | Format | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | App key |
| X-NHN-Authorization | Header | String | O | Access token |
| messageId | Query | String | X | Message ID. The value generated when a message sending request is received. |
| templateId | Query | String | X | Template ID. |
| flowId | Query | String | X | Flow ID. |
| statsKeyId | Query | String | X | Stats key ID. |
| sender | Query | String | X | Sender information. |
| contact | Query | String | X | Contact. |
| messageChannel | Query | Enum | X | Message channel. |
| messagePurpose | Query | Enum | X | Message purpose. |
| scheduled | Query | Boolean | X | Whether the message is scheduled for delivery. |
| confirmBeforeSend | Query | Boolean | X | Whether to send after approval. |
| updatedDateTimeFrom | Query | DateTime | X | Start date and time of the delivery status update. The default value is 7 days ago. |
| updatedDateTimeTo | Query | DateTime | X | End date and time of the delivery status update. The default value is the current date and time. |
| limit | Query | Number | X | Number of messages to retrieve. The default value is 10. |
| offset | Query | Number | X | Starting position of the messages to retrieve. The default value is 0. |



**Request Body**

This API does not require a request body.



**Response Body**

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "contactDeliveryResults" : [ {
    "messageId" : "메시지의 아이디",
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
    "clientReference" : "사용자 지정 필드",
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

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| contactDeliveryResults | Array | O | Message delivery results. |
| contactDeliveryResults[].messageId | String | O | Message ID |
| contactDeliveryResults[].recipientIndex | Integer | O | Recipient index. |
| contactDeliveryResults[].contactIndex | Integer | O | Contact index. |
| contactDeliveryResults[].contactType | String | O | Contact type<br>[PHONE_NUMBER (phone number), EMAIL_ADDRESS (email address), TOKEN_ADM (Amazon Device Messaging token), TOKEN_FCM (Firebase Cloud Messaging token), TOKEN_APNS (Apple Push Notification service token), TOKEN_APNS_SANDBOX (APNS Sandbox token), TOKEN_APNS_SANDBOX_VOIP (APNS Sandbox VoIP token), TOKEN_APNS_VOIP (APNS VoIP token)] |
| contactDeliveryResults[].contact | String | O | Contact. |
| contactDeliveryResults[].sender | Object | X |  |
| contactDeliveryResults[].sender.senderKey | String | X | Sender profile sender key |
| contactDeliveryResults[].sender.senderProfileId | String | X | KakaoTalk channel name |
| contactDeliveryResults[].sender.senderProfileType | String | X | Sender profile type<br>[GROUP (group sender profile), NORMAL (general sender profile)] |
| contactDeliveryResults[].sender.senderPhoneNumber | String | X | Sender phone number |
| contactDeliveryResults[].sender.senderMailAddress | String | X | Sender email address |
| contactDeliveryResults[].sender.brandId | String | X | Brand ID |
| contactDeliveryResults[].sender.chatbotId | String | X | Chatroom (chatbot) ID |
| contactDeliveryResults[].templateId | String | X | Template ID |
| contactDeliveryResults[].flowId | String | X | Flow ID |
| contactDeliveryResults[].statsKeyId | String | X | Stats key ID |
| contactDeliveryResults[].clientReference | String | X | Client reference |
| contactDeliveryResults[].messageChannel | String | O | Message channel<br>[SMS (SMS), ALIMTALK (Alim Talk), EMAIL (email), RCS (RCS), PUSH (push)] |
| contactDeliveryResults[].messagePurpose | String | O | Message content type<br>Default: NORMAL<br>[NORMAL (general), AD (advertising), AUTH (authentication)] |
| contactDeliveryResults[].options | Object | X |  |
| contactDeliveryResults[].options.expiryOption | Integer | X | (RCS) Time during which the carrier attempts to deliver to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour)<br>Default: 1 |
| contactDeliveryResults[].options.groupId | String | X | (RCS) Group ID for RCS Biz Center statistics integration [Guide](../console-guide/send-a-message/#RCS) (up to 20 bytes) |
| contactDeliveryResults[].confirmBeforeSend | Boolean | O | Whether to send after confirmation. |
| contactDeliveryResults[].confirmedDateTime | String | X | Date and time the message sending was confirmed. |
| contactDeliveryResults[].scheduled | Boolean | O | Whether the message is scheduled for delivery. |
| contactDeliveryResults[].scheduledDateTime | String | X | Scheduled delivery date and time. |
| contactDeliveryResults[].status | String | O | Delivery/received status<br>[REQUESTED, CONFIRM_WAITED, WAITED, SCHEDULED, IN_PROGRESS, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED, CANCELED] |
| contactDeliveryResults[].resultCode | String | X | Delivery result code. The value varies depending on the message channel. |
| contactDeliveryResults[].resultMessage | String | X | Delivery result message. |
| contactDeliveryResults[].templateParameters | Object | X | Template parameters. Consists of key (placeholder) and value pairs.<br><br>Template parameters cannot be specified per recipient in group sending.<br><br>Template parameters set for a recipient take precedence over message template parameters.<br><br> |
| contactDeliveryResults[].additionalProperty | Object | X |  |
| contactDeliveryResults[].createdDateTime | String | O | Date and time the message was created. |
| contactDeliveryResults[].sentDateTime | String | X | Date and time the message was sent. |
| contactDeliveryResults[].deliveredDateTime | String | X | Date and time the message was delivered. |
| contactDeliveryResults[].openedDateTime | String | X | Date and time the message was opened. |
| contactDeliveryResults[].updatedDateTime | String | X | Date and time the message was last updated. |
| totalCount | Integer | O | Total number of message delivery results retrieved. |



**Request Examples**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List Final Delivery Status Messages

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
