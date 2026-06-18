<!-- pre-align:aligned sig=8780bb7cdba0 -->

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

## お知らせトークテンプレートのカカオテンプレート一覧照会

お知らせトークテンプレートのカカオテンプレート一覧を照会します。

**リクエスト**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| templateId | Path | String | O | テンプレートID |
| limit | Query | Number | X | limitを設定しない場合、デフォルト20（最大1000） |
| offset | Query | Number | X | offsetを設定しない場合、デフォルト0 |



**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->

このAPIはリクエスト本文を要求しません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は「このAPIはレスポンス本文を返しません」と入力します。-->

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
      "templateAd" : "チャンネルを追加してこのチャンネルのマーケティングメッセージなどをKakaoTalkで受け取る",
      "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する場合があり、チェックインができない場合は予約がキャンセルされることがあります。\\n* お問い合わせ電話: 1234-1234",
      "templateTitle" : "123,450円",
      "templateSubtitle" : "承認内容",
      "templateHeader" : "注文が成立しました。",
      "templateItem" : {
        "list" : [ {
          "title" : "アイテムタイトル",
          "description" : "アイテムの説明"
        } ],
        "summary" : {
          "title" : "概要タイトル",
          "description" : "概要の説明"
        }
      },
      "templateItemHighlight" : {
        "title" : "ハイライトタイトル",
        "description" : "ハイライトの説明",
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
        "name" : "クイックリプライ名",
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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| totalCount | Integer | O | 総件数 |
| templates | Array | O |  |
| templates[].kakaoTemplateCode | String | O | カカオテンプレートコード |
| templates[].kakaoTemplateName | String | O | テンプレート名 |
| templates[].content | Object | O |  |
| templates[].content.templateMessageType | String | X | テンプレートメッセージタイプ（BA: 基本型、EX: 付加情報型、AD: チャンネル追加型、MI: 複合型、デフォルト: BA） |
| templates[].content.templateEmphasizeType | String | O | テンプレート強調表示タイプ<br>[NONE（強調なし）、TEXT（テキスト強調）、IMAGE（イメージ強調）、ITEM_LIST（アイテムリスト強調）] |
| templates[].content.templateContent | String | X | テンプレート本文 |
| templates[].content.templateAd | String | X | チャンネル追加案内メッセージ（テンプレートメッセージタイプ: チャンネル追加型、複合型の場合は固定値） |
| templates[].content.templateExtra | String | X | テンプレート付加情報（テンプレートメッセージタイプが[付加情報型/複合型]の場合は必須）、置換変数使用不可、URL含めることが可能 |
| templates[].content.templateTitle | String | X | テンプレートタイトル（最大50文字、Android: 2行、23文字以上は省略表示、iOS: 2行、27文字以上は省略表示） |
| templates[].content.templateSubtitle | String | X | テンプレート補助文言（最大50文字、Android: 18文字以上は省略表示、iOS: 21文字以上は省略表示） |
| templates[].content.templateHeader | String | X | テンプレートヘッダー、変数入力可能 |
| templates[].content.templateItem | Object | X |  |
| templates[].content.templateItem.list | Array | O |  |
| templates[].content.templateItem.list[].title | String | O | アイテムタイトル |
| templates[].content.templateItem.list[].description | String | O | アイテムの説明 |
| templates[].content.templateItem.summary | Object | X |  |
| templates[].content.templateItem.summary.title | String | O | 概要タイトル |
| templates[].content.templateItem.summary.description | String | O | 概要の説明（変数および通貨単位、数字、カンマ、ピリオドのみ使用可能） |
| templates[].content.templateItemHighlight | Object | X |  |
| templates[].content.templateItemHighlight.title | String | O | アイテムハイライトタイトル（最大30文字、サムネイル画像がある場合は21文字） |
| templates[].content.templateItemHighlight.description | String | O | アイテムハイライトの説明（最大19文字、サムネイル画像がある場合は13文字） |
| templates[].content.templateItemHighlight.attachmentId | String | X | テンプレート添付ファイルID |
| templates[].content.templateItemHighlight.imageUrl | String | X | サムネイル画像のURL |
| templates[].content.templateRepresentLink | Object | X |  |
| templates[].content.templateRepresentLink.linkMo | String | X | 代表リンク モバイルWebリンク |
| templates[].content.templateRepresentLink.linkPc | String | X | 代表リンク PC Webリンク |
| templates[].content.templateRepresentLink.schemeIos | String | X | 代表リンク iOSアプリリンク |
| templates[].content.templateRepresentLink.schemeAndroid | String | X | 代表リンク Androidアプリリンク |
| templates[].content.attachmentId | String | X | テンプレート添付ファイルID |
| templates[].content.templateImageName | String | X | テンプレート画像名 |
| templates[].content.templateImageUrl | String | X | テンプレート画像リンク |
| templates[].content.securityFlag | Boolean | X | テンプレートセキュリティ有無（デフォルト: false） |
| templates[].content.categoryCode | String | X | テンプレートカテゴリコード（テンプレートカテゴリ照会API参照、デフォルト: 999999） |
| templates[].content.buttons | Array | X | テンプレートボタン |
| templates[].content.buttons[].ordering | Integer | O | テンプレートボタンの順序 |
| templates[].content.buttons[].type | String | O | テンプレートボタンタイプ<br>[WL（Webリンク）、AL（アプリリンク）、DS（配送照会）、BK（ボットキーワード）、MD（メッセージ転達）、BC（相談トーク転換）、BT（ボット転換）、AC（チャンネル追加）、BF（ビジネスフォーム）、P1（イメージセキュリティ転送プラグイン）、P2（個人情報利用プラグイン）、P3（ワンクリック決済プラグイン）、TN（電話をかける）] |
| templates[].content.buttons[].name | String | O | テンプレートボタン名 |
| templates[].content.buttons[].linkMo | String | X | テンプレートボタン モバイルWebリンク |
| templates[].content.buttons[].linkPc | String | X | テンプレートボタン PC Webリンク |
| templates[].content.buttons[].schemeIos | String | X | テンプレートボタン iOSアプリリンク |
| templates[].content.buttons[].schemeAndroid | String | X | テンプレートボタン Androidアプリリンク |
| templates[].content.buttons[].bizFormId | Integer | X | テンプレートボタン ビジネスフォームID（BFタイプの場合は必須） |
| templates[].content.quickReplies | Array | X | テンプレートクイックリプライ |
| templates[].content.quickReplies[].ordering | Integer | O | テンプレートクイックリプライの順序 |
| templates[].content.quickReplies[].type | String | O | テンプレートクイックリプライタイプ<br>[WL（Webリンク）、AL（アプリリンク）、BK（ボットキーワード）、BC（相談トーク転換）、BT（ボット転換）、BF（ビジネスフォーム）] |
| templates[].content.quickReplies[].name | String | O | テンプレートクイックリプライ名 |
| templates[].content.quickReplies[].linkMo | String | X | テンプレートクイックリプライ モバイルWebリンク |
| templates[].content.quickReplies[].linkPc | String | X | テンプレートクイックリプライ PC Webリンク |
| templates[].content.quickReplies[].schemeIos | String | X | テンプレートクイックリプライ iOSアプリリンク |
| templates[].content.quickReplies[].schemeAndroid | String | X | テンプレートクイックリプライ Androidアプリリンク |
| templates[].content.quickReplies[].bizFormId | Integer | X | テンプレートクイックリプライ ビジネスフォームID（BFタイプの場合は必須） |
| templates[].reviewStatus | String | O | REGISTERED: リクエスト、REQUESTED: 審査中、APPROVED: 承認、REJECTED: 差し戻し<br>[REGISTERED, REQUESTED, APPROVED, REJECTED] |
| templates[].comments | Array | O | テンプレートお問い合わせリスト |
| templates[].comments[].id | Integer | O | お問い合わせID |
| templates[].comments[].content | String | X | お問い合わせ内容 |
| templates[].comments[].userName | String | O | 作成者 |
| templates[].comments[].createdAt | String | O | お問い合わせ作成日時 |
| templates[].comments[].attachments | Array | O | お問い合わせ添付ファイル |
| templates[].comments[].attachments[].originalFileName | String | O | 添付ファイル名 |
| templates[].comments[].attachments[].filePath | String | O | 添付ファイルパス |
| templates[].comments[].status | String | O | お問い合わせステータス（REQ: リクエスト、INQ: お問い合わせ、APR: 承認、REJ: 差し戻し、REP: 返答）<br>[REQ, INQ, APR, REJ, REP] |
| templates[].block | Boolean | O | テンプレートブロック有無 |
| templates[].dormant | Boolean | O | テンプレート休眠有無 |
| templates[].createdDateTime | String | O | テンプレート作成日時 |
| templates[].updatedDateTime | String | O | テンプレート更新日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレートのカカオテンプレート一覧照会

GET {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/kakao-templates
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/kakao-templates"
```

</details>

<span id="templateV10ALIMTALKTemplatesTemplateIdKakaoTemplatesKakaoTemplateCodeInquiriesDoWithFilePost"></span>

<a id="submit-an-alimtalk-template-inquiry-with-file-attachment"></a>

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

<a id="submit-an-alimtalk-template-inquiry"></a>

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
| template.templateLanguage | String | テンプレート言語のタイプ<br>デフォルト値：PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarkerテンプレート)] |
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

<a id="register-sms-template"></a>

## SMS テンプレート登録

テンプレートを登録します。

**リクエスト**

```
POST /template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は「この API はリクエスト本文を必要としません」と入力します。-->


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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様の商品が入荷されました。ぜひご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}
```

<!--リクエスト本文のフィールドについて説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | O | テンプレート名 |
| categoryId | String | X | カテゴリー ID |
| messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般)、AD(広告)、AUTH(認証)] |
| templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarker テンプレート)] |
| sender | Object | O |  |
| sender.senderPhoneNumber | String | O | 発信番号 |
| content | Object | O |  |
| content.messageType | String | O | 送信メッセージタイプ(SMS、LMS、MMS)<br>[SMS、LMS、MMS] |
| content.title | String | X | メッセージタイトル |
| content.body | String | O | メッセージ本文 |
| content.attachmentIds | Array | X | 添付ファイル ID（最大 3 件） |
| content.imageLayoutId | String | X | イメージレイアウト ID |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドについて説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| templateId | String | O | テンプレート登録時に発行されたテンプレート ID |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMS テンプレート登録

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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様の商品が入荷されました。ぜひご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/SMS/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様の商品が入荷されました。ぜひご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}'
```

</details>

<span id="templateV1x0002ReadSmsTemplateList"></span>

<a id="list-sms-templates"></a>

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

<a id="get-sms-template-details"></a>

## SMS テンプレート詳細照会

テンプレートを詳細照会します。

**リクエスト**

```
GET /template/v1.0/SMS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| templateId | Path | String | O | テンプレートID |



**リクエスト本文**

<!--このAPIはリクエスト本文を要求しません。-->

このAPIはリクエスト本文を要求しません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は「このAPIはレスポンス本文を返しません」と入力します。-->

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
      "title" : "祝日営業時間のお知らせ",
      "body" : "こんにちは。本日、お客様の商品が入荷しました。ぜひご来店ください^^",
      "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
      "imageLayoutId" : "YaX2DA4Weab1"
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--レスポンス本文のフィールドについて説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | X |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| template | Object | X |  |
| template.templateId | String | O | テンプレート登録時に発行されたテンプレートID |
| template.templateName | String | X | テンプレート名 |
| template.categoryId | String | X | カテゴリーID |
| template.messageChannel | String | X | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| template.messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| template.messagePurposes | Array | X |  |
| template.templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト), FREEMARKER(FreeMarkerテンプレート)] |
| template.sender | Object | X |  |
| template.sender.senderPhoneNumber | String | O | 発信番号 |
| template.content | Object | X |  |
| template.content.messageType | String | O | 送信メッセージタイプ (SMS、LMS、MMS)<br>[SMS, LMS, MMS] |
| template.content.title | String | X | メッセージ件名 |
| template.content.body | String | O | メッセージ本文 |
| template.content.attachmentIds | Array | X | 添付ファイルID（最大3件） |
| template.content.imageLayoutId | String | X | イメージレイアウトID |
| template.createdDateTime | String | X | テンプレート作成日時 |
| template.updatedDateTime | String | X | テンプレート更新日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMS テンプレート詳細照会

GET {{endpoint}}/template/v1.0/SMS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/SMS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0004UpdateSmsTemplate"></span>

<a id="update-sms-template"></a>

## SMS テンプレート修正

テンプレートを修正します。

**リクエスト**

```
PUT /template/v1.0/SMS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| templateId | Path | String | O | テンプレート ID |



**リクエスト本文**

<!--リクエスト本文を要求しない場合は「この API はリクエスト本文を要求しません」と入力します。-->


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
    "body" : "こんにちは。本日、お客様のご注文商品が入荷しました。ぜひご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | O | テンプレート名 |
| messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般)、AD(広告)、AUTH(認証)] |
| templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarker テンプレート)] |
| sender | Object | X |  |
| sender.senderPhoneNumber | String | O | 発信番号 |
| content | Object | O |  |
| content.messageType | String | O | 送信メッセージタイプ (SMS、LMS、MMS)<br>[SMS、LMS、MMS] |
| content.title | String | X | メッセージタイトル |
| content.body | String | O | メッセージ本文 |
| content.attachmentIds | Array | X | 添付ファイル ID（最大 3 件） |
| content.imageLayoutId | String | X | イメージレイアウト ID |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMS テンプレート修正

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
    "body" : "こんにちは。本日、お客様のご注文商品が入荷しました。ぜひご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/SMS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
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
    "body" : "こんにちは。本日、お客様のご注文商品が入荷しました。ぜひご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}'
