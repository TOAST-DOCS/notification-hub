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

You can save frequently used messages or messages that require a consistent format as templates, and then select a saved template when sending a message. For example, if you create templates for messages you frequently send — such as customer support, announcements, notifications, or marketing messages — you can send them by modifying only a few details each time, without having to write the same content from scratch.

<a id="category"></a>

### Category
* First, select the root category and click **+ Add Category** to create a category.
* A category is created under the currently selected category.

<a id="template"></a>

### Template
1. Select the category to which the template belongs and click **+ Register Template**. You will be taken to the template creation page, where additional settings for the selected message channel are displayed.
2. Complete the title, content, and any settings required by each message channel, then click **Register**.

<a id="alimtalk-template"></a>

#### Alim Talk Template

Alim Talk templates must be reviewed and approved by Kakao before they can be used.

* Available message types include Channel Add, Basic, Additional Info, and Mixed.
* Available emphasis types include Text Emphasis, Image, and Item List.
* Select the type you want and create your template.

* Kakao Alim Talk guides
    * [[Alim Talk Creation Guide]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/content-guide), [[Alim Talk Review Guide]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit), [[Alim Talk Whitelist]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit/white-list), [[Alim Talk Blacklist]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit/black-list)
* Sender profile/group
    * Select the sender profile or sender profile group to register the template under. If registered to a group, all sender profiles in the group can use the template.
    * If the same template code exists in the sender profile/group, the template registered to the sender profile takes priority for sending.
    * For sender profile groups, templates cannot be registered using the "Channel Add" or "Mixed" message types.
* Template code/template name
    * You cannot register duplicate template codes or template names under a single sender profile/group.

