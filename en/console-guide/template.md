<!-- pre-align:aligned sig=671bfe2d761c -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Template</h1>

**Notification > Notification Hub > Console User Guide > Template**


<span id="template"></span>

## Templates

You can save frequently used messages or messages that require a consistent format as templates, and use those saved templates when sending messages. For example, if you create templates for frequently used message formats such as customer support, announcements, notifications, or marketing messages, you can send them by modifying only a portion of the information each time, without having to write the same content from scratch.

<a id="category"></a>

### Category
* First, select a root category and click **+ Add Category** to create a category.
* The category is created under the selected category.

<a id="template"></a>

### Template
1. Select the category that the template belongs to and click **+ Register Template**. You will be taken to the template creation page, where additional settings for the selected message channel are displayed.
2. Complete the title, content, and settings required by each message channel, then click **Register**.

<a id="alimtalk-template"></a>

#### Alim Talk Template

Alim Talk templates require Kakao's review and approval after a registration request before they can be used.

* Available message types include: Add Channel, Basic, Supplemental Information, and Composite.
* Available emphasis types include: Emphasis, Image, and Item List.
* Select the type you want and create the template.

* KakaoTalk Alim Talk guides
    * [[Alim Talk Creation Guide]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/content-guide), [[Alim Talk Review Guide]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit), [[Alim Talk Whitelist]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit/white-list), [[Alim Talk Blacklist]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit/black-list)
* Sender Profile/Group
    * Select the sender profile or sender profile group for which to register the template. If you register it to a group, all sender profiles in the group can use that template.
    * If the same template code exists in the sender profile/group, the template registered to the sender profile takes priority.
    * For sender profile groups, templates cannot be registered using the "Add Channel" or "Composite" message types.
* Template Code/Template Name
    * You cannot register duplicate template codes or template names within the same sender profile/group.