```

</details>

<span id="templateV1x0005DeleteSmsTemplate"></span>

<a id="delete-sms-template"></a>

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

<a id="register-alimtalk-template"></a>

## お知らせトークテンプレート登録

テンプレートを登録します。

**リクエスト**

```
POST /template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は、「この API はリクエスト本文を必要としません」と入力します。-->


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
    "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをKakaoTalkで受け取る",
    "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する場合があります。チェックインができない場合、予約がキャンセルされる場合があります。\\n* お問い合わせ電話: 1234-1234",
    "templateTitle" : "123,450円",
    "templateSubtitle" : "承認履歴",
    "templateHeader" : "ご注文が確定しました。",
    "templateItem" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "description" : "アイテムの説明"
      } ],
      "summary" : {
        "title" : "サマリータイトル",
        "description" : "サマリーの説明"
      }
    },
    "templateItemHighlight" : {
      "title" : "ハイライトタイトル",
      "description" : "ハイライトの説明",
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
      "name" : "クイックリプライ名",
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

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | O | テンプレート名 |
| categoryId | String | X | カテゴリー ID |
| messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト), FREEMARKER(FreeMarker テンプレート)] |
| sender | Object | X |  |
| sender.senderKey | String | X | 発信プロフィールの発信キー |
| sender.senderProfileType | String | X | 発信プロフィールタイプ<br>[GROUP, NORMAL] |
| content | Object | O |  |
| content.templateMessageType | String | X | テンプレートメッセージタイプ (BA: 基本型、EX: 付加情報型、AD: チャンネル追加型、MI: 複合型、default: BA) |
| content.templateEmphasizeType | String | O | テンプレート強調表示タイプ<br>[NONE(強調なし), TEXT(テキスト強調), IMAGE(イメージ強調), ITEM_LIST(アイテムリスト強調)] |
| content.templateContent | String | X | テンプレート本文 |
| content.templateAd | String | X | チャンネル追加案内メッセージ (テンプレートメッセージタイプがチャンネル追加型または複合型の場合は固定値) |
| content.templateExtra | String | X | テンプレート付加情報 (テンプレートメッセージタイプが[付加情報型/複合型]の場合は必須)。置換変数は使用不可、URL は含めることができます |
| content.templateTitle | String | X | テンプレートタイトル (最大 50 文字、Android: 2 行、23 文字以上は省略表示、iOS: 2 行、27 文字以上は省略表示) |
| content.templateSubtitle | String | X | テンプレートサブ文言 (最大 50 文字、Android: 18 文字以上は省略表示、iOS: 21 文字以上は省略表示) |
| content.templateHeader | String | X | テンプレートヘッダー。変数入力可能 |
| content.templateItem | Object | X |  |
| content.templateItem.list | Array | O |  |
| content.templateItem.list[].title | String | O | アイテムタイトル |
| content.templateItem.list[].description | String | O | アイテムの説明 |
| content.templateItem.summary | Object | X |  |
| content.templateItem.summary.title | String | O | サマリータイトル |
| content.templateItem.summary.description | String | O | サマリーの説明 (変数および通貨単位、数字、カンマ、ピリオドのみ使用可能) |
| content.templateItemHighlight | Object | X |  |
| content.templateItemHighlight.title | String | O | アイテムハイライトタイトル (最大 30 文字、サムネイル画像がある場合は 21 文字) |
| content.templateItemHighlight.description | String | O | アイテムハイライトの説明 (最大 19 文字、サムネイル画像がある場合は 13 文字) |
| content.templateItemHighlight.attachmentId | String | X | テンプレート添付ファイル ID |
| content.templateItemHighlight.imageUrl | String | X | サムネイル画像の URL |
| content.templateRepresentLink | Object | X |  |
| content.templateRepresentLink.linkMo | String | X | 代表リンクのモバイル Web リンク |
| content.templateRepresentLink.linkPc | String | X | 代表リンクの PC Web リンク |
| content.templateRepresentLink.schemeIos | String | X | 代表リンクの iOS アプリリンク |
| content.templateRepresentLink.schemeAndroid | String | X | 代表リンクの Android アプリリンク |
| content.attachmentId | String | X | テンプレート添付ファイル ID |
| content.templateImageName | String | X | テンプレート画像名 |
| content.templateImageUrl | String | X | テンプレート画像リンク |
| content.securityFlag | Boolean | X | テンプレートセキュリティフラグ (default: false) |
| content.categoryCode | String | X | テンプレートカテゴリーコード (テンプレートカテゴリー照会 API 参照、default: 999999) |
| content.buttons | Array | X | テンプレートボタン |
| content.buttons[].ordering | Integer | O | テンプレートボタンの順序 |
| content.buttons[].type | String | O | テンプレートボタンタイプ<br>[WL(Web リンク), AL(アプリリンク), DS(配送照会), BK(ボットキーワード), MD(メッセージ転送), BC(相談トーク転換), BT(ボット転換), AC(チャンネル追加), BF(ビジネスフォーム), P1(イメージセキュリティ送信プラグイン), P2(個人情報利用プラグイン), P3(ワンクリック決済プラグイン), TN(電話する)] |
| content.buttons[].name | String | O | テンプレートボタン名 |
| content.buttons[].linkMo | String | X | テンプレートボタンのモバイル Web リンク |
| content.buttons[].linkPc | String | X | テンプレートボタンの PC Web リンク |
| content.buttons[].schemeIos | String | X | テンプレートボタンの iOS アプリリンク |
| content.buttons[].schemeAndroid | String | X | テンプレートボタンの Android アプリリンク |
| content.buttons[].bizFormId | Integer | X | テンプレートボタンのビジネスフォーム ID (BF タイプの場合は必須) |
| content.quickReplies | Array | X | テンプレートクイックリプライ |
| content.quickReplies[].ordering | Integer | O | テンプレートクイックリプライの順序 |
| content.quickReplies[].type | String | O | テンプレートクイックリプライのタイプ<br>[WL(Web リンク), AL(アプリリンク), BK(ボットキーワード), BC(相談トーク転換), BT(ボット転換), BF(ビジネスフォーム)] |
| content.quickReplies[].name | String | O | テンプレートクイックリプライ名 |
| content.quickReplies[].linkMo | String | X | テンプレートクイックリプライのモバイル Web リンク |
| content.quickReplies[].linkPc | String | X | テンプレートクイックリプライの PC Web リンク |
| content.quickReplies[].schemeIos | String | X | テンプレートクイックリプライの iOS アプリリンク |
| content.quickReplies[].schemeAndroid | String | X | テンプレートクイックリプライの Android アプリリンク |
| content.quickReplies[].bizFormId | Integer | X | テンプレートクイックリプライのビジネスフォーム ID (BF タイプの場合は必須) |
| additionalProperty | Object | O |  |
| additionalProperty.templateCode | String | O | テンプレートコード (英字、数字、-、_) |
| additionalProperty.kakaoTemplateCode | String | X | カカオテンプレートコード |



