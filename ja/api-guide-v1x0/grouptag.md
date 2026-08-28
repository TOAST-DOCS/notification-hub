<!-- pre-align:aligned sig=73af06a9bb23 -->

<!-- 新しいフォーマットのために追加されたstyleです。 -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 新しいフォーマットのために見出しを<h1>に変更しました。 -->
<h1>NHN Cloud Notification Hub Public API - KakaoBizCenter GroupTag v1.0</h1>




<a id="list-all-group-tags"></a>
## グループタグの全一覧照会

Kakao Biz Centerのグループタグの全一覧を照会します。

**リクエスト**

```
GET /kakaobizcenter/v1.0/group-tags
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| senderKey | Query | String | O | 送信元プロフィールキー |



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
  "groupTags" : [ {
    "groupTagKey" : "b85552999bbb335777d16fbbbbbb552b3078aaa",
    "groupTagName" : "20240619-00001"
  } ]
}
```

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| groupTags | Array | O |  |
| groupTags[].groupTagKey | String | O | グループタグキー |
| groupTags[].groupTagName | String | O | グループタグ名 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### グループタグの全一覧照会

GET {{endpoint}}/kakaobizcenter/v1.0/group-tags?senderKey={{senderKey}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/group-tags?senderKey=${senderKey}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<a id="delete-a-group-tag"></a>
## グループタグの削除

Kakao Biz Centerのグループタグを削除します。

**リクエスト**

```
DELETE /kakaobizcenter/v1.0/group-tags/{groupTagKey}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| groupTagKey | Path | String | O | グループタグキー |
| senderKey | Query | String | O | 送信元プロフィールキー |



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
### グループタグの削除

DELETE {{endpoint}}/kakaobizcenter/v1.0/group-tags/{{groupTagKey}}?senderKey={{senderKey}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/kakaobizcenter/v1.0/group-tags/${groupTagKey}?senderKey=${senderKey}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<a id="get-a-group-tag"></a>
## グループタグの1件照会

Kakao Biz Centerのグループタグを1件照会します。

**リクエスト**

```
GET /kakaobizcenter/v1.0/group-tags/{groupTagKey}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| groupTagKey | Path | String | O | グループタグキー |
| senderKey | Query | String | O | 送信元プロフィールキー |



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
  "groupTag" : {
    "groupTagKey" : "b85552999bbb335777d16fbbbbbb552b3078aaa",
    "groupTagName" : "20240619-00001"
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
| groupTag | Object | O |  |
| groupTag.groupTagKey | String | O | グループタグキー |
| groupTag.groupTagName | String | O | グループタグ名 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### グループタグの1件照会

GET {{endpoint}}/kakaobizcenter/v1.0/group-tags/{{groupTagKey}}?senderKey={{senderKey}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/group-tags/${groupTagKey}?senderKey=${senderKey}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<a id="modify-a-group-tag"></a>
## グループタグの変更

Kakao Biz Centerのグループタグを変更します。

**リクエスト**

```
PUT /kakaobizcenter/v1.0/group-tags/{groupTagKey}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| groupTagKey | Path | String | O | グループタグキー |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は"このAPIはリクエスト本文を必要としません"と入力します。-->


```
{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "newGroupTagName" : "20240619-00001"
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| senderKey | String | O | 送信元プロフィールキー |
| newGroupTagName | String | O | 新しいグループタグ名 |



**レスポンス本文**

<!--レスポンス本文を返さない場合は"このAPIはレスポンス本文を返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "groupTag" : {
    "groupTagKey" : "b85552999bbb335777d16fbbbbbb552b3078aaa",
    "groupTagName" : "20240619-00001"
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
| groupTag | Object | O |  |
| groupTag.groupTagKey | String | O | グループタグキー |
| groupTag.groupTagName | String | O | グループタグ名 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### グループタグの変更

PUT {{endpoint}}/kakaobizcenter/v1.0/group-tags/{{groupTagKey}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "newGroupTagName" : "20240619-00001"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/kakaobizcenter/v1.0/group-tags/${groupTagKey}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "newGroupTagName" : "20240619-00001"
}'
```

</details>

<a id="register-a-group-tag"></a>
## グループタグの登録

Kakao Biz Centerのグループタグを登録します。

**リクエスト**

```
POST /kakaobizcenter/v1.0/group-tags
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
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "groupTagName" : "20240619-00001"
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| senderKey | String | O | 送信元プロフィールキー |
| groupTagName | String | O | グループタグ名 |



**レスポンス本文**

<!--レスポンス本文を返さない場合は"このAPIはレスポンス本文を返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "groupTag" : {
    "groupTagKey" : "b85552999bbb335777d16fbbbbbb552b3078aaa",
    "groupTagName" : "20240619-00001"
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
| groupTag | Object | O |  |
| groupTag.groupTagKey | String | O | グループタグキー |
| groupTag.groupTagName | String | O | グループタグ名 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### グループタグの登録

POST {{endpoint}}/kakaobizcenter/v1.0/group-tags
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "groupTagName" : "20240619-00001"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/kakaobizcenter/v1.0/group-tags" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "groupTagName" : "20240619-00001"
}'
```

</details>
