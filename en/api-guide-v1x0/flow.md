<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Flow</h1>

**Notification > Notification Hub > API v1.0 User Guide > Flow**

## Flow

<span id="post-flow"></span>

### Create Flow

**Request**

```
POST /flow/v1.0/flows
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |

**Request Body**

```json
{
  "flowName": "Flow_Name",
  "description": "Flow_Description",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "Email_Template_Id",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "AlimTalk_Template_Id",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_Template_Id",
            "nextSteps": []
          }
        ]
      }
    ]
  }
}
```

| Name | Type            | Required | Description                                     |
| --- |---------------| --- |----------------------------------------|
| flowName | String        | Y | Flow name                                 |
| description | String        | N | Flow description                                 |
| messagePurpose | String        | Y | Message purpose<br>NORMAL, AD, AUTH, Authentication |
| steps | Object        | Y | Flow step                                  |
| steps.messageChannel | String        | Y | Message channel<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| steps.templateId | String        | Y | Template ID                               |
| steps.nextSteps | Object Array | N | Next step                                   |

* The above example creates a flow that uses an email, alerttalk, and SMS template.
* Once used, a message channel is not available for the next step.
* A step can have multiple next steps.
* Add all message channels to **steps**, which is only the first **step**, as you want them to be sent simultaneously, in no particular order.

**Response Body**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "flowId": "Flow_Id"
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Create a flow
POST {{endpoint}}/flow/v1.0/flows
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "flowName": "Flow_Name",
  "description": "Flow_Description",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "Email_Template_Id",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "AlimTalk_Template_Id",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_Template_Id",
            "nextSteps": []
          }
        ]
      }
    ]
  }
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/flow/v1.0/flows" \
     -H "Content-Type: application/json" \
     -h "x-nc-app-key: ${app_key}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
      "flowName": "Flow_Name",
      "description": "Flow_Description",
      "messagePurpose": "NORMAL",
      "steps": {
        "messageChannel": "EMAIL",
        "templateId": "Email_Template_Id",
        "nextSteps": [
          {
            "messageChannel": "ALIMTALK",
            "templateId": "AlimTalk_Template_Id",
            "nextSteps": [
              {
                "messageChannel": "SMS",
                "templateId": "SMS_Template_Id",
                "nextSteps": []
              }
            ]
          }
        ]
      }'
```

</details>

<span id="get-flows"></span>

### View Flows

**Request**

```
GET /flow/v1.0/flows
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description         |
| --- | --- | --- | --- |------------|
| appKey | Header | String | Y | Appkey         |
| accessToken | Header | String | Y | Authentication Token      |
| flowId | Query | String | N | Flow ID    |
| flowName | Query | String | N | Searchable by the flow name, prefix, and single character wildcard |
| limit | Query | Integer | N | Views per page |
| offset | Query | Integer | N | Page offset    |

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
  },
  "flows": [
    {
      "flowId": "Flow_Id",
      "flowName": "Flow_Name",
      "description": "Flow description",
      "messagePurpose": "NORMAL",
      "steps": [
        {
          "messageChannel": "EMAIL",
          "templateId": "Email_Template_Id",
          "nextSteps": [
            {
              "messageChannel": "ALIMTALK",
              "templateId": "AlimTalk_Template_Id",
              "nextSteps": [
                {
                  "messageChannel": "SMS",
                  "templateId": "SMS_Template_Id",
                  "nextSteps": []
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### View flows
GET {{endpoint}}/flow/v1.0/flows
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/flow/v1.0/flows" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

<span id="get-flow"></span>

### View a flow

**Request**

```
GET /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| flowId | Path | String | Y | Flow ID |

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
  },
  "flow": {
    "flowId": "Flow_Id",
    "flowName": "Flow_Name",
    "description": "Flow description",
    "messagePurpose": "NORMAL",
    "steps": [
      {
        "messageChannel": "EMAIL",
        "templateId": "Email_Template_Id",
        "nextSteps": [
          {
            "messageChannel": "ALIMTALK",
            "templateId": "AlimTalk_Template_Id",
            "nextSteps": [
              {
                "messageChannel": "SMS",
                "templateId": "SMS_Template_Id",
                "nextSteps": []
              }
            ]
          }
        ]
      }
    ]
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Get Flow
GET {{endpoint}}/flow/v1.0/flows/{{flowId}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/flow/v1.0/flows/${FLOW_ID}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

<span id="put-flow"></span>

### Modify Flow

**Request**

```
PUT /flow/v1.0/flows/{flowId}
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| flowId | Path | String | Y | Flow ID |

**Request Body**

```json
{
  "flowName": "Flow_Name",
  "description": "Flow_Description",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "Email_Template_Id",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "AlimTalk_Template_Id",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_Template_Id",
            "nextSteps": []
          }
        ]
      }
    ]
  }
}
```

* Modifying a flow uses the same request body as creating a flow.

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

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Modify a flow
PUT {{endpoint}}/flow/v1.0/flows/{{flowId}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "flowName": "Flow_Name",
  "description": "Flow_Description",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "Email_Template_Id",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "AlimTalk_Template_Id",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_Template_Id",
            "nextSteps": []
          }
        ]
      }
    ]
  }
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X PUT "${ENDPOINT}/flow/v1.0/flows/${FLOW_ID}" \
     -H "Content-Type: application/json" \
     -h "x-nc-app-key: ${app_key}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
      "flowName": "Flow_Name",
      "description": "Flow_Description",
      "messagePurpose": "NORMAL",
      "steps": {
        "messageChannel": "EMAIL",
        "templateId": "Email_Template_Id",
        "nextSteps": [
          {
            "messageChannel": "ALIMTALK",
            "templateId": "AlimTalk_Template_Id",
            "nextSteps": [
              {
                "messageChannel": "SMS",
                "templateId": "SMS_Template_Id",
                "nextSteps": []
              }
            ]
          }
        ]
      }'
}
```

</details>

<span id="delete-flow"></span>

### Delete Flow

**Request**

```
DELETE /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | In | Type | Required | Description |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | Appkey |
| accessToken | Header | String | Y | Authentication Token |
| flowId | Path | String | Y | Flow ID |

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

**Request Example**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Delete a flow
DELETE {{endpoint}}/flow/v1.0/flows/{{flowId}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X DELETE "${ENDPOINT}/flow/v1.0/flows/${FLOW_ID}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>
