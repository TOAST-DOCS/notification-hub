<!-- pre-align:aligned sig=26433962c314 -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Error Codes</h1>

**Notification > Notification Hub > Error Codes**

<a id="list-of-error-codes"></a>
## List of Error Codes

| Category | Is Successful (isSuccessful) | Result Code (resultCode) | Result Message (resultMessage) |
| --- | --- | --- | --- |
| Common | true | 0 | success |
| Common | false | 400000 | Partial failure |
| Common | false | 400002 | The Friend Talk coupon title is required, and the description must be 18 characters or fewer.<br>The linkMo field of the coupon is required, or the schemeAndroid/schemeIos format is invalid.<br>The Friend Talk template type you entered cannot have a carousel.<br>A carousel cannot be used for general message purposes.<br>The carousel list is required and must contain between 2 and 10 items.<br>The Friend Talk carousel header must be 25 characters or fewer.<br>The Friend Talk carousel message must be 100 characters or fewer.<br>The Friend Talk carousel image is required.<br>Items or headers cannot be used with this template type.<br>Items and headers are required fields.<br>The header must be 25 characters or fewer.<br>The item list size must be between 3 and 4 items.<br>The item title is a required field and must be 30 characters or fewer.<br>The item's linkMo is a required field.<br>Buttons cannot be used with this template type.<br>The number of buttons exceeded the maximum number (up to 5 for regular messages, up to 4 for coupons, up to 2 for wide item list/wide image)<br>The button type is a required field.<br>The button name is a required field.<br>Button names can be up to 14 characters long. They can be up to 9 characters in the wide item list type and up to 8 characters in the carousel type.<br>The button link must be 2,000 characters or fewer.<br>The button's linkPc must include the http or https protocol.<br>The button's linkMo must include the http or https protocol.<br>The WL button type must include the linkMo field.<br>At least 2 of the following fields must be included: linkMo, schemeAndroid, schemeIos<br>The BF button type must include the bizFormKey field.<br>The BF button type must be placed at the top.<br>The BF button type must have a button name of one of the following: Book in Talk, Survey in Talk, Enter in Talk.<br>The linkMo, linkPc, schemeIos, and schemeAndroid fields cannot be used with the MD or BK button type.<br>Images cannot be used with this template type.<br>The image is a required field.<br>templateContent cannot be used with this template type.<br>The length of templateContent is a required field and must be 1,000 characters or fewer.<br>The templateContent length for the image type must be 400 characters or fewer.<br>The templateContent length for the wide image type must be 76 characters or fewer.<br>No more tokens can be added to the recipient.<br>The maximum number of tokens per recipient has been exceeded.<br>The recipient cannot be registered in the group.<br>Invalid email address. {0}<br>Invalid recipient number.<br>The RCS recipient number is empty.<br>The body must include the (Ad) and opt-out phrases.<br>The template parameter is empty.<br>Template parameter {0} is missing.<br>Invalid template.<br>The sender number registration review request (phone authentication) failed. Please check the authentication code.<br>Failed to delete the sender number.<br>The sender number registration review request failed. Please check the phone number or the uploaded documents.<br>The attachment size must not exceed {0} MB.<br>The scheduled time cannot be in the past.<br>The scheduled time must be set within 60 days.<br>There are no recipients.<br>The maximum number of recipients has been exceeded.<br>Authentication emails cannot be sent with attachments.<br>The subject of an advertising email must start with "(광고)", "(AD)", or "(広告)".<br>This is a restricted sending type.<br>The subject length has been exceeded.<br>The body length has been exceeded.<br>The body must include the authentication phrase.<br>The body must include the required advertising phrase.<br>Individual members cannot use this service. |
| Common | false | 400100 | The 'Domain Protection' feature is enabled for this domain. |
| Common | false | 400101 | The template ID is already registered. |
| Common | false | 400102 | Authentication emails do not support sending templates that include attachments. |
| Common | false | 400103 | The template is inactive. |
| Common | false | 400104 | The email is already registered in the opt-out list. |
| Common | false | 400105 | The email is already registered in the opt-out list. |
| Common | false | 400106 | Failed to delete from the opt-out list. |
| Common | false | 400107 | Domain authentication failed. |
| Common | false | 400108 | The domain is already registered. |
| Common | false | 400109 | The domain is not authenticated. |
| Common | false | 400110 | The domain is not a root domain. |
| Common | false | 400111 | The domain is already authenticated. |
| Common | false | 400112 | A subdomain must not be a root domain. |
| Common | false | 400113 | The subdomain is not registered. |
| Common | false | 400114 | The domain is not registered. |
| Common | false | 400115 | DKIM authentication failed. |
| Common | false | 400116 | Failed to share the domain. |
| Common | false | 400117 | Failed to disable DKIM. |
| Common | false | 400118 | Failed to enable DKIM. |
| Common | false | 400119 | The root domain is not authenticated. |
| Common | false | 400120 | The domain is already shared. |
| Common | false | 400121 | The domain is not shared with other organization users. |
| Common | false | 400122 | The DMARC record does not exist. |
| Common | false | 400123 | The SPF record is duplicated. |
| Common | false | 400124 | The SPF record cannot be found because the maximum number of DNS lookups for the SPF record has been exceeded. |
| Common | false | 400125 | The 'all' mechanism in the SPF record is invalid. |
| Common | false | 400126 | The domain is not the root domain of the subdomain. |
| Common | false | 400127 | The domain and subdomain are identical. |
| Common | false | 400128 | DNS lookup failed. |
| Common | false | 400129 | Failed to delete DKIM. |
| Common | false | 400130 | The domain format is invalid. |
| Common | false | 400131 | The subdomain format is invalid. |
| Common | false | 400200 | An error occurred while uploading the attachment. |
| Common | false | 400201 | Failed to create the Excel file. |
| Common | false | 400202 | The attachment ID is already in use. |
| Common | false | 400203 | International sending has been blocked by the service. |
| Common | false | 400204 | The country is blocked by the service. |
| Common | false | 400205 | Blocked by overall metrics. |
| Common | false | 400206 | The recipient number is not included in the whitelist. |
| Common | false | 400207 | The conversion rate is below the threshold. |
| Common | false | 400208 | The template ID is already in use. |
| Common | false | 400209 | The maximum number of registered templates has been reached. |
| Common | false | 400210 | The template has been deleted. |
| Common | false | 400211 | Invalid category. |
| Common | false | 400212 | The top-level category cannot be deleted. |
| Common | false | 400213 | The sender number is already registered. |
| Common | false | 400214 | The review has already been completed. |
| Common | false | 400215 | The review has ended. |
| Common | false | 400216 | This user is already being authenticated. |
| Common | false | 400217 | The sender number is not registered. |
| Common | false | 400218 | This sender number is blocked. |
| Common | false | 400219 | This sender number is invalid. |
| Common | false | 400220 | This sender number is already in use. |
| Common | false | 400300 | Invalid app key. |
| Common | false | 400301 | Invalid secret key. |
| Common | false | 400302 | Invalid SMS app key. |
| Common | false | 400303 | Invalid SMS sender number. |
| Common | false | 400304 | The sender profile is already registered. |
| Common | false | 400305 | The same 'X-NC-API-IDEMPOTENCY-KEY' was used in the last 10 minutes. |
| Common | false | 400306 | The sender profile has no sender key. |
| Common | false | 400307 | The sender profile group already exists. |
| Common | false | 400308 | The sender profile status is not active. |
| Common | false | 400309 | The maximum number of daily message transmissions has been exceeded. |
| Common | false | 400310 | The sender profile group has already been added. |
| Common | false | 400311 | Invalid SMS opt-out number. |
| Common | false | 400312 | Invalid UUID. |
| Common | false | 400313 | The sender profile has not been added to this group. |
| Common | false | 400314 | The maximum group size is 10 members. |
| Common | false | 400315 | The sender group cannot send messages. |
| Common | false | 400316 | The sender group cannot be deleted. |
| Common | false | 400317 | The maximum number of group members is 5,000. |
| Common | false | 400318 | The sender is blocked. |
| Common | false | 400319 | Blacklist values in template parameters cannot exceed 14 characters. |
| Common | false | 400320 | A blacklisted user cannot join the group. |
| Common | false | 400321 | Identity verification is required to use this service. |
| Common | false | 400322 | The length of '{}' must be {} or fewer. |
| Common | false | 400323 | '{}' cannot be empty. |
| Common | false | 400324 | '{}' cannot be null. |
| Common | false | 400325 | '{}' must be {} or greater. |
| Common | false | 400326 | The button parameter is invalid. |
| Common | false | 400327 | Content replaced with template parameters cannot exceed 1,000 characters. |
| Common | false | 400328 | 'content' is too long. |
| Common | false | 400329 | 'content' is too long. |
| Common | false | 400330 | A message cannot be sent with a past date. |
| Common | false | 400331 | A message cannot be sent more than 90 days in the future. |
| Common | false | 400332 | The format of 'requestDate' is invalid. |
| Common | false | 400333 | The requestId is invalid. |
| Common | false | 400334 | 'content' is too long. |
| Common | false | 400335 | Too many buttons when a wide image is requested. |
| Common | false | 400336 | The template title replaced with template parameters cannot exceed 50 characters. |
| Common | false | 400337 | The template item parameter is invalid. |
| Common | false | 400338 | The template item highlight parameter is invalid. |
| Common | false | 400339 | The template header replaced with template parameters cannot exceed 16 characters. |
| Common | false | 400340 | The template representative link parameter is invalid. |
| Common | false | 400341 | Content cannot exceed 700 characters when template items are requested. |
| Common | false | 400342 | Message sending failed because the deadline has expired. |
| Common | false | 400343 | Please configure the sender profile resend settings. |
| Common | false | 400344 | The quick reply parameter is invalid. |
| Common | false | 400345 | Too many buttons when quick reply is requested. |
| Common | false | 400346 | If the template has a web link, linkMo must be entered. |
| Common | false | 400347 | The template code or template name already exists. |
| Common | false | 400348 | The field is invalid. |
| Common | false | 400349 | Please check the template parameters. |
| Common | false | 400350 | Please check the template status. |
| Common | false | 400351 | linkMo or linkPc must include http:// or https://. |
| Common | false | 400352 | If the template has an AL (appLink), at least two of the following must be entered: schemeAndroid, schemeIos, and LinkMo. |
| Common | false | 400353 | Replacement parameters cannot be included in the button name. |
| Common | false | 400354 | The content does not match the template. |
| Common | false | 400355 | The button or quick reply does not match the template. |
| Common | false | 400356 | Only templates in the TSC03 (APPROVE) or TSC04 (REJECT) status can be modified. |
| Common | false | 400357 | There is already a template being modified. |
| Common | false | 400358 | The button type is invalid. |
| Common | false | 400359 | The sender profile cannot use the CBT feature. |
| Common | false | 400360 | Templates with the 'TEXT' highlight type must have templateTitle and templateSubtitle. |
| Common | false | 400361 | Replacement parameters cannot be included in the template subtitle. |
| Common | false | 400362 | Templates with the 'EX' message type must have templateExtra. |
| Common | false | 400363 | Templates with the 'MI' message type must have templateExtra. |
| Common | false | 400364 | Replacement parameters cannot be included in additional template items. |
| Common | false | 400365 | AC type buttons can only be used with templateMessageType (AD/MI). |
| Common | false | 400366 | The AC type button must be placed alone or at the top. |
| Common | false | 400367 | The AC type button name must be 'Add Channel'. |
| Common | false | 400368 | Templates with the 'NONE' highlight type cannot have templateTitle or templateSubtitle. |
| Common | false | 400369 | Templates with the 'BA' message type cannot have templateExtra. |
| Common | false | 400370 | Templates with the 'AD' message type cannot have templateExtra. |
| Common | false | 400371 | Templates with the 'IMAGE' highlight type must have templateImageName and templateImageUrl. |
| Common | false | 400372 | The template cannot be deleted due to recently sent messages. |
| Common | false | 400373 | Templates with the 'ITEM_LIST' highlight type must have at least one of the following: templateImageInfo, templateHeader, templateItem, and templateItemHighlight. |
| Common | false | 400374 | Templates with the 'ITEM_LIST' highlight type cannot be security templates. |
| Common | false | 400375 | Replacement parameters cannot be included in the template item title. |
| Common | false | 400376 | Replacement parameters cannot be included in the template item summary title. |
| Common | false | 400377 | A template item summary cannot exist without a template item list. |
| Common | false | 400378 | Highlighting items with thumbnails The title cannot exceed 21 characters, and the description cannot exceed 13 characters. |
| Common | false | 400379 | imageUrl must include http:// or https://. |
| Common | false | 400380 | The template header does not match the template. |
| Common | false | 400381 | The template item or template item highlight does not match the template. |
| Common | false | 400382 | The BF type button must be placed at the top. |
| Common | false | 400383 | The button link type 'BF' must follow this constraint. |
| Common | false | 400384 | The template representative link does not match the template. |
| Common | false | 400385 | The template title and template item highlight title cannot end with a space. |
| Common | false | 400386 | The length of the template parameter cannot exceed 1,000 characters. |
| Common | false | 400387 | The template parameter does not match the template. |
| Common | false | 400388 | A comment cannot be added to a template in the registered or completed status. |
| Common | false | 400389 | Replacement parameters cannot be included in the quick reply name. |
| Common | false | 400390 | The format of the button or quick reply is invalid. |
| Common | false | 400391 | The Friend Talk wide item must have a title. |
| 공통 | false | 400392 | A FriendTalk wide item must have an image. |
| 공통 | false | 400393 | A FriendTalk wide item must have a linkMo. |
| 공통 | false | 400394 | A FriendTalk wide entry should have three or four lists and a header. |
| 공통 | false | 400395 | A FriendTalk carousel must have a header. |
| 공통 | false | 400396 | A FriendTalk carousel must have a message. |
| 공통 | false | 400397 | A FriendTalk carousel must have an attachment. |
| 공통 | false | 400398 | A FriendTalk carousel must have an image. |
| 공통 | false | 400399 | A FriendTalk carousel must have between 2 and 10 items. |
| 공통 | false | 400400 | A FriendTalk carousel tail must have a linkMo. |
| 공통 | false | 400401 | A FriendTalk coupon must have a title and a description. |
| 공통 | false | 400402 | For FriendTalk text/image type messages, the length of the FriendTalk coupon description cannot exceed 12 characters. |
| 공통 | false | 400403 | The FriendTalk coupon title is not valid. |
| 공통 | false | 400404 | FriendTalk must have a mobile link or a channel link in iOS/Android format. |
| 공통 | false | 400405 | FriendTalk wide items/carousels can only be sent as the AD type. |
| 공통 | false | 400406 | The subject length of the first wide item in a FriendTalk cannot exceed 25 characters, and the subject length of the second through fourth wide items cannot exceed 30 characters. |
| 공통 | false | 400407 | The FriendTalk button size is not valid. |
| 공통 | false | 400408 | The FriendTalk video URL is not valid. |
| 공통 | false | 400409 | 'content' is too long. |
| 공통 | false | 400410 | 'header' is too long. |
| 공통 | false | 400411 | The FriendTalk carousel feed type cannot have a 'head' field. |
| 공통 | false | 400412 | The FriendTalk carousel feed type cannot have an 'additionalContent' field. |
| 공통 | false | 400413 | The FriendTalk carousel feed type cannot have a 'commerce' field. |
| 공통 | false | 400414 | The FriendTalk Carousel commerce type cannot have 'header' and 'message' fields. |
| 공통 | false | 400415 | The FriendTalk carousel button size is not valid. |
| 공통 | false | 400416 | If you have a 'Discounted price' field in your commerce, then you need to have a 'Discount percentage' or 'Discount fixed amount' field. |
| 공통 | false | 400417 | The parameter is not valid. |
| 공통 | false | 400418 | The app key is already activated. |
| 공통 | false | 400419 | The app key is not activated. |
| 공통 | false | 400420 | Search is only available within the last 31 days. |
| 공통 | false | 400421 | The app key is in a deactivated state. |
| 공통 | false | 400422 | The app key does not have a sender key. |
| 공통 | false | 400423 | The file size is less than {}. |
| 공통 | false | 400424 | The file size is less than 20 MB. |
| 공통 | false | 400425 | Check the file extension. |
| 공통 | false | 400426 | The maximum recipient list size has been exceeded. |
| 공통 | false | 400427 | Only jpg/jpeg file extensions can be uploaded. |
| 공통 | false | 400428 | The file does not have a recipient number header. |
| 공통 | false | 400429 | The requestId is not valid. |
| 공통 | false | 400430 | Messages older than 90 days cannot be retrieved. |
| 공통 | false | 400431 | A file upload error has occurred. |
| 공통 | false | 400432 | The recipient number is not valid. |
| 공통 | false | 400433 | Failed to read the file. |
| 공통 | false | 400434 | The file size is less than 10 MB. |
| 공통 | false | 400435 | Failed to export data. |
| 공통 | false | 400436 | To deactivate the product, you must delete all senders. |
| 공통 | false | 400437 | Failed to reactivate the dormant template. |
| 공통 | false | 400438 | You can upload a maximum of 20 templates at a time. |
| 공통 | false | 400439 | The header of the uploaded template is not valid. |
| 공통 | false | 400440 | Failed to convert to AD/MI type. |
| 공통 | false | 400441 | Failed to convert to AD/MI type. |
| 공통 | false | 400442 | The search parameter is not valid. |
| 공통 | false | 400443 | The RequestId or the start/end request date is not valid. |
| 공통 | false | 400444 | RequestId is empty. |
| 공통 | false | 400445 | The resend message is not valid. |
| 공통 | false | 400446 | The recipient number is not valid. |
| 공통 | false | 400447 | The vendor API request failed. |
| 공통 | false | 400448 | 'imageSeq' is empty. |
| 공통 | false | 400449 | The uploaded image is not valid. |
| 공통 | false | 400450 | Failed to delete the image. |
| 공통 | false | 400451 | 'createUser' is too long. |
| 공통 | false | 400452 | Authentication-related content must be included. |
| 공통 | false | 400453 | The storage configuration cannot be empty. |
| 공통 | false | 400454 | The content contains prohibited words. |
| 공통 | false | 400455 | This project has already been shared. |
| 공통 | false | 400456 | Failed to upload the image file due to an encoding error. |
| 공통 | false | 400457 | A required part of the request is missing. |
| 공통 | false | 400458 | The type of the method argument does not match what was expected. |
| 공통 | false | 400459 | This version is deprecated. |
| 공통 | false | 400460 | Only the application/json content type is supported. |
| 공통 | false | 400461 | A client error has occurred. |
| 공통 | false | 400462 | templateMessageType (AD/MI) must include an AC type button.<br>A system error has occurred. |
| 공통 | false | 400500 | The parameter is not valid. |
| 공통 | false | 400501 | The parameter format is not valid. |
| 공통 | false | 400502 | The parameter is empty or null. |
| 공통 | false | 400503 | The certificate is not valid. |
| 공통 | false | 400504 | The certificate is a duplicate. |
| 공통 | false | 400505 | The certificate has expired. |
| 공통 | false | 400506 | The certificate is already registered. |
| 공통 | false | 400507 | The maximum limit has been exceeded. |
| 공통 | false | 400508 | The certificate has already been completed. |
| 공통 | false | 400509 | Too many. |
| 공통 | false | 400510 | The API version is not supported. |
| 공통 | false | 400511 | The deletion guide is empty. |
| 공통 | false | 400512 | The contact is empty. |
| 공통 | false | 400513 | The contact format is not valid ([0-9-]+). |
| 공통 | false | 400514 | The APNS certificate does not support VoIP. |
| 공통 | false | 400515 | The HTTP method is not supported. |
| 공통 | false | 400516 | There is no channel available to receive messages. |
| 공통 | false | 400517 | 'target |
| 공통 | false | 400518 | The push type is not valid. |
| 공통 | false | 400519 | The channel is an empty string. |
| 공통 | false | 400520 | Access is not allowed. |
| 공통 | false | 400521 | The key cannot be used. |
| 공통 | false | 400600 | The SMS project is in a deactivated state. |
| 공통 | false | 400601 | The SMS project cannot be used. |
| 공통 | false | 400602 | The button parameter is not valid. |
| 공통 | false | 400603 | An opt-out number is required when sending advertising messages. |
| 공통 | false | 400604 | Only one card can be registered for horizontal and vertical types. |
| 공통 | false | 400605 | The brand status is not valid. |
| 공통 | false | 400606 | The chatbot status is not valid. |
| 공통 | false | 400607 | The template status is not valid. |
| 공통 | false | 400608 | The template is not supported. |
| 공통 | false | 400609 | The advertising template cannot be used. |
| 공통 | false | 400610 | The media has expired. |
| 공통 | false | 400611 | The media type is not valid. |
| 공통 | false | 400612 | The maximum file size has been exceeded. |
| 공통 | false | 400613 | The media format is not valid. |
| 공통 | false | 400614 | An empty media file was uploaded. |
| 공통 | false | 400615 | The blocking service status is not valid. |
| 공통 | false | 400616 | The recipient number is blocked. |
| 공통 | false | 400617 | The sender number does not exist. |
| 공통 | false | 400618 | The type is not supported. |
| 공통 | false | 400619 | Failed to call the opt-out list retrieval API. |
| 공통 | false | 400620 | Failed to call the opt-out list retrieval API. |
| 공통 | false | 400621 | Failed to call the sender number retrieval API. |
| 공통 | false | 400622 | Failed to call the project retrieval API. |
| 공통 | false | 400623 | Failed to call the SMS project activation API. |
| 공통 | false | 400624 | Failed to call the SMS sending API. |
| 공통 | false | 400700 | There is no identity verification history. |
| 공통 | false | 404000 | {0} not found.<br>The contact was not found.<br>The recipient was not found.<br>The self-authentication was not found.<br>The identity verification record was not found.<br>The content was not found.<br>The attachment was not found.<br>The category was not found.<br>The project was not found.<br>The recipient set was not found.<br>The result of sending to the recipient (messageId: {0}, recipientIndex: {1}) does not exist.<br>Contact sending result (messageId: {0}, recipientIndex: {1}, contactIndex: {2}) does not exist. |
| 공통 | false | 404100 | Failed to retrieve the template. |
| 공통 | false | 404101 | The opt-out information was not found. |
| 공통 | false | 404102 | The category information was not found. |
| 공통 | false | 404103 | The Excel file was not found. |
| 공통 | false | 404104 | The app key does not exist. |
| 공통 | false | 404201 | The service does not exist. |
| 공통 | false | 404202 | The file has expired or does not exist. |
| 공통 | false | 404203 | The data does not exist. |
| 공통 | false | 404204 | The download schedule does not exist. |
| 공통 | false | 404205 | The template does not exist. |
| 공통 | false | 404206 | The category does not exist. |
| 공통 | false | 404207 | The registered sender number request information does not exist. |
| 공통 | false | 404208 | The data does not exist. |
| 공통 | false | 404209 | The registered request sender number does not exist. |
| 공통 | false | 404210 | This common code does not exist. |
| 공통 | false | 404211 | The AuthCode does not exist. |
| 공통 | false | 404212 | This URI does not exist. |
| 공통 | false | 404213 | This IP does not exist. |
| 공통 | false | 404214 | The search period is not valid. |
| 공통 | false | 404215 | The authentication information does not exist. |
| 공통 | false | 404216 | The Excel file was not found. |
| 공통 | false | 404217 | The configCode does not exist. |
| 공통 | false | 404218 | The CSV file was not found. |
| 공통 | false | 404219 | This is not a registered opt-out number. |
| 공통 | false | 404220 | The number is not registered. |
| 공통 | false | 404221 | The number is already registered. |
| 공통 | false | 404222 | The opt-out number is not registered. |
| 공통 | false | 404300 | The sender profile group does not exist. |
| 공통 | false | 404301 | No message was found for the requested requestId or recipientSeq. |
| 공통 | false | 404302 | The sender profile does not exist. |
| 공통 | false | 404303 | The message to cancel was not found or does not meet the cancellation conditions. |
| 공통 | false | 404304 | The bulk message request was not found. |
| 공통 | false | 404305 | The template does not exist. |
| 공통 | false | 404306 | The button name does not exist. |
| 공통 | false | 404307 | The template does not have a button or quick reply. |
| 공통 | false | 404308 | The quick reply name does not exist. |
| 공통 | false | 404309 | The app key does not exist. |
| 공통 | false | 404310 | The file was not found. |
| 공통 | false | 404311 | The recipient list was not found. |
| 공통 | false | 404312 | The data does not exist. |
| 공통 | false | 404313 | The image was not found. |
| 공통 | false | 404314 | There is no sender profile registered in your project. |
| 공통 | false | 404315 | The API does not exist. |
| 공통 | false | 404600 | The brand is not linked. |
| 공통 | false | 404601 | The brand does not exist. |
| 공통 | false | 404602 | The chatbot does not exist. |
| 공통 | false | 404603 | The template does not exist. |
| 공통 | false | 404604 | The media does not exist. |
| 공통 | false | 404605 | The opt-out list does not exist. |
| 공통 | false | 404606 | The message ID does not exist. |
| 공통 | false | 409000 | Group recipient (groupId: {0}, recipientId: {1}) already exists.<br>The recipient alias is already registered.<br>Message recipient ({0}, messageRecipientSetId: {1}, index: {2}) already exists.<br>{0} already exists. |
| 공통 | false | 500001 | An internal server error has occurred. |
| 공통 | false | 500002 | Invalid status server error. |
| Message sending | false | 400001 | The number of contacts has been exceeded.<br>The flow sending order is empty.<br>The initial flow sending channel is empty.<br>The flow sending order is invalid.<br>Duplicate message channel.<br>Unable to add message recipients.<br>Invalid phone number pattern.<br>Invalid email address pattern.<br>Invalid token pattern.<br>{0} is an invalid Alim Talk template status.<br>The email local part length has been exceeded.<br>The email address length has been exceeded.<br>The email domain length has been exceeded.<br>The phone number is empty.<br>The phone number {0} contains a non-numeric value.<br>Invalid phone number. {0}<br>Invalid date format. {0}<br>{0} is an invalid file type.<br>{0} is not supported.<br>Contact sending result lookup fields (messageId: {0}, templateId: {1}, flowId: {2}, statsKeyId: {3}, sender: {4}, contact: {5}) One of them must have a value.<br>The creation date start and creation date end must have values.<br>The creation date start must be earlier than the creation date end.<br>A message channel is required when a sender is provided.<br>Invalid contact type {1} for message channel {0}.<br>Message recipient set ID and recipient are mutually exclusive.<br>A message recipient set ID or recipient is required.<br>The message recipient set is incomplete.<br>The recipient set is currently invalid.<br>The recipient set type is not a file. {0}<br>The content is empty.<br>The attachment is empty.<br>The Alim Talk template item highlight is empty.<br>The Alim Talk template image URL is empty.<br>The Alim Talk image URL is empty.<br>The body must contain an authentication phrase.<br>A sender key is required for a group template.<br>The Friend Talk wide item list items are empty.<br>The Friend Talk carousel is empty.<br>The type of FriendTalk template you entered can't have coupons.<br>The Friend Talk coupon title is invalid.<br>A category with subcategories cannot be deleted.<br>A category with templates cannot be deleted.<br>The user access key is empty.<br>The SecretKey is empty.<br>The user UUID is empty.<br>The AppKey is empty.<br>The body is empty.<br>The title is empty.<br>The RCS brand ID is empty.<br>The RCS chatbot ID is empty.<br>The RCS chatbot ID is invalid.<br>The RCS unsubscribe number is empty.<br>The RCS body is too long.<br>The RCS title is too long.<br>The RCS MMS type is empty.<br>The RCS message default ID is empty.<br>Too many buttons.<br>The button JSON is invalid.<br>The RCS card is empty.<br>The RCS card size is invalid.<br>The RCS description is empty.<br>The RCS description is too long.<br>The SecretKey cannot be found.<br>Not available at {0}. {1}<br>The {0} value is invalid.<br>Unsupported message channel.<br>The statsId length must be 8 characters or fewer.<br>The sender's ({0}) domain is not authenticated, please authenticate your domain. |
| Message sending | false | 403000 | You do not have permission. |
| Message sending | false | 500001 | An internal server error has occurred. |
| Message sending | false | 500002 | Invalid status server error. |

