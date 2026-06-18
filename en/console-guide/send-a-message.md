<!-- pre-align:aligned sig=49c2107da561 -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Send</h1>

**Notification > Notification Hub > Console User Guide > Send **

<span id="message"></span>

!!! danger "Precaution"
The sender information for the message channel must be registered before sending. For more information about sender information, see **Notification** > **Notification Hub** > ** Console User Guide** > **Start** > **Managing sender information**.


<span id="send-flow-message"></span>

## Flow Message Sending

A registered flow is required to send flow messages.


1. Select a flow.
2. Set the recipients. You can set recipients by direct input, selecting from an address book, or uploading a file.
    * For direct input or selecting from an address book, enter the template placeholders along with the recipient information.
    * For file upload, enter the recipient information and template placeholders in the file.
    * Recipient settings are covered in detail below.
3. Set the statistics key.
4. Set the sending time. For scheduled sending, set the delivery date and time.
    * The scheduled sending time can be set up to 30 days from the current time.
5. Click **Send** to send the message.

You can use the **Copy Input Values (JSON)** button to copy the sending settings in JSON format.


<a id="send-individual-message-channels"></a>

## Send Individual Message Channel

1. Select whether to use a template. If you use a template, select the template.
    * For Alim Talk, select a sender profile and choose a template registered to that sender profile.
2. Set up recipients. You can set up recipients by entering them directly, selecting from an address book, or uploading a file.
    * When entering directly or selecting from an address book, enter the template placeholders along with the recipient information.
    * When uploading a file, enter the recipient information and template placeholders in the file.
    * Recipient setup is described in detail below.
3. If you do not use a template, enter the message title and content.
    * How to write titles and content for each message channel is described in detail below.
4. Set the delivery time. For scheduled delivery, set the delivery date and time.
    * The scheduled delivery time can be set to up to 30 days from the time of sending.
5. Click **Send** to send the message.

You can copy the delivery settings in JSON format by using the **Copy Input Values (JSON)** button.

<a id="how-to-set-up-receivers"></a>

### How to Set Up Recipients

<a id="select-receivers-from-direct-receiver-input-and-address-book"></a>

#### Direct Recipient Input and Selecting Recipients from an Address Book

* For flow sending, all contacts for the message channels configured in the flow must be filled in before the message can be sent.
* For direct input in flow sending, enter all contacts of the recipient for each message channel configured in the flow.
* For selecting recipients from an address book in flow sending, you can only select recipients whose contacts are fully configured for all message channels set in the flow.
* For individual message channel sending, enter the contact corresponding to the message channel.
* For push tokens, enter the push type and the token generated on the device.

<a id="upload-file"></a>

#### File Upload

* Download the template for the recipient contact list file.
* Each row represents a recipient, and each column represents the recipient's contact information.
* The push token column is a JSON object consisting of a contact type and a token. You can enter up to 6 tokens per recipient.


The structure of the downloaded template file is as follows:

| contactPhoneNumber | contactEmailAddress | contactTokenJson1..6 | 
| - | - | - | 
| Recipient's phone number | Recipient's email address | {"contactType": "contact_type", "token": "push_token" } |

<a id="how-to-write-a-message-title-and-content"></a>

### How to Write a Message Title and Content

<a id="sms"></a>