**レスポンス本文**

<!--レスポンス本文を返さない場合は、「この API はレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| templateId | String | O | テンプレート登録時に発行されたテンプレート ID |



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
    "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する場合があります。また、チェックインができない場合、予約がキャンセルされることがあります。\\n* お問い合わせ電話: 1234-1234",
    "templateTitle" : "123,450円",
    "templateSubtitle" : "承認履歴",
    "templateHeader" : "注文が確定しました。",
    "templateItem" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "description" : "アイテムの説明"
      } ],
      "summary" : {
        "title" : "サマリータイトル",
        "description" : "サマリーの説明"
      }
    },
    "templateItemHighlight" : {
      "title" : "ハイライトタイトル",
      "description" : "ハイライトの説明",
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
      "name" : "クイック返信名",
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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
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
    "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する場合があります。また、チェックインができない場合、予約がキャンセルされることがあります。\\n* お問い合わせ電話: 1234-1234",
    "templateTitle" : "123,450円",
    "templateSubtitle" : "承認履歴",
    "templateHeader" : "注文が確定しました。",
    "templateItem" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "description" : "アイテムの説明"
      } ],
      "summary" : {
        "title" : "サマリータイトル",
        "description" : "サマリーの説明"
      }
    },
    "templateItemHighlight" : {
      "title" : "ハイライトタイトル",
      "description" : "ハイライトの説明",
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
      "name" : "クイック返信名",
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

<a id="list-alimtalk-templates"></a>

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
| content.templateEmphasizeType | String | O | テンプレート強調表示のタイプ<br>[NONE(強調なし)、TEXT(テキスト強調)、IMAGE(画像強調)、ITEM_LIST(アイテムリスト強調)] |
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
| content.buttons[].type | String | O | テンプレートボタンのタイプ<br>[WL(Webリンク)、AL(アプリリンク)、DS(配送追跡)、BK(ボットキーワード)、MD(メッセージ転送)、BC(相談トークに切り替え)、BT(ボットに切り替え)、AC(チャンネル追加)、BF(ビジネスフォーム)、P1(画像セキュア送信プラグイン)、P2(個人情報利用プラグイン)、P3(ワンクリック決済プラグイン)、TN(電話をかける)] |
| content.buttons[].name | String | N | テンプレートボタン名 |
| content.buttons[].linkMo | String | N | テンプレートボタン モバイルWebリンク |
| content.buttons[].linkPc | String | N | テンプレートボタンPC Webリンク |
| content.buttons[].schemeIos | String | N | テンプレートボタンiOSアプリリンク |
| content.buttons[].schemeAndroid | String | N | テンプレートボタンAndroidアプリリンク |
| content.buttons[].bizFormId | Integer | N | テンプレートボタン ビジネスフォームID(BFタイプの場合は必須) |
| content.quickReplies | Array | N | テンプレートダイレクトリンク |
| content.quickReplies[].ordering | Integer | N | テンプレートダイレクトリンク順序 |
| content.quickReplies[].type | String | O | テンプレートのクイックリプライのタイプ<br>[WL(Webリンク)、AL(アプリリンク)、BK(ボットキーワード)、BC(相談トークに切り替え)、BT(ボットに切り替え)、BF(ビジネスフォーム)] |
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

<a id="list-templates-by-alimtalk-sender"></a>

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

<a id="get-alimtalk-template-details"></a>

## お知らせトークテンプレート詳細照会

テンプレートを詳細照会します。

**リクエスト**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| templateId | Path | String | O | テンプレートID |

**リクエスト本文**

<!--このAPIはリクエスト本文を要求しません。-->

このAPIはリクエスト本文を要求しません。

**レスポンス本文**

<!--レスポンス本文を返さない場合は「このAPIはレスポンス本文を返しません」と入力します。-->

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
      "kakaoTemplateCode" : "templateCode",
      "templateCode" : "templateCode",
      "comments" : [ {
        "id" : 1,
        "content" : "問い合わせ内容の例",
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
      "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをKakaoTalkで受け取る",
      "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する場合があり、チェックインができない場合は予約がキャンセルされることがあります。\\n* お問い合わせ電話番号: 1234-1234",
      "templateTitle" : "123,450円",
      "templateSubtitle" : "承認履歴",
      "templateHeader" : "注文が確定しました。",
      "templateItem" : {
        "list" : [ {
          "title" : "アイテムタイトル",
          "description" : "アイテムの説明"
        } ],
        "summary" : {
          "title" : "サマリータイトル",
          "description" : "サマリーの説明"
        }
      },
      "templateItemHighlight" : {
        "title" : "ハイライトタイトル",
        "description" : "ハイライトの説明",
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
        "name" : "クイックリプライ名",
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

<!--レスポンス本文のフィールドについて説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| template | Object | O |  |
| template.templateId | String | O | テンプレート登録時に発行されたテンプレートID |
| template.templateName | String | O | テンプレート名 |
| template.categoryId | String | O | カテゴリーID |
| template.messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| template.messagePurpose | String | O | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| template.messagePurposes | Array | O |  |
| template.templateLanguage | String | O | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト), FREEMARKER(FreeMarker テンプレート)] |
| template.sender | Object | O |  |
| template.sender.senderKey | String | O | 発信プロフィールの発信キー |
| template.sender.senderProfileId | String | O | KakaoTalkチャンネル名 |
| template.sender.senderProfileType | String | O | 発信プロフィールタイプ<br>[GROUP, NORMAL] |
| template.additionalProperty | Object | O |  |
| template.additionalProperty.kakaoTemplateCode | String | O | Kakaoテンプレートコード |
| template.additionalProperty.templateCode | String | O | テンプレートコード(英字、数字、-、_) |
| template.additionalProperty.comments | Array | O | テンプレート問い合わせリスト |
| template.additionalProperty.comments[].id | Integer | O | 問い合わせID |
| template.additionalProperty.comments[].content | String | X | 問い合わせ内容 |
| template.additionalProperty.comments[].userName | String | O | 作成者 |
| template.additionalProperty.comments[].createdAt | String | O | 問い合わせ作成日時 |
| template.additionalProperty.comments[].attachments | Array | O | 問い合わせ添付ファイル |
| template.additionalProperty.comments[].attachments[].originalFileName | String | O | 添付ファイル名 |
| template.additionalProperty.comments[].attachments[].filePath | String | O | 添付ファイルパス |
| template.additionalProperty.comments[].status | String | O | 問い合わせステータス(REQ: リクエスト、INQ: 問い合わせ、APR: 承認、REJ: 差し戻し、REP: 回答)<br>[REQ, INQ, APR, REJ, REP] |
| template.additionalProperty.status | String | X | REGISTERED: リクエスト、REQUESTED: 審査中、APPROVED: 承認、REJECTED: 差し戻し<br>[REGISTERED, REQUESTED, APPROVED, REJECTED] |
| template.additionalProperty.block | Boolean | O | テンプレートブロック有無<br>デフォルト値: false |
| template.additionalProperty.dormant | Boolean | O | テンプレート休眠有無<br>デフォルト値: false |
| template.content | Object | O |  |
| template.content.templateMessageType | String | X | テンプレートメッセージタイプ(BA: 基本型、EX: 付加情報型、AD: チャンネル追加型、MI: 複合型、default: BA) |
| template.content.templateEmphasizeType | String | O | テンプレート強調表示タイプ<br>[NONE(強調なし), TEXT(テキスト強調), IMAGE(イメージ強調), ITEM_LIST(アイテムリスト強調)] |
| template.content.templateContent | String | X | テンプレート本文 |
| template.content.templateAd | String | X | チャンネル追加案内メッセージ(テンプレートメッセージタイプがチャンネル追加型・複合型の場合は固定値) |
| template.content.templateExtra | String | X | テンプレート付加情報(テンプレートメッセージタイプが[付加情報型/複合型]の場合は必須)、置換変数使用不可、URL含めることができます |
| template.content.templateTitle | String | X | テンプレートタイトル(最大50文字、Android: 2行、23文字以上は省略表示、iOS: 2行、27文字以上は省略表示) |
| template.content.templateSubtitle | String | X | テンプレートサブ文言(最大50文字、Android: 18文字以上は省略表示、iOS: 21文字以上は省略表示) |
| template.content.templateHeader | String | X | テンプレートヘッダー、変数入力可能 |
| template.content.templateItem | Object | X |  |
| template.content.templateItem.list | Array | O |  |
| template.content.templateItem.list[].title | String | O | アイテムタイトル |
| template.content.templateItem.list[].description | String | O | アイテム説明 |
| template.content.templateItem.summary | Object | X |  |
| template.content.templateItem.summary.title | String | O | サマリータイトル |
| template.content.templateItem.summary.description | String | O | サマリー説明(変数および通貨単位、数字、カンマ、ピリオドのみ使用可能) |
| template.content.templateItemHighlight | Object | X |  |
| template.content.templateItemHighlight.title | String | O | アイテムハイライトタイトル(最大30文字、サムネイル画像がある場合は21文字) |
| template.content.templateItemHighlight.description | String | O | アイテムハイライト説明(最大19文字、サムネイル画像がある場合は13文字) |
| template.content.templateItemHighlight.attachmentId | String | X | テンプレート添付ファイルID |
| template.content.templateItemHighlight.imageUrl | String | X | サムネイル画像アドレス |
| template.content.templateRepresentLink | Object | X |  |
| template.content.templateRepresentLink.linkMo | String | X | 代表リンクモバイルWebリンク |
| template.content.templateRepresentLink.linkPc | String | X | 代表リンクPC Webリンク |
| template.content.templateRepresentLink.schemeIos | String | X | 代表リンクiOSアプリリンク |
| template.content.templateRepresentLink.schemeAndroid | String | X | 代表リンクAndroidアプリリンク |
| template.content.attachmentId | String | X | テンプレート添付ファイルID |
| template.content.templateImageName | String | X | テンプレート画像名 |
| template.content.templateImageUrl | String | X | テンプレート画像リンク |
| template.content.securityFlag | Boolean | X | テンプレートセキュリティ有無(default: false) |
| template.content.categoryCode | String | X | テンプレートカテゴリーコード(テンプレートカテゴリー照会 API 参照、default: 999999) |
| template.content.buttons | Array | X | テンプレートボタン |
| template.content.buttons[].ordering | Integer | O | テンプレートボタン順序 |
| template.content.buttons[].type | String | O | テンプレートボタンタイプ<br>[WL(Webリンク), AL(アプリリンク), DS(配送照会), BK(ボットキーワード), MD(メッセージ転達), BC(相談トーク切替), BT(ボット切替), AC(チャンネル追加), BF(ビジネスフォーム), P1(画像セキュリティ転送プラグイン), P2(個人情報利用プラグイン), P3(ワンクリック決済プラグイン), TN(電話をかける)] |
| template.content.buttons[].name | String | O | テンプレートボタン名 |
| template.content.buttons[].linkMo | String | X | テンプレートボタンモバイルWebリンク |
| template.content.buttons[].linkPc | String | X | テンプレートボタンPC Webリンク |
| template.content.buttons[].schemeIos | String | X | テンプレートボタンiOSアプリリンク |
| template.content.buttons[].schemeAndroid | String | X | テンプレートボタンAndroidアプリリンク |
| template.content.buttons[].bizFormId | Integer | X | テンプレートボタンビジネスフォームID(BFタイプの場合は必須) |
| template.content.quickReplies | Array | X | テンプレートクイックリプライ |
| template.content.quickReplies[].ordering | Integer | O | テンプレートクイックリプライ順序 |
| template.content.quickReplies[].type | String | O | テンプレートクイックリプライタイプ<br>[WL(Webリンク), AL(アプリリンク), BK(ボットキーワード), BC(相談トーク切替), BT(ボット切替), BF(ビジネスフォーム)] |
| template.content.quickReplies[].name | String | O | テンプレートクイックリプライ名 |
| template.content.quickReplies[].linkMo | String | X | テンプレートクイックリプライモバイルWebリンク |
| template.content.quickReplies[].linkPc | String | X | テンプレートクイックリプライPC Webリンク |
| template.content.quickReplies[].schemeIos | String | X | テンプレートクイックリプライiOSアプリリンク |
| template.content.quickReplies[].schemeAndroid | String | X | テンプレートクイックリプライAndroidアプリリンク |
| template.content.quickReplies[].bizFormId | Integer | X | テンプレートクイックリプライビジネスフォームID(BFタイプの場合は必須) |
| template.createdDateTime | String | O | テンプレート作成日時 |
| template.updatedDateTime | String | O | テンプレート更新日時 |

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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0010UpdateAlimtalkTemplate"></span>

<a id="update-alimtalk-template"></a>

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

<a id="delete-alimtalk-template"></a>

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

<a id="submit-an-alimtalk-template-inquiry---deprecated"></a>

## お知らせトークのカカオテンプレート一覧照会

お知らせトークのカカオテンプレート一覧を照会します。

**リクエスト**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | アプリキー |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| templateId | Path | String | Y | テンプレートID |
| limit | Query | Integer | N | limitを設定しない場合はデフォルト20(最大1000) |
| offset | Query | Integer | N | offsetを設定しない場合はデフォルト0 |



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



**リクエスト例**


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

<a id="submit-an-alimtalk-template-inquiry-with-file-attachment---deprecated"></a>

## ファイルを添付してカカオお知らせトークテンプレートを問い合わせる

カカオお知らせトークテンプレートを問い合わせる際、ファイルを添付して問い合わせます。

**リクエスト**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates/{kakaoTemplateCode}/inquiries/do-with-file
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | アプリキー |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| templateId | Path | String | Y | テンプレートID |
| kakaoTemplateCode | Path | String | Y | カカオテンプレートコード |

**リクエストボディ**

<!--リクエストボディを必要としない場合は「このAPIはリクエストボディを必要としません」と入力します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| comment | String | Y | お問い合わせ内容 |
| file | Binary | Y | 問い合わせファイル |

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

<a id="list-alimtalk-template-updates"></a>

## カカオお知らせトークテンプレート問い合わせ

カカオお知らせトークテンプレートについて問い合わせます。

**リクエスト**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates/{kakaoTemplateCode}/inquiries
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | アプリキー |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| templateId | Path | String | Y | テンプレートID |
| kakaoTemplateCode | Path | String | Y | カカオテンプレートコード |



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

<a id="list-alimtalk-template-categories"></a>

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

<a id="register-email-template"></a>

## Email テンプレート登録

テンプレートを登録します。

**リクエスト**

```
POST /template/v1.0/EMAIL/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は「この API はリクエスト本文を必要としません」と入力します。-->


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
    "body" : "こんにちは。本日、お客様のご注文商品が入荷いたしました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | O | テンプレート名 |
| categoryId | String | X | カテゴリー ID |
| messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般)、AD(広告)、AUTH(認証)] |
| templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarker テンプレート)] |
| sender | Object | O |  |
| sender.senderMailAddress | String | O | 送信元メールアドレス |
| content | Object | O |  |
| content.title | String | X | テンプレートメールの件名 |
| content.body | String | X | テンプレートメールの本文 |
| content.attachmentIds | Array | X | テンプレート添付ファイル ID |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| templateId | String | O | テンプレート登録時に発行されたテンプレート ID |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Email テンプレート登録

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
    "body" : "こんにちは。本日、お客様のご注文商品が入荷いたしました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/EMAIL/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
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
    "body" : "こんにちは。本日、お客様のご注文商品が入荷いたしました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>

<span id="templateV1x0022ReadEmailTemplate"></span>

<a id="get-email-template-details"></a>

## Email テンプレート詳細照会

テンプレートを詳細照会します。

**リクエスト**

```
GET /template/v1.0/EMAIL/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| templateId | Path | String | O | テンプレートID |



**リクエスト本文**

<!-- このAPIはリクエスト本文を必要としません。-->

このAPIはリクエスト本文を必要としません。



**レスポンス本文**

<!-- このAPIはレスポンス本文を返します。-->

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
      "body" : "こんにちは。本日、お客様の商品が入荷されました。",
      "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | X |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| template | Object | X |  |
| template.templateId | String | O | テンプレート登録時に発行されたテンプレートID |
| template.templateName | String | X | テンプレート名 |
| template.categoryId | String | X | カテゴリーID |
| template.messageChannel | String | X | メッセージチャンネル<br>[SMS(SMS)、ALIMTALK(お知らせトーク)、EMAIL(メール)、RCS(RCS)、PUSH(プッシュ)] |
| template.messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般)、AD(広告)、AUTH(認証)] |
| template.messagePurposes | Array | X |  |
| template.templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarkerテンプレート)] |
| template.sender | Object | X |  |
| template.sender.senderMailAddress | String | O | 送信元メールアドレス |
| template.content | Object | X |  |
| template.content.title | String | X | テンプレートメールの件名 |
| template.content.body | String | X | テンプレートメールの本文 |
| template.content.attachmentIds | Array | X | テンプレート添付ファイルID |
| template.createdDateTime | String | X | テンプレート作成日時 |
| template.updatedDateTime | String | X | テンプレート更新日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Email テンプレート詳細照会

