<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>
<h1>Notification Hub 문제 해결 가이드</h1>

**Notification > Notification Hub > 문제 해결 가이드**

<span id="sms-delivery-failure"></span>

## 본인 인증을 진행할 수 없습니다.

Notification Hub는 사업자 회원만 본인 인증을 통해 사용할 수 있습니다. 개인 회원인 경우 본인 인증을 진행할 수 없습니다. 사업자 회원으로 재가입 후 본인 인증을 진행하세요.

## 사업자 회원으로 가입했지만, 본인 인증을 진행할 수 없습니다.

Notification Hub에서 사업자 회원의 기준은 활성화한 프로젝트의 조직의 소유자(OWNER) 회원의 유형을 따라갑니다. 조직의 소유자 회원이 개인 회원인 경우, 사업자 회원으로 본인 인증을 진행할 수 없습니다. 조직의 소유자 회원을 사업자 회원으로 변경 후 본인 인증을 진행하세요.

## 발송한 문자가 일부 수신자 단말기에서 수신 되지 않습니다.

수신자 단말기에서 문자가 수신되지 않는 경우, 수신자의 번호가 **번호 도용 문자 차단 서비스** 또는 **통신사 스팸 차단 서비스**에 가입되어 있을 수 있습니다.서비스 해지 후 문자를 재발송하세요. **번호 도용 문자 차단 서비스**와 **통신사 스팸 차단 서비스**에 대한 자세한 내용은 아래 링크를 확인하세요.

* [번호 도용 문자 차단 서비스 안내](2-service-policy-and-precondition/2-sms#about-phone-scam-blocking-services)
* [통신사 스팸 차단 서비스 안내](2-service-policy-and-precondition/2-sms#about-phone-scam-blocking-services)

## 아이폰에서 푸시 메시지가 수신되지 않고, 등록된 토큰이 삭제됩니다.

아이폰 앱에서 토큰을 등록하고 푸시 메시지를 발송했지만, 푸시 메시지가 수신되지 않고 등록된 토큰이 삭제되는 경우, 아래 사항을 확인하세요.

* **APNS JWT 인증 정보 불일치**
  * Notification Hub에 등록된 APNS JWT 인증 정보와 앱이 불일치 하면 푸시 메시지가 수신되지 않습니다. APNS JWT 인증 정보와 앱의 번들 ID가 함께 사용할 수 있는지 확인하세요.
* **앱의 빌드 타입과 등록된 토큰의 연락처 타입(Contact Type) 불일치**
  * 앱의 빌드 타입와 등록된 토큰의 연락처 타입이 맞지 않으면 푸시 메시지가 수신되지 않습니다. 연락처 타입과 빌드 모드를 확인하세요.
  * 개발(Development) 앱의 토큰은 연락처 타입이 TOKEN_APNS_SANDBOX, 또는 TOKEN_APNS_SANDBOX_VOIP으로 등록되어야 합니다.
  * 운영(Production) 앱의 토큰은 연락처 타입이 TOKEN_APNS, 또는 TOKEN_APNS_VOIP으로 등록되어야 합니다.
  * 각 연락처 타입은 SDK에서는 다음과 같습니다.
    * TOKEN_APNS: APNS
    * TOKEN_APNS_SANDBOX: APNS_SANDBOX
    * TOKEN_APNS_VOIP: APNS_VOIP
    * TOKEN_APNS_SANDBOX_VOIP: APNS_SANDBOXVOIP

## 안드로이드 단말기에서 푸시 메시지가 수신되지 않고, 등록된 토큰이 삭제됩니다.
  
안드로이드 앱에서 토큰을 등록하고 푸시 메시지를 발송했지만, 푸시 메시지가 수신되지 않고 등록된 토큰이 삭제되는 경우, 아래 사항을 확인하세요.

* **FCM 서비스 계정 키(JSON)와 앱의 발신자 아이디(Sender ID) 불일치**
  * Notification Hub에 등록된 FCM 서비스 계정 키(JSON)와 앱의 발신자 아이디(Sender ID)가 불일치 하면 푸시 메시지가 수신되지 않습니다. FCM 서비스 계정 키(JSON)와 앱의 발신자 아이디(Sender ID)를 함께 사용할 수 있는지 확인하세요.
    * [FCM 발신자 이이디](https://firebase.google.com/docs/cloud-messaging/concept-options#credentials)
    * [FCM 서비스 계정 키(JSON) 생성](https://firebase.google.com/docs/cloud-messaging/http-server-ref)
        ```
        A registration token is tied to a certain group of senders. 
      When a client app registers for FCM, it must specify which senders are allowed to send messages. You should use one of those sender IDs when sending messages to the client app. If you switch to a different sender, the existing registration tokens won't work.
        ```


!!! tip "문제가 해결되지 않을 경우"
* 온라인 1:1 문의: [https://www.nhncloud.com/kr/support/inquiry?alias=tab5_03](https://www.nhncloud.com/kr/support/inquiry?alias=tab5_03)
* 대표 전화: 1588-7967 (운영 시간: 월\~금 10:00-19:00)