* Template content
    * Alim Talk templates can contain up to 1,000 characters regardless of language, including variables, URLs, spaces, and button names. When using variables, make sure to account for the replacement content when writing the template.<br/> For detailed character count guidelines, see [Alim Talk Template Notes](https://docs.nhncloud.com/en/Notification/KakaoTalk%20Bizmessage/ko/alimtalk-overview/#_3).
    * Write variables in the format #{variable}. (Example: The package for #{Hong Gildong} is scheduled to be delivered today at (#{09:50}).)
    * When registering buttons, button names cannot contain variables, but button URLs can. (Example: http://kakao.com/#{variable})
    * When registering button URLs, url_mobile and url_pc links must include 'http://' or 'https://', and scheme_ios and scheme_android links must follow the correct scheme format. Otherwise, template registration will fail.
* Security template
    * When security is enabled on a template, the message content is not displayed on devices other than mobile. (The message "Please check on mobile" is shown instead.)
    * For general messages, the security setting may be changed during review. Templates for OTPs, authentication codes, passwords, and credit information/rating change notices must have security enabled.

<a id="alimtalk-template-button"></a>

#### Alim Talk Template Buttons
* You can register up to 5 buttons per template.
* Quick reply
    * Quick reply cannot use tracking shipment and plug-in types, and other types can be used the same as buttons.
    * Up to 10 quick replies can be used per template. When quick replies are used, the number of buttons is limited to 2.

| Button Type | Description |
| --- | --- |
| Tracking Shipment | - Navigates to the courier's shipment tracking page.<br/> - Check the couriers that support the tracking shipment button and their invoice number patterns. [[Alim Talk Tracking Shipment Invoice Number Pattern Guide]](https://www.nhncloud.com/kr/support/notice/detail/1455)|
| Web Link | - Navigates to a mobile or PC web page.<br/> - You can set URL links as variables. |
| App Link | - Launches an app using a custom scheme.<br/> - You must set a separate custom scheme for Android and iOS. |
| Bot Keyword | - The button name is delivered to the agent.<br/> - If a channel that does not support consultation chat adds this button, Alim Talk sending will not be available. |
| Message Delivery | - The button name and message body are delivered to the agent.<br/> - If a channel that does not support consultation chat adds this button, Alim Talk sending will not be available. |
| Bot for Consultation | - Connects to consultation chat.<br/> - If a channel that does not support consultation chat adds this button, Alim Talk sending will not be available. |
| Bot Transfer | - Invokes the chatbot.<br/> - If a channel that does not support consultation chat adds this button, Alim Talk sending will not be available. |
| Add Channel | - Adds the channel that sent the Alim Talk. Can only be placed as the first button.<br/> - If the channel has already been added, it is not displayed to the recipient. |
| Image Secure Transmission Plugin | - Encrypts and transmits images containing sensitive information within the chat window.<br/> - A BizPlugin must be created. [[BizPlugin Guide]](https://business.kakao.com/info/talkbizplugin/) |
| Personal Information Use Plugin | - Collects consent for personal information required to provide the service without membership registration, within the chat window.<br/> - A BizPlugin must be created. [[BizPlugin Guide]](https://business.kakao.com/info/talkbizplugin/) |
| One-Click Payment Plugin | - Allows users to make payments within the chat window without switching screens.<br/> - Direct registration of the payment plugin is not supported on the platform. Please contact [Kakao Customer Center](https://cs.kakao.com/helps?service=127&category=572&locale=ko). |
| Business Form | - If a business form has been created and linked to the current channel, clicking the button will invoke the configured business form.<br/> - A business form must be created. [[Business Form Guide]](https://business.kakao.com/info/talkbizform/) |

<a id="template-inspection"></a>

#### Template Review
Template review and evaluation for Alim Talk is conducted directly by Kakao and is processed sequentially within 2 business days of the review request.

* Registering a template inquiry
    * If you have comments to pass on to the Kakao reviewer before submitting a review request, enter them in the inquiry registration field. Templates in the Requested/Approved status cannot be queried. (Only templates in **Under Review/Rejected** status can have an inquiry registered.)
    * Registered inquiries are added to the review result and checked by the Kakao reviewer.
    * Questions about the template's purpose and rejection reasons are added to the review result.
    * If a template is rejected, you can click **Register Inquiry** and **Edit** to request a re-review.

<a id="template-status"></a>

#### Template Status
* When a template is registered, its status is updated in the following order: **Requested > Under Review > Approved/Rejected**.
* After registration, if a template remains in the same status for one year or has no additional deliveries, it transitions to **Dormant** status. For related guidelines, see [Alim Talk Template Notes](https://docs.nhncloud.com/en/Notification/KakaoTalk%20Bizmessage/ko/alimtalk-overview/#_3).

<a id="modify-templates"></a>

#### Edit Template
* Only templates in **Approved/Rejected** status can be edited.
* When an approved template is edited and review is complete, the existing template content is replaced with the edited content.
* The sender profile/group and template code cannot be edited.
* An edited template restarts the review process from the **Under Review** status.

<a id="delete-templates"></a>

#### Delete Template
* Only templates in Requested/Rejected status can be deleted.
* A rejected template can be re-registered after **deletion**.
* Deleted template codes can be reused.

<a id="brand-message-template"></a>

#### Brand Message Template
Brand message templates, unlike Alim Talk templates, do not require a review process and can be created, edited, and deleted freely.

* Select a sender profile and register a template.
* Template codes are not entered manually by the user; Kakao assigns a random identifier.
* Select a message type and write the content.
    * Supported message types: Text, Image, Wide Image, Wide Item List, Carousel Feed, Premium Video, Commerce, Carousel Commerce
* You can register buttons.
    * Supported button types: Web Link, App Link, Bot Keyword, Message Delivery, Bot for Consultation, Bot Transfer, Business Form, Add Channel
* You can register coupons.
* To attach an image, you must first register the image.

<a id="common-alim-talk-template"></a>

#### Common Alim Talk Template
Common Alim Talk templates are templates created, reviewed, and published directly by Kakao. They can be used by all businesses in common and are not tied to a specific sender profile. Because they are provided in an already-approved state by Kakao, they can be used for sending immediately without a separate review request.

* Automatic registration
    * When you register a sender profile, common Alim Talk templates are automatically synchronized and displayed in the console. Afterward, when new common templates are published by Kakao, they are automatically synchronized on a periodic basis.
    * Common Alim Talk templates are automatically categorized under the **Kakao** category. Because this category is created and managed by the system, users cannot edit or delete it directly.
* Usage restrictions
    * Because common Alim Talk templates are managed by Kakao, they cannot be edited or deleted in the console.
    * Common Alim Talk templates cannot be moved to a general category, and general templates cannot be moved to the **Kakao** category.
* Sending
    * Because common Alim Talk templates are not tied to a specific sender profile, you must manually select the sender profile to use when sending.
    * At least one active sender profile must be registered.
    * Because review is already complete, you can send immediately without waiting for review.