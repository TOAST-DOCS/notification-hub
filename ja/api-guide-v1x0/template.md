<!-- pre-align:aligned sig=18ca1e8f5378 -->

<!-- 新しいフォームのために追加されたスタイルです。 -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 新しいフォームのために見出しを <h1> に変更しました。 -->
<h1>テンプレート</h1>

**Notification > Notification Hub > API v1.0 使用ガイド > テンプレート**



<a id="list-kakao-templates-for-alimtalk-template"></a>
## お知らせトークテンプレートのカカオテンプレート一覧照会 { #list-kakao-templates-for-alimtalk-template }

お知らせトークテンプレートのカカオテンプレート一覧を照会します。

**リクエスト**

```
GET /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| templateId | Path | String | O | テンプレートID |
| limit | Query | Number | X | limitを設定しない場合、デフォルト 20（最大 1000） |
| offset | Query | Number | X | offsetを設定しない場合、デフォルト 0 |



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
      "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
      "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する場合があり、チェックインができない場合は予約がキャンセルされることがあります。\\n* お問い合わせ電話: 1234-1234",
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
| templates[].content.templateEmphasizeType | String | O | テンプレート強調表示タイプ<br>[NONE（強調なし）、TEXT（テキスト強調）、IMAGE（画像強調）、ITEM_LIST（アイテムリスト強調）] |
| templates[].content.templateContent | String | X | テンプレート本文 |
| templates[].content.templateAd | String | X | チャンネル追加案内メッセージ（テンプレートメッセージタイプ: チャンネル追加型、複合型の場合は固定値） |
| templates[].content.templateExtra | String | X | テンプレート付加情報（テンプレートメッセージタイプが[付加情報型/複合型]の場合は必須）、置換変数使用不可、URL含めることが可能 |
| templates[].content.templateTitle | String | X | テンプレートタイトル（最大 50 文字、Android: 2行、23 文字以上は省略表示、iOS: 2行、27 文字以上は省略表示） |
| templates[].content.templateSubtitle | String | X | テンプレートサブ文言（最大 50 文字、Android: 18 文字以上は省略表示、iOS: 21 文字以上は省略表示） |
| templates[].content.templateHeader | String | X | テンプレートヘッダー、変数入力可能 |
| templates[].content.templateItem | Object | X |  |
| templates[].content.templateItem.list | Array | O |  |
| templates[].content.templateItem.list[].title | String | O | アイテムタイトル |
| templates[].content.templateItem.list[].description | String | O | アイテム説明 |
| templates[].content.templateItem.summary | Object | X |  |
| templates[].content.templateItem.summary.title | String | O | サマリータイトル |
| templates[].content.templateItem.summary.description | String | O | サマリー説明（変数および通貨単位、数字、カンマ、ピリオドのみ使用可能） |
| templates[].content.templateItemHighlight | Object | X |  |
| templates[].content.templateItemHighlight.title | String | O | アイテムハイライトタイトル（最大 30 文字、サムネイル画像がある場合は 21 文字） |
| templates[].content.templateItemHighlight.description | String | O | アイテムハイライト説明（最大 19 文字、サムネイル画像がある場合は 13 文字） |
| templates[].content.templateItemHighlight.attachmentId | String | X | テンプレート添付ファイルID |
| templates[].content.templateItemHighlight.imageUrl | String | X | サムネイル画像アドレス |
| templates[].content.templateRepresentLink | Object | X |  |
| templates[].content.templateRepresentLink.linkMo | String | X | 代表リンクモバイルWebリンク |
| templates[].content.templateRepresentLink.linkPc | String | X | 代表リンク PC Webリンク |
| templates[].content.templateRepresentLink.schemeIos | String | X | 代表リンク iOS アプリリンク |
| templates[].content.templateRepresentLink.schemeAndroid | String | X | 代表リンク Android アプリリンク |
| templates[].content.attachmentId | String | X | テンプレート添付ファイルID |
| templates[].content.templateImageName | String | X | テンプレート画像名 |
| templates[].content.templateImageUrl | String | X | テンプレート画像リンク |
| templates[].content.securityFlag | Boolean | X | テンプレートセキュリティ有無（デフォルト: false） |
| templates[].content.categoryCode | String | X | テンプレートカテゴリーコード（テンプレートカテゴリー照会 API 参照、デフォルト: 999999） |
| templates[].content.buttons | Array | X | テンプレートボタン |
| templates[].content.buttons[].ordering | Integer | O | テンプレートボタン順序 |
| templates[].content.buttons[].type | String | O | テンプレートボタンタイプ<br>[WL（Webリンク）、AL（アプリリンク）、DS（配送照会）、BK（ボットキーワード）、MD（メッセージ転送）、BC（相談トーク切替）、BT（ボット切替）、AC（チャンネル追加）、BF（ビジネスフォーム）、P1（画像セキュリティ送信プラグイン）、P2（個人情報利用プラグイン）、P3（ワンクリック決済プラグイン）、TN（電話をかける）] |
| templates[].content.buttons[].name | String | O | テンプレートボタン名 |
| templates[].content.buttons[].linkMo | String | X | テンプレートボタンモバイルWebリンク |
| templates[].content.buttons[].linkPc | String | X | テンプレートボタン PC Webリンク |
| templates[].content.buttons[].schemeIos | String | X | テンプレートボタン iOS アプリリンク |
| templates[].content.buttons[].schemeAndroid | String | X | テンプレートボタン Android アプリリンク |
| templates[].content.buttons[].bizFormId | Integer | X | テンプレートボタンビジネスフォームID（BF タイプの場合は必須） |
| templates[].content.quickReplies | Array | X | テンプレートクイックリプライ |
| templates[].content.quickReplies[].ordering | Integer | O | テンプレートクイックリプライ順序 |
| templates[].content.quickReplies[].type | String | O | テンプレートクイックリプライタイプ<br>[WL（Webリンク）、AL（アプリリンク）、BK（ボットキーワード）、BC（相談トーク切替）、BT（ボット切替）、BF（ビジネスフォーム）] |
| templates[].content.quickReplies[].name | String | O | テンプレートクイックリプライ名 |
| templates[].content.quickReplies[].linkMo | String | X | テンプレートクイックリプライモバイルWebリンク |
| templates[].content.quickReplies[].linkPc | String | X | テンプレートクイックリプライ PC Webリンク |
| templates[].content.quickReplies[].schemeIos | String | X | テンプレートクイックリプライ iOS アプリリンク |
| templates[].content.quickReplies[].schemeAndroid | String | X | テンプレートクイックリプライ Android アプリリンク |
| templates[].content.quickReplies[].bizFormId | Integer | X | テンプレートクイックリプライビジネスフォームID（BF タイプの場合は必須） |
| templates[].reviewStatus | String | O | REGISTERED: リクエスト、REQUESTED: 審査中、APPROVED: 承認、REJECTED: 反려<br>[REGISTERED, REQUESTED, APPROVED, REJECTED] |
| templates[].comments | Array | O | テンプレート問い合わせリスト |
| templates[].comments[].id | Integer | O | 問い合わせID |
| templates[].comments[].content | String | X | 問い合わせ内容 |
| templates[].comments[].userName | String | O | 作成者 |
| templates[].comments[].createdAt | String | O | 問い合わせ作成日時 |
| templates[].comments[].attachments | Array | O | 問い合わせ添付ファイル |
| templates[].comments[].attachments[].originalFileName | String | O | 添付ファイル名 |
| templates[].comments[].attachments[].filePath | String | O | 添付ファイルパス |
| templates[].comments[].status | String | O | 問い合わせステータス（REQ: リクエスト、INQ: 問い合わせ、APR: 承認、REJ: 反려、REP: 回答）<br>[REQ, INQ, APR, REJ, REP] |
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

<a id="submit-an-alimtalk-template-inquiry-with-file-attachment"></a>
## ファイルを添付してお知らせトークテンプレートを問い合わせる { #submit-an-alimtalk-template-inquiry-with-file-attachment }

お知らせトークテンプレートを問い合わせる際に、ファイルを添付して問い合わせます。

**リクエスト**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates/{kakaoTemplateCode}/inquiries/do-with-file
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| templateId | Path | String | O | テンプレートID |
| kakaoTemplateCode | Path | String | O | カカオテンプレートコード |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は、「このAPIはリクエスト本文を必要としません」と入力します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| file | Array | O | 問い合わせファイル |
| comment | String | O | 問い合わせ内容 |



**レスポンス本文**

<!--レスポンス本文を返さない場合は、「このAPIはレスポンス本文を返しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
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



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### ファイルを添付してお知らせトークテンプレートを問い合わせる

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/kakao-templates/{{kakaoTemplateCode}}/inquiries/do-with-file
comment=comment_example
file=@/path/to/file.txt
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/kakao-templates/${kakaoTemplateCode}/inquiries/do-with-file" \
-F "comment=comment_example" \
-F "file=@/path/to/file.txt"
```

</details>

<a id="submit-an-alimtalk-template-inquiry"></a>
## カカオお知らせトークテンプレートへのお問い合わせ { #submit-an-alimtalk-template-inquiry }

カカオお知らせトークテンプレートへのお問い合わせを行います。

**リクエスト**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/kakao-templates/{kakaoTemplateCode}/inquiries
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| templateId | Path | String | O | テンプレートID |
| kakaoTemplateCode | Path | String | O | カカオテンプレートコード |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は「このAPIはリクエスト本文を必要としません」と入力します。-->


```
{
  "comment" : "お問い合わせ内容の例"
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| comment | String | O | お問い合わせ内容 |



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
### カカオお知らせトークテンプレートに問い合わせる

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/kakao-templates/{{kakaoTemplateCode}}/inquiries
{
  "comment" : "問い合わせ内容の例"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/kakao-templates/${kakaoTemplateCode}/inquiries" \
-d '{
  "comment" : "お問い合わせ内容の例"
}'
```

</details>

<a id="register-sms-template"></a>
## SMS テンプレート登録 { #register-sms-template }

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

<!--リクエスト本文を必要としない場合は「このAPIはリクエスト本文を必要としません」と入力します。-->


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
    "title" : "連休中の営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様のご注文商品が入荷いたしました。ぜひご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | O | テンプレート名 |
| categoryId | String | X | カテゴリーID |
| messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般)、AD(広告)、AUTH(認証)] |
| templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarker テンプレート)] |
| sender | Object | O |  |
| sender.senderPhoneNumber | String | O | 発信番号 |
| content | Object | O |  |
| content.messageType | String | O | 送信メッセージタイプ(SMS、LMS、MMS)<br>[SMS、LMS、MMS] |
| content.title | String | X | メッセージタイトル |
| content.body | String | O | メッセージ本文 |
| content.attachmentIds | Array | X | 添付ファイルID（最大3件） |
| content.imageLayoutId | String | X | 画像レイアウトID |



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
| templateId | String | O | テンプレート登録時に発行されたテンプレートID |



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
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様のご注文商品が入荷されました。ぜひご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}'
```

</details>

<a id="list-sms-templates"></a>
## SMS テンプレートリスト照会 { #list-sms-templates }

テンプレートリストを照会します。

**リクエスト**

```
GET /template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| templateName | Query | String | X | テンプレート名 (LIKE 検索) |
| limit | Query | Number | X | limit を設定しない場合、デフォルト 20 (最大 1000) |
| offset | Query | Number | X | offset を設定しない場合、デフォルト 0 |



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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| totalCount | Integer | O | 総件数 |
| templates | Array | O |  |
| templates[].templateId | String | O | テンプレート登録時に発行されたテンプレート ID |
| templates[].templateName | String | O | テンプレート名 |
| templates[].categoryId | String | O | カテゴリー ID |
| templates[].messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| templates[].messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| templates[].messagePurposes | Array | O |  |
| templates[].createdDateTime | String | O | テンプレート作成日時 |
| templates[].updatedDateTime | String | O | テンプレート更新日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMS テンプレートリスト照会

GET {{endpoint}}/template/v1.0/SMS/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/SMS/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<a id="get-sms-template-details"></a>
## SMS テンプレート詳細照会 { #get-sms-template-details }

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
      "senderPhoneNumber" : "01012341234"
    },
    "content" : {
      "messageType" : "SMS",
      "title" : "祝日の営業時間のお知らせ",
      "body" : "こんにちは。本日、お客様の商品が入荷しました。ぜひご来店ください^^",
      "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
      "imageLayoutId" : "YaX2DA4Weab1"
    },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--レスポンス本文のフィールドを説明します。-->

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
| template.messageChannel | String | X | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| template.messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| template.messagePurposes | Array | X |  |
| template.templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト), FREEMARKER(FreeMarker テンプレート)] |
| template.sender | Object | X |  |
| template.sender.senderPhoneNumber | String | O | 発信番号 |
| template.content | Object | X |  |
| template.content.messageType | String | O | 送信メッセージタイプ (SMS、LMS、MMS)<br>[SMS, LMS, MMS] |
| template.content.title | String | X | メッセージタイトル |
| template.content.body | String | O | メッセージ本文 |
| template.content.attachmentIds | Array | X | 添付ファイル ID（最大 3 件） |
| template.content.imageLayoutId | String | X | 画像レイアウト ID |
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

<a id="update-sms-template"></a>
## SMS テンプレートの修正 { #update-sms-template }

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

<!--リクエスト本文を必要としない場合は「この API はリクエスト本文を必要としません」と入力します。-->


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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様の商品が入荷いたしました。ぜひご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
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
| sender.senderPhoneNumber | String | O | 発信番号 |
| content | Object | O |  |
| content.messageType | String | O | 送信メッセージタイプ (SMS, LMS, MMS)<br>[SMS, LMS, MMS] |
| content.title | String | X | メッセージタイトル |
| content.body | String | O | メッセージ本文 |
| content.attachmentIds | Array | X | 添付ファイル ID (最大 3 件) |
| content.imageLayoutId | String | X | 画像レイアウト ID |



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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様の商品が入荷いたしました。ぜひご来店ください^^",
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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様のご注文商品が入荷いたしました。ぜひご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ],
    "imageLayoutId" : "YaX2DA4Weab1"
  }
}'
```

</details>

<a id="delete-sms-template"></a>
## SMS テンプレートの削除 { #delete-sms-template }

テンプレートを削除します。

**リクエスト**

```
DELETE /template/v1.0/SMS/templates/{templateId}
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

