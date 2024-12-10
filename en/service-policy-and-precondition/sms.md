<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>SMS</h1> 

**Notification > Notification Hub > Usage Policy and Preset Guide > SMS**

## Enforce pre-registration of sender numbers

<b>In accordance with the Telecommunications Business Act, the registration of a sender number requires the authentication of the owner of the sender number.</b>

* The owner authentication method and required documents are determined according to the sender number type.
* After your identity verification, you can register your sender number.
* You can download the Acceptance to use form from the console.
* Documents confirming the relationship between the business and the third party can be consignment agreements, proof of headquarters and branch offices, etc.
* There are no **masked (hidden) parts of the communication service use certificate, and only documents issued within the last 3 months** are accepted.
* The certificate of employment is marked with **issuance date and only documents with seal ** are allowed. The 6 digits after the resident registration number in the certificate of employment  **masked (hidden)**. Example) 000000-0\*\*\*\*\**

<span id='fabrication-number'></span>

## Prohibition of Alteration/Falsification of the Sender Number
* When using SMS services, you must register your (or your company) number before using it.
* Please note that if you use another person (or a third party) sender number, be careful as necessary measures can be taken according to <a href="https://www.msit.go.kr/bbs/view.do?sCode=user&mId=108&mPid=103&bbsSeqNo=83&nttSeqNo=1259891" target="_blank"> [(Notice of the Ministry of Science, ICT and Future Planning No. 2015-32)] Notice concerning the prevention, etc. of damage to users due to falsely displayed telephone numbers </a> and <a href="https://www.nhncloud.com/kr/terms/terms-service" target="_blank"> [NHN Cloud Terms and Conditions] </a>. 

!!! Danger "Precaution" 
·If you send a false sending number, the user's line or service will be stopped until investigation into the matter is complete.
(However, if it is accidentally altered without malicious purposes, the service can be resumed after reviewing the user’s letter of explanation.)
·Restrictions on the use of services by users whose systems are established to make calls to numbers other than the registered calling number 
·Claim for damages for all losses caused by other calling number alterations

<span id="rejection-of-receiving-080"></span>

## Information about 080 call blocking service 
* 080 unsubscription number service provides the receiver with a blocking feature when sending an advertisement text message.
* When sending advertising information, be sure to include a free unscription method so that the receiver can refuse or withdraw the subscription for free.

### How to use
* The user will be charged for 080 unsubscription number service after the 080 service number is activated, not when the message is sent (monthly subscription).
* The 080 unsubscription service number requires 3 ~ 4 days to get a new number. Hence, temporary and repeated cancellations and applications are not recommended.
* Please be careful when registering because you cannot cancel the opening in the registration scheduled status.
* If you want to use the registered 080 unsubscription number in other projects, you can use the **080 unsubscription number sharing** feature.
* If the 080 unsubscription number has been canceled or if the number is an externally requested 080 number, sending will fail.

### Advertisement Texting Sending Guidance
In accordance with Article 50 of the Act on Promotion of Information and Communication Network Utilization and Information Protection, explicit prior consent from the receiver must be obtained when sending commercial information for commercial purposes, and also must comply with the obligations regarding delivery notation <br/>

