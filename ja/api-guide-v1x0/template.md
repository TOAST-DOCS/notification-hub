<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>テンプレート</h1>

**Notification > Notification Hub > API v1.0使用ガイド > テンプレート**

## テンプレート

<span id="create-template"></span>

### テンプレート作成

**リクエスト**

```
POST /template/v1.0/{messageChannel}/templates
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |

**リクエスト本文**

```json
{
  "templateName": "テンプレート_名前",
  "categoryId": "テンプレート_カテゴリー_ID",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "content": {
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub]告知事項",
    "body": "こんにちは。 NHN Cloud Notification Hubです。",
    "attachmentIds": [
      "添付_ファイル_ID"
    ]
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

| 名前 | タイプ | 必須 | 説明                              |
| --- | --- | --- |-----------------------------------|
| templateName | String | Y | テンプレート名                          |
| categoryId | String | Y | テンプレートカテゴリーID                      |
| messagePurpose | String | Y | メッセージ目的                          |
| templateLanguage | String | Y | テンプレート言語<br>PLAIN_TEXT, FREE_MARKER |
| sender | Object | Y | 発信者                             |
| content | Object | Y | 内容                              |

* テンプレートカテゴリーはテンプレートカテゴリーAPIを利用して作成できます。
* テンプレート言語はPLAIN_TEXT、FREE_MARKERのいずれかを選択します。
* テンプレート言語がFREE_MARKERの場合テンプレート内容にFREE_MARKER文法を使用できます。
* **sender**, **content**フィールドは自由形式メッセージ送信APIのリクエスト本文と同じです。

#### メッセージチャンネル別senderフィールド

| メッセージチャンネル | フィールド | 説明                      |
| --- | --- |---------------------------|
| SMS | sender.senderPhoneNumber | 発信者番号                  |
| RCS | sender.brandId | ブランドID                   |
| RCS | sender.chatbotId | チャットルームID                   |
| EMAIL | sender.senderMailAddress | 発信者メールアドレス              |
| ALIMTALK | sender.senderKey | 発信キー                      |
| ALIMTALK | sender.senderProfileType | 発信プロフィールタイプ<br>GROUP, NORMAL |

* お知らせトーク(ALIMTALK)は発信キー(senderKey)と発信プロフィールタイプ(senderProfileType)を必ず入力する必要があります。
* 発信者プロフィールタイプは**GROUP(グループ)**と **NORMAL(一般)**があります。**GROUP**はグループ発信者プロフィール、 **NORMAL**は一般発信者プロフィールです。

### お知らせトークテンプレート詳細リクエスト本文

* お知らせトークを送信するためには、テンプレートの登録が必須です。
* お知らせトークテンプレートを登録すると、カカオビジネスの検収と承認の過程を経て承認完了後に使用できます。
* お知らせトークテンプレートは検収と承認過程でカカオビジネス検収担当者と絡を取り合うことができます。
    * [カカオトークチャンネル管理者センター](https://center-pf.kakao.com)
    * お知らせトークテンプレートは**お知らせトークテンプレートお問い合わせ**, **お知らせトークテンプレートファイル添付お問い合わせ**, **お知らせトークテンプレート修正履歴照会**APIを追加で提供します。

```json
{
  "templateName": "テンプレート名",
  "categoryId": "カテゴリー_ID",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderKey": "発信_キー",
    "senderProfileType": "GROUP"
  },
  "content": {
    "templateMessageType": "BA",
    "templateEmphasizeType": "NONE",
    "templateContent": "#{名前}さんの注文が完了しました。",
    "templateAd": "チャンネルを追加し、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
    "templateExtra": "* リアルタイム予約の特性上、重複予約が発生する可能性があり、入室が不可能な場合、予約がキャンセルされる場合があります。\\n* お問い合わせ電話: 1234-1234",
    "templateTitle": "123,450KRW",
    "templateSubtitle": "承認履歴",
    "templateHeader": "注文が成立しました。",
    "templateItem": {
      "list": [],
      "summary": {
        "title": "string",
        "description": "string"
      }
    },
    "templateItemHighlight": {
      "title": "string",
      "description": "string",
      "attachmentId": "YaX2DA4Weab2",
      "imageUrl": "string"
    },
    "templateRepresentLink": {
      "linkMo": "string",
      "linkPc": "string",
      "schemeIos": "string",
      "schemeAndroid": "string"
    },
    "attachmentId": "YaX2DA4Weab2",
    "templateImageName": "image.png",
    "templateImageUrl": "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "securityFlag": false,
    "categoryCode": "999999",
    "buttons": [],
    "quickReplies": []
  },
  "additionalProperty": {
    "templateCode": "templateCode",
    "kakaoTemplateCode": "kakaoTemplateCode",
    "comments": [],
    "status": "APR",
    "templateModificationStatus": "APR",
    "block": false,
    "dormant": false
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |

<!--TODO:リクエスト本文のフィールドを説明します。-->


**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "templateId": "テンプレート_ID"
}
```

<!--レスポンス本文のフィールドを説明します。-->

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### テンプレート作成
POST {{endpoint}}/template/v1.0/{{messageChannel}}/templates
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "templateName": "テンプレート_名前",
  "categoryId": "テンプレート_カテゴリー_ID",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "content": {
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub]告知事項",
    "body": "こんにちは。 NHN Cloud Notification Hubです。",
    "attachmentIds": [
      "添付_ファイル_ID"
    ]
  }
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/templates" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
        "templateName": "テンプレート_名前",
        "categoryId": "テンプレート_カテゴリー_ID",
        "messagePurpose": "NORMAL",
        "templateLanguage": "PLAIN_TEXT",
        "sender": {
          "senderPhoneNumber": "01012341234"
        },
        "content": {
          "messageType": "MMS",
          "title": "[NHN Cloud Notification Hub]告知事項",
          "body": "こんにちは。 NHN Cloud Notification Hubです。",
          "attachmentIds": [
            "添付_ファイル_ID"
          ]
        }
      }'
