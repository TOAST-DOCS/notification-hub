<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>RCS</h1> 

**Notification > Notification Hub > Usage Policy and Preset Guide > RCS**

## Brand Creation and Registration

To use the RCS Bizmessage service, you have to register your brand after signing up for the RCS Biz Center. [[Shortcut to the RCS Biz Center](https://www.rcsbizcenter.com/main)]

### Create a Brand
1. In RCS Biz Center, click **Sign up** > **Sign up as Business Representative** to sign up and get approved.
    * A copy of your business license is required when you sign up.
    * RCS manager will approve and it will take 2 business days to process your membership.
2. An RCS brand is a corporate profile. After you create a brand, you request approval.
    * You can find related guides by clicking **Brand Guide**at the top of the Create a brand page.
      * [Brand Opening Guide Shortcut](https://www.rcsbizcenter.com/GuideBrand)
    * RCS manager will approve, which can take about 2 business days for brand creation approval.

### Set up a Brand Agency
After completing the RCS brand approval, set the agency to 'NHN Cloud'.

1. In RCS Biz Center, go to **Business Dashboard > Brand Dashboard > Brand Operations Management**.

2. Click **Add Agency Permissions**, then search for and select "NHN Cloud" in the agency name.

### Register Chat Room (sender number)
You can receive and view messages in chats in the Messages app. You can send and view messages on a per-chat basis.

1. Go to **Business Dashboard > Brand Dashboard > Register Chat Room**, and register a chat room with a caller ID.
    * **You can refer to the relevant guide in Chat Room Registration Guide**.
      * [RCS Biz Center - Chat Room Registration Guide Shortcut](https://www.rcsbizcenter.com/Chatbot#section01)
    * A certificate of use of communication services issued within the last month is required.
    * RCS business messaging does not support 010 numbers.
    * RCS manager will approve and it will take 2 business days to approve your chatroom.

2. If the chat room registration is complete (approved), brand linkage is possible on **Notification Hub**>**Sender Information**>**Brand Management** tab.

### Register Templates
Templates are RCS business messages that have pre-registered message content and style for your brand.
To send a template message, you need to register the template in RCS Biz Center. (You do not need to register a separate template for sending with RCS SMS/LMS/MMS messages).

1. Go to **Business Dashboard > Brand Dashboard > Register Template**, and register the template.
    * You can find related guides by clicking **Template Guide**at the top of the Create a brand page.
      * [RCS Biz Center - Template Guide Shortcut](https://www.rcsbizcenter.com/RcsMessageType#section04)
    * Only text/image templates can be registered. See **Supported delivery types** below.
    * RCS manager will approve and it will take 2 business days to approve your chatroom.

2. If your template registration is complete (approved), you can link it to the NHN Cloud Console in **Notification** > **RCS Bizmessage** > **Manage RCS Bizmessage** > **Brand Management** tab.

### Link Branding in Notification Hub Console
Once you have created a brand and set up an agency, registered a chat room (sender number), and registered a template, connect the brand to the console.

The **Notification Hub**>**Sender Information**>**Brand Management** tab enables  linkage if there are any changes after the integration, press **+Brand Interworking** button.

## Send type that supports

<table class="custom-table" style="text-align: center">
    <tr>
        <td>NO</td>
        <td>Product</td>
        <td>Product name</td>
        <td>Card Type</td>
        <td>Card Count</td>
        <td>Maximum Message Length</td>
        <td>By card</td>
        <td>Button</td>
        <td>Image</td>
    </tr>
    <tr>
        <td>1</td>
        <td>SMS</td>
        <td>SMS</td>
        <td>Standalone</td>
        <td>1</td>
        <td>100</td>
        <td>1</td>
        <td>17</td>
        <td>-</td>
    </tr>
    <tr>
        <td>2</td>
        <td>LMS</td>
        <td>LMS</td>
        <td>Standalone</td>
        <td>1</td>
        <td>1300</td>
        <td>3</td>
        <td>17</td>
        <td>-</td>
    </tr>
    <tr>
        <td>3</td>
        <td rowspan="2">MMS</td>
        <td>Vertical (Tall)</td>
        <td>Standalone Media Top</td>
        <td>1</td>
        <td>1300</td>
        <td>2</td>
        <td>17</td>
        <td>Tall (568x528)</td>
    </tr>
    <tr>
        <td>4</td>
        <td>Vertical (Medium)</td>
        <td>Standalone Media Top</td>
        <td>1</td>
        <td>1300</td>
        <td>2</td>
        <td>17</td>
        <td>Medium(568x336)</td>
    </tr>
    <tr>
        <td>5</td>
        <td rowspan="5">Text<br/>Template</td>
        <td>Description Template_Title Optional</td>
        <td>Description</td>
        <td>1</td>
        <td>90 characters</td>
        <td>2</td>
        <td>17</td>
        <td rowspan="5">-</td>
    </tr>
    <tr>
        <td>6</td>
        <td>Description Template_Title Freeform</td>
        <td>Description</td>
        <td>1</td>
        <td>90 characters</td>
        <td>2</td>
        <td>16</td>
    </tr>
    <tr>
        <td>7</td>
        <td>Style Template_Title Optional</td>
        <td>Cell</td>
        <td>1</td>
        <td>90 characters</td>
        <td>2</td>
        <td>17</td>
    </tr>
    <tr>
        <td>8</td>
        <td>Style Template_Title Freeform</td>
        <td>Cell</td>
        <td>1</td>
        <td>90 characters</td>
        <td>2</td>
        <td>16</td>
    </tr>
    <tr>
        <td>9</td>
        <td>Default Template_Title Freeform</td>
        <td>Free</td>
        <td>1</td>
        <td>90 characters</td>
        <td>0</td>
        <td>0</td>
    </tr>
    <tr>
        <td>10</td>
        <td rowspan="8">Image<br/>Template</td>
        <td>Image &amp; Title Highlighted (3:4)</td>
        <td>Highlighted Image n Title</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16</td>
        <td>Long(900x1200)</td>
    </tr>
    <tr>
        <td>11</td>
        <td>Image &amp; Title Highlighted (1:1)</td>
        <td>Highlighted Image n Title</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16</td>
        <td>Square(900x900)</td>
    </tr>
    <tr>
        <td>12</td>
        <td>Image Highlighted (3:4)</td>
        <td>Highlighted Image</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16</td>
        <td>Long(900x1200)</td>
    </tr>
    <tr>
        <td>13</td>
        <td>Image Highlighted (1:1)</td>
        <td>Highlighted Image</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16</td>
        <td>Square(900x900)</td>
    </tr>
    <tr>
        <td>14</td>
        <td>Thumbnail type(Vertical)</td>
        <td>Thumbnail</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16</td>
        <td>Vertical(900x560)</td>
    </tr>
    <tr>
        <td>15</td>
        <td>Thumbnail type(Horizontal)</td>
        <td>Thumbnail</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16</td>
        <td>Horizontal(900x560)</td>
    </tr>
    <tr>
        <td>16</td>
        <td>Social media</td>
        <td>SNS</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16</td>
        <td>Square(900x900)</td>
    </tr>
    <tr>
        <td>17</td>
        <td>Social (middle button)</td>
        <td>SNS</td>
        <td>1</td>
        <td>500 characters</td>
        <td>2</td>
        <td>16</td>
        <td>Rectangle(900x560)</td>
    </tr>
</table>