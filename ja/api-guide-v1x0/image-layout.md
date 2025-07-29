<!-- 新しい 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>画像レイアウト</h1>

**Notification > Notification Hub > API v1.0 使用ガイド > 画像レイアウト**



<span id="imageLayoutV1x0003GetImageLayout"></span>

## 画像レイアウトの個別照会

画像レイアウトをIDベースで個別照会します。

**リクエスト**

```
GET /image-layout/v1.0/image-layouts/{id}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| id | Path  | String | Y | 画像レイアウトID |



**リクエストボディ**

<!--リクエストボディを要求しない場合は、「このAPIはリクエストボディを要求しません」と入力します。-->

このAPIはリクエストボディを要求しません。



**レスポンスボディ**

<!--レスポンスボディを返さない場合は、「このAPIはレスポンスボディを返しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "imageLayout" : {
    "id" : "A9z0A9z0",
    "name" : "2025_プロモーション_クーポン",
    "backgroundImage" : {
      "fileName" : "background.png",
      "filePreviewUrl" : "https://example.com/background.png"
    },
    "cardImage" : {
      "fileName" : "cardImage.png",
      "filePreviewUrl" : "https://example.com/background.png"
    },
    "title" : "#{user}様から送信された\n#{promotion}ギフトカードが届きました。",
    "body" : "* 商品名: 今日の商品\n*有効期間: #{expirydate}まで\n*使用先: オン/オフライン店舗(一部店舗を除く)",
    "useBarcode" : true,
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
| imageLayout | Object |  |
| imageLayout.id | String | 画像レイアウトID |
| imageLayout.name | String | 画像レイアウト名 |
| imageLayout.backgroundImage | Object |  |
| imageLayout.backgroundImage.fileName | String | 背景画像ファイル名 |
| imageLayout.backgroundImage.filePreviewUrl | String | 背景画像のプレビューURL |
| imageLayout.cardImage | Object |  |
| imageLayout.cardImage.fileName | String | カード画像ファイル名 |
| imageLayout.cardImage.filePreviewUrl | String | カード画像のプレビューURL |
| imageLayout.title | String | 件名 |
| imageLayout.body | String | 本文 |
| imageLayout.useBarcode | Boolean | バーコード使用可否 |
| imageLayout.createdDateTime | String | 画像レイアウト作成日時 |
| imageLayout.updatedDateTime | String | 画像レイアウト修正日時 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 画像レイアウトの個別照会

GET {{endpoint}}/image-layout/v1.0/image-layouts/{{id}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/image-layout/v1.0/image-layouts/${id}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="imageLayoutV1x0CreateImageLayout"></span>

## 画像レイアウトの登録

画像レイアウトを登録します。

**リクエスト**

```
POST /image-layout/v1.0/image-layouts
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
Content-Type: multipart/form-data
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |



**リクエストボディ**

<!--リクエストボディを要求しない場合は、「このAPIはリクエストボディを要求しません」と入力します。-->


| 名前 | タイプ | 必須 | 説明 |
| - | - | - | - |
| name | String | Y | 画像レイアウト名 |
| backgroundImage | File | Y | 背景画像ファイル |
| cardImage | File | Y | カード画像ファイル |
| title | String | Y | 件名 |
| body | String | Y | 本文 |
| useBarcode | Boolean | Y | バーコード使用可否 |

**レスポンスボディ**

<!--レスポンスボディを返さない場合は、「このAPIはレスポンスボディを返しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "id" : "A9z0A9z0"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| id | String | 画像レイアウトID |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 画像レイアウトの登録

POST {{endpoint}}/image-layout/v1.0/image-layouts
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
Content-Type: multipart/form-data

name=画像-レイアウト
title=件名
body=本文
useBarcode=true
backgroundImage=@{{pathToImage}}
cardImage=@{{pathToImage}}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/image-layout/v1.0/image-layouts" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \
-H 'Content-Type: multipart/form-data' \
-F "name=画像-レイアウト" \
-F "backgroundImage=@{pathToImage}" \
-F "cardImage=@{pathToImage}" \
-F "title=件名" \
-F "body=本文" \
-F "useBarcode=true"
```

</details>
<span id="imageLayoutV1x0DeleteImageLayout"></span>

## 画像レイアウトの削除

画像レイアウトを削除します。

**リクエスト**

```
DELETE /image-layout/v1.0/image-layouts/{id}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| id | Path  | String | Y | 画像レイアウトID |