```

</details>

<span id="get-templates"></span>

### テンプレートリスト照会

**リクエスト**

```
GET /template/v1.0/{messageChannel}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前         | 区分 | タイプ | 必須 | 説明                      |
|--------------| --- | --- | --- |---------------------------|
| appKey       | Header | String | Y | アプリキー                      |
| accessToken  | Header | String | Y | 認証トークン                   |
| templateName | Query | String | N | テンプレート名、プレフィックス(Prefix)検索可能 |
| limit        | Query | Integer | N | 照会数(デフォルト値: 20)            |
| offset       | Query | Integer | N | 照会開始位置(デフォルト値: 0)          |

**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。 -->

このAPIはリクエスト本文を要求しません。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "templates": [
    {
      "templateId": "テンプレート_ID",
      "templateName": "テンプレート_名前",
      "categoryId": "テンプレート_カテゴリー_ID",
      "messagePurpose": "NORMAL",
      "templateLanguage": "PLAIN_TEXT",
      "sender": {
        "senderPhoneNumber": "01012341234"
      },
      "content": {
        "messageType": "MMS",
        "title": "[NHN Cloud Notification Hub]告知事項",
        "body": "こんにちは。 NHN Cloud Notification Hubです。",
        "attachmentIds": [
          "添付_ファイル_ID"
        ]
      },
      "createdDateTime": "2023-01-01T00:00:00Z",
      "updatedDateTime": "2023-01-01T00:00:00Z"
    }
  ],
  "totalCount": 1
}
```

<!--レスポンス本文のフィールドを説明します。-->

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### テンプレートリスト照会
GET {{endpoint}}/template/v1.0/{{messageChannel}}/templates
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/templates" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

<span id="get-template"></span>

### テンプレート照会

**リクエスト**

```
GET /template/v1.0/{messageChannel}/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| templateId | Path | String | Y | テンプレートID |

