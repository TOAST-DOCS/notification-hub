<!-- pre-align:aligned sig=ad89bdba0f65 -->

<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>Flow</h1>

**Notification > Notification Hub > API v1.0 User Guide > Flow**



<span id="flowV1x0001CreateFlow"></span>

<a id="create-a-flow"></a>

## Create a Flow

Creates a flow.<br>
Returns the flow ID upon flow creation.<br>
<br>
Flow steps can be defined in the **steps** field.<br>
Messages are sent in the order defined in **steps**.<br>
Message sending is attempted for each recipient starting from the first step. If sending and delivery are successful, the flow completes without proceeding to the next step. If unsuccessful, the flow proceeds to the next step.<br>


**Request**

```
POST /flow/v1.0/flows
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->


```
{
  "flowName" : "Flow name",
  "description" : "Flow description",
  "messagePurpose" : "NORMAL",
  "steps" : [ {
    "messageChannel" : "PUSH",
    "templateId" : "Tj3nE8dq",
    "nextSteps" : [ ]
  } ]
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| flowName | String | O | Flow name. Up to 20 characters can be entered. |
| description | String | X | Flow description. Up to 200 characters can be entered. |
| messagePurpose | String | O | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| steps | Array | O | Flow steps. |
| steps[].messageChannel | String | X | Message channel.<br>[SMS, RCS, ALIMTALK, BRANDMESSAGE, EMAIL, PUSH] |
| steps[].templateId | String | X | Template ID. |
| steps[].nextSteps | Array | X | Next steps. |

* The above example shows how to create a flow using email, AlimTalk, and SMS templates.
* A message channel that has already been used cannot be used in subsequent steps.
* A single step can have multiple next steps.
* To send simultaneously without a specific order, add all message channels to the first **steps**.


**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "flowId" : "R2m9Kv0x"
}
```

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| flowId | String | O | Flow ID. |

<a id="flow-definition-examples"></a>

### Flow definition examples
<a id="flow-with-linear-order"></a>

#### Flow with linear order
```
{
  "flowName": "Flow with linear order",
  "messagePurpose": "NORMAL",
  "description": "Sent in the order of PUSH > EMAIL > SMS.",
  "steps": [{
    "messageChannel": "PUSH",
    "templateId": "Template ID",
    "nextSteps": [{
      "messageChannel": "EMAIL",
      "templateId": "Template ID",
      "nextSteps": [{
        "messageChannel": "SMS",
        "templateId": "Template ID",
        "nextSteps": null
      }
      ]
    }
    ]
  }
  ]
}
```

<a id="simultaneous-send-flow"></a>

#### Simultaneous send flow
```
{
  "flowName": "Simultaneous send",
  "messagePurpose": "NORMAL",
  "description": "PUSH, EMAIL, and SMS are sent simultaneously without a specific order.",
  "steps": [{
    "messageChannel": "PUSH",
    "templateId": "Template ID",
    "nextSteps": null
  }, {
    "messageChannel": "EMAIL",
    "templateId": "Template ID",
    "nextSteps": null
  }, {
    "messageChannel": "SMS",
    "templateId": "Template ID",
    "nextSteps": null
  }
  ]
}
```


**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Create a flow

POST {{endpoint}}/flow/v1.0/flows
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "flowName" : "Flow name",
  "description" : "Flow description",
  "messagePurpose" : "NORMAL",
  "steps" : [ {
    "messageChannel" : "PUSH",
    "templateId" : "Tj3nE8dq",
    "nextSteps" : [ ]
  } ]
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/flow/v1.0/flows" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "flowName" : "Flow name",
  "description" : "Flow description",
  "messagePurpose" : "NORMAL",
  "steps" : [ {
    "messageChannel" : "PUSH",
    "templateId" : "Tj3nE8dq",
    "nextSteps" : [ ]
  } ]
}'
```

</details>

<span id="flowV1x0002ReadFlows"></span>

<a id="list-flows"></a>

## List Flows

Retrieves a list of flows.<br>
Returns the flow ID, flow name, flow description, and flow steps for each flow in the list.<br>


**Request**

