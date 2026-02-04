<!-- 新しい様式のために追加されたスタイルです。 -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 新しい様式のためにタイトルを <h1> に変更しました。 -->
<h1>テンプレート</h1>

**Notification > Notification Hub > API v1.0使用ガイド > テンプレート**



<span id="templateV1x0001CreateSmsTemplate"></span>

## SMSテンプレート登録

テンプレートを登録します。

**リクエスト**

```
POST /template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->


```
{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | Y | テンプレート名 |
| categoryId | String | N | カテゴリーID |
| messagePurpose | String | N | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.senderPhoneNumber | String | N | 発信番号 |
| content | Object | Y |  |
| content.messageType | String | N | 送信メッセージタイプ(SMS、LMS、MMS)<br>[SMS、LMS、MMS] |
| content.title | String | N | メッセージ件名 |
| content.body | String | N | メッセージ本文 |
| content.attachmentIds | Array | N | 添付ファイルID 最大3個 |



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "templateId" : "A9z0A9z0"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| templateId | String | テンプレート登録時に発行されたテンプレートID |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMSテンプレート登録

POST {{endpoint}}/template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/SMS/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>
<span id="templateV1x0002ReadSmsTemplateList"></span>

## SMSテンプレートリスト照会

テンプレートリストを照会します。

**リクエスト**

```
GET /template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateName | Query  | String | N | テンプレート名(LIKE検索) |
| limit | Query  | Integer | N | limitを設定しない場合はデフォルト20(最大1000) |
| offset | Query  | Integer | N | offsetを設定しない場合はデフォルト0 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "配送完了",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| totalCount | Integer | 総件数 |
| templates | Array |  |
| templates[].templateId | String | テンプレート登録時に発行されたテンプレートID |
| templates[].templateName | String | テンプレート名 |
| templates[].categoryId | String | カテゴリーID |
| templates[].messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | テンプレート作成日時 |
| templates[].updatedDateTime | String | テンプレート修正日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMSテンプレートリスト照会

GET {{endpoint}}/template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/SMS/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0003ReadSmsTemplate"></span>

## SMSテンプレート詳細照会

テンプレートを詳細照会します。

**リクエスト**

```
GET /template/v1.0/SMS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "テンプレート名",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "sender" : {
      "senderPhoneNumber" : "01012341234"
    },
    "content" : {
      "messageType" : "SMS",
      "title" : "祝日の営業時間のお知らせ",
      "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください^^",
      "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| template | Object |  |
| template.templateId | String | テンプレート登録時に発行されたテンプレートID |
| template.templateName | String | テンプレート名 |
| template.categoryId | String | カテゴリーID |
| template.messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array |  |
| template.templateLanguage | String | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object |  |
| template.sender.senderPhoneNumber | String | 発信番号 |
| template.content | Object |  |
| template.content.messageType | String | 送信メッセージタイプ(SMS、LMS、MMS)<br>[SMS、LMS、MMS] |
| template.content.title | String | メッセージ件名 |
| template.content.body | String | メッセージ本文 |
| template.content.attachmentIds | Array | 添付ファイルID 最大3個 |
| template.createdDateTime | String | テンプレート作成日時 |
| template.updatedDateTime | String | テンプレート修正日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMSテンプレート詳細照会

GET {{endpoint}}/template/v1.0/SMS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/SMS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0004UpdateSmsTemplate"></span>

## SMSテンプレート修正

テンプレートを修正します。

**リクエスト**

```
PUT /template/v1.0/SMS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->


```
{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | Y | テンプレート名 |
| messagePurpose | String | N | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.senderPhoneNumber | String | N | 発信番号 |
| content | Object | Y |  |
| content.messageType | String | N | 送信メッセージタイプ(SMS、LMS、MMS)<br>[SMS、LMS、MMS] |
| content.title | String | N | メッセージ件名 |
| content.body | String | N | メッセージ本文 |
| content.attachmentIds | Array | N | 添付ファイルID 最大3個 |



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMSテンプレート修正

PUT {{endpoint}}/template/v1.0/SMS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/SMS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>
<span id="templateV1x0005DeleteSmsTemplate"></span>

## SMSテンプレート削除

テンプレートを削除します。

**リクエスト**

```
DELETE /template/v1.0/SMS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMSテンプレート削除

DELETE {{endpoint}}/template/v1.0/SMS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/SMS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0006CreateAlimtalkTemplate"></span>

## お知らせトークテンプレート登録

テンプレートを登録します。

**リクエスト**

```
POST /template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->


```
{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
    "senderProfileType" : "NORMAL"
  },
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "#{名前}様のご注文が完了しました。",
    "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
    "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する可能性があり、入室できない場合は予約がキャンセルされることがあります。\\n* お問い合わせ: 1234-1234",
    "templateTitle" : "123,450KRW",
    "templateSubtitle" : "承認内訳",
    "templateHeader" : "注文が確定しました。",
    "templateItem" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "description" : "アイテム説明"
      } ],
      "summary" : {
        "title" : "サマリータイトル",
        "description" : "サマリー説明"
      }
    },
    "templateItemHighlight" : {
      "title" : "ハイライトタイトル",
      "description" : "ハイライト説明",
      "attachmentId" : "YaX2DA4Weab2",
      "imageUrl" : "https://example.com/thumbnail.jpg"
    },
    "templateRepresentLink" : {
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "attachmentId" : "YaX2DA4Weab2",
    "templateImageName" : "image.png",
    "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "securityFlag" : false,
    "categoryCode" : "999999",
    "buttons" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "ボタン名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "ダイレクトリンク名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ]
  },
  "additionalProperty" : {
    "templateCode" : "templateCode",
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | Y | テンプレート名 |
| categoryId | String | N | カテゴリーID |
| messagePurpose | String | N | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.senderKey | String | N | 発信プロファイルの発信キー |
| sender.senderProfileType | String | N | 発信プロファイルタイプ<br>[GROUP, NORMAL] |
| content | Object | Y |  |
| content.templateMessageType | String | N | テンプレートメッセージタイプ(BA: 基本型、EX: 付加情報型、AD: チャンネル追加型、MI: 複合型、default: BA) |
| content.templateEmphasizeType | String | N | テンプレート強調表示タイプ(NONE : 基本、TEXT : 強調表示、IMAGE: 画像型、ITEM_LIST: アイテムリスト型、default : NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| content.templateContent | String | N | テンプレート本文 |
| content.templateAd | String | N | チャンネル追加案内メッセージ(テンプレートメッセージタイプ: チャンネル追加型、複合型の場合は固定値) |
| content.templateExtra | String | N | テンプレート付加情報(テンプレートメッセージタイプが[付加情報型/複合型]の場合は必須)、置換変数は使用不可、URLを含むことが可能 |
| content.templateTitle | String | N | テンプレートタイトル(最大50文字、Android: 2行、23文字以上で省略表示、iOS: 2行、27文字以上で省略表示) |
| content.templateSubtitle | String | N | テンプレート補助文言(最大50文字、Android: 18文字以上で省略表示、iOS: 21文字以上で省略表示) |
| content.templateHeader | String | N | テンプレートヘッダ、変数の入力が可能 |
| content.templateItem | Object | N |  |
| content.templateItem.list | Array | N |  |
| content.templateItem.list[].title | String | N | アイテムタイトル |
| content.templateItem.list[].description | String | N | アイテム説明 |
| content.templateItem.summary | Object | N |  |
| content.templateItem.summary.title | String | N | サマリータイトル |
| content.templateItem.summary.description | String | N | サマリー説明(変数及び通貨単位、数字、カンマ、ピリオドのみ使用可能) |
| content.templateItemHighlight | Object | N |  |
| content.templateItemHighlight.title | String | N | アイテムハイライトタイトル(最大30文字、サムネイル画像がある場合は21文字) |
| content.templateItemHighlight.description | String | N | アイテムハイライト説明(最大19文字、サムネイル画像がある場合は13文字) |
| content.templateItemHighlight.attachmentId | String | N | テンプレート添付ファイルID |
| content.templateItemHighlight.imageUrl | String | N | サムネイル画像アドレス |
| content.templateRepresentLink | Object | N |  |
| content.templateRepresentLink.linkMo | String | N | 代表リンク モバイルWebリンク |
| content.templateRepresentLink.linkPc | String | N | 代表リンクPC Webリンク |
| content.templateRepresentLink.schemeIos | String | N | 代表リンクiOSアプリリンク |
| content.templateRepresentLink.schemeAndroid | String | N | 代表リンクAndroidアプリリンク |
| content.attachmentId | String | N | テンプレート添付ファイルID |
| content.templateImageName | String | N | テンプレート画像名 |
| content.templateImageUrl | String | N | テンプレート画像リンク |
| content.securityFlag | Boolean | N | テンプレートセキュリティの有無(default: false) |
| content.categoryCode | String | N | テンプレートカテゴリーコード(テンプレートカテゴリー照会API参照、default: 999999) |
| content.buttons | Array | N | テンプレートボタン |
| content.buttons[].ordering | Integer | N | テンプレートボタン順序 |
| content.buttons[].type | String | N | テンプレートボタンタイプ(WL: Webリンク、AL: アプリリンク、DS: 配送照会、BK: ボットキーワード、MD: メッセージ転送、BC: 相談トーク切替、BT: ボット切替、AC: チャンネル追加、BF: ビジネスフォーム、P1: 画像セキュリティ送信プラグインID、P2: 個人情報利用プラグインID、P3: ワンクリック決済プラグインID)<br>[WL, AL, DS, BK, MD, BC, BT, AC, BF, P1, P2, P3] |
| content.buttons[].name | String | N | テンプレートボタン名 |
| content.buttons[].linkMo | String | N | テンプレートボタン モバイルWebリンク |
| content.buttons[].linkPc | String | N | テンプレートボタンPC Webリンク |
| content.buttons[].schemeIos | String | N | テンプレートボタンiOSアプリリンク |
| content.buttons[].schemeAndroid | String | N | テンプレートボタンAndroidアプリリンク |
| content.buttons[].bizFormId | Integer | N | テンプレートボタン ビジネスフォームID(BFタイプの場合は必須) |
| content.quickReplies | Array | N | テンプレートダイレクトリンク |
| content.quickReplies[].ordering | Integer | N | テンプレートダイレクトリンク順序 |
| content.quickReplies[].type | String | N | テンプレートダイレクトリンクタイプ(WL: Webリンク、AL: アプリリンク、BK: ボットキーワード、BC: 相談トーク切替、BT: ボット切替、BF: ビジネスフォーム)<br>[WL, AL, BK, BC, BT, BF] |
| content.quickReplies[].name | String | N | テンプレートダイレクトリンク名 |
| content.quickReplies[].linkMo | String | N | テンプレートダイレクトリンク モバイルWebリンク |
| content.quickReplies[].linkPc | String | N | テンプレートダイレクトリンク PC Webリンク |
| content.quickReplies[].schemeIos | String | N | テンプレートダイレクトリンク iOSアプリリンク |
| content.quickReplies[].schemeAndroid | String | N | テンプレートダイレクトリンク Androidアプリリンク |
| content.quickReplies[].bizFormId | Integer | N | テンプレートダイレクトリンク ビジネスフォームID(BFタイプの場合は必須) |
| additionalProperty | Object | N |  |
| additionalProperty.templateCode | String | N | テンプレートコード(英字、数字、-、_) |
| additionalProperty.kakaoTemplateCode | String | N | カカオテンプレートコード |



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "templateId" : "A9z0A9z0"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| templateId | String | テンプレート登録時に発行されたテンプレートID |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレート登録

POST {{endpoint}}/template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
    "senderProfileType" : "NORMAL"
  },
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "#{名前}様のご注文が完了しました。",
    "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
    "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する可能性があり、入室できない場合は予約がキャンセルされることがあります。\\n* お問い合わせ: 1234-1234",
    "templateTitle" : "123,450KRW",
    "templateSubtitle" : "承認内訳",
    "templateHeader" : "注文が確定しました。",
    "templateItem" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "description" : "アイテム説明"
      } ],
      "summary" : {
        "title" : "サマリータイトル",
        "description" : "サマリー説明"
      }
    },
    "templateItemHighlight" : {
      "title" : "ハイライトタイトル",
      "description" : "ハイライト説明",
      "attachmentId" : "YaX2DA4Weab2",
      "imageUrl" : "https://example.com/thumbnail.jpg"
    },
    "templateRepresentLink" : {
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "attachmentId" : "YaX2DA4Weab2",
    "templateImageName" : "image.png",
    "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "securityFlag" : false,
    "categoryCode" : "999999",
    "buttons" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "ボタン名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "ダイレクトリンク名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ]
  },
  "additionalProperty" : {
    "templateCode" : "templateCode",
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
    "senderProfileType" : "NORMAL"
  },
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "#{名前}様のご注文が完了しました。",
    "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
    "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する可能性があり、入室できない場合は予約がキャンセルされることがあります。\\n* お問い合わせ: 1234-1234",
    "templateTitle" : "123,450KRW",
    "templateSubtitle" : "承認内訳",
    "templateHeader" : "注文が確定しました。",
    "templateItem" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "description" : "アイテム説明"
      } ],
      "summary" : {
        "title" : "サマリータイトル",
        "description" : "サマリー説明"
      }
    },
    "templateItemHighlight" : {
      "title" : "ハイライトタイトル",
      "description" : "ハイライト説明",
      "attachmentId" : "YaX2DA4Weab2",
      "imageUrl" : "https://example.com/thumbnail.jpg"
    },
    "templateRepresentLink" : {
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "attachmentId" : "YaX2DA4Weab2",
    "templateImageName" : "image.png",
    "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "securityFlag" : false,
    "categoryCode" : "999999",
    "buttons" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "ボタン名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "ダイレクトリンク名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ]
  },
  "additionalProperty" : {
    "templateCode" : "templateCode",
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}'
```

</details>
<span id="templateV1x0007ReadAlimtalkTemplateList"></span>

## お知らせトークテンプレートリスト照会

テンプレートリストを照会します。

**リクエスト**

```
GET /template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateName | Query  | String | N | テンプレート名(LIKE検索) |
| senderKey | Query  | String | N | 発信キー |
| templateStatus | Query  | String | N | テンプレートステータス |
| limit | Query  | Integer | N | limitを設定しない場合はデフォルト20(最大1000) |
| offset | Query  | Integer | N | offsetを設定しない場合はデフォルト0 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "配送完了",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| totalCount | Integer | 総件数 |
| templates | Array |  |
| templates[].templateId | String | テンプレート登録時に発行されたテンプレートID |
| templates[].templateName | String | テンプレート名 |
| templates[].categoryId | String | カテゴリーID |
| templates[].messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | テンプレート作成日時 |
| templates[].updatedDateTime | String | テンプレート修正日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレートリスト照会

GET {{endpoint}}/template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0008ReadAlimtalkSenderTemplates"></span>

## お知らせトーク発信者に関連するテンプレートリスト照会

発信者に関連するテンプレートリストを照会します。(発信者または発信者が含まれるグループのテンプレート)

**リクエスト**

```
GET /template/v1.0/ALIMTALK/senders/{senderKey}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| senderKey | Path  | String | Y | 発信キー |
| templateName | Query  | String | N | テンプレート名(LIKE検索) |
| templateStatus | Query  | String | N | テンプレートステータス |
| limit | Query  | Integer | N | limitを設定しない場合はデフォルト20(最大1000) |
| offset | Query  | Integer | N | offsetを設定しない場合はデフォルト0 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "配送完了",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| totalCount | Integer | 総件数 |
| templates | Array |  |
| templates[].templateId | String | テンプレート登録時に発行されたテンプレートID |
| templates[].templateName | String | テンプレート名 |
| templates[].categoryId | String | カテゴリーID |
| templates[].messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | テンプレート作成日時 |
| templates[].updatedDateTime | String | テンプレート修正日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトーク発信者に関連するテンプレートリスト照会

GET {{endpoint}}/template/v1.0/ALIMTALK/senders/{{senderKey}}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/senders/${senderKey}/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0009ReadAlimtalkTemplate"></span>

## お知らせトークテンプレート詳細照会

テンプレートを詳細照会します。

**リクエスト**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "テンプレート名",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "sender" : {
      "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
      "senderProfileId" : "@nhnCloud",
      "senderProfileType" : "GROUP"
    },
    "additionalProperty" : {
      "templateCode" : "templateCode",
      "kakaoTemplateCode" : "kakaoTemplateCode",
      "comments" : [ {
        "id" : 1,
        "content" : "お問い合わせ内容の例",
        "userName" : "ユーザー名",
        "createdAt" : "2024-10-29T06:00:01.000+09:00",
        "attachments" : [ {
          "originalFileName" : "ファイル名の例",
          "filePath" : "/path/to/file"
        } ],
        "status" : "REQ"
      } ],
      "status" : "APPROVED",
      "block" : false,
      "dormant" : false
    },
    "content" : {
      "templateMessageType" : "BA",
      "templateEmphasizeType" : "NONE",
      "templateContent" : "#{名前}様のご注文が完了しました。",
      "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
      "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する可能性があり、入室できない場合は予約がキャンセルされることがあります。\\n* お問い合わせ: 1234-1234",
      "templateTitle" : "123,450KRW",
      "templateSubtitle" : "承認内訳",
      "templateHeader" : "注文が確定しました。",
      "templateItem" : {
        "list" : [ {
          "title" : "アイテムタイトル",
          "description" : "アイテム説明"
        } ],
        "summary" : {
          "title" : "サマリータイトル",
          "description" : "サマリー説明"
        }
      },
      "templateItemHighlight" : {
        "title" : "ハイライトタイトル",
        "description" : "ハイライト説明",
        "attachmentId" : "YaX2DA4Weab2",
        "imageUrl" : "https://example.com/thumbnail.jpg"
      },
      "templateRepresentLink" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "attachmentId" : "YaX2DA4Weab2",
      "templateImageName" : "image.png",
      "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
      "securityFlag" : false,
      "categoryCode" : "999999",
      "buttons" : [ {
        "ordering" : 1,
        "type" : "WL",
        "name" : "ボタン名",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ],
      "quickReplies" : [ {
        "ordering" : 1,
        "type" : "WL",
        "name" : "ダイレクトリンク名",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ]
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| template | Object |  |
| template.templateId | String | テンプレート登録時に発行されたテンプレートID |
| template.templateName | String | テンプレート名 |
| template.categoryId | String | カテゴリーID |
| template.messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array |  |
| template.templateLanguage | String | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object |  |
| template.sender.senderKey | String | 発信プロファイルの発信キー |
| template.sender.senderProfileId | String | カカオトークチャンネル名 |
| template.sender.senderProfileType | String | 発信プロファイルタイプ<br>[GROUP, NORMAL] |
| template.additionalProperty | Object |  |
| template.additionalProperty.templateCode | String | テンプレートコード(英字、数字、-、_) |
| template.additionalProperty.kakaoTemplateCode | String | カカオテンプレートコード |
| template.additionalProperty.comments | Array | テンプレート問い合わせリスト |
| template.additionalProperty.comments[].id | Integer | 問い合わせID |
| template.additionalProperty.comments[].content | String | 問い合わせ内容 |
| template.additionalProperty.comments[].userName | String | 作成者 |
| template.additionalProperty.comments[].createdAt | String | 問い合わせ作成日時 |
| template.additionalProperty.comments[].attachments | Array | 問い合わせ添付ファイル |
| template.additionalProperty.comments[].status | String | 問い合わせステータス(REQ: リクエスト、INQ: 問い合わせ、APR: 承認、REJ: 却下、REP: 回答)<br>[REQ, INQ, APR, REJ, REP] |
| template.additionalProperty.status | String | REG: 申請、REQ: 審査中、APR: 承認、REJ: 却下<br>[REG, REQ, APR, REJ] |
| template.additionalProperty.templateModificationStatus | String | REG: 申請、REQ: 審査中、APR: 承認、REJ: 却下<br>[REG, REQ, APR, REJ] |
| template.additionalProperty.block | Boolean | テンプレートブロックの有無 |
| template.additionalProperty.dormant | Boolean | テンプレート休眠の有無 |
| template.content | Object |  |
| template.content.templateMessageType | String | テンプレートメッセージタイプ(BA: 基本型、EX: 付加情報型、AD: チャンネル追加型、MI: 複合型、default: BA) |
| template.content.templateEmphasizeType | String | テンプレート強調表示タイプ(NONE : 基本、TEXT : 強調表示、IMAGE: 画像型、ITEM_LIST: アイテムリスト型、default : NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| template.content.templateContent | String | テンプレート本文 |
| template.content.templateAd | String | チャンネル追加案内メッセージ(テンプレートメッセージタイプ: チャンネル追加型、複合型の場合は固定値) |
| template.content.templateExtra | String | テンプレート付加情報(テンプレートメッセージタイプが[付加情報型/複合型]の場合は必須)、置換変数は使用不可、URLを含むことが可能 |
| template.content.templateTitle | String | テンプレートタイトル(最大50文字、Android: 2行、23文字以上で省略表示、iOS: 2行、27文字以上で省略表示) |
| template.content.templateSubtitle | String | テンプレート補助文言(最大50文字、Android: 18文字以上で省略表示、iOS: 21文字以上で省略表示) |
| template.content.templateHeader | String | テンプレートヘッダ、変数の入力が可能 |
| template.content.templateItem | Object |  |
| template.content.templateItem.list | Array |  |
| template.content.templateItem.list[].title | String | アイテムタイトル |
| template.content.templateItem.list[].description | String | アイテム説明 |
| template.content.templateItem.summary | Object |  |
| template.content.templateItem.summary.title | String | サマリータイトル |
| template.content.templateItem.summary.description | String | サマリー説明(変数及び通貨単位、数字、カンマ、ピリオドのみ使用可能) |
| template.content.templateItemHighlight | Object |  |
| template.content.templateItemHighlight.title | String | アイテムハイライトタイトル(最大30文字、サムネイル画像がある場合は21文字) |
| template.content.templateItemHighlight.description | String | アイテムハイライト説明(最大19文字、サムネイル画像がある場合は13文字) |
| template.content.templateItemHighlight.attachmentId | String | テンプレート添付ファイルID |
| template.content.templateItemHighlight.imageUrl | String | サムネイル画像アドレス |
| template.content.templateRepresentLink | Object |  |
| template.content.templateRepresentLink.linkMo | String | 代表リンク モバイルWebリンク |
| template.content.templateRepresentLink.linkPc | String | 代表リンク PC Webリンク |
| template.content.templateRepresentLink.schemeIos | String | 代表リンク iOSアプリリンク |
| template.content.templateRepresentLink.schemeAndroid | String | 代表リンク Androidアプリリンク |
| template.content.attachmentId | String | テンプレート添付ファイルID |
| template.content.templateImageName | String | テンプレート画像名 |
| template.content.templateImageUrl | String | テンプレート画像リンク |
| template.content.securityFlag | Boolean | テンプレートセキュリティの有無(default: false) |
| template.content.categoryCode | String | テンプレートカテゴリーコード(テンプレートカテゴリー照会API参照、default: 999999) |
| template.content.buttons | Array | テンプレートボタン |
| template.content.buttons[].ordering | Integer | テンプレートボタン順序 |
| template.content.buttons[].type | String | テンプレートボタンタイプ(WL: Webリンク、AL: アプリリンク、DS: 配送照会、BK: ボットキーワード、MD: メッセージ転送、BC: 相談トーク切替、BT: ボット切替、AC: チャンネル追加、BF: ビジネスフォーム、P1: 画像セキュリティ送信プラグインID、P2: 個人情報利用プラグインID、P3: ワンクリック決済プラグインID)<br>[WL, AL, DS, BK, MD, BC, BT, AC, BF, P1, P2, P3] |
| template.content.buttons[].name | String | テンプレートボタン名 |
| template.content.buttons[].linkMo | String | テンプレートボタン モバイルWebリンク |
| template.content.buttons[].linkPc | String | テンプレートボタン PC Webリンク |
| template.content.buttons[].schemeIos | String | テンプレートボタン iOSアプリリンク |
| template.content.buttons[].schemeAndroid | String | テンプレートボタン Androidアプリリンク |
| template.content.buttons[].bizFormId | Integer | テンプレートボタン ビジネスフォームID(BFタイプの場合は必須) |
| template.content.quickReplies | Array | テンプレートダイレクトリンク |
| template.content.quickReplies[].ordering | Integer | テンプレートダイレクトリンク順序 |
| template.content.quickReplies[].type | String | テンプレートダイレクトリンクタイプ(WL: Webリンク、AL: アプリリンク、BK: ボットキーワード、BC: 相談トーク切替、BT: ボット切替、BF: ビジネスフォーム)<br>[WL, AL, BK, BC, BT, BF] |
| template.content.quickReplies[].name | String | テンプレートダイレクトリンク名 |
| template.content.quickReplies[].linkMo | String | テンプレートダイレクトリンク モバイルWebリンク |
| template.content.quickReplies[].linkPc | String | テンプレートダイレクトリンク PC Webリンク |
| template.content.quickReplies[].schemeIos | String | テンプレートダイレクトリンク iOSアプリリンク |
| template.content.quickReplies[].schemeAndroid | String | テンプレートダイレクトリンク Androidアプリリンク |
| template.content.quickReplies[].bizFormId | Integer | テンプレートダイレクトリンク ビジネスフォームID(BFタイプの場合は必須) |
| template.createdDateTime | String | テンプレート作成日時 |
| template.updatedDateTime | String | テンプレート修正日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレート詳細照会

GET {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0010UpdateAlimtalkTemplate"></span>

## お知らせトークテンプレート修正

テンプレートを修正します。

**リクエスト**

```
PUT /template/v1.0/ALIMTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->


```
{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "#{名前}様のご注文が完了しました。",
    "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
    "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する可能性があり、入室できない場合は予約がキャンセルされることがあります。\\n* お問い合わせ: 1234-1234",
    "templateTitle" : "123,450KRW",
    "templateSubtitle" : "承認内訳",
    "templateHeader" : "注文が確定しました。",
    "templateItem" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "description" : "アイテム説明"
      } ],
      "summary" : {
        "title" : "サマリータイトル",
        "description" : "サマリー説明"
      }
    },
    "templateItemHighlight" : {
      "title" : "ハイライトタイトル",
      "description" : "ハイライト説明",
      "attachmentId" : "YaX2DA4Weab2",
      "imageUrl" : "https://example.com/thumbnail.jpg"
    },
    "templateRepresentLink" : {
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "attachmentId" : "YaX2DA4Weab2",
    "templateImageName" : "image.png",
    "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "securityFlag" : false,
    "categoryCode" : "999999",
    "buttons" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "ボタン名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "ダイレクトリンク名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ]
  },
  "additionalProperty" : {
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | Y | テンプレート名 |
| messagePurpose | String | N | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| content | Object | Y |  |
| content.templateMessageType | String | N | テンプレートメッセージタイプ(BA: 基本型、EX: 付加情報型、AD: チャンネル追加型、MI: 複合型、default: BA) |
| content.templateEmphasizeType | String | N | テンプレート強調表示タイプ(NONE : 基本、TEXT : 強調表示、IMAGE: 画像型、ITEM_LIST: アイテムリスト型、default : NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| content.templateContent | String | N | テンプレート本文 |
| content.templateAd | String | N | チャンネル追加案内メッセージ(テンプレートメッセージタイプ: チャンネル追加型、複合型の場合は固定値) |
| content.templateExtra | String | N | テンプレート付加情報(テンプレートメッセージタイプが[付加情報型/複合型]の場合は必須)、置換変数は使用不可、URLを含むことが可能 |
| content.templateTitle | String | N | テンプレートタイトル(最大50文字、Android: 2行、23文字以上で省略表示、iOS: 2行、27文字以上で省略表示) |
| content.templateSubtitle | String | N | テンプレート補助文言(最大50文字、Android: 18文字以上で省略表示、iOS: 21文字以上で省略表示) |
| content.templateHeader | String | N | テンプレートヘッダ、変数の入力が可能 |
| content.templateItem | Object | N |  |
| content.templateItem.list | Array | N |  |
| content.templateItem.list[].title | String | N | アイテムタイトル |
| content.templateItem.list[].description | String | N | アイテム説明 |
| content.templateItem.summary | Object | N |  |
| content.templateItem.summary.title | String | N | サマリータイトル |
| content.templateItem.summary.description | String | N | サマリー説明(変数及び通貨単位、数字、カンマ、ピリオドのみ使用可能) |
| content.templateItemHighlight | Object | N |  |
| content.templateItemHighlight.title | String | N | アイテムハイライトタイトル(最大30文字、サムネイル画像がある場合は21文字) |
| content.templateItemHighlight.description | String | N | アイテムハイライト説明(最大19文字、サムネイル画像がある場合は13文字) |
| content.templateItemHighlight.attachmentId | String | N | テンプレート添付ファイルID |
| content.templateItemHighlight.imageUrl | String | N | サムネイル画像アドレス |
| content.templateRepresentLink | Object | N |  |
| content.templateRepresentLink.linkMo | String | N | 代表リンク モバイルWebリンク |
| content.templateRepresentLink.linkPc | String | N | 代表リンクPC Webリンク |
| content.templateRepresentLink.schemeIos | String | N | 代表リンクiOSアプリリンク |
| content.templateRepresentLink.schemeAndroid | String | N | 代表リンクAndroidアプリリンク |
| content.attachmentId | String | N | テンプレート添付ファイルID |
| content.templateImageName | String | N | テンプレート画像名 |
| content.templateImageUrl | String | N | テンプレート画像リンク |
| content.securityFlag | Boolean | N | テンプレートセキュリティの有無(default: false) |
| content.categoryCode | String | N | テンプレートカテゴリーコード(テンプレートカテゴリー照会API参照、default: 999999) |
| content.buttons | Array | N | テンプレートボタン |
| content.buttons[].ordering | Integer | N | テンプレートボタン順序 |
| content.buttons[].type | String | N | テンプレートボタンタイプ(WL: Webリンク、AL: アプリリンク、DS: 配送照会、BK: ボットキーワード、MD: メッセージ転送、BC: 相談トーク切替、BT: ボット切替、AC: チャンネル追加、BF: ビジネスフォーム、P1: 画像セキュリティ送信プラグインID、P2: 個人情報利用プラグインID、P3: ワンクリック決済プラグインID)<br>[WL, AL, DS, BK, MD, BC, BT, AC, BF, P1, P2, P3] |
| content.buttons[].name | String | N | テンプレートボタン名 |
| content.buttons[].linkMo | String | N | テンプレートボタン モバイルWebリンク |
| content.buttons[].linkPc | String | N | テンプレートボタンPC Webリンク |
| content.buttons[].schemeIos | String | N | テンプレートボタンiOSアプリリンク |
| content.buttons[].schemeAndroid | String | N | テンプレートボタンAndroidアプリリンク |
| content.buttons[].bizFormId | Integer | N | テンプレートボタン ビジネスフォームID(BFタイプの場合は必須) |
| content.quickReplies | Array | N | テンプレートダイレクトリンク |
| content.quickReplies[].ordering | Integer | N | テンプレートダイレクトリンク順序 |
| content.quickReplies[].type | String | N | テンプレートダイレクトリンクタイプ(WL: Webリンク、AL: アプリリンク、BK: ボットキーワード、BC: 相談トーク切替、BT: ボット切替、BF: ビジネスフォーム)<br>[WL, AL, BK, BC, BT, BF] |
| content.quickReplies[].name | String | N | テンプレートダイレクトリンク名 |
| content.quickReplies[].linkMo | String | N | テンプレートダイレクトリンク モバイルWebリンク |
| content.quickReplies[].linkPc | String | N | テンプレートダイレクトリンク PC Webリンク |
| content.quickReplies[].schemeIos | String | N | テンプレートダイレクトリンク iOSアプリリンク |
| content.quickReplies[].schemeAndroid | String | N | テンプレートダイレクトリンク Androidアプリリンク |
| content.quickReplies[].bizFormId | Integer | N | テンプレートダイレクトリンク ビジネスフォームID(BFタイプの場合は必須) |
| additionalProperty | Object | Y |  |
| additionalProperty.kakaoTemplateCode | String | Y | カカオテンプレートコード(英字、数字、-、_) |



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレート修正

PUT {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "#{名前}様のご注文が完了しました。",
    "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
    "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する可能性があり、入室できない場合は予約がキャンセルされることがあります。\\n* お問い合わせ: 1234-1234",
    "templateTitle" : "123,450KRW",
    "templateSubtitle" : "承認内訳",
    "templateHeader" : "注文が確定しました。",
    "templateItem" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "description" : "アイテム説明"
      } ],
      "summary" : {
        "title" : "サマリータイトル",
        "description" : "サマリー説明"
      }
    },
    "templateItemHighlight" : {
      "title" : "ハイライトタイトル",
      "description" : "ハイライト説明",
      "attachmentId" : "YaX2DA4Weab2",
      "imageUrl" : "https://example.com/thumbnail.jpg"
    },
    "templateRepresentLink" : {
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "attachmentId" : "YaX2DA4Weab2",
    "templateImageName" : "image.png",
    "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "securityFlag" : false,
    "categoryCode" : "999999",
    "buttons" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "ボタン名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "ダイレクトリンク名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ]
  },
  "additionalProperty" : {
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "#{名前}様のご注文が完了しました。",
    "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
    "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する可能性があり、入室できない場合は予約がキャンセルされることがあります。\\n* お問い合わせ: 1234-1234",
    "templateTitle" : "123,450KRW",
    "templateSubtitle" : "承認内訳",
    "templateHeader" : "注文が確定しました。",
    "templateItem" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "description" : "アイテム説明"
      } ],
      "summary" : {
        "title" : "サマリータイトル",
        "description" : "サマリー説明"
      }
    },
    "templateItemHighlight" : {
      "title" : "ハイライトタイトル",
      "description" : "ハイライト説明",
      "attachmentId" : "YaX2DA4Weab2",
      "imageUrl" : "https://example.com/thumbnail.jpg"
    },
    "templateRepresentLink" : {
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "attachmentId" : "YaX2DA4Weab2",
    "templateImageName" : "image.png",
    "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
    "securityFlag" : false,
    "categoryCode" : "999999",
    "buttons" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "ボタン名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "quickReplies" : [ {
      "ordering" : 1,
      "type" : "WL",
      "name" : "ダイレクトリンク名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ]
  },
  "additionalProperty" : {
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}'
```

</details>
<span id="templateV1x0011DeleteAlimtalkTemplate"></span>

## お知らせトークテンプレート削除

テンプレートを削除します。

**リクエスト**

```
DELETE /template/v1.0/ALIMTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレート削除

DELETE {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0012InquireAlimtalkTemplate"></span>

## お知らせトークテンプレート問い合わせ (deprecated)

!!! danger "本APIはサポートを終了しました。"
    * [カカオお知らせトークテンプレート問い合わせ](#templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesKakaoTemplateCodeInquiriesPost)を参照してください。

お知らせトークテンプレートについて問い合わせます。

**リクエスト**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/inquiries
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->


```
{
  "comment" : "お問い合わせ内容の例"
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| comment | String | Y | お問い合わせ内容 |



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレート問い合わせ

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/inquiries
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "comment" : "お問い合わせ内容の例"
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/inquiries" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "comment" : "お問い合わせ内容の例"
}'
```

</details>
<span id="templateV1x0013InquireAlimtalkTemplateWithFile"></span>

## お知らせトークテンプレート問い合わせ(ファイル添付) (deprecated)

!!! danger "本APIはサポートを終了しました。"
    * [カカオお知らせトークテンプレート問い合わせ](#templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesKakaoTemplateCodeInquiriesDoWithFilePost)を参照してください。

お知らせトークテンプレートを問い合わせる際、ファイルを添付して問い合わせます。

**リクエスト**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/inquiries/do-with-file
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレート問い合わせ(ファイル添付)

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/inquiries/do-with-file
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/inquiries/do-with-file" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0014ReadAlimtalkTemplateModifications"></span>

## お知らせトークテンプレート修正リスト照会 (deprecated)

!!! danger "本APIはサポートを終了しました。"
    * [お知らせトークテンプレートのカカオテンプレート一覧照会](#templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesGet)を参照してください。

お知らせトークテンプレート修正リストを照会します。

**リクエスト**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}/modifications
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |
| limit | Query  | Integer | N | limitを設定しない場合はデフォルト50(最大1000) |
| offset | Query  | Integer | N | offsetを設定しない場合はデフォルト0 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "テンプレート名",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "sender" : {
      "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
      "senderProfileId" : "@nhnCloud",
      "senderProfileType" : "GROUP"
    },
    "additionalProperty" : {
      "templateCode" : "templateCode",
      "kakaoTemplateCode" : "kakaoTemplateCode",
      "comments" : [ {
        "id" : 1,
        "content" : "お問い合わせ内容の例",
        "userName" : "ユーザー名",
        "createdAt" : "2024-10-29T06:00:01.000+09:00",
        "attachments" : [ {
          "originalFileName" : "ファイル名の例",
          "filePath" : "/path/to/file"
        } ],
        "status" : "REQ"
      } ],
      "status" : "APR",
      "block" : false,
      "dormant" : false,
      "activated" : false
    },
    "content" : {
      "templateMessageType" : "BA",
      "templateEmphasizeType" : "NONE",
      "templateContent" : "#{名前}様のご注文が完了しました。",
      "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
      "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する可能性があり、入室できない場合は予約がキャンセルされることがあります。\\n* お問い合わせ: 1234-1234",
      "templateTitle" : "123,450KRW",
      "templateSubtitle" : "承認内訳",
      "templateHeader" : "注文が確定しました。",
      "templateItem" : {
        "list" : [ {
          "title" : "アイテムタイトル",
          "description" : "アイテム説明"
        } ],
        "summary" : {
          "title" : "サマリータイトル",
          "description" : "サマリー説明"
        }
      },
      "templateItemHighlight" : {
        "title" : "ハイライトタイトル",
        "description" : "ハイライト説明",
        "attachmentId" : "YaX2DA4Weab2",
        "imageUrl" : "https://example.com/thumbnail.jpg"
      },
      "templateRepresentLink" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "attachmentId" : "YaX2DA4Weab2",
      "templateImageName" : "image.png",
      "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
      "securityFlag" : false,
      "categoryCode" : "999999",
      "buttons" : [ {
        "ordering" : 1,
        "type" : "WL",
        "name" : "ボタン名",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ],
      "quickReplies" : [ {
        "ordering" : 1,
        "type" : "WL",
        "name" : "ダイレクトリンク名",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ]
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| totalCount | Integer | 総件数 |
| templates | Array |  |
| templates[].templateId | String | テンプレート登録時に発行されたテンプレートID |
| templates[].templateName | String | テンプレート名 |
| templates[].categoryId | String | カテゴリーID |
| templates[].messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].templateLanguage | String | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| templates[].sender | Object |  |
| templates[].sender.senderKey | String | 発信プロファイルの発信キー |
| templates[].sender.senderProfileId | String | カカオトークチャンネル名 |
| templates[].sender.senderProfileType | String | 発信プロファイルタイプ<br>[GROUP, NORMAL] |
| templates[].additionalProperty | Object |  |
| templates[].additionalProperty.templateCode | String | テンプレートコード(英字、数字、-、_) |
| templates[].additionalProperty.kakaoTemplateCode | String | カカオテンプレートコード |
| templates[].additionalProperty.comments | Array | テンプレート問い合わせリスト |
| templates[].additionalProperty.status | String | REG: 申請、REQ: 審査中、APR: 承認、REJ: 却下<br>[REG, REQ, APR, REJ] |
| templates[].additionalProperty.block | Boolean | テンプレートブロックの有無 |
| templates[].additionalProperty.dormant | Boolean | テンプレート休眠の有無 |
| templates[].additionalProperty.activated | Boolean | 有効かどうか |
| templates[].content | Object |  |
| templates[].content.templateMessageType | String | テンプレートメッセージタイプ(BA: 基本型、EX: 付加情報型、AD: チャンネル追加型、MI: 複合型、default: BA) |
| templates[].content.templateEmphasizeType | String | テンプレート強調表示タイプ(NONE : 基本、TEXT : 強調表示、IMAGE: 画像型、ITEM_LIST: アイテムリスト型、default : NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| templates[].content.templateContent | String | テンプレート本文 |
| templates[].content.templateAd | String | チャンネル追加案内メッセージ(テンプレートメッセージタイプ: チャンネル追加型、複合型の場合は固定値) |
| templates[].content.templateExtra | String | テンプレート付加情報(テンプレートメッセージタイプが[付加情報型/複合型]の場合は必須)、置換変数は使用不可、URLを含むことが可能 |
| templates[].content.templateTitle | String | テンプレートタイトル(最大50文字、Android: 2行、23文字以上で省略表示、iOS: 2行、27文字以上で省略表示) |
| templates[].content.templateSubtitle | String | テンプレート補助文言(最大50文字、Android: 18文字以上で省略表示、iOS: 21文字以上で省略表示) |
| templates[].content.templateHeader | String | テンプレートヘッダ、変数の入力が可能 |
| templates[].content.templateItem | Object |  |
| templates[].content.templateItem.list | Array |  |
| templates[].content.templateItem.summary | Object |  |
| templates[].content.templateItem.summary.title | String | サマリータイトル |
| templates[].content.templateItem.summary.description | String | サマリー説明(変数及び通貨単位、数字、カンマ、ピリオドのみ使用可能) |
| templates[].content.templateItemHighlight | Object |  |
| templates[].content.templateItemHighlight.title | String | アイテムハイライトタイトル(最大30文字、サムネイル画像がある場合は21文字) |
| templates[].content.templateItemHighlight.description | String | アイテムハイライト説明(最大19文字、サムネイル画像がある場合は13文字) |
| templates[].content.templateItemHighlight.attachmentId | String | テンプレート添付ファイルID |
| templates[].content.templateItemHighlight.imageUrl | String | サムネイル画像アドレス |
| templates[].content.templateRepresentLink | Object |  |
| templates[].content.templateRepresentLink.linkMo | String | 代表リンク モバイルWebリンク |
| templates[].content.templateRepresentLink.linkPc | String | 代表リンク PC Webリンク |
| templates[].content.templateRepresentLink.schemeIos | String | 代表リンク iOSアプリリンク |
| templates[].content.templateRepresentLink.schemeAndroid | String | 代表リンク Androidアプリリンク |
| templates[].content.attachmentId | String | テンプレート添付ファイルID |
| templates[].content.templateImageName | String | テンプレート画像名 |
| templates[].content.templateImageUrl | String | テンプレート画像リンク |
| templates[].content.securityFlag | Boolean | テンプレートセキュリティの有無(default: false) |
| templates[].content.categoryCode | String | テンプレートカテゴリーコード(テンプレートカテゴリー照会API参照、default: 999999) |
| templates[].content.buttons | Array | テンプレートボタン |
| templates[].content.quickReplies | Array | テンプレートダイレクトリンク |
| templates[].createdDateTime | String | テンプレート作成日時 |
| templates[].updatedDateTime | String | テンプレート修正日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレート修正リスト照会

GET {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/modifications
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/modifications" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>

<span id="templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesGet"></span>

## お知らせトークのカカオテンプレート一覧照会

お知らせトークのカカオテンプレート一覧を照会します。

### リクエスト

```
GET /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates
```

### リクエストパラメータ

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | アプリキー |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| templateId | Path | String | Y | テンプレートID |
| limit | Query | Integer | N | limitを設定しない場合はデフォルト20(最大1000) |
| offset | Query | Integer | N | offsetを設定しない場合はデフォルト0 |



### リクエストボディ

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



### レスポンスボディ

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "templates" : [ {
    "kakaoTemplateCode" : "kakaoTemplateCode",
    "kakaoTemplateName" : "テンプレート名",
    "content" : {
      "templateMessageType" : "BA",
      "templateEmphasizeType" : "NONE",
      "templateContent" : "#{名前}様のご注文が完了しました。",
      "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
      "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する可能性があり、入室できない場合は予約がキャンセルされることがあります。\\n* お問い合わせ: 1234-1234",
      "templateTitle" : "123,450KRW",
      "templateSubtitle" : "承認内訳",
      "templateHeader" : "注文が確定しました。",
      "templateItem" : {
        "list" : [ {
          "title" : "アイテムタイトル",
          "description" : "アイテム説明"
        } ],
        "summary" : {
          "title" : "サマリータイトル",
          "description" : "サマリー説明"
        }
      },
      "templateItemHighlight" : {
        "title" : "ハイライトタイトル",
        "description" : "ハイライト説明",
        "attachmentId" : "YaX2DA4Weab2",
        "imageUrl" : "https://example.com/thumbnail.jpg"
      },
      "templateRepresentLink" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "attachmentId" : "YaX2DA4Weab2",
      "templateImageName" : "image.png",
      "templateImageUrl" : "https://mud-kage.kakao.com/dn/hAtIc/btshc5wAvF0/sA8gjabh4J34IMqCk0hkBK/img_l.jpg",
      "securityFlag" : false,
      "categoryCode" : "999999",
      "buttons" : [ {
        "ordering" : 1,
        "type" : "WL",
        "name" : "ボタン名",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ],
      "quickReplies" : [ {
        "ordering" : 1,
        "type" : "WL",
        "name" : "ダイレクトリンク名",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ]
    },
    "reviewStatus" : "APPROVED",
    "comments" : [ {
      "id" : 1,
      "content" : "お問い合わせ内容の例",
      "userName" : "ユーザー名",
      "createdAt" : "2024-10-29T06:00:01.000+09:00",
      "attachments" : [ {
        "originalFileName" : "ファイル名の例",
        "filePath" : "/path/to/file"
      } ],
      "status" : "REQ"
    } ],
    "block" : false,
    "dormant" : false,
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明                                                                                                                       |
| - | - |--------------------------------------------------------------------------------------------------------------------------|
| header | Object |                                                                                                                          |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true                                                                                        |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0                                                                                                  |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS                                                                                           |
| totalCount | Integer | 総件数                                                                                                                    |
| templates | Array |                                                                                                                          |
| templates[].kakaoTemplateCode | String | カカオテンプレートコード                                                                                                              |
| templates[].kakaoTemplateName | String | テンプレート名                                                                                                                  |
| templates[].content | Object |                                                                                                                          |
| templates[].content.templateMessageType | String | テンプレートメッセージタイプ(BA: 基本型、EX: 付加情報型、AD: チャンネル追加型、MI: 複合型、default: BA)                                                        |
| templates[].content.templateEmphasizeType | String | テンプレート強調表示タイプ(NONE : 基本、TEXT : 強調表示、IMAGE: 画像型、ITEM_LIST: アイテムリスト型、default: NONE)<br>[NONE, TEXT, IMAGE, ITEM_LIST] |
| templates[].content.templateContent | String | テンプレート本文                                                                                                                  |
| templates[].content.templateAd | String | チャンネル追加案内メッセージ(テンプレートメッセージタイプ: チャンネル追加型、複合型の場合は固定値)                                                                            |
| templates[].content.templateExtra | String | テンプレート付加情報(テンプレートメッセージタイプが[付加情報型/複合型]の場合は必須)、置換変数は使用不可、URLを含むことが可能                                                       |
| templates[].content.templateTitle | String | テンプレートタイトル(最大50文字、Android: 2行、23文字以上で省略表示、iOS: 2行、27文字以上で省略表示)                                                      |
| templates[].content.templateSubtitle | String | テンプレート補助文言(最大50文字、Android: 18文字以上で省略表示、iOS: 21文字以上で省略表示)                                                           |
| templates[].content.templateHeader | String | テンプレートヘッダ、変数の入力が可能                                                                                                         |
| templates[].content.templateItem | Object |                                                                                                                          |
| templates[].content.templateItem.list | Array |                                                                                                                          |
| templates[].content.templateItem.summary | Object |                                                                                                                          |
| templates[].content.templateItem.summary.title | String | サマリータイトル                                                                                                                   |
| templates[].content.templateItem.summary.description | String | サマリー説明(変数及び通貨単位、数字、カンマ、ピリオドのみ使用可能)                                                                                    |
| templates[].content.templateItemHighlight | Object |                                                                                                                          |
| templates[].content.templateItemHighlight.title | String | アイテムハイライトタイトル(最大30文字、サムネイル画像がある場合は21文字)                                                                               |
| templates[].content.templateItemHighlight.description | String | アイテムハイライト説明(最大19文字、サムネイル画像がある場合は13文字)                                                                                |
| templates[].content.templateItemHighlight.attachmentId | String | テンプレート添付ファイルID                                                                                                             |
| templates[].content.templateItemHighlight.imageUrl | String | サムネイル画像アドレス                                                                                                              |
| templates[].content.templateRepresentLink | Object |                                                                                                                          |
| templates[].content.templateRepresentLink.linkMo | String | 代表リンク モバイルWebリンク                                                                                                           |
| templates[].content.templateRepresentLink.linkPc | String | 代表リンクPC Webリンク                                                                                                           |
| templates[].content.templateRepresentLink.schemeIos | String | 代表リンク iOSアプリリンク                                                                                                           |
| templates[].content.templateRepresentLink.schemeAndroid | String | 代表リンク Androidアプリリンク                                                                                                         |
| templates[].content.attachmentId | String | テンプレート添付ファイルID                                                                                                             |
| templates[].content.templateImageName | String | テンプレート画像名                                                                                                              |
| templates[].content.templateImageUrl | String | テンプレート画像リンク                                                                                                              |
| templates[].content.securityFlag | Boolean | テンプレートセキュリティの有無(default: false)                                                                                                |
| templates[].content.categoryCode | String | テンプレートカテゴリーコード(テンプレートカテゴリー照会API参照、default: 999999)                                                                         |
| templates[].content.buttons | Array | テンプレートボタン                                                                                                                  |
| templates[].content.quickReplies | Array | テンプレートダイレクトリンク                                                                                                                |
| templates[].reviewStatus | String | REGISTERED: 申請、REQUESTED: 審査中、APPROVED: 承認、REJECTED: 却下<br>[REGISTERED, REQUESTED, APPROVED, REJECTED]               |
| templates[].comments | Array | テンプレート問い合わせリスト                                                                                                               |
| templates[].block | Boolean | テンプレートブロックの有無                                                                                                                |
| templates[].dormant | Boolean | テンプレート休眠の有無                                                                                                                |
| templates[].createdDateTime | String | テンプレート作成日時                                                                                                                |
| templates[].updatedDateTime | String | テンプレート修正日時                                                                                                               |



### リクエスト例


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークのカカオテンプレート一覧照会

GET {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/kakao-templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/kakao-templates" \
-H "X-NC-APP-KEY: {appKey}"  \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
<span id="templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesKakaoTemplateCodeInquiriesDoWithFilePost"></span>

## ファイルを添付してカカオお知らせトークテンプレートを問い合わせる

カカオお知らせトークテンプレートを問い合わせる際、ファイルを添付して問い合わせます。

### リクエスト

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates/{kakaoTemplateCode}/inquiries/do-with-file
```

### リクエストパラメータ

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | アプリキー |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| templateId | Path | String | Y | テンプレートID |
| kakaoTemplateCode | Path | String | Y | カカオテンプレートコード |

### リクエストボディ

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| comment | String | Y | お問い合わせ内容 |
| file | Binary | Y | 問い合わせファイル |

### レスポンスボディ

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



### リクエスト例


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### ファイルを添付してカカオお知らせトークテンプレートを問い合わせる

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/kakao-templates/{{kakaoTemplateCode}}/inquiries/do-with-file
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
Content-Type: multipart/form-data; boundary=boundary

--boundary
Content-Disposition: form-data; name="comment"

comment_example
--boundary
Content-Disposition: form-data; name="file"; filename="file.txt"
Content-Type: text/plain

< /path/to/file.txt
--boundary--
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/kakao-templates/${kakaoTemplateCode}/inquiries/do-with-file" \
-H "X-NC-APP-KEY: {appKey}"  \
-H "X-NHN-Authorization: Bearer {accessToken}"  \
-F "comment=comment_example" \
-F "file=@/path/to/file.txt"
```

</details>
<span id="templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesKakaoTemplateCodeInquiriesPost"></span>

## カカオお知らせトークテンプレート問い合わせ

カカオお知らせトークテンプレートについて問い合わせます。

### リクエスト

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates/{kakaoTemplateCode}/inquiries
```

### リクエストパラメータ

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | アプリキー |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| templateId | Path | String | Y | テンプレートID |
| kakaoTemplateCode | Path | String | Y | カカオテンプレートコード |



### リクエストボディ

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->


```
{
  "comment" : "お問い合わせ内容の例"
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| comment | String | Y | お問い合わせ内容 |



### レスポンスボディ

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



### リクエスト例


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### カカオお知らせトークテンプレート問い合わせ

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/kakao-templates/{{kakaoTemplateCode}}/inquiries
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "comment" : "お問い合わせ内容の例"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/kakao-templates/${kakaoTemplateCode}/inquiries" \
-H "X-NC-APP-KEY: {appKey}"  \
-H "X-NHN-Authorization: Bearer {accessToken}"  \
-d '{
  "comment" : "お問い合わせ内容の例"
}'
```

</details>

<span id="templateV1x0015ReadAlimtalkTemplateCategories"></span>

## お知らせトークテンプレートカテゴリーリスト照会

お知らせトークテンプレートカテゴリーリストを照会します。

**リクエスト**

```
GET /template/v1.0/ALIMTALK/template-categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "categories" : [ {
    "name" : "購入",
    "subCategories" : [ {
      "code" : "002001",
      "name" : "購入完了",
      "groupName" : "購入",
      "inclusion" : "注文完了、購入完了テンプレートが対象です。",
      "exclusion" : "日程に関連して予約、予約番号があるテンプレートの場合、購入完了から除外し、予約に分類します。"
    } ]
  } ]
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| categories | Array |  |
| categories[].name | String | 大分類カテゴリー名 |
| categories[].subCategories | Array | サブカテゴリー |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレートカテゴリーリスト照会

GET {{endpoint}}/template/v1.0/ALIMTALK/template-categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/template-categories" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>

<span id="templateV1x0021CreateEmailTemplate"></span>

## Emailテンプレート登録

テンプレートを登録します。

**リクエスト**

```
POST /template/v1.0/EMAIL/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->


```
{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] モニタリング通知",
    "body" : "こんにちは。本日お客様の商品が入荷されました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | Y | テンプレート名 |
| categoryId | String | N | カテゴリーID |
| messagePurpose | String | N | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.senderMailAddress | String | Y | 発信メールアドレス |
| content | Object | Y |  |
| content.title | String | N | テンプレートメール件名 |
| content.body | String | N | テンプレートメール本文 |
| content.attachmentIds | Array | N | テンプレート添付ファイルID |



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "templateId" : "A9z0A9z0"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| templateId | String | テンプレート登録時に発行されたテンプレートID |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Emailテンプレート登録

POST {{endpoint}}/template/v1.0/EMAIL/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] モニタリング通知",
    "body" : "こんにちは。本日お客様の商品が入荷されました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/EMAIL/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] モニタリング通知",
    "body" : "こんにちは。本日お客様の商品が入荷されました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>
<span id="templateV1x0022ReadEmailTemplate"></span>

## Emailテンプレート詳細照会

テンプレートを詳細照会します。

**リクエスト**

```
GET /template/v1.0/EMAIL/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "テンプレート名",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "sender" : {
      "senderMailAddress" : "abcde@nhn.com"
    },
    "content" : {
      "title" : "[NHN Cloud Email][##env##] モニタリング通知",
      "body" : "こんにちは。本日お客様の商品が入荷されました。",
      "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| template | Object |  |
| template.templateId | String | テンプレート登録時に発行されたテンプレートID |
| template.templateName | String | テンプレート名 |
| template.categoryId | String | カテゴリーID |
| template.messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array |  |
| template.templateLanguage | String | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object |  |
| template.sender.senderMailAddress | String | 発信メールアドレス |
| template.content | Object |  |
| template.content.title | String | テンプレートメール件名 |
| template.content.body | String | テンプレートメール本文 |
| template.content.attachmentIds | Array | テンプレート添付ファイルID |
| template.createdDateTime | String | テンプレート作成日時 |
| template.updatedDateTime | String | テンプレート修正日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Emailテンプレート詳細照会

GET {{endpoint}}/template/v1.0/EMAIL/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/EMAIL/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0022ReadEmailTemplateList"></span>

## Emailテンプレートリスト照会

テンプレートリストを照会します。

**リクエスト**

```
GET /template/v1.0/EMAIL/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateName | Query  | String | N | テンプレート名(LIKE検索) |
| limit | Query  | Integer | N | limitを設定しない場合はデフォルト20(最大1000) |
| offset | Query  | Integer | N | offsetを設定しない場合はデフォルト0 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "配送完了",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| totalCount | Integer | 総件数 |
| templates | Array |  |
| templates[].templateId | String | テンプレート登録時に発行されたテンプレートID |
| templates[].templateName | String | テンプレート名 |
| templates[].categoryId | String | カテゴリーID |
| templates[].messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | テンプレート作成日時 |
| templates[].updatedDateTime | String | テンプレート修正日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Emailテンプレートリスト照会

GET {{endpoint}}/template/v1.0/EMAIL/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/EMAIL/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0023UpdateEmailTemplate"></span>

## Emailテンプレート修正

テンプレートを修正します。

**リクエスト**

```
PUT /template/v1.0/EMAIL/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->


```
{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] モニタリング通知",
    "body" : "こんにちは。本日お客様の商品が入荷されました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | Y | テンプレート名 |
| messagePurpose | String | N | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.senderMailAddress | String | Y | 発信メールアドレス |
| content | Object | Y |  |
| content.title | String | N | テンプレートメール件名 |
| content.body | String | N | テンプレートメール本文 |
| content.attachmentIds | Array | N | テンプレート添付ファイルID |



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Emailテンプレート修正

PUT {{endpoint}}/template/v1.0/EMAIL/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] モニタリング通知",
    "body" : "こんにちは。本日お客様の商品が入荷されました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/EMAIL/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] モニタリング通知",
    "body" : "こんにちは。本日お客様の商品が入荷されました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>
<span id="templateV1x0024DeleteEmailTemplate"></span>

## Emailテンプレート削除

テンプレートを削除します。

**リクエスト**

```
DELETE /template/v1.0/EMAIL/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Emailテンプレート削除

DELETE {{endpoint}}/template/v1.0/EMAIL/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/EMAIL/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0025CreateRcsTemplate"></span>

## RCSテンプレート登録

テンプレートを登録します。

**リクエスト**

```
POST /template/v1.0/RCS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->


```
{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "タイトル",
      "description" : "本文",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "メインタイトル",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "タイトル1",
      "title2" : "タイトル2",
      "title3" : "タイトル3",
      "description1" : "本文1",
      "description2" : "本文2",
      "description3" : "本文3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定タイトル",
                "description" : "予定説明"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "予定を登録する",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "予定タイトル",
              "description" : "予定説明"
            }
          }
        }
      }
    } ]
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | Y | テンプレート名 |
| categoryId | String | N | カテゴリーID |
| messagePurpose | String | N | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | Y |  |
| sender.brandId | String | Y | ブランドID |
| sender.chatbotId | String | Y | トークルーム(チャットボット)ID |
| content | Object | Y |  |
| content.messageType | String | N | RCS送信メッセージタイプ<br>[SMS、LMS、MMS、RBC_TEMPLATE] |
| content.title | String | N | メッセージ件名 |
| content.body | String | N | メッセージ本文 |
| content.smsType | String | N | SMSタイプ<br>[STANDALONE] |
| content.lmsType | String | N | LMSタイプ<br>[STANDALONE, FORMAT_BASIC, FORMAT_TITLE_HIGHLIGHT, FORMAT_PARAGRAPH] |
| content.mmsType | String | N | MMSタイプ(MMS送信の場合は必須)<br>[HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL] |
| content.messagebaseId | String | N | RCS Biz CenterテンプレートID |
| content.unsubscribePhoneNumber | String | N | 配信停止番号(広告送信の場合は必須) |
| content.cards | Array | N | RCSカード |
| content.cards[].title | String | N | タイトル |
| content.cards[].description | String | N | 本文 |
| content.cards[].attachmentId | String | N | 画像添付ファイルID |
| content.cards[].mTitle | String | N | メインタイトル |
| content.cards[].mTitleMedia | String | N | メインタイトルロゴファイルID |
| content.cards[].title1 | String | N | タイトル1 |
| content.cards[].title2 | String | N | タイトル2 |
| content.cards[].title3 | String | N | タイトル3 |
| content.cards[].description1 | String | N | 本文1 |
| content.cards[].description2 | String | N | 本文2 |
| content.cards[].description3 | String | N | 本文3 |
| content.cards[].buttons | Array | N |  |
| content.buttons | Array | N | RCSボタンリスト |
| content.buttons[].buttonType | String | N | buttonType値と同じ名前を持つActionオブジェクトがbuttonJsonに含まれます。<br>ボタンタイプ トークルームを開く(COMPOSE)、コピーする(CLIPBOARD)、電話をかける(DIALER)、地図を表示する(MAP_SHOW)、地図を検索する(MAP_QUERY)、現在地を共有する(MAP_SHARE)、URLに接続する(URL)、日程を登録する(CALENDAR)<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | N |  |
| content.buttons[].buttonJson.action | Object | N | ボタンアクション |



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "templateId" : "A9z0A9z0"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| templateId | String | テンプレート登録時に発行されたテンプレートID |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### RCSテンプレート登録

POST {{endpoint}}/template/v1.0/RCS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "タイトル",
      "description" : "本文",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "メインタイトル",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "タイトル1",
      "title2" : "タイトル2",
      "title3" : "タイトル3",
      "description1" : "本文1",
      "description2" : "本文2",
      "description3" : "本文3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定タイトル",
                "description" : "予定説明"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "予定を登録する",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "予定タイトル",
              "description" : "予定説明"
            }
          }
        }
      }
    } ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/RCS/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "タイトル",
      "description" : "本文",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "メインタイトル",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "タイトル1",
      "title2" : "タイトル2",
      "title3" : "タイトル3",
      "description1" : "本文1",
      "description2" : "本文2",
      "description3" : "本文3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定タイトル",
                "description" : "予定説明"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "予定を登録する",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "予定タイトル",
              "description" : "予定説明"
            }
          }
        }
      }
    } ]
  }
}'
```

</details>
<span id="templateV1x0026ReadRcsTemplateList"></span>

## RCSテンプレートリスト照会

テンプレートリストを照会します。

**リクエスト**

```
GET /template/v1.0/RCS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateName | Query  | String | N | テンプレート名(LIKE検索) |
| limit | Query  | Integer | N | limitを設定しない場合はデフォルト20(最大1000) |
| offset | Query  | Integer | N | offsetを設定しない場合はデフォルト0 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "配送完了",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| totalCount | Integer | 総件数 |
| templates | Array |  |
| templates[].templateId | String | テンプレート登録時に発行されたテンプレートID |
| templates[].templateName | String | テンプレート名 |
| templates[].categoryId | String | カテゴリーID |
| templates[].messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | テンプレート作成日時 |
| templates[].updatedDateTime | String | テンプレート修正日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### RCSテンプレートリスト照会

GET {{endpoint}}/template/v1.0/RCS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/RCS/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0027ReadRcsTemplate"></span>

## RCSテンプレート詳細照会

テンプレートを詳細照会します。

**リクエスト**

```
GET /template/v1.0/RCS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "テンプレート名",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "sender" : {
      "brandId" : "AR.lj0eOjEI7Y",
      "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
    },
    "content" : {
      "messageType" : "SMS",
      "title" : "祝日の営業時間のお知らせ",
      "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください^^",
      "smsType" : "STANDALONE",
      "lmsType" : "HORIZONTAL",
      "mmsType" : "HORIZONTAL",
      "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
      "messagebaseformId" : "SS000000",
      "unsubscribePhoneNumber" : "08012341234",
      "cards" : [ {
        "title" : "タイトル",
        "description" : "本文",
        "attachmentId" : "20240814125609swLmoZTsGr0",
        "mTitle" : "メインタイトル",
        "mTitleMedia" : "LT-messagebase.common-2k8ydI",
        "title1" : "タイトル1",
        "title2" : "タイトル2",
        "title3" : "タイトル3",
        "description1" : "本文1",
        "description2" : "本文2",
        "description3" : "本文3",
        "buttons" : [ {
          "buttonType" : "CALENDAR",
          "buttonJson" : {
            "action" : {
              "displayText" : "予定を登録する",
              "calendarAction" : {
                "createCalendarEvent" : {
                  "startTime" : "2024-01-01T00:00:00.000+09:00",
                  "endTime" : "2024-01-01T00:00:00.000+09:00",
                  "title" : "予定タイトル",
                  "description" : "予定説明"
                }
              }
            }
          }
        } ]
      } ],
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定タイトル",
                "description" : "予定説明"
              }
            }
          }
        }
      } ]
    },
    "additionalProperty" : {
      "status" : "SUCCESS",
      "approvedDateTime" : "2024-10-29T06:00:01.000+09:00"
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| template | Object |  |
| template.templateId | String | テンプレート登録時に発行されたテンプレートID |
| template.templateName | String | テンプレート名 |
| template.categoryId | String | カテゴリーID |
| template.messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array |  |
| template.templateLanguage | String | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.sender | Object |  |
| template.sender.brandId | String | ブランドID |
| template.sender.chatbotId | String | トークルーム(チャットボット)ID |
| template.content | Object |  |
| template.content.messageType | String | RCS送信メッセージタイプ<br>[SMS、LMS、MMS、RBC_TEMPLATE] |
| template.content.title | String | メッセージ件名 |
| template.content.body | String | メッセージ本文 |
| template.content.smsType | String | SMSタイプ<br>[STANDALONE] |
| template.content.lmsType | String | LMSタイプ<br>[STANDALONE, FORMAT_BASIC, FORMAT_TITLE_HIGHLIGHT, FORMAT_PARAGRAPH] |
| template.content.mmsType | String | MMSタイプ(MMS送信の場合は必須)<br>[HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL] |
| template.content.messagebaseId | String | RCS Biz CenterテンプレートID |
| template.content.messagebaseformId | String | RCS Biz Centerで指定したmessageBase様式<br><br>[SS000000(基本型)、SL000000(基本型)、OL00000001(LMS Format基本型)、OL00000002(LMS Formatタイトル強調型)、OL00000003(LMS Format段落型)、SMwThT00(MMS縦型)、SMwThM00(MMS横型)、CMwMhM0200(MMSスライド中型(2))、CMwMhM0300(MMSスライド中型(3))、CMwMhM0400(MMSスライド中型(4))、CMwMhM0500(MMSスライド中型(5))、CMwMhM0600(MMSスライド中型(6))、CMwShS0200(MMSスライド小型(2))、CMwShS0300(MMSスライド小型(3))、CMwShS0400(MMSスライド小型(4))、CMwShS0500(MMSスライド小型(5))、CMwShS0600(MMSスライド小型(6))、CLI00001(アイテム詳細型)、ITTBNV(サムネイル型(縦))、ITTBNH(サムネイル型(横))、ITHIMS(画像強調型(1:1))、ITHIMV(画像強調型(3:4))、ITSNSS(SNS型)、ITSNSH(SNS型(中間ボタン))、ITHITS(画像＆タイトル強調型(1:1))、ITHITV(画像＆タイトル強調型(3:4))、ITCRM2(スライド型(2))、ITCRM3(スライド型(3))、ITCRM4(スライド型(4))、ITCRM5(スライド型(5))、ITCRM6(スライド型(6))、CLT00001(アイテム強調型 DESC)、CLT00002(アイテム強調型 TABLE)、TATA001C(タイトル自由型 FREE)、TATA001D(タイトル自由型 CELL)、TATA001F(タイトル自由型 DESC)、FF005C(タイトル選択型 FREE)、FF005D(明細書 CELL)、FF004C(明細書 DESC)、FF004D(キャンセル CELL)、GG003C(キャンセル DESC)、GG003D(案内 CELL)、GG002C(案内 DESC)、GG002D(認証 CELL)、GG001C(認証 DESC)、GG001D(会員登録 CELL)、GG000F(会員登録 DESC)、EE001C(予約 CELL)、EE001D(予約 DESC)、CC003C(配送 CELL)、CC003D(配送 DESC)、FF002C(入金 CELL)、FF002D(入金 DESC)、FF001C(承認 CELL)、FF001D(承認 DESC)、CC002C(注文 CELL)、CC002D(注文 DESC)、CC001C(出庫 CELL)、CC001D(出庫 DESC)、FF003C(出金 CELL)、FF003D(出金 DESC)、CLL00001(LMS明細書 A)、CLL00002(LMS段落型)、CLL00003(LMSタイトル強調型)、CLL00004(LMS基本型)、CLL00005(LMS明細書 B)、CLL00006(LMS明細書 C)] |
| template.content.unsubscribePhoneNumber | String | 配信停止番号(広告送信の場合は必須) |
| template.content.cards | Array | RCSカード |
| template.content.cards[].title | String | タイトル |
| template.content.cards[].description | String | 本文 |
| template.content.cards[].attachmentId | String | 画像添付ファイルID |
| template.content.cards[].mTitle | String | メインタイトル |
| template.content.cards[].mTitleMedia | String | メインタイトルロゴファイルID |
| template.content.cards[].title1 | String | タイトル1 |
| template.content.cards[].title2 | String | タイトル2 |
| template.content.cards[].title3 | String | タイトル3 |
| template.content.cards[].description1 | String | 本文1 |
| template.content.cards[].description2 | String | 本文2 |
| template.content.cards[].description3 | String | 本文3 |
| template.content.cards[].buttons | Array |  |
| template.content.buttons | Array | RCSボタンリスト |
| template.content.buttons[].buttonType | String | buttonType値と同じ名前を持つActionオブジェクトがbuttonJsonに含まれます。<br>ボタンタイプ トークルームを開く(COMPOSE)、コピーする(CLIPBOARD)、電話をかける(DIALER)、地図を表示する(MAP_SHOW)、地図を検索する(MAP_QUERY)、現在地を共有する(MAP_SHARE)、URLに接続する(URL)、日程を登録する(CALENDAR)<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| template.content.buttons[].buttonJson | Object |  |
| template.content.buttons[].buttonJson.action | Object | ボタンアクション |
| template.additionalProperty | Object |  |
| template.additionalProperty.status | String | テンプレートステータス<br>- SAVE: 保存<br>- APPROVE_WAIT: 承認待ち<br>- INSPECTION_START: 審査開始<br>- INSPECTION_FINISH: 審査完了<br>- APPROVE: 承認<br>- REJECT: 拒否<br>- MODIFY_APPROVE_WAIT: 修正承認待ち<br>- MODIFY_INSPECTION_START: 修正審査開始<br>- MODIFY_INSPECTION_FINISH: 修正審査完了<br>- MODIFY_REJECT: 修正拒否<br><br>[SAVE, APPROVE_WAIT, INSPECTION_START, INSPECTION_FINISH, APPROVE, REJECT, MODIFY_APPROVE_WAIT, MODIFY_INSPECTION_START, MODIFY_INSPECTION_FINISH, MODIFY_REJECT] |
| template.additionalProperty.approvedDateTime | String | テンプレート承認日時 |
| template.createdDateTime | String | テンプレート作成日時 |
| template.updatedDateTime | String | テンプレート修正日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### RCSテンプレート詳細照会

GET {{endpoint}}/template/v1.0/RCS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/RCS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0028UpdateRcsTemplate"></span>

## RCSテンプレート修正

テンプレートを修正します。

**リクエスト**

```
PUT /template/v1.0/RCS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->


```
{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "タイトル",
      "description" : "本文",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "メインタイトル",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "タイトル1",
      "title2" : "タイトル2",
      "title3" : "タイトル3",
      "description1" : "本文1",
      "description2" : "本文2",
      "description3" : "本文3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定タイトル",
                "description" : "予定説明"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "予定を登録する",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "予定タイトル",
              "description" : "予定説明"
            }
          }
        }
      }
    } ]
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | Y | テンプレート名 |
| messagePurpose | String | N | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| sender | Object | N |  |
| sender.brandId | String | Y | ブランドID |
| sender.chatbotId | String | Y | トークルーム(チャットボット)ID |
| content | Object | Y |  |
| content.messageType | String | N | RCS送信メッセージタイプ<br>[SMS、LMS、MMS、RBC_TEMPLATE] |
| content.title | String | N | メッセージ件名 |
| content.body | String | N | メッセージ本文 |
| content.smsType | String | N | SMSタイプ<br>[STANDALONE] |
| content.lmsType | String | N | LMSタイプ<br>[STANDALONE, FORMAT_BASIC, FORMAT_TITLE_HIGHLIGHT, FORMAT_PARAGRAPH] |
| content.mmsType | String | N | MMSタイプ(MMS送信の場合は必須)<br>[HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL] |
| content.messagebaseId | String | N | RCS Biz CenterテンプレートID |
| content.unsubscribePhoneNumber | String | N | 配信停止番号(広告送信の場合は必須) |
| content.cards | Array | N | RCSカード |
| content.cards[].title | String | N | タイトル |
| content.cards[].description | String | N | 本文 |
| content.cards[].attachmentId | String | N | 画像添付ファイルID |
| content.cards[].mTitle | String | N | メインタイトル |
| content.cards[].mTitleMedia | String | N | メインタイトルロゴファイルID |
| content.cards[].title1 | String | N | タイトル1 |
| content.cards[].title2 | String | N | タイトル2 |
| content.cards[].title3 | String | N | タイトル3 |
| content.cards[].description1 | String | N | 本文1 |
| content.cards[].description2 | String | N | 本文2 |
| content.cards[].description3 | String | N | 本文3 |
| content.cards[].buttons | Array | N |  |
| content.buttons | Array | N | RCSボタンリスト |
| content.buttons[].buttonType | String | N | buttonType値と同じ名前を持つActionオブジェクトがbuttonJsonに含まれます。<br>ボタンタイプ トークルームを開く(COMPOSE)、コピーする(CLIPBOARD)、電話をかける(DIALER)、地図を表示する(MAP_SHOW)、地図を検索する(MAP_QUERY)、現在地を共有する(MAP_SHARE)、URLに接続する(URL)、日程を登録する(CALENDAR)<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | N |  |
| content.buttons[].buttonJson.action | Object | N | ボタンアクション |



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### RCSテンプレート修正

PUT {{endpoint}}/template/v1.0/RCS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "タイトル",
      "description" : "本文",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "メインタイトル",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "タイトル1",
      "title2" : "タイトル2",
      "title3" : "タイトル3",
      "description1" : "本文1",
      "description2" : "本文2",
      "description3" : "本文3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定タイトル",
                "description" : "予定説明"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "予定を登録する",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "予定タイトル",
              "description" : "予定説明"
            }
          }
        }
      }
    } ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/RCS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "タイトル",
      "description" : "本文",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "メインタイトル",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "タイトル1",
      "title2" : "タイトル2",
      "title3" : "タイトル3",
      "description1" : "本文1",
      "description2" : "本文2",
      "description3" : "本文3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定タイトル",
                "description" : "予定説明"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "予定を登録する",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "予定タイトル",
              "description" : "予定説明"
            }
          }
        }
      }
    } ]
  }
}'
```

</details>
<span id="templateV1x0029DeleteRcsTemplate"></span>

## RCSテンプレート削除

テンプレートを削除します。

**リクエスト**

```
DELETE /template/v1.0/RCS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### RCSテンプレート削除

