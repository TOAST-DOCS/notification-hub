<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>Template Category</h1>

**Notification > Notification Hub > API v1.0 User Guide > Template Category**


<span id="templateV10MessageChannelCategoriesCategoryIdDelete"></span>

## Delete a Template Category

Delete a template category.

**Request**

```
DELETE /template/v1.0/{messageChannel}/categories/{categoryId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messageChannel | Path  | String | Y | Message channel<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryId | Path  | String | Y | Category ID |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Delete a Template Category

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

## Retrieve Template Category Details

Retrieve a template category.

**Request**

```
GET /template/v1.0/{messageChannel}/categories/{categoryId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messageChannel | Path  | String | Y | Message channel<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryId | Path  | String | Y | Category ID |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "category" : {
    "categoryId" : "A9z0A9z0",
    "categoryName" : "delivery confirmation",
    "parentCategoryId" : "00000000",
    "messageChannel" : "SMS",
    "categoryIds" : [ "[1,2,3]" ],
    "templateIds" : [ "[11111111,22222222]" ]
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| category | Object | |
| category.categoryId | String | Category ID |
| category.categoryName | String | Category name |
| category.parentCategoryId | String | Parent category ID |
| category.messageChannel | String | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| category.categoryIds | Array | A list of category IDs belonging to the category |
| category.templateIds | Array | A list of template IDs belonging to the category |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve Template Category Details

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

## Modify a Template Category

Modify a template category.

**Request**

```
PUT /template/v1.0/{messageChannel}/categories/{categoryId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messageChannel | Path  | String | Y | Message channel<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryId | Path  | String | Y | Category ID |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "name" : "delivery confirmation",
  "parentCategoryId" : "00000000"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| Name | String | Y | Category name |
| ParentCategoryId | String | N | Parent category ID |



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Modify a Template Category

PUT {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "name" : "delivery confirmation",
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
  "name" : "delivery confirmation",
  "parentCategoryId" : "00000000"
}'
```

</details>
<span id="templateV10MessageChannelCategoriesCategoryIdTemplatesPost"></span>

## Add a Template to a Category

Add a template to a category.

**Request**

```
POST /template/v1.0/{messageChannel}/categories/{categoryId}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messageChannel | Path  | String | Y | Message channel<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryId | Path  | String | Y | Category ID |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateId" : "11111111"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| templateId | String | N | Template ID |



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Add a Template to a Category

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

## List Template Categories

List template categories.

**Request**

```
GET /template/v1.0/{messageChannel}/categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messageChannel | Path  | String | Y | Message channel<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "categories" : [ {
    "categoryId" : "A9z0A9z0",
    "categoryName" : "delivery confirmation",
    "parentCategoryId" : "00000000",
    "messageChannel" : "SMS",
    "categoryIds" : [ "[1,2,3]" ],
    "templateIds" : [ "[11111111,22222222]" ]
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| categories | Array |  |
| categories[].categoryId | String | Category ID |
| categories[].categoryName | String | Category name |
| categories[].parentCategoryId | String | Parent category ID |
| categories[].messageChannel | String | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| categories[].categoryIds | Array | A list of category IDs belonging to the category |
| categories[].templateIds | Array | A list of template IDs belonging to the category |


**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### List Template Categories

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

## Register Template Categories

Register template categories.

**Request**

```
POST /template/v1.0/{messageChannel}/categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messageChannel | Path  | String | Y | Message channel<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "parentCategoryId" : "00000000",
  "name" : "delivery confirmation"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| Path | Type | Required | Description |
| - | - | - | - |
| parentCategoryId | String | N | Parent category ID |
| name | String | Y | Category name |



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

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

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| categoryId | String | No description |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Register Template Categories

POST {{endpoint}}/template/v1.0/{{messageChannel}}/categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "parentCategoryId" : "00000000",
  "name" : "delivery confirmation"
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
  "name" : "delivery confirmation"
}'
```

</details>
<span id="templateV10MessageChannelCategoryTreesGet"></span>

## Retrieve a Template Category Hierarchy

Retrieve a template category hierarchy.

**Request**

```
GET /template/v1.0/{messageChannel}/category-trees
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**Request Parameter**

| Name | Category | Type | Required | Description |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | Access token |
| messageChannel | Path  | String | Y | Message channel<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryTemplateName | Query  | String | N | Category/template name |
| senderProfileType | Query  | String | N | Sender profile type<br>[GROUP, NORMAL] |
| senderKey | Query  | String | N | Sender key |
| status | Query  | String | N | Template status |



**Request Body**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

This API does not require a request body.



**Response Body**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "categories" : [ {
    "categoryId" : "A9z0A9z0",
    "categoryName" : "delivery confirmation",
    "parentCategoryId" : "00000000",
    "messageChannel" : "SMS",
    "categories" : null,
    "templates" : [ {
      "templateId" : "11111111",
      "templateName" : "delivery confirmation template"
    } ]
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| Path | Type | Description |
| - | - | - |
| header | Object | |
| header.isSuccessful | Boolean | Indicates whether the request was successful.<br>Default: true |
| header.resultCode | Integer | The result code of the request.<br>Default: 0 |
| header.resultMessage | String | The result message of the request.<br>Default: SUCCESS |
| categories | Array | |
| categories[].categoryId | String | Category ID, root category |
| categories[].categoryName | String | Category name, root category |
| categories[].parentCategoryId | String | Parent category ID |
| categories[].messageChannel | String | Message channel<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| categories[].categories | Array | List of categories belonging to a category |
| categories[].templates | Array | List of templates belonging to a category |



**Request Example**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### Retrieve a Template Category Hierarchy

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