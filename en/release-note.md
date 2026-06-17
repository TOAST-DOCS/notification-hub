<!-- pre-align:aligned sig=472ab8839ab7 -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Notification Hub Release Notes</h1>

**Notification > Notification Hub > Release Notes**

## June 23, 2026
### Added Features
* [Console] Added AlimTalk common template feature
    * Provides message templates that can be used universally across industries, including orders, payments, and deliveries. Available without a separate review process.
* [Console, API] Launched brand message channel
    * Supports sending KakaoTalk brand messages.
    * Target recipients: company members (Groups M, N, and O), channel friends (existing Group I targeted sending)
    * Key differences compared to brand messages in the existing KakaoTalk BizMessage product:
        * Added Group O targeting: sends to channel friends among members who have consented to receive advertising messages from the company
        * Messages targeting company members can only be received by KakaoTalk 25.4.0 or later users

## May 27, 2026
<a id="added-features"></a>

### Added Features
* [API] Added KakaoBizCenter statistics retrieval API
    * Added an API to retrieve sending statistics and template statistics for AlimTalk and brand messages provided by KakaoBizCenter.
    * Daily (DAILY) or monthly (MONTHLY) statistics data can be retrieved based on the sender key.
    * For more information, see [API v1.0 User Guide > Kakao Statistics](./api-guide-v1x0/kakao-statistics).

<a id="march-24-2026"></a>

## March 24, 2026
<a id="added-features-2"></a>

### Added Features
* [API, Console] Added support for unified RCS messages
    * Supports sending unified RCS messages that can be received on both Android and iOS devices.
    * For the types of unified RCS messages that can be sent, see [Guide to Usage Policies and Preparations > RCS](./service-policy-and-precondition/rcs).
* [Console] Added KakaoBizCenter statistics
    * Provides a feature to retrieve statistics data for AlimTalk and brand messages provided by KakaoBizCenter.
* [API, Console] Added KakaoBizCenter group tag management feature
    * Provides a feature to manage group tags provided by KakaoBizCenter.
* [Console] Added message delivery history backup result notifications
    * You can receive result notifications when configuring backup settings for message delivery history that has exceeded the retention period.
    * You can configure this in **Project Dashboard > Notification Management**.

<a id="january-27-2026"></a>

## January 27, 2026
<a id="added-features-3"></a>

### Added Features
* [API] Added new AlimTalk template APIs and discontinued some existing APIs
    * Some existing template APIs have been replaced with new APIs due to changes in the AlimTalk template management structure. For more information, see [API v1.0 User Guide > Template](./api-guide-v1x0/template).
* [API] Added new external 080 opt-out number management API
    * APIs for registering and deleting external 080 opt-out numbers and retrieving opt-out numbers are now available. For more information, see [API v1.0 User Guide > Sender Information](./api-guide-v1x0/sender-unsubscribe).
* [Console] Added send request body JSON export feature
    * A JSON export feature for the information configured in the send menu is now available. For more information, see [Console User Guide > Send a Message](./console-guide/send-a-message).

<a id="12-31"></a>

## December 31, 2025
<a id="feature-removal"></a>

### Removed Features
* [API, Console] Discontinued Friend Talk service
    * The Friend Talk service will be discontinued on Wednesday, December 31, 2025.
    * Friend Talk-related features will no longer be available in the console, and the Friend Talk API will no longer be available.

<a id="12-04"></a>

## December 4, 2025
<a id="feature-improvements"></a>

### Feature Updates
* [API] Added the `exact` request parameter to the List Image Layouts API.
    * Previously, specifying a name with the `name` parameter applied a partial match (LIKE) search.
    * Now, setting the `exact` parameter to `true` retrieves only image layouts whose names match exactly.

<a id="08-26"></a>

## August 26, 2025
<a id="feature-improvements-2"></a>

### Feature Updates
* [API/Console] Added support for RCS image templates with financial compliance notice fields
    * Supports linking and sending image templates that include financial compliance notice fields in the RCS channel.

<a id="07-29"></a>

## July 29, 2025
<a id="new-features"></a>

### Added Features
* [API/Console] Added image layout feature
    * Image layouts are a feature for creating personalized MMS attachment images.
    * You can select an image layout when creating an MMS template, and personalized images can be generated through the image layout linked to the MMS template.
    * For more information, see [Console User Guide > Send a Message](./console-guide/image-layout) and [API v1.0 User Guide > Message > Image Layout](./api-guide-v1x0/image-layout).
