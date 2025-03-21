<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>플로우</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 플로우**



<span id="flowV1x0001CreateFlow"></span>

## 플로우 생성

플로우를 생성합니다.<br>
플로우 생성 시 플로우 아이디를 응답합니다.<br>
<br>
**steps**라는 필드에 플로우 단계를 정의할 수 있습니다.<br>
**steps**에 정의한 순서대로 메시지 발송을 진행합니다.<br> 
수신자 마다 첫 번째 단계 부터 메시지 발송을 시도하며 발송/수신이 성공하면 다음 단계로 넘어가지 않고 발송이 완료 됩니다. 실패하면 다음 단계로 넘어갑니다.<br>


**요청**

```
POST /flow/v1.0/flows
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "flowName" : "플로우 이름",
  "description" : "플로우 설명",
  "messagePurpose" : "NORMAL",
  "steps" : [ {
    "messageChannel" : "PUSH",
    "templateId" : "템플릿의 아이디",
    "nextSteps" : [ ]
  } ]
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| flowName | String | Y | 플로우 이름입니다. |
| description | String | N | 플로우 설명입니다. |
| messagePurpose | String | Y | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>[NORMAL, AD, AUTH] |
| steps | Array | Y | 플로우 단계입니다. |
| steps[].messageChannel | String | N | 메시지 채널입니다.<br>[SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH] |
| steps[].templateId | String | N | 템플릿 아이디입니다. |
| steps[].nextSteps | Array | N | 다음 단계입니다. |

* 위 예시는 이메일, 알림톡, SMS 템플릿을 사용하는 플로우를 생성하는 예시입니다.
* 한번 사용된 메시지 채널은 다음 단계에서 사용할 수 없습니다.
* 한 단계는 여러 개의 다음 단계를 가질 수 있습니다.
* 순서 없이 동시 발송을 원하는 경우 첫 번째 단계인 **steps**에 모든 메시지 채널을 추가합니다.


**응답 본문**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "flowId" : "플로우의 아이디"
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| flowId | String | 플로우 아이디입니다. |

### 플로우 정의 예시
#### 선형적인 순서를 가진 플로우
```
{
  "flowName": "선형적인 순서를 가진 플로우",
  "messagePurpose": "NORMAL",
  "description": "PUSH > EMAIL > SMS 순으로 발송 됩니다.",
  "steps": [{
    "messageChannel": "PUSH",
    "templateId": "템플릿의 아이디",
    "nextSteps": [{
      "messageChannel": "EMAIL",
      "templateId": "템플릿의 아이디",
      "nextSteps": [{
        "messageChannel": "SMS",
        "templateId": "템플릿의 아이디",
        "nextSteps": null
      }
      ]
    }
    ]
  }
  ]
}
```

#### 동시 발송 플로우
```
{
  "flowName": "동시 발송",
  "messagePurpose": "NORMAL",
  "description": "PUSH, EMAIL, SMS 순서 없이 동시에 발송 됩니다.",
  "steps": [{
    "messageChannel": "PUSH",
    "templateId": "템플릿의 아이디",
    "nextSteps": null
  }, {
    "messageChannel": "EMAIL",
    "templateId": "템플릿의 아이디",
    "nextSteps": null
  }, {
    "messageChannel": "SMS",
    "templateId": "템플릿의 아이디",
    "nextSteps": null
  }
  ]
}
```


**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 생성

POST {{endpoint}}/flow/v1.0/flows
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "flowName" : "플로우 이름",
  "description" : "플로우 설명",
  "messagePurpose" : "NORMAL",
  "steps" : [ {
    "messageChannel" : "PUSH",
    "templateId" : "템플릿의 아이디",
    "nextSteps" : [ ]
  } ]
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/flow/v1.0/flows" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "flowName" : "플로우 이름",
  "description" : "플로우 설명",
  "messagePurpose" : "NORMAL",
  "steps" : [ {
    "messageChannel" : "PUSH",
    "templateId" : "템플릿의 아이디",
    "nextSteps" : [ ]
  } ]
}'
```

</details>
<span id="flowV1x0002ReadFlows"></span>

## 플로우 목록 조회

플로우 목록을 조회합니다.<br>
플로우 목록 조회 시 플로우 아이디, 플로우 이름, 플로우 설명, 플로우 단계를 응답합니다.<br>