<!--リクエスト本文が不要な場合は「この API はリクエスト本文を必要としません」と入力します。-->

この API はリクエスト本文を必要としません。



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
### SMS テンプレートの削除

DELETE {{endpoint}}/template/v1.0/SMS/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/SMS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<a id="register-alimtalk-template"></a>
## お知らせトークテンプレート登録 { #register-alimtalk-template }

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
    "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
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
  "additionalProperty" : {
    "templateCode" : "templateCode",
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

| 経路 | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | O | テンプレート名 |
| categoryId | String | X | カテゴリー ID |
| messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| templateLanguage | String | X | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト), FREEMARKER(FreeMarker テンプレート)] |
| sender | Object | X |  |
| sender.senderKey | String | X | 発信プロフィール発信キー |
| sender.senderProfileType | String | X | 発信プロフィールタイプ<br>[GROUP, NORMAL] |
| content | Object | O |  |
| content.templateMessageType | String | X | テンプレートメッセージタイプ(BA: 基本型、EX: 付加情報型、AD: チャンネル追加型、MI: 複合型、default: BA) |
| content.templateEmphasizeType | String | O | テンプレート強調表示タイプ<br>[NONE(強調なし), TEXT(テキスト強調), IMAGE(画像強調), ITEM_LIST(アイテムリスト強調)] |
| content.templateContent | String | X | テンプレート本文 |
| content.templateAd | String | X | チャンネル追加案内メッセージ（テンプレートメッセージタイプ: チャンネル追加型、複合型の場合は固定値） |
| content.templateExtra | String | X | テンプレート付加情報（テンプレートメッセージタイプが[付加情報型/複合型]の場合は必須）、置換変数使用不可、URL 含めることが可能 |
| content.templateTitle | String | X | テンプレートタイトル（最大 50 文字、Android: 2 行、23 文字以上は省略表示、iOS: 2 行、27 文字以上は省略表示） |
| content.templateSubtitle | String | X | テンプレート補助文言（最大 50 文字、Android: 18 文字以上は省略表示、iOS: 21 文字以上は省略表示） |
| content.templateHeader | String | X | テンプレートヘッダー、変数入力可能 |
| content.templateItem | Object | X |  |
| content.templateItem.list | Array | O |  |
| content.templateItem.list[].title | String | O | アイテムタイトル |
| content.templateItem.list[].description | String | O | アイテムの説明 |
| content.templateItem.summary | Object | X |  |
| content.templateItem.summary.title | String | O | 要約タイトル |
| content.templateItem.summary.description | String | O | 要約説明（変数および通貨単位、数字、カンマ、ピリオドのみ使用可能） |
| content.templateItemHighlight | Object | X |  |
| content.templateItemHighlight.title | String | O | アイテムハイライトタイトル（最大30文字、サムネイル画像がある場合は21文字） |
| content.templateItemHighlight.description | String | O | アイテムハイライト説明（最大19文字、サムネイル画像がある場合は13文字） |
| content.templateItemHighlight.attachmentId | String | X | テンプレート添付ファイルID |
| content.templateItemHighlight.imageUrl | String | X | サムネイル画像アドレス |
| content.templateRepresentLink | Object | X |  |
| content.templateRepresentLink.linkMo | String | X | 代表リンクモバイルWebリンク |
| content.templateRepresentLink.linkPc | String | X | 代表リンク PC ウェブリンク |
| content.templateRepresentLink.schemeIos | String | X | 代表リンク iOS アプリリンク |
| content.templateRepresentLink.schemeAndroid | String | X | 代表リンク Android アプリリンク |
| content.attachmentId | String | X | テンプレート添付ファイル ID |
| content.templateImageName | String | X | テンプレート画像名 |
| content.templateImageUrl | String | X | テンプレート画像リンク |
| content.securityFlag | Boolean | X | テンプレートのセキュリティ有無(default: false) |
| content.categoryCode | String | X | テンプレートカテゴリーコード(テンプレートカテゴリー照会 API 参照、default: 999999) |
| content.buttons | Array | X | テンプレートボタン |
| content.buttons[].ordering | Integer | O | テンプレートボタンの順序 |
| content.buttons[].type | String | O | テンプレートボタンの種類<br>[WL(ウェブリンク)、AL(アプリリンク)、DS(配送照会)、BK(ボットキーワード)、MD(メッセージ転送)、BC(相談トーク切替)、BT(ボット切替)、AC(チャンネル追加)、BF(ビジネスフォーム)、P1(画像セキュリティ送信プラグイン)、P2(個人情報利用プラグイン)、P3(ワンクリック決済プラグイン)、TN(電話をかける)] |
| content.buttons[].name | String | O | テンプレートボタン名 |
| content.buttons[].linkMo | String | X | テンプレートボタンのモバイルウェブリンク |
| content.buttons[].linkPc | String | X | テンプレートボタンのPCウェブリンク |
| content.buttons[].schemeIos | String | X | テンプレートボタンのiOSアプリリンク |
| content.buttons[].schemeAndroid | String | X | テンプレートボタンのAndroidアプリリンク |
| content.buttons[].bizFormId | Integer | X | テンプレートボタンのビジネスフォームID(BFタイプの場合、必須) |
| content.quickReplies | Array | X | テンプレートのクイックリプライ |
| content.quickReplies[].ordering | Integer | O | テンプレートのクイックリプライの順序 |
| content.quickReplies[].type | String | O | テンプレートのクイックリプライの種類<br>[WL(ウェブリンク)、AL(アプリリンク)、BK(ボットキーワード)、BC(相談トーク切替)、BT(ボット切替)、BF(ビジネスフォーム)] |
| content.quickReplies[].name | String | O | テンプレートバロ連結名 |
| content.quickReplies[].linkMo | String | X | テンプレートバロ連結モバイルWebリンク |
| content.quickReplies[].linkPc | String | X | テンプレートバロ連結PC Webリンク |
| content.quickReplies[].schemeIos | String | X | テンプレートバロ連結 iOS アプリリンク |
| content.quickReplies[].schemeAndroid | String | X | テンプレートバロ連結 Android アプリリンク |
| content.quickReplies[].bizFormId | Integer | X | テンプレートバロ連結ビジネスフォーム ID（BF タイプの場合、必須） |
| additionalProperty | Object | O |  |
| additionalProperty.templateCode | String | O | テンプレートコード（英字、数字、-、_） |
| additionalProperty.kakaoTemplateCode | String | X | カカオテンプレートコード |

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
| templateId | String | O | テンプレート登録時に発行されたテンプレートID |

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
    "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する場合があります。チェックインができない場合、予約がキャンセルされることがあります。\\n* お問い合わせ電話: 1234-1234",
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
    "templateContent" : "#{이름}様のご注文が完了しました。",
    "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
    "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する場合があります。チェックインできない場合、予約がキャンセルされることがあります。\\n* お問い合わせ電話: 1234-1234",
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
      "name" : "クイック接続名",
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

<a id="list-alimtalk-templates"></a>
## お知らせトークテンプレートリスト照会 { #list-alimtalk-templates }

テンプレートリストを照会します。

**リクエスト**

```
GET /template/v1.0/ALIMTALK/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| templateName | Query | String | X | テンプレート名（LIKE 検索） |
| senderKey | Query | String | X | 発信キー |
| templateStatus | Query | String | X | テンプレートステータス |
| limit | Query | Number | X | limit を設定しない場合、デフォルト 20（最大 1000） |
| offset | Query | Number | X | offset を設定しない場合、デフォルト 0 |



**リクエスト本文**

<!--リクエスト本文を要求しない場合は「この API はリクエスト本文を要求しません」と入力します。-->

この API はリクエスト本文を要求しません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| totalCount | Integer | O | 総件数 |
| templates | Array | O |  |
| templates[].templateId | String | O | テンプレート登録時に発行されたテンプレート ID |
| templates[].templateName | String | O | テンプレート名 |
| templates[].categoryId | String | O | カテゴリー ID |
| templates[].messageChannel | String | O | メッセージチャネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| templates[].messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| templates[].messagePurposes | Array | O |  |
| templates[].createdDateTime | String | O | テンプレート作成日時 |
| templates[].updatedDateTime | String | O | テンプレート更新日時 |



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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<a id="list-templates-by-alimtalk-sender"></a>
## お知らせトーク発信者に関連するテンプレートリストの照会 { #list-templates-by-alimtalk-sender }

発信者に関連するテンプレートリストを照会します。（発信者または発信者が含まれるグループのテンプレート）

**リクエスト**

```
GET /template/v1.0/ALIMTALK/senders/{senderKey}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| senderKey | Path | String | O | 発信キー |
| templateName | Query | String | X | テンプレート名（LIKE 検索） |
| templateStatus | Query | String | X | テンプレートステータス |
| limit | Query | Number | X | limit を設定しない場合のデフォルト値は 20（最大 1000） |
| offset | Query | Number | X | offset を設定しない場合のデフォルト値は 0 |



**リクエスト本文**

<!--リクエスト本文が不要な場合は「この API はリクエスト本文を必要としません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| totalCount | Integer | O | 総件数 |
| templates | Array | O |  |
| templates[].templateId | String | O | テンプレート登録時に発行されたテンプレート ID |
| templates[].templateName | String | O | テンプレート名 |
| templates[].categoryId | String | O | カテゴリー ID |
| templates[].messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| templates[].messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| templates[].messagePurposes | Array | O |  |
| templates[].createdDateTime | String | O | テンプレート作成日時 |
| templates[].updatedDateTime | String | O | テンプレート更新日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークの発信者に関連するテンプレートリスト照会

GET {{endpoint}}/template/v1.0/ALIMTALK/senders/{{senderKey}}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/ALIMTALK/senders/${senderKey}/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<a id="get-alimtalk-template-details"></a>
## お知らせトークテンプレート詳細照会 { #get-alimtalk-template-details }

テンプレートの詳細を照会します。

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

<!--リクエスト本文を必要としない場合は「このAPIはリクエスト本文を必要としません」と入力します。-->

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
      "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する場合があり、チェックインができない場合は予約がキャンセルされることがあります。\\n* お問い合わせ電話番号: 1234-1234",
      "templateTitle" : "123,450円",
      "templateSubtitle" : "承認内訳",
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
        "name" : "クイック接続名",
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
| template.messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| template.messagePurpose | String | O | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| template.messagePurposes | Array | O |  |
| template.templateLanguage | String | O | テンプレート言語タイプ<br>デフォルト値: PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト), FREEMARKER(FreeMarker テンプレート)] |
| template.sender | Object | X |  |
| template.sender.senderKey | String | O | 発信プロフィール発信キー |
| template.sender.senderProfileId | String | O | カカオトークチャンネル名 |
| template.sender.senderProfileType | String | O | 発信プロフィールタイプ<br>[GROUP, NORMAL] |
| template.additionalProperty | Object | O |  |
| template.additionalProperty.kakaoTemplateCode | String | O | カカオテンプレートコード |
| template.additionalProperty.templateCode | String | O | テンプレートコード(英字、数字、-、_) |
| template.additionalProperty.comments | Array | O | テンプレート問い合わせリスト |
| template.additionalProperty.comments[].id | Integer | O | 問い合わせ ID |
| template.additionalProperty.comments[].content | String | X | 問い合わせ内容 |
| template.additionalProperty.comments[].userName | String | O | 作成者 |
| template.additionalProperty.comments[].createdAt | String | O | 問い合わせ作成日時 |
| template.additionalProperty.comments[].attachments | Array | O | 問い合わせ添付ファイル |
| template.additionalProperty.comments[].attachments[].originalFileName | String | O | 添付ファイル名 |
| template.additionalProperty.comments[].attachments[].filePath | String | O | 添付ファイルのパス |
| template.additionalProperty.comments[].status | String | O | 問い合わせステータス（REQ: リクエスト、INQ: 問い合わせ、APR: 承認、REJ: 差し戻し、REP: 返信）<br>[REQ, INQ, APR, REJ, REP] |
| template.additionalProperty.status | String | X | REGISTERED: リクエスト、REQUESTED: 審査中、APPROVED: 承認、REJECTED: 差し戻し<br>[REGISTERED, REQUESTED, APPROVED, REJECTED] |
| template.additionalProperty.block | Boolean | O | テンプレートのブロック有無<br>デフォルト値: false |
| template.additionalProperty.dormant | Boolean | O | テンプレート休眠かどうか<br>デフォルト値: false |
| template.content | Object | O |  |
| template.content.templateMessageType | String | X | テンプレートメッセージタイプ(BA: 基本型、EX: 付加情報型、AD: チャンネル追加型、MI: 複合型、default: BA) |
| template.content.templateEmphasizeType | String | O | テンプレート強調表示タイプ<br>[NONE(強調なし)、TEXT(テキスト強調)、IMAGE(画像強調)、ITEM_LIST(アイテムリスト強調)] |
| template.content.templateContent | String | X | テンプレート本文 |
| template.content.templateAd | String | X | チャンネル追加案内メッセージ(テンプレートメッセージタイプ: チャンネル追加型、複合型の場合は固定値) |
| template.content.templateExtra | String | X | テンプレート付加情報(テンプレートメッセージタイプが[付加情報型/複合型]の場合は必須)、置換変数は使用不可、URLは含めることが可能 |
| template.content.templateTitle | String | X | テンプレートタイトル(最大50文字、Android: 2行、23文字以上で省略処理、iOS: 2行、27文字以上で省略処理) |
| template.content.templateSubtitle | String | X | テンプレート補助フレーズ(最大50文字、Android: 18文字以上で省略処理、iOS: 21文字以上で省略処理) |
| template.content.templateHeader | String | X | テンプレートヘッダー、変数入力可 |
| template.content.templateItem | Object | X |  |
| template.content.templateItem.list | Array | O |  |
| template.content.templateItem.list[].title | String | O | アイテムタイトル |
| template.content.templateItem.list[].description | String | O | アイテムの説明 |
| template.content.templateItem.summary | Object | X |  |
| template.content.templateItem.summary.title | String | O | 要約タイトル |
| template.content.templateItem.summary.description | String | O | 要約の説明（変数および通貨単位、数字、カンマ、ピリオドのみ使用可能） |
| template.content.templateItemHighlight | Object | X |  |
| template.content.templateItemHighlight.title | String | O | アイテムハイライトタイトル（最大30文字、サムネイル画像がある場合は21文字） |
| template.content.templateItemHighlight.description | String | O | アイテムハイライトの説明（最大19文字、サムネイル画像がある場合は13文字） |
| template.content.templateItemHighlight.attachmentId | String | X | テンプレート添付ファイル ID |
| template.content.templateItemHighlight.imageUrl | String | X | サムネイル画像アドレス |
| template.content.templateRepresentLink | Object | X |  |
| template.content.templateRepresentLink.linkMo | String | X | 代表リンク モバイル Web リンク |
| template.content.templateRepresentLink.linkPc | String | X | 代表リンク PC Web リンク |
| template.content.templateRepresentLink.schemeIos | String | X | 代表リンク iOS アプリリンク |
| template.content.templateRepresentLink.schemeAndroid | String | X | 代表リンク Android アプリリンク |
| template.content.attachmentId | String | X | テンプレート添付ファイル ID |
| template.content.templateImageName | String | X | テンプレート画像名 |
| template.content.templateImageUrl | String | X | テンプレート画像リンク |
| template.content.securityFlag | Boolean | X | テンプレートのセキュリティ設定（default: false） |
| template.content.categoryCode | String | X | テンプレートカテゴリコード（テンプレートカテゴリ照会 API 参考、default: 999999） |
| template.content.buttons | Array | X | テンプレートボタン |
| template.content.buttons[].ordering | Integer | O | テンプレートボタンの順序 |
| template.content.buttons[].type | String | O | テンプレートボタンの種類<br>[WL（Webリンク）、AL（アプリリンク）、DS（配送照会）、BK（ボットキーワード）、MD（メッセージ転送）、BC（相談トーク切替）、BT（ボット切替）、AC（チャンネル追加）、BF（ビジネスフォーム）、P1（画像セキュリティ送信プラグイン）、P2（個人情報利用プラグイン）、P3（ワンクリック決済プラグイン）、TN（電話をかける）] |
| template.content.buttons[].name | String | O | テンプレートボタン名 |
| template.content.buttons[].linkMo | String | X | テンプレートボタンのモバイルWebリンク |
| template.content.buttons[].linkPc | String | X | テンプレートボタンのPC Webリンク |
| template.content.buttons[].schemeIos | String | X | テンプレートボタンの iOS アプリリンク |
| template.content.buttons[].schemeAndroid | String | X | テンプレートボタンの Android アプリリンク |
| template.content.buttons[].bizFormId | Integer | X | テンプレートボタンビジネスフォーム ID（BF タイプの場合、必須） |
| template.content.quickReplies | Array | X | テンプレートクイック接続 |
| template.content.quickReplies[].ordering | Integer | O | テンプレートクイック接続の順序 |
| template.content.quickReplies[].type | String | O | テンプレートクイック接続のタイプ<br>[WL（Web リンク）、AL（アプリリンク）、BK（ボットキーワード）、BC（相談トーク切替）、BT（ボット切替）、BF（ビジネスフォーム）] |
| template.content.quickReplies[].name | String | O | テンプレートクイック接続の名前 |
| template.content.quickReplies[].linkMo | String | X | テンプレートクイック接続のモバイル Web リンク |
| template.content.quickReplies[].linkPc | String | X | テンプレートクイック接続の PC Web リンク |
| template.content.quickReplies[].schemeIos | String | X | テンプレートクイック接続の iOS アプリリンク |
| template.content.quickReplies[].schemeAndroid | String | X | テンプレートクイック接続の Android アプリリンク |
| template.content.quickReplies[].bizFormId | Integer | X | テンプレートクイック接続ビジネスフォーム ID（BF タイプの場合、必須） |
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

