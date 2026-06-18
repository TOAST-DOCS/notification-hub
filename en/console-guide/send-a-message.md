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

To send a flow message, you must have a registered flow.


1. Select a flow.
2. Set the recipients. You can set recipients by direct input, selecting from an address book, or uploading a file.
    * If you use direct input or select from an address book, enter the template placeholders together when setting recipients.
    * If you use file upload, enter the recipient information and template placeholders in the file.
    * Recipient settings are covered in detail below.
3. Set the statistics key.
4. Set the sending time. For scheduled sending, set the date and time of delivery.
    * The scheduled sending time can be set up to 30 days from the time of sending.
5. Click **Send** to send the message.

You can use the **Copy Input Values (JSON)** button to copy the sending settings in JSON format.


<a id="send-individual-message-channels"></a>

## Send via Individual Message Channel

1. Choose whether to use a template. If you are using a template, select one.
    * For Alim Talk, select a sender profile and then select a template registered to that sender profile.
2. Set up recipients. You can set up recipients by entering them directly, selecting from an address book, or uploading a file.
    * When entering directly or selecting from an address book, enter template placeholders together when setting up recipients.
    * When uploading a file, recipient information and template placeholders must be entered in the file.
    * Recipient setup is covered in detail below.
3. If you are not using a template, write the message subject and content.
    * How to write subjects and content for each message channel is covered in detail below.
4. Set the send time. For scheduled sending, set the date and time to send.
    * The scheduled send time can be set up to a maximum of 30 days from the current time.
5. Click **Send** to send the message.

You can use the **Copy Input Values (JSON)** button to copy the send settings in JSON format.

<a id="how-to-set-up-receivers"></a>

### How to Set Up Recipients

<a id="select-receivers-from-direct-receiver-input-and-address-book"></a>

#### Enter Recipients Directly and Select Recipients from Address Book

* For flow sending, all contact information for the message channels configured in the flow must be filled in before sending.
* For direct entry in flow sending, enter all contact information for the recipients for each message channel configured in the flow.
* For selecting recipients from the address book in flow sending, only recipients with all contact information set for the message channels configured in the flow can be selected.
* For individual message channel sending, enter the contact information corresponding to the message channel.
* For push tokens, enter the push type and the token generated on the device.

<a id="upload-file"></a>

#### Upload File

* Download the template for the recipient contact list file.
* Each row represents a recipient, and each column represents the recipient's contact information.
* The push token column is a JSON object consisting of a contact type and a token. Up to 6 entries can be entered per recipient.

The template structure of the recipient contact list file is as follows:

| contactPhoneNumber | contactEmailAddress | contactTokenJson1..6 |
| - | - | - |
| Recipient's mobile phone number | Recipient's email address | {"contactType": "contact_type", "token": "push_token" } |

<a id="how-to-write-a-message-title-and-content"></a>

### How to Write a Message Subject and Content

<a id="sms"></a>