[[ Korea Internet & Security Agency (KISA) Information and Communication Network Act Guide for the Prevention of Illegal Spam](https://static.toastoven.net/prod_sms/kisa_spam_guide.pdf)] <br/>

* The sender numbers register valid numbers that can be contacted directly by the actual sender.
* Insert (advertisement) phrases at the beginning of the content
* Enter sender company name or service name
* Enter how to block 080 call blocking service 
* Do not send advertising information at night time: individual prior consent of the receiver is required when transmitting during night time (PM 09~AM08)
* Notify the result to the receiver who requested unscubscription service: inform all including the sender of the name, the facts and dates of the declaration of intent, and the results of the processing

### Delivery speed guide according to MMS attachment size
* When sending MMS, there may be a difference in delivery speed depending on the size of the attachment.
* The larger the size of the uploaded attachment, the slower the delivery speed and delivery results update due to the carrier's delivery speed constraints.
* If you want to send it quickly, we recommend that you reduce the size of the attachment.

### Guidance on sending content according to character set
* Texts included in EUC-KR are normally exposed to the same content as sent upon receipt.
* If characters that are not included in EUC-KR are included in the title/text, the content may be exposed as broken characters such as '?' are included upon receipt.
    * Depending on the type of receiving terminal and and device, the contents of the delivery may be exposed differently.

### Message received result timeout policy
* Depending on the device and communication status, the update of the message reception results may be delayed.
* If there is a delay in the result of receiving the message, we will try to send it according to the NHN Cloud re-delivery policy.
* The re-delivery policy is as follows.

| Send Type | Time of Time-out | After Time-out  |
|---|---|---|
| SMS | 25 hours | No retries. Failed to receive result update (result code: 2000) |
| LMS | 80 hours | No retries. Failed to receive result update (result code: 2000) |
| MMS | 80 hours | No retries. Failed to receive result update (result code: 2000) |

<span id="about-phone-scam-blocking-services"></span>

### Guide of Stolen Number Text Message Blocking Service  
‘Stolen Number Text Message Blocking Service’ prevents others from arbitrarily abusing one’s mobile number for text crimes or sending spam. If the sender number is subscribed to this service, the delivery may fail. To use the problematic number as the sender number, cancellation is required through the mobile carrier.

#### How to use
* It is provided free of charge by mobile carriers (including SKT, KT, LG U+ and MVNO operators), so you can register if you agree to join.
* After sending a text message, if the text sending result is confirmed as 'Failed' on the site even though it is a normal number, check whether you have subscribed to the 'Stolen Number Text Message Blocking Service'.
* Send after cancelling 'Stolen Number Text Message Blocking Service'.
* It takes about 7 days for cancellation to take effect after application.

#### Guide about cancellation
* Mobile carrier website
    * [SKT Stolen Number Text Message Blocking Service  shortcut ](http://www.tworld.co.kr/normal.do?serviceId=S_PROD2001&viewId=V_PROD2001&prod_id=NA00004406)
    * [KT  Stolen Number Text Message Blocking Service  shortcut ](https://product.kt.com/wDic/productDetail.do?ItemCode=1047)
    * [ LG U+ Stolen Number Text Message Blocking Service  shortcut ](https://www.lguplus.com/plan/addon/addon-call-msg/LRZ0002297)
* Mobile carrier customer center
    * Mobile phone 114 * Call button
    * SKT Customer Center1599-0011, KT Olleh Customer Center100, LG U+ Customer Center1544-0010

<span id="about-carrier-spam-text-blocking-services"></span>

### Mobile Carrier Spam Blocking Service Guide
It is a service that automatically blocks cumbersome advertising spam texts from mobile carriers. According to the combination standards of each mobile carrier, text messages that are judged to be spam are sent to the spam storage box rather than to the text inbox of the mobile phone. If it has been sent normally but fails to receive, the receiving number may be subscribed to the carrier spam blocking service.

#### How to use
* If the delivery result is confirmed to be successful but the text is not received, check the mobile carrier’s spam blocking service.
* Korea Internet & Security Agency's Illegal Spams Response Center has established the comprehensive countermeasure against spams, and each mobile carrier is currently operating the 'Spam blocking service'.
* If the message has been stored as spam instead of being stored in the text message inbox, please proceed after canceling the Spam blocking service.
* Due to the privacy policy, no one other than you can check it, so you must check it yourself.

#### Guide about cancellation
* Mobile carrier website
    * [SKT Spam Filtering Cancel service now](http://www.tworld.co.kr/normal.do?serviceId=S_PROD2001&viewId=V_PROD2001&prod_id=NA00002121)
    * [KT Spam block Cancel service now](https://product.kt.com/wDic/productDetail.do?ItemCode=479)
    * [LG U+ Spam block Cancel service now](https://www.lguplus.com/plan/addon/addon-call-msg/LRZ0000277)
* Mobile carrier customer center
    * Mobile phone 114 * Call button
    * SKT Customer Center1599-0011, KT Olleh Customer Center100, LG U+ Customer Center1544-0010