**요청**

```
GET /flow/v1.0/flows
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| flowName | Query  | String | N | 플로우 이름 (LIKE 검색) |
| flowId | Query  | String | N | 플로우 아이디입니다. |
| limit | Query  | Integer | N | limit 설정하지 않으면 default 50 (최대 1000) |
| offset | Query  | Integer | N | offset 설정하지 않으면 default 0 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.



**응답 본문**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "flows" : [ {
    "flowId" : "플로우의 아이디",
    "flowName" : "플로우 이름",
    "messagePurpose" : "NORMAL",
    "description" : "플로우 설명",
    "steps" : [ {
      "messageChannel" : "PUSH",
      "template" : {
        "templateId" : "템플릿의 아이디",
        "templateName" : "템플릿 이름"
      },
      "nextSteps" : [ {
        "messageChannel" : "EMAIL",
        "template" : {
          "templateId" : "템플릿의 아이디",
          "templateName" : "템플릿 이름"
        },
        "nextSteps" : [ {
          "messageChannel" : "ALIMTALK",
          "template" : {
            "templateId" : "템플릿의 아이디",
            "templateName" : "템플릿 이름"
          },
          "nextSteps" : [ {
            "messageChannel" : "SMS",
            "template" : {
              "templateId" : "템플릿의 아이디",
              "templateName" : "템플릿 이름"
            },
            "nextSteps" : null
          } ]
        } ]
      } ]
    } ],
    "messageChannels" : [ "PUSH", "SMS" ],
    "createdDateTime" : "2021-01-01T00:00:00.000Z",
    "updatedDateTime" : "2021-01-01T00:00:00.000Z"
  } ],
  "totalCount" : 10
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| flows | Array |  |
| flows[].flowId | String | 플로우 아이디입니다. |
| flows[].flowName | String | 플로우 이름입니다. |
| flows[].messagePurpose | String | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>[NORMAL, AD, AUTH] |
| flows[].description | String | 플로우 설명입니다. |
| flows[].steps | Array | 플로우 단계입니다. |
| flows[].messageChannels | Array | 플로우 단계에서 사용된 메시지 채널입니다.<br>[ALIMTALK, EMAIL, FRIENDTALK, PUSH, RCS, SMS] |
| flows[].createdDateTime | String | 플로우 생성 시간입니다. |
| flows[].updatedDateTime | String | 플로우 수정 시간입니다. |
| totalCount | Integer | 플로우 전체 개수입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 목록 조회

GET {{endpoint}}/flow/v1.0/flows
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/flow/v1.0/flows" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="flowV1x0003ReadFlow"></span>

## 플로우 조회

플로우를 조회합니다.<br>
플로우 조회 시 플로우 아이디, 플로우 이름, 플로우 설명, 플로우 단계를 응답합니다.<br>


**요청**

```
GET /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| flowId | Path  | String | Y | 플로우 아이디입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.