GET {{endpoint}}/template/v1.0/EMAIL/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/EMAIL/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0022ReadEmailTemplateList"></span>

<a id="list-email-templates"></a>

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

<a id="update-email-template"></a>

## Email テンプレート修正

テンプレートを修正します。

**リクエスト**

```
PUT /template/v1.0/EMAIL/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| templateId | Path | String | O | テンプレート ID |



**リクエスト本文**

<!--リクエスト本文を要求しない場合は「この API はリクエスト本文を要求しません」と入力します。-->


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
    "body" : "こんにちは。本日、お客様の商品が入荷されました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | O | テンプレート名 |
| messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般)、AD(広告)、AUTH(認証)] |
| templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarker テンプレート)] |
| sender | Object | O |  |
| sender.senderMailAddress | String | O | 送信元メールアドレス |
| content | Object | O |  |
| content.title | String | X | テンプレートメール件名 |
| content.body | String | X | テンプレートメール本文 |
| content.attachmentIds | Array | X | テンプレート添付ファイル ID |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Email テンプレート修正

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
    "body" : "こんにちは。本日、お客様の商品が入荷されました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/EMAIL/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "templateLanguage" : "PLAIN_TEXT",
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "content" : {
    "title" : "[NHN Cloud Email][##env##] モニタリング通知",
    "body" : "こんにちは。本日、お客様の商品が入荷されました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>

<span id="templateV1x0024DeleteEmailTemplate"></span>

<a id="delete-email-template"></a>

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

<a id="register-rcs-template"></a>

## RCS テンプレート登録

テンプレートを登録します。

**リクエスト**

```
POST /template/v1.0/RCS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |



