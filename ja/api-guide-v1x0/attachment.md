<!-- 新しい書式のために追加されたstyleです。 -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 新しい書式のために見出しを<h1>に変更しました。 -->
<h1>添付ファイル</h1>

**Notification > Notification Hub > API v1.0 使用ガイド > 添付ファイル**



<span id="attachmentV1x0001UploadAttachments"></span>

## 添付ファイルのアップロード

添付ファイルをアップロードします。FileTypeを指定した場合、個別商品に対する添付ファイルのアップロードを実行します。

**リクエスト**

```
POST /attachment/v1.0/attachments
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |



**リクエスト本文**

<!-- リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->

| パス | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| file | Binary | Y | アップロードするファイル |
| fileName | String | Y | ファイル名 |
| fileTypes | Array | N | アップロードするファイルタイプ |


**レスポンス本文**

<!-- レスポンス本文を返却しない場合は「このAPIはレスポンス本文を返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "attachmentId" : "20230131070811m2fDe1rXx80",
  "results" : [ {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  } ]
}
```

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 作業の成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| attachmentId | String | 添付ファイルIDです。 |
| results | Array |  |
| results[].isSuccessful | Boolean | 作業の成否を示します。<br>デフォルト値：true |
| results[].resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| results[].resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 添付ファイルのアップロード

POST {{endpoint}}/attachment/v1.0/attachments
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/attachment/v1.0/attachments" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="attachmentV1x0002ReadAttachments"></span>

## 添付ファイル一覧照会

添付ファイルの一覧を返します。

**リクエスト**

```
GET /attachment/v1.0/attachments
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| messageChannel | Query | V1x0MessageChannel | N | メッセージチャネル |
| fileType | Query | V1x0FileType | N | ファイルタイプ |
| fileName | Query | String | N | ファイル名 |
| limit | Query | Integer | N | limitを設定しない場合はデフォルト50 (最大1000) |
| offset | Query | Integer | N | offsetを設定しない場合はデフォルト0 |



**リクエスト本文**

<!-- リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->

このAPIはリクエスト本文を要求しません。



**レスポンス本文**

<!-- レスポンス本文を返却しない場合は「このAPIはレスポンス本文を返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 120,
  "attachments" : [ {
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "fileName" : "test.txt",
    "fileFormat" : "JPG",
    "fileSizeByte" : 21391,
    "createDateTime" : "2024-10-29T06:00:01.000+09:00",
    "expireDateTime" : "2024-10-29T06:00:01.000+09:00",
    "uploadedFileTypes" : [ "EMAIL_DEFAULT" ]
  } ]
}
```

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 作業の成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| totalCount | Integer | 総添付ファイル数 |
| attachments | Array | 添付ファイル一覧 |
| attachments[].attachmentId | String | ファイルのアップロード成功時に作成されるファイル固有ID |
| attachments[].fileName | String | アップロードファイル名 |
| attachments[].fileFormat | String | ファイル形式 |
| attachments[].fileSizeByte | Long | 添付ファイルのサイズ単位はbyte |
| attachments[].createDateTime | String | ファイルアップロード日時 |
| attachments[].expireDateTime | String | ファイル有効期限 |
| attachments[].uploadedFileTypes | Array | 個別商品にアップロードされたファイルタイプ一覧 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 添付ファイル一覧照会

GET {{endpoint}}/attachment/v1.0/attachments
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/attachment/v1.0/attachments" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="attachmentV1x0003ReadAttachment"></span>

## 添付ファイル単件照会

添付ファイルIDで添付ファイルを照会します。


**リクエスト**

```
GET /attachment/v1.0/attachments/{attachmentId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| attachmentId | Path | String | Y | 添付ファイルID |



**リクエスト本文**

<!-- リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->

このAPIはリクエスト本文を要求しません。



**レスポンス本文**

<!-- レスポンス本文を返却しない場合は「このAPIはレスポンス本文を返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "attachment" : {
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "fileName" : "test.txt",
    "fileFormat" : "JPG",
    "previewUrl" : "https://www.example.com/preview/test.txt",
    "fileSizeByte" : 21391,
    "createDateTime" : "2024-10-29T06:00:01.000+09:00",
    "expireDateTime" : "2024-10-29T06:00:01.000+09:00",
    "uploadedFileTypes" : [ "EMAIL_DEFAULT" ]
  }
}
```

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 作業の成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| attachment | Object |  |
| attachment.attachmentId | String | ファイルのアップロード成功時に作成されるファイル固有ID |
| attachment.fileName | String | アップロードファイル名 |
| attachment.fileFormat | String | ファイル形式 |
| attachment.previewUrl | String | ファイルプレビューURL - 有効期限あり (詳細照会の呼び出し時に作成) |
| attachment.fileSizeByte | Long | 添付ファイルのサイズ単位はbyte |
| attachment.createDateTime | String | ファイルアップロード日時 |
| attachment.expireDateTime | String | ファイル有効期限 |
| attachment.uploadedFileTypes | Array | 個別商品にアップロードされたファイルタイプ一覧 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 添付ファイル単件照会

