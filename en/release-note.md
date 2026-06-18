<!-- pre-align:aligned sig=472ab8839ab7 -->

<h1>Notification Hub Release Notes</h1>

**Notification > Notification Hub > Release Notes**
## 2026. 06. 23.
<a id="added-features-4"></a>

### Added Features
* [Console] Added the AlimTalk shared template feature
    * Provides message templates that can be used universally regardless of industry, such as orders, payments, and deliveries. Available without a separate review process.
* [Console, API] Launched the Branded Message channel
    * Supports sending KakaoTalk Branded Messages.
    * Recipients: Customer members (M, N, and O groups), channel friends (existing I group targeting delivery)
    * Key differences compared to branded messages in the existing KakaoTalk Bizmessage product:
        * Added O group targeting: sends messages to channel friends among members who have agreed to receive advertising messages from the customer
        * Messages sent to customer members can only be received by KakaoTalk version 25.4.0 or later users

<a id="may-27-2026"></a>

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
* [API, Console] Integrated RCS message support
  * Added support for sending integrated RCS messages that can be received on both Android and iOS devices.
  * For the types of integrated RCS messages that can be sent, refer to [Service Policy and Prerequisites > RCS](./service-policy-and-precondition/rcs).
* [Console] KakaoBizCenter statistics
  * Added a feature to retrieve statistics data for AlimTalk and brand messages provided by KakaoBizCenter.
* [API, Console] KakaoBizCenter group tag management
  * Added a feature to manage group tags provided by KakaoBizCenter.

<a id="january-27-2026"></a>

## January 27, 2026
<a id="added-features-3"></a>

### Added Features
* [API] Launch Alimtalk Template APIs and discontinue support for select APIs
    * Due to changes in the Alimtalk template management structure, some legacy template APIs have been replaced with new ones. For more information, please refer to [API v1.0 User Guide > Template](./api-guide-v1x0/template).
* [API] Release new APIs for managing external 080 opt-out numbers
    * APIs for registering/deleting external 080 opt-out numbers and inquiring about opt-out lists are now available. For more details, please refer to [API v1.0 User Guide > Sender Information](./api-guide-v1x0/sender-unsubscribe).
* [Console] Enable JSON extraction for dispatch request bodies
    * JSON extraction is now available for configurations set in the Send menu. For more information, please refer to [Console User Guide > Send](./console-guide/send-a-message).

**Notification > Notification Hub > Release Notes**

<a id="12-31"></a>

## 2025. 12. 31.
<a id="feature-removal"></a>

### Feature Removal
* [API, Console] FriendTalk Service End of Support 
    * The FriendTalk service will end on Wednesday, December 31, 2025. 
    * FriendTalk-related features will no longer be available in the console, and the FriendTalk API will no longer be available.

<a id="12-04"></a>

## 2025. 12. 04.
<a id="feature-improvements"></a>

### Feature Improvements
* [API] The `exact` request parameter has been added to the image layout list retrieval API.
    * Previously, when specifying a name using the `name` parameter, partial matching (LIKE) search was applied.
    * Now, setting the `exact` parameter to `true` retrieves only image layouts with exactly matching names.

<a id="08-26"></a>

## 2025. 08. 26.
<a id="feature-improvements-2"></a>

### Feature Improvements
* [API/Console] Support for RCS image templates including financial compliance notice fields
    * Supports integration and sending of image templates that include financial compliance notice fields in RCS channels.

<a id="07-29"></a>

## 2025. 07. 29.
<a id="new-features"></a>

### New Features
* [API/Console] Image layout feature has been released.
    * The image layout feature enables the generation of personalized MMS attached images.
    * Image layouts can be associated with MMS template, enabling the automatic creation of customized images when sending messages via the MMS template.
    * For detailed information, please refer to [Console User Guide > Send](./console-guide/image-layout) and [API v1.0 User Guide > Messages > Image Layout](./api-guide-v1x0/image-layout).
