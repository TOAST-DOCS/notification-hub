<!-- pre-align:aligned sig=42c2280c040e -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>AlimTalk/Brand Messages</h1>

**Notification > Notification Hub > Service Policy and Prerequisites > AlimTalk/Brand Messages**

<a id="create-sender-profile"></a>
## Create Sender Profile { #create-sender-profile }
In accordance with the Kakao policy, you must first open a business-authentication channel at the KakaoTalk Channel Manager Center to send KakaoTalk Biz messages.

* [Kakao Business Shortcut](https://business.kakao.com/)
* [Kakao Business - Kakao Channel Creation and Business Certification Guide Shortcut](https://kakaobusiness.gitbook.io/main/channel/start)

<a id="creating-accounts-and-channels"></a>
### Creating Accounts and Channels { #creating-accounts-and-channels }

Refer to the following topics to create and log in to your account.

* Access Kakao Business, go to the login page and create an account.
* It is recommended to sign up as a corporate representative or by public email. (You can log in to the person in charge's personal KakaoTalk account email, but there are cases where channel transfer is required when the person in charge is absent/resigned.)

Create a channel by referring to the following items.

* The channel name is a name that is exposed on channel home and the channel name and the corporate name on the business registration document are set the same. Names that are not related to the business sector may be reasons for rejection during the screening stage of the ‘business channel’ review.
* Search ID is the ID displayed when searching on KakaoTalk app. Once set, the search ID cannot be changed.
* You can also set up your profile picture after channel registration.

<a id="set-kakao-talk-channel"></a>
### Set Kakao talk Channel { #set-kakao-talk-channel }
After the channel is opened, set up the channel information and apply for the business channel by referring to the items below.

1. Select the channel opened in KakaoTalk Channel Management Center. Set channel disclosure and allow to search to ‘ON.’

2. Request to switch to a business channel. Once all information has been attached/ entered and the application is complete, the transition will be decided through a review. (It will be reviewed by Kakao and will take 2-3 business days.)
    * Business registration card and employment certificate (representative ID card). Documents will be required for submission by industry.
    * Please refer to the personal information masking guide when submitting documents. If masking is omitted, the review will be rejected.
    * In the case of mail order sales, medical device sales, and health functional food sales, a declaration certificate needs to be attached.
    * If the company name and channel name of business information entered are different, please attach additional information for review.


<a id="register-kakaotalk-channel"></a>
### Register Kakaotalk Channel { #register-kakaotalk-channel }
If the business channel conversion has been completed (approved), register the sender profile (Kakao Talk Channel) on the **Notification Hub** >**Sender Information** >**Sender Profile Management** tab. More information about registering Sender Profiles can be found in the ** Console User Guide**>**Sender Information** >**Sender Profile Management**

<a id="precautions"></a>
## Precautions { #precautions }
When using AlimTalk, the customer should inform the receiver of the following precautions for using the service.

* In the process of receiving AlimTalk, data communication charges may be incurred if it is not in a Wi-Fi environment.
* If you do not want to receive AlimTalk, please refer to the following.
  * The sender's contact information (customer center, etc.) should be provided to inform the caller that he/she can unsubscribe.
  * You can block senders by selecting [Block AlimTalk] in top layer of the chat room where the notification talk was received.
# Brand Message

Brand Message is a KakaoTalk Bizmessage product that allows you to send advertising messages to members who have agreed to receive marketing from an advertiser (hereinafter referred to as "marketing consent"), regardless of whether they are KakaoTalk channel friends.

* You can send advertising messages not only to channel friends, but also to non-friends among users who have given marketing consent.
* Brand Message can only be used to send advertising messages.
* Send text and images at a lower cost than LMS/MMS.
* Template sending and free-form sending are supported.
* If a Brand Message fails to send, you can send a text message instead.

<a id="create-a-sender-profile"></a>
## Create a Sender Profile { #create-a-sender-profile }

Brand messages use the same KakaoTalk sender profile as AlimTalk. To create a sender profile, refer to **AlimTalk > Create a Sender Profile** above.

<a id="delivery-targets-and-targeting"></a>
## Delivery Targets and Targeting { #delivery-targets-and-targeting }

Brand messages are divided into customer-targeted delivery and friend-targeted delivery depending on the delivery target type.

<a id="customer-targeted-delivery"></a>
### Customer-Targeted Delivery { #customer-targeted-delivery }

Customer-targeted delivery sends messages to the advertiser's users who have agreed to receive marketing messages. To use customer-targeted delivery, you must complete the **customer-targeted delivery application** in advance. An 080 opt-out number must be registered in the sender profile. The eligible recipients vary depending on the targeting type.

For more information about applying for customer-targeted delivery, see **Console User Guide** > **Sender Information** > **Apply for Customer-Targeted Delivery**.

* **M**: Sends advertising messages to all users who have agreed to receive marketing messages. If the recipient is not a channel friend, the message is sent as a channel message that includes free opt-out information.
* **N**: Sends advertising messages to users who have agreed to receive marketing messages, excluding channel friends.
* **O**: Sends advertising messages to users who have agreed to receive marketing messages and are channel friends.

<a id="customer-targeted-delivery-conditions-for-sending-messages-to-non-friends"></a>
#### Conditions for Sending Messages to Non-Friends

Sending messages to non-friends (targeting M, N) requires that all of the following conditions are met:

* Business-verified channel
* Business registration number registered
* Channel customer service phone number registered
* 50,000 or more channel friends
* A history of successful AlimTalk deliveries within the last 3 months

<a id="friend-targeted-delivery"></a>
### Friend-Targeted Delivery { #friend-targeted-delivery }

Friend-targeted delivery sends messages to all KakaoTalk channel friends. An 080 opt-out number is not required.

<a id="register-080-opt-out-number"></a>
## Register 080 Opt-Out Number { #register-080-opt-out-number }

When sending to customers (Targeting M, N, O), you must register an 080 opt-out number in the sender profile.

* The 080 opt-out number is applied across all sender profiles of other organizations, other projects, and other dealers under the same KakaoTalk channel.
* You can manage opt-out settings for the 080 opt-out number by integrating with the NHN Cloud SMS service.

<a id="nighttime-delivery-restrictions"></a>
## Nighttime Delivery Restrictions { #nighttime-delivery-restrictions }

Brand messages are advertising messages, so their delivery is restricted during nighttime hours according to the Telecommunications Network Act.

* Delivery restricted during night (20:50~08:00 on the following day)
* If delivery is requested during nighttime hours, it is either processed as a failure or resent after the restriction period ends, depending on the detailed settings.

<a id="caution"></a>
## Caution { #caution }

Brand messages are advertising messages, so you must comply with the following requirements:

* Display "(광고)" (ad) at the beginning of any message containing advertising content.
* The sender's name and contact information must be placed above the message body.
* The message must clearly state specific measures and methods that allow recipients to easily opt out or withdraw their consent to receive messages.
* If opting out requires additional steps (such as logging in), this is considered a violation of the law as it makes opting out difficult.
* If business authentication is revoked, permission to send non-friend messages (targeting M, N) will be revoked.