**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。 -->

このAPIはリクエスト本文を要求しません。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "template": {
    "templateId": "テンプレート_ID",
    "templateName": "テンプレート_名前",
    "categoryId": "テンプレート_カテゴリー_ID",
    "messagePurpose": "NORMAL",
    "templateLanguage": "PLAIN_TEXT",
    "sender": {
      "senderPhoneNumber": "01012341234"
    },
    "content": {
      "messageType": "MMS",
      "title": "[NHN Cloud Notification Hub]告知事項",
      "body": "こんにちは。 NHN Cloud Notification Hubです。",
      "attachmentIds": [
        "添付_ファイル_ID"
      ]
    },
    "createdDateTime": "2023-01-01T00:00:00Z",
    "updatedDateTime": "2023-01-01T00:00:00Z"
  }
}
```

<!--レスポンス本文のフィールドを説明します。-->

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### テンプレート照会
GET {{endpoint}}/template/v1.0/{{messageChannel}}/templates/{templateId}
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/templates/${TEMPLATE_ID}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

<span id="put-template"></span>

### テンプレート修正

**リクエスト**

```
PUT /template/v1.0/{messageChannel}/templates/{templateId}
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| templateId | Path | String | Y | テンプレートID |

**リクエスト本文**

```json
{
  "templateName": "テンプレート_名前",
  "categoryId": "テンプレート_カテゴリー_ID",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "content": {
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub]告知事項",
    "body": "こんにちは。 NHN Cloud Notification Hubです。",
    "attachmentIds": [
      "添付_ファイル_ID"
    ]
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

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
### テンプレート修正
PUT {{endpoint}}/template/v1.0/{{messageChannel}}/templates/{templateId}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "templateName": "テンプレート_名前",
  "categoryId": "テンプレート_カテゴリー_ID",
  "messagePurpose": "NORMAL",
  "templateLanguage": "PLAIN_TEXT",
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "content": {
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub]告知事項",
    "body": "こんにちは。 NHN Cloud Notification Hubです。",
    "attachmentIds": [
      "添付_ファイル_ID"
    ]
  }
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X PUT "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/templates/${TEMPLATE_ID}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
        "templateName": "テンプレート_名前",
        "categoryId": "テンプレート_カテゴリー_ID",
        "messagePurpose": "NORMAL",
        "templateLanguage": "PLAIN_TEXT",
        "sender": {
          "senderPhoneNumber": "01012341234"
        },
        "content": {
          "messageType": "MMS",
          "title": "[NHN Cloud Notification Hub]告知事項",
          "body": "こんにちは。 NHN Cloud Notification Hubです。",
          "attachmentIds": [
            "添付_ファイル_ID"
          ]
        }
      }'
```

</details>

<span id="delete-template"></span>

### テンプレート削除

**リクエスト**

```
DELETE /template/v1.0/{messageChannel}/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| templateId | Path | String | Y | テンプレートID |

**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。 -->

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
### テンプレート削除
DELETE {{endpoint}}/template/v1.0/{{messageChannel}}/templates/{templateId}
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X DELETE "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/templates/${TEMPLATE_ID}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

### お知らせトークテンプレートお問い合わせ

**リクエスト**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/inquiries
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| templateId | Path | String | Y | テンプレートID |

**リクエスト本文**

```json
{
  "comment": "お問い合わせ内容"
}
```

<!--リクエスト本文のフィールドを説明します。-->

| 名前 | タイプ | 必須 | 説明              |
| --- | --- | --- |-------------------|
| comment | String | Y | お問い合わせ内容(最大長さ: 500) |

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
### お知らせトークテンプレートお問い合わせ
POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{templateId}/inquiries
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "comment": "お問い合わせ内容"
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/template/v1.0/ALIMTALK/templates/${TEMPLATE_ID}/inquiries" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
        "comment": "お問い合わせ内容"
      }'
```

