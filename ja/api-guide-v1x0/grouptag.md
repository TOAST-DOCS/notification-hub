<!-- 新しいフォームのために追加されたstyleです。 -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 新しいフォームのためにタイトルを<h1>に変更しました。 -->
<h1>グループタグ</h1>




<span id="kakaobizcenterV10GroupTagsGet"></span>

## グループタグ全体一覧照会

Kakao Biz Centerのグループタグ全体一覧を照会します。

**リクエスト**

```
GET /kakaobizcenter/v1.0/group-tags
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | アクセストークン |
| senderKey | Query  | String | O | 送信プロフィールキー |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->

このAPIはリクエストボディを要求しません。



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

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

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| groupTags | Array | O |  |
| groupTags[].groupTagKey | String | O | グループタグキー |
| groupTags[].groupTagName | String | O | グループタグ名 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### グループタグ全体一覧照会

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
<span id="kakaobizcenterV10GroupTagsGroupTagKeyDelete"></span>

## グループタグ削除

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
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | アクセストークン |
| groupTagKey | Path  | String | O | グループタグキー |
| senderKey | Query  | String | O | 送信プロフィールキー |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->

このAPIはリクエストボディを要求しません。



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### グループタグ削除

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
<span id="kakaobizcenterV10GroupTagsGroupTagKeyGet"></span>

## グループタグ単件照会

Kakao Biz Centerのグループタグ単件を照会します。

**リクエスト**

```
GET /kakaobizcenter/v1.0/group-tags/{groupTagKey}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | アクセストークン |
| groupTagKey | Path  | String | O | グループタグキー |
| senderKey | Query  | String | O | 送信プロフィールキー |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->

このAPIはリクエストボディを要求しません。



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

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

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| groupTag | Object | O |  |
| groupTag.groupTagKey | String | O | グループタグキー |
| groupTag.groupTagName | String | O | グループタグ名 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### グループタグ単件照会

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
<span id="kakaobizcenterV10GroupTagsGroupTagKeyPut"></span>

## グループタグ修正

Kakao Biz Centerのグループタグを修正します。

**リクエスト**

```
PUT /kakaobizcenter/v1.0/group-tags/{groupTagKey}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | アクセストークン |
| groupTagKey | Path  | String | O | グループタグキー |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->


```
{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "newGroupTagName" : "20240619-00001"
}
```

<!-- リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| senderKey | String | O | 送信プロフィールキー |
| newGroupTagName | String | O | 新しいグループタグ名 |



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

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

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| groupTag | Object | O |  |
| groupTag.groupTagKey | String | O | グループタグキー |
| groupTag.groupTagName | String | O | グループタグ名 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### グループタグ修正

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
<span id="kakaobizcenterV10GroupTagsPost"></span>

## グループタグ登録

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
| X-NC-APP-KEY | Header  | String | O | Appkey |
| X-NHN-Authorization | Header  | String | O | アクセストークン |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->


```
{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "groupTagName" : "20240619-00001"
}
```

<!-- リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| senderKey | String | O | 送信プロフィールキー |
| groupTagName | String | O | グループタグ名 |



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

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

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| groupTag | Object | O |  |
| groupTag.groupTagKey | String | O | グループタグキー |
| groupTag.groupTagName | String | O | グループタグ名 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### グループタグ登録

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
