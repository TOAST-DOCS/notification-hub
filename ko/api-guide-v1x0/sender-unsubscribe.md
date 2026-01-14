<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>발신 정보</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 발신 정보**



<span id="senderV1x0001RegisterExternalUnsubscribePhoneNumber"></span>

## 080 수신 거부 외부 번호 등록 신청

080 수신 거부 외부 번호 등록 신청을 합니다.


**요청**

```
POST /sender/v1.0/unsubscribe-phone-numbers/external
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |



**요청 본문**

<!--요청 본문을 요구하지 않는다면 "이 API는 요청 본문을 요구하지 않습니다"로 입력합니다.-->


```
{
  "unsubscribePhoneNumber" : "0801234567",
  "corporationName" : "회사명"
}
```

<!--요청 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 필수 | 설명 |
| - | - | - | - |
| unsubscribePhoneNumber | String | Y | 080 수신 거부 외부 번호 |
| corporationName | String | Y | 회사명 |



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
### 080 수신 거부 외부 번호 등록 신청

POST {{endpoint}}/sender/v1.0/unsubscribe-phone-numbers/external
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "unsubscribePhoneNumber" : "0801234567",
  "corporationName" : "회사명"
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
  "corporationName" : "회사명"
}'
```

</details>
<span id="senderV1x0002TerminateExternalUnsubscribePhoneNumber"></span>

## 080 수신 거부 외부 등록 번호 해지

080 수신 거부 외부 등록 번호를 해지합니다.


**요청**

```
DELETE /sender/v1.0/unsubscribe-phone-numbers/external/{unsubscribePhoneNumber}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| unsubscribePhoneNumber | Path  | String | N | 080 수신 거부 외부 번호 |



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
### 080 수신 거부 외부 등록 번호 해지

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

## 080 수신 거부 번호 목록 조회

080 수신 거부 번호 목록을 조회합니다.


**요청**

```
GET /sender/v1.0/unsubscribe-phone-numbers
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| unsubscribePhoneNumber | Query  | String | N | 수신 거부 번호(LIKE 검색) |
| limit | Query  | Integer | N | limit 설정하지 않으면 default 50(최대 1000) |
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
  "unsubscribePhoneNumbers" : [ {
    "unsubscribePhoneNumber" : "0801234567",
    "corporationName" : "회사명",
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

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| totalCount | Integer | 총 건수 |
| unsubscribePhoneNumbers | Array | 080 수신 거부 번호 목록 |
| unsubscribePhoneNumbers[].unsubscribePhoneNumber | String | 080 수신 거부 번호 |
| unsubscribePhoneNumbers[].corporationName | String | 회사명 |
| unsubscribePhoneNumbers[].shareStatus | String | 080 수신 거부 번호 공유 상태<br>[PRIMARY(직접 등록한 080 번호), SECONDARY(공유 받은 080 번호)] |
| unsubscribePhoneNumbers[].provider | String | 080 수신 거부 번호 제공처 유형<br>[INTERNAL(내부 발급 번호), EXTERNAL(외부 등록 번호)] |
| unsubscribePhoneNumbers[].status | String | 080 수신 거부 번호 상태<br>[READY(준비), RESERVE_USE(심사 중), IN_USE(사용 중), TERMINATED(해지)] |
| unsubscribePhoneNumbers[].terminable | Boolean | 해지 가능 여부 |
| unsubscribePhoneNumbers[].requestedDateTime | String | 신청 일시 |
| unsubscribePhoneNumbers[].startedDateTime | String | 개통 일시 |
| unsubscribePhoneNumbers[].deletedDateTime | String | 해지 일시 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 080 수신 거부 번호 목록 조회

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

## 080 수신 거부 번호 단건 조회

080 수신 거부 번호 단건을 조회합니다.


**요청**

```
GET /sender/v1.0/unsubscribe-phone-numbers/{unsubscribePhoneNumber}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| unsubscribePhoneNumber | Path  | String | N | 수신 거부 번호 |



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
  "unsubscribePhoneNumber" : {
    "unsubscribePhoneNumber" : null,
    "corporationName" : "회사명",
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

<!--응답 본문의 필드를 설명합니다.-->

| 경로 | 타입 | 설명 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 요청이 성공했는지 여부를 나타냅니다.<br>기본값: true |
| header.resultCode | Integer | 요청의 결과 코드입니다.<br>기본값: 0 |
| header.resultMessage | String | 요청의 결과 메시지입니다.<br>기본값: SUCCESS |
| unsubscribePhoneNumber | Object |  |
| unsubscribePhoneNumber.unsubscribePhoneNumber | String | 080 수신 거부 번호 |
| unsubscribePhoneNumber.corporationName | String | 회사명 |
| unsubscribePhoneNumber.shareStatus | String | 080 수신 거부 번호 공유 상태<br>[PRIMARY(직접 등록한 080 번호), SECONDARY(공유 받은 080 번호)] |
| unsubscribePhoneNumber.provider | String | 080 수신 거부 번호 제공처 유형<br>[INTERNAL(내부 발급 번호), EXTERNAL(외부 등록 번호)] |
| unsubscribePhoneNumber.status | String | 080 수신 거부 번호 상태<br>[READY(준비), RESERVE_USE(심사 중), IN_USE(사용 중), TERMINATED(해지)] |
| unsubscribePhoneNumber.terminable | Boolean | 해지 가능 여부 |
| unsubscribePhoneNumber.requestedDateTime | String | 신청 일시 |
| unsubscribePhoneNumber.startedDateTime | String | 개통 일시 |
| unsubscribePhoneNumber.deletedDateTime | String | 해지 일시 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 080 수신 거부 번호 단건 조회

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