</details>

### お知らせトークテンプレートファイル添付お問い合わせ

**リクエスト**

```
POST /template/v1.0/ALIMTALK/templates/${TEMPLATE_ID}/inquiries/do-with-file
Content-Type: multipart/form-data
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| templateId | Path | String | Y | テンプレートID |
| comment | Query | String | Y | お問い合わせ内容(最大長さ: 500) |

**リクエスト本文**

* ファイル添付は**multipart/form-data**でリクエストします。
* **form-data**に**file** フィールドにファイルデータを設定します。

```
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="file"; filename="attachment.xlsx"
Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet

<ファイルデータ>
------WebKitFormBoundary7MA4YWxkTrZu0gW--
```

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

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレートファイル添付お問い合わせ
POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{templateId}/inquiries/do-with-file?fileName=attachment.xlsx
Content-Type: multipart/form-data
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

--boundary
Content-Disposition: form-data; name="file"; fileName="attachment.xlsx"
Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet


< ./file/attachment.xlsx
--boundary--
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/template/v1.0/ALIMTALK/templates/${TEMPLATE_ID}/inquiries/do-with-file?fileName=attachment.xlsx" \
     -H "Content-Type: multipart/form-data" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -F "file=@./file/attachment.xlsx"
```

</details>

### お知らせトークテンプレート修正履歴照会

**リクエスト**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}/modifications
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| templateId | Path | String | Y | テンプレートID |

**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。 -->