<a id="update-alimtalk-template"></a>
## お知らせトークテンプレートの修正 { #update-alimtalk-template }

テンプレートを修正します。

**リクエスト**

```
PUT /template/v1.0/ALIMTALK/templates/{templateId}
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

<!--リクエスト本文を必要としない場合は、「このAPIはリクエスト本文を必要としません」と入力します。-->

```
{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "#{名前}様のご注文が完了しました。",
    "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
    "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する場合があり、チェックインができない場合は予約がキャンセルされることがあります。\\n* お問い合わせ電話: 1234-1234",
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
      "name" : "クイック接続名",
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

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | O | テンプレート名 |
| messagePurpose | String | O | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| content | Object | O |  |
| content.templateMessageType | String | X | テンプレートメッセージタイプ(BA: 基本型, EX: 付加情報型, AD: チャンネル追加型, MI: 複合型, default: BA) |
| content.templateEmphasizeType | String | O | テンプレート強調表示タイプ<br>[NONE(強調なし), TEXT(テキスト強調), IMAGE(画像強調), ITEM_LIST(アイテムリスト強調)] |
| content.templateContent | String | X | テンプレート本文 |
| content.templateAd | String | X | チャンネル追加案内メッセージ(テンプレートメッセージタイプ: チャンネル追加型、複合型の場合は固定値) |
| content.templateExtra | String | X | テンプレート付加情報(テンプレートメッセージタイプが[付加情報型/複合型]の場合は必須)、置換変数使用不可、URL含有可 |
| content.templateTitle | String | X | テンプレートタイトル(最大50文字、Android: 2行、23文字以上は省略表示、iOS: 2行、27文字以上は省略表示) |
| content.templateSubtitle | String | X | テンプレート補助文句(最大50文字、Android: 18文字以上は省略表示、iOS: 21文字以上は省略表示) |
| content.templateHeader | String | X | テンプレートヘッダー。変数の入力が可能 |
| content.templateItem | Object | X |  |
| content.templateItem.list | Array | O |  |
| content.templateItem.list[].title | String | O | アイテムタイトル |
| content.templateItem.list[].description | String | O | アイテムの説明 |
| content.templateItem.summary | Object | X |  |
| content.templateItem.summary.title | String | O | サマリータイトル |
| content.templateItem.summary.description | String | O | サマリーの説明（変数および通貨単位、数字、カンマ、ピリオドのみ使用可能） |
| content.templateItemHighlight | Object | X |  |
| content.templateItemHighlight.title | String | O | アイテムハイライトタイトル（最大 30 文字。サムネイル画像がある場合は 21 文字） |
| content.templateItemHighlight.description | String | O | アイテムハイライトの説明（最大 19 文字、サムネイル画像がある場合は 13 文字） |
| content.templateItemHighlight.attachmentId | String | X | テンプレート添付ファイル ID |
| content.templateItemHighlight.imageUrl | String | X | サムネイル画像のアドレス |
| content.templateRepresentLink | Object | X |  |
| content.templateRepresentLink.linkMo | String | X | 代表リンクのモバイル Web リンク |
| content.templateRepresentLink.linkPc | String | X | 代表リンクの PC Web リンク |
| content.templateRepresentLink.schemeIos | String | X | 代表リンクの iOS アプリリンク |
| content.templateRepresentLink.schemeAndroid | String | X | 代表リンクの Android アプリリンク |
| content.attachmentId | String | X | テンプレート添付ファイル ID |
| content.templateImageName | String | X | テンプレート画像の名前 |
| content.templateImageUrl | String | X | テンプレート画像リンク |
| content.securityFlag | Boolean | X | テンプレートのセキュリティ有無（default: false） |
| content.categoryCode | String | X | テンプレートカテゴリコード（テンプレートカテゴリ照会 API 参照、default: 999999） |
| content.buttons | Array | X | テンプレートボタン |
| content.buttons[].ordering | Integer | O | テンプレートボタンの順序 |
| content.buttons[].type | String | O | テンプレートボタンの種類<br>[WL（ウェブリンク）、AL（アプリリンク）、DS（配送照会）、BK（ボットキーワード）、MD（メッセージ転送）、BC（相談トーク切り替え）、BT（ボット切り替え）、AC（チャンネル追加）、BF（ビジネスフォーム）、P1（画像セキュリティ送信プラグイン）、P2（個人情報利用プラグイン）、P3（ワンクリック決済プラグイン）、TN（電話をかける）] |
| content.buttons[].name | String | O | テンプレートボタン名 |
| content.buttons[].linkMo | String | X | テンプレートボタンのモバイルウェブリンク |
| content.buttons[].linkPc | String | X | テンプレートボタンの PC ウェブリンク |
| content.buttons[].schemeIos | String | X | テンプレートボタンの iOS アプリリンク |
| content.buttons[].schemeAndroid | String | X | テンプレートボタン Android アプリリンク |
| content.buttons[].bizFormId | Integer | X | テンプレートボタンビジネスフォーム ID（BF タイプの場合、必須） |
| content.quickReplies | Array | X | テンプレートクイックリプライ |
| content.quickReplies[].ordering | Integer | O | テンプレートクイックリプライ順序 |
| content.quickReplies[].type | String | O | テンプレートクイックリプライタイプ<br>[WL（Web リンク）、AL（アプリリンク）、BK（ボットキーワード）、BC（相談トーク転換）、BT（ボット転換）、BF（ビジネスフォーム）] |
| content.quickReplies[].name | String | O | テンプレートクイックリプライ名 |
| content.quickReplies[].linkMo | String | X | テンプレートクイックリプライモバイル Web リンク |
| content.quickReplies[].linkPc | String | X | テンプレートクイックリプライ PC Web リンク |
| content.quickReplies[].schemeIos | String | X | テンプレートクイックリプライ iOS アプリリンク |
| content.quickReplies[].schemeAndroid | String | X | テンプレートクイックリプライ Android アプリリンク |
| content.quickReplies[].bizFormId | Integer | X | テンプレートバロ連結ビジネスフォーム ID（BF タイプの場合、必須） |
| additionalProperty | Object | O |  |
| additionalProperty.kakaoTemplateCode | String | O | カカオテンプレートコード（英字、数字、-、_） |

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
    "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する場合があり、チェックインができない場合は予約がキャンセルされることがあります。\\n* お問い合わせ電話: 1234-1234",
    "templateTitle" : "123,450円",
    "templateSubtitle" : "承認内訳",
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
      "name" : "クイック接続名",
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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "テンプレート名",
  "messagePurpose" : "NORMAL",
  "content" : {
    "templateMessageType" : "BA",
    "templateEmphasizeType" : "NONE",
    "templateContent" : "#{名前}様のご注文が完了しました。",
    "templateAd" : "チャンネルを追加して、このチャンネルのマーケティングメッセージなどをカカオトークで受け取る",
    "templateExtra" : "* リアルタイム予約の特性上、重複予約が発生する場合があり、チェックインができない場合は予約がキャンセルされる場合があります。\\n* お問い合わせ電話番号: 1234-1234",
    "templateTitle" : "123,450円",
    "templateSubtitle" : "承認内訳",
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
  "additionalProperty" : {
    "kakaoTemplateCode" : "kakaoTemplateCode"
  }
}'
```

</details>

<a id="delete-alimtalk-template"></a>
## お知らせトークテンプレート削除 { #delete-alimtalk-template }

テンプレートを削除します。

**リクエスト**

```
DELETE /template/v1.0/ALIMTALK/templates/{templateId}
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

<!--リクエスト本文を必要としない場合は「このAPIはリクエスト本文を必要としません」と入力します。-->

このAPIはリクエスト本文を必要としません。



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

<!--レスポンス本文のフィールドについて説明します。-->

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
### お知らせトークテンプレートの削除

DELETE {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<a id="submit-an-alimtalk-template-inquiry---deprecated"></a>
## お知らせトークテンプレートのお問い合わせ - Deprecated { #submit-an-alimtalk-template-inquiry---deprecated }

!!! danger このAPIはサポートされていません。
* [カカオお知らせトークテンプレートのお問い合わせ](#submit-an-alimtalk-template-inquiry) を参照してください。

お知らせトークテンプレートのお問い合わせを行います。


**リクエスト**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/inquiries
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

<!--リクエスト本文を必要としない場合は「このAPIはリクエスト本文を必要としません」と入力します。-->


```
{
  "comment" : "お問い合わせ内容の例"
}
```

<!--リクエスト本文のフィールドについて説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| comment | String | O | お問い合わせ内容 |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「このAPIはレスポンス本文を返しません」と入力します。-->




**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレートに問い合わせる - Deprecated

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/inquiries
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "comment" : "問い合わせ内容の例"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/inquiries" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "comment" : "お問い合わせ内容の例"
}'
```

</details>

<a id="submit-an-alimtalk-template-inquiry-with-file-attachment---deprecated"></a>
## お知らせトーク テンプレートの問い合わせ（ファイル添付） - Deprecated { #submit-an-alimtalk-template-inquiry-with-file-attachment---deprecated }

!!! danger このAPIはサポートが終了しました。
* [カカオ お知らせトーク テンプレートの問い合わせ](#submit-an-alimtalk-template-inquiry) を参照してください。

お知らせトーク テンプレートに問い合わせる際、ファイルを添付して問い合わせます。


**リクエスト**

```
POST /template/v1.0/ALIMTALK/templates/{templateId}/inquiries/do-with-file
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

<!--リクエスト本文が必要ない場合は「このAPIはリクエスト本文を必要としません」と入力します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| file | Array | O | 問い合わせファイル |
| comment | String | O | 問い合わせ内容 |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「このAPIはレスポンス本文を返しません」と入力します。-->




**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレートへの問い合わせ(ファイル添付) - Deprecated

POST {{endpoint}}/template/v1.0/ALIMTALK/templates/{{templateId}}/inquiries/do-with-file
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
comment=comment_example
file=@/path/to/file.txt
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/ALIMTALK/templates/${templateId}/inquiries/do-with-file" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-F "comment=comment_example" \
-F "file=@/path/to/file.txt"
```

</details>

<a id="list-alimtalk-template-updates"></a>
## カカオお知らせトークテンプレート問い合わせ { #list-alimtalk-template-updates }

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

<a id="list-alimtalk-template-categories"></a>
## お知らせトークテンプレートカテゴリーリスト照会 { #list-alimtalk-template-categories }

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

<a id="register-email-template"></a>
## Emailテンプレート登録 { #register-email-template }

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
| templateLanguage | String | N | テンプレート言語のタイプ<br>デフォルト値：PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarkerテンプレート)] |
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

<a id="get-email-template-details"></a>
## Emailテンプレート詳細照会 { #get-email-template-details }

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
| template.messageChannel | String | X | メッセージチャネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| template.messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array |  |
| template.templateLanguage | String | テンプレート言語のタイプ<br>デフォルト値：PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarkerテンプレート)] |
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

<a id="list-email-templates"></a>
## Emailテンプレートリスト照会 { #list-email-templates }

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
| templates[].messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
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

<a id="update-email-template"></a>
## Emailテンプレート修正 { #update-email-template }

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
| templateLanguage | String | N | テンプレート言語のタイプ<br>デフォルト値：PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarkerテンプレート)] |
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

<a id="delete-email-template"></a>
## Emailテンプレート削除 { #delete-email-template }

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

<a id="register-rcs-template"></a>
## RCSテンプレート登録 { #register-rcs-template }

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
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください",
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
| templateName | String | O | テンプレート名 |
| categoryId | String | X | カテゴリーID |
| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | Y | テンプレート名 |
| categoryId | String | N | カテゴリーID |
| messagePurpose | String | N | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| templateLanguage | String | N | テンプレート言語のタイプ<br>デフォルト値：PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarkerテンプレート)] |
| sender | Object | Y |  |
| sender.brandId | String | Y | ブランドID |
| sender.chatbotId | String | Y | トークルーム(チャットボット)ID |
| content | Object | Y |  |
| content.messageType | String | N | RCS送信メッセージのタイプ<br>[SMS(ショートメッセージ)、LMS(ロングメッセージ)、MMS(マルチメディアメッセージ)、RBC_TEMPLATE(RCS Biz Centerテンプレート)] |
| content.title | String | N | メッセージ件名 |
| content.body | String | N | メッセージ本文 |
| content.smsType | String | X | SMSのタイプ<br>[STANDALONE(スタンドアロン型)、UNIFIED_STANDALONE(統合スタンドアロン型)] |
| content.lmsType | String | X | LMSのタイプ<br>[STANDALONE(スタンドアロン型)、FORMAT_BASIC(基本形式)、FORMAT_TITLE_HIGHLIGHT(タイトル強調形式)、FORMAT_PARAGRAPH(段落形式)、UNIFIED_STANDALONE(統合スタンドアロン型)] |
| content.mmsType | String | X | MMSのタイプ(MMS送信の場合は必須)<br>[HORIZONTAL(横型)、VERTICAL(縦型)、CAROUSEL_MEDIUM(カルーセル中型)、CAROUSEL_SMALL(カルーセル小型)、UNIFIED_HORIZONTAL(統合横型)、UNIFIED_VERTICAL(統合縦型)] |
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
| content.cards[].buttons[].buttonJson | Object | X | ボタン内容JSONオブジェクト |
| content.cards[].buttons | Array | N |  |
| content.buttons | Array | N | RCSボタンリスト |
| content.buttons[].buttonType | String | N | buttonType値と同じ名前を持つActionオブジェクトがbuttonJsonに含まれます。<br>ボタンタイプ トークルームを開く(COMPOSE)、コピーする(CLIPBOARD)、電話をかける(DIALER)、地図を表示する(MAP_SHOW)、地図を検索する(MAP_QUERY)、現在地を共有する(MAP_SHARE)、URLに接続する(URL)、日程を登録する(CALENDAR)<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | X | ボタン内容の JSON オブジェクト |
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
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください",
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
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください",
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

</details>

<a id="list-rcs-templates"></a>
## RCSテンプレートリスト照会 { #list-rcs-templates }

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
| templates[].messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
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

<a id="get-rcs-template-details"></a>
## RCSテンプレート詳細照会 { #get-rcs-template-details }

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
      "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください",
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
| template.messageChannel | String | X | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| template.messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array |  |
| template.templateLanguage | String | テンプレート言語のタイプ<br>デフォルト値：PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarkerテンプレート)] |
| template.sender | Object |  |
| template.sender.brandId | String | ブランドID |
| template.sender.chatbotId | String | トークルーム(チャットボット)ID |
| template.content | Object |  |
| template.content.messageType | String | RCS送信メッセージのタイプ<br>[SMS(ショートメッセージ)、LMS(ロングメッセージ)、MMS(マルチメディアメッセージ)、RBC_TEMPLATE(RCS Biz Centerテンプレート)] |
| template.content.title | String | メッセージ件名 |
| template.content.body | String | メッセージ本文 |
| template.content.smsType | String | X | SMSのタイプ<br>[STANDALONE(スタンドアロン型)、UNIFIED_STANDALONE(統合スタンドアロン型)] |
| template.content.lmsType | String | X | LMSのタイプ<br>[STANDALONE(スタンドアロン型)、FORMAT_BASIC(基本形式)、FORMAT_TITLE_HIGHLIGHT(タイトル強調形式)、FORMAT_PARAGRAPH(段落形式)、UNIFIED_STANDALONE(統合スタンドアロン型)] |
| template.content.mmsType | String | X | MMSのタイプ(MMS送信の場合は必須)<br>[HORIZONTAL(横型)、VERTICAL(縦型)、CAROUSEL_MEDIUM(カルーセル中型)、CAROUSEL_SMALL(カルーセル小型)、UNIFIED_HORIZONTAL(統合横型)、UNIFIED_VERTICAL(統合縦型)] |
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
| template.content.cards[].buttons[].buttonJson | Object | X | ボタン内容 JSON オブジェクト |
| template.content.buttons[].buttonJson | Object |  |
| template.content.buttons[].buttonJson.action | Object | ボタンアクション |
| template.additionalProperty | Object |  |
| template.content.buttons[].buttonJson | Object | X | ボタン内容の JSON オブジェクト |
| template.additionalProperty.approvedDateTime | String | テンプレート承認日時 |
| template.createdDateTime | String | テンプレート作成日時 |
| template.updatedDateTime | String | テンプレート修正日時 |



| template.additionalProperty.approvedDateTime | String | X | テンプレート承認日時 |
| template.createdDateTime | String | X | テンプレート作成日時 |
| template.updatedDateTime | String | X | テンプレートの更新日時 |
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

```http
curl -X GET "${endpoint}/template/v1.0/RCS/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>

</details>

<a id="update-rcs-template"></a>
## RCSテンプレート修正 { #update-rcs-template }

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
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください",
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
| templateLanguage | String | N | テンプレート言語のタイプ<br>デフォルト値：PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarkerテンプレート)] |
| sender | Object | N |  |
| sender.brandId | String | Y | ブランドID |
| sender.chatbotId | String | Y | トークルーム(チャットボット)ID |
| content | Object | Y |  |
| content.messageType | String | N | RCS送信メッセージのタイプ<br>[SMS(ショートメッセージ)、LMS(ロングメッセージ)、MMS(マルチメディアメッセージ)、RBC_TEMPLATE(RCS Biz Centerテンプレート)] |
| content.title | String | N | メッセージ件名 |
| content.body | String | N | メッセージ本文 |
| content.smsType | String | X | SMSのタイプ<br>[STANDALONE(スタンドアロン型)、UNIFIED_STANDALONE(統合スタンドアロン型)] |
| content.lmsType | String | X | LMSのタイプ<br>[STANDALONE(スタンドアロン型)、FORMAT_BASIC(基本形式)、FORMAT_TITLE_HIGHLIGHT(タイトル強調形式)、FORMAT_PARAGRAPH(段落形式)、UNIFIED_STANDALONE(統合スタンドアロン型)] |
| content.mmsType | String | X | MMSのタイプ(MMS送信の場合は必須)<br>[HORIZONTAL(横型)、VERTICAL(縦型)、CAROUSEL_MEDIUM(カルーセル中型)、CAROUSEL_SMALL(カルーセル小型)、UNIFIED_HORIZONTAL(統合横型)、UNIFIED_VERTICAL(統合縦型)] |
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
| content.cards[].buttons[].buttonJson | Object | X | ボタン内容のJSONオブジェクト |
| content.buttons[].buttonJson | Object | N |  |
| content.buttons[].buttonJson.action | Object | N | ボタンアクション |



