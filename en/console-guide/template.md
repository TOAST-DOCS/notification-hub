<!-- pre-align:aligned sig=671bfe2d761c -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Template</h1>

**Notification > Notification Hub > Console User Guide > Template**


<span id="template"></span>

<a id="template-2"></a>

## Template

You can save frequently used messages or messages that require a certain format as a template and set up the saved template to send messages when you send them. For example, if you template frequently used messages, such as customer support, notice items, notifications, or marketing messages, you only need to modify and send parts of the information without having to write the same thing each time.

<a id="category"></a>

### Category
* First, select a root category and click **+ Add Category** to create a category.
* The categories are created under the selected categories.

<a id="template"></a>

### Template
1. Select the category to which the template belongs and click **+ Register Template**. Go to the Create Template page and display additional settings for the selected message channel.
2. Finish the settings required by the subject and content and each message channel and click **Register**.

<a id="alimtalk-template"></a>

#### AlimTalk Template

AlimTalk template can be used only after receiving approval from Kakao's inspection after requesting registration.

* Registrable message types include Channel Add type, Basic type, Additional information type, and Complex type.
* Registrable highlights types include Highlight type, Image type and Item list type .
* Choose the type you want to create a template.

* Kakao AlimTalk Guide
    * [[ AlimTalk Creation Guide]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/content-guide), [[ AlimTalk Review Guide]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit), [[ AlimTalk Whitelist]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit/white-list), [[ AlimTalk Blacklist]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit/black-list)
* Sender profile/group
    * Select sender profile or sender profile group to which you want to register the template. If you register for a group, the template is available to all sender profiles in the group.
    * If the same template code exists in the sender profile/group, the template registered in the sender profile is sent first.
    * For sender profile groups,  ‘Channel add type‘ or  'complex type’ message types cannot be registered as templates.
* Template Code / Template Name
    * You cannot duplicate the same template code and template name in one outgoing profile/group.
