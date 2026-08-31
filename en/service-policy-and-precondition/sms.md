<!-- pre-align:aligned sig=a62b38bb217c -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>SMS</h1> 

**Notification > Notification Hub > Service Policy and Prerequisites > SMS**


<a id="sender-phone-number-pre-registration"></a>
## Enforce pre-registration of sender numbers { #sender-phone-number-pre-registration }

<b>In accordance with the Telecommunications Business Act, the registration of a sender number requires the authentication of the owner of the sender number.</b>

* The owner authentication method and required documents are determined according to the sender number type.
* After your identity verification, you can register your sender number.
* You can download the Acceptance to use form from the console.
* Documents confirming the relationship between the business and the third party can be consignment agreements, proof of headquarters and branch offices, etc.
* There are no **masked (hidden) parts of the communication service use certificate, and only documents issued within the last 3 months** are accepted.
* The certificate of employment is marked with **issuance date and only documents with seal ** are allowed. The 6 digits after the resident registration number in the certificate of employment  **masked (hidden)**. Example) 000000-0\*\*\*\*\**

<a id="prohibition-of-alterationfalsification-of-the-sender-number"></a>
## Prohibition on Sender Number Spoofing (Falsification) { #prohibition-of-alterationfalsification-of-the-sender-number }
* When using the SMS service, you must register a sender number that you (or your company) own before sending messages.
* If you use a sender number belonging to another person (or another company), the following actions may be taken in accordance with <a href="https://www.msit.go.kr/bbs/view.do?sCode=user&mId=108&mPid=103&bbsSeqNo=83&nttSeqNo=1259891" target="_blank">[(Ministry of Science, ICT and Future Planning Notice No. 2015-32) Notice on Prevention of User Damage Caused by Falsely Displayed Phone Numbers]</a> and the <a href="https://www.nhncloud.com/kr/terms/terms-service" target="_blank">[NHN Cloud Terms of Service]</a>. Please be advised.

