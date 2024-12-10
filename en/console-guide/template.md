<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Template</h1>

**Notification > Notification Hub > Console User Guide > Template**


<span id="template"></span>

## Template

You can save frequently used messages or messages that require a certain format as a template and set up the saved template to send messages when you send them. For example, if you template frequently used messages, such as customer support, notice items, notifications, or marketing messages, you only need to modify and send parts of the information without having to write the same thing each time.

### Category
* First, select a root category and click **+ Add Category** to create a category.
* The categories are created under the selected categories.

### Template
1. Select the category to which the template belongs and click **+ Register Template**. Go to the Create Template page and display additional settings for the selected message channel.
2. Finish the settings required by the subject and content and each message channel and click **Register**.

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

#### AlimTalk Template button
* You can register **up to 5 buttons** on a template.
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

#### Template inspection
The inspection and review of AlimTalk template will be conducted directly by Kakao, and will be processed sequentially within 2 business days after the inspection request.

* Register a template inquiry
    * If you have an opinion to convey to the Kakao inspection officer before requesting an inspection, enter the information in the Enquiry Registration box. You cannot inquire about templates in the Request/Approval status. (Only templates in the **Inquiry/Return** status can be registered.)
    * Enquiries registered will be added to the inspection results, which will be confirmed by the Kakao inspection representative.
    * Inquiries about the purpose of the template and reasons for return will be added to the inspection results.
    * If you reject the template, you can re-examine it by clicking **Register** and **Modify**.

#### Template status
* When registering a template, it is updated in the order of **Request > Under Inspection > Approval/Return** status.
* After registering the template, it will remain the same for 1 year or transition to **Idle** state if there are no additional deliveries. See the relevant guide at [AlimTalk Template Notes](https://docs.nhncloud.com/ko/Notification/KakaoTalk%20Bizmessage/ko/alimtalk-overview/#_3).

#### Modify Templates
* You can modify only templates in ** Approval/Return ** state.
* When re-inspection is complete after modifying the approved template, the existing template contents will be replaced with the modified one.
* Sender profiles/groups and template codes cannot be modified.
* Modified templates will be inspected again from ** Under Inspection** status.

#### Delete Templates
* You can delete only templates with Request/Return status.
* The returned template can be re-registered after **Delete**.
* Deleted template code can be reused.