<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>フロー</h1>

**Notification > Notification Hub > API v1.0使用ガイド > フロー**

## フロー

<span id="post-flow"></span>

### フロー作成

**リクエスト**

```
POST /flow/v1.0/flows
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |

**リクエスト本文**

```json
{
  "flowName": "フロー_名前",
  "description": "フロー_説明",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "メール_テンプレート_ID",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "お知らせトーク_テンプレート_ID",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_テンプレート_ID",
            "nextSteps": []
          }
        ]
      }
    ]
  }
}
```

| 名前 | タイプ          | 必須 | 説明                                   |
| --- |---------------| --- |----------------------------------------|
| flowName | String        | Y | フロー名                               |
| description | String        | N | フローの説明                               |
| messagePurpose | String        | Y | メッセージ目的<br>NORMAL(一般), AD(広告), AUTH(認証) |
| steps | Object        | Y | フロー段階                                |
| steps.messageChannel | String        | Y | メッセージチャンネル<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| steps.templateId | String        | Y | テンプレートID                               |
| steps.nextSteps | Object Array | N | 次のステップ                                 |

* 上記の例はメール、お知らせトーク、 SMSテンプレートを使用するフローを作成する例です。
* 一度使用したメッセージチャンネルは、次のステップでは使用できません。
* 1つのステップは複数の次のステップを持つことができます。
* 順序なく同時送信を希望する最初のステップである**steps**に全てのメッセージチャンネルを追加します。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "flowId": "フロー_ID"
}
```

<!--レスポンス本文のフィールドを説明します。-->

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フロー作成
POST {{endpoint}}/flow/v1.0/flows
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "flowName": "フロー_名前",
  "description": "フロー_説明",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "メール_テンプレート_ID",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "お知らせトーク_テンプレート_ID",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_テンプレート_ID",
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
      "flowName": "フロー_名前",
      "description": "フロー_説明",
      "messagePurpose": "NORMAL",
      "steps": {
        "messageChannel": "EMAIL",
        "templateId": "メール_テンプレート_ID",
        "nextSteps": [
          {
            "messageChannel": "ALIMTALK",
            "templateId": "お知らせトーク_テンプレート_ID",
            "nextSteps": [
              {
                "messageChannel": "SMS",
                "templateId": "SMS_テンプレート_ID",
                "nextSteps": []
              }
            ]
          }
        ]
      }'
```

</details>

<span id="get-flows"></span>

### フローリスト照会

**リクエスト**

```
GET /flow/v1.0/flows
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明       |
| --- | --- | --- | --- |------------|
| appKey | Header | String | Y | アプリキー       |
| accessToken | Header | String | Y | 認証トークン    |
| flowId | Query | String | N | フローID    |
| flowName | Query | String | N | フロー名、プレフィックス(Prefix)検索可能 |
| limit | Query | Integer | N | 1ページあたりの照会数 |
| offset | Query | Integer | N | ページオフセット  |

**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません。」と入力します。-->
このAPIはリクエスト本文を要求しません。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "flows": [
    {
      "flowId": "フロー_ID",
      "flowName": "フロー_名前",
      "description": "フロー_説明",
      "messagePurpose": "NORMAL",
      "steps": [
        {
          "messageChannel": "EMAIL",
          "templateId": "メール_テンプレート_ID",
          "nextSteps": [
            {
              "messageChannel": "ALIMTALK",
              "templateId": "お知らせトーク_テンプレート_ID",
              "nextSteps": [
                {
                  "messageChannel": "SMS",
                  "templateId": "SMS_テンプレート_ID",
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

<!--レスポンス本文のフィールドを説明します。-->

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フローリスト照会
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

### フロー照会

**リクエスト**

```
GET /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| flowId | Path | String | Y | フローID |

**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません。」と入力します。-->

このAPIはリクエスト本文を要求しません。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "flow": {
    "flowId": "フロー_ID",
    "flowName": "フロー_名前",
    "description": "フロー_説明",
    "messagePurpose": "NORMAL",
    "steps": [
      {
        "messageChannel": "EMAIL",
        "templateId": "メール_テンプレート_ID",
        "nextSteps": [
          {
            "messageChannel": "ALIMTALK",
            "templateId": "お知らせトーク_テンプレート_ID",
            "nextSteps": [
              {
                "messageChannel": "SMS",
                "templateId": "SMS_テンプレート_ID",
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

<!--レスポンス本文のフィールドを説明します。-->

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フロー照会
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

### フロー修正

**リクエスト**

```
PUT /flow/v1.0/flows/{flowId}
Content-Type: application/json
X-NC-APP-KEY: {{ppKey}
X-NHN-Authorization: {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| flowId | Path | String | Y | フローID |

**リクエスト本文**

```json
{
  "flowName": "フロー_名前",
  "description": "フロー_説明",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "メール_テンプレート_ID",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "お知らせトーク_テンプレート_ID",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_テンプレート_ID",
            "nextSteps": []
          }
        ]
      }
    ]
  }
}
```

* フロー修正はフロー作成と同じリクエスト本文を使用します。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

<!--レスポンス本文のフィールドを説明します。-->

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フロー修正
PUT {{endpoint}}/flow/v1.0/flows/{{flowId}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "flowName": "フロー_名前",
  "description": "フロー_説明",
  "messagePurpose": "NORMAL",
  "steps": {
    "messageChannel": "EMAIL",
    "templateId": "メール_テンプレート_ID",
    "nextSteps": [
      {
        "messageChannel": "ALIMTALK",
        "templateId": "お知らせトーク_テンプレート_ID",
        "nextSteps": [
          {
            "messageChannel": "SMS",
            "templateId": "SMS_テンプレート_ID",
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
      "flowName": "フロー_名前",
      "description": "フロー_説明",
      "messagePurpose": "NORMAL",
      "steps": {
        "messageChannel": "EMAIL",
        "templateId": "メール_テンプレート_ID",
        "nextSteps": [
          {
            "messageChannel": "ALIMTALK",
            "templateId": "お知らせトーク_テンプレート_ID",
            "nextSteps": [
              {
                "messageChannel": "SMS",
                "templateId": "SMS_テンプレート_ID",
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

### フロー削除

**リクエスト**

```
DELETE /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| flowId | Path | String | Y | フローID |

**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません。」と入力します。-->

このAPIはリクエスト本文を要求しません。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

<!--レスポンス本文のフィールドを説明します。-->

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フロー削除
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