!!! danger "Caution"
    ㆍIf a message is sent with a falsified sender number, the user's line or service may be suspended until the investigation into the issue is complete.
      (However, if the falsification was accidental and without malicious intent, the service may be resumed after receiving the user's explanation and conducting a review.)
    ㆍUse of the service may be restricted for users whose systems are configured to send messages using numbers other than registered sender numbers.
    ㆍDamages may be claimed for all losses resulting from sender number falsification.

<a id="information-about-080-call-blocking-service"></a>
## Information about 080 call blocking service { #information-about-080-call-blocking-service }
* 080 unsubscription number service provides the receiver with a blocking feature when sending an advertisement text message.
* When sending advertising information, be sure to include a free unscription method so that the receiver can refuse or withdraw the subscription for free.

[[Act on Promotion of Information and Communications Network Utilization and Information Protection](https://www.law.go.kr/%EB%B2%95%EB%A0%B9/%EC%A0%95%EB%B3%B4%ED%86%B5%EC%8B%A0%EB%A7%9D%EC%9D%B4%EC%9A%A9%EC%B4%89%EC%A7%84%EB%B0%8F%EC%A0%95%EB%B3%B4%EB%B3%B4%ED%98%B8%EB%93%B1%EC%97%90%EA%B4%80%ED%95%9C%EB%B2%95%EB%A5%A0)] Under Article 50, you must obtain the recipient's explicit prior consent when sending advertising information for commercial purposes, and you must comply with all mandatory labeling requirements for such messages.
Be aware that violations of applicable laws may result in criminal penalties or fines depending on the nature of the violation.

[[Korea Internet & Security Agency (KISA) Guide to the Act on Promotion of Information and Communications Network Utilization and Information Protection for Prevention of Illegal Spam](https://spam.kisa.or.kr/spam/na/ntt/selectNttInfo.do?mi=1020&nttSn=3001&bbsId=1002)]

<a id="consent-to-receive-advertising-information"></a>
### Consent to Receive Advertising Information { #consent-to-receive-advertising-information }
* When sending advertising information for commercial purposes, you must obtain the recipient's explicit prior consent.
* Advertising messages cannot be sent between 9 PM and 8 AM the following day. To send messages during this time period, you must obtain a separate consent from recipients for receiving nighttime advertising.

<a id="advertising-disclosure-requirements"></a>
### Advertising Disclosure Requirements { #advertising-disclosure-requirements }
* Mark '(광고)' (advertisement) at the beginning of the advertising information
    * Variations such as (광/고), (광 고), ("광고"), [광고] are prohibited
    * For LMS/MMS with a subject, mark '(광고)' at the beginning of both the subject and the body
* Include the sender's information: "company name or service name" and "contact information"
    * If the caller ID and contact number are the same, the contact number may be omitted
* Include a free opt-out 080 number at the bottom of the message

Example: Advertising disclosure requirements for messages
```
[Web발신]
(Ads) [Sender name]
[Sender's contact information]
[Or sender's address]

[Ad content]

Toll-free opt-out 080-****-****
```

<a id="notify-recipients-of-opt-out-requests"></a>
### Notify recipients of opt-out requests { #notify-recipients-of-opt-out-requests }
* Notifies recipients of the sender's name, the fact of opt-out or withdrawal of consent, the date on which the request was made, and the result of the processing.

<a id="advertisement-texting-sending-guidance"></a>
## Advertisement Texting Sending Guidance { #advertisement-texting-sending-guidance }
In accordance with Article 50 of the Act on Promotion of Information and Communication Network Utilization and Information Protection, explicit prior consent from the receiver must be obtained when sending commercial information for commercial purposes, and also must comply with the obligations regarding delivery notation <br/>

[[ Korea Internet & Security Agency (KISA) Information and Communication Network Act Guide for the Prevention of Illegal Spam](https://static.toastoven.net/prod_sms/kisa_spam_guide.pdf)] <br/>

* The sender numbers register valid numbers that can be contacted directly by the actual sender.
* Insert (advertisement) phrases at the beginning of the content
* Enter sender company name or service name
* Enter how to block 080 call blocking service 
* Do not send advertising information at night time: individual prior consent of the receiver is required when transmitting during night time (PM 09~AM08)
* Notify the result to the receiver who requested unscubscription service: inform all including the sender of the name, the facts and dates of the declaration of intent, and the results of the processing

<a id="delivery-speed-guide-according-to-mms-attachment-size"></a>
## Delivery speed guide according to MMS attachment size { #delivery-speed-guide-according-to-mms-attachment-size }
* When sending MMS, there may be a difference in delivery speed depending on the size of the attachment.
* The larger the size of the uploaded attachment, the slower the delivery speed and delivery results update due to the carrier's delivery speed constraints.
* If you want to send it quickly, we recommend that you reduce the size of the attachment.

<a id="guidance-on-sending-content-according-to-character-set"></a>
## Guidance on sending content according to character set { #guidance-on-sending-content-according-to-character-set }
* Texts included in EUC-KR are normally exposed to the same content as sent upon receipt.
* If characters that are not included in EUC-KR are included in the title/text, the content may be exposed as broken characters such as '?' are included upon receipt.
    * Depending on the type of receiving terminal and and device, the contents of the delivery may be exposed differently.

<a id="message-received-result-timeout-policy"></a>
## Message received result timeout policy { #message-received-result-timeout-policy }
* Depending on the device and communication status, the update of the message reception results may be delayed.
* If there is a delay in the result of receiving the message, we will try to send it according to the NHN Cloud re-delivery policy.
* The re-delivery policy is as follows.

| Send Type | Time of Time-out | After Time-out  |
|---|---|---|
| SMS | 25 hours | No retries. Failed to receive result update (result code: 2000) |
| LMS | 80 hours | No retries. Failed to receive result update (result code: 2000) |
| MMS | 80 hours | No retries. Failed to receive result update (result code: 2000) |

<a id="about-phone-scam-blocking-services"></a>
## Guide of Stolen Number Text Message Blocking Service { #about-phone-scam-blocking-services }
‘Stolen Number Text Message Blocking Service’ prevents others from arbitrarily abusing one’s mobile number for text crimes or sending spam. If the sender number is subscribed to this service, the delivery may fail. To use the problematic number as the sender number, cancellation is required through the mobile carrier.

<a id="guide-of-stolen-number-text-message-blocking-service-how-to-use"></a>
#### How to use
* It is provided free of charge by mobile carriers (including SKT, KT, LG U+ and MVNO operators), so you can register if you agree to join.
* After sending a text message, if the text sending result is confirmed as 'Failed' on the site even though it is a normal number, check whether you have subscribed to the 'Stolen Number Text Message Blocking Service'.
* Send after cancelling 'Stolen Number Text Message Blocking Service'.
* It takes about 7 days for cancellation to take effect after application.

<a id="guide-of-stolen-number-text-message-blocking-service-guide-about-cancellation"></a>
#### Guide about cancellation
* Mobile carrier website
    * [SKT Stolen Number Text Message Blocking Service  shortcut ](http://www.tworld.co.kr/normal.do?serviceId=S_PROD2001&viewId=V_PROD2001&prod_id=NA00004406)
    * [KT  Stolen Number Text Message Blocking Service  shortcut ](https://product.kt.com/wDic/productDetail.do?ItemCode=1047)
    * [ LG U+ Stolen Number Text Message Blocking Service  shortcut ](https://www.lguplus.com/plan/addon/addon-call-msg/LRZ0002297)
* Mobile carrier customer center
    * Mobile phone 114 * Call button
    * SKT Customer Center1599-0011, KT Olleh Customer Center100, LG U+ Customer Center1544-0010

<a id="about-carrier-spam-text-blocking-services"></a>
## Mobile Carrier Spam Blocking Service Guide { #about-carrier-spam-text-blocking-services }
It is a service that automatically blocks cumbersome advertising spam texts from mobile carriers. According to the combination standards of each mobile carrier, text messages that are judged to be spam are sent to the spam storage box rather than to the text inbox of the mobile phone. If it has been sent normally but fails to receive, the receiving number may be subscribed to the carrier spam blocking service.

<a id="mobile-carrier-spam-blocking-service-guide-how-to-use"></a>
#### How to use
* If the delivery result is confirmed to be successful but the text is not received, check the mobile carrier’s spam blocking service.
* Korea Internet & Security Agency's Illegal Spams Response Center has established the comprehensive countermeasure against spams, and each mobile carrier is currently operating the 'Spam blocking service'.
* If the message has been stored as spam instead of being stored in the text message inbox, please proceed after canceling the Spam blocking service.
* Due to the privacy policy, no one other than you can check it, so you must check it yourself.

<a id="mobile-carrier-spam-blocking-service-guide-guide-about-cancellation"></a>
#### Guide about cancellation
* Mobile carrier website
    * [SKT Spam Filtering Cancel service now](http://www.tworld.co.kr/normal.do?serviceId=S_PROD2001&viewId=V_PROD2001&prod_id=NA00002121)
    * [KT Spam block Cancel service now](https://product.kt.com/wDic/productDetail.do?ItemCode=479)
    * [LG U+ Spam block Cancel service now](https://www.lguplus.com/plan/addon/addon-call-msg/LRZ0000277)
* Mobile carrier customer center
    * Mobile phone 114 * Call button
    * SKT Customer Center1599-0011, KT Olleh Customer Center100, LG U+ Customer Center1544-0010