* Template Content
    * Alim Talk messages can be up to 1,000 characters long, regardless of language, including variables, URLs, spaces, and button names. When registering with variables, write the template with the substituted content in mind.<br/> For detailed character count guidelines, see [Alim Talk Template Notes](https://docs.nhncloud.com/ko/Notification/KakaoTalk%20Bizmessage/ko/alimtalk-overview/#_3).
    * Write variables in the format #{variable}. (Example: #{name}'s package is scheduled to be delivered today at (#{09:50}).)
    * When registering buttons, variables cannot be entered for button names, but variables can be entered for button URLs. (Example: http://kakao.com/#{variable})
    * When registering button URLs, url_mobile and url_pc links must include 'http://' or 'https://', and scheme_ios and scheme_android links must be registered in the correct scheme format. Otherwise, template registration is not possible.
* Security Template
    * When a template is set as a security template, the message content is not displayed on devices other than mobile. (The message 'Please check on your mobile device' is displayed instead.)
    * For general messages, the setting value may be changed during review. For templates related to OTP, authentication codes, passwords, and credit information/rating change notifications, the security option must be checked.

<a id="alimtalk-template-button"></a>

#### Alim Talk Template Buttons
* You can register up to 5 buttons per template.
* Quick Reply
    * Quick reply cannot use tracking shipment and plug-in types, and other types can be used the same as buttons.
    * You can use up to 10 quick replies per template. When using quick replies, the number of buttons is limited to 2.

| Button Type | Description |
| --- | --- |
| Tracking Shipment | - Navigates to the courier company's shipment tracking page.<br/> - Check the courier companies that support the Tracking Shipment button and the invoice number patterns for each courier. [[Alim Talk Tracking Shipment Invoice Number Pattern Guide]](https://www.nhncloud.com/kr/support/notice/detail/1455) |
| Web Link | - Navigates to a mobile or PC webpage.<br/> - You can set URL links as variables. |
| App Link | - Launches an app using a custom scheme.<br/> - You must set the custom scheme to run on Android and iOS separately. |
| Bot Keyword | - The button name is forwarded to the agent.<br/> - If a channel that does not support Consultation Chat adds this button, Alim Talk sending is not available. |
| Message Delivery | - The button name and message body are forwarded to the agent.<br/> - If a channel that does not support Consultation Chat adds this button, Alim Talk sending is not available. |
| Bot for Consultation | - Connects to Consultation Chat.<br/> - If a channel that does not support Consultation Chat adds this button, Alim Talk sending is not available. |
| Bot Transfer | - Invokes the chatbot.<br/> - If a channel that does not support Consultation Chat adds this button, Alim Talk sending is not available. |
| Add Channel | - Adds the channel that sent the Alim Talk. The display position can only be used as the first button.<br/> - If the channel has already been added, it is not displayed to the recipient. |
| Image Secure Transmission Plugin | - Encrypts and transmits images containing sensitive information within the chat window.<br/> - A BizPlugin must be created. [[BizPlugin Guide]](https://business.kakao.com/info/talkbizplugin/) |
| Personal Information Use Plugin | - Obtains consent for collecting personal information required to provide services within the chat window, without membership registration.<br/> - A BizPlugin must be created. [[BizPlugin Guide]](https://business.kakao.com/info/talkbizplugin/) |
| One-Click Payment Plugin | - Allows users to pay for products within the chat window without switching screens.<br/> - The payment plugin does not support direct registration on the platform. Contact [Kakao Customer Center](https://cs.kakao.com/helps?service=127&category=572&locale=ko) for assistance. |
| Business Form | - If a business form has been created and connected to the current channel, clicking the button invokes the configured business form.<br/> - A business form must be created. [[Business Form Guide]](https://business.kakao.com/info/talkbizform/) |

<a id="template-inspection"></a>

#### Template Review
Alim Talk template review and screening are conducted directly by Kakao, and they are processed sequentially within 2 business days after the review request.

* Register Template Inquiry
    * If you have comments to deliver to the Kakao review team before submitting a review request, enter the content in the inquiry registration field. Templates in the Requested/Approved state cannot submit inquiries. (Only templates in the **Under Review/Rejected** state can register inquiries.)
    * The registered inquiry is added to the review results, and the Kakao review team confirms it.
    * The review results include inquiries about the template's purpose and rejection reasons.
    * When a template is rejected, you can request re-review by clicking **Register Inquiry** and **Edit**.

<a id="template-status"></a>

#### Template Status
* When a template is registered, the status is updated in the following order: **Requested > Under Review > Approved/Rejected**.
* After template registration, if the same status is maintained for one year or no additional messages are sent, the template transitions to **Dormant** status. For the related guide, see [Alim Talk Template Notes](https://docs.nhncloud.com/ko/Notification/KakaoTalk%20Bizmessage/ko/alimtalk-overview/#_3).

<a id="modify-templates"></a>

#### Edit Templates
* Only templates in the **Approved/Rejected** state can be edited.
* When you edit an approved template and the review is complete, the original template content is replaced with the edited content.
* The sender profile/group and template code cannot be edited.
* Edited templates go through the review process again, starting from the **Under Review** state.

<a id="delete-templates"></a>

#### Delete Templates
* Only templates in the Requested/Rejected state can be deleted.
* Rejected templates can be re-registered after **deletion**.
* Deleted template codes can be reused.

<a id="brand-message-template"></a>

#### Brand Message Template
Unlike Alim Talk templates, brand message templates do not require a review process and can be created, edited, and deleted freely.

* Select a sender profile and register the template.
* Template codes are not registered directly by users; instead, Kakao assigns a random identifier.
* Select a message type and write the content.
    * Supported message types: Text, Image, Wide Image, Wide Item List, Carousel Feed, Premium Video, Commerce, Carousel Commerce
* You can register buttons.
    * Supported button types: Web Link, App Link, Bot Keyword, Message Delivery, Bot for Consultation, Bot Transfer, Business Form, Add Channel
* You can register coupons.
* To attach an image, you must first register the image.

<a id="shared-alim-talk-template"></a>

#### Shared Alim Talk Template
Shared Alim Talk templates are templates created, reviewed, and published directly by Kakao. They can be used by all businesses in common and are not tied to a specific sender profile. Since Kakao's review is already complete, they can be used for sending immediately without a separate review request.

* Automatic Registration
    * When you register a sender profile, shared Alim Talk templates are automatically synchronized and displayed in the console. After that, when new shared templates are published by Kakao, they are automatically synchronized periodically.
    * Shared Alim Talk templates are automatically classified under the **Kakao** category. Since this category is created and managed by the system, users cannot edit or delete it directly.
* Usage Restrictions
    * Shared Alim Talk templates are managed by Kakao and cannot be edited or deleted in the console.
    * Shared Alim Talk templates cannot be moved to a general category, and general templates cannot be moved to the **Kakao** category.
* Sending
    * Since shared Alim Talk templates are not tied to a specific sender profile, you must select the sender profile to use when sending.
    * At least one active sender profile must be registered.
    * Since the review is already complete, you can send messages immediately without waiting for review.