**リクエスト本文**

<!--リクエスト本文が不要な場合は「この API はリクエスト本文を必要としません」と入力します。-->


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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、ご注文の商品が入荷しました。ぜひご来店ください^^",
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
      "title1" : "タイトル 1",
      "title2" : "タイトル 2",
      "title3" : "タイトル 3",
      "description1" : "本文 1",
      "description2" : "本文 2",
      "description3" : "本文 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定のタイトル",
                "description" : "予定の説明"
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
              "title" : "予定のタイトル",
              "description" : "予定の説明"
            }
          }
        }
      }
    } ]
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | O | テンプレート名 |
| categoryId | String | X | カテゴリー ID |
| messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト), FREEMARKER(FreeMarker テンプレート)] |
| sender | Object | O |  |
| sender.brandId | String | O | ブランド ID |
| sender.chatbotId | String | O | トークルーム（チャットボット）ID |
| content | Object | O |  |
| content.messageType | String | X | RCS 送信メッセージタイプ<br>[SMS(短文メッセージ), LMS(長文メッセージ), MMS(マルチメディアメッセージ), RBC_TEMPLATE(RCS Biz Center テンプレート)] |
| content.title | String | X | (Deprecated、content.cards[].title を使用) メッセージタイトル |
| content.body | String | X | (Deprecated、content.cards[].description を使用) メッセージ本文 |
| content.smsType | String | X | SMS タイプ<br>[STANDALONE(独立型), UNIFIED_STANDALONE(統合独立型)] |
| content.lmsType | String | X | LMS タイプ<br>[STANDALONE(独立型), FORMAT_BASIC(基本形式), FORMAT_TITLE_HIGHLIGHT(タイトル強調形式), FORMAT_PARAGRAPH(段落形式), UNIFIED_STANDALONE(統合独立型)] |
| content.mmsType | String | X | MMS タイプ（MMS 送信時は必須）<br>[HORIZONTAL(横型), VERTICAL(縦型), CAROUSEL_MEDIUM(カルーセル中型), CAROUSEL_SMALL(カルーセル小型), UNIFIED_HORIZONTAL(統合横型), UNIFIED_VERTICAL(統合縦型)] |
| content.messagebaseId | String | X | RCS Biz Center テンプレート ID |
| content.unsubscribePhoneNumber | String | X | 受信拒否番号（広告送信時は必須） |
| content.cards | Array | X | RCS カード |
| content.cards[].title | String | X | タイトル |
| content.cards[].description | String | X | 本文 |
| content.cards[].attachmentId | String | X | 添付ファイル ID<br>※ 統合 MMS カードに GIF 画像を添付した場合、iOS デバイスでは受信できません。 |
| content.cards[].mTitle | String | X | メインタイトル |
| content.cards[].mTitleMedia | String | X | メインタイトルロゴファイル ID |
| content.cards[].title1 | String | X | タイトル 1 |
| content.cards[].title2 | String | X | タイトル 2 |
| content.cards[].title3 | String | X | タイトル 3 |
| content.cards[].description1 | String | X | 本文 1 |
| content.cards[].description2 | String | X | 本文 2 |
| content.cards[].description3 | String | X | 本文 3 |
| content.cards[].buttons | Array | X | RCS ボタンリスト |
| content.cards[].buttons[].buttonType | String | X | COMPOSE(トークルームを開く), CLIPBOARD(コピーする), DIALER(電話をかける), MAP_SHOW(地図を表示する), MAP_QUERY(地図を検索する), MAP_SHARE(現在地を共有する), URL(URL に接続する), CALENDAR(予定を登録する)<br>※ 統合メッセージタイプに CLIPBOARD(コピーする) ボタンを使用すると、iOS デバイスでは受信できません。<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.cards[].buttons[].buttonJson | Object | X |  |
| content.cards[].buttons[].buttonJson.action | Object | X | ボタンアクション |
| content.buttons | Array | X | (Deprecated、content.cards[].buttons を使用) RCS ボタンリスト |
| content.buttons[].buttonType | String | X | COMPOSE(トークルームを開く), CLIPBOARD(コピーする), DIALER(電話をかける), MAP_SHOW(地図を表示する), MAP_QUERY(地図を検索する), MAP_SHARE(現在地を共有する), URL(URL に接続する), CALENDAR(予定を登録する)<br>※ 統合メッセージタイプに CLIPBOARD(コピーする) ボタンを使用すると、iOS デバイスでは受信できません。<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | X |  |
| content.buttons[].buttonJson.action | Object | X | ボタンアクション |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| templateId | String | O | テンプレート登録時に発行されたテンプレート ID |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http

