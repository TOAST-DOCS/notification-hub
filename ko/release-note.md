<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Notification Hub 릴리스 노트</h1>

**Notification > Notification Hub > 릴리스 노트**

## 2025.02.11

### 기능 추가
* [Console/API] RCS BizCenter LMS 템플릿 발송 지원
    * RCS BizCenter LMS 템플릿 타입들도 발송할 수 있습니다.
* [API] Instant Flow Message API 추가
    * 사전에 플로우나 템플릿을 등록하지 않고도 요청 시점에 메시지를 즉시 생성·발송할 수 있는 API가 추가되었습니다.
    * 자세한 내용은 [[API v1.0 사용 가이드 > 메시지 > 인스턴트 플로우 메시지 발송](./api-guide-v1x0/message/#_6)]을 참고하시기 바랍니다.
* [Console/API] 발송 수신자 중복 체크 기능
    * 수신자 목록에 중복된 연락처가 존재하면 발송 전에 이를 확인하여 중복 발송을 방지할 수 있습니다.
* [Console] 플로우 템플릿 미리보기 기능 추가
    * 플로우 관리 메뉴에서 플로우에 포함된 여러 채널의 템플릿을 미리보기할 수 있는 기능이 추가되었습니다.
* [Console] 알림톡 바로 연결 미리보기 추가
    * 알림톡 채널 템플릿 미리보기에서 '바로 연결' 항목을 확인할 수 있도록 수정되었습니다.

### 기능 개선
* [Console/API] RCS 템플릿 기능 개선
    * RCS BizCenter에 등록한 템플릿을 다시 템플릿을 등록하지 않아도 연동되도록 개선되었습니다.
        * 브랜드 연동 시 템플릿에 자동으로 연동됩니다.
        * RCS BizCenter 템플릿은 수동 등록/수정/삭제는 불가합니다.
        * RCS BizCenter 템플릿은 챗봇, 수신거부 번호는 공란으로 등록이 되며, 발송 시에 챗봇은 가장 최근 등록한 챗봇으로 발송됩니다.

## 2024. 11. 12.

### Notification Hub 베타(beta) 출시

### 오류 수정
* [Console] 오류 수정
    * 발송, 플로우, 템플릿, 통계 기능의 오류를 수정했습니다.
* [API] 인증 오류 수정
    * 일부 API 요청 시 인증이 정상적으로 처리되지 않는 문제를 수정했습니다.

## 2024. 10. 29.

### Notification Hub 알파(alpha) 출시
* 사용 방법 안내
    * 알파로 출시된 상품은 **고객 센터 > 1:1 문의**를 통해 사용하실 수 있습니다.
* [Console] 콘솔 공개
    * 발송, 발송 조회, 주소록, 템플릿, 플로우, 상세 설정, 통계, 본인 인증 탭을 추가했습니다.
* [API] API v1.0 추가
    * 메시지, 연락처 수신 결과 목록 조회, 템플릿, 플로우 API v1.0을 추가했습니다.