<a id="delivery-result-code"></a>
## Received Results Code

| Category | Success (isSuccessful) | Result Code (resultCode) | Result Message (resultMessage) |
| --- | --- | --- | --- |
| Common | true | 00000000 | Success |
| Common | false | 00999999 | Other errors |
| Common | false | 09000000 | Cancel delivery |
| SMS | false | 11100001 | Failed to send the message due to advertising sending time restrictions. |
| SMS | false | 11100002 | Failed to send the message due to duplicate sending restrictions. |
| SMS | false | 11902023 | Failed to send the message because the subject or body contains a disallowed character set. |
| SMS | false | 11902044 | Failed to send the message because international sending is not allowed in that country. |
| SMS | false | 11902045 | Failed to send the message because international sending is disabled. |
| SMS | false | 11902047 | Failed to send the message because the monthly international sending limit has been exceeded. |
| SMS | false | 11902049 | Failed to send the message due to whitelist settings. |
| SMS | false | 11902051 | Failed to send the message due to a conversion rate issue. |
| SMS | false | 11902052 | Failed to send the message due to the per-organization sending volume limit. |
| SMS | false | 11906001 | Failed to send the message due to an opt-out. |
| SMS | false | 12000002 | Failed to send the message due to an error while processing sequential flow sending. |
| SMS | false | 12000003 | Failed to send the message due to an error while preparing to send the message. |
| SMS | false | 12100911 | Failed to send the message because the attachment has no file extension. |
| SMS | false | 12100913 | Failed to send the message because the attachment size is 0. |
| SMS | false | 12909999 | Failed to send the message due to a system error. |
| SMS | false | 13004001 | Failed to send the message due to a signature format error. |
| SMS | false | 13004002 | Failed to send the message due to a sender number error. |
| SMS | false | 13004003 | Failed to send the message due to a recipient number error. |
| SMS | false | 13100900 | Failed to send the message due to other errors. |
| SMS | false | 16001001 | Failed to send the message because the server is congested. |
| SMS | false | 16001002 | Failed to send the message because the recipient number format is invalid. |
| SMS | false | 16001003 | Failed to send the message because the sender number format is invalid. |
| SMS | false | 16001004 | Failed to send the message because the message was deleted due to a carrier error. |
| SMS | false | 16001019 | Failed to send the message due to TTL expiration. |
| SMS | false | 16002000 | Failed to send the message because the sending time has expired. |
| SMS | false | 16002001 | Failed to send the message due to a wireless network issue. |
| SMS | false | 16002002 | Failed to send the message because the message was not delivered from the wireless network to the device. |
| SMS | false | 16002004 | Failed to send the message because the message buffer between the carrier and the device is full. |
| SMS | false | 16002006 | Failed to send the message because the message was deleted. |
| SMS | false | 16003000 | Failed to send the message because the message could not be sent. |
| SMS | false | 16003009 | Failed to send the message due to a message format error. |
| SMS | false | 16003011 | Failed to send the message due to a server error. |
| SMS | false | 16003012 | Failed to send the message because it was classified as spam. |
| SMS | false | 16003013 | Message sending was rejected by the service. |
| SMS | false | 16003014 | Failed to send the message due to other reasons. |
| SMS | false | 16003016 | Failed to send the message because the attachment size limit was exceeded. |
| SMS | false | 16004004 | Failed to send the message due to a temporary device issue. |
| SMS | false | 16004005 | Failed to send the message because the subscriber does not exist. |
| SMS | false | 16004006 | Failed to send the message due to a recipient error. |
| SMS | false | 16004007 | Failed to send the message due to a carrier error or block. |
| SMS | false | 16004008 | Failed to send the message because it was classified as spam. |
| SMS | false | 16004009 | Failed to send the message due to a temporary network error. |
| SMS | false | 16004010 | Failed to send the message due to an abnormal sending pattern. |
| SMS | false | 16100915 | Failed to send the message due to a duplicate message. |
| SMS | false | 16100919 | Failed to send the message because it is outside the sending time window or message resending is prohibited. |
| SMS | false | 16100999 | Failed to send the message due to other errors. |
| SMS | false | 17002003 | Failed to send the message because the device is powered off. |
| SMS | false | 17002005 | Failed to send the message due to a coverage dead zone. |
| SMS | false | 17002007 | Failed to send the message due to a temporary device issue. |
| SMS | false | 17003001 | Failed to send the message because the subscriber does not exist. |
| SMS | false | 17003003 | Failed to send the message due to an invalid recipient number format or a non-existent number. |
| SMS | false | 17003004 | Failed to send the message because the device service is temporarily suspended. |
| SMS | false | 17003005 | Failed to send the message because the message was not delivered while the device was processing a call. |
| SMS | false | 17003006 | Failed to send the message because the incoming call was rejected. |
| SMS | false | 17003008 | Failed to send the message due to other device issues. |
| SMS | false | 17003010 | Failed to send the message because the device does not support MMS. |
| SMS | false | 17003017 | Failed to send the message because the number format is invalid due to the caller ID spoofing prevention service. |
| SMS | false | 17003018 | Failed to send the message because the sender number is a personal mobile number registered with the caller ID spoofing prevention service. |
| SMS | false | 17003019 | Failed to send the message because the sender number is blocked by KISA or the Ministry of Science and ICT. |
| ALIMTALK | false | 21901000 | Failed to send the message due to an invalid appKey. |
| ALIMTALK | false | 21901001 | Failed to send the message due to an invalid secretKey. |
| ALIMTALK | false | 21901002 | Failed to send the message due to an invalid SMS appKey. |
| ALIMTALK | false | 21901003 | Failed to send the message due to an invalid SMS Sendno. |
| ALIMTALK | false | 21901004 | Failed to send the message because the Plus Friend is already registered. |
| ALIMTALK | false | 21901005 | Failed to send the message because the same 'X-NC-API-IDEMPOTENCY-KEY' was used within the last 10 minutes. |
| ALIMTALK | false | 21901006 | Failed to send the message because senderKey does not exist in the Plus Friend. |
| ALIMTALK | false | 21901010 | Failed to send the message because the Plus Friend group does not exist. |
| ALIMTALK | false | 21901013 | Failed to send the message because the Plus Friend group already exists. |
| ALIMTALK | false | 21901014 | Failed to send the message because the Plus Friend is not in an active state. |
| ALIMTALK | false | 21901016 | Failed to send the message because no message matching the requestId or recipientSeq could be found. |
| ALIMTALK | false | 21901017 | Failed to send the message because the daily maximum message count has been exceeded. |
| ALIMTALK | false | 21901018 | Failed to send the message because the Plus Friend has already been added. |
| ALIMTALK | false | 21901019 | Failed to send the message due to an invalid SMS UnSubscribeno. |
| ALIMTALK | false | 21901020 | Failed to send the message due to an invalid uuid. |
| ALIMTALK | false | 21901022 | Failed to send the message because the Plus Friend has not been added to the group. |
| ALIMTALK | false | 21901023 | Failed to send the message because the maximum Plus Friend group size of 10 has been exceeded. |
| ALIMTALK | false | 21901024 | Failed to send the message because a sender group cannot send messages. |
| ALIMTALK | false | 21901025 | Failed to send the message because a sender group cannot be deleted. |
| ALIMTALK | false | 21901026 | Failed to send the message because the maximum group member count (5,000) has been exceeded. |
| ALIMTALK | false | 21901027 | Failed to send the message because the sender is blocked. |
| ALIMTALK | false | 21901028 | Failed to send the message because the template value exceeds 14 characters. |
| ALIMTALK | false | 21901029 | Failed to send the message because a blacklisted sender cannot join a group. |
| ALIMTALK | false | 21901030 | Failed to send the message because identity verification is required. |
| ALIMTALK | false | 21902000 | Failed to send the message because '{}' must be {} or less. |
| ALIMTALK | false | 21902001 | Failed to send the message because '{}' cannot be blank. |
| ALIMTALK | false | 21902002 | Failed to send the message because '{}' cannot be null. |
| ALIMTALK | false | 21902003 | Failed to send the message because '{}' must be {} or more. |
| ALIMTALK | false | 21902004 | Failed to send the message because '{}' must be between {} and {}. |
| ALIMTALK | false | 21902005 | Failed to send the message because '{}' must be {} or less. |
| ALIMTALK | false | 21902017 | Failed to send the message because the Plus Friend does not exist. |
| ALIMTALK | false | 21902018 | Failed to send the message because the button parameter is invalid. |
| ALIMTALK | false | 21902019 | Failed to send the message because the template parameter replacement content exceeds 1,000 characters. |
| ALIMTALK | false | 21902023 | Failed to send the message because 'content' is too long (maximum 400 characters when using an image). |
| ALIMTALK | false | 21902024 | Failed to send the message because 'content' is too long (maximum 1,000 characters when not using an image). |
| ALIMTALK | false | 21902025 | Failed to send the message because a past date cannot be used. Check `requestDate`. |
| ALIMTALK | false | 21902026 | Failed to send the message because a date more than 90 days in the future cannot be used. Check `requestDate`. |
| ALIMTALK | false | 21902027 | Failed to send the message because the 'requestDate' format is invalid. |
| ALIMTALK | false | 21902028 | Failed to send the message because 'requestId' is invalid. |
| ALIMTALK | false | 21902029 | Failed to send the message because there is no message to cancel or the conditions are not met. |
| ALIMTALK | false | 21902030 | Failed to send the message because 'content' is too long (maximum 76 characters when using a wide image). |
| ALIMTALK | false | 21902031 | Failed to send the message because there are too many 'buttons' (maximum 2 when using a wide image). |
| ALIMTALK | false | 21902032 | Failed to send the message because the templateTitle replaced by template parameters exceeds 50 characters. |
| ALIMTALK | false | 21902033 | Failed to send the message because the TemplateItem parameter is invalid. |
| ALIMTALK | false | 21902034 | Failed to send the message because the TemplateItemHighlight parameter is invalid. |
| ALIMTALK | false | 21902035 | Failed to send the message because templateHeader exceeds 16 characters. |
| ALIMTALK | false | 21902036 | Failed to send the message because the TemplateRepresentLink parameter is invalid. |
| ALIMTALK | false | 21902037 | Failed to send the message because 'content' is too long (maximum 700 characters when using templateItem). |
| ALIMTALK | false | 21902500 | Failed to send the message because the bulk message request could not be found. |
| ALIMTALK | false | 21902501 | Failed to send the message because the sending request deadline has expired. |
| ALIMTALK | false | 21902502 | Failed to send the message because the Plus Friend resending settings are required. |
| ALIMTALK | false | 21902504 | Failed to send the message because the quickReplies parameter is invalid. |
| ALIMTALK | false | 21902505 | Failed to send the message because there are too many 'buttons' (maximum 2 when using quickReplies). |
| ALIMTALK | false | 21903000 | Failed to send the message because linkMo was not entered even though the template has a WL (webLink). |
| ALIMTALK | false | 21903001 | Failed to send the message because the templateCode or templateName already exists. |
| ALIMTALK | false | 21903002 | Failed to send the message because a field is invalid. |
| ALIMTALK | false | 21903003 | Failed to send the message because the template does not exist. |
| ALIMTALK | false | 21903004 | Failed to send the message because the template parameter is invalid. |
| ALIMTALK | false | 21903005 | Failed to send the message because the template status is invalid. (Check the approval/rejection status.) |
| ALIMTALK | false | 21903006 | Failed to send the message because linkMo/linkPc does not contain http:// or https://. |
| ALIMTALK | false | 21903007 | Failed to send the message because the template has an AL (appLink) but at least two of schemeAndroid, schemeIos, and linkMo are missing. |
| ALIMTALK | false | 21903008 | Failed to send the message because the button name contains a replacement parameter. |
| ALIMTALK | false | 21903009 | Failed to send the message due to a non-existent button name. |
| ALIMTALK | false | 21903010 | Failed to send the message because the content does not match the template. (SMS fallback is available when resending is configured.) |
| ALIMTALK | false | 21903011 | Failed to send the message because the buttons/quickReplies do not match the template. (SMS fallback is available when resending is configured.) |
| ALIMTALK | false | 21903012 | Failed to send the message because the template status must be TSC03/APPROVE or TSC04/REJECT to allow editing. |
| ALIMTALK | false | 21903013 | Failed to send the message because a template that is already being edited exists. |
| ALIMTALK | false | 21903014 | Failed to send the message because the button type is invalid. |
| ALIMTALK | false | 21903015 | Failed to send the message because the use of the CBT feature is not allowed for this Plus Friend. |
| ALIMTALK | false | 21903016 | Failed to send the message because the template with emphasizeType set to 'TEXT' is missing templateTitle or templateSubtitle. |
| ALIMTALK | false | 21903017 | Failed to send the message because templateSubtitle contains a replacement parameter. |
| ALIMTALK | false | 21903018 | Failed to send the message because the template with messageType set to 'EX' is missing templateExtra. |
| ALIMTALK | false | 21903020 | Failed to send the message because the template with messageType set to 'MI' is missing templateExtra. |
| ALIMTALK | false | 21903021 | Failed to send the message because templateExtra contains a replacement parameter. |
| ALIMTALK | false | 21903024 | Failed to send the message because an AC type button can only be used with templateMessageType (AD/MI). |
| ALIMTALK | false | 21903025 | Failed to send the message because an AC type button must be placed alone or at the top position. |
| ALIMTALK | false | 21903026 | Failed to send the message because the AC type button name does not include 'Add Channel'. |
| ALIMTALK | false | 21903027 | Failed to send the message because the template with emphasizeType set to 'NONE' has templateTitle or templateSubtitle. |
| ALIMTALK | false | 21903028 | Failed to send the message because the template with messageType 'BA' contains templateExtra. |
| ALIMTALK | false | 21903030 | Failed to send the message because the template with messageType 'AD' contains templateExtra. |
| ALIMTALK | false | 21903032 | Failed to send the message because the template with emphasizeType 'IMAGE' is missing templateImageName and templateImageUrl. |
| ALIMTALK | false | 21903033 | Failed to send the message because the specified button/quickReply does not exist in the template. |
| ALIMTALK | false | 21903034 | Failed to send the message because the template cannot be deleted due to a recently sent message. (requestId: {}) |
| ALIMTALK | false | 21903035 | Failed to send the message because the template with emphasizeType 'ITEM_LIST' is missing required fields (templateImageInfo, templateHeader, templateItem, etc.). |
| ALIMTALK | false | 21903036 | Failed to send the message because a template with emphasizeType 'ITEM_LIST' cannot be a security template. |
| ALIMTALK | false | 21903037 | Failed to send the message because the templateItem title contains a replacement parameter. |
| ALIMTALK | false | 21903038 | Failed to send the message because the templateItem summary title contains a replacement parameter. |
| ALIMTALK | false | 21903039 | Failed to send the message because a summary cannot exist without a templateItem list. |
| ALIMTALK | false | 21903040 | Failed to send the message because the itemHighlight with a thumbnail exceeds the title (up to 21 characters) or description (up to 13 characters) limit. |
| ALIMTALK | false | 21903041 | Failed to send the message because imageUrl does not contain http:// or https://. |
| ALIMTALK | false | 21903042 | Failed to send the message because templateHeader does not match the template. (SMS fallback on resend) |
| ALIMTALK | false | 21903043 | Failed to send the message because templateItem or templateItemHighlight does not match the template. (SMS fallback on resend) |
| ALIMTALK | false | 21903044 | Failed to send the message because the BF type button must be placed at the top but this requirement was not met. |
| ALIMTALK | false | 21903045 | Failed to send the message because the 'BF' link type button requires a bizFormKey, and the button name must be one of "톡에서 예약하기", "톡에서 설문하기", or "톡에서 응모하기", but this requirement was not met. |
| ALIMTALK | false | 21903046 | Failed to send the message because templateRepresentLink does not match the template. (SMS fallback on resend) |
| ALIMTALK | false | 21903047 | Failed to send the message because templateTitle or the title of templateItemHighlight ends with a space. |
| ALIMTALK | false | 21903048 | Failed to send the message because the template parameter length exceeds 1,000 characters. |
| ALIMTALK | false | 21903049 | Failed to send the message because the template parameters do not match the template. |
| ALIMTALK | false | 21903050 | Failed to send the message because an AC type button is required for templateMessageType (AD/MI) but is missing. |
| ALIMTALK | false | 21903100 | Failed to send the message because adding a comment is not allowed when the template is in a registered/completed state. |
| ALIMTALK | false | 21903101 | Failed to send the message because the quickReply name does not exist. |
| ALIMTALK | false | 21903102 | Failed to send the message because the quickReply name contains a replacement parameter. |
| ALIMTALK | false | 21903103 | Failed to send the message because the button/quickReply format is invalid. |
| ALIMTALK | false | 21903200 | Failed to send the message because the FriendTalk wide item has no title. |
| ALIMTALK | false | 21903201 | Failed to send the message because the FriendTalk wide item has no image. |
| ALIMTALK | false | 21903202 | Failed to send the message because the FriendTalk wide item has no linkMo. |
| ALIMTALK | false | 21903203 | Failed to send the message because the FriendTalk wide item requires at least 3 to 4 list items and a header, but they are missing. |
| ALIMTALK | false | 21903204 | Failed to send the message because the FriendTalk carousel has no header. |
| ALIMTALK | false | 21903205 | Failed to send the message because the FriendTalk carousel has no message. |
| ALIMTALK | false | 21903206 | Failed to send the message because the FriendTalk carousel has no attachment. |
| ALIMTALK | false | 21903207 | Failed to send the message because the FriendTalk carousel has no image. |
| ALIMTALK | false | 21903208 | Failed to send the message because the FriendTalk carousel item count is invalid (2 to 10 items, or 1 to 10 items when an intro is included). |
| ALIMTALK | false | 21903209 | Failed to send the message because the FriendTalk carousel tail has no linkMo. |
| ALIMTALK | false | 21903210 | Failed to send the message because the FriendTalk coupon has no title or description. |
| ALIMTALK | false | 21903211 | Failed to send the message because the FriendTalk coupon description exceeds the limit (up to 12 characters for text/image type, up to 18 characters for wide image/item list). |
| ALIMTALK | false | 21903212 | Failed to send the message because the FriendTalk coupon title is invalid. |
| ALIMTALK | false | 21903213 | Failed to send the message because FriendTalk has no mobile link or iOS/Android channel link. |
| ALIMTALK | false | 21903215 | Failed to send the message because FriendTalk wide items/carousels can only be sent as AD type but this condition was not met. |
| ALIMTALK | false | 21903216 | Failed to send the message because the first wide item title exceeds 25 characters, or the 2nd through 4th wide item titles exceed 30 characters. |
| ALIMTALK | false | 21903217 | Failed to send the message because the FriendTalk button count is invalid (up to 5 by default; up to 4 with a coupon; up to 2 with a wide image; up to 1 with a video; 1 to 2 for commerce type). |
| ALIMTALK | false | 21903218 | Failed to send the message because the FriendTalk video URL is invalid. |
| ALIMTALK | false | 21903219 | Failed to send the message because 'content' is too long (up to 76 characters when using video). |
| ALIMTALK | false | 21903220 | Failed to send the message because 'header' is too long (up to 20 characters when using video). |
| ALIMTALK | false | 21903221 | Failed to send the message because the FriendTalk carousel (feed type) contains a 'head' field. |
| ALIMTALK | false | 21903222 | Failed to send the message because the FriendTalk carousel (feed type) contains an 'additionalContent' field. |
| ALIMTALK | false | 21903223 | Failed to send the message because the FriendTalk carousel (feed type) cannot include a 'commerce' field. |
| ALIMTALK | false | 21903224 | Failed to send the message because the FriendTalk carousel (commerce type) cannot include 'header' or 'message' fields. |
| ALIMTALK | false | 21903225 | Failed to send the message because the FriendTalk carousel button count is invalid (up to 2 for feed type; 1 to 2 for commerce type). |
| ALIMTALK | false | 21903226 | Failed to send the message because if commerce has 'discountPrice', either 'discountRate' or 'discountFixed' is required but is missing. |
| ALIMTALK | false | 21903300 | Failed to send the message because the opt-out number could not be found. |
| ALIMTALK | false | 21903301 | Failed to send the message because the opted-out recipient could not be found. |
| ALIMTALK | false | 21903302 | Failed to send the message because marketing consent messages are only available for text, image, wide image, carousel feed, and premium video types. |
| ALIMTALK | false | 21904000 | Failed to send the message due to invalid parameters. |
| ALIMTALK | false | 21904001 | Failed to send the message because the appkey is already activated. |
| ALIMTALK | false | 21904002 | Failed to send the message because the appkey is deactivated. |
| ALIMTALK | false | 21904003 | Failed to send the message because searches are limited to within 31 days. |
| ALIMTALK | false | 21904004 | Failed to send the message because the appkey does not exist. |
| ALIMTALK | false | 21904005 | Failed to send the message because the appkey is in a deactivated state. |
| ALIMTALK | false | 21904006 | Failed to send the message because the appkey has no sender key. |
| ALIMTALK | false | 21904007 | Failed to send the message because the file size is less than {}. |
| ALIMTALK | false | 21904008 | Failed to send the message because the file size must be less than 20 MB but the limit was exceeded. |
| ALIMTALK | false | 21904009 | Failed to send the message because the file extension is invalid. |
| ALIMTALK | false | 21904010 | Failed to send the message because the file could not be found. |
| ALIMTALK | false | 21904011 | Failed to send the message because the recipient list could not be found. |
| ALIMTALK | false | 21904012 | Failed to send the message because the maximum number of recipients (10,000) was exceeded. |
| ALIMTALK | false | 21904013 | Failed to send the message because only jpg/jpeg extensions can be uploaded. |
| ALIMTALK | false | 21904014 | Failed to send the message because the file has no recipient_no header. |
| ALIMTALK | false | 21904015 | Failed to send the message because the requestId is invalid. |
| ALIMTALK | false | 21904016 | Failed to send the message because the data does not exist. |
| ALIMTALK | false | 21904017 | Failed to send the message because messages older than 90 days cannot be searched. |
| ALIMTALK | false | 21904018 | Failed to send the message due to an attachment file upload error. |
| ALIMTALK | false | 21904019 | Failed to send the message due to an invalid recipient number. |
| ALIMTALK | false | 21904020 | Failed to send the message due to a file read failure. |
| ALIMTALK | false | 21904021 | Failed to send the message because the file size must be less than 10 MB but the limit was exceeded. |
| ALIMTALK | false | 21904022 | Failed to send the message because the data export failed. |
| ALIMTALK | false | 21904023 | Failed to send the message because all senders must be deleted to deactivate the product, but this condition was not met. |
| ALIMTALK | false | 21904024 | Failed to send the message because deactivating the dormant template failed. |
| ALIMTALK | false | 21904025 | Failed to send the message because only up to 20 templates can be uploaded at a time. |
| ALIMTALK | false | 21904026 | Failed to send the message because the uploaded template header is invalid. |
| ALIMTALK | false | 21904027 | Failed to send the message because the AD/MI type conversion failed: the 'buttons' length exceeds the maximum. |
| ALIMTALK | false | 21904028 | Failed to send the message because the AD/MI type conversion failed: the template is not in an approved state. |
| ALIMTALK | false | 21904101 | Failed to send the message due to invalid search parameters. |
| ALIMTALK | false | 21904103 | Failed to send the message because the RequestId or startRequestDate/endRequestDate is invalid. |
| ALIMTALK | false | 21904104 | Failed to send the message because the RequestId value is empty. |
| ALIMTALK | false | 21904200 | Failed to send the message because the resend message is invalid. |
| ALIMTALK | false | 21905000 | Failed to send the message due to an invalid RecipientNo. |
| ALIMTALK | false | 21907000 | Failed to send the message due to a vendor API request failure. |
| ALIMTALK | false | 21908000 | Failed to send the message because 'imageSeq' is empty. |
| ALIMTALK | false | 21908001 | Failed to send the message because the uploaded image is invalid. |
| ALIMTALK | false | 21908002 | Failed to send the message because a required image (e.g., for carousel feed or commerce) is missing. |
| ALIMTALK | false | 21908003 | Failed to send the message because the image deletion failed. |
| ALIMTALK | false | 21908004 | Failed to send the message because the 'createUser' length exceeds 100 characters. |
| ALIMTALK | false | 21908005 | Failed to send the message because the project has no Plus Friend. (Please register a Plus Friend first.) |
| ALIMTALK | false | 21908006 | Failed to send the message because the content does not include the authentication guide. |
| ALIMTALK | false | 21908007 | Failed to send the message because the storage configuration is empty. |
| ALIMTALK | false | 21908008 | Failed to send the message because the content contains a prohibited word. |
| ALIMTALK | false | 21908009 | Failed to send the message because this project is already shared. |
| ALIMTALK | false | 21908010 | Failed to send the message because the image upload failed due to an unexpected error. |
| ALIMTALK | false | 21908011 | Failed to send the message because the image type is invalid. |
| ALIMTALK | false | 21909993 | Failed to send the message because a required request part is missing. |
| ALIMTALK | false | 21909994 | Failed to send the message because the method argument type does not match the expected type. |
| ALIMTALK | false | 21909995 | Failed to send the message because the version is no longer supported. |
| ALIMTALK | false | 21909996 | Failed to send the message because only application/json is supported. |
| ALIMTALK | false | 21909997 | Failed to send the message due to a client error. |
| ALIMTALK | false | 21909998 | Failed to send the message because the API does not exist. |
| ALIMTALK | false | 22000002 | Failed to send the message because an error occurred during flow sequential send processing. |
| ALIMTALK | false | 22000003 | Failed to send the message because an error occurred while preparing the message for sending. |
| ALIMTALK | false | 22909999 | Failed to send the message due to a system error (contact support@toast.com). |
| ALIMTALK | false | 23001001 | Failed to send the message because the Request Body is not in JSON format. |
| ALIMTALK | false | 23001002 | Failed to send the message because the hub partner key is invalid. |
| ALIMTALK | false | 23001003 | Failed to send the message because the sender profile key is invalid. |
| ALIMTALK | false | 23001004 | Failed to send the message because the name is missing from the Request Body (JSON). |
| ALIMTALK | false | 23001006 | Failed to send the message because the sender profile has been deleted (please contact customer support). |
| ALIMTALK | false | 23001007 | Failed to send the message because the sender profile is in a blocked state (please contact customer support). |
| ALIMTALK | false | 23001011 | Failed to send the message because the contract information could not be found (please contact customer support). |
| ALIMTALK | false | 23001012 | Failed to send the message due to a malformed user key request. |
| ALIMTALK | false | 23001013 | Failed to send the message due to an invalid app connection. |
| ALIMTALK | false | 23001014 | Failed to send the message due to an invalid business registration number. |
| ALIMTALK | false | 23001015 | Failed to send the message due to an invalid app user ID request. |
| ALIMTALK | false | 23001016 | Failed to send the message due to a business registration number mismatch. |
| ALIMTALK | false | 23001020 | Failed to send the message because the phone number or app user ID is invalid or missing. |
| ALIMTALK | false | 23001021 | Failed to send the message due to a blocked KakaoTalk channel. |
| ALIMTALK | false | 23001022 | Failed to send the message due to a closed KakaoTalk channel. |
| ALIMTALK | false | 23001023 | Failed to send the message due to a deleted KakaoTalk channel. |
| ALIMTALK | false | 23001024 | Failed to send the message due to a KakaoTalk channel that is pending deletion. |
| ALIMTALK | false | 23001025 | Failed to send the message due to a channel sanction. |
| ALIMTALK | false | 23001027 | Failed to send the message due to a channel message sanction. |
| ALIMTALK | false | 23001030 | Failed to send the message due to an invalid parameter request. |
| ALIMTALK | false | 23002001 | Failed to send the message because sending is not possible (unexpected error). |
| ALIMTALK | false | 23002003 | Failed to send the message because the KakaoTalk channel has not been added on the test server. |
| ALIMTALK | false | 23002005 | Failed to send the message because image information could not be retrieved due to a Kakao internal system error. |
| ALIMTALK | false | 23003000 | Failed to send the message due to an unexpected error. |
| ALIMTALK | false | 23003005 | Failed to send the message because the message was sent but delivery was not confirmed (uncertain success). |
| ALIMTALK | false | 23003006 | Failed to send the message due to an internal system error. |
| ALIMTALK | false | 23003008 | Failed to send the message due to a phone number error. |
| ALIMTALK | false | 23003010 | Failed to send the message due to an unexpected error. |
| ALIMTALK | false | 23003011 | Failed to send the message because the message does not exist. |
| ALIMTALK | false | 23003012 | Failed to send the message due to a Kakao communication failure. |
| ALIMTALK | false | 23003013 | Failed to send the message because the message is empty. |
| ALIMTALK | false | 23003014 | Failed to send the message due to a message length limit error. |
| ALIMTALK | false | 23003015 | Failed to send the message because the template could not be found. |
| ALIMTALK | false | 23003016 | Failed to send the message because the message content does not match the template. |
| ALIMTALK | false | 23003018 | Failed to send the message because sending is not possible (e.g., mismatch between the Android device SIM number and KakaoTalk number, inactive user, sanctioned user). |
| ALIMTALK | false | 23003019 | Failed to send the message because the recipient is not a KakaoTalk user. |
| ALIMTALK | false | 23003020 | Failed to send the message because the recipient has blocked Alim Talk notifications. |
| ALIMTALK | false | 23003021 | Failed to send the message because the minimum required KakaoTalk version is not supported. |
| ALIMTALK | false | 23003022 | Failed to send the message because it is outside the allowed sending hours (Friend Talk: 8 AM to 8:50 PM). |
| ALIMTALK | false | 23003023 | Failed to send the message due to a message syntax error (JSON format error). |
| ALIMTALK | false | 23003024 | Failed to send the message because the image included in the message could not be sent (link error or specification violation). |
| ALIMTALK | false | 23003025 | Failed to send the message because the variable character limit was exceeded. |
| ALIMTALK | false | 23003026 | Failed to send the message because the character limit for the consultation/bot switch button (extra, event) was exceeded. |
| ALIMTALK | false | 23003027 | Failed to send the message because the message button/quick link does not match the template. |
| ALIMTALK | false | 23003028 | Failed to send the message because the message emphasis title does not match the template. |
| ALIMTALK | false | 23003029 | Failed to send the message because the message emphasis title exceeds 50 characters. |
| ALIMTALK | false | 23003030 | Failed to send the message because the message type does not match the template emphasis type. |
| ALIMTALK | false | 23003031 | Failed to send the message because the header does not match the template. |
| ALIMTALK | false | 23003032 | Failed to send the message because the header exceeds 16 characters. |
| ALIMTALK | false | 23003033 | Failed to send the message because the item highlight does not match the template. |
| ALIMTALK | false | 23003034 | Failed to send the message because the item highlight title exceeds the character limit (30 characters without an image / 21 characters with an image). |
| ALIMTALK | false | 23003035 | Failed to send the message because the item highlight description exceeds the character limit (19 characters without an image / 13 characters with an image). |
| ALIMTALK | false | 23003036 | Failed to send the message because the item list does not match the template. |
| ALIMTALK | false | 23003037 | Failed to send the message because the item list description exceeds the character limit (23 characters). |
| ALIMTALK | false | 23003038 | Failed to send the message because the item summary does not match the template. |
| ALIMTALK | false | 23003039 | Failed to send the message because the item summary description exceeds the character limit (14 characters). |
| ALIMTALK | false | 23003040 | Failed to send the message because the item summary description contains disallowed characters. (Only currency symbols/codes, numbers, commas, decimal points, and spaces are allowed.) |
| ALIMTALK | false | 23003041 | Failed to send the message because the number of wide item list items does not meet the minimum or maximum range. |
| ALIMTALK | false | 23003042 | Failed to send the message because the representative link does not match the template. |
| ALIMTALK | false | 23003046 | Failed to send the message because the maximum length limit for additional information was exceeded. |
| ALIMTALK | false | 23003047 | Failed to send the message because the product name in the commerce information exceeds the character limit. |
| ALIMTALK | false | 23003048 | Failed to send the message due to an invalid group tag key. |
| ALIMTALK | false | 23003051 | Failed to send the message because the number of carousel item list items does not meet the minimum or maximum count. |
| ALIMTALK | false | 23003052 | Failed to send the message because the carousel item message length was exceeded. |
| ALIMTALK | false | 23003056 | Failed to send the message due to a wide item list title length limit error. |
| ALIMTALK | false | 23003058 | Failed to send the message due to a carousel header length limit error. |
| ALIMTALK | false | 23004000 | Failed to send the message because the message delivery result could not be found. |
| ALIMTALK | false | 23004001 | Failed to send the message due to an unknown message status. |
| ALIMTALK | false | 23009998 | A system issue has occurred and is currently being investigated. Message sending is not available at this time. |
| ALIMTALK | false | 23009999 | Failed to send the message due to an unknown system error. (Under investigation) |
| FRIENDTALK | false | 31901000 | Failed to send the message due to an invalid appKey. |
| FRIENDTALK | false | 31901001 | Failed to send the message due to an invalid secretKey. |
| FRIENDTALK | false | 31901002 | Failed to send the message due to an invalid SMS appkey. |
| FRIENDTALK | false | 31901003 | Failed to send the message due to an invalid SMS Sendno. |
| FRIENDTALK | false | 31901004 | Failed to send the message because the Plus Friend is already registered. |
| FRIENDTALK | false | 31901005 | Failed to send the message because the same 'X-NC-API-IDEMPOTENCY-KEY' was used within the last 10 minutes. |
| FRIENDTALK | false | 31901006 | Failed to send the message because the Plus Friend does not have a senderKey. |
| FRIENDTALK | false | 31901010 | Failed to send the message because the Plus Friend group does not exist. |
| FRIENDTALK | false | 31901013 | Failed to send the message because the Plus Friend group already exists. |
| FRIENDTALK | false | 31901014 | Failed to send the message because the Plus Friend is not in an active state. |
| FRIENDTALK | false | 31901016 | Failed to send the message because no message matching the requestId or recipientSeq could be found. |
| FRIENDTALK | false | 31901017 | Failed to send the message because the daily maximum message count was exceeded. |
| FRIENDTALK | false | 31901018 | Failed to send the message because the Plus Friend has already been added. |
| FRIENDTALK | false | 31901019 | Failed to send the message due to an invalid SMS UnSubscribeno. |
| FRIENDTALK | false | 31901020 | Failed to send the message due to an invalid uuid. |
| FRIENDTALK | false | 31901022 | Failed to send the message because the Plus Friend has not been added to the group. |
| FRIENDTALK | false | 31901023 | Failed to send the message because the maximum Plus Friend group size (10) was exceeded. |
| FRIENDTALK | false | 31901024 | Failed to send the message because a sender group cannot send messages. |
| FRIENDTALK | false | 31901025 | Failed to send the message because a sender group cannot be deleted. |
| FRIENDTALK | false | 31901026 | Failed to send the message because the maximum group member count (5,000) was exceeded. |
| FRIENDTALK | false | 31901027 | Failed to send the message because the sender has been blocked. |
| FRIENDTALK | false | 31901028 | Failed to send the message because the template value exceeds 14 characters. |
| FRIENDTALK | false | 31901029 | Failed to send the message because a blacklisted sender cannot join a group. |
| FRIENDTALK | false | 31901030 | Failed to send the message because identity verification is required. |
| FRIENDTALK | false | 31902000 | Failed to send the message because '{}' must be {} or less. |
| FRIENDTALK | false | 31902001 | Failed to send the message because '{}' cannot be blank. |
| FRIENDTALK | false | 31902002 | Failed to send the message because '{}' cannot be null. |
| FRIENDTALK | false | 31902003 | Failed to send the message because '{}' must be {} or more. |
| FRIENDTALK | false | 31902004 | Failed to send the message because '{}' must be between {} and {}. |
| FRIENDTALK | false | 31902005 | Failed to send the message because '{}' must be {} or less. |
| FRIENDTALK | false | 31902017 | Failed to send the message because the Plus Friend does not exist. |
| FRIENDTALK | false | 31902018 | Failed to send the message because the button parameter is invalid. |
| FRIENDTALK | false | 31902019 | Failed to send the message because the template parameter replacement content exceeds 1,000 characters. |
| FRIENDTALK | false | 31902023 | Failed to send the message because 'content' is too long (up to 400 characters when using an image). |
| FRIENDTALK | false | 31902024 | Failed to send the message because 'content' is too long (up to 1,000 characters when not using an image). |
| FRIENDTALK | false | 31902025 | Failed to send the message because a past date cannot be used for sending. (Check requestDate.) |
| FRIENDTALK | false | 31902026 | Failed to send the message because a date more than 90 days in the future cannot be used for sending. (Check requestDate.) |
| FRIENDTALK | false | 31902027 | Failed to send the message because the 'requestDate' format is invalid. |
| FRIENDTALK | false | 31902028 | Failed to send the message because 'requestId' is invalid. |
| FRIENDTALK | false | 31902029 | Failed to send the message because there is no message to cancel or the conditions are not met. |
| FRIENDTALK | false | 31902030 | Failed to send the message because 'content' is too long (up to 76 characters when using a wide image). |
| FRIENDTALK | false | 31902031 | Failed to send the message because too many 'buttons' were specified (up to 2 when using a wide image). |
| FRIENDTALK | false | 31902032 | Failed to send the message because the templateTitle replaced by template parameters exceeds 50 characters. |
| FRIENDTALK | false | 31902033 | Failed to send the message because the TemplateItem parameter is invalid. |
| FRIENDTALK | false | 31902034 | Failed to send the message because the TemplateItemHighlight parameter is invalid. |
| FRIENDTALK | false | 31902035 | Failed to send the message because templateHeader exceeds 16 characters. |
| FRIENDTALK | false | 31902036 | Failed to send the message because the TemplateRepresentLink parameter is invalid. |
| FRIENDTALK | false | 31902037 | Failed to send the message because 'content' is too long (up to 700 characters when using templateItem). |
| FRIENDTALK | false | 31902500 | Failed to send the message because the bulk message request could not be found. |
| FRIENDTALK | false | 31902501 | Failed to send the message because the delivery request deadline has expired. |
| FRIENDTALK | false | 31902502 | Failed to send the message because the Plus Friend fallback sending configuration is required. |
| FRIENDTALK | false | 31902504 | Failed to send the message because the quickReplies parameter is invalid. |
| FRIENDTALK | false | 31902505 | Failed to send the message because too many 'buttons' were specified (up to 2 when using quickReplies). |
| FRIENDTALK | false | 31903000 | Failed to send the message because the template has a WL (webLink) but linkMo is missing. |
| FRIENDTALK | false | 31903001 | Failed to send the message because templateCode or templateName already exists. |
| FRIENDTALK | false | 31903002 | Failed to send the message because a field is invalid. |
| FRIENDTALK | false | 31903003 | Failed to send the message because the template does not exist. |
| FRIENDTALK | false | 31903004 | Failed to send the message because the template parameter is invalid. |
| FRIENDTALK | false | 31903005 | Failed to send the message because the template status is invalid. (Check whether the status is approved or rejected.) |
| FRIENDTALK | false | 31903006 | Failed to send the message because linkMo/linkPc does not include http:// or https://. |
| FRIENDTALK | false | 31903007 | Failed to send the message because the template has an AL (appLink) but two or more of schemeAndroid, schemeIos, and linkMo are missing. |
| FRIENDTALK | false | 31903008 | Failed to send the message because the button name contains a replacement parameter. |
| FRIENDTALK | false | 31903009 | Failed to send the message due to a non-existent button name. |
| FRIENDTALK | false | 31903010 | Failed to send the message because the content does not match the template. (SMS fallback is available upon resending.) |
| FRIENDTALK | false | 31903011 | Failed to send the message because the button/quickReplies do not match the template. (SMS fallback is available upon resending.) |
| FRIENDTALK | false | 31903012 | Failed to send the message because the template can only be modified when its status is TSC03 (APPROVE) or TSC04 (REJECT). |
| FRIENDTALK | false | 31903013 | Failed to send the message because a template that is already being modified exists. |
| FRIENDTALK | false | 31903014 | Failed to send the message because the button type is invalid. |
| FRIENDTALK | false | 31903015 | Failed to send the message because the use of the CBT feature is not permitted for this Plus Friend. |
| FRIENDTALK | false | 31903016 | Failed to send the message because the template with emphasizeType set to 'TEXT' is missing templateTitle and templateSubtitle. |
| FRIENDTALK | false | 31903017 | Failed to send the message because templateSubtitle contains a replacement parameter. |
| FRIENDTALK | false | 31903018 | The message failed to send because the template with messageType 'EX' does not have templateExtra. |
| FRIENDTALK | false | 31903020 | The message failed to send because the template with messageType 'MI' does not have templateExtra. |
| FRIENDTALK | false | 31903021 | The message failed to send because templateExtra contains a replacement parameter. |
| FRIENDTALK | false | 31903024 | The message failed to send because the AC type button can only be used with templateMessageType (AD/MI), but this condition was violated. |
| FRIENDTALK | false | 31903025 | The message failed to send because the AC type button must be placed alone or at the top, but this condition was violated. |
| FRIENDTALK | false | 31903026 | The message failed to send because the AC type button name does not include the text 'Add Channel'. |
| FRIENDTALK | false | 31903027 | The message failed to send because templateTitle and templateSubtitle exist in a template with emphasizeType 'NONE'. |
| FRIENDTALK | false | 31903028 | The message failed to send because the template with messageType 'BA' has templateExtra. |
| FRIENDTALK | false | 31903030 | The message failed to send because the template with messageType 'AD' has templateExtra. |
| FRIENDTALK | false | 31903032 | The message failed to send because the template with emphasizeType 'IMAGE' does not have templateImageName or templateImageUrl. |
| FRIENDTALK | false | 31903033 | The message failed to send because the specified button/quickReply does not exist in the template. |
| FRIENDTALK | false | 31903034 | The message failed to send because the template cannot be deleted due to a recently sent message. (requestId: {}) |
| FRIENDTALK | false | 31903035 | The message failed to send because the template with emphasizeType 'ITEM_LIST' is missing required fields (templateImageInfo, templateHeader, templateItem, etc.). |
| FRIENDTALK | false | 31903036 | The message failed to send because a template with emphasizeType 'ITEM_LIST' cannot be a security template. |
| FRIENDTALK | false | 31903037 | The message failed to send because the title of templateItem contains a replacement parameter. |
| FRIENDTALK | false | 31903038 | The message failed to send because the summary title of templateItem contains a replacement parameter. |
| FRIENDTALK | false | 31903039 | The message failed to send because a summary cannot exist without a templateItem list. |
| FRIENDTALK | false | 31903040 | The message failed to send because the title (up to 21 characters) or description (up to 13 characters) limit for itemHighlight with a thumbnail was exceeded. |
| FRIENDTALK | false | 31903041 | The message failed to send because imageUrl does not start with http:// or https://. |
| FRIENDTALK | false | 31903042 | The message failed to send because templateHeader does not match the template. (Replaced with SMS on resend) |
| FRIENDTALK | false | 31903043 | The message failed to send because templateItem or templateItemHighlight does not match the template. (Replaced with SMS on resend) |
| FRIENDTALK | false | 31903044 | The message failed to send because the BF type button must be placed at the top, but this condition was violated. |
| FRIENDTALK | false | 31903045 | The message failed to send because the 'BF' link type button requires a bizFormKey and the button name must be one of "Book in Talk", "Survey in Talk", or "Enter in Talk", but this condition was violated. |
| FRIENDTALK | false | 31903046 | The message failed to send because templateRepresentLink does not match the template. (Replaced with SMS on resend) |
| FRIENDTALK | false | 31903047 | The message failed to send because templateTitle or the title of templateItemHighlight ends with a space. |
| FRIENDTALK | false | 31903048 | The message failed to send because the template parameter length exceeds 1,000 characters. |
| FRIENDTALK | false | 31903049 | The message failed to send because the template parameters do not match the template. |
| FRIENDTALK | false | 31903050 | The message failed to send because an AC type button is required for templateMessageType (AD/MI) but is missing. |
| FRIENDTALK | false | 31903100 | The message failed to send because comments cannot be added to a template in the registered/completed status. |
| FRIENDTALK | false | 31903101 | The message failed to send because the quickReply name does not exist. |
| FRIENDTALK | false | 31903102 | The message failed to send because the quickReply name contains a replacement parameter. |
| FRIENDTALK | false | 31903103 | The message failed to send because the button/quickReply format is invalid. |
| FRIENDTALK | false | 31903200 | The message failed to send because the Friend Talk wide item does not have a title. |
| FRIENDTALK | false | 31903201 | The message failed to send because the Friend Talk wide item does not have an image. |
| FRIENDTALK | false | 31903202 | The message failed to send because the Friend Talk wide item does not have linkMo. |
| FRIENDTALK | false | 31903203 | The message failed to send because the Friend Talk wide item does not have 3 to 4 list items and a header. |
| FRIENDTALK | false | 31903204 | The message failed to send because the Friend Talk carousel does not have a header. |
| FRIENDTALK | false | 31903205 | The message failed to send because the Friend Talk carousel does not have a message. |
| FRIENDTALK | false | 31903206 | The message failed to send because the Friend Talk carousel does not have an attachment. |
| FRIENDTALK | false | 31903207 | The message failed to send because the Friend Talk carousel does not have an image. |
| FRIENDTALK | false | 31903208 | The message failed to send because the number of Friend Talk carousel items is invalid (2 to 10 items, or 1 to 10 items when commerce and intro are included). |
| FRIENDTALK | false | 31903209 | The message failed to send because the Friend Talk carousel tail does not have linkMo. |
| FRIENDTALK | false | 31903210 | The message failed to send because the Friend Talk coupon does not have a title or description. |
| FRIENDTALK | false | 31903211 | The message failed to send because the coupon description in a text/image type Friend Talk message exceeds the limit (up to 12 characters by default; up to 18 characters for wide-image/wide-item-list). |
| FRIENDTALK | false | 31903212 | The message failed to send because the Friend Talk coupon title is invalid. |
| FRIENDTALK | false | 31903213 | The message failed to send because Friend Talk does not have a mobile link or an iOS/Android channel link. |
| FRIENDTALK | false | 31903215 | The message failed to send because Friend Talk wide items/carousels can only be sent as the AD type, but this condition was violated. |
| FRIENDTALK | false | 31903216 | The message failed to send because the title limit for the first wide item (up to 25 characters) or for wide items 2 through 4 (up to 30 characters) was exceeded. |
| FRIENDTALK | false | 31903217 | The message failed to send because the number of Friend Talk buttons is invalid (up to 5 by default; up to 4 with a coupon; up to 2 with wide; up to 1 with video; 1 to 2 with commerce). |
| FRIENDTALK | false | 31903218 | The message failed to send because the Friend Talk video URL is invalid. |
| FRIENDTALK | false | 31903219 | The message failed to send because 'content' is too long (up to 76 characters when video is used). |
| FRIENDTALK | false | 31903220 | The message failed to send because 'header' is too long (up to 20 characters when video is used). |
| FRIENDTALK | false | 31903221 | The message failed to send because the Friend Talk carousel (feed type) cannot include a 'head' field. |
| FRIENDTALK | false | 31903222 | The message failed to send because the Friend Talk carousel (feed type) cannot include an 'additionalContent' field. |
| FRIENDTALK | false | 31903223 | The message failed to send because the Friend Talk carousel (feed type) cannot include a 'commerce' field. |
| FRIENDTALK | false | 31903224 | The message failed to send because the Friend Talk carousel (commerce type) has 'header' and 'message' fields. |
| FRIENDTALK | false | 31903225 | The message failed to send because the number of Friend Talk carousel buttons is invalid (up to 2 for feed; 1 to 2 for commerce). |
| FRIENDTALK | false | 31903226 | The message failed to send because 'discountRate' or 'discountFixed' is required when 'discountPrice' is present in commerce, but it is missing. |
| FRIENDTALK | false | 31903300 | The message failed to send because the opt-out number could not be found. |
| FRIENDTALK | false | 31903301 | The message failed to send because the opted-out recipient could not be found. |
| FRIENDTALK | false | 31903302 | The message failed to send because marketing consent messages can only be sent as text, image, wide image, carousel feed, or premium video types. |
| FRIENDTALK | false | 31904000 | The message failed to send due to an invalid parameter. |
| FRIENDTALK | false | 31904001 | The message failed to send because the appkey is already activated. |
| FRIENDTALK | false | 31904002 | The message failed to send because the appkey is deactivated. |
| FRIENDTALK | false | 31904003 | The message failed to send because searches are only available within the last 31 days. |
| FRIENDTALK | false | 31904004 | The message failed to send because the appkey does not exist. |
| FRIENDTALK | false | 31904005 | The message failed to send because the appkey is deactivated. |
| FRIENDTALK | false | 31904006 | The message failed to send because the appkey does not have a sender key. |
| FRIENDTALK | false | 31904007 | The message failed to send because the file size is less than {}. |
| FRIENDTALK | false | 31904008 | The message failed to send because the file size exceeds the limit of 20 MB. |
| FRIENDTALK | false | 31904009 | The message failed to send because the file extension is invalid. |
| FRIENDTALK | false | 31904010 | The message failed to send because the file could not be found. |
| FRIENDTALK | false | 31904011 | The message failed to send because the recipient list could not be found. |
| FRIENDTALK | false | 31904012 | The message failed to send because the number of recipients exceeds the maximum limit of 10,000. |
| FRIENDTALK | false | 31904013 | The message failed to send because only jpg/jpeg extensions can be uploaded. |
| FRIENDTALK | false | 31904014 | The message failed to send because the file does not have a recipient_no header. |
| FRIENDTALK | false | 31904015 | The message failed to send because the requestId is invalid. |
| FRIENDTALK | false | 31904016 | The message failed to send because the data does not exist. |
| FRIENDTALK | false | 31904017 | The message failed to send because messages older than 90 days cannot be searched. |
| FRIENDTALK | false | 31904018 | The message failed to send due to an attachment upload error. |
| FRIENDTALK | false | 31904019 | The message failed to send due to an invalid recipient number. |
| FRIENDTALK | false | 31904020 | The message failed to send because the file could not be read. |
| FRIENDTALK | false | 31904021 | The message failed to send because the file size exceeds the limit of 10 MB. |
| FRIENDTALK | false | 31904022 | The message could not be sent because data export failed. |
| FRIENDTALK | false | 31904023 | The message failed to send because all senders must be deleted before deactivating the product, but this condition was not met. |
| FRIENDTALK | false | 31904024 | The message could not be sent because the dormant template could not be reactivated. |
| FRIENDTALK | false | 31904025 | The message failed to send because only up to 20 templates can be uploaded at a time. |
| FRIENDTALK | false | 31904026 | The message failed to send because the uploaded template header is invalid. |
| FRIENDTALK | false | 31904027 | The message failed to send because the AD/MI type conversion failed: the length of 'buttons' exceeds the maximum limit. |
| FRIENDTALK | false | 31904028 | The message failed to send because the AD/MI type conversion failed: the template is not in the approved status. |
| FRIENDTALK | false | 31904101 | The message failed to send due to an invalid search parameter. |
| FRIENDTALK | false | 31904103 | The message failed to send because the RequestId or startRequestDate/endRequestDate is invalid. |
| FRIENDTALK | false | 31904104 | The message failed to send because the RequestId is empty. |
| FRIENDTALK | false | 31904200 | The message failed to send because the resend message is invalid. |
| FRIENDTALK | false | 31905000 | The message failed to send due to an invalid RecipientNo. |
| FRIENDTALK | false | 31907000 | The message failed to send due to a vendor API request failure. |
| FRIENDTALK | false | 31908000 | The message failed to send because 'imageSeq' is empty. |
| FRIENDTALK | false | 31908001 | The message failed to send because the uploaded image is invalid. |
| FRIENDTALK | false | 31908002 | The message failed to send because the image could not be found. (carousel-feed type requires a carousel type image; carousel-commerce type requires a commerce type image; commerce requires an IMAGE type image) |
| FRIENDTALK | false | 31908003 | The message could not be sent because the image deletion failed. |
| FRIENDTALK | false | 31908004 | The message failed to send because the length of 'createUser' exceeds 100 characters. |
| FRIENDTALK | false | 31908005 | The message failed to send because the project does not have a PlusFriend. (Registration is required first.) |
| FRIENDTALK | false | 31908006 | The message failed to send because the content does not include authentication guidance. |
| FRIENDTALK | false | 31908007 | The message failed to send because the storage configuration is empty. |
| FRIENDTALK | false | 31908008 | The message failed to send because it contains a prohibited word. |
| FRIENDTALK | false | 31908009 | The message failed to send because this project is already shared. |
| FRIENDTALK | false | 31908010 | The message failed to send because the image upload failed due to an unexpected error. |
| FRIENDTALK | false | 31908011 | The message failed to send because the image type is invalid. |
| FRIENDTALK | false | 31909993 | The message failed to send because a required part of the request is missing. |
| FRIENDTALK | false | 31909994 | The message failed to send because the method argument type is different from what was expected. |
| FRIENDTALK | false | 31909995 | The message failed to send because the version is no longer supported. |
| FRIENDTALK | false | 31909996 | The message failed to send because only application/json is supported. |
| FRIENDTALK | false | 31909997 | The message failed to send due to a client error. |
| FRIENDTALK | false | 31909998 | The message failed to send because the API does not exist. |
| FRIENDTALK | false | 32000002 | The message failed to send because an error occurred while processing the sequential flow delivery. |
| FRIENDTALK | false | 32000003 | The message failed to send because an error occurred while preparing to send the message. |
| FRIENDTALK | false | 32909999 | Message sending failed due to a system error. |
| FRIENDTALK | false | 33001001 | Message sending failed because the request body is not in JSON format. |
| FRIENDTALK | false | 33001002 | Message sending failed because the hub partner key is invalid. |
| FRIENDTALK | false | 33001003 | Message sending failed because the sender profile key is invalid. |
| FRIENDTALK | false | 33001004 | Message sending failed because the name field is missing from the request body (JSON). |
| FRIENDTALK | false | 33001006 | Message sending failed due to a deleted sender profile (contact customer support). |
| FRIENDTALK | false | 33001007 | Message sending failed due to a blocked sender profile (contact customer support). |
| FRIENDTALK | false | 33001011 | Message sending failed because contract information could not be found (contact customer support). |
| FRIENDTALK | false | 33001012 | Message sending failed due to an invalid user key format in the request. |
| FRIENDTALK | false | 33001013 | Message sending failed due to an invalid app connection. |
| FRIENDTALK | false | 33001014 | Message sending failed due to an invalid business registration number. |
| FRIENDTALK | false | 33001015 | Message sending failed due to an invalid app user ID in the request. |
| FRIENDTALK | false | 33001016 | Message sending failed due to a business registration number mismatch. |
| FRIENDTALK | false | 33001020 | Message sending failed because the phone number or app user ID is invalid or missing. |
| FRIENDTALK | false | 33001021 | Message sending failed because the KakaoTalk channel is in a blocked state. |
| FRIENDTALK | false | 33001022 | Message sending failed because the KakaoTalk channel is in a closed state. |
| FRIENDTALK | false | 33001023 | Message sending failed because the KakaoTalk channel has been deleted. |
| FRIENDTALK | false | 33001024 | Message sending failed because the KakaoTalk channel is pending deletion. |
| FRIENDTALK | false | 33001025 | Message sending failed because the channel is under sanctions. |
| FRIENDTALK | false | 33001027 | Message sending failed because the channel message is under sanctions. |
| FRIENDTALK | false | 33001030 | Message sending failed due to an invalid parameter in the request. |
| FRIENDTALK | false | 33002001 | Message sending failed because sending is unavailable (unexpected error). |
| FRIENDTALK | false | 33002003 | Message sending failed because the KakaoTalk channel has not been added on the test server. |
| FRIENDTALK | false | 33002005 | Message sending failed because image information could not be loaded due to an internal Kakao system error. |
| FRIENDTALK | false | 33003000 | Message sending failed due to an unexpected error. |
| FRIENDTALK | false | 33003005 | Message sending failed because the message was sent but delivery could not be confirmed (success uncertain). |
| FRIENDTALK | false | 33003006 | Message sending failed due to an internal system error. |
| FRIENDTALK | false | 33003008 | Message sending failed due to a phone number error. |
| FRIENDTALK | false | 33003010 | Message sending failed due to an unexpected error. |
| FRIENDTALK | false | 33003011 | Message sending failed because the message does not exist. |
| FRIENDTALK | false | 33003012 | Message sending failed due to a Kakao communication failure. |
| FRIENDTALK | false | 33003013 | Message sending failed because the message is empty. |
| FRIENDTALK | false | 33003014 | Message sending failed due to a message length limit error. |
| FRIENDTALK | false | 33003015 | Message sending failed because the template could not be found. |
| FRIENDTALK | false | 33003016 | Message sending failed because the message content does not match the template. |
| FRIENDTALK | false | 33003018 | Message sending failed because the message cannot be sent. (Possible causes include a mismatch between the SIM card number and the KakaoTalk number on Android devices, the user is not active, or the user is under sanctions.) |
| FRIENDTALK | false | 33003019 | Message sending failed because the recipient is not a KakaoTalk user. |
| FRIENDTALK | false | 33003020 | Message sending failed because the recipient has blocked Alim Talk notifications. |
| FRIENDTALK | false | 33003021 | Message sending failed because the minimum required version of KakaoTalk is not supported. |
| FRIENDTALK | false | 33003022 | Message sending failed because it is outside the allowed sending hours (FriendTalk is available from 8:00 AM to 8:50 PM). |
| FRIENDTALK | false | 33003023 | Message sending failed due to a message syntax error (JSON format). |
| FRIENDTALK | false | 33003024 | Message sending failed because the image included in the message cannot be sent (invalid URL/link or specification violation). |
| FRIENDTALK | false | 33003025 | Message sending failed because the variable character limit has been exceeded. |
| FRIENDTALK | false | 33003026 | Message sending failed because the character limit for the consultation/bot switch button (extra, event) has been exceeded. |
| FRIENDTALK | false | 33003027 | Message sending failed because the message button/quick link does not match the template. |
| FRIENDTALK | false | 33003028 | Message sending failed because the message emphasis title does not match the template. |
| FRIENDTALK | false | 33003029 | Message sending failed because the message emphasis title exceeds the character limit (50 characters). |
| FRIENDTALK | false | 33003030 | Message sending failed because the message type does not match the template emphasis type. |
| FRIENDTALK | false | 33003031 | Message sending failed because the header does not match the template. |
| FRIENDTALK | false | 33003032 | Message sending failed because the header exceeds the character limit (16 characters). |
| FRIENDTALK | false | 33003033 | Message sending failed because the item highlight does not match the template. |
| FRIENDTALK | false | 33003034 | Message sending failed because the item highlight title exceeds the character limit (30 characters without an image / 21 characters with an image). |
| FRIENDTALK | false | 33003035 | Message sending failed because the item highlight description exceeds the character limit (19 characters without an image / 13 characters with an image). |
| FRIENDTALK | false | 33003036 | Message sending failed because the item list does not match the template. |
| FRIENDTALK | false | 33003037 | Message sending failed because the item list description exceeds the character limit (23 characters). |
| FRIENDTALK | false | 33003038 | Message sending failed because the item summary does not match the template. |
| FRIENDTALK | false | 33003039 | Message sending failed because the item summary description exceeds the character limit (14 characters). |
| FRIENDTALK | false | 33003040 | Message sending failed because the item summary description contains disallowed characters. |
| FRIENDTALK | false | 33003041 | Message sending failed because the wide item list count is out of the allowed range. |
| FRIENDTALK | false | 33003042 | Message sending failed because the representative link does not match the template. |
| FRIENDTALK | false | 33003046 | Message sending failed due to an additional information length limit error. |
| FRIENDTALK | false | 33003047 | Message sending failed due to a commerce information product name length limit error. |
| FRIENDTALK | false | 33003048 | Message sending failed due to an invalid group tag key. |
| FRIENDTALK | false | 33003051 | Message sending failed because the carousel item list count is out of the allowed range. |
| FRIENDTALK | false | 33003052 | Message sending failed because the carousel item message exceeds the length limit. |
| FRIENDTALK | false | 33003056 | Message sending failed due to a wide item list title length limit error. |
| FRIENDTALK | false | 33003058 | Message sending failed due to a carousel header length limit error. |
| FRIENDTALK | false | 33004000 | Message sending failed because the message sending result could not be found. |
| FRIENDTALK | false | 33004001 | Message sending failed due to an unknown message status. |
| FRIENDTALK | false | 33009998 | A system issue has occurred and is being investigated by the responsible team (service is currently unavailable). Message sending is not possible. |
| FRIENDTALK | false | 33009999 | Message sending failed due to an unknown system error. (Being investigated by the responsible team.) |
| RCS | false | 41903004 | Message sending failed due to an invalid statsKeyId. |
| RCS | false | 41904000 | Message sending failed because the brand does not exist. |
| RCS | false | 41904001 | Message sending failed because the brand status is invalid. |
| RCS | false | 41904010 | Message sending failed because the chatbot does not exist. |
| RCS | false | 41904011 | Message sending failed because the chatbot status is invalid. |
| RCS | false | 41904020 | Message sending failed because the template does not exist. |
| RCS | false | 41904021 | Message sending failed because the template status is invalid. |
| RCS | false | 41904022 | Message sending failed due to an unsupported template. |
| RCS | false | 41904023 | Message sending failed because the template does not allow advertising. |
| RCS | false | 41904024 | Message sending failed because template parameter input is missing. |
| RCS | false | 41904025 | Message sending failed because the free template body length has been exceeded. |
| RCS | false | 41904040 | Message sending failed because the block service does not exist. |
| RCS | false | 41904041 | Message sending failed because the block service status is invalid. |
| RCS | false | 41904042 | Message sending failed due to a blocked recipient number. |
| RCS | false | 41909000 | Message sending failed due to nighttime advertising sending time restrictions. |
| RCS | false | 42000002 | Message sending failed due to an error during flow sequential sending processing. |
| RCS | false | 42000003 | Message sending failed due to an error during message sending preparation. |
| RCS | false | 42099999 | Message sending failed due to an internal server error (sender). |
| RCS | false | 42909999 | Message sending failed due to an internal server error (batch). |
| RCS | false | 43072101 | Message sending failed because a parameter is missing. |
| RCS | false | 43072102 | Message sending failed due to a parameter range error. |
| RCS | false | 43072103 | Message sending failed due to a parameter format error. |
| RCS | false | 43072104 | Message sending failed due to an invalid parameter. |
| RCS | false | 43072108 | Message sending failed due to a duplicate request. |
| RCS | false | 43072109 | Message sending failed due to an invalid or expired file. |
| RCS | false | 43072114 | Message sending failed due to a parameter size error. |
| RCS | false | 43072115 | Message sending failed due to a disallowed parameter. |
| RCS | false | 43072116 | Message sending failed due to a disallowed parameter. |
| RCS | false | 43079999 | Message sending failed due to another error. |
| RCS | false | 46040001 | Message sending failed because the Authorization header is missing. |
| RCS | false | 46040002 | Message sending failed because the token is missing. |
| RCS | false | 46040003 | Message sending failed due to an invalid token. |
| RCS | false | 46040004 | Message sending failed because the token has expired. |
| RCS | false | 46040005 | Message sending failed because the token payload is invalid. |
| RCS | false | 46040006 | Message sending failed due to an invalid client ID. |
| RCS | false | 46040007 | Message sending failed because the permission scope is insufficient. |
| RCS | false | 46041000 | Message sending failed due to an internal server error. |
| RCS | false | 46041001 | Message sending failed due to an RCS request timeout. |
| RCS | false | 46041003 | Message sending failed due to a message sending rate limit. |
| RCS | false | 46041004 | Message sending failed because the RCS server is busy. |
| RCS | false | 46041005 | Message sending failed because the RCS server is temporarily unavailable. |
| RCS | false | 46041006 | Message sending failed because the session does not exist. |
| RCS | false | 46041007 | Message sending failed due to cancellation (cancel processing). |
| RCS | false | 46041008 | Message sending failed because the session has already expired. |
| RCS | false | 46041100 | Message sending failed due to a SUBSCRIBE timeout. |
| RCS | false | 46041101 | Message sending failed because the user could not be found. |
| RCS | false | 46041108 | Message sending failed due to a failure during message request processing. |
| RCS | false | 46041200 | Message sending failed because the target user for message delivery could not be found. |
| RCS | false | 46041201 | Message sending failed because message delivery is not allowed. |
| RCS | false | 46041202 | Message sending failed because the message has already been canceled. |
| RCS | false | 46041250 | Message sending failed because the message content type could not be retrieved. |
| RCS | false | 46042001 | Message sending failed due to an invalid status. |
| RCS | false | 46042002 | Message sending failed due to an invalid message. |
| RCS | false | 46042003 | Message sending failed due to an invalid date/time format. |
| RCS | false | 46042004 | Message sending failed because the contact is missing. |
| RCS | false | 46042005 | Message sending failed due to an invalid contact. |
| RCS | false | 46042006 | Message sending failed due to emulator-only access. |
| RCS | false | 46042007 | Message sending failed because the contact is not on the whitelist. |
| RCS | false | 46042008 | Message sending failed because the message content is missing. |
| RCS | false | 46042009 | Message sending failed due to invalid message content. |
| RCS | false | 46042010 | Message sending failed because the message is ambiguous. |
| RCS | false | 46042011 | Message sending failed due to an invalid message status. |
| RCS | false | 46042012 | Message sending failed due to an invalid isTyping status. |
| RCS | false | 46042013 | Message sending failed due to an invalid traffic type. |
| RCS | false | 46042014 | Message sending failed due to an invalid suggested chip list association. |
| RCS | false | 46042015 | Message sending failed because the text message is empty. |
| RCS | false | 46042031 | Message sending failed because the rich card is missing. |
| RCS | false | 46042032 | Message sending failed because the rich card is ambiguous. |
| RCS | false | 46042033 | Message sending failed because there are too many rich cards. |
| RCS | false | 46042034 | Message sending failed because the rich card layout is missing. |
| RCS | false | 46042035 | Message sending failed because the rich card content is missing. |
| RCS | false | 46042036 | Message sending failed due to an invalid card orientation. |
| RCS | false | 46042037 | Message sending failed because the image alignment is missing. |
| RCS | false | 46042038 | Message sending failed due to an invalid image alignment. |
| RCS | false | 46042039 | Message sending failed due to duplicate image alignment. |
| RCS | false | 46042040 | Failed to send the message due to an invalid rich card carousel cardWidth. |
| RCS | false | 46042041 | Failed to send the message due to a media height mismatch. |
| RCS | false | 46042042 | Failed to send the message due to invalid rich card content. |
| RCS | false | 46042043 | Failed to send the message due to invalid suggestions. |
| RCS | false | 46042044 | Failed to send the message because the chip list contains too many suggestions (maximum 11). |
| RCS | false | 46042045 | Failed to send the message due to an invalid suggestion. |
| RCS | false | 46042046 | Failed to send the message because the suggestion is ambiguous. |
| RCS | false | 46042047 | Failed to send the message because the suggested action is ambiguous. |
| RCS | false | 46042048 | Failed to send the message because the rich card contains too many suggestions (maximum 4). |
| RCS | false | 46042049 | Failed to send the message because the suggestion data is too large (maximum 2,048). |
| RCS | false | 46042050 | Failed to send the message due to an invalid action. |
| RCS | false | 46042051 | Failed to send the message due to invalid location information. |
| RCS | false | 46042052 | Failed to send the message because the location information is ambiguous. |
| RCS | false | 46042053 | Failed to send the message due to an invalid map action. |
| RCS | false | 46042054 | Failed to send the message because the map action is ambiguous. |
| RCS | false | 46042055 | Failed to send the message due to an invalid dial action. |
| RCS | false | 46042056 | Failed to send the message because the dial action is ambiguous. |
| RCS | false | 46042057 | Failed to send the message due to an invalid compose action. |
| RCS | false | 46042058 | Failed to send the message because the compose action is ambiguous. |
| RCS | false | 46042059 | Failed to send the message due to an invalid settings action. |
| RCS | false | 46042060 | Failed to send the message because the settings action is ambiguous. |
| RCS | false | 46042061 | Failed to send the message due to an invalid clipboard action. |
| RCS | false | 46042062 | Failed to send the message because localBrowserAction is missing. |
| RCS | false | 46042063 | Failed to send the message due to an invalid share action. |
| RCS | false | 46042064 | Failed to send the message because CalendarAction is missing. |
| RCS | false | 46042065 | Failed to send the message due to an invalid CalendarAction. |
| RCS | false | 46042066 | Failed to send the message because the CalendarAction title is out of range (1,100 characters). |
| RCS | false | 46042067 | Failed to send the message because the CalendarAction description is out of range (1,500 characters). |
| RCS | false | 46042068 | Failed to send the message because ComposeAction is missing a phone number or the text is out of range (between 1 and 100 characters). |
| RCS | false | 46042069 | Failed to send the message because the ComposeAction voice/video recording message is missing a phone number or has an invalid type (AUDIO/VIDEO). |
| RCS | false | 46042070 | Failed to send the message because DeviceAction is missing. |
| RCS | false | 46042071 | Failed to send the message because the dial action is missing a phone number or the title exceeds the maximum length (60). |
| RCS | false | 46042072 | Failed to send the message because the location to display for the map action is missing. |
| RCS | false | 46042073 | Failed to send the message because urlAction openUrl is missing. |
| RCS | false | 46042100 | Failed to send the message due to an invalid thumbnail. |
| RCS | false | 46042101 | Failed to send the message because fileUrl is missing. |
| RCS | false | 46042102 | Failed to send the message because the audio fileUrl is missing. |
| RCS | false | 46042103 | Failed to send the message because pos is missing. |
| RCS | false | 46042104 | Failed to send the message because media information is missing. |
| RCS | false | 46042105 | Failed to send the message because media information is missing. |
| RCS | false | 46042106 | Failed to send the message because media information is missing. |
| RCS | false | 46042107 | Failed to send the message because media information is missing. |
| RCS | false | 46042108 | Failed to send the message because postback data is missing. |
| RCS | false | 46042200 | Failed to send the message due to an invalid URI format. |
| RCS | false | 46042201 | Failed to send the message due to an invalid location. |
| RCS | false | 46042202 | Failed to send the message because the media content description is invalid. |
| RCS | false | 46042203 | Failed to send the message due to an invalid media title. |
| RCS | false | 46042204 | Failed to send the message due to an invalid media description. |
| RCS | false | 46042205 | Failed to send the message because the rich card carousel contains too much content. |
| RCS | false | 46042206 | Failed to send the message due to an invalid media file size. |
| RCS | false | 46042207 | Failed to send the message because the expiration time format is invalid. |
| RCS | false | 46042208 | Failed to send the message due to an invalid expiration time. |
| RCS | false | 46042301 | Failed to send the message because Openrichcard is ambiguous. |
| RCS | false | 46042302 | Failed to send the message because Openrichcard is missing. |
| RCS | false | 46042303 | Failed to send the message because the Openrichcard Layout Widget is missing. |
| RCS | false | 46042304 | Failed to send the message because Openrichcard View content is missing. |
| RCS | false | 46042305 | Failed to send the message because Openrichcard LinearLayout content is missing. |
| RCS | false | 46042306 | Failed to send the message because Openrichcard Textview content is missing. |
| RCS | false | 46042307 | Failed to send the message because Openrichcard Textview content is invalid. |
| RCS | false | 46042308 | Failed to send the message due to an Openrichcard Textview text length error. |
| RCS | false | 46042309 | Failed to send the message because Openrichcard Imageview content is missing. |
| RCS | false | 46042310 | Failed to send the message because the Openrichcard Imageview media size is too small. |
| RCS | false | 46042311 | Failed to send the message because the Openrichcard Imageview Scaletype is invalid. |
| RCS | false | 46042312 | Failed to send the message because the Openrichcard width/height is missing. |
| RCS | false | 46042313 | Failed to send the message because the Openrichcard width/height is invalid. |
| RCS | false | 46042314 | Failed to send the message because the Openrichcard common content is invalid. |
| RCS | false | 46042315 | Failed to send the message because the Openrichcard contains too many child elements. |
| RCS | false | 46042401 | Failed to send the message due to an invalid file type. |
| RCS | false | 46042402 | Failed to send the message due to a download failure. |
| RCS | false | 46042501 | Failed to send the message because the contact is missing. |
| RCS | false | 46042502 | Failed to send the message because the content is missing. |
| RCS | false | 46042503 | Failed to send the message because the title is missing. |
| RCS | false | 46042504 | Failed to send the message because the description is missing. |
| RCS | false | 46042505 | Failed to send the message because the image URL is missing. |
| RCS | false | 46042506 | Failed to send the message because the image type is missing. |
| RCS | false | 46042507 | Failed to send the message because the button link is missing. |
| RCS | false | 46042508 | Failed to send the message because the button text is missing. |
| RCS | false | 46042509 | Failed to send the message due to an invalid title. |
| RCS | false | 46042510 | Failed to send the message due to an invalid description. |
| RCS | false | 46042511 | Failed to send the message due to an invalid image URL. |
| RCS | false | 46042512 | Failed to send the message due to an invalid button URL. |
| RCS | false | 46042513 | Failed to send the message due to invalid button text. |
| RCS | false | 46042514 | Failed to send the message because the message ID is duplicated. |
| RCS | false | 46042601 | Failed to send the message because there are too many requests. |
| RCS | false | 46042602 | Failed to send the message because the message was filtered. |
| RCS | false | 46045000 | Failed to send the message due to an internal server error. |
| RCS | false | 46045001 | Failed to send the message due to a bot data processing error. |
| RCS | false | 46045002 | Failed to send the message due to a feature data processing error. |
| RCS | false | 46045003 | Failed to send the message due to an XML data processing error. |
| RCS | false | 46045004 | Failed to send the message due to a failure to access the message information cache. |
| RCS | false | 46045005 | Failed to send the message due to a failure to access the chat information cache. |
| RCS | false | 46045006 | Failed to send the message due to a failure to create an HTTP client for the MaaP registry. |
| RCS | false | 46045007 | Failed to send the message due to a failure to create an HTTP client for the bot. |
| RCS | false | 46050000 | Failed to send the message because it matches the new specification. (Internal reason) |
| RCS | false | 46050001 | Failed to send the message because the Authorization header is missing. |
| RCS | false | 46050002 | Failed to send the message because the token is missing. |
| RCS | false | 46050003 | Failed to send the message due to an invalid token. |
| RCS | false | 46050004 | Failed to send the message because the token has expired. |
| RCS | false | 46050005 | Failed to send the message due to an authentication error. |
| RCS | false | 46050006 | Failed to send the message due to an invalid client ID. |
| RCS | false | 46050007 | Failed to send the message due to an invalid sender ID. |
| RCS | false | 46050008 | Failed to send the message due to an invalid password. |
| RCS | false | 46050009 | Failed to send the message because the IP address is not allowed. |
| RCS | false | 46050010 | Unable to send the message due to an unpaid balance. |
| RCS | false | 46050011 | Failed to send the message due to an agency product permission error. |
| RCS | false | 46050012 | Failed to send the message due to an agency API permission error. |
| RCS | false | 46050100 | Failed to send the message due to an invalid status. |
| RCS | false | 46050101 | Failed to send the message because it is forbidden. |
| RCS | false | 46050201 | Failed to send the message because the message TPS limit has been exceeded. |
| RCS | false | 46050202 | Failed to send the message because the message quota has been exceeded. |
| RCS | false | 46051003 | Failed to send the message due to a duplicate error. |
| RCS | false | 46051004 | Failed to send the message due to a parameter error. |
| RCS | false | 46051005 | Failed to send the message due to a JSON parsing error. |
| RCS | false | 46051006 | Failed to send the message because no data exists. |
| RCS | false | 46051101 | Failed to send the message because the agency key could not be found. |
| RCS | false | 46051102 | Failed to send the message due to an invalid agency key. |
| RCS | false | 46051103 | Failed to send the message because the brand key could not be found. |
| RCS | false | 46051104 | Failed to send the message due to an invalid brand key. |
| RCS | false | 46051900 | Failed to send the message because the handler could not be found. |
| RCS | false | 46051901 | Failed to send the message due to a Samsung MaaP Connect IF error. |
| RCS | false | 46051902 | Failed to send the message due to a Samsung MaaP Service IF error. |
| RCS | false | 46051903 | Failed to send the message due to a Capri IF error. |
| RCS | false | 46051904 | Failed to send the message because the webhook is in an unexecutable state. |
| RCS | false | 46051905 | Failed to send the message due to a failure to record the webhook CDR log. |
| RCS | false | 46051906 | Failed to send the message due to an invalid webhook URL. |
| RCS | false | 46051907 | Failed to send the message because the webhook message has expired. |
| RCS | false | 46051908 | Failed to send the message because the message retry count has been exceeded. |
| RCS | false | 46051909 | Failed to send the message because the webhook message does not exist. |
| RCS | false | 46051910 | Failed to send the message because the webhook GW vendor does not exist. |
| RCS | false | 46051911 | Failed to send the message because there is no subscription. |
| RCS | false | 46051912 | Failed to send the message due to a webhook sending pre-preparation failure. |
| RCS | false | 46051913 | Failed to send the message due to a failure to update the webhook sending result status. |
| RCS | false | 46051914 | Failed to send the message due to a failure to update the CDR result status. |
| RCS | false | 46051915 | Failed to send the message due to a failure to update the completion result status. |
| RCS | false | 46051916 | Failed to send the message due to a failure to update the expiration result status. |
| RCS | false | 46051917 | Failed to send the message due to a webhook message log creation error. |
| RCS | false | 46051918 | Failed to send the message due to a webhook message log creation failure. |
| RCS | false | 46051919 | Failed to send the message due to an invalid webhook receive request. |
| RCS | false | 46051920 | Failed to send the message because no chatbot exists for the request. |
| RCS | false | 46051921 | Failed to send the message due to a chatbot error in an unavailable state. |
| RCS | false | 46051922 | Failed to send the message because no GW vendor exists for the request. |
| RCS | false | 46051923 | Failed to send the message because the MO message URL is not defined in the chatbot. |
| RCS | false | 46051924 | Failed to send the message due to a webhook gateway execution error. |
| RCS | false | 46051925 | Failed to send the message due to a disallowed request event error. |
| RCS | false | 46051926 | Failed to send the message due to a webhook receive execution error. |
| RCS | false | 46051927 | Failed to send the message due to a webhook asynchronous receive execution error. |
| RCS | false | 46051928 | Failed to send the message because the webhook URL for the GW vendor Cid is not defined. |
| RCS | false | 46051929 | Failed to send the message because the GW vendor is not a CDR log target. |
| RCS | false | 46051930 | Failed to send the message due to an unreceived webhook command error log. |
| RCS | false | 46051931 | Failed to send the message due to an MO message registration error. |
| RCS | false | 46051932 | Failed to send the message due to an MO message registration failure. |
| RCS | false | 46051933 | Failed to send the message due to an auto-reply message sending error. |
| RCS | false | 46051934 | Failed to send the message due to an unsupported service error. |
| RCS | false | 46051935 | Failed to send the message due to a Samsung MaaP Core file server connection error. |
| RCS | false | 46051936 | Failed to send the message due to a file download error in the message FileMessage event. |
| RCS | false | 46051937 | Failed to send the message due to a message FileMessage event file download error. |
| RCS | false | 46051938 | Failed to send the message due to a message FileMessage DB registration error. |
| RCS | false | 46051939 | Failed to send the message due to a message FileMessage DB registration error. |
| RCS | false | 46051950 | Failed to send the message due to a webhook scheduler asynchronous execution error. |
| RCS | false | 46051951 | Failed to send the message due to a webhook scheduler DB execution error. |
| RCS | false | 46051952 | Failed to send the message due to a webhook scheduler DB execution failure. |
| RCS | false | 46051953 | Failed to send the message due to a webhook scheduler process execution error. |
| RCS | false | 46051954 | Failed to send the message due to a webhook scheduler process execution failure. |
| RCS | false | 46051955 | Failed to send the message due to a webhook scheduler processor execution error. |
| RCS | false | 46051956 | Failed to send the message due to a webhook scheduler processor execution failure. |
| RCS | false | 46051957 | Failed to send the message due to a non-existent MO message error. |
| RCS | false | 46051958 | Failed to send the message due to an undefined webhook scheduler type error. |
| RCS | false | 46052001 | Failed to send the message due to an invalid phone number format. |
| RCS | false | 46052002 | Failed to send the message due to an invalid message status. |
| RCS | false | 46052003 | Failed to send the message because the bot already exists. |
| RCS | false | 46052004 | Failed to send the message due to a bot creation failure. |
| RCS | false | 46052005 | Failed to send the message due to a bot update failure. |
| RCS | false | 46052006 | Failed to send the message due to a brand deletion failure. |
| RCS | false | 46052007 | Failed to send the message due to an invalid chatbot service type. |
| RCS | false | 46052008 | Failed to send the message due to a chatbot ID mismatch. |
| RCS | false | 46052009 | Failed to send the message due to invalid chatbot data. |
| RCS | false | 46052010 | Failed to send the message due to an invalid bot agency. |
| RCS | false | 46052011 | Failed to send the message because the bot agency is missing. |
| RCS | false | 46052012 | Failed to send the message due to invalid persistent menu data. |
| RCS | false | 46052016 | Failed to send the message because the message send time has expired. |
| RCS | false | 46052023 | Failed to send the message because the message base ID is suspended. |
| RCS | false | 46052098 | Failed to send the message due to a non-editable field. |
| RCS | false | 46052099 | Failed to send the message due to a non-editable chatbot. |
| RCS | false | 46052108 | Failed to send the message due to a response event Postback statistics log DB error. |
| RCS | false | 46052109 | Failed to send the message due to a response event Postback statistics log DB failure. |
| RCS | false | 46053001 | Failed to send the message due to an invalid file type. |
| RCS | false | 46053002 | Failed to send the message due to a file attribute error. |
| RCS | false | 46053003 | Failed to send the message due to a file ID format error. |
| RCS | false | 46053004 | Failed to send the message due to a file upload error. |
| RCS | false | 46053005 | Failed to send the message due to an invalid multipart request. |
| RCS | false | 46053006 | Failed to send the message due to an attachment file size error. |
| RCS | false | 46053007 | Failed to send the message due to a file information extraction error. |
| RCS | false | 46053008 | Failed to send the message due to a file size format error. |
| RCS | false | 46054001 | Failed to send the message due to an invalid contact user number. |
| RCS | false | 46054002 | Failed to send the message because RCS is not supported. |
| RCS | false | 46054003 | Failed to send the message because it cannot be delivered to the recipient. |
| RCS | false | 46054004 | Failed to send the message due to an internal server error. |
| RCS | false | 46055001 | Failed to send the message due to a business content error. |
| RCS | false | 46055002 | Failed to send the message due to an invalid attribute. |
| RCS | false | 46055101 | Failed to send the message due to an agency content error. |
| RCS | false | 46055102 | Failed to send the message due to an invalid agency ID. |
| RCS | false | 46055103 | Failed to send the message due to an agency ID permission error. |
| RCS | false | 46055104 | Failed to send the message due to a contract content error. |
| RCS | false | 46055201 | Failed to send the message due to a brand content error. |
| RCS | false | 46055202 | Failed to send the message due to a brand name error. |
| RCS | false | 46055203 | Failed to send the message due to a brand profile image error. |
| RCS | false | 46055204 | Failed to send the message due to a brand CS number error. |
| RCS | false | 46055205 | Failed to send the message due to a brand menu error. |
| RCS | false | 46055206 | Failed to send the message due to a brand category error. |
| RCS | false | 46055207 | Failed to send the message due to a brand homepage error. |
| RCS | false | 46055208 | Failed to send the message due to a brand email error. |
| RCS | false | 46055209 | Failed to send the message due to a brand address error. |
| RCS | false | 46055210 | Failed to send the message due to an invalid brand ID. |
| RCS | false | 46055301 | Failed to send the message due to a bot content error. |
| RCS | false | 46055302 | Failed to send the message due to an invalid bot ID. |
| RCS | false | 46055304 | Failed to send the message due to a bot ID permission error. |
| RCS | false | 46055501 | Failed to send the message due to a message base content error. |
| RCS | false | 46055502 | Failed to send the message due to an invalid message base ID. |
| RCS | false | 46055503 | Failed to send the message due to a message base ID permission error. |
| RCS | false | 46055504 | Failed to send the message due to an invalid format string. |
| RCS | false | 46055505 | Failed to send the message due to invalid message base policy information. |
| RCS | false | 46055506 | Failed to send the message due to an invalid message base parameter. |
| RCS | false | 46055507 | Failed to send the message due to an invalid message base attribute. |
| RCS | false | 46055508 | Failed to send the message due to an invalid message base type. |
| RCS | false | 46055509 | Failed to send the message due to a product type mismatch. |
| RCS | false | 46055601 | Failed to send the message due to a message base form content error. |
| RCS | false | 46055602 | Failed to send the message due to an invalid message base form ID. |
| RCS | false | 46055603 | Failed to send the message due to an invalid message base product code. |
| RCS | false | 46055604 | Failed to send the message because the message base has too many child layouts. |
| RCS | false | 46055621 | Failed to send the message due to an auto-reply message body JSON format error. |
| RCS | false | 46055622 | Failed to send the message due to an auto-reply message button JSON format error. |
| RCS | false | 46055701 | Failed to send the message due to prohibited text content. |
| RCS | false | 46055702 | Failed to send the message due to an action button permission error. |
| RCS | false | 46055703 | Failed to send the message due to a prohibited header value. |
| RCS | false | 46055704 | Failed to send the message due to a prohibited footer field. |
| RCS | false | 46055705 | Failed to send the message because the footer content is missing. |
| RCS | false | 46055706 | Failed to send the message due to a footer content syntax error. |
| RCS | false | 46055707 | Failed to send the message due to a content pattern error. |
| RCS | false | 46055708 | Failed to send the message because the title exceeds the maximum character limit. |
| RCS | false | 46055709 | Failed to send the message because the description exceeds the maximum character limit. |
| RCS | false | 46055710 | Failed to send the message because the number of buttons exceeds the maximum limit. |
| RCS | false | 46055711 | Failed to send the message due to a carousel card count mismatch. |
| RCS | false | 46055712 | Failed to send the message because the media size exceeds the maximum limit. |
| RCS | false | 46055801 | Failed to send the message due to a GW vendor content error. |
| RCS | false | 46055802 | Failed to send the message due to an invalid message. |
| RCS | false | 46055803 | Failed to send the message due to a message syntax error. |
| RCS | false | 46055804 | Failed to send the message due to missing message content. |
| RCS | false | 46055805 | Failed to send the message due to invalid message content. |
| RCS | false | 46055806 | Failed to send the message due to a duplicate MessageId. |
| RCS | false | 46055807 | Failed to send the message due to an invalid chatbot permission. |
| RCS | false | 46055808 | Failed to send the message due to an invalid chatbot status. |
| RCS | false | 46055809 | Failed to send the message due to an invalid agency permission. |
| RCS | false | 46055810 | Failed to send the message due to an invalid expiration field. |
| RCS | false | 46055811 | Failed to send the message because the parameter exceeds the maximum character limit. |
| RCS | false | 46055812 | Failed to send the message due to an invalid reseller ID. |
| RCS | false | 46055813 | Failed to send the message because the button text exceeds the maximum length. |
| RCS | false | 46055814 | Failed to send the message due to an invalid message base button. |
| RCS | false | 46055815 | Failed to send the message because the message body file could not be found. |
| RCS | false | 46055816 | Failed to send the message due to a suggestion count mismatch. |
| RCS | false | 46055817 | Failed to send the message due to an invalid destination phone number. |
| RCS | false | 46055818 | Failed to send the message due to an invalid message base ID. |
| RCS | false | 46055819 | Failed to send the message due to an invalid chatbot ID. |
| RCS | false | 46055820 | Failed to send the message because the message was canceled. |
| RCS | false | 46055821 | Failed to send the message due to a miscellaneous timeout. |
| RCS | false | 46055822 | Failed to send the message because the message was canceled. |
| RCS | false | 46055880 | Failed to send the message due to a suggestion count mismatch. |
| RCS | false | 46055881 | Failed to send the message due to an invalid response ID. |
| RCS | false | 46055882 | Failed to send the message because the response ID is missing. |
| RCS | false | 46055883 | Failed to send the message due to an invalid message base product code for the session message. |
| RCS | false | 46055884 | Failed to send the message due to an invalid user contact for the session message. |
| RCS | false | 46055885 | Failed to send the message due to an invalid chatbot ID for the session message. |
| RCS | false | 46055886 | Failed to send the message because chip lists are not allowed. |
| RCS | false | 46055887 | Failed to send the message due to a chatbot that is not allowed for the session message. |
| RCS | false | 46055900 | Failed to send the message due to a non-retryable error caused by an invalid message. |
| RCS | false | 46056002 | Failed to send the message due to a cancellation failure. |
| RCS | false | 46056007 | Failed to send the message because it expired before the session was established. |
| RCS | false | 46059001 | Failed to send the message due to a system IO error. |
| RCS | false | 46059002 | Failed to send the message due to an IO error. |
| RCS | false | 46059003 | Failed to send the message due to a backend timeout. |
| RCS | false | 46059202 | Failed to send the message due to a backend error. |
| RCS | false | 46059203 | Failed to send the message due to a backend timeout. |
| RCS | false | 46059901 | Failed to send the message because the service is unavailable. |
| RCS | false | 46059999 | Failed to send the message due to an unknown error. |
| RCS | false | 47041210 | Failed to send the message because the user does not support the TEXT feature. |
| RCS | false | 47041211 | Failed to send the message because the user does not support the FT feature. |
| RCS | false | 47041212 | Failed to send the message because the user does not support the rich card feature. |
| RCS | false | 47041220 | Failed to send the message because the user does not support XBOTMESSAGE 1.0. |
| RCS | false | 47041221 | Failed to send the message because the user does not support XBOTMESSAGE 1.1. |
| RCS | false | 47041222 | Failed to send the message because the user does not support XBOTMESSAGE 1.2. |
| RCS | false | 47041230 | Failed to send the message because the user does not support OPENRICHARD 1.0. |
| RCS | false | 47041231 | Failed to send the message because the user does not support OPENRICHARD 1.1. |
| RCS | false | 47041232 | Failed to send the message because the user does not support OPENRICHARD 1.2. |
| RCS | false | 47041240 | Failed to send the message because the user does not support GEOLOCATION PUSH requests. |
| RCS | false | 47054006 | Failed to send the message because the device is an RCS subscriber but does not support OPENRICHARD. |
| EMAIL | false | 51100005 | Failed to send the mail because the recipient refused to receive it. |
| EMAIL | false | 51100006 | Failed to send the mail because the scheduled send was canceled. |
| EMAIL | false | 51100007 | Failed to send the mail because the sending domain is not verified. |
| EMAIL | false | 51100008 | Failed to send the mail due to whitelist filtering. |
| EMAIL | false | 52000002 | Failed to send the message due to an error during flow sequential send processing. |
| EMAIL | false | 52000003 | Failed to send the message due to an error while preparing to send the message. |
| EMAIL | false | 52100003 | Failed to send the mail. |
| EMAIL | false | 56100002 | Failed to send the mail because it was bounced by the receiving SMTP server. |
| PUSH | false | 61100004 | Failed to send the push message due to a message format error. |
| PUSH | false | 61100005 | Failed to send the push message because authentication of the registered certificate/API key failed. |
| PUSH | false | 61100006 | Failed to send the push message because authentication of the registered certificate/API key failed. |
| PUSH | false | 61100014 | Failed to send the duplicate message due to the duplicate send prevention feature. |
| PUSH | false | 62000002 | Failed to send the message due to an error during flow sequential send processing. |
| PUSH | false | 62000003 | Failed to send the message due to an error while preparing to send the message. |
| PUSH | false | 62100007 | Failed to send the push message because the internal message TTL has expired. |
| PUSH | false | 62100009 | (This code is no longer in use.) |
| PUSH | false | 62100012 | Failed to send the push message due to an internal error. |
| PUSH | false | 62100014 | Push delivery failed due to an unsupported message type. |
| PUSH | false | 62109999 | Push delivery failed due to an internal error. |
| PUSH | false | 63100008 | Push delivery failed due to an APNS error response. |
| PUSH | false | 63100009 | Push delivery failed due to an FCM error response. |
| PUSH | false | 63100011 | Push delivery failed due to an ADM error response. |
| PUSH | false | 64100001 | Push delivery failed because the token is in an unsubscribed state. |
| PUSH | false | 67100002 | Push delivery failed because no registered contact was found. |
| PUSH | false | 67100003 | Push delivery failed because the token has expired. |
| PUSH | false | 67100013 | Push delivery failed because the token was deleted after the push token retention period (up to 2 years) expired. |