DELETE {{endpoint}}/template/v1.0/RCS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/RCS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0030CreatePushTemplate"></span>

## Pushテンプレート登録

テンプレートを登録します。

**リクエスト**

```
POST /template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->


```
{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "代表番号",
    "unsubscribeGuide" : "メニュー > 設定",
    "title" : "タイトル",
    "body" : "内容",
    "richMessage" : {
      "buttons" : [ {
        "name" : "ボタン名",
        "submitName" : "送信ボタン名",
        "buttonType" : "ボタンタイプ、REPLY、DEEP_LINK、OPEN_APP、OPEN_URL、DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに関するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きなアイコンの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
        "description" : "グループに関する説明"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | Y | テンプレート名 |
| categoryId | String | N | カテゴリーID |
| messagePurpose | String | N | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| content | Object | Y | プッシュメッセージ内容 |



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "templateId" : "A9z0A9z0"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| templateId | String | テンプレート登録時に発行されたテンプレートID |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Pushテンプレート登録

POST {{endpoint}}/template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "代表番号",
    "unsubscribeGuide" : "メニュー > 設定",
    "title" : "タイトル",
    "body" : "内容",
    "richMessage" : {
      "buttons" : [ {
        "name" : "ボタン名",
        "submitName" : "送信ボタン名",
        "buttonType" : "ボタンタイプ、REPLY、DEEP_LINK、OPEN_APP、OPEN_URL、DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに関するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きなアイコンの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
        "description" : "グループに関する説明"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/PUSH/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "テンプレート名",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "代表番号",
    "unsubscribeGuide" : "メニュー > 設定",
    "title" : "タイトル",
    "body" : "内容",
    "richMessage" : {
      "buttons" : [ {
        "name" : "ボタン名",
        "submitName" : "送信ボタン名",
        "buttonType" : "ボタンタイプ、REPLY、DEEP_LINK、OPEN_APP、OPEN_URL、DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに関するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きなアイコンの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
        "description" : "グループに関する説明"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}'
```

</details>
<span id="templateV1x0031ReadPushTemplateList"></span>

## Pushテンプレートリスト照会

テンプレートリストを照会します。

**リクエスト**

```
GET /template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateName | Query  | String | N | テンプレート名(LIKE検索) |
| limit | Query  | Integer | N | limitを設定しない場合はデフォルト20(最大1000) |
| offset | Query  | Integer | N | offsetを設定しない場合はデフォルト0 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "templates" : [ {
    "templateId" : "A9z0A9z0",
    "templateName" : "配送完了",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| totalCount | Integer | 総件数 |
| templates | Array |  |
| templates[].templateId | String | テンプレート登録時に発行されたテンプレートID |
| templates[].templateName | String | テンプレート名 |
| templates[].categoryId | String | カテゴリーID |
| templates[].messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| templates[].messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templates[].messagePurposes | Array |  |
| templates[].createdDateTime | String | テンプレート作成日時 |
| templates[].updatedDateTime | String | テンプレート修正日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Pushテンプレートリスト照会

GET {{endpoint}}/template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/PUSH/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0032ReadPushTemplate"></span>

## Pushテンプレート詳細照会

テンプレートを詳細照会します。

**リクエスト**

```
GET /template/v1.0/PUSH/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "template" : {
    "templateId" : "A9z0A9z0",
    "templateName" : "テンプレート名",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "templateLanguage" : "PLAIN_TEXT",
    "content" : {
      "unsubscribePhoneNumber" : "代表番号",
      "unsubscribeGuide" : "メニュー > 設定",
      "title" : "タイトル",
      "body" : "内容",
      "richMessage" : {
        "buttons" : [ {
          "name" : "ボタン名",
          "submitName" : "送信ボタン名",
          "buttonType" : "ボタンタイプ、REPLY、DEEP_LINK、OPEN_APP、OPEN_URL、DISMISS",
          "link" : "ボタンを押したときに遷移するリンク",
          "hint" : "ボタンに関するヒント"
        } ],
        "media" : {
          "sourceType" : "メディアの位置、REMOTE、LOCAL",
          "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
          "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
          "extension" : "メディアファイルの拡張子、jpg、png",
          "expandable" : true
        },
        "androidMedia" : {
          "sourceType" : "メディアの位置、REMOTE、LOCAL",
          "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
          "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
          "extension" : "メディアファイルの拡張子、jpg、png",
          "expandable" : true
        },
        "iosMedia" : {
          "sourceType" : "メディアの位置、REMOTE、LOCAL",
          "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
          "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
          "extension" : "メディアファイルの拡張子、jpg、png",
          "expandable" : true
        },
        "largeIcon" : {
          "sourceType" : "大きなアイコンの位置、REMOTE、LOCAL",
          "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE"
        },
        "group" : {
          "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
          "description" : "グループに関する説明"
        }
      },
      "style" : {
        "useHtmlStyle" : true
      },
      "customKey" : "customValue"
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| template | Object |  |
| template.templateId | String | テンプレート登録時に発行されたテンプレートID |
| template.templateName | String | テンプレート名 |
| template.categoryId | String | カテゴリーID |
| template.messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| template.messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array |  |
| template.templateLanguage | String | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| template.content | Object | プッシュメッセージ内容 |
| template.createdDateTime | String | テンプレート作成日時 |
| template.updatedDateTime | String | テンプレート修正日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Pushテンプレート詳細照会

GET {{endpoint}}/template/v1.0/PUSH/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/PUSH/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0033UpdatePushTemplate"></span>

## Pushテンプレート修正

テンプレートを修正します。

**リクエスト**

```
PUT /template/v1.0/PUSH/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->


```
{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "代表番号",
    "unsubscribeGuide" : "メニュー > 設定",
    "title" : "タイトル",
    "body" : "内容",
    "richMessage" : {
      "buttons" : [ {
        "name" : "ボタン名",
        "submitName" : "送信ボタン名",
        "buttonType" : "ボタンタイプ、REPLY、DEEP_LINK、OPEN_APP、OPEN_URL、DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに関するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きなアイコンの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
        "description" : "グループに関する説明"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | Y | テンプレート名 |
| messagePurpose | String | N | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | テンプレートタイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT, FREEMARKER] |
| content | Object | Y | プッシュメッセージ内容 |



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Pushテンプレート修正

PUT {{endpoint}}/template/v1.0/PUSH/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "代表番号",
    "unsubscribeGuide" : "メニュー > 設定",
    "title" : "タイトル",
    "body" : "内容",
    "richMessage" : {
      "buttons" : [ {
        "name" : "ボタン名",
        "submitName" : "送信ボタン名",
        "buttonType" : "ボタンタイプ、REPLY、DEEP_LINK、OPEN_APP、OPEN_URL、DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに関するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きなアイコンの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
        "description" : "グループに関する説明"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/PUSH/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "content" : {
    "unsubscribePhoneNumber" : "代表番号",
    "unsubscribeGuide" : "メニュー > 設定",
    "title" : "タイトル",
    "body" : "内容",
    "richMessage" : {
      "buttons" : [ {
        "name" : "ボタン名",
        "submitName" : "送信ボタン名",
        "buttonType" : "ボタンタイプ、REPLY、DEEP_LINK、OPEN_APP、OPEN_URL、DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに関するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きなアイコンの位置、REMOTE、LOCAL",
        "source" : "メディアの配置場所のアドレス、URL、LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
        "description" : "グループに関する説明"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}'
```

</details>
<span id="templateV1x0034DeletePushTemplate"></span>

## Pushテンプレート削除

テンプレートを削除します。

**リクエスト**

```
DELETE /template/v1.0/PUSH/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Pushテンプレート削除

DELETE {{endpoint}}/template/v1.0/PUSH/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/PUSH/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV1x0035ReadTemplateParameters"></span>

## テンプレートパラメータ照会

テンプレートに含まれているパラメータリストを照会します。

**リクエスト**

```
GET /template/v1.0/{messageChannel}/templates/{templateId}/parameters
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| messageChannel | Path  | String | Y | メッセージチャネルです。<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| templateId | Path  | String | Y | テンプレートID |



**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "templateParameter" : {
    "validateTimestamp" : "",
    "timestamp" : "",
    "validateFailDomainList" : [ {
      "domain" : "",
      "verifyYn" : "",
      "spfYn" : "",
      "dkimVerifyYn" : "",
      "dmarcYn" : ""
    } ]
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| templateParameter | Object | テンプレートパラメータ結果JSON |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### テンプレートパラメータ照会

GET {{endpoint}}/template/v1.0/{{messageChannel}}/templates/{{templateId}}/parameters
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/${messageChannel}/templates/${templateId}/parameters" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
