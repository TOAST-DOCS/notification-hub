<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>
<h1>통계</h1>

**Notification > Notification Hub > 통계**


## 통계

Notification Hub에서 발생하는 다양한 이벤트를 수집하고 통계 데이터로 조회할 수 있습니다.

### 통계 조회

발송된 메시지의 수신 결과를 수신자의 연락처 단위로 조회할 수 있습니다.

* 메시지 채널, 발송 시점(즉시, 예약), 발송 목적, 발송/수신/열람 상태를 복합적으로 설정해 연락처 수신 결과를 조회합니다.
* 조회 시 기간은 요청 일시 기준으로 설정합니다.
    * 조회 기간 설정 가능 범위는 기본, 최대 7일입니다.
    * 조회 기간은 최대 180일 전 까지 가능합니다.
* 상세 조건 중 하나를 추가적으로 선택해 연락처 수신 결과를 조회할 수 있습니다.
    * 메시지 아이디, 템플릿 이름, 플로우 이름, 통계 키 이름, 발신 정보, 수신자 정보

* 메시지 채널, 통계 기준, 통계 키, 메시지 아이디를 복합적으로 설정해 통계 데이터를 조회합니다.
* 설정한 메시지 채널에 따라 설정할 수 있는 통계 기준이 달라집니다.

#### 메시지 채널, 통계 기준에 따른 통계 이벤트

| 메시지 채널 | 통계 기준 | 이벤트                                                                                                      | 비고 |
| - | - |----------------------------------------------------------------------------------------------------------| - |
| 전체 | 메시지 | 요청(REQUESTED), 요청 취소(CANCELED), 발송(SENT), 발송 실패(SEND_FAILED), 수신(DELIVERED), 수신 실패(DELIVERY_FAILED)    | 발송 과정에서 발생한 이벤트입니다. |
| SMS | 메시지 | 요청(REQUESTED), 요청 취소(CANCELED), 발송(SENT), 발송 실패(SEND_FAILED), 수신(DELIVERED), 수신 실패(DELIVERY_FAILED)    | |
| RCS | 메시지 | 요청(REQUESTED), 요청 취소(CANCELED), 발송(SENT), 발송 실패(SEND_FAILED), 수신(DELIVERED), 수신 실패(DELIVERY_FAILED)    | |
| 알림톡 | 메시지 | 요청(REQUESTED), 요청 취소(CANCELED), 발송(SENT), 발송 실패(SEND_FAILED), 수신(DELIVERED), 수신 실패(DELIVERY_FAILED)    | |
| 친구톡 | 메시지 | 요청(REQUESTED), 요청 취소(CANCELED), 발송(SENT), 발송 실패(SEND_FAILED), 수신(DELIVERED), 수신 실패(DELIVERY_FAILED)    | |
| Push | 메시지 | 요청(REQUESTED), 요청 취소(CANCELED), 발송(SENT), 발송 실패(SEND_FAILED), 수신(DELIVERED), 수신 실패(DELIVERY_FAILED), 열람됨(OPENED) | 메시지 열람에 대한 이벤트도 수집됩니다. |
| Email | 메시지 | 요청(REQUESTED), 요청 취소(CANCELED), 발송(SENT), 발송 실패(SEND_FAILED), 수신(DELIVERED), 수신 실패(DELIVERY_FAILED), 열람됨(OPENED) | 메시지 열람에 대한 이벤트도 수집됩니다. |
| SMS | 국제 SMS 메시지 | 요청(REQUESTED), 요청 취소(CANCELED), 발송(SENT), 발송 실패(SEND_FAILED), 수신(DELIVERED), 수신 실패(DELIVERY_FAILED)  | |

### 통계 키 관리

메시지 발송 시 통계 키를 설정하면 통계 조회에서 통계 키를 조회 조건으로 설정해 같은 통계 키로 발송된 메시지들의 통계 데이터를 조회할 수 있습니다.

1. **+ 통계 키 추가**를 클릭합니다.
2. 통계 키 이름, 상세 설명, 수집 기간을 설정합니다.
    * 수집 기간을 무제한으로 설정할 수 있습니다.
    * 기한이 없는 공지나 주기적인 발송이 필요한 메시지에 설정되는 통계 키가 해당 됩니다.
3. 수집 기간이 되지 않았거나 수집 기간이 지난 통계 키로 발생한 이벤트는 수집되지 않습니다.
    * 특정 기간 동안 진행하는 캠페인이나 이벤트인 경우 수집 기한을 정해 통계 이벤트를 수집할 수 있습니다.