### RCS テンプレート登録

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
    "body" : "こんにちは。本日、お客様の商品が入荷されました。ぜひご来店ください^^",
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
      "title1" : "タイトル 1",
      "title2" : "タイトル 2",
      "title3" : "タイトル 3",
      "description1" : "本文 1",
      "description2" : "本文 2",
      "description3" : "本文 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定のタイトル",
                "description" : "予定の説明"
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
              "title" : "予定のタイトル",
              "description" : "予定の説明"
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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
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
    "body" : "こんにちは。本日、お客様の商品が入荷されました。ぜひご来店ください^^",
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
      "title1" : "タイトル 1",
      "title2" : "タイトル 2",
      "title3" : "タイトル 3",
      "description1" : "本文 1",
      "description2" : "本文 2",
      "description3" : "本文 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定のタイトル",
                "description" : "予定の説明"
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
              "title" : "予定のタイトル",
              "description" : "予定の説明"
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

<a id="list-rcs-templates"></a>

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

<a id="get-rcs-template-details"></a>

## RCS テンプレート詳細照会

テンプレートを詳細照会します。

**リクエスト**

```
GET /template/v1.0/RCS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| templateId | Path | String | O | テンプレート ID |

**リクエスト本文**

<!--リクエスト本文を必要としない場合は「この API はリクエスト本文を必要としません」と入力します。-->

この API はリクエスト本文を必要としません。

**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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
      "title" : "祝日営業時間のお知らせ",
      "body" : "こんにちは。本日、お客様の商品が入荷いたしました。ぜひご来店ください^^",
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
        "title1" : "タイトル 1",
        "title2" : "タイトル 2",
        "title3" : "タイトル 3",
        "description1" : "本文 1",
        "description2" : "本文 2",
        "description3" : "本文 3",
        "buttons" : [ {
          "buttonType" : "CALENDAR",
          "buttonJson" : {
            "action" : {
              "displayText" : "予定を登録する",
              "calendarAction" : {
                "createCalendarEvent" : {
                  "startTime" : "2024-01-01T00:00:00.000+09:00",
                  "endTime" : "2024-01-01T00:00:00.000+09:00",
                  "title" : "予定のタイトル",
                  "description" : "予定の説明"
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
                "title" : "予定のタイトル",
                "description" : "予定の説明"
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

<!--レスポンス本文のフィールドについて説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | X |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| template | Object | X |  |
| template.templateId | String | O | テンプレート登録時に発行されたテンプレート ID |
| template.templateName | String | X | テンプレート名 |
| template.categoryId | String | X | カテゴリー ID |
| template.messageChannel | String | X | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| template.messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| template.messagePurposes | Array | X |  |
| template.templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト), FREEMARKER(FreeMarker テンプレート)] |
| template.sender | Object | X |  |
| template.sender.brandId | String | O | ブランド ID |
| template.sender.chatbotId | String | O | トークルーム(チャットボット) ID |
| template.content | Object | X |  |
| template.content.messageType | String | X | RCS 送信メッセージタイプ<br>[SMS(短文メッセージ), LMS(長文メッセージ), MMS(マルチメディアメッセージ), RBC_TEMPLATE(RCS Biz Center テンプレート)] |
| template.content.title | String | X | メッセージタイトル |
| template.content.body | String | X | メッセージ本文 |
| template.content.smsType | String | X | SMS タイプ<br>[STANDALONE(独立型), UNIFIED_STANDALONE(統合独立型)] |
| template.content.lmsType | String | X | LMS タイプ<br>[STANDALONE(独立型), FORMAT_BASIC(基本形式), FORMAT_TITLE_HIGHLIGHT(タイトル強調形式), FORMAT_PARAGRAPH(段落形式), UNIFIED_STANDALONE(統合独立型)] |
| template.content.mmsType | String | X | MMS タイプ(MMS 送信の場合は必須)<br>[HORIZONTAL(横型), VERTICAL(縦型), CAROUSEL_MEDIUM(カルーセル中型), CAROUSEL_SMALL(カルーセル小型), UNIFIED_HORIZONTAL(統合横型), UNIFIED_VERTICAL(統合縦型)] |
| template.content.messagebaseId | String | X | RCS Biz Center テンプレート ID |
| template.content.messagebaseformId | String | X | RCS Biz Center で指定した messageBase 形式<br>- SS000000(SMS 基本型)<br>- SL000000(LMS 基本型)<br>- OL00000001(LMS Format 基本型)<br>- OL00000002(LMS Format タイトル強調型)<br>- OL00000003(LMS Format 段落型)<br>- SMwThT00(MMS 縦型)<br>- SMwThM00(MMS 横型)<br>- CMwMhM0200(MMS スライド中型(2))<br>- CMwMhM0300(MMS スライド中型(3))<br>- CMwMhM0400(MMS スライド中型(4))<br>- CMwMhM0500(MMS スライド中型(5))<br>- CMwMhM0600(MMS スライド中型(6))<br>- CMwShS0200(MMS スライド小型(2))<br>- CMwShS0300(MMS スライド小型(3))<br>- CMwShS0400(MMS スライド小型(4))<br>- CMwShS0500(MMS スライド小型(5))<br>- CMwShS0600(MMS スライド小型(6))<br>- CLI00001(アイテム詳細型)<br>- CLI00002(イメージ強調型 (1:1))<br>- CLI00003(イメージ強調型 (3:4))<br>- CLI00004(イメージ & タイトル強調型 (1:1))<br>- CLI00005(イメージ & タイトル強調型 (3:4))<br>- CLI00006(サムネイル型 (横))<br>- CLI00007(サムネイル型 (縦))<br>- CLI00008(SNS 型 (下部ボタン))<br>- CLI00009(SNS 型 (中間ボタン))<br>- ITTBNV(サムネイル型(縦))<br>- ITTBNH(サムネイル型(横))<br>- ITHIMS(イメージ強調型(1:1))<br>- ITHIMV(イメージ強調型(3:4))<br>- ITSNSS(SNS 型)<br>- ITSNSH(SNS 型(中間ボタン))<br>- ITHITS(イメージ & タイトル強調型(1:1))<br>- ITHITV(イメージ & タイトル強調型(3:4))<br>- ITCRM2(スライド型(2))<br>- ITCRM3(スライド型(3))<br>- ITCRM4(スライド型(4))<br>- ITCRM5(スライド型(5))<br>- ITCRM6(スライド型(6))<br>- CLT00001(アイテム強調型 DESC)<br>- CLT00002(アイテム強調型 TABLE)<br>- TATA001F(タイトル自由型 FREE)<br>- TATA001C(タイトル自由型 CELL)<br>- TATA001D(タイトル自由型 DESC)<br>- GG000F(タイトル選択型 FREE)<br>- FF005C(明細書 CELL)<br>- FF005D(明細書 DESC)<br>- FF004C(キャンセル CELL)<br>- FF004D(キャンセル DESC)<br>- GG003C(案内 CELL)<br>- GG003D(案内 DESC)<br>- GG002C(認証 CELL)<br>- GG002D(認証 DESC)<br>- GG001C(会員登録 CELL)<br>- GG001D(会員登録 DESC)<br>- EE001C(予約 CELL)<br>- EE001D(予約 DESC)<br>- CC003C(配送 CELL)<br>- CC003D(配送 DESC)<br>- FF002C(入金 CELL)<br>- FF002D(入金 DESC)<br>- FF001C(承認 CELL)<br>- FF001D(承認 DESC)<br>- CC002C(注文 CELL)<br>- CC002D(注文 DESC)<br>- CC001C(出荷 CELL)<br>- CC001D(出荷 DESC)<br>- FF003C(出金 CELL)<br>- FF003D(出金 DESC)<br>- CLL00001(LMS 明細書 A)<br>- CLL00002(LMS 段落型)<br>- CLL00003(LMS タイトル強調型)<br>- CLL00004(LMS 基本型)<br>- CLL00005(LMS 明細書 B)<br>- CLL00006(LMS 明細書 C)<br>- RPSSAXX001(統合 SMS カード)<br>- RPLSAXX001(統合 LMS カード)<br>- RPMSMMX001(統合 MMS カード M)<br>- RPMSMTX001(統合 MMS カード T)<br>- RPISMMX001(統合イメージテンプレート M)<br>- RPISMTX001(統合イメージテンプレート T)<br>- RPTDXXX001(統合情報性テンプレート)<br>- RPTFXXX001(統合フリーテンプレート)<br><br>[SS000000, SL000000, OL00000001, OL00000002, OL00000003, SMwThT00, SMwThM00, CMwMhM0200, CMwMhM0300, CMwMhM0400, CMwMhM0500, CMwMhM0600, CMwShS0200, CMwShS0300, CMwShS0400, CMwShS0500, CMwShS0600, CLI00001, CLI00002, CLI00003, CLI00004, CLI00005, CLI00006, CLI00007, CLI00008, CLI00009, ITTBNV, ITTBNH, ITHIMS, ITHIMV, ITSNSS, ITSNSH, ITHITS, ITHITV, ITCRM2, ITCRM3, ITCRM4, ITCRM5, ITCRM6, CLT00001, CLT00002, TATA001C, TATA001D, TATA001F, FF005C, FF005D, FF004C, FF004D, GG003C, GG003D, GG002C, GG002D, GG001C, GG001D, GG000F, EE001C, EE001D, CC003C, CC003D, FF002C, FF002D, FF001C, FF001D, CC002C, CC002D, CC001C, CC001D, FF003C, FF003D, CLL00001, CLL00002, CLL00003, CLL00004, CLL00005, CLL00006, RPSSAXX001, RPLSAXX001, RPMSMMX001, RPMSMTX001, RPISMMX001, RPISMTX001, RPTDXXX001, RPTFXXX001] |
| template.content.unsubscribePhoneNumber | String | X | 受信拒否番号(広告送信の場合は必須) |
| template.content.cards | Array | X | RCS カード |
| template.content.cards[].title | String | X | タイトル |
| template.content.cards[].description | String | X | 本文 |
| template.content.cards[].attachmentId | String | X | 添付ファイル ID<br>※ 統合 MMS カードで GIF 画像を添付すると、iOS 端末では受信できません。 |
| template.content.cards[].mTitle | String | X | メインタイトル |
| template.content.cards[].mTitleMedia | String | X | メインタイトルロゴファイル ID |
| template.content.cards[].title1 | String | X | タイトル 1 |
| template.content.cards[].title2 | String | X | タイトル 2 |
| template.content.cards[].title3 | String | X | タイトル 3 |
| template.content.cards[].description1 | String | X | 本文 1 |
| template.content.cards[].description2 | String | X | 本文 2 |
| template.content.cards[].description3 | String | X | 本文 3 |
| template.content.cards[].buttons | Array | X | RCS ボタンリスト |
| template.content.cards[].buttons[].buttonType | String | X | COMPOSE(トークルームを開く), CLIPBOARD(コピーする), DIALER(電話をかける), MAP_SHOW(地図を表示する), MAP_QUERY(地図を検索する), MAP_SHARE(現在地を共有する), URL(URL を開く), CALENDAR(予定を登録する)<br>※ 統合メッセージタイプで CLIPBOARD(コピーする) ボタンを使用すると、iOS 端末では受信できません。<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| template.content.cards[].buttons[].buttonJson | Object | X |  |
| template.content.cards[].buttons[].buttonJson.action | Object | X | ボタンアクション |
| template.content.buttons | Array | X | RCS ボタンリスト |
| template.content.buttons[].buttonType | String | X | COMPOSE(トークルームを開く), CLIPBOARD(コピーする), DIALER(電話をかける), MAP_SHOW(地図を表示する), MAP_QUERY(地図を検索する), MAP_SHARE(現在地を共有する), URL(URL を開く), CALENDAR(予定を登録する)<br>※ 統合メッセージタイプで CLIPBOARD(コピーする) ボタンを使用すると、iOS 端末では受信できません。<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| template.content.buttons[].buttonJson | Object | X |  |
| template.content.buttons[].buttonJson.action | Object | X | ボタンアクション |
| template.additionalProperty | Object | X |  |
| template.additionalProperty.status | String | X | テンプレートステータス<br>- SAVE: 保存<br>- APPROVE_WAIT: 承認待機<br>- INSPECTION_START: 審査開始<br>- INSPECTION_FINISH: 審査完了<br>- APPROVE: 承認<br>- REJECT: 拒否<br>- MODIFY_APPROVE_WAIT: 修正承認待機<br>- MODIFY_INSPECTION_START: 修正審査開始<br>- MODIFY_INSPECTION_FINISH: 修正審査完了<br>- MODIFY_REJECT: 修正拒否<br><br>[SAVE, APPROVE_WAIT, INSPECTION_START, INSPECTION_FINISH, APPROVE, REJECT, MODIFY_APPROVE_WAIT, MODIFY_INSPECTION_START, MODIFY_INSPECTION_FINISH, MODIFY_REJECT] |
| template.additionalProperty.approvedDateTime | String | X | テンプレート承認日時 |
| template.createdDateTime | String | X | テンプレート作成日時 |
| template.updatedDateTime | String | X | テンプレート更新日時 |

**リクエスト例**

<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http

### RCS テンプレート詳細照会

GET {{endpoint}}/template/v1.0/RCS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/RCS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0028UpdateRcsTemplate"></span>

<a id="update-rcs-template"></a>

## RCS テンプレート修正

テンプレートを修正します。

**リクエスト**

```
PUT /template/v1.0/RCS/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| templateId | Path | String | O | テンプレートID |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は「この API はリクエスト本文を必要としません」と入力します。-->


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
    "title" : "連休営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様の商品が入荷されました。ぜひご来店ください^^",
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
      "title1" : "タイトル 1",
      "title2" : "タイトル 2",
      "title3" : "タイトル 3",
      "description1" : "本文 1",
      "description2" : "本文 2",
      "description3" : "本文 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "スケジュールを登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "スケジュールのタイトル",
                "description" : "スケジュールの説明"
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
          "displayText" : "スケジュールを登録する",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "スケジュールのタイトル",
              "description" : "スケジュールの説明"
            }
          }
        }
      }
    } ]
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | O | テンプレート名 |
| messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト), FREEMARKER(FreeMarker テンプレート)] |
| sender | Object | X |  |
| sender.brandId | String | O | ブランドID |
| sender.chatbotId | String | O | チャットルーム(チャットボット)ID |
| content | Object | O |  |
| content.messageType | String | X | RCS 送信メッセージタイプ<br>[SMS(短文メッセージ), LMS(長文メッセージ), MMS(マルチメディアメッセージ), RBC_TEMPLATE(RCS Biz Center テンプレート)] |
| content.title | String | X | (Deprecated、content.cards[].title を使用) メッセージタイトル |
| content.body | String | X | (Deprecated、content.cards[].description を使用) メッセージ本文 |
| content.smsType | String | X | SMS タイプ<br>[STANDALONE(スタンドアロン), UNIFIED_STANDALONE(統合スタンドアロン)] |
| content.lmsType | String | X | LMS タイプ<br>[STANDALONE(スタンドアロン), FORMAT_BASIC(基本形式), FORMAT_TITLE_HIGHLIGHT(タイトル強調形式), FORMAT_PARAGRAPH(段落形式), UNIFIED_STANDALONE(統合スタンドアロン)] |
| content.mmsType | String | X | MMS タイプ(MMS 送信の場合は必須)<br>[HORIZONTAL(横型), VERTICAL(縦型), CAROUSEL_MEDIUM(カルーセル中間型), CAROUSEL_SMALL(カルーセル小型), UNIFIED_HORIZONTAL(統合横型), UNIFIED_VERTICAL(統合縦型)] |
| content.messagebaseId | String | X | RCS Biz Center テンプレートID |
| content.unsubscribePhoneNumber | String | X | 受信拒否番号(広告送信の場合は必須) |
| content.cards | Array | X | RCS カード |
| content.cards[].title | String | X | タイトル |
| content.cards[].description | String | X | 本文 |
| content.cards[].attachmentId | String | X | 添付ファイルID<br>※ 統合 MMS カードに GIF 画像を添付すると、iOS 端末では受信できません。 |
| content.cards[].mTitle | String | X | メインタイトル |
| content.cards[].mTitleMedia | String | X | メインタイトルロゴファイル ID |
| content.cards[].title1 | String | X | タイトル 1 |
| content.cards[].title2 | String | X | タイトル 2 |
| content.cards[].title3 | String | X | タイトル 3 |
| content.cards[].description1 | String | X | 本文 1 |
| content.cards[].description2 | String | X | 本文 2 |
| content.cards[].description3 | String | X | 本文 3 |
| content.cards[].buttons | Array | X | RCS ボタンリスト |
| content.cards[].buttons[].buttonType | String | X | COMPOSE(チャットルームを開く), CLIPBOARD(コピーする), DIALER(電話をかける), MAP_SHOW(地図を表示する), MAP_QUERY(地図を検索する), MAP_SHARE(現在地を共有する), URL(URL に接続する), CALENDAR(スケジュールを登録する)<br>※ 統合メッセージタイプに CLIPBOARD(コピーする) ボタンを使用すると、iOS 端末では受信できません。<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.cards[].buttons[].buttonJson | Object | X |  |
| content.cards[].buttons[].buttonJson.action | Object | X | ボタンアクション |
| content.buttons | Array | X | (Deprecated、content.cards[].buttons を使用) RCS ボタンリスト |
| content.buttons[].buttonType | String | X | COMPOSE(チャットルームを開く), CLIPBOARD(コピーする), DIALER(電話をかける), MAP_SHOW(地図を表示する), MAP_QUERY(地図を検索する), MAP_SHARE(現在地を共有する), URL(URL に接続する), CALENDAR(スケジュールを登録する)<br>※ 統合メッセージタイプに CLIPBOARD(コピーする) ボタンを使用すると、iOS 端末では受信できません。<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | X |  |
| content.buttons[].buttonJson.action | Object | X | ボタンアクション |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http

