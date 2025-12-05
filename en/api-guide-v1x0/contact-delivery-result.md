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

## Retrieve a List of Received Results by Contacts

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
| messageChannel | Query | String | N | Message channel.<br>[SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, and PUSH] |
| messagePurpose | Query | String | N | The message purpose.<br>[AD, AUTH, NORMAL] |
| statuses | Query | List | N | The message status. You can view the sending result.<br> When a message sending request is received, the message status is set to REQUESTED. <br>[REQUESTED, SCHEDULED, READY, CONFIRM_WAITED, WAITED, IN_PROGRESS, SENT, SEND_FAILED, DELIVERED, OPENED, DELIVERY_FAILED, and CANCELED] |
| scheduled | Query | Boolean | N | Whether to schedule sending. |
| confirmBeforeSend | Query | Boolean | N | Whether to send after approval. |
| createdDateTimeFrom | Query | Date | N | The request start date and time. The default is 7 days ago. |
| createdDateTimeTo | Query | Date | N | The request end date and time. The default is the current date and time. |
| limit | Query | Integer | N | The number of messages to retrieve. The default is 10. |
| offset | Query | Integer | N | The starting position of the messages to retrieve. The default is 0. |

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
    "templateId" : "Template ID",
    "flowId" : "Flow ID",
    "statsKeyId" : "Statistics Key ID",
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

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| contactDeliveryResults | Array | The result of sending the message. |
| contactDeliveryResults[].messageId | String | The message ID. |
| contactDeliveryResults[].recipientIndex | Integer | The recipient index. |
| contactDeliveryResults[].contactIndex | Integer | The contact index. |
| contactDeliveryResults[].contactType | String | Contact Type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| contactDeliveryResults[].contact | String | Contact information. |
| contactDeliveryResults[].sender | Object | |
| contactDeliveryResults[].sender.senderKey | String | Sender profile sender key |
| contactDeliveryResults[].sender.senderProfileId | String | KakaoTalk channel name |
| contactDeliveryResults[].sender.senderProfileType | String | Sender profile type<br>[GROUP, NORMAL] |
| contactDeliveryResults[].sender.senderPhoneNumber | String | Sender number |
| contactDeliveryResults[].sender.senderMailAddress | String | Sender email address |
| contactDeliveryResults[].sender.brandId | String | Brand ID |
| contactDeliveryResults[].sender.chatbotId | String | Chat room (chatbot) ID |
| contactDeliveryResults[].templateId | String | Template ID |
| contactDeliveryResults[].flowId | String | Flow ID |
| contactDeliveryResults[].statsKeyId | String | Statistics key ID |
| contactDeliveryResults[].clientReference | String | Custom field |
| contactDeliveryResults[].messageChannel | String | Message channel <br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| contactDeliveryResults[].messagePurpose | String | Sent content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| contactDeliveryResults[].options | Object | |
| contactDeliveryResults[].options.expiryOption | Integer | The time the carrier attempts to send to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour)<br>Default: 1 |
| contactDeliveryResults[].options.groupId | String | Group ID for RCS Biz Center statistics integration |
| contactDeliveryResults[].confirmBeforeSend | Boolean | Whether to send after confirmation. |
| contactDeliveryResults[].confirmedDateTime | String | The time the message sending was confirmed. |
| contactDeliveryResults[].scheduled | Boolean | Whether to schedule sending. |
| contactDeliveryResults[].scheduledDateTime | String | Scheduled delivery time. |
| contactDeliveryResults[].status | String | Delivery/reception status. <br>[REQUESTED, CONFIRM_WAITED, WAITED, SCHEDULED, IN_PROGRESS, SENT, SEND_FAILED, DELIVERED, OPENED, DELIVERY_FAILED, CANCELED] |
| contactDeliveryResults[].resultCode | String | Delivery result code. The value varies depending on the message channel. |
| contactDeliveryResults[].resultMessage | String | Delivery result message. |
| contactDeliveryResults[].templateParameters | Object | Template parameters. It consists of a pair of keys (key, placeholder) and values ​​(value).<br><br>You cannot specify template parameters for each recipient in group delivery.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| contactDeliveryResults[].additionalProperty | Object | |
| contactDeliveryResults[].createdDateTime | String | The time the message was created. |
| contactDeliveryResults[].sentDateTime | String | The time the message was sent. |
| contactDeliveryResults[].deliveredDateTime | String | The time the message was received. |
| contactDeliveryResults[].openedDateTime | String | The time the message was opened. |
| contactDeliveryResults[].updatedDateTime | String | The time the message was modified. |
| totalCount | Integer | The total number of message delivery results retrieved. |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="contactDeliveryResultV1x0002ReadFinalContactDeliveryResults"></span>