GET {{endpoint}}/attachment/v1.0/attachments/{{attachmentId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/attachment/v1.0/attachments/${attachmentId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="attachmentV1x0004DoValidateAttachments"></span>

## アップロード前の添付ファイル検証

アップロードする添付ファイルの有効性を検証します。ファイルタイプ、ファイルフォーマット、ファイルサイズ、解像度、横幅、縦幅を通じて、設定したファイルタイプの有効性を検証します。添付ファイルのアップロード前に、ファイルタイプに対する有効性を検証できます。


**リクエスト**

```
POST /attachment/v1.0/attachments/do-validate
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |



**リクエスト本文**

<!-- リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->

このAPIはリクエスト本文を要求しません。



**レスポンス本文**

<!-- レスポンス本文を返却しない場合は「このAPIはレスポンス本文を返却しません」と入力します。-->

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

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 作業の成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| results | Array |  |
| results[].isSuccessful | Boolean | 作業の成否を示します。<br>デフォルト値：true |
| results[].resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| results[].resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### アップロード前の添付ファイル検証

POST {{endpoint}}/attachment/v1.0/attachments/do-validate
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/attachment/v1.0/attachments/do-validate" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="attachmentV1x0005DoValidateAttachment"></span>

## アップロード済み添付ファイル検証

アップロード済みの添付ファイルに対して、新しいファイルタイプの有効性を検証します。ファイルタイプ修正APIの呼び出し前に、ファイルタイプに対する有効性を検証できます。


**リクエスト**

```
POST /attachment/v1.0/attachments/{attachmentId}/do-validate
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| attachmentId | Path | String | Y | 添付ファイルID |



**リクエスト本文**

<!-- リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->


```
{
  "fileTypes" : [ "EMAIL_DEFAULT" ]
}
```

<!-- リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| fileTypes | Array | Y | 添付ファイルの検証のためのファイルタイプ一覧 |



**レスポンス本文**

<!-- レスポンス本文を返却しない場合は「このAPIはレスポンス本文を返却しません」と入力します。-->

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

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 作業の成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| results | Array |  |
| results[].isSuccessful | Boolean | 作業の成否を示します。<br>デフォルト値：true |
| results[].resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| results[].resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### アップロード済み添付ファイル検証

POST {{endpoint}}/attachment/v1.0/attachments/{{attachmentId}}/do-validate
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "fileTypes" : [ "EMAIL_DEFAULT" ]
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/attachment/v1.0/attachments/${attachmentId}/do-validate" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "fileTypes" : [ "EMAIL_DEFAULT" ]
}'
```

</details>
<span id="attachmentV1x0006UpdateFileType"></span>

## アップロード済み添付ファイルのファイルタイプ修正

アップロード済みの添付ファイルのファイルタイプを修正します。


**リクエスト**

```
POST /attachment/v1.0/attachments/{attachmentId}/file-types
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| attachmentId | Path | String | Y | 添付ファイルID |



**リクエスト本文**

<!-- リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->


```
{
  "fileTypes" : [ "EMAIL_DEFAULT", "SMS_DEFAULT", "RCS_DEFAULT", "ALIMTALK_IMAGE", "ALIMTALK_ITEM_HIGHLIGHT_IMAGE" ]
}
```

<!-- リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| fileTypes | Array | N | 個別商品の添付ファイルアップロード時に指定するファイルタイプ一覧、1つ以上入力可能。テンプレートアップロード時に使用する場合、EMAILはEMAIL_TEMPLATE、SMSはSMS_TEMPLATEとしてアップロードリクエストが必要 |



**レスポンス本文**

<!-- レスポンス本文を返却しない場合は「このAPIはレスポンス本文を返却しません」と入力します。-->

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

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 作業の成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| results | Array | マルチリソース作業の結果です。 |
| results[].isSuccessful | Boolean | 作業の成否を示します。<br>デフォルト値：true |
| results[].resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| results[].resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### アップロード済み添付ファイルのファイルタイプ修正

POST {{endpoint}}/attachment/v1.0/attachments/{{attachmentId}}/file-types
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "fileTypes" : [ "EMAIL_DEFAULT", "SMS_DEFAULT", "EMAIL_TEMPLATE", "SMS_TEMPLATE" ]
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/attachment/v1.0/attachments/${attachmentId}/file-types" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "fileTypes" : [ "EMAIL_DEFAULT", "SMS_DEFAULT", "EMAIL_TEMPLATE", "SMS_TEMPLATE" ]
}'
```

</details>
<span id="attachmentV1x0007ReadFileTypes"></span>

## 添付ファイルタイプ一覧照会

サポート中の添付ファイルタイプの一覧を照会します。メッセージチャネルを設定すると、該当のメッセージチャネルで提供するファイルタイプ一覧を照会できます。


**リクエスト**

```
GET /attachment/v1.0/attachments/file-types
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| messageChannel | Query | V1x0MessageChannel | N | メッセージチャネル |



**リクエスト本文**

<!-- リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->

このAPIはリクエスト本文を要求しません。



**レスポンス本文**

<!-- レスポンス本文を返却しない場合は「このAPIはレスポンス本文を返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "fileTypes" : [ "EMAIL_DEFAULT", "SMS_DEFAULT", "RCS_DEFAULT", "ALIMTALK_IMAGE", "ALIMTALK_ITEM_HIGHLIGHT_IMAGE" ]
}
```

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 作業の成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| fileTypes | Array | ファイルタイプ一覧 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 添付ファイルタイプ一覧照会

GET {{endpoint}}/attachment/v1.0/attachments/file-types
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/attachment/v1.0/attachments/file-types" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
