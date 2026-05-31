<!-- 新しいフォーマットのために追加されたstyleです。 -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 新しいフォーマットのために見出しを<h1>に変更しました。 -->
<h1>フロー</h1>

**Notification > Notification Hub > API v1.0 使用ガイド > フロー**



<span id="flowV1x0001CreateFlow"></span>

## フローの作成

フローを作成します。<br>
フロー作成時、フローIDをレスポンスとして返します。<br>
<br>
**steps**というフィールドにフローの段階を定義できます。<br>
**steps**で定義した順序でメッセージの送信を進行します。<br>
受信者ごとに最初の段階からメッセージの送信を試み、送信と受信に成功すると次の段階へ進まずに完了します。失敗した場合は次の段階へ進みます。<br>


**リクエスト**

```
POST /flow/v1.0/flows
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は"このAPIはリクエスト本文を必要としません"と入力します。-->


```
{
  "flowName" : "フロー名",
  "description" : "フローの説明",
  "messagePurpose" : "NORMAL",
  "steps" : [ {
    "messageChannel" : "PUSH",
    "templateId" : "Tj3nE8dq",
    "nextSteps" : [ ]
  } ]
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| flowName | String | O | フロー名です。最大20文字まで入力できます。 |
| description | String | X | フローの説明です。最大200文字まで入力できます。 |
| messagePurpose | String | O | 送信内容のタイプ<br>デフォルト値：NORMAL<br>[NORMAL(一般)、AD(広告)、AUTH(認証)] |
| steps | Array | O | フローの段階です。 |
| steps[].messageChannel | String | X | メッセージのチャンネルです。<br>[SMS、RCS、ALIMTALK、EMAIL、PUSH] |
| steps[].templateId | String | X | テンプレートのIDです。 |
| steps[].nextSteps | Array | X | 次の段階です。 |

* 上記はEMAIL、お知らせトーク、SMSのテンプレートを使用するフローを作成する例です。
* 一度使用されたメッセージのチャンネルは次の段階で使用できません。
* 1つの段階は複数の次の段階を持つことができます。
* 順序なしで同時に送信したい場合は、最初の段階である**steps**に全てのメッセージのチャンネルを追加します。


**レスポンス本文**

<!--レスポンス本文を返さない場合は"このAPIはレスポンス本文を返しません"と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| flowId | String | O | フローIDです。 |

### フロー定義の例
#### 線形的な順序を持つフロー
```
{
  "flowName": "線形的な順序を持つフロー",
  "messagePurpose": "NORMAL",
  "description": "PUSH > EMAIL > SMSの順で送信されます。",
  "steps": [{
    "messageChannel": "PUSH",
    "templateId": "テンプレートのID",
    "nextSteps": [{
      "messageChannel": "EMAIL",
      "templateId": "テンプレートのID",
      "nextSteps": [{
        "messageChannel": "SMS",
        "templateId": "テンプレートのID",
        "nextSteps": null
      }
      ]
    }
    ]
  }
  ]
}
```

#### 同時送信フロー
```
{
  "flowName": "同時送信",
  "messagePurpose": "NORMAL",
  "description": "PUSH、EMAIL、SMSが順不同で同時に送信されます。",
  "steps": [{
    "messageChannel": "PUSH",
    "templateId": "テンプレートのID",
    "nextSteps": null
  }, {
    "messageChannel": "EMAIL",
    "templateId": "テンプレートのID",
    "nextSteps": null
  }, {
    "messageChannel": "SMS",
    "templateId": "テンプレートのID",
    "nextSteps": null
  }
  ]
}
```


**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フローの作成

POST {{endpoint}}/flow/v1.0/flows
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "flowName" : "フロー名",
  "description" : "フローの説明",
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
  "flowName" : "フロー名",
  "description" : "フローの説明",
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

## フロー一覧の照会

フローの一覧を照会します。<br>
フロー一覧の照会時、フローID、フロー名、フローの説明、フローの段階をレスポンスとして返します。<br>


**リクエスト**

```
GET /flow/v1.0/flows
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| flowName | Query | String | X | フロー名(LIKE検索) |
| flowId | Query | String | X | フローIDです。 |
| limit | Query | Number | X | limitを設定しない場合はデフォルトで50(最大1,000) |
| offset | Query | Number | X | offsetを設定しない場合はデフォルトで0 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は"このAPIはリクエスト本文を必要としません"と入力します。-->

このAPIはリクエスト本文を必要としません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は"このAPIはレスポンス本文を返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "flows" : [ {
    "flowId" : "R2m9Kv0x",
    "flowName" : "フロー名",
    "messagePurpose" : "NORMAL",
    "description" : "フローの説明",
    "steps" : [ {
      "messageChannel" : "PUSH",
      "template" : {
        "templateId" : "Tj3nE8dq",
        "templateName" : "テンプレート名"
      },
      "nextSteps" : [ {
        "messageChannel" : "EMAIL",
        "template" : {
          "templateId" : "Tj3nE8dq",
          "templateName" : "テンプレート名"
        },
        "nextSteps" : [ {
          "messageChannel" : "ALIMTALK",
          "template" : {
            "templateId" : "Tj3nE8dq",
            "templateName" : "テンプレート名"
          },
          "nextSteps" : [ {
            "messageChannel" : "SMS",
            "template" : {
              "templateId" : "Tj3nE8dq",
              "templateName" : "テンプレート名"
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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| flows | Array | O |  |
| flows[].flowId | String | O | フローIDです。 |
| flows[].flowName | String | O | フロー名です。 |
| flows[].messagePurpose | String | O | 送信内容のタイプ<br>デフォルト値：NORMAL<br>[NORMAL(一般)、AD(広告)、AUTH(認証)] |
| flows[].description | String | X | フローの説明です。 |
| flows[].steps | Array | O | フローの段階です。 |
| flows[].steps[].messageChannel | String | O | メッセージのチャンネルです。<br>[ALIMTALK、EMAIL、PUSH、RCS、SMS] |
| flows[].steps[].template | Object | O |  |
| flows[].steps[].template.templateId | String | O | テンプレートのIDです。 |
| flows[].steps[].template.templateName | String | X | テンプレート名です。 |
| flows[].steps[].nextSteps | Array | X | 次の段階です。 |
| flows[].messageChannels | Array | O | フローの段階で使用されたメッセージのチャンネルです。<br>[ALIMTALK、EMAIL、PUSH、RCS、SMS] |
| flows[].createdDateTime | String | O | フローの作成時間です。 |
| flows[].updatedDateTime | String | O | フローの変更時間です。 |
| totalCount | Integer | O | フローの総数です。 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フロー一覧の照会

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

## フローの照会

フローを照会します。<br>
フローの照会時、フローID、フロー名、フローの説明、フローの段階をレスポンスとして返します。<br>


**リクエスト**

```
GET /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| flowId | Path | String | O | フローIDです。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は"このAPIはリクエスト本文を必要としません"と入力します。-->

このAPIはリクエスト本文を必要としません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は"このAPIはレスポンス本文を返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "flow" : {
    "flowId" : "R2m9Kv0x",
    "flowName" : "フロー名",
    "messagePurpose" : "NORMAL",
    "description" : "フローの説明",
    "steps" : [ {
      "messageChannel" : "PUSH",
      "template" : {
        "templateId" : "Tj3nE8dq",
        "templateName" : "テンプレート名"
      },
      "nextSteps" : [ {
        "messageChannel" : "EMAIL",
        "template" : {
          "templateId" : "Tj3nE8dq",
          "templateName" : "テンプレート名"
        },
        "nextSteps" : [ {
          "messageChannel" : "ALIMTALK",
          "template" : {
            "templateId" : "Tj3nE8dq",
            "templateName" : "テンプレート名"
          },
          "nextSteps" : [ {
            "messageChannel" : "SMS",
            "template" : {
              "templateId" : "Tj3nE8dq",
              "templateName" : "テンプレート名"
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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| flow | Object | O |  |
| flow.flowId | String | O | フローIDです。 |
| flow.flowName | String | O | フロー名です。 |
| flow.messagePurpose | String | O | 送信内容のタイプ<br>デフォルト値：NORMAL<br>[NORMAL(一般)、AD(広告)、AUTH(認証)] |
| flow.description | String | X | フローの説明です。 |
| flow.steps | Array | O | フローの段階です。 |
| flow.steps[].messageChannel | String | O | メッセージのチャンネルです。<br>[ALIMTALK、EMAIL、PUSH、RCS、SMS] |
| flow.steps[].template | Object | O |  |
| flow.steps[].template.templateId | String | O | テンプレートのIDです。 |
| flow.steps[].template.templateName | String | X | テンプレート名です。 |
| flow.steps[].nextSteps | Array | X | 次の段階です。 |
| flow.messageChannels | Array | O | フローの段階で使用されたメッセージのチャンネルです。<br>[ALIMTALK、EMAIL、PUSH、RCS、SMS] |
| flow.createdDateTime | String | O | フローの作成時間です。 |
| flow.updatedDateTime | String | O | フローの変更時間です。 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フローの照会

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

## フローの変更

フローを変更します。<br>


**リクエスト**

```
PUT /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| flowId | Path | String | O | フローIDです。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は"このAPIはリクエスト本文を必要としません"と入力します。-->


```
{
  "flowName" : "フロー名",
  "description" : "フローの説明",
  "messagePurpose" : "NORMAL",
  "steps" : [ {
    "messageChannel" : "PUSH",
    "templateId" : "Tj3nE8dq",
    "nextSteps" : [ ]
  } ]
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| flowName | String | O | フロー名です。最大20文字まで入力できます。 |
| description | String | X | フローの説明です。最大200文字まで入力できます。 |
| messagePurpose | String | O | 送信内容のタイプ<br>デフォルト値：NORMAL<br>[NORMAL(一般)、AD(広告)、AUTH(認証)] |
| steps | Array | O | フローの段階です。 |
| steps[].messageChannel | String | X | メッセージのチャンネルです。<br>[SMS、RCS、ALIMTALK、EMAIL、PUSH] |
| steps[].templateId | String | X | テンプレートのIDです。 |
| steps[].nextSteps | Array | X | 次の段階です。 |



**レスポンス本文**

<!--レスポンス本文を返さない場合は"このAPIはレスポンス本文を返しません"と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| flowId | String | O | フローIDです。 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フローの変更

PUT {{endpoint}}/flow/v1.0/flows/{{flowId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "flowName" : "フロー名",
  "description" : "フローの説明",
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
  "flowName" : "フロー名",
  "description" : "フローの説明",
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

## フローの削除

フローを削除します。<br>


**リクエスト**

```
DELETE /flow/v1.0/flows/{flowId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| flowId | Path | String | O | フローIDです。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は"このAPIはリクエスト本文を必要としません"と入力します。-->

このAPIはリクエスト本文を必要としません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は"このAPIはレスポンス本文を返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フローの削除

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

## フローの削除

フローを削除します。<br>


**リクエスト**

```
POST /flow/v1.0/flows/do-delete
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は"このAPIはリクエスト本文を必要としません"と入力します。-->


```
{
  "flowIds" : [ "R2m9Kv0x" ]
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| flowIds | Array | O | フローIDです。 |



**レスポンス本文**

<!--レスポンス本文を返さない場合は"このAPIはレスポンス本文を返しません"と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | X |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| results | Array | X | 一括処理リクエストの結果です。 |
| results[].isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| results[].resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| results[].resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フローの削除

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
