<!-- pre-align:aligned sig=674d72b2ce04 -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a { 
    display: inline !important;
}
</style>
<h1>Get Started With Notification Hub</h1>

**Notification > Notification Hub > Console User Guide > Get Started with Notification Hub **

<span id="identity-verification"></span>

## Verify your identity

After Notification Hub is activated, you must complete identity verification before you can use it. For more information about identity verification, see **Service Policy and Prerequisites > Identity Verification**.

* [Go to Identity Verification Guide](../service-policy-and-precondition/identity-verification)


<span id="manage-sender-info"></span>

<a id="sender-information-management"></a>

## Manage Sender Information

<span id="manage-sender-phone-number"></span>

<a id="sender-number-management"></a>

### Manage Sender Numbers

To send SMS, LMS, and MMS messages, you must register a sender number. Submit a review request for sender number registration. When the review is approved, the sender number is registered.

1. Click **+ Register Sender Number** and agree to the **Personal Information Collection and Use Agreement**.
2. Select the sender number type to register and enter the sender number.
3. Attach the required documents for the sender number type.

For more information about the sender number pre-registration system, see **Guide to Usage Policies and Preparations > SMS > Sender Number Pre-Registration System**.

* [Go to Sender Number Pre-Registration System](../service-policy-and-precondition/sms#sender-phone-number-pre-registration)

<span id="manage-sender-brand"></span>

<a id="brand-management"></a>

### Manage Brands

To send RCS messages, you must complete brand integration. If the pre-registration requirements have been completed in the RCS Biz Center (brand approval), proceed with integration with the NHN Cloud console. For brand creation in the RCS Biz Center, see **Guide to Usage Policies and Preparations** > **RCS**.

* [Go to Guide to Usage Policies and Preparations > RCS](../service-policy-and-precondition/rcs)
* [Go to RCS Biz Center](https://www.rcsbizcenter.com/main)

When brand creation, agency settings, chatroom (sender number) registration, and template registration have been completed (approved) in the RCS Biz Center, integrate the brand in the console.

* Click **+ Integrate Brand** to complete synchronization.

<span id="manage-sender-domain"></span>

<a id="manage-domains"></a>

### Manage Domains

To send emails, you need a domain that you own, and SPF, DKIM, and DMARC authentication.

For more information about sender domains and SPF, DKIM, and DMARC, see **Guide to Usage Policies and Preparations > Email**.

* [Go to Guide to Usage Policies and Preparations > Email](../service-policy-and-precondition/email)

<a id="email-domain-registration-and-ownership-authentication"></a>

#### Register Email Domains and Verify Ownership

You must register a domain and verify domain ownership. Register the value provided by Notification Hub in the email domain DNS TXT record. Verify ownership by checking that the provided value matches the TXT record of the registered domain.

1. Click **+ Register Domain**.
2. Enter the root domain to register and click **Verify**.
3. If verification succeeds, click **Register** to complete the registration.
4. In the domain list, click **Verify** next to the domain ownership verification status.

If domain ownership verification succeeds, the domain verification status changes to "Completed."

<a id="spf-authentication"></a>

#### SPF Authentication

Sender policy framework (SPF) is a mechanism for verifying the reliability of email senders and sending servers. The email receiving server checks whether an email sent from a specific domain actually came from an authorized email sending server. The email receiving server checks the SPF record registered in the sender's email domain DNS and treats emails sent from unregistered IP addresses as spam.

**SPF**
```
v=spf1 include:_spfblocka.toast.com ~all
```

1. Register the SPF record from the **SPF** section above in the domain TXT record.
2. Select a domain from the list.
3. Click **Check Status** in the **SPF Record Authentication Status** section to complete SPF authentication.


!!! danger "Caution"
    * Only one SPF record must be registered in the domain TXT record. If two or more SPF records are registered in the domain TXT record, SPF verification may fail and the email receiving server may reject incoming emails.
    * The use of mechanisms (include) and modifiers (redirect) that trigger DNS lookups when checking SPF records is limited to a maximum of 10. Exceeding this limit may cause the email receiving server to reject incoming emails.
    
For more information about SPF, see the following documents.

* [Go to Introduction to Email Security Enhancement Features (SPF)](https://meetup.nhncloud.com/posts/244)
* [Go to RFC 4408 - 4.5 Selecting Records](https://datatracker.ietf.org/doc/html/rfc4408#section-4.5)
* [Go to RFC 4408 - 10.1 Processing Limits](https://datatracker.ietf.org/doc/html/rfc4408#section-10.1)

<a id="dkim-authentication"></a>

#### DKIM Authentication

DomainKeys identified mail (DKIM) is an email verification method in which the email sending server digitally signs emails and the email receiving server verifies the authenticity of the sender to ensure that messages have not been forged or altered during transmission. DKIM prevents spammers and other malicious attackers from forging or altering emails.


1. After completing domain ownership verification, select a domain from the list and click **DKIM Settings**.
2. Set the TXT record value for the DNS hostname provided for DKIM authentication and click **Verify** below.
    * If the registered domain is `example.com`, set the value in the `toast._domainkey.example.com` TXT record.
3. After verification is complete, enable the settings and click **Save** to complete DKIM authentication.

For more information about DKIM, see the following document.

* [Go to Introduction to Email Security Enhancement Features - Domain Protection, DKIM, and DMARC](https://meetup.nhncloud.com/posts/248)


<a id="dmarc-authentication"></a>

#### DMARC Authentication

Domain-based message authentication, reporting and conformance (DMARC) is the final step in enhancing email security. It is a domain-based message authentication, reporting, and conformance policy to prevent phishing and fraud using email spoofing. The email receiving server looks up the DMARC record in the DNS of the sender address (From) domain. The receiving server authenticates received emails according to the policy defined in the DMARC record.

**DMARC**
```
"v=DMARC1;p=none;sp=quarantine;pct=100;rua=mailto:${email_address_to_receive_reports}"
```

1. Add the email address to receive DMARC reports to the value in the **DMARC** section above to complete the DMARC TXT record.
2. Register it in the subdomain TXT record with `_dmarc.` prepended.
    * Example: If the domain is `example.com`, register it in the TXT record of `_dmarc.example.com`.
3. Click **Check Status** in the **DMARC Authentication Status** section to complete DMARC authentication.

For more information about DMARC, see the following document.

* [Go to Introduction to Email Security Enhancement Features - Domain Protection, DKIM, and DMARC](https://meetup.nhncloud.com/posts/248)

##### Domain Protection

Domains with domain protection enabled cannot be used by other projects. To use a protected domain in another project, the domain must be registered and ownership must be verified in the same way.

!!! danger "Caution"
    If domain protection is disabled, other projects can use the domain without restriction. For domains that have completed all verifications, emails sent from other projects are also received normally by the email receiving server. If such emails are spam or phishing, recipients may be harmed and the domain's reputation may decline, causing the email receiving server to reject incoming emails.

<span id="manage-sender-push-authorization"></span>

<a id="push-authentication-management"></a>

### Manage Push Authentication

For information on how to obtain Push authentication credentials, see **Guide to Usage Policies and Preparations > Push**.

* [Go to Guide to Usage Policies and Preparations > Push](../service-policy-and-precondition/push)

<a id="fcm-authentication-settings"></a>

#### FCM Authentication Settings
1. Enable **Register Service Account Key**.
2. Copy and paste the contents of the FCM Service Account Credential file that you obtained into the service account key (JSON) field.
3. Click **Verify** > **Save** to complete the settings.

<a id="pns-authentication-settings"></a>

#### APNS Authentication Settings
1. Enable **Register APNS JWT Certificate**.
2. Enter the **Team ID** and **Key ID**.
3. Enter the **Topic**. The topic is the bundle ID of the app.
4. Copy and paste the contents of the **Private Key** file.
5. Click **Verify** > **Save** to complete the settings.

<a id="adm-authentication-settings"></a>

#### ADM Authentication Settings
1. Enable **Register Credentials**.
2. Enter the **Client ID** and **Client Key**.
3. Click **Verify** > **Save** to complete the settings.

<span id="manage-sender-profile"></span>

<a id="manage-outgoing-profiles"></a>

### Manage Sender Profiles

To send Alim Talk and brand messages, you must create and register a sender profile.

You can create a sender profile in Kakao Business.

* [Go to Sender Profile Creation Guide](../service-policy-and-precondition/alimtalk-and-friendtalk)


When a sender profile has been created in Kakao Business, register it by following the steps below.

1. Click **+ Register Sender Profile**, set the sender profile ID, administrator mobile phone number, and category, and then click **Request Token**.
2. Enter the token sent to the administrator's mobile phone and click **Confirm** > **Register** to complete the sender profile registration.


<span id="manage-080-unsubscription-number"></span>

<a id="manage-opt-out-numbers"></a>

### Manage 080 Opt-Out Numbers

The 080 opt-out number service provides recipients with an opt-out option when sending advertising messages. When sending promotional messages, a free opt-out method must be included so that recipients can opt out or withdraw their consent to receive messages free of charge.

<a id="apply-subscription"></a>

#### Apply for Subscription

* Click **+ Apply for 080 Opt-Out Number** and enter the company name. The company name that you enter is the business name announced when someone calls the 080 opt-out number.
* When the subscription is fully applied, the status is changed to Registration Scheduled. It takes 3 to 4 business days to open the 080 opt-out number service, and the service is enabled after opening.
* When the service is completely open, you can find the start date and status of service. While the 080 opt-out number service is scheduled for registration, the SMS Service cannot be closed. Service can be closed only after it is canceled. To cancel the service, click **Cancel Service**.

<a id="set-080-unsubscription-number-when-advertising-texts"></a>

#### Set Up 080 Opt-Out Number for Advertising Messages

* You can send advertising messages only when the 080 opt-out number service is active.
* On the **Send > SMS** tab, when you select Advertising as the message purpose, the 080 opt-out number selection window appears.
* Click **Apply Selection** to add the required advertising phrases.
* When sending advertising messages, the message body must include the required advertising phrases. The rules are as follows:
    * Starting phrase: (광고)
    * Ending phrase: 무료수신 거부 {080 opt-out number} or 무료거부 {080 opt-out number} (These phrases may contain spaces.)

##### Example
```
(광고)

[무료 수신 거부]080XXXXXXX
```
```
(광고)

무료거부 080XXXXXXX
```