**リクエストボディ**

<!--リクエストボディを要求しない場合は、「このAPIはリクエストボディを要求しません」と入力します。-->

このAPIはリクエストボディを要求しません。



**レスポンスボディ**

<!--レスポンスボディを返さない場合は、「このAPIはレスポンスボディを返しません」と入力します。-->

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



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 画像レイアウトの削除

DELETE {{endpoint}}/image-layout/v1.0/image-layouts/{{id}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/image-layout/v1.0/image-layouts/${id}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="imageLayoutV1x0GetImageLayoutList"></span>

## 画像レイアウトのリスト照会

画像レイアウトをリストで照会します。

**リクエスト**

```
GET /image-layout/v1.0/image-layouts
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| name | Query  | String | N | 画像レイアウト名(LIKE検索) |
| limit | Query  | Integer | N | limitを設定しない場合はデフォルト20(最大1000) |
| offset | Query  | Integer | N | offsetを設定しない場合はデフォルト0 |



**リクエストボディ**

<!--リクエストボディを要求しない場合は、「このAPIはリクエストボディを要求しません」と入力します。-->

このAPIはリクエストボディを要求しません。



**レスポンスボディ**

<!--レスポンスボディを返さない場合は、「このAPIはレスポンスボディを返しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "imageLayouts" : [ {
    "id" : "A9z0A9z0",
    "name" : "2025_プロモーション_クーポン"
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
| imageLayouts | Array |  |
| imageLayouts[].id | String | 画像レイアウトID |
| imageLayouts[].name | String | 画像レイアウト名 |
| imageLayouts[].backgroundImage | Object |  |
| imageLayouts[].backgroundImage.fileName | String | 背景画像ファイル名 |
| imageLayouts[].backgroundImage.filePreviewUrl | String | 背景画像のプレビューURL |
| imageLayouts[].cardImage | Object |  |
| imageLayouts[].cardImage.fileName | String | カード画像ファイル名 |
| imageLayouts[].cardImage.filePreviewUrl | String | カード画像のプレビューURL |
| imageLayouts[].title | String | 件名 |
| imageLayouts[].body | String | 本文 |
| imageLayouts[].useBarcode | Boolean | バーコード使用可否 |
| imageLayouts[].createdDateTime | String | 画像レイアウト作成日時 |
| imageLayouts[].updatedDateTime | String | 画像レイアウト修正日時 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 画像レイアウトのリスト照会

GET {{endpoint}}/image-layout/v1.0/image-layouts
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/image-layout/v1.0/image-layouts" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="imageLayoutV1x0UpdateImageLayout"></span>

## 画像レイアウトの修正

画像レイアウトを修正します。修正が必要なフィールドのみ入力して部分修正が可能です。

**リクエスト**

```
PATCH /image-layout/v1.0/image-layouts/{id}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
Content-Type: multipart/form-data
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |


**リクエストボディ**

<!--リクエストボディを要求しない場合は、「このAPIはリクエストボディを要求しません」と入力します。-->


| 名前 | タイプ | 必須 | 説明 |
| - | - | - | - |
| name | String | N | 画像レイアウト名 |
| backgroundImage | String | N | 背景画像ファイル |
| cardImage | String | N | カード画像ファイル |
| title | String | N | 件名 |
| body | String | N | 本文 |
| useBarcode | Boolean | N | バーコード使用可否 |


**レスポンスボディ**

<!--レスポンスボディを返さない場合は、「このAPIはレスポンスボディを返しません」と入力します。-->

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



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 画像レイアウトの修正

PATCH {{endpoint}}/image-layout/v1.0/image-layouts/{{id}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
Content-Type: multipart/form-data

name=画像-レイアウト
title=件名
body=本文
useBarcode=true
backgroundImage=@{{pathToImage}}
cardImage=@{{pathToImage}}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PATCH "${endpoint}/image-layout/v1.0/image-layouts/${id}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \
-H 'Content-Type: multipart/form-data' \
-F "name=画像-レイアウト" \
-F "backgroundImage=@{pathToImage}" \
-F "cardImage=@{pathToImage}" \
-F "title=件名" \
-F "body=本文" \
-F "useBarcode=true"
```

</details>