| content.buttons[].buttonType | String | X | COMPOSE(会話室を開く)、CLIPBOARD(コピーする)、DIALER(電話をかける)、MAP_SHOW(地図を表示する)、MAP_QUERY(地図を検索する)、MAP_SHARE(現在地を共有する)、URL(URLに接続する)、CALENDAR(スケジュールを登録する)<br>※ 統合メッセージタイプで CLIPBOARD(コピーする) ボタンを使用すると、iOS 端末では受信できません。<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | X | ボタン内容の JSON オブジェクト |
| content.buttons[].buttonJson.action | Object | X | ボタンアクション |
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
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください",
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
    "body" : "こんにちは。本日お客様の商品が入荷されました。ご来店ください",
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

</details>

<a id="delete-rcs-template"></a>
## RCSテンプレート削除 { #delete-rcs-template }

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

<a id="register-push-template"></a>
## Pushテンプレート登録 { #register-push-template }

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
| templateLanguage | String | N | テンプレート言語のタイプ<br>デフォルト値：PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarkerテンプレート)] |
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

<a id="list-push-templates"></a>
## Pushテンプレートリスト照会 { #list-push-templates }

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
| templates[].messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
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

<a id="get-push-template-details"></a>
## Pushテンプレート詳細照会 { #get-push-template-details }

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
| template.messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| template.messagePurpose | String | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL, AD, AUTH] |
| template.messagePurposes | Array |  |
| template.templateLanguage | String | テンプレート言語のタイプ<br>デフォルト値：PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarkerテンプレート)] |
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

<a id="update-push-template"></a>
## Pushテンプレート修正 { #update-push-template }

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
| templateLanguage | String | N | テンプレート言語のタイプ<br>デフォルト値：PLAIN_TEXT<br>[PLAIN_TEXT(プレーンテキスト)、FREEMARKER(FreeMarkerテンプレート)] |
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

<a id="delete-push-template"></a>
## Pushテンプレート削除 { #delete-push-template }

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

<a id="retrieve-template-parameters"></a>
## テンプレートパラメーター照会 { #retrieve-template-parameters }

テンプレートが含むパラメーターの一覧を照会します。

**リクエスト**

