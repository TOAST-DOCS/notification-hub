<!-- pre-align:aligned sig=bed054b4a3bb -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>AlimTalk</h1>

**Notification > Notification Hub > Usage Policy and Preset Guide > AlimTalk**

## Create Sender Profile
In accordance with the Kakao policy, you must first open a business-authentication channel at the KakaoTalk Channel Manager Center to send KakaoTalk Biz messages.

* [Kakao Business Shortcut](https://business.kakao.com/)
* [Kakao Business - Kakao Channel Creation and Business Certification Guide Shortcut](https://kakaobusiness.gitbook.io/main/channel/start)

<a id="creating-accounts-and-channels"></a>

### Creating Accounts and Channels

Refer to the following topics to create and log in to your account.

* Access Kakao Business, go to the login page and create an account.
* It is recommended to sign up as a corporate representative or by public email. (You can log in to the person in charge's personal KakaoTalk account email, but there are cases where channel transfer is required when the person in charge is absent/resigned.)

Create a channel by referring to the following items.

* The channel name is a name that is exposed on channel home and the channel name and the corporate name on the business registration document are set the same. Names that are not related to the business sector may be reasons for rejection during the screening stage of the ‘business channel’ review.
* Search ID is the ID displayed when searching on KakaoTalk app. Once set, the search ID cannot be changed.
* You can also set up your profile picture after channel registration.

<a id="set-kakao-talk-channel"></a>

### Set Kakao talk Channel 
After the channel is opened, set up the channel information and apply for the business channel by referring to the items below.

1. Select the channel opened in KakaoTalk Channel Management Center. Set channel disclosure and allow to search to ‘ON.’

2. Request to switch to a business channel. Once all information has been attached/ entered and the application is complete, the transition will be decided through a review. (It will be reviewed by Kakao and will take 2-3 business days.)
    * Business registration card and employment certificate (representative ID card). Documents will be required for submission by industry.
    * Please refer to the personal information masking guide when submitting documents. If masking is omitted, the review will be rejected.
    * In the case of mail order sales, medical device sales, and health functional food sales, a declaration certificate needs to be attached.
    * If the company name and channel name of business information entered are different, please attach additional information for review.


<a id="register-kakaotalk-channel"></a>

### Register Kakaotalk Channel 
If the business channel conversion has been completed (approved), register the sender profile (Kakao Talk Channel) on the **Notification Hub** >**Sender Information** >**Sender Profile Management** tab. More information about registering Sender Profiles can be found in the ** Console User Guide**>**Sender Information** >**Sender Profile Management**

<a id="precautions"></a>

## Precautions
When using Alim Talk, the customer must inform recipients of the following precautions regarding the service.

* If you are not connected to Wi-Fi when receiving Alim Talk, data charges may apply.
* If you do not want to receive Alim Talk, refer to the following:
  * You must inform recipients that they can notify the sender of their opt-out request through the sender's contact information (such as a customer service center).
  * You can block the sender by selecting **Block Alim Talk** from the top layer of the chat room where the Alim Talk was received.

<span id="brand-message"></span>

# Brand Message

Brand Message is a KakaoTalk Bizmessage product that allows advertisers to send advertising messages to members who have agreed to receive marketing (hereinafter referred to as marketing consent), regardless of whether they are KakaoTalk channel friends.

* You can send advertising messages not only to channel friends, but also to non-friends among users who have given marketing consent.
* Brand Message can only be used to send advertising messages.
* Send text and images with attachments at a lower cost than LMS/MMS.
* Both template and free-form sending are supported.
* If a Brand Message fails to send, you can send a text message instead.

## Create a Sender Profile

Brand messages use the same KakaoTalk sender profile as AlimTalk. To create a sender profile, refer to **AlimTalk > Create a Sender Profile** above.

## Delivery Targets and Targeting

Brand messages are divided into customer targeting and friend targeting based on the type of delivery target.

### Customer Targeting

Customer targeting sends messages to users who have agreed to receive marketing messages (마수동 users) from the advertiser. To use customer targeting, you must complete the **Apply for Customer Targeting** process in advance. A free opt-out number (080) must be registered in the sender profile. The available recipients vary depending on the targeting type.

For more information about applying for customer targeting, see **Console User Guide** > **Sender Information** > **Apply for Customer Targeting**.

* **M**: Sends advertising messages to all users who have consented to receive marketing messages. If the recipient is not a channel friend, the message is sent as a channel message that includes free opt-out information.
* **N**: Sends advertising messages to users who have consented to receive marketing messages, excluding channel friends.
* **O**: Sends advertising messages to channel friends among users who have consented to receive marketing messages.

#### Conditions for Sending Messages to Non-Friends

To send messages to non-friends (targeting M, N), all of the following conditions must be met:

* Business-verified channel
* Business registration number registered
* Channel customer service phone number registered
* At least 50,000 channel friends
* A history of successful AlimTalk message delivery within the last 3 months

### Friend Targeting

Friend targeting sends messages to all KakaoTalk channel friends. Registration of a free opt-out number (080) is not required.

## Register 080 Opt-Out Number

When sending to customers (targeting M, N, O), you must register an 080 opt-out number in the sender profile.

* The 080 opt-out number is applied collectively to all sender profiles of other organizations, other projects, and other dealers on the same KakaoTalk channel.
* You can manage opt-out subscriptions for the 080 opt-out number by integrating with the NHN Cloud SMS service.

## Nighttime Delivery Restrictions

Brand messages are advertising messages, so delivery is restricted during nighttime hours in accordance with the Telecommunications Network Act.

* Delivery restricted during night: 20:50~08:00 on the following day
* If delivery is requested during nighttime hours, the message will either fail or be resent after the restriction is lifted, depending on the detailed settings.

## Caution

Brand messages are advertising messages, so you must comply with the following:

* The message must display "(ad)" at the beginning if it contains advertising content.
* The sender's name and contact information must appear above the message body.
* The message must clearly specify the method and procedure by which recipients can opt out or withdraw their consent to receive messages.
* If opting out requires additional steps (such as logging in), this is considered a violation of the law, as it makes opting out unnecessarily difficult.
* If business authentication is revoked, permission to send non-friend messages (targeting M and N) will be revoked as well.
