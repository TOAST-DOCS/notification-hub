<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>AlimTalk, FriendTalk</h1> 

**Notification > Notification Hub > Usage Policy and Preset Guide > AlimTalk, FriendTalk**

## Create Sender Profile
In accordance with the Kakao policy, you must first open a business-authentication channel at the KakaoTalk Channel Manager Center to send KakaoTalk Biz messages.

* [Kakao Business Shortcut](https://business.kakao.com/)
* [Kakao Business - Kakao Channel Creation and Business Certification Guide Shortcut](https://kakaobusiness.gitbook.io/main/channel/start)

### Creating Accounts and Channels

Refer to the following topics to create and log in to your account.

* Access Kakao Business, go to the login page and create an account.
* It is recommended to sign up as a corporate representative or by public email. (You can log in to the person in charge's personal KakaoTalk account email, but there are cases where channel transfer is required when the person in charge is absent/resigned.)

Create a channel by referring to the following items.

* The channel name is a name that is exposed on channel home and the channel name and the corporate name on the business registration document are set the same. Names that are not related to the business sector may be reasons for rejection during the screening stage of the ‘business channel’ review.
* Search ID is the ID displayed when searching on KakaoTalk app. Once set, the search ID cannot be changed.
* You can also set up your profile picture after channel registration.

### Set Kakao talk Channel 
After the channel is opened, set up the channel information and apply for the business channel by referring to the items below.

1. Select the channel opened in KakaoTalk Channel Management Center. Set channel disclosure and allow to search to ‘ON.’

2. Request to switch to a business channel. Once all information has been attached/ entered and the application is complete, the transition will be decided through a review. (It will be reviewed by Kakao and will take 2-3 business days.)
    * Business registration card and employment certificate (representative ID card). Documents will be required for submission by industry.
    * Please refer to the personal information masking guide when submitting documents. If masking is omitted, the review will be rejected.
    * In the case of mail order sales, medical device sales, and health functional food sales, a declaration certificate needs to be attached.
    * If the company name and channel name of business information entered are different, please attach additional information for review.


### Register Kakaotalk Channel 
If the business channel conversion has been completed (approved), register the sender profile (Kakao Talk Channel) on the **Notification Hub** >**Sender Information** >**Sender Profile Management** tab. More information about registering Sender Profiles can be found in the ** Console User Guide**>**Sender Information** >**Sender Profile Management**

## Precautions
When using AlimTalk, the customer should inform the receiver of the following precautions for using the service.

* In the process of receiving AlimTalk, data communication charges may be incurred if it is not in a Wi-Fi environment.
* If you do not want to receive AlimTalk, please refer to the following.
  * The sender's contact information (customer center, etc.) should be provided to inform the caller that he/she can unsubscribe.
  * You can block senders by selecting [Block AlimTalk] in top layer of the chat room where the notification talk was received.


## Comparison of AlimTalk and FriendTalk

| Classification    | AlimTalk                                    | FriendTalk                                                                                 |
| ----- |----------------------------------------|-------------------------------------------------------------------------------------|
| Send contents | Able to send informational messages                          | Able to send advertising messages                                                                       |
| Send To | Doesn’t matter if friend or not (needs phone number information)                 | Users who made friends with the KakaoTalk channel (need phone number information)                                                     |
| Send type | Text type<br>Image Type                           | Text type<br>Image Type<br>Wide image type<br>Wide item list type<br>Carousel feed type<br>Premium video type<br>Commerce type<br>Carousel Commerce type |
| Considerations | - Limited to informational Biz messages<br />- Send based on approved templates | - Delivery restricted during night (20:50~08:00 on the following day)                                                        |


<span id="ktb-supported-types"></span>

### FriendTalk Sending support type

|Classification	| Description                                                                                                                                                                                                                                                                                                 | Kakao Image Upload Specification |
|-- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| --|
|Text	| Up to 1,000 characters of text + up to 5 link buttons                                                                                                                                                                                                                                                                        | Not available  |
|Image	| Up to 400 characters of text + 1 image + up to 5 link buttons                                                                                                                                                                                                                                                                 | </li><li> Size Limit- Width 500px or more, Width: Length ratio 2:1 or more and 3:4 or less</li><li>File format and size: JPG, PNG/max 5 MB |
|Wide image	| Up to 76 characters of text + 1 wide image + up to 2 link buttons                                                                                                                                                                                                                                                              | </li><li> Size limit – width 800px, length 600px</li><li>File format and size: JPG, PNG/max 5 MB |
|Wide item list| 	Text + item list image + up to 2 link buttons (horizontally aligned)<br><li>Requires a list of maximum 4 items / minimum 3 items.</li><li>Text phrases are limited to 25 characters for the first item and 30 characters for items 2-4.</li><li>You can only send ads.</li>                                                                                                                                       | </li><li> Upload a minimum of 3 images and a maximum of 4 images to match the number of items in the list.</li><li>Size limits - 400px wide, 400px tall to 800px wide, 400px tall</li><li>Check proportions and horizontal pixels X. Center and crop to fit the thumbnail size</li><li>File format and size: JPG, PNG/up to 5 MB each file |
|Carousel feeds| 	Per 1 carousel: title (header) + text copy + link buttons (2/arranged horizontally) + send image for carousel<li>Requires a list of maximum 10 / minimum 2 carousel.</li><li>The title (header) is limited to 20 characters and the text copy to 180 characters.</li><li>Each carousel can have a maximum of 2 buttons and is sent horizontally aligned.</li><li>You can only send ads.</li>                                                                                         | </li><li>Upload a minimum of 2 images and a maximum of 10 images to match the number of carousel listings. </li><li>Size Limit- Width 500px or more, Width: Length ratio 2:1 or more and 3:4 or less</li><li>File format and size: JPG, PNG/up to 5 MB each file |
|Premium videos| 	Title (header) + text phrase + 1 video uploaded to Kakao TV + up to 1 link button<li>The video link can only be used for videos uploaded to Kakao TV (e.g. https://tv.kakao.com/v/#{숫자} / https://tv.kakao.com/channel/#{숫자}/cliplink/#{숫자}).</li><li>Headers are limited to 20 characters and text to 76 characters.</li><li>The header and text are optional and can be sent without them.</li><li>You can send up to 1 button.</li>                | </li><li>Size Limit- Width 500px or more, Width: Length ratio 2:1 or more and 3:4 or less </li><li>File format and size: JPG, PNG/max 5 MB |
|Commerce| 	Product title+price info+additional info+link buttons (arranged in 2/price) + send commerce-ready image<li>Additional information is limited to 34 characters.</li><li>Buttons must contain a minimum of one button, with a maximum of 2, and are sent horizontally aligned.</li>                                                                                                                                                      | </li><li>Size Limit- Width 500px or more, Width: Length ratio 2:1 or more and 3:4 or less </li><li>File format and size: JPG, PNG/max 5 MB |
|Carousel commerce| 	Per 1 carousel: product title + pricing info + additional info + link buttons (arranged in 2 rows/column) + send image for carousel commerce<br><li>You can send multiple commerce speech bubbles as a carousel.</li><li>If a carousel intro exists, you can send at least 1 carousel and no more than 10 carousels.</li><li>If the carousel intro doesn't exist, then you can send at least 2 carousels and no more than 10 carousels.</li><li>One button is required for each carousel, with a maximum of 2 supported.</li><li>You can only send ads.</li> | </li><li> Upload and use a minimum of 1 image and a maximum of 10 images, depending on the number of carousel intros + carousel lists.</li><li>The entire image must have the same proportions.</li><li>Size Limit- Width 500px or more, Width: Length ratio 2:1 or more and 3:4 or less</li><li>File format and size: JPG, PNG/up to 5 MB each file |

![FriendTalk Sending support type](../../img/friendtalk-img-types.png)
