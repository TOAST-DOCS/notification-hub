<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Email</h1>

**Notification > Notification Hub > 이용 정책 및 사전 설정 안내 > Email**

## 발신 도메인과 DNS TXT 레코드 등록

Notification Hub에서 이메일을 발송하려면 자신이 소유한 발신 도메인이 있어야 합니다. 각 사용자가 자신의 도메인을 통해 발신자 신원을 인증하고 이메일이 스팸으로 분류되지 않도록 하기 위함입니다. 발신 도메인을 통해 SPF, DKIM, DMARC 등의 인증 설정을 적용하여 이메일의 신뢰성을 높일 수 있습니다. 이를 통해 이메일이 수신자의 메일함에 안전하게 도달하고, 피싱이나 스푸핑을 방지할 수 있습니다. Notification Hub 이메일 발송(SMTP) 서버를 통해 사용자 소유의 도메인이 포함된 이메일 주소와 함께 이메일이 수신 서버(SMTP)로 발송됩니다. 이메일 수신 서버가 Notification Hub 이메일 발송 서버를 신뢰하기 위해서는 사용자 소유의 도메인이 서비스되는 DNS에 SPF, DKIM, DMARC TXT 레코드 설정이 필요합니다. 

### 주의 사항

* Notification Hub는 이메일 반송률이 과도하게 높을 경우 서비스의 운영 정책에 따라 발송이 제한될 수 있습니다.
    * 반송률이란, 고객이 발송을 요청한 이메일 주소 중 수신 SMTP 서버로부터 이메일을 전달할 수 없다(반송 혹은 발송 실패율)고 전달 받은 이메일 주소 비율입니다.
* 과도한 이메일 반송률이 발생하지 않도록 관리하세요.
* 반송률(반송 혹은 발송 실패)이 발생하는 원인은 다음과 같습니다.
    * 유효하지 않은 발신자 이메일 주소나 발신 도메인
    * 유효하지 않은 수신자 이메일 주소나 수신 도메인
    * SPF, DKIM, DMARC 등 이메일 보안 조치를 적용하지 않은 발신 도메인
    * 동일한 수신자가 과도하게 반복되거나 중복된 이메일을 발송하는 경우
    * 수신 거부 회피를 위한 조작된 이메일을 발송하는 경우
    * 피싱이나 스팸으로 의심 받을 수 있는 내용을 포함한 이메일을 발송하는 경우
    * 정보통신망법 가이드를 지키지 않은 광고성 이메일을 발송하는 경우
