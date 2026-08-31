<!-- pre-align:aligned sig=e8b03b463453 -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Sender Information</h1>

**Notifications > Notification Hub > Console User Guide > Sender Information**

Register and manage sender information for each message channel. To send messages, the sender information for each message channel must be registered in advance.

<a id="manage-sender-numbers"></a>
## Manage Sender Numbers { #manage-sender-numbers }

To send SMS, LMS, or MMS messages, you must register a sender number. In accordance with the notice related to the Telecommunications Business Act, identity verification of the account holder is required when registering a sender number. The verification method and required documents are determined by the member type and sender number type.

<a id="register-a-sender-number"></a>
### Register a Sender Number { #register-a-sender-number }

1. Click **+ Register Sender Number** and agree to **the consent form for the collection and use of personal information**.
2. Select the sender number type to register and enter the sender number.
3. Attach the documents required for the sender number type.
4. Once the review is approved after submitting the registration request, the sender number is registered.

For information on the sender number pre-registration system, refer to **Service Policy and Prerequisites > SMS > Implementation of Sender Number Pre-Registration System**.

* [Go to Sender Number Pre-Registration System](../service-policy-and-precondition/sms#sender-phone-number-pre-registration)

<a id="account-holder-verification-guide"></a>
### Account Holder Verification Guide { #account-holder-verification-guide }

| Member Type | Sender Number Type | Verification Method | Required Document |
|---|---|---|---|
| Business Member | Representative number, business own number | Document verification | Telecommunications service usage certificate |
| Business Member | Employee number | Document verification | Telecommunications service usage certificate, certificate of employment |
| Business Member | Third-party number | Document verification | Telecommunications service usage certificate, letter of consent, (third-party) business registration certificate, document confirming relationship between business and third party (contract, etc.) |
| Business Member | Other person's number | Document verification | Telecommunications service usage certificate, letter of consent |

* The basic form for the letter of consent can be downloaded from the console.
* Documents confirming the relationship between the business and the third party can be consignment agreements, proof of headquarters and branch offices, etc.
* There are no masked (hidden) parts of the communication service use certificate, and only documents issued within the last 3 months are accepted.
* Proof of employment **must be dated and stamped**with a seal.
* **Be sure to mask (hide) the last 6 digits of your social security number** on your proof of employment. e.g., 000000-0\*\*\*\*\**

<a id="about-sender-number-input-format"></a>
### About Sender Number Input Format { #about-sender-number-input-format }

* Landline number: 02-YYY-YYYY (register including area code)
* Mobile number: 010-ABYY-YYYY
* Common service identification number: 0N0 series (area code must not be used before the number)
* Sender numbers between 8 and 11 digits can be entered
* Messages cannot be sent to non-existent number ranges (e.g., 070-0YYY, 070-1YYY, 010-0YYY, 010-1YYY)

<a id="delete-an-sender-number"></a>
### Delete an Sender Number { #delete-an-sender-number }

You can delete a registered sender number.

1. Select the checkboxes of the sender numbers you want to delete.
2. Click **Delete Sender Number**.

<a id="brand-management"></a>
## Brand Management { #brand-management }

To send RCS messages, you need to register your brand in RCS Biz Center and integrate with NHN Cloud Console.

<a id="prerequisites"></a>
### Prerequisites { #prerequisites }

The following must be completed (approved) in RCS Biz Center before integrating a brand:

1. Sign up for RCS Biz Center, create and get a brand approved
2. Designate "NHN Cloud" as an agency in the Brand Operations Management menu
3. Register and get a chatroom (sender number) approved

For prerequisites in RCS Biz Center, refer to **Service Policy and Prerequisites > RCS**.

* Go to [Service Policy and Prerequisites > RCS](../service-policy-and-precondition/rcs)
* [Go to RCS Biz Center](https://www.rcsbizcenter.com/main)

<a id="integrate-a-brand"></a>
### Integrate a Brand { #integrate-a-brand }

Brand is linked based on the business registration number on the attached business registration card when authenticating yourself.

* Click **+ Integrate Brand** to synchronize brands registered in RCS Biz Center
* Once brand integration is complete, the brand list is displayed.
* If you've changed your brand information in RCS Biz Center, click **Integrate Brand** to proceed with the update.

<a id="manage-domains"></a>
## Manage Domains { #manage-domains }

To send emails, you must register a domain you own and verify domain ownership. After successful domain verification, you can configure SPF record verification, DMARC verification, and DKIM settings.

For sender domains and SPF, DKIM, and DMARC, refer to **Service Policy and Prerequisites > Email**.

* [Go to Service Policy and Prerequisites > Email](../service-policy-and-precondition/email)

<a id="register-an-email-domain-and-verify-ownership"></a>
### Register an Email Domain and Verify Ownership { #register-an-email-domain-and-verify-ownership }

You must register a domain and verify domain ownership. Register the value provided by Notification Hub in the email domain DNS TXT record. Verify ownership by checking that the provided value matches the TXT record of the registered domain.

1. Click **+ Register Domain**.
2. Enter the root domain to register and click **Verify**.
3. If verification is successful, click **Register** to complete the registration.
4. Click **Verify** in the domain ownership verification status in the domain list.

If domain ownership verification is successful, the domain verification status changes to **Completed**.

<a id="spf-authentication"></a>
### SPF Authentication { #spf-authentication }

Sender policy framework (SPF) is a mechanism for verifying the reliability of email senders and sending servers. The email receiving server checks whether an email sent from a specific domain actually came from an authorized email sending server.

SPF
```
v=spf1 include:_spfblocka.toast.com ~all
```

1. Register the SPF record from the SPF field above in the domain TXT record.
2. Select a domain from the list.
3. Click **Check Status** in the **SPF Record Authentication Status** field to complete SPF verification


!!! danger "Caution"
\* Only one SPF record must be registered in the domain TXT record. If two or more SPF records are registered in the domain TXT record, SPF verification may fail and the email receiving server may reject incoming emails.
\* The use of mechanisms (include) and modifiers (redirect) that trigger DNS lookups when checking SPF records is limited to a maximum of 10. Exceeding this limit may cause the email receiving server to reject incoming emails.

<a id="configure-dkim"></a>
### Configure DKIM { #configure-dkim }

DomainKeys identified mail (DKIM) is an email verification method in which the email sending server digitally signs emails and the email receiving server verifies the authenticity of the sender to ensure that messages have not been forged or altered during transmission.

1. After completing domain ownership verification, check the domain in the list and click **Configure DKIM**.
2. Set the TXT record value for the DNS hostname provided for DKIM verification and click **Verify** below.
    * If the registered domain is `example.com`, set the value in the `toast._domainkey.example.com` TXT record.
3. After verification is complete, enable the setting and click **Save** to complete DKIM configuration.

<a id="dmarc-authentication"></a>
### DMARC Authentication { #dmarc-authentication }

Domain-based message authentication, reporting and conformance (DMARC) is the final step in enhancing email security. It is a domain-based message authentication, reporting, and conformance policy to prevent phishing and fraud using email spoofing.

DMARC
```
v=DMARC1;p=none;sp=quarantine;pct=100;rua=mailto:${email_address_to_receive_reports}
```

1. Add the email address to receive DMARC reports to the value in the DMARC field above to complete the DMARC TXT record.
2. Register in the subdomain TXT record with `_dmarc.` added.
    * e.g., If the domain is `example.com`, register in the TXT record of `_dmarc.example.com`.
3. Click **Check Status** in the **DMARC Authentication Status** field to complete DMARC authentication.

<a id="domain-protection"></a>
### Domain Protection { #domain-protection }

Domains with domain protection enabled cannot be used in other projects. To use a protected domain in another project, domain registration and ownership verification must be completed in the same way.

!!! danger "Caution"
If domain protection is disabled, other projects can use the domain without restriction. For domains that have completed all verifications, emails sent from other projects are also received normally by the email receiving server. If such emails are spam or phishing, recipients may be harmed and the domain's reputation may decline, causing the email receiving server to reject incoming emails.

<a id="delete-a-domain"></a>
### Delete a Domain { #delete-a-domain }

You can delete a registered domain.

1. Select the checkbox of the domain to delete.
2. Click **Delete Domain**.

<a id="manage-push-authentication"></a>
## Manage Push Authentication { #manage-push-authentication }

To send push messages, you must register the credentials issued by the push service.

For information on how to obtain push authentication information, refer to **Service Policy and Prerequisites > Push**.

* [Go to Service Policy and Prerequisites > Push](../service-policy-and-precondition/push)

<a id="configure-fcm-authentication"></a>
### Configure FCM Authentication { #configure-fcm-authentication }

Firebase cloud messaging (FCM) authentication must be configured to send push messages to Android devices.

1. Click **Change Setting** in **FCM Service Account Key Registration**.
2. Copy and paste the contents of the FCM Service Account Credential file issued to the service account key (JSON).
3. Click **Verify > Save** to complete the configuration.

<a id="configure-apns-authentication"></a>
### Configure APNS Authentication { #configure-apns-authentication }

Apple Push Notification Service (APNS) authentication must be configured to send push messages to iPhones.

1. Click **Change Setting** in **APNS JWT Certificate Registration**.
2. Enter the **Team ID** and **Key ID**.
3. Enter the **topic**. The topic is the app's Bundle ID.
4. Copy and paste the contents of the **private key** file.
5. Click **Verify > Save** to complete the configuration.

<a id="adm-authentication-settings"></a>
### ADM Authentication Settings { #adm-authentication-settings }

Amazon device messaging (ADM) authentication must be configured to send push messages to Amazon Kindle, Fire, and other devices.

1. Click **Change Setting** in **ADM Authentication Registration**.
2. Enter the **Client ID** and **Client Key**.
3. Click **Verify > Save** to complete the configuration.

<a id="manage-sender-profiles"></a>
## Manage Sender Profiles { #manage-sender-profiles }

To send AlimTalk or brand messages, you must register a KakaoTalk sender profile.

<a id="manage-sender-profiles-prerequisites"></a>
### Prerequisites { #manage-sender-profiles-prerequisites }

To register a sender profile, a KakaoTalk channel must be created. Create a KakaoTalk channel on the KakaoTalk website.

* [Go to Create KakaoTalk Channel](https://center-pf.kakao.com/)

To register a sender profile, business verification must be completed after registering the KakaoTalk channel.

For information on how to create a sender profile, refer to **Service Policy and Prerequisites > AlimTalk/Brand Messages**.

* [Go to Service Policy and Prerequisites > AlimTalk/Brand Messages](../service-policy-and-precondition/alimtalk-and-friendtalk)

<a id="register-sender-profile"></a>
### Register a Sender Profile { #register-sender-profile }

1. Click **+ Register Sender Profile**.
2. Set the sender profile ID, administrator mobile number, and category, then click **Request Token**.
3. Enter the 6-digit token number sent to the administrator's mobile phone.
4. Click **Confirm > Register** to complete sender profile registration.

!!! danger "Caution"
    **The default maximum daily delivery count for AlimTalk is 1,000**. To change the maximum daily delivery count, contact [Customer Center](https://www.nhncloud.com/kr/support/inquiry).

!!! danger "Caution"
    Brand messages can only send **advertising (AD) messages**. When sending to customers (Targeting M, N, O), **registering an 080 opt-out number in the sender profile is required**.

<a id="manage-sender-profile-groups"></a>
### Manage Sender Profile Groups { #manage-sender-profile-groups }

You can manage sender profiles in groups.

* Click **Manage Sender Profile Groups** to create a group and add sender profiles to the group.

<a id="view-kakao-statistics"></a>
### View Kakao Statistics { #view-kakao-statistics }

Click **Go to Kakao Statistics** in the sender profile details to view Kakao statistics in a new window. Statistics criteria include delivery statistics and template statistics, and the query conditions vary depending on the message channel. You can view the results in charts and tables.

* Real-time statistics are not provided. Data collected the previous day is provided daily at around 7 AM.
* AlimTalk statistics are first provided on D+1 and finalized on D+2.
* Valid opens are not counted more than once for the same message.
* Clicks are counted multiple times for the same message.
* If the number of successful deliveries is 10 or fewer, valid opens and clicks are not provided.

<a id="view-kakao-statistics-delivery-statistics"></a>
#### Delivery Statistics

Retrieves the daily delivery count, valid opens, and clicks by sender profile. You can query by setting conditions such as period, delivery identifier, and message type.

<a id="view-kakao-statistics-template-statistics"></a>
#### Template Statistics

Retrieves the daily delivery count, valid opens, and clicks by template and group tag. You can query by setting conditions such as period and message type.

* Brand message free format is provided only when a group tag is used.

<a id="manage-group-tags"></a>
### Manage Group Tags { #manage-group-tags }

Group tags are identification tags used when querying template statistics for brand messages. Click the **Group Tag Management** tab in the new **Go to Kakao Statistics** window to manage group tags.

!!! danger "Caution"
Group tags can only be used for brand messages. AlimTalk is not applicable.

* Click **+ Register Group Tag** to enter a group tag name and register it.
* Select the checkbox of the group tag to modify or delete, and click **Modify Group Tag** or **Delete Group Tag**.

<a id="apply-to-use-customer-targeted-sending"></a>
### Apply to Use Customer-Targeted Sending { #apply-to-use-customer-targeted-sending }

To use customer-targeted sending for brand messages, you must submit an application. Without an approved application, you cannot use customer-targeted sending (targeting M, N, or O).

1. In the sender profile details, click **Apply to Use Customer-Targeted Sending**.
2. Upload the evidence file showing consent to receive advertising information.
    * The evidence file is stored at the KakaoTalk channel level. If you update the file, the change is applied to all sender profiles of other dealers using the same channel.
    * If a file uploaded by another dealer already exists, you can skip the file upload step and proceed with the application.
3. The application is approved when all of the following conditions are met:
    * Business-verified channel
    * Business registration number registered
    * Channel customer center phone number registered
    * 50,000 or more channel friends
    * History of at least one successful AlimTalk delivery within the last 3 months

!!! danger "Caution"
    If business verification is revoked, your permission to use customer-targeted sending is also revoked. You must reapply after the business verification re-review is completed.

<a id="delete-a-sender-profile"></a>
### Delete a Sender Profile { #delete-a-sender-profile }

You can delete a registered sender profile.

1. Select the checkbox of the sender profile to delete.
2. Click **Delete Sender Profile**.

<a id="manage-080-opt-out-numbers"></a>
## Manage 080 Opt-Out Numbers { #manage-080-opt-out-numbers }

The 080 opt-out number service provides recipients with an opt-out option when sending advertising messages. When sending promotional messages, **a free opt-out method must be included** so that recipients can opt out or withdraw their consent to receive messages free of charge.

!!! danger "Caution"
Violations may result in **a fine of up to 30,000,000 KRW** under the Act on Promotion of Information and Communications Network Utilization and Information Protection.

<a id="apply-for-an-080-opt-out-number"></a>
### Apply for an 080 Opt-Out Number { #apply-for-an-080-opt-out-number }

1. Click **+ Apply for 080 Opt-Out Number**.
2. Enter the company name. The company name entered will be announced when a call is made to the 080 opt-out number.
3. Once the application is complete, the status changes to Under Review.
4. Activation of the 080 opt-out service takes 3–4 business days, and the service can be used once activation is complete.

<a id="cancel-080-opt-out-number-service"></a>
### Cancel 080 Opt-Out Number Service { #cancel-080-opt-out-number-service }

* Select the checkbox of the registered 080 opt-out number and click **Cancel 080 Opt-Out Number Service**.
* 080 numbers with the status **In Use - Shared Number** cannot be cancelled.
