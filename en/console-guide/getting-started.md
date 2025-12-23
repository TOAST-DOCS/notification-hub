<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a { 
    display: inline !important;
}
</style>
<h1>Get Started With Notification Hub</h1>

**Notification > Notification Hub > Console User Guide > Get Started with Notification Hub **

<span id="identity-verification"></span>

## Identity verification

The Notification Hub is available after it is activated and Identity verification is completed. For more information on Identity verification, please check the ** Usage Policy and Preset Guide > Identity verification**.

* [Go to Identity verification Guide](./2-service-policy#identity-verification)


<span id="manage-sender-info"></span>

## Sender Information Management

<span id="manage-sender-phone-number"></span>

### Sender Number Management

To send SMS, LMS, and MMS messages, you need to register a sender number. Once you request a sender number registration review and it is approved, the sender number will be registered.

1. Click **+ Add Sender Number** and agree to **Agreement to collect and use Personal Information**.
2. Select the type of sender number you want to register and enter the sender number.
3. Attach the required documents for sender number type.

For more information on the Sender Number Pre-Registration System, see **Service Policy & Precondition > SMS > Sender Number Pre-Registration System**.

* [Sender Number Pre-Registration System Shortcut](./preconditions#sender-phone-number-pre-registration)

<span id="manage-sender-brand"></span>

### Brand Management

To send the RCS message, you must complete the brand linkage. If the pre-registration has been completed (brand approved) in the RCS Biz Center, proceed to link with the NHN Cloud console. For information on creating a brand in the RCS Biz Center, see **Service Policy & Precondition** > **RCS**.

* [Service Policy & Precondition > RCS Shortcut](./preconditions/preconditions-rcs)
* [Shortcut to the RCS Biz Center](https://www.rcsbizcenter.com/main)

When the RCS Biz Center has created a brand and set up an agency, registered a chat room (sender number), and registered a template (approved), the console will link the brand.

* Click **+ Brand linkage ** to complete the connection.

<span id="manage-sender-domain"></span>

### Manage Domains

To send emails, you need a domain, SPF authentication, DKIM authentication, and DMARC authentication that belongs to you.

For more information on sending domains and SPF, DKIM, and DMARC, check **Service Policy & Precondition > Email**.

* [Service Policy & Precondition > Email](./preconditions/preconditions-email).

#### Email Domain Registration and Ownership Authentication

You must register the domain and verify ownership of the domain. Register the values provided by Notification Hub in email domain DNS TXT record. Authentication ownership is confirmed by matching the TXT record in the domain you registered.

1. Click **+ Register Domain**.
2. Enter the root domain to register and click **Verify**.
3. If verification is successful, click **Register** to complete the registration.
4. In the Domain list, click **Authentication** in Domain Ownership Authentication Status.

If domain ownership authentication is successful, the domain authentication status changes to 'Completed'.

#### SPF Authentication

The sender policy framework (SPF) is a mechanism for authentication the credibility of email senders and sending servers, and it ensures that mail from a particular domain actually comes from an authorized email delivery server. The mail receiving server checks the SPF records registered in the sender's email domain DNS and processes mail sent from unregistered IP addresses as spam mail.

**SPF**
```
v=spf1 include:_spfblocka.toast.com ~all
```

1. Register the SPF record of item **SPF** above in the domain TXT record.
2. Select a domain from the list.
3. Click **Check Status** in **SPF Record Authentication Status** to complete SPF authentication.


!!! danger " Precautions "
    * Only one SPF record must be registered in the domain TXT record. If more than 2 or more SPF record is registered in the domain TXT record, SPF authentication may fail and the email receiving server may deny reception.
    * When inspecting SPF records, the use of mechanisms (include) and modifiers (redirects) to generate DNS queries is limited to a maximum of 10 and anything beyond that may cause the email receiving server to deny reception.
    
For a detailed description of SPF, please refer to the document below.

* [Introduce feature of Email Security Enhancement (SPF) Shortcut](https://meetup.nhncloud.com/posts/244)
* [RFC 4408 - 4.5 Selecting Records Shortcut](https://datatracker.ietf.org/doc/html/rfc4408#section-4.5)
* [RFC 4408 - 10.1 Processing Limits Shortcut](https://datatracker.ietf.org/doc/html/rfc4408#section-10.1)

#### DKIM Authentication

Domainkey identified mail (DKIM) is an email verification method in which an email sending server digitally signs an email and the email receiving server verifies the authenticity of the sender to ensure that messages are not forged or tampered with during delivery. DKIM prevents spammers and other malicious attackers from falsifying and tampering emails.


1. After completing domain ownership authentication, check the domain in the list and click **DKIM Settings**.
2. Set the TXT record value in the DNS hostname provided for DKIM authentication and click **Authentication** below.
    * If the registered domain is `example.com `, you must set a value in `toast._domainkey.example.com ` TXT record.
3. After the authentication is complete, enable it and click **Save** to complete DKIM authentication.

Please refer to the document below for a detailed description of DKIM.

* [Introducing Email Security Enhancements - Domain Protection, DKIM, DMARC Shortcuts](https://meetup.nhncloud.com/posts/248)


#### 3. DMARC authentication

Domain-based message authentication reporting and performance (DMARC) is the final step in enabling email security. It is a reporting and compliance policy for domain-based message authentication to prevent phishing and fraud using email spoofing. The email receiving server searches the DMARC record in DNS of the sender address (From) domain. According to the policy defined in the DMARC record, the receiving server authenticates the mail it receives.

**DMARC**
```
"v=DMARC1;p=none;sp=quarantine;pct=100;rua=mailto:${ Email_address_to_receive_ report }"
```

1. Complete the DMARC TXT record by adding an email address to the value in the above **DMARC** item to receive the DMARC report.
2. `_dmarc.` registers with the added subdomain TXT record.
    * For example, if the domain is `example.com ` register with the TXT record of `_dmarc.example.com `.
3.  Click **Check Status** in **DMARC Authentication Status** to complete DMARC authentication.

For a detailed description of DMARC, refer to the document below.

* [Introducing Email Security Enhancements - Domain Protection, DKIM, DMARC Shortcuts](https://meetup.nhncloud.com/posts/248)

##### Domain Protection

Domains with domain protection enabled cannot be used by other projects. To use the protected domains in other projects, the same domain registration and ownership authentication are required.

!!! danger " Precautions "
    If you disable domain protection, you can use the domain arbitrarily for other projects. For all authenticated domains, email from other projects will also be received as normal by the email receiving server. If the email is spam or phishing, the receiver can be harmed and the domain's reputation can be degraded causing the receiving email server to refuse reception.

<span id="manage-sender-push-authorization"></span>

### Push Authentication Management

For more information on issuing Push Credentials, check **Service Policy & Precondition > Push**.

* [Service Policy & Precondition > Push](./preconditions/preconditions-push)

#### FCM Authentication Settings
1. Enable **Service Account Key Registration**.
2. Copy and paste the contents of the FCM Service Account Credential file issued to the Service Account Key (JSON).
3. Click **Authenticate > Save** to complete the setup.

#### PNS Authentication Settings
1. Enable **APNS JWT certificate registration**.
2. Enter your **team ID and** **key ID**.
3. Enter **Topic**. The topic is the Bundle ID of App.
4. Copy and paste the contents of the **private key** file.
5. Click **Authenticate > Save** to complete the setup.

#### ADM Authentication Settings
1. Enable **Credentials Registration**.
2. Enter **Client ID** and **Client Key**.
3. Click **Authenticate > Save** to complete the setup.

<span id="manage-sender-profile"></span>

### Manage Outgoing Profiles

You need to create and register an outgoing profile to send a Alimtalk.

Outgoing profiles can be created by Kakao Business.

* [Outgoing Profile Generation Guide Shortcut](./preconditions#ktb-sender-profile)


Once the outgoing profile has been created in Kakao Business, follow the following steps to register.

1. Click **+ Register outgoing profile**, set outgoing profile ID, administrator mobile number, category, and click ** Request token**.
2. Enter the token sent to the administrator's mobile phone and click **OK > Register** to complete outgoing profile registration.


<span id="manage-080-unsubscription-number"></span>

### Manage Opt Out Numbers

Opt out number is a service that provides receivers with Unsubscription when sending advertising texts. When sending advertising information, you must include a free Unsubscription method so that the receiver can refuse or withdraw the consent.

#### Apply Subscription

* Click **+ Apply for 080 opt out number** to enter the company name. The company name you entered is the company name that will be displayed when calling the 080 Unsubscription number.
* When subscription is fully applied, the status is changed to Registration Scheduled. It takes 3 to 4 business days to open the 080-number service for unsubscription, and the service is enabled after opening.
* Once the opening is complete, you can check the starting date and time of use and the status. SMS product cannot be terminated while the 080-number service is reserved for registration or is being used. The product can be terminated after cancellation. To cancel, click **Cancel**.

#### Set 080 Unsubscription Number When Advertising Texts

* Advertising text can only be sent with 080 Unsubscription Number service is opened in a system.
* If you select the purpose of sending as an advertising on **Send > SMS** tab, the 080 Unsubscription Number Selection window will appear.
* Click **Opt out** to add required advertising phrases.
* When sending advertising, the message body must contain required advertising phrases, and the rules are as follows.
    * Starting phrase: (Advertising)
    * Ending phrase: Free Unsubscription {080 Unsubscription Number} or Free Unsubscription {080 Unsubscription Number} (the phrase may contain spaces)

##### Example
```
(Advertising) 
 
[Free Unsubscription]080XXXXXXX
```
```
(Advertising) 
 
Free Rejection 080XXXXXXX
```
