<!-- pre-align:aligned sig=24efee552792 -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>RCS</h1> 

**Notification > Notification Hub > Usage Policy and Preset Guide > RCS**

<a id="brand-creation-and-registration"></a>

## Brand Creation and Registration

To use the RCS Bizmessage service, you have to register your brand after signing up for the RCS Biz Center. [[Shortcut to the RCS Biz Center](https://www.rcsbizcenter.com/main)]

<a id="create-a-brand"></a>

### Create a Brand
1. In RCS Biz Center, click **Sign up** > **Sign up as Business Representative** to sign up and get approved.
    * A copy of your business license is required when you sign up.
    * RCS manager will approve and it will take 2 business days to process your membership.
2. An RCS brand is a corporate profile. After you create a brand, you request approval.
    * You can find related guides by clicking **Brand Guide**at the top of the Create a brand page.
      * [Brand Opening Guide Shortcut](https://docs.rcsbizcenter.com/useguide/readme/brandopen)
    * RCS manager will approve, which can take about 2 business days for brand creation approval.

<a id="set-up-a-brand-agency"></a>

### Set up a Brand Agency
After completing the RCS brand approval, set the agency to "NHN Cloud".

1. In RCS Biz Center, go to **Business Dashboard > Brand Dashboard > Brand Operations Management**.

2. Click **Add Agency Permissions**, then search for and select "NHN Cloud" in the agency name.

<a id="register-chat-room-sender-number"></a>

### Register Chat Room (sender number)
You can receive and view messages in chats in the Messages app. You can send and view messages on a per-chat basis.

1. Go to **Business Dashboard > Brand Dashboard > Register Chat Room**, and register a chat room with a caller ID.
    * **You can refer to the relevant guide in Chat Room Registration Guide**.
      * [RCS Biz Center - Chat Room Registration Guide Shortcut](https://docs.rcsbizcenter.com/useguide/readme/chatbot#id-1)
    * A certificate of use of communication services issued within the last month is required.
    * RCS business messaging does not support 010 numbers.
    * RCS manager will approve and it will take 2 business days to approve your chatroom.

2. If the chat room registration is complete (approved), brand linkage is possible on **Notification Hub**>**Sender Information**>**Brand Management** tab.

<a id="register-templates"></a>

### Register Templates
Templates are RCS business messages that have pre-registered message content and style for your brand.
To send a template message, you need to register the template in RCS Biz Center. (You do not need to register a separate template for sending with RCS SMS/LMS/MMS messages).

1. Go to **Business Dashboard > Brand Dashboard > Register Template**, and register the template.
    * You can find related guides by clicking **Template Guide**at the top of the Create a brand page.
      * [RCS Biz Center - Template Guide Shortcut](https://docs.rcsbizcenter.com/useguide/readme/msg#id-1)
    * Only text/image templates can be registered. See **Supported delivery types** below.
    * RCS manager will approve and it will take 2 business days to approve your chatroom.

2. If your template registration is complete (approved), you can link it to the NHN Cloud Console in **Notification** > **RCS Bizmessage** > **Manage RCS Bizmessage** > **Brand Management** tab.

<a id="link-branding-in-notification-hub-console"></a>

### Link Branding in Notification Hub Console
Once you have created a brand and set up an agency, registered a chat room (sender number), and registered a template, connect the brand to the console.

The **Notification Hub**>**Sender Information**>**Brand Management** tab enables  linkage if there are any changes after the integration, press **+Brand Interworking** button.

<a id="introduction-to-integrated-rcs"></a>

## Introduction to Integrated RCS

<!-- TODO: translate body -->

<a id="android-rcs-vs-integrated-rcs"></a>

### Android RCS vs Integrated RCS

<!-- TODO: translate body -->

<a id="notes"></a>

### Notes

<!-- TODO: translate body -->

<a id="send-type-that-supports"></a>

## Supported Sending Types
- Sending types marked "O" in the "Unified RCS" column of the table below are unified RCS types that can be received on both Android and iPhone devices. (Sending types marked "X" are Android RCS types that can only be received on Android devices.)

<table class="custom-table" style="text-align: center">
    <tr>
        <td>NO</td>
        <td>Product</td>
        <td>Product Name</td>
        <td>Unified RCS</td>
        <td>Card Type</td>
        <td>No. of Cards</td>
        <td>Max. Message Length</td>
        <td>Max. Buttons per Card</td>
        <td>Max. Button Name Length</td>
        <td>Image</td>
    </tr>
    <tr>
        <td>1</td>
        <td rowspan="2">SMS</td>
        <td>SMS</td>
        <td>X</td>
        <td>Standalone</td>
        <td>1</td>
        <td>100 characters</td>
        <td>1</td>
        <td>17 characters</td>
        <td rowspan="2">-</td>
    </tr>
    <tr>
        <td>2</td>
        <td>Unified SMS Card</td>
        <td>O</td>
        <td>Standalone</td>
        <td>1</td>
        <td>100 characters</td>
        <td>1</td>
        <td>7 characters</td>
    </tr>
    <tr>
        <td>3</td>
        <td rowspan="5">LMS</td>
        <td>LMS</td>
        <td>X</td>
        <td>Standalone</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>3</td>
        <td>17 characters</td>
        <td rowspan="5">-</td>
    </tr>
    <tr>
        <td>4</td>
        <td>Basic</td>
        <td>X</td>
        <td>Format</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>2</td>
        <td>17 characters</td>
    </tr>
    <tr>
        <td>5</td>
        <td>Title Highlight</td>
        <td>X</td>
        <td>Format</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>2</td>
        <td>17 characters</td>
    </tr>
    <tr>
        <td>6</td>
        <td>Paragraph</td>
        <td>X</td>
        <td>Format</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>2 per paragraph</td>
        <td>7 characters</td>
    </tr>
    <tr>
        <td>7</td>
        <td>Unified LMS Card</td>
        <td>O</td>
        <td>Standalone</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>3</td>
        <td>7 characters</td>
    </tr>
    <tr>
        <td>8</td>
        <td rowspan="6">MMS</td>
        <td>Vertical (Tall)</td>
        <td>X</td>
        <td>Standalone Media Top</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>2</td>
        <td>17 characters</td>
        <td>Tall(568x528)</td>
    </tr>
    <tr>
        <td>9</td>
        <td>Vertical (Medium)</td>
        <td>X</td>
        <td>Standalone Media Top</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>2</td>
        <td>17 characters</td>
        <td>Medium(568x336)</td>
    </tr>
    <tr>
        <td>10</td>
        <td>Slide (Medium)</td>
        <td>X</td>
        <td>Carousel Medium</td>
        <td>2 <br/> to 6</td>
        <td>1,300 characters</td>
        <td>2</td>
        <td>13 characters</td>
        <td>Medium(696x504)</td>
    </tr>
    <tr>
        <td>11</td>
        <td>Slide (Small)</td>
        <td>X</td>
        <td>Carousel Small</td>
        <td>2 <br/> to 6</td>
        <td>1,300 characters</td>
        <td>2</td>
        <td>5 characters</td>
        <td>Short(360x336)</td>
    </tr>
    <tr>
        <td>12</td>
        <td>Unified MMS Card M</td>
        <td>O</td>
        <td>Standalone Media Top</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>2</td>
        <td>7 characters</td>
        <td>Medium(900x504)</td>
    </tr>
    <tr>
        <td>13</td>
        <td>Unified MMS Card T</td>
        <td>O</td>
        <td>Standalone Media Top</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>2</td>
        <td>7 characters</td>
        <td>Tall(900x792)</td>
    </tr>
    <tr>
        <td>14</td>
        <td rowspan="7">Text<br/>Template</td>
        <td>Description Template_Title Select</td>
        <td>X</td>
        <td>Description</td>
        <td>1</td>
        <td>90 characters</td>
        <td>2</td>
        <td>17 characters</td>
        <td rowspan="7">-</td>
    </tr>
    <tr>
        <td>15</td>
        <td>Description Template_Title Free</td>
        <td>X</td>
        <td>Description</td>
        <td>1</td>
        <td>90 characters</td>
        <td>2</td>
        <td>16 characters</td>
    </tr>
    <tr>
        <td>16</td>
        <td>Style Template_Title Select</td>
        <td>X</td>
        <td>Cell</td>
        <td>1</td>
        <td>90 characters</td>
        <td>2</td>
        <td>17 characters</td>
    </tr>
    <tr>
        <td>17</td>
        <td>Style Template_Title Free</td>
        <td>X</td>
        <td>Cell</td>
        <td>1</td>
        <td>90 characters</td>
        <td>2</td>
        <td>16 characters</td>
    </tr>
    <tr>
        <td>18</td>
        <td>Basic Template_Title Free</td>
        <td>X</td>
        <td>Free</td>
        <td>1</td>
        <td>90 characters</td>
        <td>-</td>
        <td>-</td>
    </tr>
    <tr>
        <td>19</td>
        <td>Unified Informational Template</td>
        <td>O</td>
        <td>Description</td>
        <td>1</td>
        <td>90 characters</td>
        <td>2</td>
        <td>7 characters</td>
    </tr>
    <tr>
        <td>20</td>
        <td>Unified Free Template</td>
        <td>O</td>
        <td>Free</td>
        <td>1</td>
        <td>90 characters</td>
        <td>-</td>
        <td>-</td>
    </tr>
    <tr>
        <td>21</td>
        <td rowspan="10">Image<br/>Template</td>
        <td>Image &amp; Title Highlight (3:4)</td>
        <td>X</td>
        <td>Highlighted Image n Title</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16 characters</td>
        <td>Long(900x1200)</td>
    </tr>
    <tr>
        <td>22</td>
        <td>Image &amp; Title Highlight (1:1)</td>
        <td>X</td>
        <td>Highlighted Image n Title</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16 characters</td>
        <td>Square(900x900)</td>
    </tr>
    <tr>
        <td>23</td>
        <td>Image Highlight (3:4)</td>
        <td>X</td>
        <td>Highlighted Image</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16 characters</td>
        <td>Long(900x1200)</td>
    </tr>
    <tr>
        <td>24</td>
        <td>Image Highlight (1:1)</td>
        <td>X</td>
        <td>Highlighted Image</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16 characters</td>
        <td>Square(900x900)</td>
    </tr>
    <tr>
        <td>25</td>
        <td>Thumbnail (Vertical)</td>
        <td>X</td>
        <td>Thumbnail</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16 characters</td>
        <td>Vertical(900x560)</td>
    </tr>
    <tr>
        <td>26</td>
        <td>Thumbnail (Horizontal)</td>
        <td>X</td>
        <td>Thumbnail</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16 characters</td>
        <td>Horizontal(900x560)</td>
    </tr>
    <tr>
        <td>27</td>
        <td>SNS</td>
        <td>X</td>
        <td>SNS</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16 characters</td>
        <td>Square(900x900)</td>
    </tr>
    <tr>
        <td>28</td>
        <td>SNS (Middle Button)</td>
        <td>X</td>
        <td>SNS</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16 characters</td>
        <td>Rectangle(900x560)</td>
    </tr>
    <tr>
        <td>29</td>
        <td>Unified Image Template M</td>
        <td>O</td>
        <td>Standalone Media Top</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>7 characters</td>
        <td>Medium(900x504)</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Unified Image Template T</td>
        <td>O</td>
        <td>Standalone Media Top</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>7 characters</td>
        <td>Tall(900x792)</td>
    </tr>
    <tr>
        <td>31</td>
        <td rowspan="6">LMS<br/>Template</td>
        <td>Statement Type A</td>
        <td>X</td>
        <td>Description</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>2</td>
        <td>17 characters</td>
        <td rowspan="6">-</td>
    </tr>
    <tr>
        <td>32</td>
        <td>Statement Type B</td>
        <td>X</td>
        <td>Description</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>2</td>
        <td>17 characters</td>
    </tr>
    <tr>
        <td>33</td>
        <td>Statement Type C</td>
        <td>X</td>
        <td>Description</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>2</td>
        <td>17 characters</td>
    </tr>
    <tr>
        <td>34</td>
        <td>Basic</td>
        <td>X</td>
        <td>Description</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>2</td>
        <td>17 characters</td>
    </tr>
    <tr>
        <td>35</td>
        <td>Title Highlight</td>
        <td>X</td>
        <td>Description</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>2</td>
        <td>17 characters</td>
    </tr>
    <tr>
        <td>36</td>
        <td>Paragraph</td>
        <td>X</td>
        <td>Description</td>
        <td>1</td>
        <td>1,300 characters</td>
        <td>2 per paragraph</td>
        <td>7 characters</td>
    </tr>
</table>