このAPIはリクエスト本文を要求しません。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "templates": [
    {
      "templateId": "テンプレート_ID",
      "templateName": "テンプレート_名前",
      "categoryId": "テンプレート_カテゴリー_ID",
      "messageChannel": "ALIMTALK",
      "messagePurpose": "NORMAL",
      "templateLanguage": "PLAIN_TEXT",
      "sender": {
        "senderKey": "発信者_キー",
        "senderProfileId": "発信者_プロフィール_ID",
        "senderProfileType": "GROUP"
      },
      "content": {
          "templateMessageType": "BA",
          "templateEmphasizeType": "NONE",
          "templateContent": "#{名前}さんの注文が完了しました。",
            "templateAd": "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
            "templateExtra": "* リアルタイム予約の特性上、重複予約が発生する可能性があり、入室が不可能な場合、予約がキャンセルされる場合があります。\\n* お問い合わせ電話: 1234-1234",
            "templateTitle": "123,450KRW",
            "templateSubtitle": "承認履歴",
            "templateHeader": "注文が成立しました。",
            "templateItem": {
              "list": [
                {
                "title": "タイトル",
                "description": "説明"
                }
              ],
              "summary": {
                "title": "タイトル",
                "description": "説明"
              }
            },
            "templateItemHighlight": {
              "title": "タイトル",
              "description": "説明",
              "attachmentId": "ハイライト_すでに_添付ファイル_ID",
              "imageUrl": "ハイライト_画像_リンク"
            },
            "templateRepresentLink": {
              "linkMo": "モバイル_リンク",
              "linkPc": "PC_リンク",
              "schemeIos": "iOS_リンク",
              "schemeAndroid": "Android_リンク"
            },
            "attachmentId": "添付_ファイル_ID",
            "templateImageName": "画像_ファイル_名前",
            "templateImageUrl": "画像_リンク",
            "securityFlag": false,
            "categoryCode": "999999",
            "buttons": [
              {
                "ordering": 1,
                "type": "WL",
                "name": "ボタン_名前",
                "linkMo": "モバイル_リンク",
                "linkPc": "PC_リンク",
                "schemeIos": "iOS_リンク",
                "schemeAndroid": "Android_リンク",
                "bizFormId": 1
              }
            ],
            "quickReplies": [
              {
                "ordering": 1,
                "type": "WL",
                "name": "ボタン_名前",
                "linkMo": "モバイル_リンク",
                "linkPc": "PC_リンク",
                "schemeIos": "iOS_リンク",
                "schemeAndroid": "Android_リンク",
                "bizFormId": 1
              }
            ]
      },
      "createdDateTime": "2023-01-01T00:00:00Z",
      "updatedDateTime": "2023-01-01T00:00:00Z"
    }
  ],
  "totalCount": 1
}
```

<!--レスポンス本文のフィールドを説明します。-->

| 名前 | タイプ          | 説明              |
| --- |---------------| ------------------|
| templateCode         | String        | テンプレートコード(最大20文字) |
| templateName         | String        | テンプレート名(最大150文字) |
| templateContent      | String        | テンプレート本文(最大1000文字) |
| templateMessageType  | String        | テンプレートメッセージタイプ<br>BA:基本型, EX:付加情報型, AD:チャンネル追加型, MI:複合型(デフォルト値: BA) |
| templateEmphasizeType| String        | テンプレート強調表示タイプ<br>NONE:基本、 TEXT:強調表示、 IMAGE:画像型、 ITEM_LIST:アイテムリスト型(デフォルト値: NONE)<br>- TEXT選択時: templateTitle, templateSubtitle必須<br>- IMAGE選択時: templateImageName, templateImageUrl必須<br>- ITEM_LIST選択時:画像、ヘッダ、アイテムハイライト、アイテムリスト中1個以上必須 |
| templateExtra        | String        | テンプレート付加情報<br>テンプレートメッセージタイプが付加情報型または複合型の場合必須 |
| templateTitle        | String        | テンプレートタイトル(最大50文字)<br>Android: 2行、23文字以上の場合、短縮処理<br>iOS: 2行、27文字以上の場合、短縮処理 |
| templateSubtitle     | String        | テンプレート補助文言(最大50文字)<br>Android: 18文字以上の場合、短縮処理<br>iOS: 21文字以上の場合、短縮処理 |
| templateHeader       | String        | テンプレートヘッダ(最大16文字) |
| templateItem         | Object        | アイテム |
| templateItem.list    | Object Array | アイテムリスト(最小2個、最大10個) |
| templateItem.list.title | String        | タイトル(最大6文字) |
| templateItem.list.description | String        | ディスクリプション(最大23文字) |
| templateItem.summary | Object        | アイテム要約情報 |
| templateItem.summary.title | String        | タイトル(最大6文字) |
| templateItem.summary.description | String        | ディスクリプション(変数及び貨幣単位、数字、カンマ、ピリオドのみ使用可能、最大14文字) |
| templateItemHighlight | Object        | アイテムハイライト |
| templateItemHighlight.title | String        | タイトル(最大30文字、サムネイル画像がある場合21文字) |
| templateItemHighlight.description | String        | ディスクリプション(最大19文字、サムネイル画像がある場合13文字) |
| templateItemHighlight.imageUrl | String        | サムネイル画像アドレス |
| templateRepresentLink | Object        | 代表リンク |
| templateRepresentLink.linkMo | String        | モバイルWebリンク(最大500文字) |
| templateRepresentLink.linkPc | String        | PC Webリンク(最大500文字) |
| templateRepresentLink.schemeIos | String        | iOSアプリリンク(最大500文字) |
| templateRepresentLink.schemeAndroid | String        | Androidアプリリンク(最大500文字) |
| templateImageName   | String        | 画像名(アップロードしたファイル名) |
| templateImageUrl    | String        | 画像URL |
| securityFlag        | Boolean       | セキュリティテンプレートかどうか<br>OTPなどセキュリティメッセージの場合に設定<br>送信時にメインデバイス以外のデバイスにメッセージテキストを表示しない(デフォルト値: false) |
| categoryCode        | String        | テンプレートカテゴリーコード(テンプレートカテゴリー照会API参考、デフォルト値: 999999)<br>カテゴリーその他の場合、最下位優先順位で審査 |
| buttons             | Object Array | ボタンリスト(最大5個) |
| buttons[].ordering    | Integer       | ボタン順序(1～5) |
| buttons[].type        | String        | ボタンタイプ<br>WL: Webリンク、 AL:アプリリンク、 DS:配送照会、 BK: Botキーワード、 MD:メッセージ伝達、 BC:相談トーク切り替え, BT: Bot切り替え, AC:チャンネル追加、 BF:ビジネスフォーム, P1:画像セキュリティ送信プラグインID, P2:個人情報利用プラグインID, P3:ワンクリック決済プラグインID |
| buttons[].name        | String        | ボタン名(ボタンがある場合必須、最大14文字) |
| buttons[].linkMo      | String        | モバイルWebリンク(WLタイプの場合必須フィールド、最大500文字) |
| buttons[].linkPc      | String        | PC Webリンク(WLタイプの場合選択フィールド、最大500文字) |
| buttons[].schemeIos   | String        | iOSアプリリンク(ALタイプの場合必須フィールド、最大500文字) |
| buttons[].schemeAndroid | String        | Androidアプリリンク(ALタイプの場合必須フィールド、最大500文字) |
| buttons[].bizFormId   | Integer       | ビジネスフォームID (BFタイプの場合必須) |
| buttons[].pluginId    | String        | プラグインID (最大24文字) |
| quickReplies        | Object Array         | クイック接続リスト(最大5個) |
| quickReplies[].ordering | Integer       | クイック接続順序(クイック接続がある場合、必須) |
| quickReplies[].type   | String        | クイック接続タイプ<br>WL: Webリンク、 AL:アプリリンク、 BK: Botキーワード、 BC:相談トーク切り替え、 BT: Bot切り替え、 BF:ビジネスフォーム |
| quickReplies[].name   | String        | クイック接続名(クイック接続がある場合必須、最大14文字) |
| quickReplies[].linkMo | String        | モバイルWebリンク(WLタイプの場合必須フィールド、最大500文字) |
| quickReplies[].linkPc | String        | PC Webリンク(WLタイプの場合、任意フィールド、最大500文字) |
| quickReplies[].schemeIos | String        | iOSアプリリンク(ALタイプの場合必須フィールド、最大500文字) |
| quickReplies[].schemeAndroid | String        | Androidアプリリンク(ALタイプの場合、必須フィールド、最大500文字) |
| quickReplies[].bizFormId | Integer       | ビジネスフォームID (BFタイプの場合、必須) |

* チャンネル追加型(AD)または複合型(MI)メッセージタイプテンプレート登録時、templateAd値が固定されます。
* チャンネル追加型(AD)または複合型(MI)メッセージタイプテンプレート登録時、チャンネル追加(AC)ボタンが最初の順番に位置する必要があります。
* チャンネル追加(AC)ボタンのボタン名は「チャンネル追加」に固定して登録する必要があります。

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレート修正履歴照会
GET {{endpoint}}/template/v1.0/ALIMTALK/templates/{templateId}/modifications
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/template/v1.0/ALIMTALK/templates/${TEMPLATE_ID}/modifications" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

---

### テンプレートカテゴリー作成

**リクエスト**

```
POST /template/v1.0/{messageChannel}/categories
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| messageChannel | Path | String | Y | メッセージチャンネル<br>SMS, RCS, ALIMTALK, EMAIL, PUSH |