* Template Content
    * AlimTalk can be written up to 1,000 characters, including variables, URLs, spaces, and button names, regardless of Korean or English. If you register by entering variables, consider the contents to be replaced and create a template.<br/> See [AlimTalk Template Notes](https://docs.nhncloud.com/ko/Notification/KakaoTalk%20Bizmessage/ko/alimtalk-overview/#_3) for a detailed guide on the number of characters.
    * Create a variable in the form of #{variable}. (Example: #{HongGildong}'s package will be delivered today (#{09:50})
    * When registering a button, the button name cannot be entered as a variable, and the button url can be entered as a variable. (Example http://kakao.com/#{변수})
    * When registering a button url, url_mobile, url_pc links must include 'http://' and 'https://'가 and the 'scheme_ios, 'scheme_android links must be registered according to the scheme type. Otherwise, template registration will not be possible.
* Whether it is a security template
    * When securing the template, the message content is not exposed on devices other than mobile (expose the phrase 'Please check on mobile')
    * In the case of general messages, the setting values may change during inspection, and be sure to check the security of OTP, authentication number, password, and credit information/grade change guide template.

<a id="alimtalk-template-button"></a>

#### AlimTalk Template button
* You can register **up to 5 buttons** per template.
* Quick Reply
    * Tracking and plug-in types are not available and other types can be used the same as buttons.
    * You can use up to 10 buttons per template, and the number of buttons is limited to 2 when using a direct connection.

| Button type | Description |
| --- | --- |
| View delivery  | - Go to the View delivery page.<br/> - Check the delivery company that supports invoice number pattern and tracking button. [[AlimTalk Tracking Invoice Number Pattern Guide]](https://www.nhncloud.com/kr/support/notice/detail/1455)|
| Web link | - Go to your mobile or PC webpage.<br/> - You can set URL links as variables. |
| App link | - Run the app with a custom scheme.<br/> - You must set up custom schemes to run on Android and iOS respectively. |
| Bot Keyword | - The name of the button is forwarded to consultation agent.<br/> - If a channel that does not support consultation talk adds the corresponding button, AlimTalk cannot be sent. |
| Message forwarding | - The name of the button, the body of the message, is forwarded to consultation agent.<br/> - If a channel that does not support consultation talk adds the corresponding button, AlimTalk cannot be sent. |
| Switch to a consultation talk | -Connect to consultation talk<br/> - If a channel that does not support consultation talk adds the corresponding button, AlimTalk cannot be sent. |
| Switching to Bot | -Chatbot is called<br/> - If a channel that does not support consultation talk adds the corresponding button, AlimTalk cannot be sent. |
| Add channel | - Add the channel that sent AlimTalk. The exposure location is only available on the first button.<br/> - If a channel is already added, it will not appear to the receiver. |
| Image Secure Transfer Plugin | - If image contains sensitive information, it encrypts and transfers within the chat window.<br/> - You need to create Bizplugin. [[Bizplugin Guide]](https://business.kakao.com/info/talkbizplugin/) |
| Personal Information Use Plug-in | - In the chat window, consent is obtained to collect personal information necessary to provide services without signing up for membership.<br/> - You need to create Bizplugin. [[Bizplugin Guide]](https://business.kakao.com/info/talkbizplugin/) |
| One-Click Payment Plugin | - Users can pay for the product without changing screens within the chat window.<br/> - The payment plug-in does not support registration directly on the platform, so contact [Kakao Customer Center](https://cs.kakao.com/helps?service=127&category=572&locale=ko). | 
| Business Form | - If you created a business form and connected it to the current channel, the business form you set is called when you click the button.<br/> - Business Form Creation is required: [[Business Form Guide]](https://business.kakao.com/info/talkbizform/) |

<a id="template-inspection"></a>

#### Template inspection
The inspection and review of AlimTalk template will be conducted directly by Kakao, and will be processed sequentially within 2 business days after the inspection request.

* Register a template inquiry
    * If you have an opinion to convey to the Kakao inspection officer before requesting an inspection, enter the information in the Enquiry Registration box. You cannot inquire about templates in the Request/Approval status. (Only templates in the **Inquiry/Return** status can be registered.)
    * Enquiries registered will be added to the inspection results, which will be confirmed by the Kakao inspection representative.
    * Inquiries about the purpose of the template and reasons for return will be added to the inspection results.
    * If you reject the template, you can re-examine it by clicking **Register** and **Modify**.

<a id="template-status"></a>

#### Template status
* When registering a template, it is updated in the order of **Request > Under Inspection > Approval/Return** status.
* After registering the template, it will remain the same for 1 year or transition to **Idle** state if there are no additional deliveries. See the relevant guide at [AlimTalk Template Notes](https://docs.nhncloud.com/ko/Notification/KakaoTalk%20Bizmessage/ko/alimtalk-overview/#_3).

<a id="modify-templates"></a>

#### Modify Templates
* You can modify only templates in ** Approval/Return ** state.
* When re-inspection is complete after modifying the approved template, the existing template contents will be replaced with the modified one.
* Sender profiles/groups and template codes cannot be modified.
* Modified templates will be inspected again from ** Under Inspection** status.

<a id="delete-templates"></a>

#### Delete Templates
* You can delete only templates with Request/Return status.
* The returned template can be re-registered after **Delete**.
* Deleted template code can be reused.

<a id="brand-message-templates"></a>

#### Brand message templates
Unlike AlimTalk templates, brand message templates do not go through a review process and can be created, modified, and deleted freely.

* Select a sender profile and register a template.
* Template codes are not entered by users; instead, Kakao assigns a random identifier.
* Select a message type and compose the content.
    * Supported message types: Text, Image, Wide Image, Wide Item List, Carousel Feed, Premium Video, Commerce, Carousel Commerce
* You can register buttons.
    * Supported button types: Web Link, App Link, Bot Keyword, Message Delivery, Bot for Consultation, Bot Transfer, Business Form, Channel Added
* You can register coupons.
* To attach an image, you must register the image first.

<a id="public-alim-talk-templates"></a>

#### Public Alim Talk Templates
Public Alim Talk templates are templates created, reviewed, and published directly by Kakao. All businesses can use them in common, and they are not tied to a specific sender profile. Because they are provided with Kakao's review already complete, you can use them for sending immediately without a separate review request.

* Auto registration
    * When you register a sender profile, public Alim Talk templates are automatically synchronized and displayed in the console. When new public templates are published on Kakao, they are automatically synchronized on a periodic basis.
    * Public Alim Talk templates are automatically classified under the **Kakao** category. Because the system creates and manages this category, you cannot modify or delete it directly.
* Usage restrictions
    * Because public Alim Talk templates are managed by Kakao, you cannot modify or delete them in the console.
    * You cannot move public Alim Talk templates to a regular category, or move regular templates to the **Kakao** category.
* Sending
    * Because public Alim Talk templates are not tied to a specific sender profile, you must manually select the sender profile to use when sending.
    * At least one active sender profile must be registered.
    * Because the review is already complete, you can send immediately without waiting for review.