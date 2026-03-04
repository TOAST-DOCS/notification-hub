<!-- 新しい書式のために追加されたstyleです。 -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 新しい書式のために見出しを<h1>に変更しました。 -->
<h1>テンプレートカテゴリー</h1>

**Notification > Notification Hub > API v1.0 使用ガイド > テンプレートカテゴリー**


<span id="templateV10MessageChannelCategoriesCategoryIdDelete"></span>

## テンプレートカテゴリーの削除

テンプレートカテゴリーを削除します。

**リクエスト**

```
DELETE /template/v1.0/{messageChannel}/categories/{categoryId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| messageChannel | Path | String | Y | メッセージチャネル<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryId | Path | String | Y | カテゴリーID |



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
  }
}
```

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### テンプレートカテゴリーの削除

DELETE {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X DELETE "${endpoint}/template/v1.0/${messageChannel}/categories/${categoryId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV10MessageChannelCategoriesCategoryIdGet"></span>

## テンプレートカテゴリー単件照会

テンプレートカテゴリーを単件照会します。

**リクエスト**

```
GET /template/v1.0/{messageChannel}/categories/{categoryId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| messageChannel | Path | String | Y | メッセージチャネル<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryId | Path | String | Y | カテゴリーID |



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
  "category" : {
    "categoryId" : "A9z0A9z0",
    "categoryName" : "配送完了案内カテゴリー",
    "parentCategoryId" : "00000000",
    "messageChannel" : "SMS",
    "categoryIds" : [ "[1,2,3]" ],
    "templateIds" : [ "[11111111,22222222]" ]
  }
}
```

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| category | Object |  |
| category.categoryId | String | カテゴリーID |
| category.categoryName | String | カテゴリー名 |
| category.parentCategoryId | String | 上位カテゴリーID |
| category.messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| category.categoryIds | Array | カテゴリーに属するカテゴリーIDリスト |
| category.templateIds | Array | カテゴリーに属するテンプレートIDリスト |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### テンプレートカテゴリー単件照会

GET {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/${messageChannel}/categories/${categoryId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV10MessageChannelCategoriesCategoryIdPut"></span>

## テンプレートカテゴリーの修正

テンプレートカテゴリーを修正します。

**リクエスト**

```
PUT /template/v1.0/{messageChannel}/categories/{categoryId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| messageChannel | Path | String | Y | メッセージチャネル<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryId | Path | String | Y | カテゴリーID |



**リクエスト本文**

<!-- リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->


```
{
  "name" : "配送完了案内カテゴリー",
  "parentCategoryId" : "00000000"
}
```

<!-- リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| name | String | Y | カテゴリー名 |
| parentCategoryId | String | N | 上位カテゴリーID |



**レスポンス本文**

<!-- レスポンス本文を返却しない場合は「このAPIはレスポンス本文を返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### テンプレートカテゴリーの修正

PUT {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "name" : "配送完了案内カテゴリー",
  "parentCategoryId" : "00000000"
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X PUT "${endpoint}/template/v1.0/${messageChannel}/categories/${categoryId}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "name" : "配送完了案内カテゴリー",
  "parentCategoryId" : "00000000"
}'
```

</details>
<span id="templateV10MessageChannelCategoriesCategoryIdTemplatesPost"></span>

## カテゴリーにテンプレートを追加

カテゴリーにテンプレートを追加します。

**リクエスト**

```
POST /template/v1.0/{messageChannel}/categories/{categoryId}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| messageChannel | Path | String | Y | メッセージチャネル<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryId | Path | String | Y | カテゴリーID |



**リクエスト本文**

<!-- リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->


```
{
  "templateId" : "11111111"
}
```

<!-- リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| templateId | String | N | テンプレートID |



**レスポンス本文**

<!-- レスポンス本文を返却しない場合は「このAPIはレスポンス本文を返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### カテゴリーにテンプレートを追加

POST {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "templateId" : "11111111"
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/${messageChannel}/categories/${categoryId}/templates" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "templateId" : "11111111"
}'
```

</details>
<span id="templateV10MessageChannelCategoriesGet"></span>

## テンプレートカテゴリー一覧照会

テンプレートカテゴリー一覧を照会します。

**リクエスト**

```
GET /template/v1.0/{messageChannel}/categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| messageChannel | Path | String | Y | メッセージチャネル<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |



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
  "categories" : [ {
    "categoryId" : "A9z0A9z0",
    "categoryName" : "配送完了案内カテゴリー",
    "parentCategoryId" : "00000000",
    "messageChannel" : "SMS",
    "categoryIds" : [ "[1,2,3]" ],
    "templateIds" : [ "[11111111,22222222]" ]
  } ]
}
```

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| categories | Array |  |
| categories[].categoryId | String | カテゴリーID |
| categories[].categoryName | String | カテゴリー名 |
| categories[].parentCategoryId | String | 上位カテゴリーID |
| categories[].messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| categories[].categoryIds | Array | カテゴリーに属するカテゴリーIDリスト |
| categories[].templateIds | Array | カテゴリーに属するテンプレートIDリスト |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### テンプレートカテゴリー一覧照会

GET {{endpoint}}/template/v1.0/{{messageChannel}}/categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/${messageChannel}/categories" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="templateV10MessageChannelCategoriesPost"></span>

## テンプレートカテゴリーの登録

テンプレートカテゴリーを登録します。

**リクエスト**

```
POST /template/v1.0/{messageChannel}/categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| messageChannel | Path | String | Y | メッセージチャネル<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |



**リクエスト本文**

<!-- リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->


```
{
  "parentCategoryId" : "00000000",
  "name" : "配送完了案内カテゴリー"
}
```

<!-- リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| parentCategoryId | String | N | 上位カテゴリーID |
| name | String | Y | カテゴリー名 |



**レスポンス本文**

<!-- レスポンス本文を返却しない場合は「このAPIはレスポンス本文を返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "categoryId" : "String - Default and Example is not provided."
}
```

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| categoryId | String | No description |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### テンプレートカテゴリーの登録

POST {{endpoint}}/template/v1.0/{{messageChannel}}/categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "parentCategoryId" : "00000000",
  "name" : "配送完了案内カテゴリー"
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/template/v1.0/${messageChannel}/categories" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
-d '{
  "parentCategoryId" : "00000000",
  "name" : "配送完了案内カテゴリー"
}'
```

</details>
<span id="templateV10MessageChannelCategoryTreesGet"></span>

## テンプレートカテゴリーツリー一覧照会

テンプレートカテゴリーのツリー一覧を照会します。

**リクエスト**

```
GET /template/v1.0/{messageChannel}/category-trees
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| messageChannel | Path | String | Y | メッセージチャネル<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryTemplateName | Query  | String | N | カテゴリー/テンプレート名 |
| senderProfileType | Query | String | N | 送信元プロファイルタイプ<br>[GROUP, NORMAL] |
| senderKey | Query | String | N | 送信キー |
| status | Query  | String | N | テンプレート状態 |



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
  "categories" : [ {
    "categoryId" : "A9z0A9z0",
    "categoryName" : "配送完了案内カテゴリー",
    "parentCategoryId" : "00000000",
    "messageChannel" : "SMS",
    "categories" : null,
    "templates" : [ {
      "templateId" : "11111111",
      "templateName" : "配送完了テンプレート"
    } ]
  } ]
}
```

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| categories | Array |  |
| categories[].categoryId | String | カテゴリーID、ルートカテゴリー(ROOT) |
| categories[].categoryName | String | カテゴリー名、ルートカテゴリー(Root Category) |
| categories[].parentCategoryId | String | 上位カテゴリーID |
| categories[].messageChannel | String | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| categories[].categories | Array | カテゴリーに属するカテゴリーリスト |
| categories[].templates | Array | カテゴリーに属するテンプレートリスト |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### テンプレートカテゴリーツリー一覧照会

GET {{endpoint}}/template/v1.0/{{messageChannel}}/category-trees
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/template/v1.0/${messageChannel}/category-trees" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
