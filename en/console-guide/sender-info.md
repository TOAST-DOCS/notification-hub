<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Sender Information</h1>

**Notifications > Notification Hub > Console User Guide > Sender Information**

Register and manage sender information for each message channel. To send messages, the sender information for each message channel must be registered in advance.

<span id="manage-sender-phone-number"></span>

## Manage Sender Numbers

To send SMS, LMS, or MMS messages, you must register a sender number. In accordance with the notice related to the Telecommunications Business Act, identity verification of the account holder is required when registering a sender number. The verification method and required documents are determined by the member type and sender number type.

<span id="register-sender-phone-number"></span>

### Register a Sender Number

1. Click **+ Register Sender Number** and agree to **the consent form for the collection and use of personal information**.
2. Select the sender number type to register and enter the sender number.
3. Attach the documents required for the sender number type.
4. Once the review is approved after submitting the registration request, the sender number is registered.

For information on the sender number pre-registration system, refer to **Service Policy and Prerequisites > SMS > Implementation of Sender Number Pre-Registration System**.

* [Go to Sender Number Pre-Registration System](../service-policy-and-precondition/sms#sender-phone-number-pre-registration)

<span id="sender-phone-number-verification"></span>

### Account Holder Verification Guide

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

<span id="sender-phone-number-format"></span>

### About Sender Number Input Format

* Landline number: 02-YYY-YYYY (register including area code)
* Mobile number: 010-ABYY-YYYY
* Common service identification number: 0N0 series (area code must not be used before the number)
* Sender numbers between 8 and 11 digits can be entered
* Messages cannot be sent to non-existent number ranges (e.g., 070-0YYY, 070-1YYY, 010-0YYY, 010-1YYY)

<span id="delete-sender-phone-number"></span>

### Delete an Sender Number

You can delete a registered sender number.

1. Select the checkboxes of the sender numbers you want to delete.
2. Click **Delete Sender Number**.

<span id="manage-brand"></span>

## Brand Management

To send RCS messages, you need to register your brand in RCS Biz Center and integrate with NHN Cloud Console.

<span id="brand-prerequisites"></span>

### Prerequisites

The following must be completed (approved) in RCS Biz Center before integrating a brand:

1. Sign up for RCS Biz Center, create and get a brand approved
2. Designate "NHN Cloud" as an agency in the Brand Operations Management menu
3. Register and get a chatroom (sender number) approved

For prerequisites in RCS Biz Center, refer to **Service Policy and Prerequisites > RCS**.

* Go to [Service Policy and Prerequisites > RCS](../service-policy-and-precondition/rcs)
* [Go to RCS Biz Center](https://www.rcsbizcenter.com/main)

<span id="brand-sync"></span>

### Integrate a Brand

Brand is linked based on the business registration number on the attached business registration card when authenticating yourself.

* Click **+ Integrate Brand** to synchronize brands registered in RCS Biz Center
* Once brand integration is complete, the brand list is displayed.
* If you've changed your brand information in RCS Biz Center, click **Integrate Brand** to proceed with the update.

<span id="manage-domain"></span>

## Manage Domains

To send emails, you must register a domain you own and verify domain ownership. After successful domain verification, you can configure SPF record verification, DMARC verification, and DKIM settings.

For sender domains and SPF, DKIM, and DMARC, refer to **Service Policy and Prerequisites > Email**.

* [Go to Service Policy and Prerequisites > Email](../service-policy-and-precondition/email)

<span id="register-domain"></span>

### Register an Email Domain and Verify Ownership

You must register a domain and verify domain ownership. Register the value provided by Notification Hub in the email domain DNS TXT record. Verify ownership by checking that the provided value matches the TXT record of the registered domain.

1. Click **+ Register Domain**.
2. Enter the root domain to register and click **Verify**.
3. If verification is successful, click **Register** to complete the registration.
4. Click **Verify** in the domain ownership verification status in the domain list.

If domain ownership verification is successful, the domain verification status changes to **Completed**.

<span id="spf-authentication"></span>

### SPF Authentication

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

<span id="dkim-authentication"></span>

### Configure DKIM

DomainKeys identified mail (DKIM) is an email verification method in which the email sending server digitally signs emails and the email receiving server verifies the authenticity of the sender to ensure that messages have not been forged or altered during transmission.

1. After completing domain ownership verification, check the domain in the list and click **Configure DKIM**.
2. Set the TXT record value for the DNS hostname provided for DKIM verification and click **Verify** below.
    * If the registered domain is `example.com`, set the value in the `toast._domainkey.example.com` TXT record.
3. After verification is complete, enable the setting and click **Save** to complete DKIM configuration.

<span id="dmarc-authentication"></span>

### DMARC Authentication

Domain-based message authentication, reporting and conformance (DMARC) is the final step in enhancing email security. It is a domain-based message authentication, reporting, and conformance policy to prevent phishing and fraud using email spoofing.

DMARC
```
v=DMARC1;p=none;sp=quarantine;pct=100;rua=mailto:${email_address_to_receive_reports}
```

1. Add the email address to receive DMARC reports to the value in the DMARC field above to complete the DMARC TXT record.
2. Register in the subdomain TXT record with `_dmarc.` added.
    * e.g., If the domain is `example.com`, register in the TXT record of `_dmarc.example.com`.
3. Click **Check Status** in the **DMARC Authentication Status** field to complete DMARC authentication.

<span id="domain-protection"></span>

### Domain Protection

Domains with domain protection enabled cannot be used in other projects. To use a protected domain in another project, domain registration and ownership verification must be completed in the same way.

!!! danger "Caution"
If domain protection is disabled, other projects can use the domain without restriction. For domains that have completed all verifications, emails sent from other projects are also received normally by the email receiving server. If such emails are spam or phishing, recipients may be harmed and the domain's reputation may decline, causing the email receiving server to reject incoming emails.

<span id="delete-domain"></span>

### Delete a Domain

You can delete a registered domain.

1. Select the checkbox of the domain to delete.
2. Click **Delete Domain**.

<span id="manage-push-authentication"></span>

## Manage Push Authentication

To send push messages, you must register the credentials issued by the push service.

For information on how to obtain push authentication information, refer to **Service Policy and Prerequisites > Push**.

* [Go to Service Policy and Prerequisites > Push](../service-policy-and-precondition/push)

<span id="fcm-authentication"></span>

### Configure FCM Authentication

Firebase cloud messaging (FCM) authentication must be configured to send push messages to Android devices.

1. Click **Change Setting** in **FCM Service Account Key Registration**.
2. Copy and paste the contents of the FCM Service Account Credential file issued to the service account key (JSON).
3. Click **Verify > Save** to complete the configuration.

<span id="apns-authentication"></span>

### Configure APNS Authentication

Apple Push Notification Service (APNS) authentication must be configured to send push messages to iPhones.

1. Click **Change Setting** in **APNS JWT Certificate Registration**.
2. Enter the **Team ID** and **Key ID**.
3. Enter the **topic**. The topic is the app's Bundle ID.
4. Copy and paste the contents of the **private key** file.
5. Click **Verify > Save** to complete the configuration.

<span id="adm-authentication"></span>

### ADM Authentication Settings

Amazon device messaging (ADM) authentication must be configured to send push messages to Amazon Kindle, Fire, and other devices.

1. Click **Change Setting** in **ADM Authentication Registration**.
2. Enter the **Client ID** and **Client Key**.
3. Click **Verify > Save** to complete the configuration.

<span id="manage-sender-profile"></span>

## Manage Sender Profiles

To send AlimTalk or brand messages, you must register a KakaoTalk sender profile.

<span id="sender-profile-prerequisites"></span>

### Prerequisites

To register a sender profile, a KakaoTalk channel must be created. Create a KakaoTalk channel on the KakaoTalk website.

* [Go to Create KakaoTalk Channel](https://center-pf.kakao.com/)

To register a sender profile, business verification must be completed after registering the KakaoTalk channel.

For information on how to create a sender profile, refer to **Service Policy and Prerequisites > AlimTalk/Brand Messages**.

* [Go to Service Policy and Prerequisites > AlimTalk/Brand Messages](../service-policy-and-precondition/alimtalk-and-friendtalk)

<span id="register-sender-profile"></span>

### Register Sender Profile

1. Click **+ Register Sender Profile**.
2. Set the sender profile ID, administrator mobile number, and category, then click **Request Token**.
3. Enter the 6-digit token number sent to the administrator's mobile phone.
4. Click **Confirm > Register** to complete sender profile registration.

!!! danger "Caution"
**The default maximum daily delivery count for AlimTalk is 1,000**. To change the maximum daily delivery count, contact [Customer Center](https://www.nhncloud.com/kr/support/inquiry).

<span id="manage-sender-profile-group"></span>

### Manage Sender Profile Groups

You can manage sender profiles in groups.

* Click **Manage Sender Profile Groups** to create a group and add sender profiles to the group.

<span id="kakao-statistics"></span>

### View Kakao Statistics

Click **Go to Kakao Statistics** in the sender profile details to view Kakao statistics in a new window. Statistics criteria include delivery statistics and template statistics, and the query conditions vary depending on the message channel. You can view the results in charts and tables.

* Real-time statistics are not provided. Data collected the previous day is provided daily at around 7 AM.
* AlimTalk statistics are first provided on D+1 and finalized on D+2.
* Valid opens are not counted more than once for the same message.
* Clicks are counted multiple times for the same message.
* If the number of successful deliveries is 10 or fewer, valid opens and clicks are not provided.

#### Delivery Statistics

Retrieves the daily delivery count, valid opens, and clicks by sender profile. You can query by setting conditions such as period, delivery identifier, and message type.

#### Template Statistics

Retrieves the daily delivery count, valid opens, and clicks by template and group tag. You can query by setting conditions such as period and message type.

* Brand message free format is provided only when a group tag is used.

<span id="manage-group-tag"></span>

### Manage Group Tags

Group tags are identification tags used when querying template statistics for brand messages. Click the **Group Tag Management** tab in the new **Go to Kakao Statistics** window to manage group tags.

!!! danger "Caution"
Group tags can only be used for brand messages. AlimTalk is not applicable.

* Click **+ Register Group Tag** to enter a group tag name and register it.
* Select the checkbox of the group tag to modify or delete, and click **Modify Group Tag** or **Delete Group Tag**.

<span id="delete-sender-profile"></span>

### Delete a Sender Profile

You can delete a registered sender profile.

1. Select the checkbox of the sender profile to delete.
2. Click **Delete Sender Profile**.

<span id="manage-080-unsubscription-number"></span>

## Manage 080 Opt-Out Numbers

The 080 opt-out number service provides recipients with an opt-out option when sending advertising messages. When sending promotional messages, **a free opt-out method must be included** so that recipients can opt out or withdraw their consent to receive messages free of charge.

!!! danger "Caution"
Violations may result in **a fine of up to 30,000,000 KRW** under the Act on Promotion of Information and Communications Network Utilization and Information Protection.

<span id="register-080-number"></span>

### Apply for an 080 Opt-Out Number

1. Click **+ Apply for 080 Opt-Out Number**.
2. Enter the company name. The company name entered will be announced when a call is made to the 080 opt-out number.
3. Once the application is complete, the status changes to Under Review.
4. Activation of the 080 opt-out service takes 3–4 business days, and the service can be used once activation is complete.

<span id="cancel-080-number"></span>

### Cancel 080 Opt-Out Number Service

* Select the checkbox of the registered 080 opt-out number and click **Cancel 080 Opt-Out Number Service**.
* 080 numbers with the status **In Use - Shared Number** cannot be cancelled.
