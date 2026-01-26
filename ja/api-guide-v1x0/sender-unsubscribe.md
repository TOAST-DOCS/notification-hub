<!-- 新しい様式のために追加されたスタイルです。 -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 新しい様式に合わせて、タイトルを <h1> に変更しました。 -->
<h1>発信情報</h1>

**Notification > Notification Hub > API v1.0利用ガイド > 発信情報**



<span id="senderV1x0001RegisterExternalUnsubscribePhoneNumber"></span>

## 080受信拒否外部番号の登録申請

080受信拒否外部番号の登録を申請します。


**リクエスト**

```
POST /sender/v1.0/unsubscribe-phone-numbers/external
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |



**リクエスト本文**

<!--リクエスト本文が不要な場合は、「このAPIはリクエスト本文を必要としません」と入力してください。-->


```
{
  "unsubscribePhoneNumber" : "0801234567",
  "corporationName" : "会社名"
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| unsubscribePhoneNumber | String | Y | 080受信拒否外部番号 |
| corporationName | String | Y | 会社名 |



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
### 080受信拒否外部番号の登録申請

POST {{endpoint}}/sender/v1.0/unsubscribe-phone-numbers/external
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "unsubscribePhoneNumber" : "0801234567",
  "corporationName" : "会社名"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/sender/v1.0/unsubscribe-phone-numbers/external" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "unsubscribePhoneNumber" : "0801234567",
  "corporationName" : "会社名"
}'
```

</details>
<span id="senderV1x0002TerminateExternalUnsubscribePhoneNumber"></span>

## 080受信拒否外部登録番号の削除

080受信拒否外部登録番号を削除します。


**リクエスト**

```
DELETE /sender/v1.0/unsubscribe-phone-numbers/external/{unsubscribePhoneNumber}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y  | アプリキー |
| X-NHN-Authorization | Header  | String | Y  | アクセストークン |
| unsubscribePhoneNumber | Path  | String | Y  | 080受信拒否外部番号 |



**リクエスト本文**

<!--リクエスト本文が不要な場合は、「このAPIはリクエスト本文を必要としません」と入力してください。-->

このAPIはリクエスト本文を要求しません。



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
### 080受信拒否外部登録番号の削除

DELETE {{endpoint}}/sender/v1.0/unsubscribe-phone-numbers/external/{{unsubscribePhoneNumber}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/sender/v1.0/unsubscribe-phone-numbers/external/${unsubscribePhoneNumber}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
<span id="senderV1x0003ReadUnsubscribePhoneNumbers"></span>

## 080受信拒否番号リストの照会

080受信拒否番号リストを照会します。


**リクエスト**

```
GET /sender/v1.0/unsubscribe-phone-numbers
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| unsubscribePhoneNumber | Query  | String | N | 受信拒否番号(LIKE検索) |
| limit | Query  | Integer | N | limitを設定しない場合はデフォルト50(最大1000) |
| offset | Query  | Integer | N | offsetを設定しない場合はデフォルト0 |



**リクエスト本文**

<!--リクエスト本文が不要な場合は、「このAPIはリクエスト本文を必要としません」と入力してください。-->

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
  "unsubscribePhoneNumbers" : [ {
    "unsubscribePhoneNumber" : "0801234567",
    "corporationName" : "会社名",
    "shareStatus" : "PRIMARY",
    "provider" : "INTERNAL",
    "status" : "READY",
    "terminable" : true,
    "requestedDateTime" : "2024-10-29T06:00:01.000+09:00",
    "startedDateTime" : "2024-10-29T06:00:01.000+09:00",
    "deletedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ]
}
```

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| totalCount | Integer | 総件数 |
| unsubscribePhoneNumbers | Array | 080受信拒否番号リスト |
| unsubscribePhoneNumbers[].unsubscribePhoneNumber | String | 080受信拒否番号 |
| unsubscribePhoneNumbers[].corporationName | String | 会社名 |
| unsubscribePhoneNumbers[].shareStatus | String | 080受信拒否番号の共有状態<br>[PRIMARY(直接登録した080番号)、SECONDARY(共有された080番号)] |
| unsubscribePhoneNumbers[].provider | String | 080受信拒否番号の提供元タイプ<br>[INTERNAL(内部発番)、EXTERNAL(外部登録番号)] |
| unsubscribePhoneNumbers[].status | String | 080受信拒否番号の状態<br>[READY(準備)、RESERVE_USE(審査中)、IN_USE(使用中)、TERMINATED(削除)] |
| unsubscribePhoneNumbers[].terminable | Boolean | 削除可否 |
| unsubscribePhoneNumbers[].requestedDateTime | String | 申請日時 |
| unsubscribePhoneNumbers[].startedDateTime | String | 開通日時 |
| unsubscribePhoneNumbers[].deletedDateTime | String | 削除日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 080受信拒否番号リストの照会

GET {{endpoint}}/sender/v1.0/unsubscribe-phone-numbers
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/sender/v1.0/unsubscribe-phone-numbers" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
<span id="senderV1x0004ReadUnsubscribePhoneNumber"></span>

## 080受信拒否番号の単件照会

080受信拒否番号の単件を照会します。


**リクエスト**

```
GET /sender/v1.0/unsubscribe-phone-numbers/{unsubscribePhoneNumber}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| unsubscribePhoneNumber | Path  | String | Y | 受信拒否番号 |



**リクエスト本文**

<!--リクエスト本文が不要な場合は、「このAPIはリクエスト本文を必要としません」と入力してください。-->

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
  "unsubscribePhoneNumber" : {
    "unsubscribePhoneNumber" : 0801234567,
    "corporationName" : "会社名",
    "shareStatus" : "PRIMARY",
    "provider" : "INTERNAL",
    "status" : "READY",
    "terminable" : true,
    "requestedDateTime" : "2024-10-29T06:00:01.000+09:00",
    "startedDateTime" : "2024-10-29T06:00:01.000+09:00",
    "deletedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| unsubscribePhoneNumber | Object |  |
| unsubscribePhoneNumber.unsubscribePhoneNumber | String | 080受信拒否番号 |
| unsubscribePhoneNumber.corporationName | String | 会社名 |
| unsubscribePhoneNumber.shareStatus | String | 080受信拒否番号の共有状態<br>[PRIMARY(直接登録した080番号)、SECONDARY(共有された080番号)] |
| unsubscribePhoneNumber.provider | String | 080受信拒否番号の提供元タイプ<br>[INTERNAL(内部発番)、EXTERNAL(外部登録番号)] |
| unsubscribePhoneNumber.status | String | 080受信拒否番号の状態<br>[READY(準備)、RESERVE_USE(審査中)、IN_USE(使用中)、TERMINATED(削除)] |
| unsubscribePhoneNumber.terminable | Boolean | 削除可否 |
| unsubscribePhoneNumber.requestedDateTime | String | 申請日時 |
| unsubscribePhoneNumber.startedDateTime | String | 開通日時 |
| unsubscribePhoneNumber.deletedDateTime | String | 削除日時 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 080受信拒否番号の単件照会

GET {{endpoint}}/sender/v1.0/unsubscribe-phone-numbers/{{unsubscribePhoneNumber}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/sender/v1.0/unsubscribe-phone-numbers/${unsubscribePhoneNumber}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