#### SMS
* Select a sender number and message purpose. If the message purpose is advertising, select an 080 opt-out number.
* Select the send type. Send types include SMS (short message), LMS (long message), and MMS (media long message).
* The character set that can be entered for SMS, LMS, and MMS is EUC-KR.
    * [Wikipedia EUC-KR](https://ko.wikipedia.org/wiki/EUC-KR)
* SMS supports up to 90 bytes — up to 45 Korean characters or 90 English characters.
* LMS and MMS support up to 2,000 bytes — up to 1,000 Korean characters or 2,000 English characters.
* MMS supports image attachments.
* If message delivery fails due to a blocked sender number, check the phone scam text blocking service.
    * [Phone Scam Text Blocking Service Guide](../service-policy-and-precondition/sms#about-phone-scam-blocking-services)
* If the delivery result is successful but the message is not received, check the carrier spam blocking service.
    * [Carrier Spam Text Blocking Service Guide](../service-policy-and-precondition/sms#about-carrier-spam-text-blocking-services)
* For authentication SMS messages, an authentication phrase must be included.
      * Authentication phrases: auth, password, verif, にんしょう, 認証, 비밀번호, 인증

##### MMS Attachable Image Specifications

* Maximum MMS size: files of 1000×1000 or smaller
* Supported MMS specifications: 300 KB or less per image; if 3 images are attached, the combined total must be 800 KB or less. Supported formats: .jpg, .jpeg


<a id="international-sms"></a>

#### International SMS
International SMS is sent as a Concatenated Message depending on the encoding and number of characters.

* A Concatenated message is a service that makes a message appear as one long text on the device — similar to LMS in Korea — to overcome the character limit for international SMS sending.
  The Concatenated message feature is available or restricted depending on the number of characters in the body, the encoding, and the support of the recipient's mobile carrier.
* If Concatenated message is not supported, the device may receive multiple short messages.
* A header added during the process of creating a Concatenated message occupies space in the message body (approximately 6 bytes) for message linking, which reduces the number of characters that can be entered.
* Charges are based on the number of Concatenated message segments.

| Encoding | 1 segment | 2 segments | 3 segments | 4 segments | 5 segments |
| --- | --- | --- | --- | --- | --- |
| UCS-2<br>(Unicode) | 70 characters | 134 characters<br>(=67×2) | 201 characters<br>(=67×3) | 268 characters<br>(=67×4) | 335 characters<br>(=67×5) |
| GSM-7bit | 160 characters | 306 characters<br>(=153×2) | 459 characters<br>(=153×3) | 612 characters<br>(=153×4) | 765 characters<br>(=153×5) |


<a id="rcs"></a>

#### RCS

1. Select a sender brand and chat room (sender number).
2. Select the message purpose. If the purpose is advertising, select an 080 opt-out number.
3. Select the send type. To use an RCS Biz Center template, set Template to **Use**. Otherwise, only SMS, LMS, and MMS can be selected.
    * SMS supports up to 100 Korean or English characters and allows 1 button to be configured.
    * For authentication SMS messages, an authentication phrase must be included.
      * Authentication phrases: auth, password, verif, にんしょう, 認証, 비밀번호, 인증
    * Buttons cannot be added to authentication SMS messages.
    * LMS Standard allows up to 30 characters for the body title and up to 1,300 characters for the body content, regardless of whether Korean or English, and up to 3 buttons can be configured.
    * For LMS Format type — Default and Title Emphasis — the main title supports up to 17 characters, the body title up to 30 characters, the body content up to 1,300 characters, and up to 2 buttons can be configured.
    * For LMS Format type — Paragraph — the main title supports up to 17 characters, the body title up to 30 characters, the body content up to 1,300 characters, and up to 2 buttons can be configured within the body.
        * Additionally, up to 3 body sections can be added, and the combined total of all body titles and body content must not exceed 1,300 characters.
    * MMS allows up to 30 characters for the title and up to 1,300 characters for the content per card, regardless of Korean or English, along with 1 image and up to 2 buttons per card.
        * For MMS, you can choose between horizontal, vertical, and slide layouts in the detailed settings.
        * When the slide layout is selected, a minimum of 3 and a maximum of 6 slides can be added.
    * When a free template is selected from the RCS Biz Center template, up to 90 characters can be entered for the message.
    * RCS Biz Center templates require pre-registration in RCS Biz Center.
    * When sending integrated message types for advertising purposes, the message must include the "(Advertisement)" phrase and an opt-out phrase.
        * For integrated SMS cards, since there is no title, the "(Advertisement)" phrase must be included at the beginning of the body, and the opt-out phrase along with the 080 number must be included at the end of the body.
        * For integrated LMS cards and integrated MMS cards, the "(Advertisement)" phrase must be included at the beginning of the title, and the opt-out phrase along with the 080 number must be included at the end of the body.

!!! danger "Caution"
    * If a Copy button is included in integrated message types (integrated SMS card, integrated LMS card, integrated MMS card), the message cannot be received on iOS devices.
    * If a GIF image is attached to an integrated MMS card, the message cannot be received on iOS devices.

##### RCS Group ID
* Message statistics can be viewed in RCS Biz Center only for messages that have a group ID added.
* We recommend that you set a group ID for each message that you want to analyze.
* Data is aggregated for 4 days (D+3) from the send date of the same group ID.
* Aggregation is performed only when the number of successfully sent messages with the same group ID and the same message format is approximately 500 (with at least 100 successful sends per mobile carrier).
* You can search within a maximum of 31 days within the last 1 year and 6 months. When searching, make sure to include the campaign send start date in your query.
* Duplicate button clicks by the same customer within a single day are excluded.

##### RCS Button Types
* Open Chat Room
    * Sends the configured message to the configured phone number.
    * Enter the button name, then enter the phone number to which the message will be sent.
    * Enter the content of the message to be sent.
* Copy
    * Copies the configured value.
    * Enter the button name, then enter the value to be copied when the button is clicked.
* Make a Call
    * Makes a call to the configured phone number.
    * Enter the button name, then enter the phone number to call when the button is clicked.
* Show Map / Search Map
    * Displays the configured location in a map app.
    * Enter the button name, then enter the latitude and longitude of the location.
    * Enter the location name and map URL. (URL must include <span>https://</span>)
* Share Current Location
    * The recipient sends their current location to the sender as a message.
    * Enter the button name.
* Open URL
    * Opens a web link.
    * Enter the button name, then enter the link to open when the button is clicked.
    * When entering a link, `http://` or `https://` must be included.
* Add to Calendar
    * Adds an event to the recipient's calendar app.
    * Enter the button name, then select the event start date and end date.
    * Enter the event title and event content.


<a id="alimtalk"></a>

#### Alim Talk

* Select a sender profile and a template registered to that sender profile.
* Alim Talk only supports template sending, so no content input is required.
* Even when sending a shared Alim Talk template, a sender profile must be selected. Since a shared Alim Talk template is not tied to a specific sender profile, it is sent using the selected sender profile.

<a id="brand-message"></a>

#### Brand Message

Brand messages can only be sent as advertising messages.

1. Select a sender profile.
2. Choose whether to use a template.
    * If you are using a template, select a template registered to the sender profile.
    * If you are not using a template, select a message type and write the content.
3. Choose whether to use push notifications.
    * If you select **Do Not Use** for push notifications, message push notifications will not be sent.
4. If you are not using a template, select a message type.
    * **Text**: Up to 1,300 characters of text (Korean/English, including spaces) + up to 5 link buttons (vertical layout)
    * **Image**: Up to 1,300 characters of text (Korean/English, including spaces) + 1 image + up to 5 link buttons (vertical layout)
    * **Wide Image**: Up to 76 characters of text (Korean/English, including spaces) + 1 image + up to 2 link buttons
    * **Wide Item List**: 1 title with 3–4 list items (image + item) + up to 2 link buttons (horizontal layout). First item title: 25 characters; 2nd–4th item titles: 30 characters.
    * **Carousel Feed**: Up to 6 items, each consisting of a 20-character title text + 180-character body text + image + 2 link buttons (horizontal layout)
    * **Premium Video**: A video uploaded to Kakao TV + 20-character header text + 76-character body text + 1 link button
    * **Commerce**: A type that emphasizes product price and discount information. 20-character title text + 34-character supplementary information text + up to 2 link buttons (horizontal layout)
    * **Carousel Commerce**: A type that presents product information in a catalog format. Up to 6 items, each consisting of a 30-character title text + 34-character supplementary information text + up to 2 link buttons (horizontal layout). All images must have the same aspect ratio.
5. If the message includes images, select an image. You must register the image before attaching it.
6. You can insert buttons.
7. Select the target recipient type.
    * **Send to Customers**: Sends to users who have agreed to receive marketing messages from the advertiser. Registering an 080 opt-out number is required.
    * **Send to Friends**: Sends to all KakaoTalk channel friends.
8. For sending to customers, select the targeting type.
    * **M**: Sends advertising messages to all users who have agreed to receive marketing messages.
    * **N**: Sends advertising messages to users who have agreed to receive marketing messages, excluding channel friends.
    * **O**: Sends advertising messages to channel friends among users who have agreed to receive marketing messages.
9. For sending to customers, configure the 080 opt-out number.
    * You can use the 080 opt-out number configured in the sender profile or enter one manually.
10. Choose whether to configure a fallback message.
    * If a brand message fails to send, it can be sent as a text message instead.
11. Add recipients.
12. Click **Send** to send the message.

##### Brand Message Button Types

| Button Type | Description |
| --- | --- |
| Web Link | Navigates to a mobile or PC webpage. |
| App Link | Launches an app using a custom scheme. Set Android and iOS schemes separately. |
| Bot Keyword | The button name is delivered to the agent. |
| Message Delivery | The button name and message body are delivered to the agent. |
| Switch to Consultation | Connects to the consultation chat. |
| Switch to Bot | Invokes the chatbot. |
| Business Form | Invokes the configured business form. |
| Add Channel | Adds the sending channel. Can only be used in the last button position. |

<a id="email"></a>

#### Email

1. Select the message purpose.
    * If you select advertising as the message purpose, additional input is required.
        * The "(Advertisement)" phrase must be included at the beginning of the subject.
        * The body must display the sender's name, email address, phone number, and address.
        * An opt-out link in both Korean and English must be included, and a technical measure that allows recipients to opt out must be in place.
        * Users registered as opted out will not receive advertising emails.
        * When you select advertising as the message purpose, a notification popup is displayed and you must configure the opt-out guidance text.
2. Enter the sender address. Using the name format allows you to enter both a sender name and an email address.
    * When sending in the format "Sender Name<sender email>", the recipient will see the sender name and email address.
3. Attach files by uploading them directly or selecting previously registered files.
    * Up to 10 files can be attached, and each file must be 30 MB or less.
    * The total size of all attachments cannot exceed 30 MB.
    * You can attach up to 30 MB, but depending on the attachment limit policy of the receiving email system (gmail.com, naver.com, etc.), we recommend attachments that are 10 MB or less, as they may be rejected for exceeding the limit or result in a higher spam flagging rate.


##### Precautions When Sending Advertising Emails

In accordance with the Telecommunications Network Act, the following requirements must be met when sending commercial advertising emails or promotional emails. ([Check related content at the Korea Internet & Security Agency](https://spam.kisa.or.kr/spam/cm/cntnts/cntntsView.do?mi=1061&cntntsId=1086)) <br>


1. Advertising emails must only be sent to recipients who have explicitly consented to receive them. If a dispute arises from a violation of this rule, the responsibility lies with the sender of the advertising email.
2. The "(Advertisement)" phrase must be included at the beginning of the subject.
3. The body must display sender information including the sender's name, email address, phone number, and address.
4. The body must include instructions that allow recipients to easily express their intention to opt out or withdraw their consent.
5. A technical measure must be in place so that recipients can easily opt out or withdraw their consent by clicking [Opt-out] or similar links within the body. In this case, both the instructions and the technical measure must be provided in Korean and English.

```
메일 수신을 원치 않으시면 [수신 거부]를 클릭하세요.
If you do not want to receive it, please click a [Unsubscription].
```

NHN Cloud provides the following technical measures for advertising emails to help you comply with the Telecommunications Network Act.

- Inserts the "(Advertisement)" phrase in the subject.
- Provides an opt-out feature in both Korean and English so that recipients can choose to opt out.
- Does not send advertising emails to email addresses registered as opted out.

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
2. If you select advertising as the message purpose, additional input is required.
    * Enter a representative number in the sending contact.
    * In the opt-out guide, enter how users can opt out of push messages in the app.
        * Example: Opt-out: Settings > Notification Settings
3. Select an input type. If you select JSON as the input type, all content must be entered in JSON format.
4. Choose whether to use HTML styling.
    * Using HTML styling allows HTML to be rendered on Android devices.
    * iPhone (iOS) does not support HTML styling.
    * If you send a message using HTML styling, you must write separate messages for Android and iPhone.
5. You can send push messages in various formats by adding buttons, images, and more.
    * To properly display buttons and images in push messages received on a device, the SDK must be applied to the app.
        * [Android SDK](https://docs.nhncloud.com/ko/nhncloud/ko/nhncloud-sdk/push-android/)
        * [iOS SDK](https://docs.nhncloud.com/ko/nhncloud/ko/nhncloud-sdk/push-ios/)


<a id="button"></a>

#### Button

| Name | Description |
| --- | --- |
| Name | The name of the button |
| Type | The button type: Reply (REPLY), Open App (OPEN_APP), Open URL (OPEN_URL), Dismiss (DISMISS) |
| Send Button Name | If the button type is Reply, you can set the send button name on iOS. |
| Link | The link to navigate to or execute when the button is pressed. Applies when the button type is Open URL. |
| Hint | A description of the button. |

<a id="type-of-buttons"></a>

#### Button Types
- Reply
    - Executes the direct reply feature.
    - When the user taps the send button, the user's input text is delivered to the action listener.
- Open App
    - Launches the app.
    - The full message content is delivered through the action listener. You can implement features such as navigating to a specific page by including information in the message.
- Open URL
    - Executes the URL (https://...) or scheme (scheme://...) entered in the Link field.
    - Entering a URL launches the web browser and loads that URL.
    - Entering a scheme executes the scheme predefined in the app.
- Dismiss
    - Closes the notification.

<a id="media"></a>

#### Media

| Name | Description |
| --- | --- |
| Location | Where the media is located: 'REMOTE' or 'LOCAL' |
| Address | The address where the media is located; can be a URL, URI, etc. |
| Type | You can select from image, GIF, video, or sound. (Android supports images only) |
| Extension | The file extension of the media, such as .png or .avi. |
| Expand | The media expand feature; available on Android only. |

<a id="specify-media-files"></a>

#### Specify Media Files
- External
    - Downloads and uses the media file corresponding to the entered URL.
    - Android
        - To use HTTP on Android Pie or later, you must configure <a href="http://docs.toast.com/ko/TOAST/ko/toast-sdk/push-android/#android-p">network-security-config</a>.
    - iOS
        - To use HTTP on iOS 9 or later, ATS (App Transport Security) must be configured in the Info.plist file.
        - The extension information of the actual media file must be entered in the extension field. (e.g., jpg, png, mp4, wav, ...)
- Internal
    - Uses resources included within the app.
    - Android
        - Files must be added to 'res > drawable' in advance.
        - Since access is through resource identifiers, enter the file name without the extension in 'richMessage.media.source' when composing a message.
        - On Android, file names are used as resource identifiers, so files with the same name cannot be used even if they have different extensions.
          Supported image formats are png, jpg, and gif. (Video and audio media formats are not currently supported.)
    - iOS
        - Resources must be added in advance to the <a href="http://docs.toast.com/ko/TOAST/ko/toast-sdk/push-ios/#notification-service-extension">Notification Service Extension</a> project that creates rich messages.
        - Add the file or directory to the 'NotificationServiceExtension' project in XCode.
        - Verify that the file has been added correctly under 'Build Phases > TARGETS'.
        - Since access is through bundle resources, the full file name including the extension is required.
        - When composing a message, enter the added file name in 'richMessage.media.source'.

<a id="media-type"></a>

#### Media Types
- Image

| | Android | iOS |
| - | - | - |
| Supported formats | JPEG, PNG, GIF | JPEG, PNG, GIF |
| GIF animation | Not supported | Supported |
| File size | No limit | 10 MB |
| Recommendations | Landscape image with a 2:1 ratio recommended<br>Small: 512×256<br>Medium: 1024×512<br>Large: 2048×1024 | Landscape image recommended<br>Maximum size: 1038×1038 |

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

#### Large Icon
This feature is available on Android only. It specifies a large icon for the notification. The method for specifying the file is the same as for specifying media files.

| Name | Description |
| --- | --- |
| Location | Where it is located: 'REMOTE' or 'LOCAL' |
| Address | The address where the image is located; can be a URL, URI, etc. |

<a id="groups"></a>

#### Groups
This feature is available on Android only. It sets a group for notifications, and notifications with the same group key are displayed together.

| Name | Description |
| --- | --- |
| Key | The group key |
| Description | A description of the group |

<a id="notification-sound"></a>

#### Notification Sound
| | Android | iOS |
| - | - | - |
| Supported formats | MP3, PCM/WAVE, Vorbis | Linear PCM, MP4 (IMA/ADPCM), μ-law, aLaw |
| Extension | .mp3, .wav, .ogg | .aiff, .wav, .caf |
| Play duration | No limit | 30 seconds |

- Only resources included within the app can be specified. (External URLs are not supported.)
- Android
    - Resources must be added to the 'res > raw' folder in advance.
    - Since access is through resource identifiers, file extensions are ignored.
    - Works only on Android versions below Oreo.
- iOS
    - Resources must be added in advance as bundle resources in the app project.
    - Since access is through bundle resources, the full file name including the extension is required.