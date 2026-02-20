<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>템플릿 카테고리</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 템플릿 카테고리**


<span id="templateV10MessageChannelCategoriesCategoryIdDelete"></span>

## 템플릿 카테고리 삭제

템플릿 카테고리를 삭제합니다.

**요청**

```
DELETE /template/v1.0/{messageChannel}/categories/{categoryId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageChannel | Path  | String | Y | 메시지 채널<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryId | Path  | String | Y | 카테고리 아이디 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.



**응답 본문**

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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 카테고리 삭제

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

## 템플릿 카테고리 단건 조회

템플릿 카테고리 단건 조회합니다.

**요청**

```
GET /template/v1.0/{messageChannel}/categories/{categoryId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageChannel | Path  | String | Y | 메시지 채널<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryId | Path  | String | Y | 카테고리 아이디 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.



**응답 본문**

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
    "categoryName" : "배송완료 안내 카테고리",
    "parentCategoryId" : "00000000",
    "messageChannel" : "SMS",
    "categoryIds" : [ "[1,2,3]" ],
    "templateIds" : [ "[11111111,22222222]" ]
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| category | Object |  |
| category.categoryId | String | 카테고리 아이디 |
| category.categoryName | String | 카테고리 이름 |
| category.parentCategoryId | String | 상위 카테고리 아이디 |
| category.messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| category.categoryIds | Array | 카테고리에 속한 카테고리 아이디 리스트 |
| category.templateIds | Array | 카테고리에 속한 템플릿 아이디 리스트 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 카테고리 단건 조회

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

## 템플릿 카테고리 수정

템플릿 카테고리를 수정합니다.

**요청**

```
PUT /template/v1.0/{messageChannel}/categories/{categoryId}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageChannel | Path  | String | Y | 메시지 채널<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryId | Path  | String | Y | 카테고리 아이디 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "name" : "배송완료 안내 카테고리",
  "parentCategoryId" : "00000000"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| name | String | Y | 카테고리 이름 |
| parentCategoryId | String | N | 상위 카테고리 아이디 |



**응답 본문**

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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 카테고리 수정

PUT {{endpoint}}/template/v1.0/{{messageChannel}}/categories/{{categoryId}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "name" : "배송완료 안내 카테고리",
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
  "name" : "배송완료 안내 카테고리",
  "parentCategoryId" : "00000000"
}'
```

</details>
<span id="templateV10MessageChannelCategoriesCategoryIdTemplatesPost"></span>

## 카테고리에 템플릿 추가

카테고리에 템플릿 추가합니다.

**요청**

```
POST /template/v1.0/{messageChannel}/categories/{categoryId}/templates
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageChannel | Path  | String | Y | 메시지 채널<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryId | Path  | String | Y | 카테고리 아이디 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "templateId" : "11111111"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| templateId | String | N | 템플릿 아이디 |



**응답 본문**

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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 카테고리에 템플릿 추가

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

## 템플릿 카테고리 리스트 조회

템플릿 카테고리 리스트를 조회합니다.

**요청**

```
GET /template/v1.0/{messageChannel}/categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageChannel | Path  | String | Y | 메시지 채널<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.



**응답 본문**

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
    "categoryName" : "배송완료 안내 카테고리",
    "parentCategoryId" : "00000000",
    "messageChannel" : "SMS",
    "categoryIds" : [ "[1,2,3]" ],
    "templateIds" : [ "[11111111,22222222]" ]
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| categories | Array |  |
| categories[].categoryId | String | 카테고리 아이디 |
| categories[].categoryName | String | 카테고리 이름 |
| categories[].parentCategoryId | String | 상위 카테고리 아이디 |
| categories[].messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| categories[].categoryIds | Array | 카테고리에 속한 카테고리 아이디 리스트 |
| categories[].templateIds | Array | 카테고리에 속한 템플릿 아이디 리스트 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 카테고리 리스트 조회

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

## 템플릿 카테고리 등록

템플릿 카테고리를 등록합니다.

**요청**

```
POST /template/v1.0/{messageChannel}/categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageChannel | Path  | String | Y | 메시지 채널<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "parentCategoryId" : "00000000",
  "name" : "배송완료 안내 카테고리"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| parentCategoryId | String | N | 상위 카테고리 아이디 |
| name | String | Y | 카테고리 이름 |



**응답 본문**

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

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| categoryId | String | No description |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 카테고리 등록

POST {{endpoint}}/template/v1.0/{{messageChannel}}/categories
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

{
  "parentCategoryId" : "00000000",
  "name" : "배송완료 안내 카테고리"
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
  "name" : "배송완료 안내 카테고리"
}'
```

</details>
<span id="templateV10MessageChannelCategoryTreesGet"></span>

## 템플릿 카테고리 트리 리스트 조회

템플릿 카테고리 트리 리스트를 조회합니다.

**요청**

```
GET /template/v1.0/{messageChannel}/category-trees
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| messageChannel | Path  | String | Y | 메시지 채널<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| categoryTemplateName | Query  | String | N | 카테고리/템플릿 이름 |
| senderProfileType | Query  | String | N | 발신프로필 타입<br>[GROUP, NORMAL] |
| senderKey | Query  | String | N | 발신 키 |
| status | Query  | String | N | 템플릿 상태 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->

이 API는 요청 본문을 요구하지 않습니다.



**응답 본문**

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
    "categoryName" : "배송완료 안내 카테고리",
    "parentCategoryId" : "00000000",
    "messageChannel" : "SMS",
    "categories" : null,
    "templates" : [ {
      "templateId" : "11111111",
      "templateName" : "배송 완료 템플릿"
    } ]
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| categories | Array |  |
| categories[].categoryId | String | 카테고리 아이디, 루트 카테고리(ROOT) |
| categories[].categoryName | String | 카테고리 이름, 루트 카테고리(Root Category) |
| categories[].parentCategoryId | String | 상위 카테고리 아이디 |
| categories[].messageChannel | String | 메시지 채널<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| categories[].categories | Array | 카테고리에 속한 카테고리 리스트 |
| categories[].templates | Array | 카테고리에 속한 템플릿 리스트 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 템플릿 카테고리 트리 리스트 조회

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