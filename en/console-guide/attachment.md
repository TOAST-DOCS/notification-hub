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

You can pre-register and manage files to attach when sending messages.

* Click **+ Upload Attachment**.
* In the Upload Attachment pop-up, select the message channel to use the attachment for.
* Click **Select File** and choose a file.
* Click **Save** to upload the file.
* If the uploaded file is not suitable for the selected message channel, the upload will fail and the reason for failure will be displayed.

The retention period for attachments is 7 days. Attachments used in templates are stored until the template is deleted.
You can also manage attachments uploaded when registering templates and sending messages.


### Attachment Specifications by Message Channel

| Message Channel | Type             | File Format                                               | Max File Size | Resolution                           | Ratio                          |
| ----------- | ---------------- | ------------------------------------------------------- | ------------- | -------------------------------- | ----------------------------- |
| SMS         | MMS              | .jpg, .jpeg                                             | 300KB         | Width 1000px, Height 1000px or less    |                               |
| RCS         | MMS              | .jpg, .jpeg, .png, .gif, .bmp                           | 1MB           |                                  |                               |
| Alimtalk      | Image           | .jpg, .png                                              | 500KB         | Width 500px or more                  | (2:1)                         |
| Alimtalk      | Item List    | .jpg, .png                                              | 500KB         | Width 108px or more                  | (1:1)                         |
| Email       | -                | All formats except .js, .exe, .bat, .cmd, .com, .cpl, .scr, .vbs, .wsr | 30MB          |                                  |                               |

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

