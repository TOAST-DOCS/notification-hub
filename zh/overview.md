<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Notification Hub 개요</h1>

**Notification > Notification Hub > 개요**

푸시, 이메일, SMS, RCS, 알림톡, 친구톡 메시지를 발송하고 관리하는 클라우드 기반 통합 메시징 플랫폼입니다. Notification Hub는 다양한 메시지 채널을 통합하여 메시지를 발송하고 관리할 수 있습니다. 또한, 플로우 발송을 통해 여러 메시지 채널을 우선순위에 따라 순차적으로 발송할 수 있습니다. Notification의 다른 상품과 설정과 자원을 공유해 기존 Notification 고객이 빠르게 Notification Hub로 전환할 수 있습니다.

![전체 구조](../img/overview_800.png)

## 멀티 채널 메시징

* SMS, 알림톡, 친구톡, RCS, Email, Push 6개의 메시지 채널로 메시지를 발송할 수 있습니다.
  * 다양한 메시지 채널을 하나의 API로 통합 관리하여 간편하게 메시지를 전송할 수 있습니다.

## 주소록

* 수신자의 연락처(이메일, 휴대폰 번호, 토큰)를 체계적으로 관리할 수 있습니다.
  * 수신자를 그룹으로 관리할 수 있습니다.
  * 수신자가 수신 거부한 내역을 관리하여 불필요한 메시지 발송을 방지할 수 있습니다.

## 템플릿

* 모든 메시지 채널의 템플릿을 등록 및 관리할 수 있습니다.
  * 템플릿을 통해 반복적인 메시지 작성을 줄이고, 일관된 메시지를 쉽게 발송할 수 있습니다.

## 플로우

* 사전에 등록한 템플릿으로 플로우를 생성할 수 있습니다.
  * 플로우를 이용해 최대 6개의 채널로 동시에 메시지를 발송할 수 있으며, 단말기 상태로 인해 메시지 수신을 실패하면 사전에 설정한 발송 순서에 따라 다음 순서의 채널로 자동 발송할 수 있습니다.
  * 메시지 채널의 우선순위 설정 방법에 따라 수신율을 높이거나 발송 비용을 절약하는 등 다양한 목적으로 사용할 수 있습니다.

## 대량 발송

* 메시지를 여러 수신자에게 한 번에 발송할 수 있습니다.
  * 수신자 파일 업로드
  * 수신자 목록이 저장된 Excel 파일을 업로드하여 메시지를 발송할 수 있습니다.
  * 업로드된 Excel 파일의 유효한 수신자와 유효하지 않은 수신자를 구분합니다.

## Notification 서비스 간 리소스 및 기능 설정 공유 안내

* NHN Cloud Notification의 Push, SMS, RCS Bizmessage, KakaoTalk Bizmessage, Email 서비스의 리소스 및 기능 설정 내역이 Notification Hub 서비스와 공유됩니다. (예, SMS 서비스에서 발신번호 등록 시, Notification Hub 서비스에서 해당 발신번호가 공유됨)
  기존 NHN Cloud Notification 사용자는 Notification Hub 서비스로 손쉽게 전환하여 이용할 수 있습니다.
  * 공유 항목
    * 리소스
      * 주소록
      * 발신 정보
      * 템플릿
      * 플로우
      * 통계 키
      * 본인인증
    *  기능 설정
      * (메시지 채널별) 상세 설정

## 발송량 제한 안내

* 일부 메시지 채널에서 발송량을 제한하고 있습니다.
  * SMS
    * SMS는 조직 당 월 5,000건으로 발송량을 제한합니다.
      * 발송 유형(SMS, LMS, MMS)에 관계없이 SMS와 Notification Hub 서비스의 발송량을 모두 합산하여 계산합니다.
      * 발송 기준으로 발송량을 계산합니다.
  * 알림톡/친구톡
    * 알림톡/친구톡은 각각 프로젝트 당 일 1,000건으로 발송량을 제한합니다.
* 월 발송량은 **콘솔** > **조직** > **프로젝트** > **쿼터 관리**에서 확인 가능합니다.
* 월 발송량 조정이 필요한 경우 **고객 센터** > **1:1 문의**로 문의하세요.
  * [1:1 문의 바로 가기](https://www.nhncloud.com/kr/support/inquiry)
* 리소스 제공 정책은 **사용자 가이드** > **NHN Cloud** > **리소스 제공 정책**]를 참고하세요.
  * [리소스 제공 정책 바로 가기](https://docs.nhncloud.com/ko/nhncloud/ko/resource-policy/)

## 개인정보 처리에 대한 안내

Notification Hub 서비스를 이용하는 과정에서 고객은 이용자의 개인정보를 수집할 수 있습니다. 따라서 본 서비스를 이용하는 고객은 개인정보보호법에 따라 이용자에게 법적 고지사항을 알리고 동의를 받아야 합니다.
또한, 이 과정에서 고객과 NHN Cloud 간 개인정보 처리에 관한 업무 위수탁 관계가 발생할 수 있습니다. 위탁자의 지위에 있는 고객은 수탁사인 NHN Cloud와 별도 서면에 의한 위탁 계약을 체결할 수 있으며 고객이 운영하는 개인정보처리방침에 아래 내용을 참고하여 고지할 수 있습니다.

* 수탁 업체: 엔에이치엔클라우드 ㈜
* 위탁 업무의 내용: Notification Hub 서비스 제공 업무

## 이용 약관

* [Notification 이용 약관 바로 가기](https://kr1-0lodw5frr5-real.api.nhncloudservice.com/popup/terms)
