<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Receiving Results by Contact</h1>

**Notification > Notification Hub > API v1.0 User Guide > Receiving Results by Contact**

<span id="read-contact-delivery-results"></span>

### View a List of Receiving Results by Contact

View the results of sending and receiving requested messages by recipient's contact.

For example, if you send two flow messages consisting of an email and SMS template to 10 recipients with emails and phone numbers, you'll see 40 items when you view the list of received results by contact. (2 contacts X 10 recipients X 2 flow messages = 40 received results by contact)
You can view received results by contact with different search criteria.

<!-- !!! tip "알아두기"-->
<!-- API를 사용할 때 사용자가 알아 두면 좋을 참고 사항이나 추가 정보를 제공할 때 사용합니다.-->

<!-- !!! warning "주의"-->
<!--API를 사용할 때 따르지 않을 경우 서비스의 비정상 또는 비효율적 동작이 발생할 수 있는 주의 사항을 표기할 때 사용합니다.-->

**Request**

```
GET /message/v1.0/contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- |----| --- |
| appKey | Header | String | Y  | Appkey |
| accessToken | Header | String | Y  | Authentication Token |
| createdDateTimeFrom | Query | DateTime(ISO 8601) | Y  | Created time starts |
| createdDateTimeTo | Query | DateTime(ISO 8601) | Y  | Created time ends |
| messageId | Query | String | N  | Message ID |
| templateId | Query | String | N  | Template ID |
| flowId | Query | String | N  | Flow ID |
| statsKeyId | Query | String | N  | Statistics Key ID |
| sender | Query | String | N  | Sender |
| contact | Query | String | N  | Contact |
| messageChannel | Query | String | N  | Message channel<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| messagePurpose | Query | String | N  | Message purpose |
| String | Query | String | N  | Status |
| scheduled | Query | Boolean | N  | Scheduled sending or not |
| confirmBeforeSend | Query | Boolean | N  | Confirm before sending or not |
| limit | Query | Integer | N  | Query count |
| offset | Query | Integer | N  | Where to start lookup |

* The maximum lookup period for **createdDateTimeFrom** and **createdDateTimeTo** is 7 days.

**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "contactDeliveryResults": [
    {
      "messageId": "Message ID",
      "recipientIndex": 0,
      "contactIndex": 0,
      "contactType": "PHONE_NUMBER",
      "contact": "01012345678",
      "sender": {
        "senderKey": "sender_key",
        "senderProfileId": "@nhnCloud",
        "senderProfileType": "GROUP",
        "senderPhoneNumber": "01012341234",
        "senderMailAddress": "abcde@nhn.com",
        "brandId": "AR.lj0eOjEI7Y",
        "chatbotId": "01012341234"
      },
      "templateId": "Id of the template",
      "flowId": "Id of the flow",
      "statsKeyId": "Id of the statistics key",
      "messageChannel": "SMS",
      "messagePurpose": "NORMAL",
      "confirmBeforeSend": false,
      "confirmedDateTime": "2023-01-01T00:00:00Z",
      "scheduled": false,
      "scheduledDateTime": "2024-10-26T07:52:12.728Z",
      "status": "REQUESTED",
      "resultCode": "5.0.0",
      "resultMessage": "Success",
      "templateParameters": {
        "key1": "value1",
        "key2": "value2"
      },
      "additionalProperty": {
      },
      "createdDateTime": "2023-01-01T00:00:00Z",
      "sentDateTime": "2023-01-01T00:00:00Z",
      "deliveredDateTime": "2023-01-01T00:00:00Z",
      "openedDateTime": "2023-01-01T00:00:00Z",
      "updatedDateTime": "2023-01-01T00:00:00Z"
    }
  ],
  "totalCount": 1
}
```

<!--요청 본문의 필드를 설명합니다.-->

**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->


