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

You can save frequently used messages or messages that require a consistent format as templates, and then use those saved templates when sending messages. For example, you can create templates for frequently used message formats such as customer support, announcements, notifications, or marketing messages. This allows you to send messages by modifying only a few details, without having to write the same content from scratch each time.

<a id="category"></a>

### Category
* First, select the root category, and then click **+ Add Category** to create a category.
* The category is created under the currently selected category.

<a id="template"></a>

### Template
1. Select the category that the template will belong to, and then click **+ Register Template**. The template creation page opens, displaying additional settings for the selected message channel.
2. Complete the title, content, and any settings required by each message channel, and then click **Register**.

<a id="alimtalk-template"></a>

#### Alim Talk Template

Alim Talk templates must receive inspection approval from Kakao after a registration request is submitted before they can be used.

* Available message types include Channel Addition, Basic, Supplementary Information, and Complex.
* Available emphasis types include Highlighted Text, Image, and Item List.
* Select the type you want and create your template.

* Kakao Alim Talk guides
    * [[Alim Talk Creation Guide]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/content-guide), [[Alim Talk Inspection Guide]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit), [[Alim Talk Whitelist]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit/white-list), [[Alim Talk Blacklist]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit/black-list)
* Sender profile/group
    * Select the sender profile or sender profile group to register the template under. If you register under a group, all sender profiles included in the group can use that template.
    * If the same template code already exists in the sender profile/group, the template registered under the sender profile takes priority for sending.
    * For sender profile groups, you cannot register templates using the "Channel Addition" or "Complex" message types.
* Template code/Template name
    * You cannot register duplicate template codes or template names under the same sender profile/group.

