<!-- pre-align:aligned sig=ff946ac84827 -->

<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>카카오 통계</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 카카오 통계**

카카오 비즈센터에서 제공하는 통계 데이터를 조회합니다.
통계 데이터는 발신 키 기준으로 일별(DAILY) 또는 월별(MONTHLY)로 조회할 수 있습니다.
DAILY: 최근 90일 이내 데이터만 조회 가능하며, 조회 범위는 최대 90일입니다.
MONTHLY: 최근 3개월 이내 데이터만 조회 가능하며, 조회 범위는 최대 3개월입니다.

* 실시간 통계는 제공하지 않으며, 전날 수집한 데이터를 매일 오전 7시경 제공합니다.
* 알림톡 통계는 D+1에 최초 제공하며, D+2에 확정합니다.
* 유효 읽음 수는 같은 메시지에 대해 중복 집계하지 않습니다.
* 클릭 수는 같은 메시지에 대해 중복 집계합니다.
* 발송 성공 건수가 10건 이하이면 유효 읽음 수와 클릭 수를 제공하지 않습니다.

### 발송 통계

발신 프로필을 기준으로 일별 발송 수, 유효 읽음 수, 클릭 수를 조회합니다. 기간, 발송 식별자, 메시지 타입 등을 설정해 조회할 수 있습니다.

<a id="template-statistics"></a>

### 템플릿 통계

템플릿 및 그룹 태그를 기준으로 일별 발송 수, 유효 읽음 수, 클릭 수를 조회합니다. 기간, 메시지 타입 등을 설정해 조회할 수 있습니다.

* 브랜드 메시지 자유형은 그룹 태그를 사용한 경우에만 제공합니다.



<span id="kakaobizcenterV1x0001ReadAlimtalkDeliveryStatistics"></span>

<a id="retrieve-alimtalk-delivery-statistics"></a>

## 알림톡 발송 통계 조회

알림톡 발송 통계를 조회합니다.
발신 프로필을 기준으로 일별 발송 수, 유효 읽음 수, 클릭 수를 조회합니다. 기간, 발송 식별자, 메시지 타입 등을 설정해 조회할 수 있습니다.

조회 기간(startDate ~ endDate)은 최대 3개월입니다.


**요청**

