<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>플로우</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 플로우**

## 플로우

<span id="post-flow"></span>

### 플로우 생성

**요청**

```
POST /flow/v1.0/flows
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |

**요청 본문**

```json
{
  "flowName": "플로우_이름",
  "description": "플로우_설명",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "이메일_템플릿_아이디",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "알림톡_템플릿_아이디",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_템플릿_아이디",
            "nextSteps": []
          }
        ]
      }
    ]
  }
}
```

| 이름 | 타입            | 필수 | 설명                                     |
| --- |---------------| --- |----------------------------------------|
| flowName | String        | Y | 플로우 이름                                 |
| description | String        | N | 플로우 설명                                 |
| messagePurpose | String        | Y | 메시지 목적<br>NORMAL(일반), AD(광고), AUTH(인증) |
| steps | Object        | Y | 플로우 단계                                  |
| steps.messageChannel | String        | Y | 메시지 채널<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| steps.templateId | String        | Y | 템플릿 아이디                               |
| steps.nextSteps | Object Array | N | 다음 단계                                   |

* 위 예시는 이메일, 알림톡, SMS 템플릿을 사용하는 플로우를 생성하는 예시입니다.
* 한번 사용된 메시지 채널은 다음 단계에서 사용할 수 없습니다.
* 한 단계는 여러 개의 다음 단계를 가질 수 있습니다.
* 순서 없이 동시 발송을 원하는 경우 첫 번째 단계인 **steps**에 모든 메시지 채널을 추가합니다.

**응답 본문**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "flowId": "플로우_아이디"
}
```

<!--응답 본문의 필드를 설명합니다.-->

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 생성
POST {{endpoint}}/flow/v1.0/flows
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "flowName": "플로우_이름",
  "description": "플로우_설명",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "이메일_템플릿_아이디",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "알림톡_템플릿_아이디",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_템플릿_아이디",
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
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
      "flowName": "플로우_이름",
      "description": "플로우_설명",
      "messagePurpose": "NORMAL",
      "steps": {
        "messageChannel": "EMAIL",
        "templateId": "이메일_템플릿_아이디",
        "nextSteps": [
          {
            "messageChannel": "ALIMTALK",
            "templateId": "알림톡_템플릿_아이디",
            "nextSteps": [
              {
                "messageChannel": "SMS",
                "templateId": "SMS_템플릿_아이디",
                "nextSteps": []
              }
            ]
          }
        ]
      }'
```

</details>

<span id="get-flows"></span>

### 플로우 목록 조회

**요청**

```
GET /flow/v1.0/flows
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명         |
| --- | --- | --- | --- |------------|
| appKey | Header | String | Y | 앱키         |
| accessToken | Header | String | Y | 인증 토큰      |
| flowId | Query | String | N | 플로우 아이디    |
| flowName | Query | String | N | 플로우 이름, 접두사(Prefix) 검색 가능 |
| limit | Query | Integer | N | 페이지당 조회 개수 |
| offset | Query | Integer | N | 페이지 오프셋    |

**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->
이 API는 요청 본문을 요구하지 않습니다.

**응답 본문**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "flows": [
    {
      "flowId": "플로우_아이디",
      "flowName": "플로우_이름",
      "description": "플로우_설명",
      "messagePurpose": "NORMAL",
      "steps": [
        {
          "messageChannel": "EMAIL",
          "templateId": "이메일_템플릿_아이디",
          "nextSteps": [
            {
              "messageChannel": "ALIMTALK",
              "templateId": "알림톡_템플릿_아이디",
              "nextSteps": [
                {
                  "messageChannel": "SMS",
                  "templateId": "SMS_템플릿_아이디",
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

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 목록 조회
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

### 플로우 조회

**요청**

```
GET /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| flowId | Path | String | Y | 플로우 아이디 |

**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.

**응답 본문**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "flow": {
    "flowId": "플로우_아이디",
    "flowName": "플로우_이름",
    "description": "플로우_설명",
    "messagePurpose": "NORMAL",
    "steps": [
      {
        "messageChannel": "EMAIL",
        "templateId": "이메일_템플릿_아이디",
        "nextSteps": [
          {
            "messageChannel": "ALIMTALK",
            "templateId": "알림톡_템플릿_아이디",
            "nextSteps": [
              {
                "messageChannel": "SMS",
                "templateId": "SMS_템플릿_아이디",
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

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 조회
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

### 플로우 수정

**요청**

```
PUT /flow/v1.0/flows/{flowId}
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| flowId | Path | String | Y | 플로우 아이디 |

**요청 본문**

```json
{
  "flowName": "플로우_이름",
  "description": "플로우_설명",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "이메일_템플릿_아이디",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "알림톡_템플릿_아이디",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_템플릿_아이디",
            "nextSteps": []
          }
        ]
      }
    ]
  }
}
```

* 플로우 수정은 플로우 생성과 동일한 요청 본문을 사용합니다.

**응답 본문**

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

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 수정
PUT {{endpoint}}/flow/v1.0/flows/{{flowId}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "flowName": "플로우_이름",
  "description": "플로우_설명",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "이메일_템플릿_아이디",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "알림톡_템플릿_아이디",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_템플릿_아이디",
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
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
      "flowName": "플로우_이름",
      "description": "플로우_설명",
      "messagePurpose": "NORMAL",
      "steps": {
        "messageChannel": "EMAIL",
        "templateId": "이메일_템플릿_아이디",
        "nextSteps": [
          {
            "messageChannel": "ALIMTALK",
            "templateId": "알림톡_템플릿_아이디",
            "nextSteps": [
              {
                "messageChannel": "SMS",
                "templateId": "SMS_템플릿_아이디",
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

### 플로우 삭제

**요청**

```
DELETE /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | 앱키 |
| accessToken | Header | String | Y | 인증 토큰 |
| flowId | Path | String | Y | 플로우 아이디 |

**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.

**응답 본문**

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

**요청 예시**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 플로우 삭제
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