* Template content
    * Alim Talk allows up to 1,000 characters regardless of language (Korean or English), including variables, URLs, spaces, and button names. When including variables, take into account the content that will replace them when creating the template.<br/> For detailed character count guidelines, see [Alim Talk Template Notes](https://docs.nhncloud.com/en/Notification/KakaoTalk%20Bizmessage/ko/alimtalk-overview/#_3).
    * Write variables in the format #{variable}. (Example: Your package for #{홍길동} is scheduled for delivery today at (#{09:50}).)
    * When registering buttons, variables cannot be entered in the button name, but variables can be entered in the button URL. (Example: http://kakao.com/#{variable})
    * When registering button URLs, the url_mobile and url_pc links must include 'http://' or 'https://', and scheme_ios and scheme_android links must be registered in the appropriate scheme format. Otherwise, template registration will not be possible.
* Security template
    * When a template is set as secure, the message content is not displayed on devices other than mobile. (The message "Please check on mobile" is shown instead.)
    * For general messages, the security setting may be changed during inspection. Templates for OTP, authentication codes, passwords, and credit information/grade change notifications must have the security option checked.

<a id="alimtalk-template-button"></a>

#### Alim Talk Template Buttons
* You can register up to 5 buttons per template.
* Quick reply
    * Quick reply cannot use tracking shipment and plug-in types, and other types can be used the same as buttons.
    * You can use up to 10 quick replies per template. When quick replies are used, the number of buttons is limited to 2.

| Button type | Description |
| --- | --- |
| Tracking shipment | - Navigates to the courier company's shipment tracking page.<br/> - Check courier companies that support the tracking shipment button and their invoice number patterns. [[Alim Talk Tracking Shipment Invoice Number Pattern Guide]](https://www.nhncloud.com/kr/support/notice/detail/1455)|
| Web link | - Navigates to a mobile or PC web page.<br/> - URL links can be set as variables. |
| App link | - Launches an app using a custom scheme.<br/> - You must set separate custom schemes for Android and iOS. |
| Bot keyword | - The button name is delivered to the counselor.<br/> - If a channel that does not support consultation chat adds this button, Alim Talk sending will not be possible. |
| Message delivery | - The button name and message body are delivered to the counselor.<br/> - If a channel that does not support consultation chat adds this button, Alim Talk sending will not be possible. |
| Bot for Consultation | - Connects to consultation chat.<br/> - If a channel that does not support consultation chat adds this button, Alim Talk sending will not be possible. |
| Bot Transfer | - Invokes the chatbot.<br/> - If a channel that does not support consultation chat adds this button, Alim Talk sending will not be possible. |
| Add channel | - Adds the channel that sent the Alim Talk. This can only be used as the first button position.<br/> - If the channel has already been added, it is not displayed to the recipient. |
| Image secure transmission plugin | - Encrypts and sends images containing sensitive information within the chat window.<br/> - A Biz plugin must be created. [[Biz Plugin Guide]](https://business.kakao.com/info/talkbizplugin/) |
| Personal information use plugin | - Collects consent for personal information required to provide services within the chat window, without requiring membership registration.<br/> - A Biz plugin must be created. [[Biz Plugin Guide]](https://business.kakao.com/info/talkbizplugin/) |
| One-click payment plugin | - Allows users to make payments within the chat window without switching screens.<br/> - The payment plugin does not support direct registration from the platform. Contact the [Kakao Customer Center](https://cs.kakao.com/helps?service=127&category=572&locale=ko) for assistance. |
| Business form | - If a business form has been created and linked to the current channel, clicking the button invokes the configured business form.<br/> - A business form must be created. [[Business Form Guide]](https://business.kakao.com/info/talkbizform/) |

<a id="template-inspection"></a>

#### Template Inspection
Alim Talk template inspection and review are conducted directly by Kakao and are processed sequentially within 2 business days of the inspection request.

* Register a template inquiry
    * If you have comments to pass on to the Kakao inspection reviewer before submitting the inspection request, enter them in the inquiry field. Templates in the Requested/Approved status cannot be submitted for inquiry. (Only templates in **Under Inspection/Rejected** status can submit an inquiry.)
    * The registered inquiry is added to the inspection results and reviewed by the Kakao inspection reviewer.
    * Inquiries about the template's purpose and rejection reasons are added to the inspection results.
    * When a template is rejected, you can click **Register Inquiry** and **Edit** to request re-inspection.

<a id="template-status"></a>

#### Template Status
* When a template is registered, the status updates in the following order: **Requested > Under Inspection > Approved/Rejected**.
* After registration, if a template remains in the same status for one year or has no additional sends, it transitions to **Dormant** status. For related guidelines, see [Alim Talk Template Notes](https://docs.nhncloud.com/en/Notification/KakaoTalk%20Bizmessage/ko/alimtalk-overview/#_3).

<a id="modify-templates"></a>

#### Edit Templates
* Only templates in **Approved/Rejected** status can be edited.
* Once an approved template is edited and inspection is complete, the original template content is replaced with the edited content.
* The sender profile/group and template code cannot be edited.
* An edited template goes back through inspection starting from the **Under Inspection** status.

<a id="delete-templates"></a>

#### Delete Templates
* Only templates in Requested/Rejected status can be deleted.
* Rejected templates can be re-registered after **deletion**.
* Deleted template codes can be reused.

#### Brand Message Template
Unlike Alim Talk templates, brand message templates do not go through an inspection process and can be created, edited, and deleted freely.

* Select a sender profile and register the template.
* Template codes are not registered by the user directly; instead, Kakao assigns a random identifier.
* Select a message type and write the content.
    * Supported message types: Text, Image, Wide Image, Wide Item List, Carousel Feed, Premium Video, Commerce, Carousel Commerce
* You can register buttons.
    * Supported button types: Web link, App link, Bot keyword, Message delivery, Bot for Consultation, Bot Transfer, Business form, Add channel
* You can register coupons.
* To attach an image, you must register the image first.

#### Shared Alim Talk Template
Shared Alim Talk templates are templates that Kakao creates, inspects, and publishes directly. They can be used by all businesses in common and are not tied to a specific sender profile. Because they are provided in a state where Kakao inspection has already been completed, they can be used for sending immediately without a separate inspection request.

* Automatic registration
    * When a sender profile is registered, shared Alim Talk templates are automatically synchronized and displayed in the console. Thereafter, when new shared templates are published by Kakao, they are automatically synchronized periodically.
    * Shared Alim Talk templates are automatically categorized under the **Kakao** category. Because this category is created and managed by the system, users cannot edit or delete it directly.
* Usage restrictions
    * Shared Alim Talk templates are managed by Kakao and cannot be edited or deleted from the console.
    * Shared Alim Talk templates cannot be moved to a general category, and general templates cannot be moved to the **Kakao** category.
* Sending
    * Because shared Alim Talk templates are not tied to a specific sender profile, you must select the sender profile to use when sending.
    * At least one active sender profile must be registered.
    * Because inspection has already been completed, you can send immediately without waiting for inspection.