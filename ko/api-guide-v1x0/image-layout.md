<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>이미지 레이아웃</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 이미지 레이아웃**



<span id="imageLayoutV1x0003GetImageLayout"></span>

## 이미지 레이아웃 단건 조회

이미지 레이아웃을 ID 기반으로 단건 조회합니다.

**요청**

```
GET /image-layout/v1.0/image-layouts/{id}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| id | Path  | String | Y | 이미지 레이아웃 아이디 |



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
  "imageLayout" : {
    "id" : "A9z0A9z0",
    "name" : "2025_프로모션_쿠폰",
    "backgroundImage" : {
      "fileName" : "background.png",
      "filePreviewUrl" : "https://example.com/background.png"
    },
    "cardImage" : {
      "fileName" : "cardImage.png",
      "filePreviewUrl" : "https://example.com/background.png"
    },
    "title" : "%user%님이 보내신\\n%promotion% 기프트 카드가 도착했어요.",
    "body" : "* 상품명: 오늘의 상품\\n*유효기간: %expirydate%까지\\n*사용처: 온/오프라인 매장(일부 매장 제외)",
    "useBarcode" : true,
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| imageLayout | Object | N|  |
| imageLayout.id | String | N| 이미지 레이아웃 아이디 |
| imageLayout.name | String | N| 이미지 레이아웃 이름 |
| imageLayout.backgroundImage | Object | N|  |
| imageLayout.backgroundImage.fileName | String | N| 배경 이미지 파일 이름 |
| imageLayout.backgroundImage.filePreviewUrl | String | N| 배경 이미지 미리보기 URL |
| imageLayout.cardImage | Object | N|  |
| imageLayout.cardImage.fileName | String | N| 카드 이미지 파일 이름 |
| imageLayout.cardImage.filePreviewUrl | String | N| 카드 이미지 미리보기 URL |
| imageLayout.title | String | N| 제목 |
| imageLayout.body | String | N| 본문 |
| imageLayout.useBarcode | Boolean | N| 바코드 사용 여부 |
| imageLayout.createdDateTime | String | N| 이미지 레이아웃 생성 일시 |
| imageLayout.updatedDateTime | String | N| 이미지 레이아웃 수정 일시 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 이미지 레이아웃 단건 조회

GET {{endpoint}}/image-layout/v1.0/image-layouts/{{id}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}



```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http

curl -X GET "${endpoint}/image-layout/v1.0/image-layouts/${id}"  \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"   
```

</details>


<span id="imageLayoutV1x0CreateImageLayout"></span>

## 이미지 레이아웃 등록

이미지 레이아웃을 등록합니다.

**요청**

```
POST /image-layout/v1.0/image-layouts
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| backgroundImage | Form  | File | Y | null |
| cardImage | Form  | File | Y | null |
| name | Form  | String | Y | null |
| title | Form  | String | Y | null |
| body | Form  | String | Y | null |
| useBarcode | Form  | Boolean | Y | null |



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
  "id" : "A9z0A9z0"
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| id | String | N| 이미지 레이아웃 아이디 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 이미지 레이아웃 등록

POST {{endpoint}}/image-layout/v1.0/image-layouts
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

name=name_example
title=title_example
body=body_example
useBarcode=true
backgroundImage=@BINARY_DATA_PATH
cardImage=@BINARY_DATA_PATH


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http

curl -X POST "${endpoint}/image-layout/v1.0/image-layouts"  \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"  \
-F "name=name_example" \
-F "title=title_example" \
-F "body=body_example" \
-F "useBarcode=true"  \
-F "backgroundImage=@BINARY_DATA_PATH" \
-F "cardImage=@BINARY_DATA_PATH" 
```

</details>


<span id="imageLayoutV1x0DeleteImageLayout"></span>

## 이미지 레이아웃 삭제

이미지 레이아웃을 삭제합니다.

**요청**

```
DELETE /image-layout/v1.0/image-layouts/{id}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| id | Path  | String | Y | 이미지 레이아웃 아이디 |



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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 이미지 레이아웃 삭제