**응답 본문**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "flow" : {
    "flowId" : "플로우의 아이디",
    "flowName" : "플로우 이름",
    "messagePurpose" : "NORMAL",
    "description" : "플로우 설명",
    "steps" : [ {
      "messageChannel" : "PUSH",
      "template" : {
        "templateId" : "템플릿의 아이디",
        "templateName" : "템플릿 이름"
      },
      "nextSteps" : [ {
        "messageChannel" : "EMAIL",
        "template" : {
          "templateId" : "템플릿의 아이디",
          "templateName" : "템플릿 이름"
        },
        "nextSteps" : [ {
          "messageChannel" : "ALIMTALK",
          "template" : {
            "templateId" : "템플릿의 아이디",
            "templateName" : "템플릿 이름"
          },
          "nextSteps" : [ {
            "messageChannel" : "SMS",
            "template" : {
              "templateId" : "템플릿의 아이디",
              "templateName" : "템플릿 이름"
            },
            "nextSteps" : null
          } ]
        } ]
      } ]
    } ],
    "messageChannels" : [ "PUSH", "SMS" ],
    "createdDateTime" : "2021-01-01T00:00:00.000Z",
    "updatedDateTime" : "2021-01-01T00:00:00.000Z"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| flow | Object |  |
| flow.flowId | String | 플로우 아이디입니다. |
| flow.flowName | String | 플로우 이름입니다. |
| flow.messagePurpose | String | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>[NORMAL, AD, AUTH] |
| flow.description | String | 플로우 설명입니다. |
| flow.steps | Array | 플로우 단계입니다. |
| flow.steps[].messageChannel | String | 메시지 채널입니다.<br>[ALIMTALK, EMAIL, FRIENDTALK, PUSH, RCS, SMS] |
| flow.steps[].template | Object |  |
| flow.steps[].template.templateId | String | 템플릿 아이디입니다. |
| flow.steps[].template.templateName | String | 템플릿 이름입니다. |
| flow.steps[].nextSteps | Array | 다음 단계입니다. |
| flow.messageChannels | Array | 플로우 단계에서 사용된 메시지 채널입니다.<br>[ALIMTALK, EMAIL, FRIENDTALK, PUSH, RCS, SMS] |
| flow.createdDateTime | String | 플로우 생성 시간입니다. |
| flow.updatedDateTime | String | 플로우 수정 시간입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 조회

GET {{endpoint}}/flow/v1.0/flows/{{flowId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/flow/v1.0/flows/${flowId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="flowV1x0004UpdateFlow"></span>

## 플로우 수정

플로우를 수정합니다.<br>


**요청**

```
PUT /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| flowId | Path  | String | Y | 플로우 아이디입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "flowName" : "플로우 이름",
  "description" : "플로우 설명",
  "messagePurpose" : "NORMAL",
  "steps" : [ {
    "messageChannel" : "PUSH",
    "templateId" : "템플릿의 아이디",
    "nextSteps" : [ ]
  } ]
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| flowName | String | Y | 플로우 이름입니다. |
| description | String | N | 플로우 설명입니다. |
| messagePurpose | String | Y | 발송 내용 유형(NORMAL: 일반, AD: 광고, AUTH: 인증, default: NORMAL)<br>[NORMAL, AD, AUTH] |
| steps | Array | Y | 플로우 단계입니다. |
| steps[].messageChannel | String | N | 메시지 채널입니다.<br>[SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH] |
| steps[].templateId | String | N | 템플릿 아이디입니다. |
| steps[].nextSteps | Array | N | 다음 단계입니다. |



**응답 본문**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "flowId" : "플로우의 아이디"
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| flowId | String | 플로우 아이디입니다. |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 수정

PUT {{endpoint}}/flow/v1.0/flows/{{flowId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "flowName" : "플로우 이름",
  "description" : "플로우 설명",
  "messagePurpose" : "NORMAL",
  "steps" : [ {
    "messageChannel" : "PUSH",
    "templateId" : "템플릿의 아이디",
    "nextSteps" : [ ]
  } ]
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/flow/v1.0/flows/${flowId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "flowName" : "플로우 이름",
  "description" : "플로우 설명",
  "messagePurpose" : "NORMAL",
  "steps" : [ {
    "messageChannel" : "PUSH",
    "templateId" : "템플릿의 아이디",
    "nextSteps" : [ ]
  } ]
}'
```

</details>
<span id="flowV1x0005DeleteFlow"></span>

## 플로우 삭제

플로우를 삭제합니다.<br>


**요청**

```
DELETE /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| flowId | Path  | String | Y | 플로우 아이디입니다. |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.



**응답 본문**

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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 삭제

DELETE {{endpoint}}/flow/v1.0/flows/{{flowId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/flow/v1.0/flows/${flowId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="flowV1x0006DeleteFlows"></span>

## 플로우 삭제

플로우를 삭제합니다.<br>


**요청**

```
POST /flow/v1.0/flows/do-delete
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "flowIds" : [ "플로우의 아이디" ]
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| flowIds | Array | Y | 플로우 아이디입니다. |



**응답 본문**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

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

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |
| results | Array | 다중 처리 요청의 결과입니다. |
| results[].isSuccessful | Boolean | 작업이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| results[].resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| results[].resultMessage | String | 요청과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 삭제

POST {{endpoint}}/flow/v1.0/flows/do-delete
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "flowIds" : [ "플로우의 아이디" ]
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/flow/v1.0/flows/do-delete" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "flowIds" : [ "플로우의 아이디" ]
}'
```

</details>