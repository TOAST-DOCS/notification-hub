<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Email</h1>

**Notification > Notification Hub > Usage Policy and Preset Guide > Email**

## Register sending domain and DNS TXT record

To send emails from Notification Hub, you must have an sending domain of your own, so that each user can authenticate the sender's identity through their domain and that the email is not classified as spam. E-mail reliability can be enhanced by applying authentication settings such as SPF, DKIM, and DMARC through the sending domain. This allows e-mail to reach the receiver's mailbox safely and prevent phishing or spoofing. Through Notification Hub email sending (SMTP) server, an email is sent to the receiving server (SMTP) with an email address containing your own domain. For the email receiving server to trust Notification Hub email sending server, the SPF, DKIM, and DMARC TXT record settings are required in DNS where the user-owned domain is served. 

### Precautions

* Notification Hub may be restricted from sending when email bounce rates are excessively high, depending on the service's operational policy.
    * The bounce rate is the percentage of email addresses that were notified by the inbound SMTP server that the email could not be delivered (bounce or sending failure) among all the email addresses that the customer requested sending.
* Please manage not to cause excessive e-mail bounce rates.
* Return rate (return or fail to deliver) is caused by the following reasons.
    * Invalid sender email address or sending domain
    * Invalid receiver email address or receiving domain
    * Sending domains that do not apply email security measures such as SPF, DKIM, DMARC, etc.
    * When sending repeated or duplicate emails to the same receiver excessively
    * When sending a forged email to circumvent opt-out
    * When sending an email containing content that may be suspected of phishing or spam
    * When sending an advertising email that does not comply with the Act on Promotion of Information and Communications Network Utilization and Information Protection
* If email sending is restricted due to the bounce rate, check if there is any reason for the return and take improvement measures.
    * Then contact [Customer Center > 1:1 Inquiry](https://www.nhncloud.com/kr/support/inquiry) to enquire of releasing sending restrictions.

### SPF

The sender policy framework (SPF) is an authentication mechanism that defines a list of allowed servers when sending emails to prevent spam or phishing attacks that falsify sending domains. By adding an SPF record to the DNS of the sending domain, the email receiving server can authenticate whether the email was sent from the servers included in that list. This increases the confidence of the emailing server and prevents emails from being classified as spam.

* [Email Security Enhancement (SPF) Shortcut](https://meetup.nhncloud.com/posts/244)

### DKIM, DMARC

Domain Keys identified mail (DKIM) is an authentication method that adds a digital signature to an email to prove that the sending domain is not forged. The email sending server adds an email header containing the signature, and the email receiving server verifies the validity of the signature through the public key in the sending domain. This ensures that the email is not tampered with during transmission and increases the reliability of the sender and email sending server.

Domain-based message authentication, reporting, and conformity (DMARC) is a way to strengthen email authentication based on SPF and DKIM, and to define in policy how emails that fail to authenticate will be handled. Domain owners provide policies (reject, isolate, allow) to handle emails in the event of an authentication failure on the email receiving server through DMARC. The report feature also enables DMARC to receive report emails from email receiving servers about authentication failure cases, which it analyzes to help enhance domain protection.

* [Introduction to Email Security Enhancements (Domain Protection, DKIM, DMARC) Shortcuts](https://meetup.nhncloud.com/posts/248)

## Gmail-Related Guidelines

### Enhanced Gmail and Yahoo's email receiving standards

Starting February 1, 2024, Gmail and Yahoo's email sender guidelines has changed to deny sending requests to some incoming mail systems if domain authentication and SPF, DKIM, and DMARC authentication are not completed. As a result, sending to Gmail and Yahoo will fail for sending domains that have not completed SPF, DKIM, and DMARC authentication in Notification Hub.  

* [Gmail * Email Sender Guidelines](https://support.google.com/a/answer/81126)
* [Yahoo * Sender Requirements & Recommanations](https://senders.yahooinc.com/best-practices/)

#### Restricted Domain when SPF, DKIM, DMARC authentication is not completed.
* gmail.com
* yahoo.com

Gmail uses domain reputation as the primary criterion for spam mail decisions. If a sender with a low domain reputation sends a large number of emails at a high speed or an advertising email that the receiver does not want, it will be stored in the receiver's inbox, but it will be able to display alerts or store them in the spam mailbox, and furthermore, it will be able to slow down or deny reception at all. Therefore, if you want to send an email in bulk, always be careful to keep your domain reputation high by referring to the following guide

### Guide about being not possible to collect Viewed Event with Gmail.

If the receiver's email is Gmail, it is not possible to collect whether the email is viewed or not. Typically, the image tag is inserted into the body of the email to verify the receiver's email viewing, but Gmail modifies the body of the email to prevent the image proxy server from caching and tracking the image. This was intentionally blocked by Gmail, and it is currently not technically possible to collect events for such viewing.

!!! tip "Be informed - Gmail Image Proxy" 
    Because the Gmail Image Proxy service does not forward users' cookies, you can't use the measurement protocol to track Gmail users. The Gmail Image Proxy service prevents this by having the measurement protocol requests passed through an intermediate server.


* [Google Analytics > Email Tracking * Measurement Protocol](https://developers.google.com/analytics/devguides/collection/protocol/v1/email)

### Gmail’s low reputation issue

This is a brief guide to Gmail reputation criteria. Learn how Gmail evaluates reputation and learn how to raise and maintain reputation. For more information, read the references below.

#### Reputation?
When sending mail, the ISP (inbox service provider, Gmail, incoming SMPT server) evaluates the reputation of the sending SMTP server to determine whether it is received or not, and classifies spam. If you send mail that does not fit your ISP's reputation evaluation method, it can slow down the sending speed or make it difficult for recipients who use that ISP to receive mail.

Reputation can be largely divided into, IP reputation and domain reputation.
* IP Reputation: IP is the IP of the sending SMTP. It means the reputation of the IP of the sending SMTP.
* Domain Reputation: The domain is the mail sending domain. The domain of NHN will be 'nhn.com '. It refers to the reputation of the domain that is responsible for sending mail.

#### Gmail's reputation evaluation method
* Evaluates domain reputation more importantly: Domains are more important than IP because multiple domains often share and send IP. Engagement is more important than Complaints. Here, Complaints refers the recipient's spam processing, etc. Engagement refers to the recipient checking the contents of the mail, clicking on the links in the contents, and de-spam processing, etc.
* Other evaluation items: Evaluate various factors to determine your reputation, such as whether it is a personal mail or not, what the reputation of the sending IP is, whether there is a link in the mail, and what it contains every day.

#### How to raise reputation
* Need a warm-up process: sending large amounts of mail to new IPs and domains from the start is not desirable, and it can be lower your reputation. It should be gradually increased over the course of a few days, like 50, 100, 500, 1000...
* Send to high engagement recipients: You need to prove that the mail you send to Gmail is what they want. You can easily increase your reputation, in the process of preparation, by sending it to those who are far more engaged and loyal to the service and waiting for the mail to arrive than the average person.
* Providing a Unsubscription feature: The service should provide a feature to enable receive settings. One-Click Unsubscribe or provide a Unsubscription link at the bottom of the mail to help boost your reputation.
* Sending High Relevancy mail to receivers: To maintain a reputation, you should send mail to a person who is relevant to the content of the mail. It is more important than just sending mail often. The size of the delivery does not matter. You should segment  mail content and targets in detail. 66% of the reasons for cancellation of subscriptions are irrelevant mail, and 55% are due to message fatigue.

#### Refer to external documentation for reputation
* [Mailgun * Domain Reputation Or IP Reputation: Which One Does Gmail Care About More?](https://www.mailgun.com)
