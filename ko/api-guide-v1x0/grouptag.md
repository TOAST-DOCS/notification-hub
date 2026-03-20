<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>그룹 태그</h1>




<span id="kakaobizcenterV10GroupTagsGet"></span>

## 그룹 태그 전체 목록 조회

카카오 비즈센터 그룹 태그 전체 목록을 조회합니다.

**요청**

```
GET /kakaobizcenter/v1.0/group-tags
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | 앱키 |
| X-NHN-Authorization | Header  | String | O | 액세스 토큰 |
| senderKey | Query  | String | O | 발신 프로필 키 |



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
  "groupTags" : [ {
    "groupTagKey" : "b85552999bbb335777d16fbbbbbb552b3078aaa",
    "groupTagName" : "20240619-00001"
  } ]
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| groupTags | Array | O |  |
| groupTags[].groupTagKey | String | O | 그룹 태그 키 |
| groupTags[].groupTagName | String | O | 그룹 태그 이름 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 그룹 태그 전체 목록 조회

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

## 그룹 태그 삭제

카카오 비즈센터 그룹 태그를 삭제합니다.

**요청**

```
DELETE /kakaobizcenter/v1.0/group-tags/{groupTagKey}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | 앱키 |
| X-NHN-Authorization | Header  | String | O | 액세스 토큰 |
| groupTagKey | Path  | String | O | 그룹 태그 키 |
| senderKey | Query  | String | O | 발신 프로필 키 |



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

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 그룹 태그 삭제

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

## 그룹 태그 단건 조회

카카오 비즈센터 그룹 태그 단건을 조회합니다.

**요청**

```
GET /kakaobizcenter/v1.0/group-tags/{groupTagKey}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | 앱키 |
| X-NHN-Authorization | Header  | String | O | 액세스 토큰 |
| groupTagKey | Path  | String | O | 그룹 태그 키 |
| senderKey | Query  | String | O | 발신 프로필 키 |



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
  "groupTag" : {
    "groupTagKey" : "b85552999bbb335777d16fbbbbbb552b3078aaa",
    "groupTagName" : "20240619-00001"
  }
}
```

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| groupTag | Object | O |  |
| groupTag.groupTagKey | String | O | 그룹 태그 키 |
| groupTag.groupTagName | String | O | 그룹 태그 이름 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 그룹 태그 단건 조회

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

## 그룹 태그 수정

카카오 비즈센터 그룹 태그를 수정합니다.

**요청**

```
PUT /kakaobizcenter/v1.0/group-tags/{groupTagKey}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | 앱키 |
| X-NHN-Authorization | Header  | String | O | 액세스 토큰 |
| groupTagKey | Path  | String | O | 그룹 태그 키 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "newGroupTagName" : "20240619-00001"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| senderKey | String | O | 발신 프로필 키 |
| newGroupTagName | String | O | 새 그룹 태그 이름 |



**응답 본문**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

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

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| groupTag | Object | O |  |
| groupTag.groupTagKey | String | O | 그룹 태그 키 |
| groupTag.groupTagName | String | O | 그룹 태그 이름 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 그룹 태그 수정

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

## 그룹 태그 등록

카카오 비즈센터 그룹 태그를 등록합니다.

**요청**

```
POST /kakaobizcenter/v1.0/group-tags
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | O | 앱키 |
| X-NHN-Authorization | Header  | String | O | 액세스 토큰 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "senderKey" : "883b8b5375fd0960caa1cdeb4bd870c8cdfa403a",
  "groupTagName" : "20240619-00001"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| senderKey | String | O | 발신 프로필 키 |
| groupTagName | String | O | 그룹 태그 이름 |



**응답 본문**

<!--응답 본문을 반환하지 않는다면 "이 API는 응답 본문을 반환하지 않습니다"로 입력합니다.-->

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

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | Not Null | 설명 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | O | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | O | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| groupTag | Object | O |  |
| groupTag.groupTagKey | String | O | 그룹 태그 키 |
| groupTag.groupTagName | String | O | 그룹 태그 이름 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 그룹 태그 등록

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