* 반송률로 인해 이메일 발송이 제한된 경우 반송이 발생하는 원인에 해당하는 사항이 있는지 확인한 뒤 개선 조치하세요.
    * 이후, [고객 센터 > 1:1 문의](https://www.nhncloud.com/kr/support/inquiry)를 통해 발송 제한 해제를 문의하세요.

### SPF

SPF(sender policy framework, 발신자 정책 프레임워크)는 이메일 발송 시 허용된 서버 목록을 정의하여 발신 도메인을 위조한 스팸 메일이나 피싱 공격을 방지하는 인증 메커니즘입니다. 발신 도메인의 DNS에 SPF 레코드를 추가하면, 이메일 수신 서버는 해당 목록에 포함된 서버에서 이메일이 발송되었는지 인증할 수 있습니다. 이를 통해 이메일 발송 서버의 신뢰도를 높이고 이메일이 스팸으로 분류되지 않도록 합니다.

* [Email 보안 강화 기능 소개(SPF) 바로가기](https://meetup.nhncloud.com/posts/244)

### DKIM, DMARC

DKIM(domainKeys identified mail, 도메인 키 식별 메일)은 이메일에 디지털 서명을 추가하여 발신 도메인이 위조되지 않았음을 증명하는 인증 방법입니다. 이메일 발송 서버는 서명을 포함한 이메일 헤더를 추가하고, 이메일 수신 서버는 발신 도메인의 공개 키를 통해 서명의 유효성을 확인합니다. 이를 통해 이메일이 전송 중 변조되지 않았는지 확인할 수 있으며, 발신자 및 이메일 발송 서버의 신뢰성을 높입니다.

DMARC(domain-based message authentication, reporting, and conformance, 도메인 기반 메시지 인증 보고 및 적합성)은 SPF와 DKIM을 기반으로 이메일 인증을 강화하고, 인증에 실패한 이메일이 어떻게 처리될지를 정책으로 정의하는 방법입니다. 도메인 소유자는 DMARC를 통해 이메일 수신 서버에서 인증 실패가 발생한 경우 이메일을 어떻게 처리할지 정책(거부, 격리, 허용)을 제공합니다. DMARC는 또한 보고서 기능을 통해 이메일 수신 서버로부터 인증 실패 사례에 대해 보고서 이메일을 받을 수 있으며, 이를 분석해 도메인 보호를 강화할 수 있도록 돕습니다.

* [이메일 보안 강화 기능 소개(도메인 보호, DKIM, DMARC) 바로가기](https://meetup.nhncloud.com/posts/248)

## Gmail 관련 안내 사항

### Gmail과 Yahoo의 이메일 수신 기준 강화

2024년 2월 1일부터 Gmail과 Yahoo의 이메일 발신자 가이드라인이 변경되어 도메인 인증 및 SPF, DKIM, DMARC 인증을 하지 않을 경우 일부 수신하는 메일 시스템에 대한 발송 요청이 거부될 수 있습니다. 이에 따라 Notification Hub에서 SPF, DKIM, DMARC 인증을 완료하지 않은 발신 도메인은 Gmail, Yahoo로 발송이 실패 처리됩니다.  

* [Gmail * Email Sender Guidelines](https://support.google.com/a/answer/81126)
* [Yahoo * Sender Requirements & Recommanations](https://senders.yahooinc.com/best-practices/)

#### SPF, DKIM, DMARC 미인증 시 발송 제한 대상 도메인
* gmail.com
* yahoo.com

Gmail은 도메인 평판을 스팸 메일 판정의 주요 기준으로 삼고 있습니다. 낮은 도메인 평판을 가진 발송자가 빠른 속도로 대량의 이메일을 발송하거나, 수신자가 원하지 않는 광고성 이메일을 발송하면 수신자의 '받은 메일함'에 저장하지만 경고를 표시하거나 '스팸 메일함'에 저장하며, 나아가 아예 수신 속도를 제한하거나 수신을 거부할 수 있습니다. 그러므로 이메일을 대량으로 발송하고자 하는 경우 다음 가이드의 도메인 평판 관리 방법을 참고하여 항상 도메인 평판을 높게 유지하도록 신경 써야 합니다.

### Gmail 열람됨 이벤트 수집 불가 안내

수신자의 메일이 Gmail인 경우 이메일의 열람 여부를 수집할 수 없습니다. 일반적으로 수신자의 이메일 열람을 확인하기 위해 이메일 본문에 이미지 태그를 삽입하는 방식을 사용하는데, Gmail에서는 이미지 프록시 서버가 이미지를 캐싱해 추적할 수 없도록 이메일 본문을 수정합니다. 이는 Gmail에서 의도적으로 막아 놓은 것으로 기술적으로 열람에 대한 이벤트를 수집하는 것은 현재 불가능합니다.

!!! tip "알아두기 - Gmail Image Proxy"
    Because the Gmail Image Proxy service does not forward users' cookies, you can't use the measurement protocol to track Gmail users. The Gmail Image Proxy service prevents this by having the measurement protocol requests passed through an intermediate server.


* [Google Analytics > Email Tracking * Measurement Protocol](https://developers.google.com/analytics/devguides/collection/protocol/v1/email)

### Gmail 낮은 평판(Low Reputation) 문제

Gmail 평판 평가 기준에 대해 간략하게 정리한 가이드입니다. Gmail에서 평판을 평가하는 방식을 살펴보고, 평판을 올리고 유지하기 위한 방법은 무엇인지 다룹니다. 더 자세한 내용은 문서 아래의 참고 문서를 확인하세요.

#### 평판(Reputation)?
메일 발송 시 ISP(inbox service provider, Gmail, 수신 SMPT 서버)는 발송 SMTP 서버의 평판을 평가해 수신 여부를 정하고, 스팸을 분류합니다. ISP의 평판 평가 방식에 맞지 않게 메일을 발송하면 발송 속도가 저하되거나 해당 ISP를 사용하는 수신인의 메일 수신이 어려워질 수 있습니다.

평판은 크게 IP 평판, 도메인 평판이 있습니다.
* IP 평판: IP는 발송 SMTP의 IP입니다. 발송 SMTP가 가지는 IP의 평판을 의미합니다.
* 도메인 평판: 도메인은 메일 발송 도메인입니다. NHN의 도메인은 'nhn.com'이 됩니다. 메일 발송의 주체가 되는 도메인의 평판을 의미합니다.

#### Gmail의 평판 평가 방식
* 도메인 평판을 더 중요하게 평가: 여러 도메인이 IP를 공유해서 발송하는 경우가 많기 때문에 IP보다 도메인을 더 중요하게 평가합니다. Complaints(불만)보다 Engagement(참여)를 더 중요하게 평가합니다. 여기서 Complaints는 수신인의 스팸 처리 등을 뜻합니다. Engagement는 수신인이 메일 내용 확인 및 내용에 있는 링크 클릭, 스팸 처리 해제 등을 뜻합니다.
* 그 밖의 평가 항목: 개인적인 메일인지 아닌지, 발송 IP의 평판은 어떤지, 메일 내 링크가 들어가 있는지, 매일 내용 등 여러 가지 요소들을 평가하여 평판을 결정합니다.

#### 평판을 올리는 방법
* 준비(warm-Up) 과정 필요: 처음부터 새로운 IP와 도메인으로 많은 양의 메일을 발송하는 것은 바람직하지 않으며, 오히려 평판이 낮아질 수 있습니다. 며칠에 걸쳐서 50, 100, 500, 1000, ...처럼 서서히 증가시켜야 합니다.
* 참여도(Engagement)가 높은 수신인에게 발송: Gmail에게 발송한 메일이 수신인들이 원하는 것이라는 것을 증명해야 합니다. 준비 과정에서 일반적인 사용자들보다 훨씬 서비스 참여도와 충성도가 높은, 메일이 오기만을 기다리고 있는 사용자들에게 발송하면 평판을 쉽게 높일 수 있습니다.
* 수신 거부 기능 제공: 서비스에서 수신 여부 설정을 할 수 있도록 기능을 제공해야 합니다. 원 클릭 수신 거부(One-Click Unsubscribe)나 메일 하단에 수신 거부 링크를 제공하는 것이 평판 상승에 도움이 됩니다.
* 수신자에게 적합성(Relevancy)이 높은 메일 발송: 평판을 유지하기 위해서는 메일 내용과 관련성이 있는 대상에게 발송해야 합니다. 단지 메일을 자주 보내는 것보다 더 중요합니다. 발송 대상의 크기는 중요하지 않습니다. 메일 내용과 대상을 세분화해서 발송해야 합니다. 구독 취소의 원인 66%는 관련성이 없는 메일, 55%는 메시지의 피로도 때문입니다.

#### 평판에 대한 외부 문서 참고
* [Mailgun * Domain Reputation Or IP Reputation: Which One Does Gmail Care About More?](https://www.mailgun.com)
