<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Notification Hub 릴리스 노트</h1>

**Notification > Notification Hub > 릴리스 노트**

### 2025. 08. 26.
#### 기능 개선
* [API/Console] 금융준법고지 필드 포함 이미지 템플릿 지원
  * 금융준법고지 필드가 포함된 이미지 템플릿의 연동 및 발송을 지원합니다.

## 2025. 07. 29.
### 기능 추가
* [API/Console] 이미지 레이아웃 기능이 추가되었습니다.
    * 이미지 레이아웃은 개인화된 MMS 첨부 이미지를 생성하기 위한 기능입니다.
    * 이미지 레이아웃은 MMS 템플릿 생성 시 선택할 수 있으며, MMS 템플릿에 연동된 이미지 레이아웃을 통해 개인화된 이미지를 생성할 수 있습니다.
    * 자세한 내용은 [콘솔 사용 가이드 > 발송](./console-guide/image-layout), [API v1.0 사용 가이드 > 메시지 > 이미지 레이아웃](./api-guide-v1x0/image-layout)을 참고하시기 바랍니다.
* [API/Console] MMS 템플릿에 이미지 레이아웃을 연동할 수 있습니다.
    * MMS 템플릿 생성 시 첨부 파일 섹션에서 이미지 레이아웃을 선택할 수 있습니다.
    * 자세한 내용은 [콘솔 사용 가이드 > 템플릿](./console-guide/template/#templateV1x0001CreateSmsTemplate) [API v1.0 사용 가이드 > 메시지 > MMS 템플릿](./api-guide-v1x0/template/#templateV1x0001CreateSmsTemplate)을 참고하시기 바랍니다.
* [Console] 국제 SMS 발송 시, 발송 상세 조회에서 인코딩, 실 발송 건수를 확인할 수 있습니다.
* [Console] "첨부 파일 관리" 메뉴의 위치가 변경되었습니다.
    * "상세 설정" 메뉴 하위에 있던 첨부 파일 관리 메뉴가 상단 메뉴로 이동되었습니다.

## 2025. 05. 27.
### 기능 추가
* [Console] 지정한 이벤트 발생 시 URL을 지정하여 웹훅 이벤트를 받을 수 있습니다.
    * 자세한 내용은 [콘솔 사용 가이드 > 상세 설정 > 웹훅](./console-guide/detailed-setting/#webhook)을 참고하시기 바랍니다.
* [Console] 지난 메시지 발송 내역을 백업 할 수 있습니다.
    * 자세한 내용은 [콘솔 사용 가이드 > 상세 설정 > 백업](./console-guide/detailed-setting/#backup)을 참고하시기 바랍니다.

## 2025. 04. 15.
### 기능 추가
* [API/Console] 서비스에서 발생하는 다양한 이벤트 이력을 CloudTrail에서 확인할 수 있습니다.
    * 확인 가능한 이벤트 목록은 [[CloudTrail > 수집되는 이벤트 목록]](../../../Governance%20&%20Audit/CloudTrail/ko/event-list)을 참고하시기 바랍니다.
* [API/Console] RCS 인증용 메시지 발송이 추가되었습니다.
* [API] 연락처별 수신 결과 목록 조회 API에 응답 필드가 추가되었습니다.
    * 자세한 내용은 [[API v1.0 사용 가이드 > 연락처별 수신 결과 > 연락처별 수신 결과 목록 조회]](./api-guide-v1x0/contact-delivery-result/#_1)를 참고하시기 바랍니다.
* [Console] RCS BizCenter LMS 포맷형 지원
    * RCS 메시지 발송 시 LMS 포맷형으로 발송할 수 있습니다.
    * 템플릿 생성 시 LMS 포맷형을 선택할 수 있습니다.

### 기능 개선
* [API/Console] Push 채널의 수신, 열림 이벤트가 통계에 수집되도록 개선되었습니다.

## 2025. 03. 25.
### 기능 추가
* [API] 첨부파일/통계 API 가 추가되었습니다.
    * 자세한 내용은 [[API v1.0 사용 가이드 > 첨부파일]](./api-guide-v1x0/attachment), [[API v1.0 사용 가이드 > 통계]](./api-guide-v1x0/stats)를 참고하시기 바랍니다.

## 2025. 03. 11.

### 기능 추가
* [API] RCS BizCenter 브랜드 메시지 통계 연동
    * 메시지 발송 시 그룹ID를 추가하여 RCS BizCenter 가 제공하는 메시지 통계를 사용할 수 있습니다.
* [API] RCS 메시지 수신 대기 만료 기간 설정값 추가
    * RCS 메시지 발송 시, 디바이스로의 전송 시도에 대한 타임아웃(4가지 유형)을 설정할 수 있습니다.
* [API] RCS BizCenter LMS 포맷형 지원
    * RCS 메시지 발송 시 LMS 포맷형으로 발송할 수 있습니다.
    * 템플릿 생성 시 LMS 포맷형을 선택할 수 있습니다.
* 자세한 내용은 [[API v1.0 사용 가이드 > 메시지]](./api-guide-v1x0/message)를 참고하시기 바랍니다.

### 기능 개선
* [Console] RCS 템플릿 기능 개선
    * 이제 RCS BizCenter 템플릿 연동 시 브랜드 연동 버튼을 클릭할 필요가 없으며, RCS BizCenter 템플릿의 변경 사항이 자동으로 반영됩니다.

## 2025. 02. 25.

### 기능 추가
* [API] 연락처별 최종 발송 결과 목록 조회 API가 추가되었습니다.
    * 자세한 내용은 [[API v1.0 사용 가이드 > 연락처별 수신 결과 > 연락처별 최종 발송 결과 목록 조회]](./api-guide-v1x0/contact-delivery-result/#_2)를 참고하시기 바랍니다.
* [API] RCS Bizcenter 템플릿 발송 시 대화방 아이디, 수신거부번호를 추가할 수 있도록 개선되었습니다.

### 기능 개선
* [Console] 발송 조회 시 상세 결과 코드 및 메시지를 확인 할 수 있도록 개선되었습니다.

## 2025. 02. 11.

### 기능 추가
* [Console/API] RCS BizCenter LMS 템플릿 발송 지원
    * RCS BizCenter LMS 템플릿 타입들도 발송할 수 있습니다.
* [API] Instant Flow Message API 추가
    * 사전에 플로우나 템플릿을 등록하지 않고도 요청 시점에 메시지를 즉시 생성·발송할 수 있는 API가 추가되었습니다.
    * 자세한 내용은 [[API v1.0 사용 가이드 > 메시지 > 인스턴트 플로우 메시지 발송]](./api-guide-v1x0/message/#_6)을 참고하시기 바랍니다.
* [Console/API] 발송 수신자 중복 체크 기능
    * 수신자 목록에 중복된 연락처가 존재하면 발송 전에 이를 확인하여 중복 발송을 방지할 수 있습니다.
* [Console] 플로우 템플릿 미리보기 기능 추가
    * 플로우 관리 메뉴에서 플로우에 포함된 여러 채널의 템플릿을 미리보기할 수 있는 기능이 추가되었습니다.
* [Console] 알림톡 바로 연결 미리보기 추가
    * 알림톡 채널 템플릿 미리보기에서 '바로 연결' 항목을 확인할 수 있도록 수정되었습니다.
* [API] 발송 API 사용자 커스텀 필드 추가
    * 발송 API 요청 시 사용자 커스텀 필드를 포함하여 요청할 수 있도록 추가되었습니다.
    * 자세한 내용은 [[API v1.0 사용 가이드 > 메시지]](./api-guide-v1x0/message)를 참고하시기 바랍니다.

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