```
GET /flow/v1.0/flows
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| flowName | Query | String | X | Flow name (LIKE search) |
| flowId | Query | String | X | Flow ID. |
| limit | Query | Number | X | If limit is not set, the default value is 50. (Maximum 1,000) |
| offset | Query | Number | X | If offset is not set, the default value is 0. |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->

This API does not require a request body.



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "flows" : [ {
    "flowId" : "R2m9Kv0x",
    "flowName" : "Flow name",
    "messagePurpose" : "NORMAL",
    "description" : "Flow description",
    "steps" : [ {
      "messageChannel" : "PUSH",
      "template" : {
        "templateId" : "Tj3nE8dq",
        "templateName" : "Template name"
      },
      "nextSteps" : [ {
        "messageChannel" : "EMAIL",
        "template" : {
          "templateId" : "Tj3nE8dq",
          "templateName" : "Template name"
        },
        "nextSteps" : [ {
          "messageChannel" : "ALIMTALK",
          "template" : {
            "templateId" : "Tj3nE8dq",
            "templateName" : "Template name"
          },
          "nextSteps" : [ {
            "messageChannel" : "SMS",
            "template" : {
              "templateId" : "Tj3nE8dq",
              "templateName" : "Template name"
            },
            "nextSteps" : null
          } ]
        } ]
      } ]
    } ],
    "messageChannels" : [ "PUSH", "EMAIL", "ALIMTALK", "SMS" ],
    "createdDateTime" : "2021-01-01T00:00:00.000Z",
    "updatedDateTime" : "2021-01-01T00:00:00.000Z"
  } ],
  "totalCount" : 10
}
```

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| flows | Array | O |  |
| flows[].flowId | String | O | Flow ID. |
| flows[].flowName | String | O | Flow name. |
| flows[].messagePurpose | String | O | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| flows[].description | String | X | Flow description. |
| flows[].steps | Array | O | Flow steps. |
| flows[].steps[].messageChannel | String | O | Message channel.<br>[ALIMTALK, BRANDMESSAGE, EMAIL, PUSH, RCS, SMS] |
| flows[].steps[].template | Object | O |  |
| flows[].steps[].template.templateId | String | O | Template ID. |
| flows[].steps[].template.templateName | String | X | Template name. |
| flows[].steps[].nextSteps | Array | X | Next steps. |
| flows[].messageChannels | Array | O | Message channels used in the flow steps.<br>[ALIMTALK, BRANDMESSAGE, EMAIL, PUSH, RCS, SMS] |
| flows[].createdDateTime | String | O | Flow creation time. |
| flows[].updatedDateTime | String | O | Flow modification time. |
| totalCount | Integer | O | Total number of flows. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List flows

GET {{endpoint}}/flow/v1.0/flows
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/flow/v1.0/flows" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="flowV1x0003ReadFlow"></span>

<a id="get-a-flow"></a>

## Get a Flow

Retrieves a flow.<br>
Returns the flow ID, flow name, flow description, and flow steps.<br>


**Request**

```
GET /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| flowId | Path | String | O | Flow ID. |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->

This API does not require a request body.



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "flow" : {
    "flowId" : "R2m9Kv0x",
    "flowName" : "Flow name",
    "messagePurpose" : "NORMAL",
    "description" : "Flow description",
    "steps" : [ {
      "messageChannel" : "PUSH",
      "template" : {
        "templateId" : "Tj3nE8dq",
        "templateName" : "Template name"
      },
      "nextSteps" : [ {
        "messageChannel" : "EMAIL",
        "template" : {
          "templateId" : "Tj3nE8dq",
          "templateName" : "Template name"
        },
        "nextSteps" : [ {
          "messageChannel" : "ALIMTALK",
          "template" : {
            "templateId" : "Tj3nE8dq",
            "templateName" : "Template name"
          },
          "nextSteps" : [ {
            "messageChannel" : "SMS",
            "template" : {
              "templateId" : "Tj3nE8dq",
              "templateName" : "Template name"
            },
            "nextSteps" : null
          } ]
        } ]
      } ]
    } ],
    "messageChannels" : [ "PUSH", "EMAIL", "ALIMTALK", "SMS" ],
    "createdDateTime" : "2021-01-01T00:00:00.000Z",
    "updatedDateTime" : "2021-01-01T00:00:00.000Z"
  }
}
```

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| flow | Object | O |  |
| flow.flowId | String | O | Flow ID. |
| flow.flowName | String | O | Flow name. |
| flow.messagePurpose | String | O | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| flow.description | String | X | Flow description. |
| flow.steps | Array | O | Flow steps. |
| flow.steps[].messageChannel | String | O | Message channel.<br>[ALIMTALK, BRANDMESSAGE, EMAIL, PUSH, RCS, SMS] |
| flow.steps[].template | Object | O |  |
| flow.steps[].template.templateId | String | O | Template ID. |
| flow.steps[].template.templateName | String | X | Template name. |
| flow.steps[].nextSteps | Array | X | Next steps. |
| flow.messageChannels | Array | O | Message channels used in the flow steps.<br>[ALIMTALK, BRANDMESSAGE, EMAIL, PUSH, RCS, SMS] |
| flow.createdDateTime | String | O | Flow creation time. |
| flow.updatedDateTime | String | O | Flow modification time. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Get a flow