#### SMS
* Select the sender number and message purpose. If the message purpose is advertising, select the 080 opt-out number.
* Select the message type. Available message types are SMS (short message), LMS (long message), and MMS (media long message).
* The character set that can be used for SMS, LMS, and MMS is EUC-KR.
    * [Wikipedia EUC-KR](https://ko.wikipedia.org/wiki/EUC-KR)
* SMS supports up to 90 bytes: up to 45 Korean characters or 90 English characters.
* LMS and MMS support up to 2,000 bytes: up to 1,000 Korean characters or 2,000 English characters.
* MMS supports image attachments.
* If message sending fails due to a blocked sender number, check the 'Phone Scam Text Blocking Service'.
    * [Shortcut to Phone Scam Text Blocking Service guide](../service-policy-and-precondition/sms#about-phone-scam-blocking-services)
* If the sending is successful but you do not receive the text, check the 'Carrier Spam Blocking Service'.
    * [Shortcut to Carrier Spam Blocking Service guide](../service-policy-and-precondition/sms#about-carrier-spam-text-blocking-services)
* For authentication SMS messages, an authentication phrase must be included.
      * Authentication phrases: auth, password, verif, にんしょう, 認証, 비밀번호, 인증

##### Image Specifications for MMS Attachments

* MMS maximum size: files up to 1000×1000
* MMS supported specifications: 300 KB or less per image, 800 KB or less total for 3 images. Only .jpg, .jpeg files can be attached


<a id="international-sms"></a>

#### International SMS
International SMS messages are sent as concatenated messages depending on the encoding and number of characters.

* A concatenated message is a service that makes a message appear to be connected as one long text on the device, like an LMS in Korea, to overcome the limitation of the number of characters that can be sent in international SMS sending.
  The concatenated message feature is available or restricted depending on the number of characters in the body, encoding, and support from international mobile carriers.
* If concatenated message is not supported, the device may receive multiple short messages.
* A header added during the concatenation process occupies space in the message body (approximately 6 bytes) for message linking, which reduces the number of characters that can be entered.
* Charges are applied based on the number of concatenated messages.

| Encoding | 1 message charged | 2 messages charged | 3 messages charged | 4 messages charged | 5 messages charged |
| --- | --- | --- | --- | --- | --- |
| UCS-2<br>(Unicode) | 70 characters | 134 characters<br>(=67×2) | 201 characters<br>(=67×3) | 268 characters<br>(=67×4) | 335 characters<br>(=67×5) |
| GSM-7bit | 160 characters | 306 characters<br>(=153×2) | 459 characters<br>(=153×3) | 612 characters<br>(=153×4) | 765 characters<br>(=153×5) |


<a id="rcs"></a>

#### RCS

1. Select the sender brand and chatroom (sender number).
2. Select the message purpose. If the purpose is advertising, select the 080 opt-out number.
3. Select the message type. To use an RCS Biz Center template, set the template option to **Enable**. Otherwise, only SMS, LMS, and MMS can be selected.
    * SMS supports up to 100 Korean or English characters and allows up to 1 button.
    * For authentication SMS messages, an authentication phrase must be included.
      * Authentication phrases: auth, password, verif, にんしょう, 認証, 비밀번호, 인증
    * Buttons cannot be added to authentication SMS messages.
    * LMS Standard type supports up to 30 characters for the body title and up to 1,300 characters for the body content, regardless of Korean or English, and allows up to 3 buttons.
    * For LMS Format type — Default and Title Emphasis formats — the main title supports up to 17 characters, the body title up to 30 characters, and the body content up to 1,300 characters, with up to 2 buttons.
    * For LMS Format type — Paragraph format — the main title supports up to 17 characters, the body title up to 30 characters, and the body content up to 1,300 characters, with up to 2 in-body buttons.
        * In addition, up to 3 body sections can be added, and the combined total of all body titles and body content must not exceed 1,300 characters.
    * MMS supports up to 30 characters for the title and up to 1,300 characters for the content per card, regardless of Korean or English, with 1 image and up to 2 buttons per card.
        * MMS allows you to select horizontal, vertical, or slide layout in the detailed settings.
        * When the slide layout is selected, you can add a minimum of 3 and a maximum of 6 slides.
    * If a free template is selected from the RCS Biz Center template, up to 90 characters can be entered for the message.
    * RCS Biz Center templates must be pre-registered in the RCS Biz Center.
    * When sending a combined message type for advertising purposes, the message must include the "(Ad)" phrase and an opt-out phrase.
        * For the combined SMS card, since there is no title, the "(Ad)" phrase must be included at the beginning of the body, and the opt-out phrase and 080 number must be included at the end of the body.
        * For the combined LMS card and combined MMS card, the "(Ad)" phrase must be included at the beginning of the title, and the opt-out phrase and 080 number must be included at the end of the body.

!!! danger "Caution"
    * If a Copy button is included in a combined message type (combined SMS card, combined LMS card, combined MMS card), it cannot be received on iOS devices.
    * If a GIF image is attached to a combined MMS card, it cannot be received on iOS devices.

##### RCS Group ID
* Message statistics can be viewed in the RCS Biz Center only for messages that have a group ID added.
* We recommend that you set a group ID for each message that you want to analyze.
* Messages with the same group ID are aggregated for 4 days from the sending date (D+3).
* Aggregation applies only when the number of successfully sent messages with the same group ID and the same message format is approximately 500 (at least 100 successful sends per mobile carrier).
* You can search within a period of up to 31 days within the last 18 months. When querying, make sure to include the campaign sending start date in the search range.
* Duplicate button clicks from the same customer within a single day are excluded.

##### RCS Button Types
* Open chatroom
    * Sends a preset message to a preset phone number.
    * Enter the button name and then enter the phone number to send the message to.
    * Enter the content of the message to send.
* Copy
    * Copies the preset value.
    * Enter the button name and then enter the value to be copied when the button is clicked.
* Make a call
    * Makes a call to the preset phone number.
    * Enter the button name and then enter the phone number to call when the button is clicked.
* Show map/Search map
    * Shows the preset location in the maps app.
    * Enter the button name and then enter the latitude and longitude of the location.
    * Enter the location name and map URL. (URL including <span>https://</span>)
* Share current location
    * The recipient sends their current location to the sender as a message.
    * Enter the button name.
* URL link
    * Links to a web page.
    * Enter the button name and then enter the link to connect to when the button is clicked.
    * When entering a link, 'http://' or 'https://' must be included.
* Add to calendar
    * Adds an event to the recipient's calendar app.
    * Enter the button name and then select the event start date and end date.
    * Enter the event title and event details.


<a id="alimtalk"></a>

#### Alim Talk

* Select the sender profile and the template registered under the sender profile.
* Alim Talk supports template sending only, so no content input is required.
* When sending a shared Alim Talk template, you must also select a sender profile. Since shared Alim Talk templates are not tied to a specific sender profile, the message is sent using the selected sender profile.

<a id="brand-message"></a>

#### Brand Message

Brand messages can only be sent for advertising purposes.

1. Select the sender profile.
2. Select whether to use a template.
    * If using a template, select the template registered under the sender profile.
    * If not using a template, select the message type and compose the content.
3. Select whether to use push notifications.
    * If you set push notifications to **Disable**, message push notifications will not be sent.
4. If not using a template, select the message type.
    * **Text**: Up to 1,300 characters of text including spaces, regardless of Korean or English + up to 5 link buttons (vertical layout)
    * **Image**: Up to 1,300 characters of text including spaces, regardless of Korean or English + 1 image + up to 5 link buttons (vertical layout)
    * **Wide image**: Up to 76 characters of text including spaces, regardless of Korean or English + 1 image + up to 2 link buttons
    * **Wide item list**: 1 title with 3–4 list items (image + item) + up to 2 link buttons (horizontal layout). First item title: 25 characters, 2nd–4th item titles: 30 characters.
    * **Carousel feed**: Up to 6 items, each consisting of a 20-character title text + 180-character text + image + 2 link buttons (horizontal layout)
    * **Premium video**: Video uploaded to Kakao TV + 20-character header text + 76-character text + 1 link button
    * **Commerce**: A type that emphasizes product price and discount information. 20-character title text + 34-character additional information text + up to 2 link buttons (horizontal layout)
    * **Carousel commerce**: A type that organizes product information in catalog form. Up to 6 items, each consisting of a 30-character title text + 34-character additional information text + up to 2 link buttons (horizontal layout). All images must have the same aspect ratio.
5. If there is an image, select the image. To attach an image, you must first register the image.
6. You can insert buttons.
7. Select the recipient type.
    * **Send to customers**: Sends to users who have given marketing consent (marketing opt-in) to the advertiser. Registering an 080 opt-out number is required.
    * **Send to friends**: Sends to all KakaoTalk channel friends.
8. If sending to customers, select the targeting type.
    * **M**: Sends advertising messages to all users who have given marketing consent.
    * **N**: Sends advertising messages to users who have given marketing consent, excluding channel friends.
    * **O**: Sends advertising messages to channel friends among users who have given marketing consent.
9. If sending to customers, set the 080 opt-out number.
    * You can use the 080 opt-out number set in the sender profile, or enter one manually.
10. Select whether to configure a fallback message.
    * If a brand message fails to send, it can be sent as a fallback SMS message.
11. Add recipients.
12. Click **Send** to send the message.

##### Brand Message Button Types

| Button Type | Description |
| --- | --- |
| Web link | Navigates to a mobile or PC web page. |
| App link | Launches an app using a custom scheme. Set Android and iOS schemes separately. |
| Bot keyword | The button name is delivered to the agent. |
| Message delivery | The button name and message body are delivered to the agent. |
| Switch to consultation | Connects to the consultation chat. |
| Switch to bot | Invokes the chatbot. |
| Business form | Invokes the configured business form. |
| Add channel | Adds the sending channel. Can only be used in the last button position. |

<a id="email"></a>

#### Email

1. Select the message purpose.
    * If you select advertising as the message purpose, additional input is required.
        * The "(Ad)" phrase must be included at the beginning of the subject line.
        * The sender's name, email address, phone number, and address must be displayed in the body.
        * An opt-out link must be included in both Korean and English, and technical measures to allow opt-out must be implemented.
        * Users who have opted out will not receive advertising emails.
        * When you select advertising as the message purpose, a notification pop-up is displayed and you can configure the opt-out guidance message.
2. Enter the sender address. You can enter both the sender name and email address in name format.
    * When sending in the format "Sender Name<sender email>", the recipient sees the sender's name and email address.
3. Attach files by uploading them directly or by selecting registered files.
    * Up to 10 files can be attached, and each file must be 30 MB or less.
    * The total size of all attachments cannot exceed 30 MB.
    * You can attach up to 30 MB, but depending on the attachment limit policy of the receiving email system (gmail.com, naver.com, etc.), we recommend attachments that are 10 MB or less, as they may be rejected for exceeding the limit or result in a higher spam flagging rate.


##### Notes on Sending Advertising Emails

In accordance with the Telecommunications Network Act, you must comply with the following requirements when sending commercial advertising emails or business promotional emails. ([View related information from KISA](https://spam.kisa.or.kr/spam/cm/cntnts/cntntsView.do?mi=1061&cntntsId=1086)) <br>


1. Advertising emails must only be sent to recipients who have explicitly consented to receive them. If a dispute arises from a violation of this requirement, the responsibility lies with the sender of the advertising email.
2. The "(Ad)" phrase must be included at the beginning of the subject line.
3. The body must display sender information, including the sender's name, email address, phone number, and address.
4. The body must include instructions that allow recipients to easily indicate their intent to opt out or withdraw consent.
5. Technical measures must be implemented to allow recipients to easily opt out or withdraw consent by clicking [Unsubscribe] or similar links in the body. In this case, the instructions and technical measures must be provided in both Korean and English.

```
메일 수신을 원치 않으시면 [수신 거부]를 클릭하세요.
If you do not want to receive it, please click a [Unsubscription].
```

NHN Cloud provides the following technical measures for 'advertising emails' to help you comply with the Telecommunications Network Act.

- Inserts the "(Ad)" phrase in the subject line.
- Provides an opt-out feature in both Korean and English so that recipients can choose to opt out.
- Does not send advertising emails to email addresses that have opted out.

##### Keys Provided as Opt-Out Links

| Key | Phrase | Usage Example |
|-------------------------| - |-------------------------------------------------------------------------------------------------------------------------------|
| BLOCK_RECEIVER_LINK | [수신 거부](#) | 메일 수신을 원치 않으시면 ##BLOCK_RECEIVER_LINK##를 클릭하세요. |
| EN_BLOCK_RECEIVER_LINK | [Unsubscription](#) | If you no longer wish to receive these emails, please click the ##EN_BLOCK_RECEIVER_LINK##. |
| JA_BLOCK_RECEIVER_LINK | [受信拒否](#) | メールの受信を希望しない場合、##JA_BLOCK_RECEIVER_LINK##をクリックしてください。 |
| BLOCK_RECEIVER_LINK_URL | - | If you no longer wish to receive these emails, please `<a href='##BLOCK_RECEIVER_LINK_URL##' target='_blank'>click here</a>`. |


<a id="push"></a>

### Push

1. Select the message purpose.
2. If you select advertising as the message purpose, additional information is required.
    * Enter a representative number for the sending contact.
    * In the opt-out guide, enter the method for opting out of push messages in the app.
        * Example: Opt-out: Settings > Notification Settings
3. Select the input type. If you select JSON as the input type, you must enter the full content in JSON format.
4. Select whether to use HTML style.
    * Using HTML style allows HTML to be rendered on Android devices.
    * iPhone (iOS) does not support HTML style.
    * If you send a message using HTML style, you must write separate messages for Android and iPhone.
5. You can send push messages in various formats by adding buttons, images, and more.
    * To properly display buttons and images in push messages received on a device, the SDK must be integrated into the app.
        * [Go to Android SDK](https://docs.nhncloud.com/ko/nhncloud/ko/nhncloud-sdk/push-android/)
        * [Go to iOS SDK](https://docs.nhncloud.com/ko/nhncloud/ko/nhncloud-sdk/push-ios/)


<a id="button"></a>

#### Button

| Name | Description |
| --- | --- |
| Name | The name of the button |
| Type | The type of the button: Reply (REPLY), Open App (OPEN_APP), Open URL (OPEN_URL), Dismiss (DISMISS) |
| Send button name | If the button type is Reply, you can set the send button name on iOS. |
| Link | The link to navigate to or execute when the button is tapped. Applies when the button type is Open URL. |
| Hint | A description of the button. |

<a id="type-of-buttons"></a>

#### Button types
- Reply
    - Activates the direct reply feature.
    - When the user taps the send button, the user's input text is delivered to the action listener.
- Open App
    - Launches the app.
    - The full message body is delivered through the action listener. You can implement features such as navigating to a specific page by including information in the message.
- Open URL
    - Executes the URL (https://...) or scheme (scheme://...) entered in the Link field.
    - If a URL is entered, a web browser launches and loads the URL.
    - If a scheme is entered, the scheme predefined in the app is executed.
- Dismiss
    - Closes the notification.

<a id="media"></a>

#### Media

| Name | Description |
| --- | --- |
| Location | Where the media is located: 'REMOTE' or 'LOCAL' |
| Address | The address where the media is located. Can be a URL, URI, etc. |
| Type | You can select image, GIF, video, or sound. (Android supports images only.) |
| Extension | The file extension of the media, such as .png or .avi. |
| Expand | Media expand feature. Available on Android only. |

<a id="specify-media-files"></a>

#### Specify media files
- External
    - Downloads and uses the media file at the specified URL.
    - Android
        - To use HTTP on Android Pie or later, you must configure <a href="http://docs.toast.com/ko/TOAST/ko/toast-sdk/push-android/#android-p">network-security-config</a>.
    - iOS
        - To use HTTP on iOS 9 or later, you must configure ATS (app transport security) in the Info.plist file.
        - You must enter the actual media file's extension information in the extension field. (Example: jpg, png, mp4, wav, ...)
- Internal
    - Uses resources included in the app.
    - Android
        - Files must be added to 'res > drawable' in advance.
        - Since resources are accessed by resource identifier, enter the file name without the extension in 'richMessage.media.source' when composing a message.
        - On Android, file names are used as resource identifiers, so you cannot use the same file name even if the extensions are different.
          Supported image formats are PNG, JPG, and GIF. (Video and audio media formats are not currently supported.)
    - iOS
        - Resources must be added in advance to the <a href="http://docs.toast.com/ko/TOAST/ko/toast-sdk/push-ios/#notification-service-extension">Notification Service Extension</a> project that generates rich messages.
        - Add files or directories to the 'NotificationServiceExtension' project in Xcode.
        - Verify that the files have been added correctly under 'Build Phases > TARGETS'.
        - Since resources are accessed through the bundle, the full file name including the extension is required.
        - When composing a message, enter the added file name in 'richMessage.media.source'.

<a id="media-type"></a>

#### Media types
- Image

| | Android | iOS |
| - | - | - |
| Supported formats | JPEG, PNG, GIF | JPEG, PNG, GIF |
| GIF animation | Not supported | Supported |
| File size | No limit | 10 MB |
| Recommendations | Landscape image with a 2:1 ratio recommended<br>Small: 512x256<br>Medium: 1024x512<br>Large: 2048x1024 | Landscape image recommended<br>Maximum size: 1038x1038 |

- Video

| | Android | iOS |
| - | - | - |
| Supported formats | Not supported | MPEG, MPEG3Video, MPEG4, AVIMovie |
| File size | Not supported | 50 MB |

- Sound

| | Android | iOS |
| - | - | - |
| Supported formats | Not supported | WaveAudio, MP3, MPEG4Audio |
| File size | Not supported | 5 MB |

<a id="big-icon"></a>

#### Large icon
This feature is available on Android only. Assigns a large icon to a notification. The method for specifying the file is the same as for specifying media files.

| Name | Description |
| --- | --- |
| Location | Where the icon is located: 'REMOTE' or 'LOCAL' |
| Address | The address where the image is located. Can be a URL, URI, etc. |

<a id="groups"></a>

#### Groups
This feature is available on Android only. Sets a group for a notification, and notifications with the same group key are displayed together.

| Name | Description |
| --- | --- |
| Key | The key of the group |
| Description | A description of the group |

<a id="notification-sound"></a>

#### Notification sound
| | Android | iOS |
| - | - | - |
| Supported formats | MP3, PCM/WAVE, Vorbis | Linear PCM, MP4 (IMA/ADPCM), μ-law, aLaw |
| Extensions | .mp3, .wav, .ogg | .aiff, .wav, .caf |
| Play duration | No limit | 30 seconds |

- Only resources included in the app can be specified. (External URLs are not supported.)
- Android
    - Resources must be added to the 'res > raw' folder in advance.
    - Since resources are accessed by resource identifier, file extensions are ignored.
    - Works only on versions below Android Oreo.
- iOS
    - Resources must be added in advance as bundle resources of the app project.
    - Since resources are accessed through the bundle, the full file name including the extension is required.