**リクエスト本文**

```json
{
  "parentCategoryId": "上位_カテゴリー_ID",
  "name": "カテゴリー_名前"
}
```

<!--リクエスト本文のフィールドを説明します。-->

| 名前 | タイプ | 必須 | 説明              |
| --- | --- | --- |-------------------|
| parentCategoryId | String | 任意 | 上位カテゴリーID |
| name | String | 必須 | カテゴリー名(最大50文字) |

* 最上位カテゴリーはデフォルトで作成されています。最上位カテゴリーIDは**ROOT**です。
* 新しいカテゴリーは最上位カテゴリーを下位から作成できます。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "categoryId": "カテゴリー_ID"
}
```

<!--レスポンス本文のフィールドを説明します。-->

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### カテゴリー作成
POST {{endpoint}}/template/v1.0/{{messageChannel}}/categories
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "parentCategoryId": "上位_カテゴリー_ID",
  "name": "カテゴリー_名前"
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
     -d '{
         "parentCategoryId": "上位_カテゴリー_ID",
         "name": "カテゴリー_名前"
     }'
```

</details>

### カテゴリーリスト照会

**リクエスト**

```
GET /template/v1.0/{messageChannel}/categories
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| messageChannel | Path | String | Y | メッセージチャンネル<br>SMS, RCS, ALIMTALK, EMAIL, PUSH |

**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。 -->

このAPIはリクエスト本文を要求しません。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "categories": [
    {
      "categoryId": "カテゴリー_ID",
      "name": "カテゴリー_名前",
      "parentCategoryId": "上位_カテゴリー_ID",
      "categoryIds": [
        "下位_カテゴリー_ID"
      ],
      "templateIds": [
        "カテゴリーに属するテンプレート_ID"
      ]
    }
  ]
}
```