### RCS テンプレート修正

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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様の商品が入荷されました。ぜひご来店ください^^",
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
      "title1" : "タイトル 1",
      "title2" : "タイトル 2",
      "title3" : "タイトル 3",
      "description1" : "本文 1",
      "description2" : "本文 2",
      "description3" : "本文 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定のタイトル",
                "description" : "予定の説明"
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
              "title" : "予定のタイトル",
              "description" : "予定の説明"
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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様の商品が入荷されました。ぜひご来店ください^^",
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
      "title1" : "タイトル 1",
      "title2" : "タイトル 2",
      "title3" : "タイトル 3",
      "description1" : "本文 1",
      "description2" : "本文 2",
      "description3" : "本文 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定のタイトル",
                "description" : "予定の説明"
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
              "title" : "予定のタイトル",
              "description" : "予定の説明"
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

<a id="delete-rcs-template"></a>

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

<a id="register-push-template"></a>

## Push テンプレート登録

テンプレートを登録します。

**リクエスト**

```
POST /template/v1.0/PUSH/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |



**リクエスト本文**

<!--このAPIはリクエスト本文を必要としません。-->


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
        "buttonType" : "ボタンタイプ、REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに関するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの場所、REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス、URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子、jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの場所、REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス、URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子、jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの場所、REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス、URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子、jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きいアイコンの場所、REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス、URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー。複数のメッセージをグループ単位にまとめる機能。Androidでのみサポート",
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

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | O | テンプレート名 |
| categoryId | String | X | カテゴリー ID |
| messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト), FREEMARKER(FreeMarker テンプレート)] |
| content | Object | O | プッシュメッセージ内容 |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「このAPIはレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| templateId | String | O | テンプレート登録時に発行されたテンプレート ID |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Push テンプレート登録

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
        "buttonType" : "ボタンタイプ、REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに関するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの場所、REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス、URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子、jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの場所、REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス、URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子、jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの場所、REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス、URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子、jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きいアイコンの場所、REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス、URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー。複数のメッセージをグループ単位にまとめる機能。Androidでのみサポート",
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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
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
        "buttonType" : "ボタンタイプ、REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに関するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの場所、REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス、URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子、jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの場所、REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス、URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子、jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの場所、REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス、URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子、jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きいアイコンの場所、REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス、URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー。複数のメッセージをグループ単位にまとめる機能。Androidでのみサポート",
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

<a id="list-push-templates"></a>

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

<a id="get-push-template-details"></a>

## Push テンプレート詳細照会

テンプレートを詳細照会します。

**リクエスト**

```
GET /template/v1.0/PUSH/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| templateId | Path | String | O | テンプレートID |