GET {{endpoint}}/flow/v1.0/flows/{{flowId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/flow/v1.0/flows/${flowId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="flowV1x0004UpdateFlow"></span>

<a id="update-a-flow"></a>

## Update a Flow

Updates a flow.<br>


**Request**

```
PUT /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| flowId | Path | String | O | Flow ID. |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->


```
{
  "flowName" : "Flow name",
  "description" : "Flow description",
  "messagePurpose" : "NORMAL",
  "steps" : [ {
    "messageChannel" : "PUSH",
    "templateId" : "Tj3nE8dq",
    "nextSteps" : [ ]
  } ]
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| flowName | String | O | Flow name. Up to 20 characters can be entered. |
| description | String | X | Flow description. Up to 200 characters can be entered. |
| messagePurpose | String | O | Message purpose type<br>Default: NORMAL<br>[NORMAL (general), AD (advertisement), AUTH (authentication)] |
| steps | Array | O | Flow steps. |
| steps[].messageChannel | String | X | Message channel.<br>[SMS, RCS, ALIMTALK, BRANDMESSAGE, EMAIL, PUSH] |
| steps[].templateId | String | X | Template ID. |
| steps[].nextSteps | Array | X | Next steps. |



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "flowId" : "R2m9Kv0x"
}
```

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| flowId | String | O | Flow ID. |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Update a flow

PUT {{endpoint}}/flow/v1.0/flows/{{flowId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "flowName" : "Flow name",
  "description" : "Flow description",
  "messagePurpose" : "NORMAL",
  "steps" : [ {
    "messageChannel" : "PUSH",
    "templateId" : "Tj3nE8dq",
    "nextSteps" : [ ]
  } ]
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/flow/v1.0/flows/${flowId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "flowName" : "Flow name",
  "description" : "Flow description",
  "messagePurpose" : "NORMAL",
  "steps" : [ {
    "messageChannel" : "PUSH",
    "templateId" : "Tj3nE8dq",
    "nextSteps" : [ ]
  } ]
}'
```

</details>

<span id="flowV1x0005DeleteFlow"></span>

<a id="delete-a-flow"></a>

## Delete a Flow

Deletes a flow.<br>


**Request**

```
DELETE /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |
| flowId | Path | String | O | Flow ID. |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->

This API does not require a request body.



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Delete a flow

DELETE {{endpoint}}/flow/v1.0/flows/{{flowId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/flow/v1.0/flows/${flowId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="flowV1x0006DeleteFlows"></span>

<a id="delete-flows"></a>

## Delete Flows

Deletes flows.<br>


**Request**

```
POST /flow/v1.0/flows/do-delete
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameters**

| Name | In | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | Appkey |
| X-NHN-Authorization | Header | String | O | Access token |



**Request Body**

<!--If no request body is required, enter "This API does not require a request body."-->


```
{
  "flowIds" : [ "R2m9Kv0x" ]
}
```

<!--Describes the fields in the request body.-->

| Path | Type | Required | Description |
| - | - | - | - |
| flowIds | Array | O | Flow IDs. |



**Response Body**

<!--If no response body is returned, enter "This API does not return a response body."-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "results" : [ {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  } ]
}
```

<!--Describes the fields in the response body.-->

| Path | Type | Not Null | Description |
| - | - | - | - |
| header | Object | X |  |
| header.isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| header.resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |
| results | Array | X | Results of the bulk processing request. |
| results[].isSuccessful | Boolean | O | Indicates whether the request was successful.<br>Default: true |
| results[].resultCode | Integer | O | Result code of the request.<br>Default: 0 |
| results[].resultMessage | String | O | Result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Delete flows

POST {{endpoint}}/flow/v1.0/flows/do-delete
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "flowIds" : [ "R2m9Kv0x" ]
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/flow/v1.0/flows/do-delete" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "flowIds" : [ "R2m9Kv0x" ]
}'
```

</details>