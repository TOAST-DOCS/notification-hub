<!-- pre-align:aligned sig=e722c2023294 -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Attachments</h1>

**Notification > Notification Hub > Console User Guide > Attachments**

Manage attachments and image layouts.

<span id="attachment-management"></span>

## Attachment Management

You can pre-register and manage attachments to be included when sending messages.

* Click **+ Upload Attachment**.
* In the Upload Attachment popup, select the message channel for which you want to use the attachment.
* Click **Select File** and select a file.
* Click **Save** to upload the file.
* If the file you upload is not compatible with the selected message channel, the upload will fail and the reason for the failure will be displayed.

Attachments have a 7-day retention period, and attachments used in a template are kept until the template is deleted.
You can also manage attachments uploaded when registering templates and sending messages.


<a id="attachment-specifications-by-message-channel"></a>

### Attachment Specifications by Message Channel

| Message Channel | Type | File Format | Max File Size | Resolution | Ratio |
| --- | --- | --- | --- | --- | --- |
| SMS | MMS | .jpg, .jpeg | 300KB | Up to 1000px wide and 1000px tall | |
| RCS | MMS | .jpg, .jpeg, .png, .gif, .bmp | 1MB | | |
| Alim Talk | Image | .jpg, .png | 500KB | At least 500px wide | (2:1) |
| Alim Talk | Item list | .jpg, .png | 500KB | At least 108px wide | (1:1) |
| Brand Message | Image (basic/wide) | .jpg, .png | 5MB | At least 500px wide | (2:1) ~ (3:4) |
| Brand Message | Wide image | .jpg, .png | 5MB | At least 500px wide | (2:1) ~ (1:1) |
| Brand Message | Wide item list (first) | .jpg, .png | 5MB | At least 500px wide | (2:1) |
| Brand Message | Wide item list (others) | .jpg, .png | 5MB | At least 500px wide | (1:1) |
| Brand Message | Carousel feed | .jpg, .png | 5MB | At least 500px wide | (2:1) ~ (3:4) |
| Brand Message | Carousel commerce | .jpg, .png | 5MB | At least 500px wide | (2:1) ~ (3:4) |
| Email | - | All formats except .js, .exe, .bat, .cmd, .com, .cpl, .scr, .vbs, .wsr | 30MB | | |

<a id="image-layout-management"></a>

## Image Layout Management

You can use image layouts to personalize images when sending MMS messages via SMS. An image layout consists of a background image, an image, content, and a barcode. You can use the image layout feature when creating SMS - MMS type templates.

* Click **+ Create Image Layout**.
* Enter a name for the image layout.
* Background Image > Click **Select File** and choose a file to use as the background image.
* Image > Click **Select File** and choose a file to use as the image.
* Enter the content to be displayed on the image. The content is divided into a highlighted phrase and detailed content. You can use template variables in the content. Template variables entered in the image layout are replaced with the template variables entered in the sending request to generate the image.

| Type | File Format | Resolution |
| - | - | - |
| Background Image | .jpg, .jpeg | Width 500px, Height 663px |
| Image | .jpg, .jpeg | Width 430px, Height 274px |