<!--TODO: categoryIds => childCategoryIdsに名前変更必要-->
<!--TODO: totalCount追加必要-->

<!--レスポンス本文のフィールドを説明します。-->

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### カテゴリーリスト照会
GET {{endpoint}}/template/v1.0/{{messageChannel}}/categories
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

### カテゴリーツリー照会

**リクエスト**

```
GET /template/v1.0/{messageChannel}/category-tree
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明                                                   |
| --- | --- | --- | --- |--------------------------------------------------------|
| appKey | Header | String | Y | アプリキー                                                   |
| accessToken | Header | String | Y | 認証トークン                                                |
| messageChannel | Path | String | Y | メッセージチャンネル<br>SMS, RCS, ALIMTALK, EMAIL, PUSH  |
| categoryTemplateName | Query | String | N | カテゴリーまたはテンプレート名、プレフィックス(Prefix)検索可能                    |

<!--TODO: statusフィールドがないため、必要かどうか確認が必要-->

**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。 -->

このAPIはリクエスト本文を要求しません。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "categories": [
    {
      "categoryId": "ROOT",
      "categoryName": "Root Category",
      "parentCategoryId": null,
      "messageChannel": "SMS",
      "categories": [
        {
          "categoryId": "カテゴリー_ID",
          "categoryName": "カテゴリー_名前",
          "parentCategoryId": "ROOT",
          "messageChannel": "SMS",
          "categories": [
            {
              "categoryId": "カテゴリー_ID",
              "categoryName": "カテゴリー_名前",
              "parentCategoryId": "6XAeH2yo",
              "messageChannel": "SMS",
              "categories": [],
              "templates": [
                {
                  "templateId": "テンプレート_ID",
                  "templateName": "テンプレート_名前"
                },
                {
                  "templateId": "テンプレート_ID",
                  "templateName": "テンプレート_名前"
                }
              ]
            }
          ],
          "templates": []
        }
      ],
      "templates": []
    }
  ]
}
```

<!--レスポンス本文のフィールドを説明します。-->

| 名前                    | タイプ          | 説明              |
|-------------------------|---------------|-------------------|
| categories.[]categoryId | String        | カテゴリーID |
| categories.[]categoryName            | String        | カテゴリー名 |
| categories.[]parentCategoryId        | String        | 上位カテゴリーID |
| categories.[]messageChannel          | String        | メッセージチャンネル<br>SMS, RCS, ALIMTALK, EMAIL, PUSH |
| categories.[]categories              | Object Array | 下位カテゴリーリスト |
| categories.[]templates               | Object Array         | テンプレートリスト |
| categories.[]templates.[]templateId  | String        | テンプレートID |
| categories.[]templates.[]templateName| String        | テンプレート名 |

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### カテゴリーツリー照会
GET {{endpoint}}/template/v1.0/{{messageChannel}}/category-tree
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/category-tree" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