```
GET /kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/ALIMTALK
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| senderKey | Query | String | O | 발신 키입니다. |
| periodType | Query | Enum | O | 조회 기간 단위입니다. |
| startDate | Query | String | O | 조회 시작 날짜입니다. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) |
| endDate | Query | String | O | 조회 종료 날짜입니다. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) startDate ~ endDate는 최대 3개월입니다. |
| messageType | Query | Enum | X | 메시지 유형입니다. |
| receiveUserType | Query | Enum | X | 발송 식별자입니다. |
| limit | Query | Number | X | limit을 설정하지 않으면 기본값은 500입니다. (최대 1,000) |
| offset | Query | Number | X | offset을 설정하지 않으면 기본값은 0입니다. |



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
  "alimtalkDeliveryStatistics" : [ {
    "date" : "2026-01-15",
    "messageType" : "AT",
    "receiveUserType" : "PhoneNumber",
    "totalSendRequestCount" : 1000,
    "validSendRequestCount" : 950,
    "validReadCount" : 800
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
| totalCount | Integer | O | 총 건수 |
| alimtalkDeliveryStatistics | Array | O |  |
| alimtalkDeliveryStatistics[].date | String | O | 날짜 (일별: YYYY-MM-DD, 월별: YYYY-MM) |
| alimtalkDeliveryStatistics[].messageType | String | O | 알림톡 메시지 유형<br>[AT(일반 알림톡), AI(이미지 알림톡)] |
| alimtalkDeliveryStatistics[].receiveUserType | String | O | 발송 식별자<br>[PhoneNumber(전화번호), AppUserId(앱 유저 아이디), UserKey(유저 키), None(수신자 식별자 없음)] |
| alimtalkDeliveryStatistics[].totalSendRequestCount | Integer | O | 총 발송 요청 수 |
| alimtalkDeliveryStatistics[].validSendRequestCount | Integer | O | 유효 발송 요청 수 |
| alimtalkDeliveryStatistics[].validReadCount | Integer | O | 유효 읽음 수 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 발송 통계 조회

GET {{endpoint}}/kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/ALIMTALK?senderKey={{senderKey}}&periodType={{periodType}}&startDate={{startDate}}&endDate={{endDate}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/ALIMTALK?senderKey=${senderKey}&periodType=${periodType}&startDate=${startDate}&endDate=${endDate}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="kakaobizcenterV1x0002ReadAlimtalkTemplateStatistics"></span>

<a id="retrieve-alimtalk-template-statistics"></a>

## 알림톡 템플릿 통계 조회

알림톡 템플릿 통계를 조회합니다.
템플릿 및 그룹 태그를 기준으로 일별 발송 수, 유효 읽음 수, 클릭 수를 조회합니다. 기간, 메시지 타입 등을 설정해 조회할 수 있습니다.

조회 기간(startDate ~ endDate)은 최대 3개월입니다.


**요청**

```
GET /kakaobizcenter/v1.0/kakao-statistics/template-statistics/ALIMTALK
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| senderKey | Query | String | O | 발신 키입니다. |
| periodType | Query | Enum | O | 조회 기간 단위입니다. |
| startDate | Query | String | O | 조회 시작 날짜입니다. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) |
| endDate | Query | String | O | 조회 종료 날짜입니다. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) startDate ~ endDate는 최대 3개월입니다. |
| kakaoTemplateCode | Query | String | X | 카카오 템플릿 코드입니다. |
| messageType | Query | Enum | X | 메시지 유형입니다. |
| limit | Query | Number | X | limit을 설정하지 않으면 기본값은 500입니다. (최대 1,000) |
| offset | Query | Number | X | offset을 설정하지 않으면 기본값은 0입니다. |



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
  "alimtalkTemplateStatistics" : [ {
    "date" : "2026-01-15",
    "messageType" : "AT",
    "templateCode" : "template_001",
    "totalSendSuccessCount" : 950,
    "validReadCount" : 800,
    "totalClickCount" : 500
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
| totalCount | Integer | O | 총 건수 |
| alimtalkTemplateStatistics | Array | O |  |
| alimtalkTemplateStatistics[].date | String | O | 날짜 (일별: YYYY-MM-DD, 월별: YYYY-MM) |
| alimtalkTemplateStatistics[].messageType | String | O | 알림톡 메시지 유형<br>[AT(일반 알림톡), AI(이미지 알림톡)] |
| alimtalkTemplateStatistics[].templateCode | String | O | 템플릿 코드 |
| alimtalkTemplateStatistics[].totalSendSuccessCount | Integer | O | 총 발송 성공 수 |
| alimtalkTemplateStatistics[].validReadCount | Integer | O | 유효 읽음 수 |
| alimtalkTemplateStatistics[].totalClickCount | Integer | O | 총 클릭 수 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 알림톡 템플릿 통계 조회

GET {{endpoint}}/kakaobizcenter/v1.0/kakao-statistics/template-statistics/ALIMTALK?senderKey={{senderKey}}&periodType={{periodType}}&startDate={{startDate}}&endDate={{endDate}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/kakao-statistics/template-statistics/ALIMTALK?senderKey=${senderKey}&periodType=${periodType}&startDate=${startDate}&endDate=${endDate}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="kakaobizcenterV1x0003ReadBrandmessageDeliveryStatistics"></span>

<a id="retrieve-brand-message-delivery-statistics"></a>

## 브랜드 메시지 발송 통계 조회

브랜드 메시지 발송 통계를 조회합니다.
발신 프로필을 기준으로 일별 발송 수, 유효 읽음 수, 클릭 수를 조회합니다. 기간, 발송 식별자, 메시지 타입 등을 설정해 조회할 수 있습니다.

조회 기간(startDate ~ endDate)은 최대 3개월입니다.


**요청**

```
GET /kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/BRANDMESSAGE
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| senderKey | Query | String | O | 발신 키입니다. |
| periodType | Query | Enum | O | 조회 기간 단위입니다. |
| startDate | Query | String | O | 조회 시작 날짜입니다. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) |
| endDate | Query | String | O | 조회 종료 날짜입니다. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) startDate ~ endDate는 최대 3개월입니다. |
| messageSpec | Query | Enum | X | 발송 타입입니다. |
| chatBubbleType | Query | Enum | X | 메시지 타입입니다. |
| targeting | Query | Enum | X | 발송 타겟팅 여부입니다. |
| friendType | Query | Enum | X | 친구 타입입니다. |
| receiveUserType | Query | Enum | X | 발송 식별자입니다. |
| limit | Query | Number | X | limit을 설정하지 않으면 기본값은 500입니다. (최대 1,000) |
| offset | Query | Number | X | offset을 설정하지 않으면 기본값은 0입니다. |



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
  "brandmessageDeliveryStatistics" : [ {
    "date" : "2026-01-15",
    "receiveUserType" : "PhoneNumber",
    "messageSpec" : "BASIC",
    "chatBubbleType" : "TEXT",
    "friendType" : "F",
    "targeting" : "M",
    "totalSendRequestCount" : 1000,
    "validSendRequestCount" : 950,
    "validReadCount" : 800,
    "totalClickCount" : 500
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
| totalCount | Integer | O | 총 건수 |
| brandmessageDeliveryStatistics | Array | O |  |
| brandmessageDeliveryStatistics[].date | String | O | 날짜 (일별: YYYY-MM-DD, 월별: YYYY-MM) |
| brandmessageDeliveryStatistics[].receiveUserType | String | O | 발송 식별자<br>[PhoneNumber(전화번호), AppUserId(앱 유저 아이디), UserKey(유저 키), None(수신자 식별자 없음)] |
| brandmessageDeliveryStatistics[].messageSpec | String | O | 발송 타입<br>[BASIC(기본형), FREESTYLE(자유형)] |
| brandmessageDeliveryStatistics[].chatBubbleType | String | O | 메시지 타입<br>[TEXT(텍스트형), IMAGE(이미지형), WIDE(와이드 이미지형), WIDE_ITEM_LIST(와이드 아이템리스트형), CAROUSEL_FEED(캐러셀 피드형), PREMIUM_VIDEO(프리미엄 비디오형), COMMERCE(커머스형), CAROUSEL_COMMERCE(캐러셀 커머스형)] |
| brandmessageDeliveryStatistics[].friendType | String | O | 친구 타입<br>[F(친구), N(비친구)] |
| brandmessageDeliveryStatistics[].targeting | String | O | 발송 타겟팅 여부<br>[M(마케팅 수신 동의 유저 전체), N(채널 친구 제외), I(채널 친구만), F(채널 친구 전체)] |
| brandmessageDeliveryStatistics[].totalSendRequestCount | Integer | O | 총 발송 요청 수 |
| brandmessageDeliveryStatistics[].validSendRequestCount | Integer | O | 유효 발송 요청 수 |
| brandmessageDeliveryStatistics[].validReadCount | Integer | O | 유효 읽음 수 |
| brandmessageDeliveryStatistics[].totalClickCount | Integer | O | 총 클릭 수 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 브랜드 메시지 발송 통계 조회

GET {{endpoint}}/kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/BRANDMESSAGE?senderKey={{senderKey}}&periodType={{periodType}}&startDate={{startDate}}&endDate={{endDate}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/BRANDMESSAGE?senderKey=${senderKey}&periodType=${periodType}&startDate=${startDate}&endDate=${endDate}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="kakaobizcenterV1x0004ReadBrandmessageTemplateStatistics"></span>

<a id="retrieve-brand-message-template-statistics"></a>

## 브랜드 메시지 템플릿 통계 조회

브랜드 메시지 템플릿 통계를 조회합니다.
템플릿 및 그룹 태그를 기준으로 일별 발송 수, 유효 읽음 수, 클릭 수를 조회합니다. 기간, 메시지 타입 등을 설정해 조회할 수 있습니다.

조회 기간(startDate ~ endDate)은 최대 3개월입니다.


**요청**

```
GET /kakaobizcenter/v1.0/kakao-statistics/template-statistics/BRANDMESSAGE
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | 앱키 |
| X-NHN-Authorization | Header | String | O | 액세스 토큰 |
| senderKey | Query | String | O | 발신 키입니다. |
| periodType | Query | Enum | O | 조회 기간 단위입니다. |
| startDate | Query | String | O | 조회 시작 날짜입니다. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) |
| endDate | Query | String | O | 조회 종료 날짜입니다. (DAILY: YYYY-MM-DD, MONTHLY: YYYY-MM) startDate ~ endDate는 최대 3개월입니다. |
| kakaoTemplateCode | Query | String | X | 카카오 템플릿 코드입니다. |
| groupTagKey | Query | String | X | 그룹 태그 키입니다. |
| messageSpec | Query | Enum | X | 발송 타입입니다. |
| chatBubbleType | Query | Enum | X | 메시지 타입입니다. |
| targeting | Query | Enum | X | 발송 타겟팅 여부입니다. |
| friendType | Query | Enum | X | 친구 타입입니다. |
| limit | Query | Number | X | limit을 설정하지 않으면 기본값은 500입니다. (최대 1,000) |
| offset | Query | Number | X | offset을 설정하지 않으면 기본값은 0입니다. |



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
  "brandmessageTemplateStatistics" : [ {
    "date" : "2026-01-15",
    "templateCode" : "template_001",
    "groupTagKey" : "group_tag_001",
    "messageSpec" : "BASIC",
    "chatBubbleType" : "TEXT",
    "friendType" : "F",
    "targeting" : "M",
    "totalSendSuccessCount" : 950,
    "validReadCount" : 800,
    "totalClickCount" : 500
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
| totalCount | Integer | O | 총 건수 |
| brandmessageTemplateStatistics | Array | O |  |
| brandmessageTemplateStatistics[].date | String | O | 날짜 (일별: YYYY-MM-DD, 월별: YYYY-MM) |
| brandmessageTemplateStatistics[].templateCode | String | O | 템플릿 코드 |
| brandmessageTemplateStatistics[].groupTagKey | String | X | 그룹 태그 키 |
| brandmessageTemplateStatistics[].messageSpec | String | O | 발송 타입<br>[BASIC(기본형), FREESTYLE(자유형)] |
| brandmessageTemplateStatistics[].chatBubbleType | String | O | 메시지 타입<br>[TEXT(텍스트형), IMAGE(이미지형), WIDE(와이드 이미지형), WIDE_ITEM_LIST(와이드 아이템리스트형), CAROUSEL_FEED(캐러셀 피드형), PREMIUM_VIDEO(프리미엄 비디오형), COMMERCE(커머스형), CAROUSEL_COMMERCE(캐러셀 커머스형)] |
| brandmessageTemplateStatistics[].friendType | String | O | 친구 타입<br>[F(친구), N(비친구)] |
| brandmessageTemplateStatistics[].targeting | String | O | 발송 타겟팅 여부<br>[M(마케팅 수신 동의 유저 전체), N(채널 친구 제외), I(채널 친구만), F(채널 친구 전체)] |
| brandmessageTemplateStatistics[].totalSendSuccessCount | Integer | O | 총 발송 성공 수 |
| brandmessageTemplateStatistics[].validReadCount | Integer | O | 유효 읽음 수 |
| brandmessageTemplateStatistics[].totalClickCount | Integer | O | 총 클릭 수 |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 브랜드 메시지 템플릿 통계 조회

GET {{endpoint}}/kakaobizcenter/v1.0/kakao-statistics/template-statistics/BRANDMESSAGE?senderKey={{senderKey}}&periodType={{periodType}}&startDate={{startDate}}&endDate={{endDate}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/kakao-statistics/template-statistics/BRANDMESSAGE?senderKey=${senderKey}&periodType=${periodType}&startDate=${startDate}&endDate=${endDate}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