DELETE {{endpoint}}/image-layout/v1.0/image-layouts/{{id}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}



```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http

curl -X DELETE "${endpoint}/image-layout/v1.0/image-layouts/${id}"  \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"   
```

</details>


<span id="imageLayoutV1x0GetImageLayoutList"></span>

## 이미지 레이아웃 리스트 조회

이미지 레이아웃을 리스트로 조회합니다.

**요청**

```
GET /image-layout/v1.0/image-layouts
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| name | Query  | String | N | 이미지 레이아웃 이름(LIKE 검색) |
| limit | Query  | Integer | N | limit 설정하지 않으면 default 20(최대 1000) |
| offset | Query  | Integer | N | offset 설정하지 않으면 default 0 |



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
  "totalCount" : 1,
  "imageLayouts" : [ {
    "id" : "A9z0A9z0",
    "name" : "2025_프로모션_쿠폰"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | N| 총 건수 |
| imageLayouts | Array | N|  |
| imageLayouts[].id | String | N| 이미지 레이아웃 아이디 |
| imageLayouts[].name | String | N| 이미지 레이아웃 이름 |
| imageLayouts[].backgroundImage | Object | N|  |
| imageLayouts[].backgroundImage.fileName | String | N| 배경 이미지 파일 이름 |
| imageLayouts[].backgroundImage.filePreviewUrl | String | N| 배경 이미지 미리보기 URL |
| imageLayouts[].cardImage | Object | N|  |
| imageLayouts[].cardImage.fileName | String | N| 카드 이미지 파일 이름 |
| imageLayouts[].cardImage.filePreviewUrl | String | N| 카드 이미지 미리보기 URL |
| imageLayouts[].title | String | N| 제목 |
| imageLayouts[].body | String | N| 본문 |
| imageLayouts[].useBarcode | Boolean | N| 바코드 사용 여부 |
| imageLayouts[].createdDateTime | String | N| 이미지 레이아웃 생성 일시 |
| imageLayouts[].updatedDateTime | String | N| 이미지 레이아웃 수정 일시 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 이미지 레이아웃 리스트 조회

GET {{endpoint}}/image-layout/v1.0/image-layouts
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}



```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http

curl -X GET "${endpoint}/image-layout/v1.0/image-layouts"  \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"   
```

</details>


<span id="imageLayoutV1x0UpdateImageLayout"></span>

## 이미지 레이아웃 수정

이미지 레이아웃을 수정합니다.

**요청**

```
PATCH /image-layout/v1.0/image-layouts/{id}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| id | Path  | String | Y | 이미지 레이아웃 아이디 |
| backgroundImage | Form  | File | N | null |
| cardImage | Form  | File | N | null |
| name | Form  | String | N | null |
| title | Form  | String | N | null |
| body | Form  | String | N | null |
| useBarcode | Form  | Boolean | N | null |



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

| 경로 | 타입 | Null 가능 | 설명 |
| - | - | - | - |
| header | Object | N|  |
| header.isSuccessful | Boolean | N| 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | N| 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | N| 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 이미지 레이아웃 수정

PATCH {{endpoint}}/image-layout/v1.0/image-layouts/{{id}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}

name=name_example
title=title_example
body=body_example
useBarcode=true
backgroundImage=@BINARY_DATA_PATH
cardImage=@BINARY_DATA_PATH


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http

curl -X PATCH "${endpoint}/image-layout/v1.0/image-layouts/${id}"  \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"  \
-F "name=name_example" \
-F "title=title_example" \
-F "body=body_example" \
-F "useBarcode=true"  \
-F "backgroundImage=@BINARY_DATA_PATH" \
-F "cardImage=@BINARY_DATA_PATH" 
```

</details>