* [API/Console] Image layouts can be associated with MMS templates.
    * An image layout can be selected in the attachment section during MMS template creation.
    * For detailed information, please refer to [Console User Guide > Templates](./console-guide/template/#templateV1x0001CreateSmsTemplate) and [API v1.0 User Guide > Messages > MMS Templates](./api-guide-v1x0/template/#templateV1x0001CreateSmsTemplate).
* [Console] Encoding and message count information is now available in send details when sending international SMS messages.
* [Console] The "Attachment File" menu has been relocated.
    * The attachment file management menu, previously located under the "Detailed Settings" menu, has been moved to the top-level menu.

<a id="05-27"></a>

## 2025. 05. 27.
<a id="new-features-2"></a>

### New Features
* [Console] Webhook events can be received for specified event occurrences by designating a URL.
    * For detailed information, please refer to the [Console User Guide > Detailed Settings > Webhook](./console-guide/detailed-setting/#webhook).
* [Console] Past message dispatch history can now be backed up.
    * For detailed information, please refer to the [Console User Guide > Detailed Settings > Backup](./console-guide/detailed-setting/#backup).

<a id="04-15"></a>

## 2025. 04. 15.
<a id="new-features-3"></a>

### New Features
* [API/Console] Event history from the service can now be monitored through CloudTrail.
    * For a list of available events, please refer to [[CloudTrail > List of Collected Events]](../../../Governance%20&%20Audit/CloudTrail/en/event-list).
* [API/Console] Message sending for RCS authentication purposes has been added.
* [API] A response field has been added to the API for retrieving the list of delivery results per contact.
    * For detailed information, please refer to [[API v1.0 User Guide > Delivery Results by Contact > Retrieve List of Delivery Results by Contact]](./api-guide-v1x0/contact-delivery-result/#_1).
* [Console] Support for RCS BizCenter LMS format has been added.
    * RCS messages can now be sent in LMS format.
    * The LMS format can be selected during template creation.

<a id="enhancements"></a>

### Enhancements
* [API/Console] The system has been improved to collect receive and open events for the Push channel in statistics.

<a id="03-25"></a>

## 2025. 03. 25.
<a id="new-features-4"></a>

### New Features
* [API] Attachment and Statistics APIs have been added.
    * For detailed information, please refer to [[API v1.0 User Guide > Attachment]](./api-guide-v1x0/attachment) and [[API v1.0 User Guide > Statistics]](./api-guide-v1x0/stats).

<a id="03-11"></a>

## 2025. 03. 11.
<a id="new-features-5"></a>

### New Features
* [API] Integration with RCS BizCenter brand message statistics.
    * By adding a group ID when sending messages, you can use the message statistics provided by RCS BizCenter.
* [API] Added setting for RCS message reception timeout period.
    * A timeout (in 4 types) can be set for transmission attempts to a device when sending RCS messages.
* [API] Support for RCS BizCenter LMS format.
    * RCS messages can now be sent in LMS format.
    * The LMS format can be selected during template creation.
* For detailed information, please refer to the [[API v1.0 User Guide > Message]](./api-guide-v1x0/message).

<a id="enhancements-2"></a>

### Enhancements
* [Console] RCS template functionality has been improved.
    * It is no longer necessary to click the brand integration button when linking RCS BizCenter templates; changes to the templates are now reflected automatically.

<a id="02-25"></a>

## 2025. 02. 25.
<a id="new-features-6"></a>

### New Features
* [API] An API for retrieving the final list of delivery results per contact has been added.
    * For detailed information, please refer to [[API v1.0 User Guide > Delivery Results by Contact > Retrieve Final List of Delivery Results by Contact]](./api-guide-v1x0/contact-delivery-result/#_2).
* [API] The system has been improved to allow the addition of a chat room ID and opt-out number when sending RCS BizCenter template messages.

<a id="enhancements-3"></a>

### Enhancements
* [Console] The send tracking feature has been improved to allow confirmation of detailed result codes and messages.

<a id="02-11"></a>

## 2025. 02. 11.
<a id="new-features-7"></a>

### New Features
* [Console/API] Support for sending RCS BizCenter LMS templates.
    * RCS BizCenter LMS template types can now be sent.
* [API] Instant Flow Message API has been added.
    * This API allows for the immediate creation and dispatch of messages at the time of request, without prior registration of flows or templates.
    * For detailed information, please refer to [[API v1.0 User Guide > Message > Send Instant Flow Message]](./api-guide-v1x0/message/#_6).
* [Console/API] Duplicate recipient check function.
    * If duplicate contacts exist in the recipient list, this can be checked before sending to prevent duplicate dispatches.
* [Console] Flow template preview function has been added.
    * This function allows for previewing templates of various channels included in a flow within the flow management menu.
* [Console] Alimtalk direct link preview has been added.
    * The 'direct link' item can now be checked in the Alimtalk channel template preview.
* [API] User custom field has been added to the Send API.
    * Requests can now be made to the Send API including a user custom field.
    * For detailed information, please refer to the [[API v1.0 User Guide > Message]](./api-guide-v1x0/message).

<a id="enhancements-4"></a>

### Enhancements
* [Console/API] RCS template functionality has been improved.
    * Templates registered in RCS BizCenter are now integrated without needing to be re-registered.
        * Templates are automatically linked upon brand integration.
        * RCS BizCenter templates cannot be manually registered, modified, or deleted.
        * For RCS BizCenter templates, the chatbot and opt-out number fields are registered as blank; the most recently registered chatbot will be used for sending.

<a id="11-12"></a>

## 2024. 11. 12.

<a id="notification-hub-beta-release"></a>

### Notification Hub Beta Release

<a id="bug-fixes"></a>

### Bug Fixes
* [Console] Error resolution
    * Resolved errors in the send, flow, template, and statistics features.
* [API] Authentication error resolution
    * Resolved an issue where authentication was not being processed correctly for certain API requests.

<a id="10-29"></a>

## 2024. 10. 29.

<a id="notification-hub-alpha-release"></a>

### Notification Hub Alpha Release
* How to Use
    * Products released in alpha are available through **Customer Center > 1:1 Inquiry**.
* [Console] Released Console 
    * Added Send, Send tracking, Address book, Templates, Flows, Details, Statistics, and Identity verification tabs.
* [API] Added API v1.0
    * Added messages, contacts received results list lookup, templates, and flow API v1.0