## Retrieve a List of the Final Send Status Messages

View a list of message results after the sending process has completed.<br>
Final sending statuses include "SEND_FAILED," "DELIVERED," "DELIVERY_FAILED," and "CANCELED."


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
| messageChannel | Query | String | N | Message channel.<br>[SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH] |
| messagePurpose | Query | String | N | The message purpose. <br>[AD, AUTH, NORMAL] |
| scheduled | Query | Boolean | N | Whether to schedule sending. |
| confirmBeforeSend | Query | Boolean | N | Whether to send after approval. |
| updatedDateTimeFrom | Query | Date | N | The start date and time of sending status updates. The default is 7 days ago. |
| updatedDateTimeTo | Query | Date | N | The end date and time of sending status updates. The default is the current date and time. |
| limit | Query | Integer | N | The number of messages to retrieve. The default is 10. |
| offset | Query | Integer | N | The starting position of the messages to retrieve. The default is 0. |



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
    "templateId" : "Template ID",
    "flowId" : "Flow ID",
    "statsKeyId" : "Statistics Key ID",
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

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| contactDeliveryResults | Array | The result of sending the message. |
| contactDeliveryResults[].messageId | String | The message ID. |
| contactDeliveryResults[].recipientIndex | Integer | The recipient index. |
| contactDeliveryResults[].contactIndex | Integer | The contact index. |
| contactDeliveryResults[].contactType | String | Contact Type<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| contactDeliveryResults[].contact | String | Contact information. |
| contactDeliveryResults[].sender | Object | |
| contactDeliveryResults[].sender.senderKey | String | Sender profile sender key |
| contactDeliveryResults[].sender.senderProfileId | String | KakaoTalk channel name |
| contactDeliveryResults[].sender.senderProfileType | String | Sender profile type<br>[GROUP, NORMAL] |
| contactDeliveryResults[].sender.senderPhoneNumber | String | Sender number |
| contactDeliveryResults[].sender.senderMailAddress | String | Sender email address |
| contactDeliveryResults[].sender.brandId | String | Brand ID |
| contactDeliveryResults[].sender.chatbotId | String | Chat room (chatbot) ID |
| contactDeliveryResults[].templateId | String | Template ID |
| contactDeliveryResults[].flowId | String | Flow ID |
| contactDeliveryResults[].statsKeyId | String | Statistics key ID |
| contactDeliveryResults[].clientReference | String | Custom field |
| contactDeliveryResults[].messageChannel | String | Message channel <br>[SMS, ALIMTALK, FRIENDTALK, EMAIL, RCS, PUSH] |
| contactDeliveryResults[].messagePurpose | String | Sent content type<br>Default: NORMAL<br>[NORMAL, AD, AUTH] |
| contactDeliveryResults[].options | Object | |
| contactDeliveryResults[].options.expiryOption | Integer | The time the carrier attempts to send to the device (1: 1 day, 2: 40 seconds, 3: 3 minutes, 4: 1 hour)<br>Default: 1 |
| contactDeliveryResults[].options.groupId | String | Group ID for RCS Biz Center statistics integration |
| contactDeliveryResults[].confirmBeforeSend | Boolean | Whether to send after confirmation. |
| contactDeliveryResults[].confirmedDateTime | String | The time the message sending was confirmed. |
| contactDeliveryResults[].scheduled | Boolean | Whether to schedule sending. |
| contactDeliveryResults[].scheduledDateTime | String | Scheduled delivery time. |
| contactDeliveryResults[].status | String | Delivery/reception status. <br>[REQUESTED, CONFIRM_WAITED, WAITED, SCHEDULED, IN_PROGRESS, SENT, SEND_FAILED, DELIVERED, OPENED, DELIVERY_FAILED, CANCELED] |
| contactDeliveryResults[].resultCode | String | Delivery result code. The value varies depending on the message channel. |
| contactDeliveryResults[].resultMessage | String | Delivery result message. |
| contactDeliveryResults[].templateParameters | Object | Template parameters. It consists of a pair of keys (key, placeholder) and values ​​(value).<br><br>You cannot specify template parameters for each recipient in group delivery.<br><br>Template parameters set for recipients take precedence over message template parameters.<br><br> |
| contactDeliveryResults[].additionalProperty | Object | |
| contactDeliveryResults[].createdDateTime | String | The time the message was created. |
| contactDeliveryResults[].sentDateTime | String | The time the message was sent. |
| contactDeliveryResults[].deliveredDateTime | String | The time the message was received. |
| contactDeliveryResults[].openedDateTime | String | The time the message was opened. |
| contactDeliveryResults[].updatedDateTime | String | The time the message was modified. |
| totalCount | Integer | The total number of message delivery results retrieved. |



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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>