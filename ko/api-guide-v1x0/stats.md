<!-- 새로운 양식을 위해 추가된 style 입니다. -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 새로운 양식을 위해 제목을 <h1>로 변경하였습니다. -->
<h1>통계</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 통계**



<span id="statsV1x0001ReadStats"></span>

## 통계 조회

통계 이벤트를 이벤트가 발생한 시간 기준으로 조회합니다.<br>


**요청**

```
GET /stats/v1.0/stats
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**요청 파라미터**

| 이름 | 구분 | 타입 | 필수 | 설명 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | 앱키 |
| X-NHN-Authorization | Header  | String | Y | 액세스 토큰 |
| eventCategory | Query  | V1x0EventCategory | Y | 이벤트 카테고리  |
| messageChannel | Query  | V1x0MessageChannel | N | 메시지 채널입니다. 설정하지 않으면 메시지 채널 전체에 대해 통계 데이터가 조회되며, 이벤트 카테고리는 메시지 발송(MESSAGE_SEND)만 설정할 수 있습니다.<br>  |
| statsKeyId | Query  | String | N | 통계 키 아이디입니다.  |
| messageId | Query  | String | N | 메시지 아이디입니다.  |
| templateId | Query  | String | N | 템플릿 아이디입니다.  |
| eventDateTimeFrom | Query  | Date | N | 통계 이벤트 조회 시작 일시(포함)입니다. 연월일시분까지 적용됩니다. 초와 밀리초는 사용되지 않습니다.<br> 예로, \"2023-12-31T00:00:30.999+09:00\"는 \"2023-12-31T00:00:00.000+09:00\"으로 처리됩니다.  |
| eventDateTimeTo | Query  | Date | N | 통계 이벤트 조회 종료 일시(미포함)입니다. 연월일시분까지 적용됩니다. 초와 밀리초는 사용되지 않습니다.<br> 예로, \"2024-01-01T00:00:30.999+09:00\"는 \"2024-01-01T00:00:00.000+09:00\"으로 처리됩니다.  |
| statsType | Query  | V1x0StatsType | N | 통계 유형<br> - MINUTELY: 0분 ~ 59분 사이 그룹핑<br> - HOURLY: 0시 ~ 23시 사이 그룹핑<br> - DAILY: 0일 ~ 30일 사이 그룹핑<br> - BY_DAY_OF_WEEK: 월화수목금토일 그룹핑<br> 예: timeGrouping을 BY_DAY_OF_WEEK로 설정하면, 30일치를 조회하더라도 요일(월~일) 기준으로 데이터가 그룹화됩니다.  |
| timeZone | Query  | String | N | 통계 조회 타임존(시간대)입니다. 예: Asia/Seoul, UTC, America/New_York <br> 통계 조회 시 데이터를 받을 때 원하는 시간대로 설정해서 받을 수 있습니다. 일반적으로 조회하는 클라이언트/브라우저의 시간대를 설정하면 됩니다.<br> 예를 들어, 요일별로 그룹핑된 통계 데이터를 한국이 아닌 다른 곳에서 조회한 경우 시간대가 다르기 때문에 원하는 데이터가 조회되지 않을 수 있습니다.  |
| statsCriteria | Query  | List | N | 조회 기준입니다. 설정된 이벤트 카테고리에 따라 설정할 수 있는 조회 기준이 달라집니다.<br>  |
| extra1 | Query  | String | N | 추가 수집되는 데이터입니다.  |
| extra2 | Query  | String | N | 추가 수집되는 데이터입니다.  |
| extra3 | Query  | String | N | 추가 수집되는 데이터입니다.  |

* 메시지 채널에 따라 설정할 수 있는 이벤트 카테고리가 달라집니다.

    | 메시지 채널 | 이벤트 카테고리 |
    | --- | --- |
    | SMS | MESSAGE_SEND, INTERNATIONAL_MESSAGE_SEND |
    | ALIMTALK, FRIENDTALK, RCS, EMAIL, PUSH | MESSAGE_SEND |
* 조회 시작 일시는 조회 기간에 포함이 되며, 조회 종료 일시는 조회 기간에 포함되지 않습니다.
    * 예: 2025년 1월 1일 하루 데이터를 조회하기 위해서는 eventDateTimeFrom을 2025-01-01T00:00:00.000+09:00로 설정하고 eventDateTimeTo를 2025-01-02T00:00:00.000+09:00로 설정해야 합니다.
* 이벤트 외 추가로 데이터를 수집해 총 3개(extra1, extra2, extra3)의 추가 필드를 제공합니다.
설정된 이벤트 카테고리에 따라 추가 수집되는 데이터의 종류가 다릅니다.

    | 이벤트 카테고리 | 추가 데이터 1 | 추가 데이터 2 | 추가 데이터 3 |
    | --- | --- | --- | --- |
    | MESSAGE_SEND | 발송 유형(SMS, LMS, MMS 등) | 발송 목적(NORMAL, AUTH, AD) | 발신 정보(발신 번호, 발신 도메인 등) |
    | INTERNATIONAL_MESSAGE_SEND | 발송 유형(SMS, LMS, MMS 등) | 발송 목적(NORMAL, AUTH, AD) | 발신 정보(발신 번호, 발신 도메인 등) |


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
  "stats" : {
    "columns" : [ {
      "name" : "EVENT_DATE_TIME"
    }, {
      "name" : "REQUESTED"
    }, {
      "name" : "SENT"
    }, {
      "name" : "SEND_FAILED"
    }, {
      "name" : "DELIVERED"
    }, {
      "name" : "DELIVERY_FAILED"
    }, {
      "name" : "OPENED"
    } ],
    "rows" : [ {
      "EVENT_DATE_TIME" : "2023-12-31T00:00:00.000+09:00",
      "REQUESTED" : 10,
      "SENT" : 10,
      "SEND_FAILED" : 1,
      "DELIVERED" : 7,
      "DELIVERY_FAILED" : 1,
      "OPENED" : 1
    } ]
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
| stats | Object | N|  |
| stats.columns | Array | N| 이벤트 카테고리에 대한 이벤트가 칼럼으로 응답됩니다.<br>EVENT_DATE_TIME 칼럼은 이벤트 발생 일시를 나타냅니다.<br> |
| stats.rows | Array | N| EVENT_DATE_TIME 필드을 제외한 나머지 필드은 이벤트 카테고리에 따라 응답됩니다.<br><br> |



**요청 예시**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 통계 조회

GET {{endpoint}}/stats/v1.0/stats?eventCategory={{eventCategory}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}



```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/stats/v1.0/stats?eventCategory=${eventCategory}"  \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"   
```

</details>