* [API/Console] Added support for linking image layouts to MMS templates
    * You can select an image layout in the attachment section when creating an MMS template.
    * For more information, see [Console User Guide > Template](./console-guide/template/#templateV1x0001CreateSmsTemplate) and [API v1.0 User Guide > Message > MMS Template](./api-guide-v1x0/template/#templateV1x0001CreateSmsTemplate).
* [Console] When sending international SMS, you can now check the encoding and actual send count in the delivery details.
* [Console] The location of the **Attachment Management** menu has been changed.
    * The attachment management menu, previously located under the **Detailed Settings** menu, has been moved to the top-level menu.

<a id="05-27"></a>

## May 27, 2025
<a id="new-features-2"></a>

### Added Features
* [Console] Added support for receiving webhook events by specifying a URL when a designated event occurs.
    * For more information, see [Console User Guide > Detailed Settings > Webhook](./console-guide/detailed-setting/#webhook).
* [Console] Added support for backing up past message delivery history.
    * For more information, see [Console User Guide > Detailed Settings > Backup](./console-guide/detailed-setting/#backup).

<a id="04-15"></a>

## April 15, 2025
<a id="new-features-3"></a>

### Added Features
* [API/Console] Added support for viewing various event history generated by the service in CloudTrail.
    * For the list of events that can be viewed, see [CloudTrail > List of Collected Events](../../../Governance%20&%20Audit/CloudTrail/en/event-list).
* [API/Console] Added RCS authentication message sending.
* [API] Added response fields to the List Received Results by Contacts API.
    * For more information, see [API v1.0 User Guide > Received Results by Contacts > List Received Results by Contacts](./api-guide-v1x0/contact-delivery-result/#_1).
* [Console] Added RCS BizCenter LMS format type support
    * You can send RCS messages in LMS format type.
    * You can select the LMS format type when creating a template.

<a id="enhancements"></a>

### Feature Updates
* [API/Console] Improved the Push channel so that received and open events are collected in statistics.

<a id="03-25"></a>

## March 25, 2025
<a id="new-features-4"></a>

### Added Features
* [API] Added attachment and statistics APIs.
    * For more information, see [API v1.0 User Guide > Attachment](./api-guide-v1x0/attachment) and [API v1.0 User Guide > Statistics](./api-guide-v1x0/stats).

<a id="03-11"></a>

## March 11, 2025

<a id="new-features-5"></a>

### Added Features
* [API] Added RCS BizCenter brand message statistics integration
    * You can use message statistics provided by RCS BizCenter by adding a group ID when sending messages.
* [API] Added RCS message pending expiration period setting
    * When sending RCS messages, you can set timeouts (four types) for delivery attempts to devices.
* [API] Added RCS BizCenter LMS format type support
    * You can send RCS messages in LMS format type.
    * You can select the LMS format type when creating a template.
* For more information, see [API v1.0 User Guide > Message](./api-guide-v1x0/message).

<a id="enhancements-2"></a>

### Feature Updates
* [Console] Improved RCS template feature
    * When linking RCS BizCenter templates, you no longer need to click the brand link button, and changes to RCS BizCenter templates are now reflected automatically.

<a id="02-25"></a>

## February 25, 2025

<a id="new-features-6"></a>

### Added Features
* [API] Added List Final Delivery Results by Contacts API.
    * For more information, see [API v1.0 User Guide > Received Results by Contacts > List Final Delivery Results by Contacts](./api-guide-v1x0/contact-delivery-result/#_2).
* [API] Improved RCS BizCenter template sending to support adding a chat room ID and opt-out number.

<a id="enhancements-3"></a>

### Feature Updates
* [Console] Improved the delivery result view to display detailed result codes and messages.

<a id="02-11"></a>

## February 11, 2025

<a id="new-features-7"></a>

### Added Features
* [Console/API] Added support for sending RCS BizCenter LMS templates
    * RCS BizCenter LMS template types can now be sent.
* [API] Added Instant Flow Message API
    * Added an API that allows you to immediately create and send messages at the time of the request without registering a flow or template in advance.
    * For more information, see [API v1.0 User Guide > Message > Send Instant Flow Message](./api-guide-v1x0/message/#_6).
* [Console/API] Added duplicate recipient check feature
    * If duplicate contacts exist in the recipient list, you can check for them before sending to prevent duplicate deliveries.
* [Console] Added flow template preview feature
    * Added a feature to preview templates across multiple channels included in a flow from the Flow Management menu.
* [Console] Added AlimTalk quick link preview
    * Updated the AlimTalk channel template preview to display the **Quick Link** section.
* [API] Added user custom fields to the send API
    * Updated the send API to support including user custom fields in requests.
    * For more information, see [API v1.0 User Guide > Message](./api-guide-v1x0/message).

<a id="enhancements-4"></a>

### Feature Updates
* [Console/API] Improved RCS template feature
    * Improved so that templates registered in RCS BizCenter are automatically linked without requiring re-registration.
        * Templates are automatically linked when a brand is connected.
        * RCS BizCenter templates cannot be manually registered, modified, or deleted.
        * RCS BizCenter templates are registered with the chatbot and opt-out number left blank; when sending, the most recently registered chatbot is used.

<a id="11-12"></a>

## November 12, 2024

<a id="notification-hub-beta-release"></a>

### Notification Hub Beta Release

<a id="bug-fixes"></a>

### Bug Fixes
* [Console] Bug fixes
    * Fixed bugs in the send, flow, template, and statistics features.
* [API] Fixed authentication errors
    * Fixed an issue where authentication was not processed correctly for some API requests.

<a id="10-29"></a>

## October 29, 2024

<a id="notification-hub-alpha-release"></a>

### Notification Hub Alpha Release
* How to use
    * Products released in alpha can be accessed through **Customer Support > Contact Us**.
* [Console] Console released
    * Added the Send, Delivery Result, Address Book, Template, Flow, Detailed Settings, Statistics, and Identity Verification tabs.
* [API] Added API v1.0
    * Added Message, List Received Results by Contacts, Template, and Flow API v1.0.