```
GET /template/v1.0/{messageChannel}/templates/{templateId}/parameters
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messageChannel | Path | Enum | O | メッセージチャンネルです。<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), RCS(RCS), EMAIL(メール), PUSH(プッシュ)] |
| templateId | Path | String | O | テンプレートID |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は「このAPIはリクエスト本文を必要としません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: `true` |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| templateParameter | Object | X | テンプレートパラメーター結果JSON |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### テンプレートパラメーター照会

GET {{endpoint}}/template/v1.0/{{messageChannel}}/templates/{{templateId}}/parameters
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/${messageChannel}/templates/${templateId}/parameters" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<a id="register-brand-message-template"></a>
## ブランドメッセージテンプレートの登録 { #register-brand-message-template }

テンプレートを登録します。

**リクエスト**

```
POST /template/v1.0/BRANDMESSAGE/templates
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
  "templateName" : "ブランドメッセージテンプレート",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a",
    "senderProfileType" : "NORMAL"
  },
  "content" : {
    "messageType" : "TEXT",
    "adult" : false,
    "header" : "ヘッダー",
    "content" : null,
    "additionalContent" : "価格情報",
    "image" : {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    },
    "carousel" : {
      "head" : {
        "header" : "イントロヘッダー",
        "content" : null,
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "additionalContent" : "価格情報",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg",
          "imageLink" : "https://www.example.com"
        },
        "commerce" : {
          "title" : "商品タイトル",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "buttons" : [ {
          "name" : "ボタン名",
          "type" : "WL",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android",
          "bizFormId" : 12345
        } ],
        "coupon" : {
          "title" : "5000円割引クーポン",
          "description" : "初回購入者限定",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "item" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "video" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    },
    "commerce" : {
      "title" : "商品タイトル",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "buttons" : [ {
      "name" : "ボタン名",
      "type" : "WL",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "coupon" : {
      "title" : "5000円割引クーポン",
      "description" : "初回購入者限定",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    }
  }
}
```

<!--リクエスト本文のフィールドについて説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | O | テンプレート名 |
| categoryId | String | X | カテゴリID |
| messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| sender | Object | O | 発信者情報 |
| sender.senderKey | String | O | 発信プロフィール発信キー(40文字) |
| sender.senderProfileType | String | O | 発信プロフィールタイプ(NORMAL: 一般、GROUP: グループ)<br>[GROUP, NORMAL] |
| content | Object | O | ブランドメッセージコンテンツ |
| content.messageType | String | O | ブランドメッセージ吹き出しタイプ。TEXT: テキスト型、IMAGE: イメージ型、WIDE: ワイドイメージ型、WIDE_ITEM_LIST: ワイドアイテムリスト型、CAROUSEL_FEED: カルーセルフィード型、CAROUSEL_COMMERCE: カルーセルコマース型、COMMERCE: コマース型、PREMIUM_VIDEO: プレミアムビデオ型<br>[TEXT, IMAGE, WIDE, WIDE_ITEM_LIST, CAROUSEL_FEED, PREMIUM_VIDEO, COMMERCE, CAROUSEL_COMMERCE] |
| content.adult | Boolean | X | 成人向けメッセージかどうか(デフォルト: false)。成人向け設定時は、成人認証を完了した受信者にのみ表示<br>デフォルト値: false |
| content.header | String | X | メッセージタイトル。WIDE_ITEM_LIST: 必須(最大20文字)、PREMIUM_VIDEO: 任意(最大20文字)。その他のタイプ: 使用不可 |
| content.content | String | X | テンプレート本文。TEXT: 必須（最大 1,300 文字、改行最大 99 個）、IMAGE: 必須（最大 1,300 文字）、WIDE: 必須（最大 76 文字、改行最大 5 個）、PREMIUM_VIDEO: 選択（最大 76 文字、改行最大 5 個）。WIDE_ITEM_LIST/CAROUSEL_FEED/CAROUSEL_COMMERCE: 使用不可。URL 入力可能 |
| content.additionalContent | String | X | 付加コンテンツ。COMMERCE タイプでのみ使用（選択、最大 34 文字）。CAROUSEL_COMMERCE はカルーセルアイテム内の additionalContent を使用 |
| content.image | Object | X | ブランドメッセージ画像。attachmentId と imageUrl のいずれか一方が必須 |
| content.image.attachmentId | String | X | 添付ファイル ID。attachmentId と imageUrl のいずれか一方を選択 |
| content.image.imageUrl | String | X | 画像 URL。attachmentId と imageUrl のいずれか一方を選択 |
| content.image.imageLink | String | X | 画像クリック時に遷移する URL（http/https）。選択。未設定の場合は KakaoTalk 画像ビューアーを使用 |
| content.carousel | Object | X | カルーセルメッセージ情報。CAROUSEL_FEED/CAROUSEL_COMMERCE タイプで必須 |
| content.carousel.head | Object | X | カルーセルイントロ領域。CAROUSEL_COMMERCE のみ使用可能（選択）。使用する場合は header、content、画像（image.attachmentId または image.imageUrl）が必須。head を使用する場合は list は 1〜5 個、未使用の場合は 2〜6 個 |
| content.carousel.head.header | String | X | イントロヘッダー。head 使用時は必須（最大 20 文字） |
| content.carousel.head.content | String | X | イントロ内容。head 使用時は必須（最大 50 文字） |
| content.carousel.head.image | Object | X | ブランドメッセージ画像。attachmentId と imageUrl のいずれか必須 |
| content.carousel.head.image.attachmentId | String | X | 添付ファイルID。attachmentId と imageUrl のいずれかを選択 |
| content.carousel.head.image.imageUrl | String | X | 画像 URL。attachmentId と imageUrl のいずれかを選択 |
| content.carousel.head.linkMo | String | X | イントロクリック時に移動するモバイル Web リンク。他のリンク（linkPc/schemeIos/schemeAndroid）を入力する場合は必須 |
| content.carousel.head.linkPc | String | X | イントロクリック時に移動する PC Web リンク。任意 |
| content.carousel.head.schemeIos | String | X | イントロクリック時に起動する iOS アプリリンク。任意 |
| content.carousel.head.schemeAndroid | String | X | イントロクリック時に起動する Android アプリリンク。任意 |
| content.carousel.list | Array | O | カルーセルアイテムのリスト。head 使用時は 1〜5 個、未使用時は 2〜6 個 |
| content.carousel.list[].header | String | X | カルーセルアイテムのタイトル。CAROUSEL_FEED: 必須（最大 20 文字）。CAROUSEL_COMMERCE: 使用不可 |
| content.carousel.list[].message | String | X | カルーセルアイテムのメッセージ。CAROUSEL_FEED: 必須（最大 180 文字）。CAROUSEL_COMMERCE: 使用不可 |
| content.carousel.list[].additionalContent | String | X | 追加コンテンツ。CAROUSEL_COMMERCE: 選択（最大 34 文字）。CAROUSEL_FEED: 使用不可 |
| content.carousel.list[].image | Object | X | ブランドメッセージ画像。attachmentId と imageUrl のいずれか一方が必須 |
| content.carousel.list[].image.attachmentId | String | X | 添付ファイル ID。attachmentId と imageUrl のいずれか一方を選択 |
| content.carousel.list[].image.imageUrl | String | X | 画像 URL。attachmentId と imageUrl のいずれか一方を選択 |
| content.carousel.list[].image.imageLink | String | X | 画像クリック時に移動する URL（http/https）。選択。未設定の場合は KakaoTalk 画像ビューアーを使用 |
| content.carousel.list[].commerce | Object | X | コマース情報。COMMERCE/CAROUSEL_COMMERCE タイプの場合は必須 |
| content.carousel.list[].commerce.title | String | O | 商品タイトル（最大 30 文字）。必須 |
| content.carousel.list[].commerce.regularPrice | Integer | O | 通常価格（0〜99,999,999）。必須 |
| content.carousel.list[].commerce.discountPrice | Integer | X | 割引後の価格（0〜99,999,999）。選択。使用する場合は discountRate または discountFixed のいずれか一方が必須 |
| content.carousel.list[].commerce.discountRate | Integer | X | 割引率（0〜100）。discountPrice が存在する場合、discountFixed とのいずれか一方を選択 |
| content.carousel.list[].commerce.discountFixed | Integer | X | 定額割引価格（0〜999,999）。discountPrice が存在する場合、discountRate とどちらか一方を選択 |
| content.carousel.list[].buttons | Array | O | カルーセルアイテムボタン。最小 1 個、最大 2 個必須。AC ボタンは最後の位置 |
| content.carousel.list[].buttons[].name | String | X | ボタン名。TEXT/IMAGE: 最大 14 文字、その他: 最大 8 文字。AC タイプ: 値なしで送信。BF タイプ: 「アンケートに参加する」「申し込む」「応募する」のいずれかを選択 |
| content.carousel.list[].buttons[].type | String | O | ボタンタイプ。WL: Web リンク、AL: アプリリンク、BK: ボットキーワード、MD: メッセージ転送、BC: 相談トーク切替、BT: チャットボット切替、BF: ビジネスフォーム、AC: チャンネル追加<br>[WL, AL, MD, BT, AC, BK, BF, BC] |
| content.carousel.list[].buttons[].linkMo | String | X | モバイル Web リンク（http/https）。WL タイプ必須、AL タイプ任意（schemeIos/schemeAndroid のいずれかと併せて入力する場合に必要） |
| content.carousel.list[].buttons[].linkPc | String | X | PC Web リンク（http/https）。WL/AL タイプ任意 |
| content.carousel.list[].buttons[].schemeIos | String | X | iOS アプリリンク。AL タイプ: linkMo、schemeAndroid、schemeIos のうち 2 つ以上必須 |
| content.carousel.list[].buttons[].schemeAndroid | String | X | Android アプリリンク。AL タイプ: linkMo、schemeAndroid、schemeIos のうち 2 つ以上必須 |
| content.carousel.list[].buttons[].bizFormId | Integer | X | ビジネスフォーム ID。BF タイプ必須 |
| content.carousel.list[].coupon | Object | X | クーポン情報。TEXT/IMAGE/WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO/COMMERCE: 任意。CAROUSEL_FEED/CAROUSEL_COMMERCE: カルーセルアイテム内で使用 |
| content.carousel.list[].coupon.title | String | O | クーポンタイトル。必須。形式：「{N}円割引クーポン」(N: 1〜99,999,999)、「{N}%割引クーポン」(N: 1〜100)、「送料割引クーポン」、「{商品名}無料クーポン」(商品名最大7文字)、「{商品名} UPクーポン」(商品名最大7文字)のいずれか1つを選択 |
| content.carousel.list[].coupon.description | String | O | クーポン詳細説明。必須。TEXT/IMAGE/COMMERCE: 最大12文字、WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO: 最大18文字 |
| content.carousel.list[].coupon.linkMo | String | X | クーポンクリック時に移動するモバイルWebリンク(http/https)。チャネルクーポンURLでない場合は必須 |
| content.carousel.list[].coupon.linkPc | String | X | クーポンクリック時に移動するPC Webリンク。任意 |
| content.carousel.list[].coupon.schemeIos | String | X | クーポンクリック時に起動するiOSアプリリンク。チャネルクーポンURLを使用する場合、schemeAndroidとともに1つ以上が必須 |
| content.carousel.list[].coupon.schemeAndroid | String | X | クーポンクリック時に起動するAndroidアプリリンク。チャネルクーポンURLを使用する場合、schemeIosとともに1つ以上が必須 |
| content.carousel.tail | Object | X | カルーセルのさらに見るボタンのリンク情報。任意。使用する場合はlinkMoが必須 |
| content.carousel.tail.linkMo | String | X | さらに見るボタンクリック時に移動するモバイルWebリンク(http/https)。tailを使用する場合は必須 |
| content.carousel.tail.linkPc | String | X | さらに見るボタンクリック時に移動するPC Webリンク。任意 |
| content.carousel.tail.schemeIos | String | X | さらに見るボタンクリック時に起動するiOSアプリリンク。任意 |
| content.carousel.tail.schemeAndroid | String | X | 「もっと見る」ボタンをクリックした際に実行する Android アプリリンク。選択 |
| content.item | Object | X | ワイドアイテムリスト型（WIDE_ITEM_LIST）のアイテム情報。WIDE_ITEM_LIST タイプの場合は必須 |
| content.item.list | Array | O | ワイドアイテムリスト。最小 3 個、最大 4 個 |
| content.item.list[].title | String | X | アイテムのタイトル（改行は最大 1 回）。1 番目のアイテム: 選択（最大 25 文字）、2〜4 番目のアイテム: 必須（最大 30 文字） |
| content.item.list[].image | Object | X | ブランドメッセージ画像。attachmentId と imageUrl のいずれか一方が必須 |
| content.item.list[].image.attachmentId | String | X | 添付ファイル ID。attachmentId と imageUrl のどちらか一方を選択 |
| content.item.list[].image.imageUrl | String | X | 画像 URL。attachmentId と imageUrl のどちらか一方を選択 |
| content.item.list[].linkMo | String | O | アイテムをクリックした際に遷移するモバイル Web リンク（http/https）。必須 |
| content.item.list[].linkPc | String | X | アイテムをクリックした際に遷移する PC Web リンク（http/https）。選択 |
| content.item.list[].schemeIos | String | X | アイテムをクリックした際に実行する iOS アプリリンク。選択 |
| content.item.list[].schemeAndroid | String | X | アイテムクリック時に実行する Android アプリリンク。選択 |
| content.video | Object | X | 動画情報。PREMIUM_VIDEO タイプ必須 |
| content.video.videoUrl | String | O | カカオTV 動画 URL（https://tv.kakao.com/ で始まる）。PREMIUM_VIDEO タイプ必須 |
| content.video.thumbnailUrl | String | X | 動画サムネイル画像 URL。選択。未設定時はカカオTV デフォルトサムネイルを使用 |
| content.commerce | Object | X | コマース情報。COMMERCE/CAROUSEL_COMMERCE タイプ必須 |
| content.commerce.title | String | O | 商品タイトル（最大 30 文字）。必須 |
| content.commerce.regularPrice | Integer | O | 通常価格（0〜99,999,999）。必須 |
| content.commerce.discountPrice | Integer | X | 割引後価格（0〜99,999,999）。選択。使用時は discountRate または discountFixed のいずれか一方が必須 |
| content.commerce.discountRate | Integer | X | 割引率（0〜100）。discountPrice が存在する場合、discountFixed と択一 |
| content.commerce.discountFixed | Integer | X | 定額割引価格（0〜999,999）。discountPrice が存在する場合、discountRate と択一 |
| content.buttons | Array | X | メッセージボタンリスト。TEXT/IMAGE: 最大5個（クーポン適用時は最大4個）、WIDE/WIDE_ITEM_LIST: 最大2個、PREMIUM_VIDEO: 最大1個、COMMERCE: 必須（最小1個、最大2個）。CAROUSEL_FEED/CAROUSEL_COMMERCE: カルーセルアイテム内の buttons を使用 |
| content.buttons[].name | String | X | ボタン名。TEXT/IMAGE: 最大14文字、その他: 最大8文字。AC タイプ: 値なしで送信。BF タイプ: 「アンケートに参加する」「申し込む」「応募する」のいずれか1つを選択 |
| content.buttons[].type | String | O | ボタンタイプ。WL: Webリンク、AL: アプリリンク、BK: ボットキーワード、MD: メッセージ転送、BC: 相談トーク切り替え、BT: チャットボット切り替え、BF: ビジネスフォーム、AC: チャンネル追加<br>[WL, AL, MD, BT, AC, BK, BF, BC] |
| content.buttons[].linkMo | String | X | モバイルWebリンク（http/https）。WL タイプは必須、AL タイプは任意（schemeIos/schemeAndroid のいずれかと併せて入力する場合に必要） |
| content.buttons[].linkPc | String | X | PC Webリンク（http/https）。WL/AL タイプは任意 |
| content.buttons[].schemeIos | String | X | iOS アプリリンク。AL タイプ: linkMo、schemeAndroid、schemeIos のうち2つ以上が必須 |
| content.buttons[].schemeAndroid | String | X | Android アプリリンク。AL タイプ: linkMo、schemeAndroid、schemeIos のうち2つ以上が必須 |
| content.buttons[].bizFormId | Integer | X | ビジネスフォーム ID。BF タイプは必須 |
| content.coupon | Object | X | クーポン情報。TEXT/IMAGE/WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO/COMMERCE: 任意。CAROUSEL_FEED/CAROUSEL_COMMERCE: カルーセルアイテム内で使用 |
| content.coupon.title | String | O | クーポンタイトル。必須。形式: 「{N}円割引クーポン」（N: 1〜99,999,999）、「{N}%割引クーポン」（N: 1〜100）、「送料割引クーポン」、「{商品名}無料クーポン」（商品名は最大7文字）、「{商品名} UP クーポン」（商品名は最大7文字）のいずれか1つを選択 |
| content.coupon.description | String | O | クーポンの詳細説明。必須。TEXT/IMAGE/COMMERCE: 最大 12 文字、WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO: 最大 18 文字 |
| content.coupon.linkMo | String | X | クーポンクリック時に移動するモバイル Web リンク (http/https)。チャンネルクーポン URL でない場合は必須 |
| content.coupon.linkPc | String | X | クーポンクリック時に移動する PC Web リンク。任意 |
| content.coupon.schemeIos | String | X | クーポンクリック時に起動する iOS アプリリンク。チャンネルクーポン URL 使用時は schemeAndroid とともに 1 つ以上必須 |
| content.coupon.schemeAndroid | String | X | クーポンクリック時に起動する Android アプリリンク。チャンネルクーポン URL 使用時は schemeIos とともに 1 つ以上必須 |

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

<!--レスポンス本文のフィールドについて説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| templateId | String | O | テンプレート登録時に発行されたテンプレートID |

**リクエスト例**

<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### ブランドメッセージテンプレート登録

POST {{endpoint}}/template/v1.0/BRANDMESSAGE/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "ブランドメッセージテンプレート",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a",
    "senderProfileType" : "NORMAL"
  },
  "content" : {
    "messageType" : "TEXT",
    "adult" : false,
    "header" : "ヘッダー",
    "content" : null,
    "additionalContent" : "価格情報",
    "image" : {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    },
    "carousel" : {
      "head" : {
        "header" : "イントロヘッダー",
        "content" : null,
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "additionalContent" : "価格情報",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg",
          "imageLink" : "https://www.example.com"
        },
        "commerce" : {
          "title" : "商品タイトル",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "buttons" : [ {
          "name" : "ボタン名",
          "type" : "WL",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android",
          "bizFormId" : 12345
        } ],
        "coupon" : {
          "title" : "5000円割引クーポン",
          "description" : "初回購入のお客様限定",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "item" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "video" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    },
    "commerce" : {
      "title" : "商品タイトル",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "buttons" : [ {
      "name" : "ボタン名",
      "type" : "WL",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "coupon" : {
      "title" : "5000円割引クーポン",
      "description" : "初回購入のお客様限定",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    }
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/BRANDMESSAGE/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "ブランドメッセージテンプレート",
  "categoryId" : "20230131070811m2fDe1rXx80",
  "messagePurpose" : "NORMAL",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a",
    "senderProfileType" : "NORMAL"
  },
  "content" : {
    "messageType" : "TEXT",
    "adult" : false,
    "header" : "ヘッダー",
    "content" : null,
    "additionalContent" : "価格情報",
    "image" : {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    },
    "carousel" : {
      "head" : {
        "header" : "イントロヘッダー",
        "content" : null,
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "additionalContent" : "価格情報",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg",
          "imageLink" : "https://www.example.com"
        },
        "commerce" : {
          "title" : "商品タイトル",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "buttons" : [ {
          "name" : "ボタン名",
          "type" : "WL",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android",
          "bizFormId" : 12345
        } ],
        "coupon" : {
          "title" : "5000円割引クーポン",
          "description" : "初回購入のお客様限定",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "item" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "video" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    },
    "commerce" : {
      "title" : "商品タイトル",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "buttons" : [ {
      "name" : "ボタン名",
      "type" : "WL",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "coupon" : {
      "title" : "5000円割引クーポン",
      "description" : "初回購入のお客様限定",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    }
  }
}'
```

</details>

<a id="list-brand-message-templates"></a>
## ブランドメッセージテンプレートリスト照会 { #list-brand-message-templates }

テンプレートリストを照会します。

**リクエスト**

```
GET /template/v1.0/BRANDMESSAGE/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| templateName | Query | String | X | テンプレート名 (LIKE 検索) |
| senderKey | Query | String | X | 発信キー |
| limit | Query | Number | X | limit を設定しない場合、デフォルト 20 (最大 1000) |
| offset | Query | Number | X | offset を設定しない場合、デフォルト 0 |



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

<!--レスポンス本文のフィールドについて説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| totalCount | Integer | O | 総件数 |
| templates | Array | O |  |
| templates[].templateId | String | O | テンプレート登録時に発行されたテンプレート ID |
| templates[].templateName | String | O | テンプレート名 |
| templates[].categoryId | String | O | カテゴリー ID |
| templates[].messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS)、ALIMTALK(お知らせトーク)、BRANDMESSAGE(ブランドメッセージ)、EMAIL(メール)、RCS(RCS)、PUSH(プッシュ)] |
| templates[].messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般)、AD(広告)、AUTH(認証)] |
| templates[].messagePurposes | Array | O |  |
| templates[].createdDateTime | String | O | テンプレート作成日時 |
| templates[].updatedDateTime | String | O | テンプレート更新日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### ブランドメッセージテンプレートリスト照会

GET {{endpoint}}/template/v1.0/BRANDMESSAGE/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/BRANDMESSAGE/templates" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<a id="get-brand-message-template-details"></a>
## ブランドメッセージテンプレート詳細照会 { #get-brand-message-template-details }

テンプレートを詳細照会します。

**リクエスト**

```
GET /template/v1.0/BRANDMESSAGE/templates/{templateId}
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
    "templateCode" : "TMPL_001",
    "templateName" : "ブランドメッセージテンプレート",
    "categoryId" : "20230131070811m2fDe1rXx80",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "messagePurposes" : [ "NORMAL" ],
    "sender" : {
      "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a",
      "senderProfileId" : "@nhnCloud",
      "senderProfileType" : "NORMAL"
    },
    "content" : {
      "messageType" : "TEXT",
      "adult" : false,
      "header" : "ヘッダー",
      "content" : null,
      "additionalContent" : "価格情報",
      "image" : {
        "attachmentId" : "20230131070811m2fDe1rXx80",
        "imageUrl" : "https://example.com/image.jpg",
        "imageLink" : "https://www.example.com"
      },
      "carousel" : {
        "head" : {
          "header" : "イントロヘッダー",
          "content" : null,
          "image" : {
            "attachmentId" : "20230131070811m2fDe1rXx80",
            "imageUrl" : "https://example.com/image.jpg"
          },
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        },
        "list" : [ {
          "header" : "Carousel Header",
          "message" : "Carousel Message",
          "additionalContent" : "価格情報",
          "image" : {
            "attachmentId" : "20230131070811m2fDe1rXx80",
            "imageUrl" : "https://example.com/image.jpg",
            "imageLink" : "https://www.example.com"
          },
          "commerce" : {
            "title" : "商品タイトル",
            "regularPrice" : 50000,
            "discountPrice" : 45000,
            "discountRate" : 10,
            "discountFixed" : 5000
          },
          "buttons" : [ {
            "name" : "ボタン名",
            "type" : "WL",
            "linkMo" : "https://m.example.com",
            "linkPc" : "https://www.example.com",
            "schemeIos" : "example://ios",
            "schemeAndroid" : "example://android",
            "bizFormId" : 12345
          } ],
          "coupon" : {
            "title" : "5000円割引クーポン",
            "description" : "初回購入者限定",
            "linkMo" : "https://m.example.com",
            "linkPc" : "https://www.example.com",
            "schemeIos" : "example://ios",
            "schemeAndroid" : "example://android"
          }
        } ],
        "tail" : {
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        }
      },
      "item" : {
        "list" : [ {
          "title" : "アイテムタイトル",
          "image" : {
            "attachmentId" : "20230131070811m2fDe1rXx80",
            "imageUrl" : "https://example.com/image.jpg"
          },
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        } ]
      },
      "video" : {
        "videoUrl" : "https://tv.kakao.com/v/123456789",
        "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
      },
      "commerce" : {
        "title" : "商品タイトル",
        "regularPrice" : 50000,
        "discountPrice" : 45000,
        "discountRate" : 10,
        "discountFixed" : 5000
      },
      "buttons" : [ {
        "name" : "ボタン名",
        "type" : "WL",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android",
        "bizFormId" : 12345
      } ],
      "coupon" : {
        "title" : "5000円割引クーポン",
        "description" : "初回購入者限定",
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "status" : "A",
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | X |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| template | Object | X |  |
| template.templateId | String | X | テンプレートID |
| template.templateCode | String | X | カカオテンプレートコード |
| template.templateName | String | X | テンプレート名 |
| template.categoryId | String | X | カテゴリーID |
| template.messageChannel | String | X | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| template.messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| template.messagePurposes | Array | X |  |
| template.sender | Object | X | ブランドメッセージ発信者情報 |
| template.sender.senderKey | String | O | 発信プロフィール発信キー(40文字)。グループ発信キーは使用不可 |
| template.sender.senderProfileId | String | X | カカオトークチャンネル名 |
| template.sender.senderProfileType | String | X | 発信プロフィールタイプ(NORMAL: 一般, GROUP: グループ)<br>[GROUP, NORMAL] |
| template.content | Object | X | ブランドメッセージコンテンツ |
| template.content.messageType | String | O | ブランドメッセージ吹き出しタイプ。TEXT: テキスト型、IMAGE: イメージ型、WIDE: ワイドイメージ型、WIDE_ITEM_LIST: ワイドアイテムリスト型、CAROUSEL_FEED: カルーセルフィード型、CAROUSEL_COMMERCE: カルーセルコマース型、COMMERCE: コマース型、PREMIUM_VIDEO: プレミアムビデオ型<br>[TEXT, IMAGE, WIDE, WIDE_ITEM_LIST, CAROUSEL_FEED, PREMIUM_VIDEO, COMMERCE, CAROUSEL_COMMERCE] |
| template.content.adult | Boolean | X | 成人向けメッセージかどうか(デフォルト: `false`)。成人向け設定時は成人認証を完了した受信者にのみ表示<br>デフォルト値: `false` |
| template.content.header | String | X | メッセージタイトル。WIDE_ITEM_LIST: 必須(最大20文字)、PREMIUM_VIDEO: 任意(最大20文字)。その他のタイプ: 使用不可 |
| template.content.content | String | X | テンプレート本文。TEXT: 必須(最大 1,300 文字、改行最大 99 個)、IMAGE: 必須(最大 1,300 文字)、WIDE: 必須(最大 76 文字、改行最大 5 個)、PREMIUM_VIDEO: 選択(最大 76 文字、改行最大 5 個)。WIDE_ITEM_LIST/CAROUSEL_FEED/CAROUSEL_COMMERCE: 使用不可。URL 入力可能 |
| template.content.additionalContent | String | X | 追加コンテンツ。COMMERCE タイプでのみ使用可能(選択、最大 34 文字)。CAROUSEL_COMMERCE はカルーセルアイテム内の additionalContent を使用 |
| template.content.image | Object | X | ブランドメッセージ画像。attachmentId と imageUrl のいずれか一方が必須 |
| template.content.image.attachmentId | String | X | 添付ファイル ID。attachmentId と imageUrl のいずれか一方を選択 |
| template.content.image.imageUrl | String | X | 画像 URL。attachmentId と imageUrl のいずれか一方を選択 |
| template.content.image.imageLink | String | X | 画像クリック時に遷移する URL(http/https)。選択。未設定の場合、カカオトーク画像ビューアーを使用 |
| template.content.carousel | Object | X | カルーセルメッセージ情報。CAROUSEL_FEED/CAROUSEL_COMMERCE タイプで必須 |
| template.content.carousel.head | Object | X | カルーセルイントロ領域。CAROUSEL_COMMERCE のみ使用可能(選択)。使用時は header、content、画像(image.attachmentId または image.imageUrl)が必須。head 使用時は list が 1〜5 個、未使用時は 2〜6 個 |
| template.content.carousel.head.header | String | X | イントロヘッダー。head 使用時に必須(最大 20 文字) |
| template.content.carousel.head.content | String | X | イントロ内容。head 使用時に必須(最大 50 文字) |
| template.content.carousel.head.image | Object | X | ブランドメッセージ画像。attachmentId と imageUrl のいずれか必須 |
| template.content.carousel.head.image.attachmentId | String | X | 添付ファイルID。attachmentId と imageUrl のいずれか1つを選択 |
| template.content.carousel.head.image.imageUrl | String | X | 画像 URL。attachmentId と imageUrl のいずれか1つを選択 |
| template.content.carousel.head.linkMo | String | X | イントロクリック時に遷移するモバイル Web リンク。他のリンク（linkPc/schemeIos/schemeAndroid）入力時は必須 |
| template.content.carousel.head.linkPc | String | X | イントロクリック時に遷移する PC Web リンク。任意 |
| template.content.carousel.head.schemeIos | String | X | イントロクリック時に起動する iOS アプリリンク。任意 |
| template.content.carousel.head.schemeAndroid | String | X | イントロクリック時に起動する Android アプリリンク。任意 |
| template.content.carousel.list | Array | O | カルーセルアイテムリスト。head 使用時は1〜5個、未使用時は2〜6個 |
| template.content.carousel.list[].header | String | X | カルーセルアイテムのタイトル。CAROUSEL_FEED: 必須（最大 20 文字）。CAROUSEL_COMMERCE: 使用不可 |
| template.content.carousel.list[].message | String | X | カルーセルアイテムのメッセージ。CAROUSEL_FEED: 必須（最大 180 文字）。CAROUSEL_COMMERCE: 使用不可 |
| template.content.carousel.list[].additionalContent | String | X | 追加コンテンツ。CAROUSEL_COMMERCE: 任意（最大 34 文字）。CAROUSEL_FEED: 使用不可 |
| template.content.carousel.list[].image | Object | X | ブランドメッセージ画像。attachmentId と imageUrl のいずれか一方が必須 |
| template.content.carousel.list[].image.attachmentId | String | X | 添付ファイル ID。attachmentId と imageUrl のいずれか一方を選択 |
| template.content.carousel.list[].image.imageUrl | String | X | 画像 URL。attachmentId と imageUrl のいずれか一方を選択 |
| template.content.carousel.list[].image.imageLink | String | X | 画像クリック時の遷移先 URL（http/https）。任意。未設定時は KakaoTalk 画像ビューアーを使用 |
| template.content.carousel.list[].commerce | Object | X | コマース情報。COMMERCE/CAROUSEL_COMMERCE タイプで必須 |
| template.content.carousel.list[].commerce.title | String | O | 商品タイトル（最大 30 文字）。必須 |
| template.content.carousel.list[].commerce.regularPrice | Integer | O | 通常価格（0〜99,999,999）。必須 |
| template.content.carousel.list[].commerce.discountPrice | Integer | X | 割引後価格（0〜99,999,999）。任意。使用する場合は discountRate または discountFixed のいずれか一方が必須 |
| template.content.carousel.list[].commerce.discountRate | Integer | X | 割引率（0〜100）。discountPrice が存在する場合は discountFixed のいずれか一方を選択 |
| template.content.carousel.list[].commerce.discountFixed | Integer | X | 定額割引価格（0〜999,999）。discountPrice が存在する場合、discountRate と択一 |
| template.content.carousel.list[].buttons | Array | O | カルーセルアイテムのボタン。最小 1 個、最大 2 個必須。AC ボタンは最後の位置 |
| template.content.carousel.list[].buttons[].name | String | X | ボタン名。TEXT/IMAGE: 最大 14 文字、その他: 最大 8 文字。AC タイプ: 値なしで送信。BF タイプ: 「アンケートに参加する」「申し込む」「応募する」のいずれか択一 |
| template.content.carousel.list[].buttons[].type | String | O | ボタンタイプ。WL: Web リンク、AL: アプリリンク、BK: ボットキーワード、MD: メッセージ転送、BC: 相談トーク転換、BT: チャットボット転換、BF: ビジネスフォーム、AC: チャンネル追加<br>[WL, AL, MD, BT, AC, BK, BF, BC] |
| template.content.carousel.list[].buttons[].linkMo | String | X | モバイル Web リンク（http/https）。WL タイプ必須、AL タイプ任意（schemeIos/schemeAndroid のいずれかと併せて入力する場合に必要） |
| template.content.carousel.list[].buttons[].linkPc | String | X | PC Web リンク（http/https）。WL/AL タイプ任意 |
| template.content.carousel.list[].buttons[].schemeIos | String | X | iOS アプリリンク。AL タイプ: linkMo、schemeAndroid、schemeIos のうち 2 つ以上必須 |
| template.content.carousel.list[].buttons[].schemeAndroid | String | X | Android アプリリンク。AL タイプ: linkMo、schemeAndroid、schemeIos のうち 2 つ以上必須 |
| template.content.carousel.list[].buttons[].bizFormId | Integer | X | ビジネスフォーム ID。BF タイプ必須 |
| template.content.carousel.list[].coupon | Object | X | クーポン情報。TEXT/IMAGE/WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO/COMMERCE: 任意。CAROUSEL_FEED/CAROUSEL_COMMERCE: カルーセルアイテム内で使用 |
| template.content.carousel.list[].coupon.title | String | O | クーポンタイトル。必須。形式: 「{N}円割引クーポン」(N: 1〜99,999,999)、「{N}%割引クーポン」(N: 1〜100)、「送料割引クーポン」、「{商品名}無料クーポン」(商品名最大7文字)、「{商品名} UPクーポン」(商品名最大7文字)のいずれか1つを選択 |
| template.content.carousel.list[].coupon.description | String | O | クーポンの詳細説明。必須。TEXT/IMAGE/COMMERCE: 最大12文字、WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO: 最大18文字 |
| template.content.carousel.list[].coupon.linkMo | String | X | クーポンクリック時に遷移するモバイルウェブリンク(http/https)。チャンネルクーポンURLでない場合は必須 |
| template.content.carousel.list[].coupon.linkPc | String | X | クーポンクリック時に遷移するPCウェブリンク。任意 |
| template.content.carousel.list[].coupon.schemeIos | String | X | クーポンクリック時に起動するiOSアプリリンク。チャンネルクーポンURL使用時はschemeAndroidとともに1つ以上必須 |
| template.content.carousel.list[].coupon.schemeAndroid | String | X | クーポンクリック時に起動するAndroidアプリリンク。チャンネルクーポンURL使用時はschemeIosとともに1つ以上必須 |
| template.content.carousel.tail | Object | X | カルーセルのもっと見るボタンリンク情報。任意。使用時はlinkMoが必須 |
| template.content.carousel.tail.linkMo | String | X | もっと見るボタンクリック時に遷移するモバイルウェブリンク(http/https)。tail使用時は必須 |
| template.content.carousel.tail.linkPc | String | X | もっと見るボタンクリック時に遷移するPCウェブリンク。任意 |
| template.content.carousel.tail.schemeIos | String | X | もっと見るボタンクリック時に起動するiOSアプリリンク。任意 |
| template.content.carousel.tail.schemeAndroid | String | X | 「もっと見る」ボタンクリック時に実行する Android アプリリンク。選択 |
| template.content.item | Object | X | ワイドアイテムリスト型 (WIDE_ITEM_LIST) のアイテム情報。WIDE_ITEM_LIST タイプ必須 |
| template.content.item.list | Array | O | ワイドアイテムリスト。最小 3 個、最大 4 個 |
| template.content.item.list[].title | String | X | アイテムタイトル (改行最大 1 個)。1 番目のアイテム: 選択 (最大 25 文字)、2〜4 番目のアイテム: 必須 (最大 30 文字) |
| template.content.item.list[].image | Object | X | ブランドメッセージ画像。attachmentId と imageUrl のいずれか必須 |
| template.content.item.list[].image.attachmentId | String | X | 添付ファイル ID。attachmentId と imageUrl のいずれか 1 つを選択 |
| template.content.item.list[].image.imageUrl | String | X | 画像 URL。attachmentId と imageUrl のいずれか 1 つを選択 |
| template.content.item.list[].linkMo | String | O | アイテムクリック時に移動するモバイル Web リンク (http/https)。必須 |
| template.content.item.list[].linkPc | String | X | アイテムクリック時に移動する PC Web リンク (http/https)。選択 |
| template.content.item.list[].schemeIos | String | X | アイテムクリック時に実行する iOS アプリリンク。選択 |
| template.content.item.list[].schemeAndroid | String | X | アイテムクリック時に実行する Android アプリリンク。選択 |
| template.content.video | Object | X | 動画情報。PREMIUM_VIDEO タイプ必須 |
| template.content.video.videoUrl | String | O | カカオ TV 動画 URL（https://tv.kakao.com/ で始まる）。PREMIUM_VIDEO タイプ必須 |
| template.content.video.thumbnailUrl | String | X | 動画サムネイル画像 URL。選択。未設定の場合はカカオ TV デフォルトサムネイルを使用 |
| template.content.commerce | Object | X | コマース情報。COMMERCE/CAROUSEL_COMMERCE タイプ必須 |
| template.content.commerce.title | String | O | 商品タイトル（最大 30 文字）。必須 |
| template.content.commerce.regularPrice | Integer | O | 通常価格（0〜99,999,999）。必須 |
| template.content.commerce.discountPrice | Integer | X | 割引後価格（0〜99,999,999）。選択。使用する場合は discountRate または discountFixed のいずれか一方が必須 |
| template.content.commerce.discountRate | Integer | X | 割引率（0〜100）。discountPrice が存在する場合は discountFixed とどちらか一方を選択 |
| template.content.commerce.discountFixed | Integer | X | 定額割引価格（0〜999,999）。discountPrice が存在する場合は discountRate とどちらか一方を選択 |
| template.content.buttons | Array | X | メッセージボタンのリスト。TEXT/IMAGE: 最大5個（クーポン適用時は最大4個）、WIDE/WIDE_ITEM_LIST: 最大2個、PREMIUM_VIDEO: 最大1個、COMMERCE: 必須（最小1個、最大2個）。CAROUSEL_FEED/CAROUSEL_COMMERCE: カルーセルアイテム内の buttons を使用 |
| template.content.buttons[].name | String | X | ボタン名。TEXT/IMAGE: 最大14文字、その他: 最大8文字。AC タイプ: 値なしで送信。BF タイプ: 「アンケートに参加する」「申請する」「応募する」のいずれか1つを選択 |
| template.content.buttons[].type | String | O | ボタンタイプ。WL: Webリンク、AL: アプリリンク、BK: ボットキーワード、MD: メッセージ転送、BC: 相談トーク切り替え、BT: チャットボット切り替え、BF: ビジネスフォーム、AC: チャンネル追加<br>[WL, AL, MD, BT, AC, BK, BF, BC] |
| template.content.buttons[].linkMo | String | X | モバイルWebリンク（http/https）。WL タイプは必須、AL タイプは任意（schemeIos/schemeAndroid のいずれかと組み合わせて入力する場合に必要） |
| template.content.buttons[].linkPc | String | X | PC Webリンク（http/https）。WL/AL タイプは任意 |
| template.content.buttons[].schemeIos | String | X | iOS アプリリンク。AL タイプ: linkMo、schemeAndroid、schemeIos のうち2つ以上が必須 |
| template.content.buttons[].schemeAndroid | String | X | Android アプリリンク。AL タイプ: linkMo、schemeAndroid、schemeIos のうち2つ以上が必須 |
| template.content.buttons[].bizFormId | Integer | X | ビジネスフォーム ID。BF タイプは必須 |
| template.content.coupon | Object | X | クーポン情報。TEXT/IMAGE/WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO/COMMERCE: 任意。CAROUSEL_FEED/CAROUSEL_COMMERCE: カルーセルアイテム内で使用 |
| template.content.coupon.title | String | O | クーポンタイトル。必須。形式: 「{N}円割引クーポン」（N: 1〜99,999,999）、「{N}%割引クーポン」（N: 1〜100）、「送料割引クーポン」、「{商品名}無料クーポン」（商品名最大7文字）、「{商品名} UPクーポン」（商品名最大7文字）のいずれか1つを選択 |
| template.content.coupon.description | String | O | クーポンの詳細説明。必須。TEXT/IMAGE/COMMERCE: 最大 12 文字、WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO: 最大 18 文字 |
| template.content.coupon.linkMo | String | X | クーポンクリック時に移動するモバイル Web リンク (http/https)。チャンネルクーポン URL 以外の場合は必須 |
| template.content.coupon.linkPc | String | X | クーポンクリック時に移動する PC Web リンク。任意 |
| template.content.coupon.schemeIos | String | X | クーポンクリック時に起動する iOS アプリリンク。チャンネルクーポン URL 使用時は schemeAndroid とともに 1 つ以上必須 |
| template.content.coupon.schemeAndroid | String | X | クーポンクリック時に起動する Android アプリリンク。チャンネルクーポン URL 使用時は schemeIos とともに 1 つ以上必須 |
| template.status | String | X | テンプレートステータス。A: 登録済み (Active)、S: ブロック (Stopped)<br>[A, S] |
| template.createdDateTime | String | X | テンプレート作成日時 |
| template.updatedDateTime | String | X | テンプレート更新日時 |

**リクエスト例**

<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### ブランドメッセージテンプレート詳細照会

GET {{endpoint}}/template/v1.0/BRANDMESSAGE/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/BRANDMESSAGE/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<a id="modify-brand-message-template"></a>
## ブランドメッセージテンプレートの修正 { #modify-brand-message-template }

テンプレートを修正します。

**リクエスト**

```
PUT /template/v1.0/BRANDMESSAGE/templates/{templateId}
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

```
{
  "templateName" : "ブランドメッセージテンプレート修正",
  "messagePurpose" : "NORMAL",
  "content" : {
    "messageType" : "TEXT",
    "adult" : false,
    "header" : "ヘッダー",
    "content" : null,
    "additionalContent" : "価格情報",
    "image" : {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    },
    "carousel" : {
      "head" : {
        "header" : "イントロヘッダー",
        "content" : null,
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "additionalContent" : "価格情報",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg",
          "imageLink" : "https://www.example.com"
        },
        "commerce" : {
          "title" : "商品タイトル",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "buttons" : [ {
          "name" : "ボタン名",
          "type" : "WL",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android",
          "bizFormId" : 12345
        } ],
        "coupon" : {
          "title" : "5000円割引クーポン",
          "description" : "初回購入のお客様限定",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "item" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "video" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    },
    "commerce" : {
      "title" : "商品タイトル",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "buttons" : [ {
      "name" : "ボタン名",
      "type" : "WL",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "coupon" : {
      "title" : "5000円割引クーポン",
      "description" : "初回購入のお客様限定",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    }
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

| 経路 | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateName | String | O | テンプレート名 |
| messagePurpose | String | X | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| content | Object | O | ブランドメッセージコンテンツ |
| content.messageType | String | O | ブランドメッセージ吹き出しタイプ。TEXT: テキスト型、IMAGE: 画像型、WIDE: ワイド画像型、WIDE_ITEM_LIST: ワイドアイテムリスト型、CAROUSEL_FEED: カルーセルフィード型、CAROUSEL_COMMERCE: カルーセルコマース型、COMMERCE: コマース型、PREMIUM_VIDEO: プレミアムビデオ型<br>[TEXT, IMAGE, WIDE, WIDE_ITEM_LIST, CAROUSEL_FEED, PREMIUM_VIDEO, COMMERCE, CAROUSEL_COMMERCE] |
| content.adult | Boolean | X | 成人向けメッセージかどうか（デフォルト: `false`）。成人向けに設定した場合、成人認証を完了した受信者にのみ表示<br>デフォルト値: `false` |
| content.header | String | X | メッセージタイトル。WIDE_ITEM_LIST: 必須（最大 20 文字）、PREMIUM_VIDEO: 任意（最大 20 文字）。その他のタイプ: 使用不可 |
| content.content | String | X | テンプレート本文。TEXT: 必須（最大 1,300 文字、改行最大 99 個）、IMAGE: 必須（最大 1,300 文字）、WIDE: 必須（最大 76 文字、改行最大 5 個）、PREMIUM_VIDEO: 任意（最大 76 文字、改行最大 5 個）。WIDE_ITEM_LIST/CAROUSEL_FEED/CAROUSEL_COMMERCE: 使用不可。URL 入力可能 |
| content.additionalContent | String | X | 追加コンテンツ。COMMERCE タイプのみ使用可能（任意、最大 34 文字）。CAROUSEL_COMMERCE はカルーセルアイテム内の additionalContent を使用 |
| content.image | Object | X | ブランドメッセージ画像。attachmentId と imageUrl のいずれか一方が必須 |
| content.image.attachmentId | String | X | 添付ファイル ID。attachmentId と imageUrl のいずれか一方を選択 |
| content.image.imageUrl | String | X | 画像 URL。attachmentId と imageUrl のいずれか1つを選択 |
| content.image.imageLink | String | X | 画像クリック時に移動する URL（http/https）。任意。未設定の場合は KakaoTalk 画像ビューアーを使用 |
| content.carousel | Object | X | カルーセルメッセージ情報。CAROUSEL_FEED/CAROUSEL_COMMERCE タイプで必須 |
| content.carousel.head | Object | X | カルーセルイントロ領域。CAROUSEL_COMMERCE のみ使用可能（任意）。使用時は header、content、画像（image.attachmentId または image.imageUrl）が必須。head 使用時は list が1〜5個、未使用時は2〜6個 |
| content.carousel.head.header | String | X | イントロヘッダー。head 使用時は必須（最大20文字） |
| content.carousel.head.content | String | X | イントロ内容。head 使用時は必須（最大50文字） |
| content.carousel.head.image | Object | X | ブランドメッセージ画像。attachmentId と imageUrl のいずれか1つが必須 |
| content.carousel.head.image.attachmentId | String | X | 添付ファイル ID。attachmentId と imageUrl のいずれか1つを選択 |
| content.carousel.head.image.imageUrl | String | X | 画像 URL。attachmentId と imageUrl のいずれか1つを選択 |
| content.carousel.head.linkMo | String | X | イントロクリック時に移動するモバイル Web リンク。他のリンク（linkPc/schemeIos/schemeAndroid）を入力する場合は必須 |
| content.carousel.head.linkPc | String | X | イントロクリック時に移動する PC ウェブリンク。選択 |
| content.carousel.head.schemeIos | String | X | イントロクリック時に実行する iOS アプリリンク。選択 |
| content.carousel.head.schemeAndroid | String | X | イントロクリック時に実行する Android アプリリンク。選択 |
| content.carousel.list | Array | O | カルーセルアイテムの一覧。head 使用時は 1〜5 個、未使用時は 2〜6 個 |
| content.carousel.list[].header | String | X | カルーセルアイテムのタイトル。CAROUSEL_FEED: 必須（最大 20 文字）。CAROUSEL_COMMERCE: 使用不可 |
| content.carousel.list[].message | String | X | カルーセルアイテムのメッセージ。CAROUSEL_FEED: 必須（最大 180 文字）。CAROUSEL_COMMERCE: 使用不可 |
| content.carousel.list[].additionalContent | String | X | 付加コンテンツ。CAROUSEL_COMMERCE: 選択（最大 34 文字）。CAROUSEL_FEED: 使用不可 |
| content.carousel.list[].image | Object | X | ブランドメッセージ画像。attachmentId と imageUrl のいずれか一方が必須 |
| content.carousel.list[].image.attachmentId | String | X | 添付ファイル ID。attachmentId と imageUrl のいずれかを選択 |
| content.carousel.list[].image.imageUrl | String | X | 画像 URL。attachmentId と imageUrl のいずれかを選択 |
| content.carousel.list[].image.imageLink | String | X | 画像クリック時に移動する URL (http/https)。選択。未設定の場合は KakaoTalk 画像ビューアーを使用 |
| content.carousel.list[].commerce | Object | X | コマース情報。COMMERCE/CAROUSEL_COMMERCE タイプ必須 |
| content.carousel.list[].commerce.title | String | O | 商品タイトル（最大 30 文字）。必須 |
| content.carousel.list[].commerce.regularPrice | Integer | O | 通常価格（0〜99,999,999）。必須 |
| content.carousel.list[].commerce.discountPrice | Integer | X | 割引後価格（0〜99,999,999）。選択。使用時は discountRate または discountFixed のいずれか必須 |
| content.carousel.list[].commerce.discountRate | Integer | X | 割引率（0〜100）。discountPrice が存在する場合は discountFixed と択一 |
| content.carousel.list[].commerce.discountFixed | Integer | X | 定額割引価格（0〜999,999）。discountPrice が存在する場合は discountRate と択一 |
| content.carousel.list[].buttons | Array | O | カルーセルアイテムボタン。最小 1 個、最大 2 個必須。AC ボタンは最後の位置 |
| content.carousel.list[].buttons[].name | String | X | ボタン名。TEXT/IMAGE: 最大 14 文字、その他: 最大 8 文字。AC タイプ: 値なしで送信。BF タイプ: 「설문 참여하기」「신청하기」「응모하기」のいずれか択一 |
| content.carousel.list[].buttons[].type | String | O | ボタンタイプ。WL: Web リンク、AL: アプリリンク、BK: ボットキーワード、MD: メッセージ転達、BC: 相談トーク転換、BT: チャットボット転換、BF: ビジネスフォーム、AC: チャンネル追加<br>[WL, AL, MD, BT, AC, BK, BF, BC] |
| content.carousel.list[].buttons[].linkMo | String | X | モバイル Web リンク（http/https）。WL タイプ必須、AL タイプ選択（schemeIos/schemeAndroid のいずれかと併せて入力する場合に必要） |
| content.carousel.list[].buttons[].linkPc | String | X | PC Web リンク（http/https）。WL/AL タイプ選択 |
| content.carousel.list[].buttons[].schemeIos | String | X | iOS アプリリンク。AL タイプ：linkMo、schemeAndroid、schemeIos のうち 2 つ以上必須 |
| content.carousel.list[].buttons[].schemeAndroid | String | X | Android アプリリンク。AL タイプ：linkMo、schemeAndroid、schemeIos のうち 2 つ以上必須 |
| content.carousel.list[].buttons[].bizFormId | Integer | X | ビジネスフォーム ID。BF タイプ必須 |
| content.carousel.list[].coupon | Object | X | クーポン情報。TEXT/IMAGE/WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO/COMMERCE：選択。CAROUSEL_FEED/CAROUSEL_COMMERCE：カルーセルアイテム内で使用 |
| content.carousel.list[].coupon.title | String | O | クーポンタイトル。必須。形式：「{N}円割引クーポン」（N：1〜99,999,999）、「{N}%割引クーポン」（N：1〜100）、「送料割引クーポン」、「{商品名}無料クーポン」（商品名最大 7 文字）、「{商品名} UP クーポン」（商品名最大 7 文字）のいずれか 1 つ |
| content.carousel.list[].coupon.description | String | O | クーポン詳細説明。必須。TEXT/IMAGE/COMMERCE：最大 12 文字、WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO：最大 18 文字 |
| content.carousel.list[].coupon.linkMo | String | X | クーポンクリック時に遷移するモバイル Web リンク（http/https）。チャンネルクーポン URL でない場合は必須 |
| content.carousel.list[].coupon.linkPc | String | X | クーポンクリック時に遷移する PC Web リンク。選択 |
| content.carousel.list[].coupon.schemeIos | String | X | クーポンクリック時に起動する iOS アプリリンク。チャンネルクーポン URL 使用時は schemeAndroid とともに1つ以上必須 |
| content.carousel.list[].coupon.schemeAndroid | String | X | クーポンクリック時に起動するAndroidアプリリンク。チャンネルクーポン URL 使用時は schemeIos とともに1つ以上必須 |
| content.carousel.tail | Object | X | カルーセルのもっと見るボタンのリンク情報。任意。使用時は linkMo 必須 |
| content.carousel.tail.linkMo | String | X | もっと見るボタンクリック時に遷移するモバイル Web リンク（http/https）。tail 使用時は必須 |
| content.carousel.tail.linkPc | String | X | もっと見るボタンクリック時に遷移する PC Web リンク。任意 |
| content.carousel.tail.schemeIos | String | X | もっと見るボタンクリック時に起動する iOS アプリリンク。任意 |
| content.carousel.tail.schemeAndroid | String | X | もっと見るボタンクリック時に起動するAndroidアプリリンク。任意 |
| content.item | Object | X | ワイドアイテムリスト型（WIDE_ITEM_LIST）のアイテム情報。WIDE_ITEM_LIST タイプ必須 |
| content.item.list | Array | O | ワイドアイテムの一覧。最小3件、最大4件 |
| content.item.list[].title | String | X | アイテムのタイトル（改行最大1回）。1番目のアイテム：任意（最大25文字）、2〜4番目のアイテム：必須（最大30文字） |
| content.item.list[].image | Object | X | ブランドメッセージ画像。attachmentId と imageUrl のいずれか必須 |
| content.item.list[].image.attachmentId | String | X | 添付ファイルID。attachmentId と imageUrl のいずれかを選択 |
| content.item.list[].image.imageUrl | String | X | 画像 URL。attachmentId と imageUrl のいずれかを選択 |
| content.item.list[].linkMo | String | O | アイテムクリック時に遷移するモバイルウェブリンク (http/https)。必須 |
| content.item.list[].linkPc | String | X | アイテムクリック時に遷移する PC ウェブリンク (http/https)。任意 |
| content.item.list[].schemeIos | String | X | アイテムクリック時に起動する iOS アプリリンク。任意 |
| content.item.list[].schemeAndroid | String | X | アイテムクリック時に起動する Android アプリリンク。任意 |
| content.video | Object | X | 動画情報。PREMIUM_VIDEO タイプで必須 |
| content.video.videoUrl | String | O | カカオ TV 動画 URL (https://tv.kakao.com/ から始まる)。PREMIUM_VIDEO タイプで必須 |
| content.video.thumbnailUrl | String | X | 動画サムネイル画像 URL。任意。未設定時はカカオ TV のデフォルトサムネイルを使用 |
| content.commerce | Object | X | コマース情報。COMMERCE/CAROUSEL_COMMERCE タイプ必須 |
| content.commerce.title | String | O | 商品タイトル（最大 30 文字）。必須 |
| content.commerce.regularPrice | Integer | O | 通常価格（0〜99,999,999）。必須 |
| content.commerce.discountPrice | Integer | X | 割引後価格（0〜99,999,999）。任意。使用する場合は discountRate または discountFixed のいずれかが必須 |
| content.commerce.discountRate | Integer | X | 割引率（0〜100）。discountPrice が存在する場合、discountFixed といずれか一方を選択 |
| content.commerce.discountFixed | Integer | X | 定額割引価格（0〜999,999）。discountPrice が存在する場合、discountRate といずれか一方を選択 |
| content.buttons | Array | X | メッセージボタンリスト。TEXT/IMAGE: 最大 5 個（クーポン適用時は最大 4 個）、WIDE/WIDE_ITEM_LIST: 最大 2 個、PREMIUM_VIDEO: 最大 1 個、COMMERCE: 必須（最小 1 個、最大 2 個）。CAROUSEL_FEED/CAROUSEL_COMMERCE: カルーセルアイテム内の buttons を使用 |
| content.buttons[].name | String | X | ボタン名。TEXT/IMAGE: 最大 14 文字、その他: 最大 8 文字。AC タイプ: 値なしで送信。BF タイプ: 「アンケートに参加する」「申し込む」「応募する」のいずれかを選択 |
| content.buttons[].type | String | O | ボタンタイプ。WL: Web リンク、AL: アプリリンク、BK: ボットキーワード、MD: メッセージ転送、BC: 相談トーク転換、BT: チャットボット転換、BF: ビジネスフォーム、AC: チャンネル追加<br>[WL, AL, MD, BT, AC, BK, BF, BC] |
| content.buttons[].linkMo | String | X | モバイル Web リンク（http/https）。WL タイプ必須、AL タイプ任意（schemeIos/schemeAndroid のいずれかと併せて入力する場合に必要） |
| content.buttons[].linkPc | String | X | PC Webリンク（http/https）。WL/AL タイプ選択 |
| content.buttons[].schemeIos | String | X | iOS アプリリンク。AL タイプ: linkMo、schemeAndroid、schemeIos のうち2つ以上必須 |
| content.buttons[].schemeAndroid | String | X | Android アプリリンク。AL タイプ: linkMo、schemeAndroid、schemeIos のうち2つ以上必須 |
| content.buttons[].bizFormId | Integer | X | ビジネスフォーム ID。BF タイプ必須 |
| content.coupon | Object | X | クーポン情報。TEXT/IMAGE/WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO/COMMERCE: 任意。CAROUSEL_FEED/CAROUSEL_COMMERCE: カルーセルアイテム内で使用 |
| content.coupon.title | String | O | クーポンタイトル。必須。形式: 「{N}円割引クーポン」（N: 1〜99,999,999）、「{N}%割引クーポン」（N: 1〜100）、「送料割引クーポン」、「{商品名}無料クーポン」（商品名最大7文字）、「{商品名} UPクーポン」（商品名最大7文字）のいずれか1つ |
| content.coupon.description | String | O | クーポン詳細説明。必須。TEXT/IMAGE/COMMERCE: 最大12文字、WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO: 最大18文字 |
| content.coupon.linkMo | String | X | クーポンクリック時に遷移するモバイル Web リンク（http/https）。チャンネルクーポン URL 以外の場合は必須 |
| content.coupon.linkPc | String | X | クーポンクリック時に遷移する PC Web リンク。任意 |
| content.coupon.schemeIos | String | X | クーポンクリック時に起動する iOS アプリリンク。チャンネルクーポン URL 使用時は schemeAndroid とともに1つ以上必須 |
| content.coupon.schemeAndroid | String | X | クーポンをクリックしたときに実行する Android アプリリンク。チャンネルクーポン URL を使用する場合、schemeIos とともに少なくとも 1 つ必須 |

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
### ブランドメッセージテンプレート修正

PUT {{endpoint}}/template/v1.0/BRANDMESSAGE/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "templateName" : "ブランドメッセージテンプレート修正",
  "messagePurpose" : "NORMAL",
  "content" : {
    "messageType" : "TEXT",
    "adult" : false,
    "header" : "ヘッダー",
    "content" : null,
    "additionalContent" : "価格情報",
    "image" : {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    },
    "carousel" : {
      "head" : {
        "header" : "イントロヘッダー",
        "content" : null,
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "additionalContent" : "価格情報",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg",
          "imageLink" : "https://www.example.com"
        },
        "commerce" : {
          "title" : "商品タイトル",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "buttons" : [ {
          "name" : "ボタン名",
          "type" : "WL",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android",
          "bizFormId" : 12345
        } ],
        "coupon" : {
          "title" : "5000円割引クーポン",
          "description" : "初回購入のお客様限定",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "item" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "video" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    },
    "commerce" : {
      "title" : "商品タイトル",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "buttons" : [ {
      "name" : "ボタン名",
      "type" : "WL",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "coupon" : {
      "title" : "5000円割引クーポン",
      "description" : "初回購入のお客様限定",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    }
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/BRANDMESSAGE/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "templateName" : "ブランドメッセージテンプレート修正",
  "messagePurpose" : "NORMAL",
  "content" : {
    "messageType" : "TEXT",
    "adult" : false,
    "header" : "ヘッダー",
    "content" : null,
    "additionalContent" : "価格情報",
    "image" : {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    },
    "carousel" : {
      "head" : {
        "header" : "イントロヘッダー",
        "content" : null,
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "additionalContent" : "価格情報",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg",
          "imageLink" : "https://www.example.com"
        },
        "commerce" : {
          "title" : "商品タイトル",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "buttons" : [ {
          "name" : "ボタン名",
          "type" : "WL",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android",
          "bizFormId" : 12345
        } ],
        "coupon" : {
          "title" : "5000円割引クーポン",
          "description" : "初回購入のお客様限定",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "item" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "video" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    },
    "commerce" : {
      "title" : "商品タイトル",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "buttons" : [ {
      "name" : "ボタン名",
      "type" : "WL",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormId" : 12345
    } ],
    "coupon" : {
      "title" : "5000円割引クーポン",
      "description" : "初回購入のお客様限定",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    }
  }
}'
```

</details>

<a id="delete-brand-message-template"></a>
## ブランドメッセージテンプレート削除 { #delete-brand-message-template }

テンプレートを削除します。

**リクエスト**

```
DELETE /template/v1.0/BRANDMESSAGE/templates/{templateId}
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

<!--リクエスト本文を必要としない場合は「このAPIはリクエスト本文を必要としません」と入力します。-->

このAPIはリクエスト本文を必要としません。



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

<!--レスポンス本文のフィールドについて説明します。-->

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
### ブランドメッセージテンプレートの削除

DELETE {{endpoint}}/template/v1.0/BRANDMESSAGE/templates/{{templateId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/BRANDMESSAGE/templates/${templateId}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
