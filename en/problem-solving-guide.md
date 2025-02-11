<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Notification Hub Troubleshooting Guide</h1>

**Notifications > Notification Hub > Troubleshooting Guide**

<span id="sms-delivery-failure"></span>

## You cannot proceed with identity verification.

Only business members can use Notification Hub through identity verification. If you are an individual member, you cannot proceed with self-authentication. Re-register as a business member and proceed with Identity verification.

## Despite joining as a business member, you cannot proceed with your Identity Verification.

In Notification Hub, the criteria for business membership follow the type of organization (OWNER) member of the project you activated. If the organization's owner member is an individual member, you cannot proceed with Identity verification as a business member. Change the organization's individual owner member to a business member and proceed with Identity verification.

## Sent characters are not received by some receiver devices.

If texts are not received from the receiver device, the receiver's number may be subscribed to the **Stolen Number Text Message Blocking Service’** or the **Mobile Carrier spam blocking service**. Resend the text after terminating the service. For more information about **Stolen Number Text Message Blocking Service’** and **Mobile Carrier spam blocking service**, check the link below.

* [Guide of Stolen Number Text Message Blocking Service](service-policy-and-precondition/sms#about-phone-scam-blocking-services)
* [Mobile Carrier Spam Blocking Service Guide](service-policy-and-precondition/sms#about-phone-scam-blocking-services)

## iPhone will not receive push messages, and the registered token will be deleted.

If registered your token in iPhone App and sent a push message, but don't receive a push message and the registered token is deleted, check the below.

* **APNS JWT credentials mismatch**
  * If the APNS JWT credentials registered with Notification Hub and the app do not match, push messages will not be received. Make sure the APNS JWT credentials and the app's bundle ID can be used together.
* **Mismatch between build type of App and contact type of registered token**
  * If the build type of the app and the contact type of the registered token do not match, the push message will not be received. Check the contact type and build mode.
  * Tokens in the Development app must be registered as TOKEN_APNS_SANDBOX, or TOKEN_APNS_SANDBOX_VOIP.
  * Tokens in the Production app must be registered as TOKEN_APNS, or TOKEN_APNS_VOIP.
  * Each contact type is as follows in SDK.
    * TOKEN_APNS: APNS
    * TOKEN_APNS_SANDBOX: APNS_SANDBOX
    * TOKEN_APNS_VOIP: APNS_VOIP
    * TOKEN_APNS_SANDBOX_VOIP: APNS_SANDBOXVOIP

## Push messages are not received on an Android device and the registered token has been deleted.
  
If you have registered your token in Android App and sent a push message, but don't receive a push message and the registered token is deleted, check the below.

* **FCM service account key (JSON) and app Sender ID (Sender ID) mismatch**
  * If the FCM service account key (JSON) registered in Notification Hub and the app's sender ID (Sender ID) do not match, push messages will not be received. Make sure that the FCM service account key (JSON) and the app's sender ID (Sender ID) can be used together.
    * [FCM - Description of Sender ID shortcut](https://firebase.google.com/docs/cloud-messaging/concept-options#credentials)
    * [FCM - Service Account Key (JSON) Generation Guide Shortcut](https://firebase.google.com/docs/cloud-messaging/http-server-ref)
        ```
        A registration token is tied to a certain group of senders.  
        When a client app registers for FCM, it must specify which senders are allowed to send messages.  
        You should use one of those sender IDs when sending messages to the client app.  
        If you switch to a different sender, the existing registration tokens won't work.
        ```


!!! tip "If the problem is not resolved" 
    * On line 1:1 Enquiry: [https://www.nhncloud.com/kr/support/inquiry?alias=tab5_03](https://www.nhncloud.com/kr/support/inquiry?alias=tab5_03) 
    * Representative Phone #: 1588-7967 (Operating hours: Monday to Friday 10:00-19:00)