### カテゴリー照会

**リクエスト**

```
GET /template/v1.0/{messageChannel}/categories/{categoryId}
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| messageChannel | Path | String | Y | メッセージチャンネル<br>SMS, RCS, ALIMTALK, EMAIL, PUSH |
| categoryId | Path | String | Y | カテゴリーID |

**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。 -->

このAPIはリクエスト本文を要求しません。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "category": {
    "categoryId": "カテゴリー_ID",
    "categoryName": "カテゴリー_名前",
    "parentCategoryId": "上位_カテゴリー_ID",
    "messageChannel": "SMS",
    "categoryIds": [
      "下位_カテゴリー_ID"
    ],
    "templateIds": [
      "カテゴリーに_属する_テンプレート_ID"
    ]
  }
}
```

<!--TODO:カテゴリー名をname or categoryNameにするか統一必要、 nameに変更必要-->

<!--レスポンス本文のフィールドを説明します。-->

**リクエスト例**


<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### メッセージチャンネル別カテゴリー照会
GET {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories/{categoryId}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

### カテゴリー修正

**リクエスト**

```
PUT /template/v1.0/{messageChannel}/categories/{categoryId}
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| messageChannel | Path | String | Y | メッセージチャンネル<br>SMS, RCS, ALIMTALK, EMAIL, PUSH |
| categoryId | Path | String | Y | カテゴリーID |

**リクエスト本文**

```json
{
  "parentCategoryId": "上位_カテゴリー_ID",
  "name": "カテゴリー_名前"
}
```

<!--リクエスト本文のフィールドを説明します。-->

| 名前 | タイプ | 必須 | 説明              |
| --- | --- | --- |-------------------|
| parentCategoryId | String | 任意 | 上位カテゴリーID |
| name | String | 必須 | カテゴリー名(最大50文字) |

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
### カテゴリー修正
PUT {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "parentCategoryId": "上位_カテゴリー_ID",
  "name": "カテゴリー_名前"
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X PUT "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories/{categoryId}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
         "parentCategoryId": "上位_カテゴリー_ID",
         "name": "カテゴリー_名前"
     }'
```

</details>

### テンプレートカテゴリーにテンプレート追加

**リクエスト**

```
POST /template/v1.0/${MESSAGE_CHANNEL}/categories/${CATEGORY_ID}/templates
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| messageChannel | Path | String | Y | メッセージチャンネル<br>SMS, RCS, ALIMTALK, EMAIL, PUSH |

**リクエスト本文**

```json
{
  "templateId": "テンプレート_ID"
}
```

<!--リクエスト本文のフィールドを説明します。-->

| 名前 | タイプ | 必須 | 説明              |
| --- | --- | --- |-------------------|
| templateId | String | 必須 | テンプレートID |

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
### テンプレートカテゴリーにテンプレート追加
POST {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}/templates
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}

{
  "templateId": "テンプレート_ID"
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories/${CATEGORY_ID}/templates" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
         "templateId": "テンプレート_ID"
     }'
```

</details>

### カテゴリー削除

**リクエスト**

```
DELETE /template/v1.0/{messageChannel}/categories/{categoryId}
Content-Type: application/json
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| messageChannel | Path | String | Y | メッセージチャンネル<br>SMS, RCS, ALIMTALK, EMAIL, PUSH |
| categoryId | Path | String | Y | カテゴリーID |

**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。 -->
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
### カテゴリー削除
DELETE {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorization}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X DELETE "${ENDPOINT}/template/v1.0/${MESSAGE_CHANNEL}/categories/${CATEGORY_ID}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>