```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "contactDeliveryResults": [
    {
      "messageId": "Message ID",
      "recipientIndex": 0,
      "contactIndex": 0,
      "contactType": "PHONE_NUMBER",
      "contact": "01012345678",
      "sender": {
        "senderKey": "sender_key",
        "senderProfileId": "@nhnCloud",
        "senderProfileType": "GROUP",
        "senderPhoneNumber": "01012341234",
        "senderMailAddress": "abcde@nhn.com",
        "brandId": "AR.lj0eOjEI7Y",
        "chatbotId": "01012341234"
      },
      "templateId": "Id of the template",
      "flowId": "Id of the flow",
      "statsKeyId": "Id of the statistics key",
      "messageChannel": "SMS",
      "messagePurpose": "NORMAL",
      "confirmBeforeSend": false,
      "confirmedDateTime": "2023-01-01T00:00:00Z",
      "scheduled": false,
      "scheduledDateTime": "2024-10-26T07:52:12.728Z",
      "status": "REQUESTED",
      "resultCode": "5.0.0",
      "resultMessage": "Success",
      "templateParameters": {
        "key1": "value1",
        "key2": "value2"
      },
      "additionalProperty": {
        
      },
      "createdDateTime": "2023-01-01T00:00:00Z",
      "sentDateTime": "2023-01-01T00:00:00Z",
      "deliveredDateTime": "2023-01-01T00:00:00Z",
      "openedDateTime": "2023-01-01T00:00:00Z",
      "updatedDateTime": "2023-01-01T00:00:00Z"
    }
  ],
  "totalCount": 1
}
```



<!--응답 본문의 필드를 설명합니다.-->

| Name | Type | Description |
| --- | --- | --- |
| header.isSuccessful | Boolean | API Request successful or not |
| header.resultCode | Integer | Result code |
| header.resultMessage | String | Result message |
| contactDeliveryResults | Object Array | Receiving results by contact |
| contactDeliveryResults[].messageId | String| Message ID |
| contactDeliveryResults[].recipientIndex | Number| Recipient index|
| contactDeliveryResults[].contactIndex | Number| Contact index|
| contactDeliveryResults[].contactType | String| Contact type |
| contactDeliveryResults[].contact | String| Contact|
| contactDeliveryResults[].sender | Object| Sender|
| contactDeliveryResults[].sender.senderKey | String| Sender profile’s sender key, only appears in AlimTalk and FriendTalk|
| contactDeliveryResults[].sender.senderProfileId | String| Sender profile’s ID, only appears in AlimTalk and FriendTalk |
| contactDeliveryResults[].sender.senderProfileType | String| Sender profile type, only appears in AlimTalk and FriendTalk|
| contactDeliveryResults[].sender.senderPhoneNumber | String| Sender’s phone number, only appears in SMS|
| contactDeliveryResults[].sender.senderMailAddress | String| Sender email address, only appears in emails|
| contactDeliveryResults[].sender.brandId | String| Brand ID, only appears in RCS |
| contactDeliveryResults[].sender.chatbotId | String| Chatroom ID, only appears in RCS |
| contactDeliveryResults[].templateId | String| Template’s ID, only appears in template messages|
| contactDeliveryResults[].flowId | String| Flow’s ID, only appears in template messages|
| contactDeliveryResults[].statsKeyId | String| ID of the statistics key|
| contactDeliveryResults[].messageChannel | String| Message channel<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| contactDeliveryResults[].messagePurpose | String| Message purpose |
| contactDeliveryResults[].confirmBeforeSend | Boolean | Whether to enable send after approval|
| contactDeliveryResults[].confirmedDateTime | DateTime(ISO 86091) | Approval date (e.g., 2024-10-29T06:09:00+09:00)|
| contactDeliveryResults[].scheduled | Boolean | Scheduled sending or not |
| contactDeliveryResults[].scheduledDateTime | DateTime(ISO 86091) | Scheduled send date |
| contactDeliveryResults[].status | String| Status |
| contactDeliveryResults[].resultCode | String| Result code|
| contactDeliveryResults[].resultMessage | String| Result message |
| contactDeliveryResults[].templateParameters | Object| Template parameter |
| contactDeliveryResults[].additionalProperty | Object| Additional properties, AlimTalk, RCS only|
| contactDeliveryResults[].createdDateTime | DateTime(ISO 86091) | Creation date (e.g., 2024-10-29T06:09:00+09:00)|
| contactDeliveryResults[].sentDateTime | DateTime(ISO 86091) | Date of sending, null until sending event is collected|
| contactDeliveryResults[].deliveredDateTime | DateTime(ISO 86091) | Date of receiving, null until receiving event is collected|
| contactDeliveryResults[].openedDateTime | DateTime(ISO 86091) | View date, null until view event is collected, push and email only |
| contactDeliveryResults[].updatedDateTime | DateTime(ISO 86091) | Date of last update|
| totalCount | Number| Total number|



**Request example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Send entire message
POST {{endpoint}}/message/v1.0/contact-delivery-results
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
curl -X GET "${ENDPOINT}/message/v1.0/contact-delivery-results" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