**リクエスト本文**

<!--このAPIはリクエスト本文を必要としません。-->

このAPIはリクエスト本文を必要としません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は「このAPIはレスポンス本文を返しません」と入力します。-->

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
          "buttonType" : "ボタンタイプ, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
          "link" : "ボタンを押したときに遷移するリンク",
          "hint" : "ボタンに関するヒント"
        } ],
        "media" : {
          "sourceType" : "メディアの場所, REMOTE, LOCAL",
          "source" : "メディアの格納先アドレス, URL, LOCAL_RESOURCE",
          "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO. Androidでは IMAGE のみサポート",
          "extension" : "メディアファイルの拡張子, jpg, png",
          "expandable" : true
        },
        "androidMedia" : {
          "sourceType" : "メディアの場所, REMOTE, LOCAL",
          "source" : "メディアの格納先アドレス, URL, LOCAL_RESOURCE",
          "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO. Androidでは IMAGE のみサポート",
          "extension" : "メディアファイルの拡張子, jpg, png",
          "expandable" : true
        },
        "iosMedia" : {
          "sourceType" : "メディアの場所, REMOTE, LOCAL",
          "source" : "メディアの格納先アドレス, URL, LOCAL_RESOURCE",
          "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO. Androidでは IMAGE のみサポート",
          "extension" : "メディアファイルの拡張子, jpg, png",
          "expandable" : true
        },
        "largeIcon" : {
          "sourceType" : "大きいアイコンの場所, REMOTE, LOCAL",
          "source" : "メディアの格納先アドレス, URL, LOCAL_RESOURCE"
        },
        "group" : {
          "key" : "グループのキー。複数のメッセージをグループ単位にまとめる機能。Androidでのみサポート",
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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| template | Object | O |  |
| template.templateId | String | O | テンプレート登録時に発行されたテンプレートID |
| template.templateName | String | O | テンプレート名 |
| template.categoryId | String | O | カテゴリーID |
| template.messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| template.messagePurpose | String | O | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| template.messagePurposes | Array | O |  |
| template.templateLanguage | String | O | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト), FREEMARKER(FreeMarker テンプレート)] |
| template.content | Object | O | プッシュメッセージの内容 |
| template.createdDateTime | String | O | テンプレート作成日時 |
| template.updatedDateTime | String | O | テンプレート更新日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Push テンプレート詳細照会

GET {{endpoint}}/template/v1.0/PUSH/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/PUSH/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="templateV1x0033UpdatePushTemplate"></span>

<a id="update-push-template"></a>

## Push テンプレート修正

テンプレートを修正します。

**リクエスト**

```
PUT /template/v1.0/PUSH/templates/{templateId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| templateId | Path | String | O | テンプレート ID |



**リクエスト本文**

<!--このAPIはリクエスト本文を要求しません。と入力します。リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->


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
        "buttonType" : "ボタンタイプ, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンのヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの位置, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの位置, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの位置, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きいアイコンの位置, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
        "description" : "グループの説明"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | O | テンプレート名 |
| messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト), FREEMARKER(FreeMarker テンプレート)] |
| content | Object | O | プッシュメッセージ内容 |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「このAPIはレスポンス本文を返しません」と入力します。-->

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
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Push テンプレート修正

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
        "buttonType" : "ボタンタイプ, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンのヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの位置, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの位置, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの位置, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きいアイコンの位置, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
        "description" : "グループの説明"
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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
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
        "buttonType" : "ボタンタイプ, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンのヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの位置, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの位置, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの位置, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Androidでは IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きいアイコンの位置, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
        "description" : "グループの説明"
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

<a id="delete-push-template"></a>

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

<a id="retrieve-template-parameters"></a>

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
