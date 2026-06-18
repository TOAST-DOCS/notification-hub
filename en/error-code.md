<!-- pre-align:aligned sig=6b437cd3fe5d -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Error Code</h1>

**Notifications > Notification Hub > Error Codes**

## List of Error Codes

| Category | Success (isSuccessful) | Result Code (resultCode) | Result Message (resultMessage) |
| --- | --- | --- | --- |
| Common | true | 0 | success |
| Common | false | 400000 | Partial failure |
| Common | false | 400002 | The FriendTalk coupon title is required, and the description must be 18 characters or fewer.<br>The linkMo field of the coupon is required, or the schemeAndroid/schemeIos format is invalid.<br>The FriendTalk template type you entered cannot have a carousel.<br>A carousel cannot be used for general message purposes.<br>The carousel list is required and must contain between 2 and 10 items.<br>The FriendTalk carousel header must be 25 characters or fewer.<br>The FriendTalk carousel message must be 100 characters or fewer.<br>A FriendTalk carousel image is required.<br>Items or headers cannot be used with this template type.<br>Items and headers are required fields.<br>The header must be 25 characters or fewer.<br>The item list size must be between 3 and 4.<br>The item title is a required field and must be 30 characters or fewer.<br>The item linkMo is a required field.<br>Buttons cannot be used with this template type.<br>The number of buttons exceeded the maximum number (up to 5 for regular messages, up to 4 for coupons, up to 2 for wide item list/wide image)<br>The button type is a required field.<br>The button name is a required field.<br>The button name can be up to 14 characters. For the wide item list type, up to 9 characters; for the carousel type, up to 8 characters.<br>The button link must be 2,000 characters or fewer.<br>The button linkPc must include the http or https protocol.<br>The button linkMo must include the http or https protocol.<br>The WL button type must include the linkMo field.<br>At least 2 of the following fields must be included: linkMo, schemeAndroid, schemeIos<br>The BF button type must include the bizFormKey field.<br>The BF button type must be placed at the top.<br>The BF button type must have a button name of one of the following: Book in Talk, Survey in Talk, Enter in Talk.<br>The linkMo, linkPc, schemeIos, and schemeAndroid fields cannot be used with the MD or BK button type.<br>Images cannot be used with this template type.<br>An image is a required field.<br>templateContent cannot be used with this template type.<br>The templateContent length is a required field and must be 1,000 characters or fewer.<br>The templateContent length for the image type must be 400 characters or fewer.<br>The templateContent length for the wide image type must be 76 characters or fewer.<br>Cannot add more tokens to the recipient.<br>The maximum number of tokens per recipient has been exceeded.<br>The recipient cannot be registered to the group.<br>Invalid email address. {0}<br>Invalid recipient number.<br>The RCS recipient number is empty.<br>The body must include the "(광고)" and opt-out phrases.<br>The template parameter is empty.<br>Template parameter {0} is missing.<br>Invalid template.<br>The sender number registration review request (mobile phone verification) failed. Please check the verification code.<br>Failed to delete the sender number.<br>The sender number registration review request failed. Please check the phone number or the uploaded documents.<br>The attachment size can be up to {0} MB.<br>The scheduled time cannot be in the past.<br>The scheduled time must be set within 60 days.<br>No recipients.<br>The maximum number of recipients has been exceeded.<br>An authentication email cannot be sent with attachments.<br>The subject of an advertising email must start with "(광고)", "(AD)", or "(広告)".<br>This is a restricted sending type.<br>The subject length has been exceeded.<br>The body length has been exceeded.<br>The body must include the authentication phrase.<br>The body must include the required advertising phrase.<br>Individual members cannot use this service. |
| Common | false | 400100 | The 'Domain Protection' feature is enabled for this domain. |
| Common | false | 400101 | The template ID is already registered. |
| Common | false | 400102 | Authentication emails do not support sending templates that include attachments. |
| Common | false | 400103 | The template is inactive. |
| Common | false | 400104 | The email address is already registered in the opt-out list. |
| Common | false | 400105 | The email address is already registered in the opt-out list. |
| Common | false | 400106 | Failed to delete from the opt-out list. |
| Common | false | 400107 | Domain verification failed. |
| Common | false | 400108 | The domain is already registered. |
| Common | false | 400109 | The domain is not verified. |
| Common | false | 400110 | The domain is not a root domain. |
| Common | false | 400111 | The domain is already verified. |
| Common | false | 400112 | A subdomain must not be a root domain. |
| Common | false | 400113 | The subdomain is not registered. |
| Common | false | 400114 | The domain is not registered. |
| Common | false | 400115 | DKIM verification failed. |
| Common | false | 400116 | Failed to share the domain. |
| Common | false | 400117 | Failed to disable DKIM. |
| Common | false | 400118 | Failed to enable DKIM. |
| Common | false | 400119 | The root domain is not verified. |
| Common | false | 400120 | The domain is already shared. |
| Common | false | 400121 | The domain is not shared with users of other organizations. |
| Common | false | 400122 | The DMARC record does not exist. |
| Common | false | 400123 | The SPF record is duplicated. |
| Common | false | 400124 | The SPF record cannot be found because the maximum number of DNS lookups for the SPF record has been exceeded. |
| Common | false | 400125 | The 'all' in the SPF record is invalid. |
| Common | false | 400126 | The domain is not the root domain of the subdomain. |
| Common | false | 400127 | The domain and subdomain are identical. |
| Common | false | 400128 | DNS lookup failed. |
| Common | false | 400129 | Failed to delete DKIM. |
| Common | false | 400130 | The domain format is invalid. |
| Common | false | 400131 | The subdomain format is invalid. |
| Common | false | 400200 | Attachment file upload error. |
| Common | false | 400201 | Failed to create the Excel file. |
| Common | false | 400202 | The attachment ID is already in use. |
| Common | false | 400203 | International sending has been blocked by the service. |
| Common | false | 400204 | The country has been blocked by the service. |
| Common | false | 400205 | Blocked by overall metrics. |
| Common | false | 400206 | The recipient number is not in the whitelist. |
| Common | false | 400207 | The conversion rate is below the threshold. |
| Common | false | 400208 | The template ID is already in use. |
| Common | false | 400209 | The maximum number of registered templates has been reached. |
| Common | false | 400210 | The template has been deleted. |
| Common | false | 400211 | Invalid category. |
| Common | false | 400212 | The top-level category cannot be deleted. |
| Common | false | 400213 | The sender number is already registered. |
| Common | false | 400214 | Already reviewed. |
| Common | false | 400215 | The review has ended. |
| Common | false | 400216 | This user is already under verification. |
| Common | false | 400217 | The sender number is not registered. |
| Common | false | 400218 | This sender number is blocked. |
| Common | false | 400219 | This sender number is invalid. |
| Common | false | 400220 | This sender number is already in use. |
| Common | false | 400300 | Invalid app key. |
| Common | false | 400301 | Invalid secret key. |
| Common | false | 400302 | Invalid SMS app key. |
| Common | false | 400303 | Invalid SMS sender number. |
| Common | false | 400304 | The sender profile is already registered. |
| Common | false | 400305 | The same 'X-NC-API-IDEMPOTENCY-KEY' was used within the last 10 minutes. |
| Common | false | 400306 | The sender profile does not have a sender key. |
| Common | false | 400307 | The sender profile group already exists. |
| Common | false | 400308 | The sender profile status is not active. |
| Common | false | 400309 | The maximum number of daily message transmissions has been exceeded. |
| Common | false | 400310 | The sender profile group has already been added. |
| Common | false | 400311 | Invalid SMS opt-out number. |
| Common | false | 400312 | Invalid UUID. |
| Common | false | 400313 | The sender profile has not been added to this group. |
| Common | false | 400314 | The maximum group size is 10. |
| Common | false | 400315 | The sender group cannot send messages. |
| Common | false | 400316 | The sender group cannot be deleted. |
| Common | false | 400317 | The maximum number of group members is 5,000. |
| Common | false | 400318 | The sender is blocked. |
| Common | false | 400319 | The blacklist in the template value cannot exceed 14 characters. |
| Common | false | 400320 | A blacklisted user cannot join the group. |
| Common | false | 400321 | Identity verification is required to use this service. |
| Common | false | 400322 | The length of '{}' must be {} or fewer. |
| Common | false | 400323 | '{}' cannot be empty. |
| Common | false | 400324 | '{}' cannot be null. |
| Common | false | 400325 | '{}' must be {} or more. |
| Common | false | 400326 | The button parameter is invalid. |
| Common | false | 400327 | The content replaced with template parameters cannot exceed 1,000 characters. |
| Common | false | 400328 | 'content' is too long. |
| Common | false | 400329 | 'content' is too long. |
| Common | false | 400330 | Cannot send a message with a past date. |
| Common | false | 400331 | Cannot send a message more than 90 days in the future. |
| Common | false | 400332 | The format of 'requestDate' is invalid. |
| Common | false | 400333 | The requestId is invalid. |
| Common | false | 400334 | 'content' is too long. |
| Common | false | 400335 | Too many buttons when wide-image is requested. |
| Common | false | 400336 | The template subject replaced with template parameters cannot exceed 50 characters. |
| Common | false | 400337 | The template item parameter is invalid. |
| Common | false | 400338 | The template item highlight parameter is invalid. |
| Common | false | 400339 | The template header replaced with template parameters cannot exceed 16 characters. |
| Common | false | 400340 | The template representative link parameter is invalid. |
| Common | false | 400341 | When a template item is requested, the content cannot exceed 700 characters. |
| Common | false | 400342 | The message sending failed because the deadline has expired. |
| Common | false | 400343 | Please configure the sender profile retransmission settings. |
| Common | false | 400344 | The quick reply parameter is invalid. |
| Common | false | 400345 | Too many buttons when quick reply is requested. |
| Common | false | 400346 | If the template has a web link, linkMo must be entered. |
| Common | false | 400347 | The template code or template name already exists. |
| Common | false | 400348 | Invalid field. |
| Common | false | 400349 | Please check the template parameters. |
| Common | false | 400350 | Please check the template status. |
| Common | false | 400351 | linkMo or linkPc must include http:// or https://. |
| Common | false | 400352 | If the template has an AL (appLink), at least two of the following must be entered: schemeAndroid, schemeIos, and LinkMo. |
| Common | false | 400353 | Replacement parameters cannot be included in the button name. |
| Common | false | 400354 | The content does not match the template. |
| Common | false | 400355 | The button or quick reply does not match the template. |
| Common | false | 400356 | Only templates in TSC03 (APPROVE) or TSC04 (REJECT) status can be modified. |
| Common | false | 400357 | A template is already being modified. |
| Common | false | 400358 | The button type is invalid. |
| Common | false | 400359 | The sender profile cannot use the CBT feature. |
| Common | false | 400360 | Templates with the 'TEXT' highlight type must have templateTitle and templateSubtitle. |
| Common | false | 400361 | Replacement parameters cannot be included in the template subtitle. |
| Common | false | 400362 | Templates with the 'EX' message type must have templateExtra. |
| Common | false | 400363 | Templates with the 'MI' message type must have templateExtra. |
| Common | false | 400364 | Replacement parameters cannot be included in the template additional content. |
| Common | false | 400365 | AC type buttons can only be used with templateMessageType (AD/MI). |
| Common | false | 400366 | An AC type button must be placed alone or at the top. |
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
| Common | false | 400378 | The item highlight title with a thumbnail cannot exceed 21 characters, and the description cannot exceed 13 characters. |
| Common | false | 400379 | imageUrl must include http:// or https://. |
| Common | false | 400380 | The template header does not match the template. |
| Common | false | 400381 | The template item or template item highlight does not match the template. |
| Common | false | 400382 | The BF type button must be placed at the top. |
| Common | false | 400383 | The button link type 'BF' must follow this constraint. |
| Common | false | 400384 | The template representative link does not match the template. |
| Common | false | 400385 | The template title and template item highlight title cannot end with a space. |
| Common | false | 400386 | The template parameter length cannot exceed 1,000 characters. |
| Common | false | 400387 | The template parameter does not match the template. |
| Common | false | 400388 | Comments cannot be added to a template in registered or completed status. |
| Common | false | 400389 | Replacement parameters cannot be included in the quick reply name. |
| Common | false | 400390 | The format of the button or quick reply is invalid. |
| Common | false | 400391 | A FriendTalk wide item must have a title. |
| Common | false | 400392 | A FriendTalk wide item must have an image. |
| Common | false | 400393 | A FriendTalk wide item must have a linkMo. |
| Common | false | 400394 | FriendTalk wide items must have between 3 and 4 items and a header. |
| Common | false | 400395 | A FriendTalk carousel must have a header. |
| Common | false | 400396 | A FriendTalk carousel must have a message. |
| Common | false | 400397 | A FriendTalk carousel must have an attachment. |
| Common | false | 400398 | A FriendTalk carousel must have an image. |
| Common | false | 400399 | A FriendTalk carousel must have between 2 and 10 items. |
| Common | false | 400400 | The FriendTalk carousel tail must have a linkMo. |
| Common | false | 400401 | A FriendTalk coupon must have a title and description. |
| Common | false | 400402 | For FriendTalk text/image type messages, the FriendTalk coupon description cannot exceed 12 characters. |
| Common | false | 400403 | The FriendTalk coupon title is invalid. |
| Common | false | 400404 | FriendTalk must have a mobile link or a channel link in iOS/Android format. |
| Common | false | 400405 | FriendTalk wide items/carousels can only be sent as the AD type. |
| Common | false | 400406 | The subject length of the first wide item in a FriendTalk cannot exceed 25 characters, and the subject length of the second through fourth wide items cannot exceed 30 characters. |
| Common | false | 400407 | The FriendTalk button size is invalid. |
| Common | false | 400408 | The FriendTalk video URL is invalid. |
| Common | false | 400409 | 'content' is too long. |
| Common | false | 400410 | 'header' is too long. |
| Common | false | 400411 | The FriendTalk carousel feed type cannot have a 'head' field. |
| Common | false | 400412 | The FriendTalk carousel feed type cannot have an 'additionalContent' field. |
| Common | false | 400413 | The FriendTalk carousel feed type cannot have a 'commerce' field. |
| Common | false | 400414 | The FriendTalk carousel commerce type cannot have 'header' or 'message' fields. |
| Common | false | 400415 | The FriendTalk carousel button size is invalid. |
| Common | false | 400416 | If the commerce has a 'discounted price' field, it must also have a 'discount rate' or 'fixed discount amount' field. |
| Common | false | 400417 | Invalid parameter. |
| Common | false | 400418 | The app key is already activated. |
| Common | false | 400419 | The app key is not activated. |
| Common | false | 400420 | Searches are only available within 31 days. |
| Common | false | 400421 | The app key status is inactive. |
| Common | false | 400422 | The app key does not have a sender key. |
| Common | false | 400423 | The file size is less than {}. |
| Common | false | 400424 | The file size is less than 20 MB. |
| Common | false | 400425 | Please check the file extension. |
| Common | false | 400426 | The maximum recipient list has been exceeded. |
| Common | false | 400427 | Only jpg/jpeg extensions can be uploaded. |
| Common | false | 400428 | The file does not have a recipient number header. |
| Common | false | 400429 | The requestId is invalid. |
| Common | false | 400430 | Messages older than 90 days cannot be searched. |
| Common | false | 400431 | A file upload error occurred. |
| Common | false | 400432 | The recipient number is invalid. |
| Common | false | 400433 | Failed to read the file. |
| Common | false | 400434 | The file size is less than 10 MB. |
| Common | false | 400435 | Data export failed. |
| Common | false | 400436 | All senders must be deleted before deactivating the product. |
| Common | false | 400437 | Failed to deactivate the dormant template. |
| Common | false | 400438 | A maximum of 20 templates can be uploaded at a time. |
| Common | false | 400439 | The header of the uploaded template is invalid. |
| Common | false | 400440 | Failed to convert to AD/MI type. |
| Common | false | 400441 | Failed to convert to AD/MI type. |
| Common | false | 400442 | The search parameter is invalid. |
| Common | false | 400443 | The RequestId or start/end request date is invalid. |
| Common | false | 400444 | The RequestId is empty. |
| Common | false | 400445 | The retransmission message is invalid. |
| Common | false | 400446 | The recipient number is invalid. |
| Common | false | 400447 | The vendor API request failed. |
| Common | false | 400448 | 'imageSeq' is empty. |
| Common | false | 400449 | The uploaded image is invalid. |
| Common | false | 400450 | Failed to delete the image. |
| Common | false | 400451 | 'createUser' is too long. |
| Common | false | 400452 | Authentication-related content must be included. |
| Common | false | 400453 | The storage configuration cannot be empty. |
| Common | false | 400454 | The content contains prohibited words. |
| Common | false | 400455 | This project is already shared. |
| Common | false | 400456 | Failed to upload the image file due to an encoding error. |
| Common | false | 400457 | A required request part is missing. |
| Common | false | 400458 | The type of the method argument does not match what was expected. |
| Common | false | 400459 | This version is deprecated. |
| Common | false | 400460 | Only the application/json content type is supported. |
| Common | false | 400461 | Client error. |
| Common | false | 400462 | templateMessageType (AD/MI) must include an AC type button.<br>System error. |
| Common | false | 400500 | The parameter is invalid. |
| Common | false | 400501 | The parameter format is invalid. |
| Common | false | 400502 | The parameter is empty or null. |
| Common | false | 400503 | Invalid certificate. |
| Common | false | 400504 | Duplicate certificate. |
| Common | false | 400505 | The certificate has expired. |
| Common | false | 400506 | The certificate is already registered. |
| Common | false | 400507 | The maximum limit has been exceeded. |
| Common | false | 400508 | The certificate has already been completed. |
| Common | false | 400509 | Too many. |
| Common | false | 400510 | The API version is not supported. |
| Common | false | 400511 | The deletion guide is empty. |
| Common | false | 400512 | The contact is empty. |
| Common | false | 400513 | The contact format is invalid ([0-9-]+). |
| Common | false | 400514 | The APNS certificate does not support VoIP. |
| Common | false | 400515 | The HTTP method is not supported. |
| Common | false | 400516 | There is no channel to receive messages. |
| Common | false | 400517 | 'target |
| Common | false | 400518 | Invalid push type. |
| Common | false | 400519 | The channel is an empty string. |
| Common | false | 400520 | Access is not permitted. |
| Common | false | 400521 | The key is unavailable. |
| Common | false | 400600 | The SMS project is inactive. |
| Common | false | 400601 | The SMS project cannot be used. |
| Common | false | 400602 | The button parameter is invalid. |
| Common | false | 400603 | An opt-out number is required when sending advertising messages. |
| Common | false | 400604 | Only one card can be registered for horizontal and vertical types. |
| Common | false | 400605 | Invalid brand status. |
| Common | false | 400606 | Invalid chatbot status. |
| Common | false | 400607 | Invalid template status. |
| Common | false | 400608 | The template is not supported. |
| Common | false | 400609 | The advertising template cannot be used. |
| Common | false | 400610 | The media has expired. |
| Common | false | 400611 | Invalid media type. |
| Common | false | 400612 | The maximum file size has been exceeded. |
| Common | false | 400613 | Invalid media format. |
| Common | false | 400614 | An empty media file was uploaded. |
| Common | false | 400615 | The blocking service status is invalid. |
| Common | false | 400616 | The recipient number is blocked. |
| Common | false | 400617 | The sender number does not exist. |
| Common | false | 400618 | The type is not supported. |
| Common | false | 400619 | Failed to call the opt-out list lookup API. |
| Common | false | 400620 | Failed to call the opt-out list lookup API. |
| Common | false | 400621 | Failed to call the sender number lookup API. |
| Common | false | 400622 | Failed to call the project lookup API. |
| Common | false | 400623 | Failed to call the SMS project activation API. |
| Common | false | 400624 | Failed to call the SMS sending API. |
| Common | false | 400700 | No identity verification history found. |
| Common | false | 404000 | {0} not found.<br>The contact was not found.<br>The recipient was not found.<br>Self-verification was not found.<br>The identity verification record was not found.<br>The content was not found.<br>The attachment was not found.<br>The category was not found.<br>The project was not found.<br>The recipient set was not found.<br>The recipient sending result (messageId: {0}, recipientIndex: {1}) does not exist.<br>The contact sending result (messageId: {0}, recipientIndex: {1}, contactIndex: {2}) does not exist. |
| Common | false | 404100 | Failed to retrieve the template. |
| Common | false | 404101 | The opt-out information was not found. |
| Common | false | 404102 | The category information was not found. |
| Common | false | 404103 | The Excel file was not found. |
| Common | false | 404104 | The app key does not exist. |
| Common | false | 404201 | The service does not exist. |
| Common | false | 404202 | The file has expired or does not exist. |
| Common | false | 404203 | The data does not exist. |
| Common | false | 404204 | The download reservation does not exist. |
| Common | false | 404205 | The template does not exist. |
| Common | false | 404206 | The category does not exist. |
| Common | false | 404207 | The registered sender number request information does not exist. |
| Common | false | 404208 | The data does not exist. |
| Common | false | 404209 | The registered request sender number does not exist. |
| Common | false | 404210 | This common code does not exist. |
| Common | false | 404211 | The AuthCode does not exist. |
| Common | false | 404212 | This URI does not exist. |
| Common | false | 404213 | This IP does not exist. |
| Common | false | 404214 | Invalid search period. |
| Common | false | 404215 | The authentication information does not exist. |
| Common | false | 404216 | The Excel file was not found. |
| Common | false | 404217 | The configCode does not exist. |
| Common | false | 404218 | The CSV file was not found. |
| Common | false | 404219 | This is not a registered opt-out number. |
| Common | false | 404220 | The number is not registered. |
| Common | false | 404221 | The number is already registered. |
| Common | false | 404222 | The opt-out number is not registered. |
| Common | false | 404300 | The sender profile group does not exist. |
| Common | false | 404301 | No message found for the requested requestId or recipientSeq. |
| Common | false | 404302 | The sender profile does not exist. |
| Common | false | 404303 | The message to cancel was not found or does not meet the cancellation conditions. |
| Common | false | 404304 | The bulk message request was not found. |
| Common | false | 404305 | The template does not exist. |
| Common | false | 404306 | The button name does not exist. |
| Common | false | 404307 | No button or quick reply exists in the template. |
| Common | false | 404308 | The quick reply name does not exist. |
| Common | false | 404309 | The app key does not exist. |
| Common | false | 404310 | The file was not found. |
| Common | false | 404311 | The recipient list was not found. |
| Common | false | 404312 | The data does not exist. |
| Common | false | 404313 | The image was not found. |
| Common | false | 404314 | There is no sender profile registered in your project. |
| Common | false | 404315 | The API does not exist. |
| Common | false | 404600 | The brand is not linked. |
| Common | false | 404601 | The brand does not exist. |
| Common | false | 404602 | The chatbot does not exist. |
| Common | false | 404603 | The template does not exist. |
| Common | false | 404604 | The media does not exist. |
| Common | false | 404605 | The opt-out list does not exist. |
| Common | false | 404606 | The message ID does not exist. |
| Common | false | 409000 | The group recipient (groupId: {0}, recipientId: {1}) already exists.<br>The recipient alias is already registered.<br>The message recipient ({0}, messageRecipientSetId: {1}, index: {2}) already exists.<br>{0} already exists. |
| Common | false | 500001 | An internal server error occurred. |
| Common | false | 500002 | Invalid status server error |
| Message Sending | false | 400001 | The number of contacts has been exceeded.<br>The flow sending sequence is empty.<br>The initial flow sending channel is empty.<br>The flow sending sequence is invalid.<br>Duplicate message channel.<br>Cannot add message recipients.<br>Invalid phone number pattern.<br>Invalid email address pattern.<br>Invalid token pattern.<br>{0} is an invalid Alim Talk template status.<br>The email local part length has been exceeded.<br>The email address length has been exceeded.<br>The email domain length has been exceeded.<br>The phone number is empty.<br>The phone number {0} contains non-numeric characters.<br>Invalid phone number. {0}<br>Invalid date format. {0}<br>{0} is an invalid file type.<br>{0} is not supported.<br>Contact sending result lookup fields (messageId

<a id="delivery-result-code"></a>

## Result code of receiving

| 값 | 설명 |
| --- | --- |
| MTR1 | 수신 성공 |
| MTR2 | 수신 실패 |
| MTR3 | 수신 중 |

## 수신 결과 상세 코드

| 값 | 설명 |
| --- | --- |
| MTR1 | 수신 성공 |
| MTR2_1 | 가입자 없음 |
| MTR2_2 | 단말기 전원 꺼짐 |
| MTR2_3 | 정보 없음 |
| MTR2_4 | 통화중/서비스 거절 |
| MTR2_5 | 기타 |

| Category | Is Successful (isSuccessful) | Result Code (resultCode) | Result Message (resultMessage) |
| --- | --- | --- | --- |
| Common | true | 00000000 | Success |
| Common | false | 00999999 | Other error |
| Common | false | 09000000 | Cancel delivery |
| SMS | false | 11100001 | Failed to send the message due to advertising send time restrictions. |
| SMS | false | 11100002 | Failed to send the message due to duplicate send restrictions. |
| SMS | false | 11902023 | Failed to send the message because the subject or body contains an unsupported character set. |
| SMS | false | 11902044 | Failed to send the message because international sending is not permitted in the destination country. |
| SMS | false | 11902045 | Failed to send the message because international sending is disabled. |
| SMS | false | 11902047 | Failed to send the message because the monthly international send limit has been exceeded. |
| SMS | false | 11902049 | Failed to send the message due to whitelist settings. |
| SMS | false | 11902051 | Failed to send the message due to a conversion rate issue. |
| SMS | false | 11902052 | Failed to send the message due to the per-organization send volume limit. |
| SMS | false | 11906001 | Failed to send the message because the recipient has opted out. |
| SMS | false | 12000002 | Failed to send the message due to an error during flow sequential send processing. |
| SMS | false | 12000003 | Failed to send the message due to an error during message send preparation. |
| SMS | false | 12100911 | Failed to send the message because the attached file has no extension. |
| SMS | false | 12100913 | Failed to send the message because the attached file size is 0. |
| SMS | false | 12909999 | Failed to send the message due to a system error. |
| SMS | false | 13004001 | Failed to send the message due to a signature format error. |
| SMS | false | 13004002 | Failed to send the message due to a sender number error. |
| SMS | false | 13004003 | Failed to send the message due to a recipient number error. |
| SMS | false | 13100900 | Failed to send the message due to another error. |
| SMS | false | 16001001 | Failed to send the message because the server is congested. |
| SMS | false | 16001002 | Failed to send the message because the recipient number format is invalid. |
| SMS | false | 16001003 | Failed to send the message because the sender number format is invalid. |
| SMS | false | 16001004 | Failed to send the message because the message was deleted due to a carrier error. |
| SMS | false | 16001019 | Failed to send the message due to TTL expiration. |
| SMS | false | 16002000 | Failed to send the message because the send time has expired. |
| SMS | false | 16002001 | Failed to send the message due to a wireless network issue. |
| SMS | false | 16002002 | Failed to send the message because the message was not delivered from the wireless network to the device. |
| SMS | false | 16002004 | Failed to send the message because the message buffer between the carrier and the device is full. |
| SMS | false | 16002006 | Failed to send the message because the message was deleted. |
| SMS | false | 16003000 | Failed to send the message because the message could not be sent. |
| SMS | false | 16003009 | Failed to send the message due to a message format error. |
| SMS | false | 16003011 | Failed to send the message due to a server error. |
| SMS | false | 16003012 | Failed to send the message because it was classified as spam. |
| SMS | false | 16003013 | Message sending was rejected by the service. |
| SMS | false | 16003014 | Failed to send the message due to another reason. |
| SMS | false | 16003016 | Failed to send the message because the attachment size limit was exceeded. |
| SMS | false | 16004004 | Failed to send the message due to a temporary device issue. |
| SMS | false | 16004005 | Failed to send the message because the subscriber does not exist. |
| SMS | false | 16004006 | Failed to send the message due to a recipient error. |
| SMS | false | 16004007 | Failed to send the message due to a carrier error or block. |
| SMS | false | 16004008 | Failed to send the message because it was classified as spam. |
| SMS | false | 16004009 | Failed to send the message due to a temporary network error. |
| SMS | false | 16004010 | Failed to send the message due to an abnormal send pattern. |
| SMS | false | 16100915 | Failed to send the message because it is a duplicate message. |
| SMS | false | 16100919 | Failed to send the message because it is outside the permitted send time or message resending is prohibited. |
| SMS | false | 16100999 | Failed to send the message due to another error. |
| SMS | false | 17002003 | Failed to send the message because the device is powered off. |
| SMS | false | 17002005 | Failed to send the message due to a dead zone. |
| SMS | false | 17002007 | Failed to send the message due to a temporary device issue. |
| SMS | false | 17003001 | Failed to send the message because the subscriber does not exist. |
| SMS | false | 17003003 | Failed to send the message due to an invalid recipient number format or non-existent number. |
| SMS | false | 17003004 | Failed to send the message because the device service is temporarily suspended. |
| SMS | false | 17003005 | Failed to send the message because the message was not delivered while the device was processing a call. |
| SMS | false | 17003006 | Failed to send the message because the incoming call was rejected. |
| SMS | false | 17003008 | Failed to send the message due to another device issue. |
| SMS | false | 17003010 | Failed to send the message because the recipient device does not support MMS. |
| SMS | false | 17003017 | Failed to send the message because the sender number format is invalid due to the caller ID spoofing prevention service. |
| SMS | false | 17003018 | Failed to send the message because the sender number is a personal mobile number subscribed to the caller ID spoofing prevention service. |
| SMS | false | 17003019 | Failed to send the message because the sender number is blocked by KISA or the Ministry of Science and ICT. |
| ALIMTALK | false | 21901000 | Failed to send the message due to an invalid appKey. |
| ALIMTALK | false | 21901001 | Failed to send the message due to an invalid secretKey. |
| ALIMTALK | false | 21901002 | Failed to send the message due to an invalid SMS appkey. |
| ALIMTALK | false | 21901003 | Failed to send the message due to an invalid SMS Sendno. |
| ALIMTALK | false | 21901004 | Failed to send the message because the Plus Friend is already registered. |
| ALIMTALK | false | 21901005 | Failed to send the message because the same 'X-NC-API-IDEMPOTENCY-KEY' was used within the last 10 minutes. |
| ALIMTALK | false | 21901006 | Failed to send the message because the senderKey does not exist for the Plus Friend. |
| ALIMTALK | false | 21901010 | Failed to send the message because the Plus Friend group does not exist. |
| ALIMTALK | false | 21901013 | Failed to send the message because the Plus Friend group already exists. |
| ALIMTALK | false | 21901014 | Failed to send the message because the Plus Friend is not in an active state. |
| ALIMTALK | false | 21901016 | Failed to send the message because no message was found for the specified requestId or recipientSeq. |
| ALIMTALK | false | 21901017 | Failed to send the message because the daily maximum message count has been exceeded. |
| ALIMTALK | false | 21901018 | Failed to send the message because the Plus Friend has already been added. |
| ALIMTALK | false | 21901019 | Failed to send the message due to an invalid SMS UnSubscribeno. |
| ALIMTALK | false | 21901020 | Failed to send the message due to an invalid uuid. |
| ALIMTALK | false | 21901022 | Failed to send the message because the Plus Friend has not been added to the group. |
| ALIMTALK | false | 21901023 | Failed to send the message because the maximum Plus Friend group size of 10 has been exceeded. |
| ALIMTALK | false | 21901024 | Failed to send the message because a sender group cannot send messages. |
| ALIMTALK | false | 21901025 | Failed to send the message because a sender group cannot be deleted. |
| ALIMTALK | false | 21901026 | Failed to send the message because the maximum group member count of 5,000 has been exceeded. |
| ALIMTALK | false | 21901027 | Failed to send the message because the sender is blocked. |
| ALIMTALK | false | 21901028 | Failed to send the message because the template value exceeds 14 characters. |
| ALIMTALK | false | 21901029 | Failed to send the message because a blacklisted sender cannot join a group. |
| ALIMTALK | false | 21901030 | Failed to send the message because identity verification is required. |
| ALIMTALK | false | 21902000 | Failed to send the message because '{}' must be {} or less. |
| ALIMTALK | false | 21902001 | Failed to send the message because '{}' cannot be blank. |
| ALIMTALK | false | 21902002 | Failed to send the message because '{}' cannot be null. |
| ALIMTALK | false | 21902003 | Failed to send the message because '{}' must be {} or greater. |
| ALIMTALK | false | 21902004 | Failed to send the message because '{}' must be between {} and {}. |
| ALIMTALK | false | 21902005 | Failed to send the message because '{}' must be {} or less. |
| ALIMTALK | false | 21902017 | Failed to send the message because the Plus Friend does not exist. |
| ALIMTALK | false | 21902018 | Failed to send the message because the button parameter is invalid. |
| ALIMTALK | false | 21902019 | Failed to send the message because the template parameter replacement content exceeds 1,000 characters. |
| ALIMTALK | false | 21902023 | Failed to send the message because 'content' is too long (maximum 400 characters when using an image). |
| ALIMTALK | false | 21902024 | Failed to send the message because 'content' is too long (maximum 1,000 characters when not using an image). |
| ALIMTALK | false | 21902025 | Failed to send the message because messages cannot be sent to a past date. Check `requestDate`. |
| ALIMTALK | false | 21902026 | Failed to send the message because messages cannot be sent to a date more than 90 days in the future. Check `requestDate`. |
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
| ALIMTALK | false | 21902500 | Failed to send the message because the bulk message request was not found. |
| ALIMTALK | false | 21902501 | Failed to send the message because the send request deadline has expired. |
| ALIMTALK | false | 21902502 | Failed to send the message because the Plus Friend resend settings are required. |
| ALIMTALK | false | 21902504 | Failed to send the message because the quickReplies parameter is invalid. |
| ALIMTALK | false | 21902505 | Failed to send the message because there are too many 'buttons' (maximum 2 when using quickReplies). |
| ALIMTALK | false | 21903000 | Failed to send the message because linkMo was not entered even though the template has a WL (webLink). |
| ALIMTALK | false | 21903001 | Failed to send the message because the templateCode or templateName already exists. |
| ALIMTALK | false | 21903002 | Failed to send the message because a field is invalid. |
| ALIMTALK | false | 21903003 | Failed to send the message because the template does not exist. |
| ALIMTALK | false | 21903004 | Failed to send the message because the template parameter is invalid. |
| ALIMTALK | false | 21903005 | Failed to send the message because the template status is invalid. (Check the approval/rejection status.) |
| ALIMTALK | false | 21903006 | Failed to send the message because linkMo/linkPc does not include http:// or https://. |
| ALIMTALK | false | 21903007 | Failed to send the message because the template has an AL (appLink) but two or more of schemeAndroid, schemeIos, and linkMo are missing. |
| ALIMTALK | false | 21903008 | Failed to send the message because the button name contains a replacement parameter. |
| ALIMTALK | false | 21903009 | Failed to send the message due to a non-existent button name. |
| ALIMTALK | false | 21903010 | Failed to send the message because the content does not match the template. (SMS substitution is available when resend settings are configured.) |
| ALIMTALK | false | 21903011 | Failed to send the message because buttons/quickReplies do not match the template. (SMS substitution is available when resend settings are configured.) |
| ALIMTALK | false | 21903012 | Failed to send the message because the template must be in TSC03/APPROVE or TSC04/REJECT status to be modified. |
| ALIMTALK | false | 21903013 | Failed to send the message because a template that is already being modified exists. |
| ALIMTALK | false | 21903014 | Failed to send the message because the button type is invalid. |
| ALIMTALK | false | 21903015 | Failed to send the message because the CBT feature is not permitted for the Plus Friend. |
| ALIMTALK | false | 21903016 | Failed to send the message because the template with emphasizeType set to 'TEXT' is missing templateTitle and templateSubtitle. |
| ALIMTALK | false | 21903017 | Failed to send the message because templateSubtitle contains a replacement parameter. |
| ALIMTALK | false | 21903018 | Failed to send the message because the template with messageType set to 'EX' is missing templateExtra. |
| ALIMTALK | false | 21903020 | Failed to send the message because the template with messageType set to 'MI' is missing templateExtra. |
| ALIMTALK | false | 21903021 | Failed to send the message because templateExtra contains a replacement parameter. |
| ALIMTALK | false | 21903024 | Failed to send the message because the AC type button can only be used with templateMessageType (AD/MI), but this condition was violated. |
| ALIMTALK | false | 21903025 | Failed to send the message because the AC type button must be placed alone or at the top, but this condition was violated. |
| ALIMTALK | false | 21903026 | Failed to send the message because the AC type button name does not include 'Add Channel'. |
| ALIMTALK | false | 21903027 | Failed to send the message because the template with emphasizeType set to 'NONE' contains templateTitle or templateSubtitle. |
| ALIMTALK | false | 21903028 | Failed to send the message because the template with messageType set to 'BA' contains templateExtra. |
| ALIMTALK | false | 21903030 | Failed to send the message because the template with messageType set to 'AD' contains templateExtra. |
| ALIMTALK | false | 21903032 | Failed to send the message because the template with emphasizeType set to 'IMAGE' is missing templateImageName and templateImageUrl. |
| ALIMTALK | false | 21903033 | Failed to send the message because the specified button/quickReply does not exist in the template. |
| ALIMTALK | false | 21903034 | Failed to send the message because the template cannot be deleted due to a recently sent message. (requestId: {}) |
| ALIMTALK | false | 21903035 | Failed to send the message because the template with emphasizeType set to 'ITEM_LIST' is missing required items (templateImageInfo, templateHeader, templateItem, etc.). |
| ALIMTALK | false | 21903036 | Failed to send the message because a template with emphasizeType set to 'ITEM_LIST' cannot be a security template. |
| ALIMTALK | false | 21903037 | Failed to send the message because the title of templateItem contains a replacement parameter. |
| ALIMTALK | false | 21903038 | Failed to send the message because the summary title of templateItem contains a replacement parameter. |
| ALIMTALK | false | 21903039 | Failed to send the message because a summary cannot exist without a templateItem list. |
| ALIMTALK | false | 21903040 | Failed to send the message because the title (maximum 21 characters) or description (maximum 13 characters) of an itemHighlight with a thumbnail exceeds the limit. |
| ALIMTALK | false | 21903041 | Failed to send the message because imageUrl does not include http:// or https://. |
| ALIMTALK | false | 21903042 | Failed to send the message because templateHeader does not match the template. (SMS substitution on resend.) |
| ALIMTALK | false | 21903043 | Failed to send the message because templateItem or templateItemHighlight does not match the template. (SMS substitution on resend.) |
| ALIMTALK | false | 21903044 | Failed to send the message because a BF type button must be placed at the top, but this condition was violated. |
| ALIMTALK | false | 21903045 | Failed to send the message because a 'BF' link type button requires a bizFormKey, and the button name must be one of "Reserve in Talk", "Survey in Talk", or "Enter in Talk", but this condition was violated. |
| ALIMTALK | false | 21903046 | Failed to send the message because templateRepresentLink does not match the template. (SMS substitution on resend.) |
| ALIMTALK | false | 21903047 | Failed to send the message because templateTitle and the title of templateItemHighlight end with a space. |
| ALIMTALK | false | 21903048 | Failed to send the message because the template parameter length exceeds 1,000 characters. |
| ALIMTALK | false | 21903049 | Failed to send the message because the template parameters do not match the template. |
| ALIMTALK | false | 21903050 | Failed to send the message because the AC type button is required for templateMessageType (AD/MI) but is missing. |
| ALIMTALK | false | 21903100 | Failed to send the message because comments cannot be added when the template is in a registered/completed status. |
| ALIMTALK | false | 21903101 | Failed to send the message due to a non-existent quickReply name. |
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
| ALIMTALK | false | 21903208 | Failed to send the message because the FriendTalk carousel item count (2–10, or 1–10 when including an intro) is incorrect. |
| ALIMTALK | false | 21903209 | Failed to send the message because the FriendTalk carousel tail has no linkMo. |
| ALIMTALK | false | 21903210 | Failed to send the message because the FriendTalk coupon has no title or description. |
| ALIMTALK | false | 21903211 | Failed to send the message because the coupon description exceeds the limit (maximum 12 characters for FriendTalk text/image types; maximum 18 characters for wide-image/item-list types). |
| ALIMTALK | false | 21903212 | Failed to send the message because the FriendTalk coupon title is invalid. |
| ALIMTALK | false | 21903213 | Failed to send the message because FriendTalk has no mobile link or iOS/Android channel link. |
| ALIMTALK | false | 21903215 | Failed to send the message because FriendTalk wide items/carousels can only be sent as AD type, but this condition was violated. |
| ALIMTALK | false | 21903216 | Failed to send the message because the title length limit was exceeded (maximum 25 characters for the first wide item; maximum 30 characters for the 2nd through 4th wide items). |
| ALIMTALK | false | 21903217 | Failed to send the message because the FriendTalk button count is incorrect (maximum 5 for standard; maximum 4 with a coupon; maximum 2 with wide; maximum 1 with video; 1–2 for commerce). |
| ALIMTALK | false | 21903218 | Failed to send the message because the FriendTalk video URL is invalid. |
| ALIMTALK | false | 21903219 | Failed to send the message because 'content' is too long (maximum 76 characters when using video). |
| ALIMTALK | false | 21903220 | Failed to send the message because 'header' is too long (maximum 20 characters when using video). |
| ALIMTALK | false | 21903221 | Failed to send the message because a FriendTalk carousel (feed type) contains a 'head' field. |
| ALIMTALK | false | 21903222 | Failed to send the message because a FriendTalk carousel (feed type) contains an 'additionalContent' field. |
| ALIMTALK | false | 21903223 | Failed to send the message because a FriendTalk carousel (feed type) cannot contain a 'commerce' field. |
| ALIMTALK | false | 21903224 | Failed to send the message because a FriendTalk carousel (commerce type) cannot contain 'header' or 'message' fields. |
| ALIMTALK | false | 21903225 | Failed to send the message because the FriendTalk carousel button count is incorrect (maximum 2 for feed; 1–2 for commerce). |
| ALIMTALK | false | 21903226 | Failed to send the message because 'discountPrice' exists in commerce but either 'discountRate' or 'discountFixed' is missing. |
| ALIMTALK | false | 21903300 | Failed to send the message because the unsubscribe number was not found. |
| ALIMTALK | false | 21903301 | Failed to send the message because the unsubscribed recipient was not found. |
| ALIMTALK | false | 21903302 | Failed to send the message because marketing consent messages are only available for text/image/wide image/carousel feed/premium video types. |
| ALIMTALK | false | 21904000 | Failed to send the message due to an invalid parameter. |
| ALIMTALK | false | 21904001 | Failed to send the message because the appkey is already active. |
| ALIMTALK | false | 21904002 | Failed to send the message because the appkey is inactive. |
| ALIMTALK | false | 21904003 | Failed to send the message because only the last 31 days can be searched. |
| ALIMTALK | false | 21904004 | Failed to send the message because the appkey does not exist. |
| ALIMTALK | false | 21904005 | Failed to send the message because the appkey is in an inactive state. |
| ALIMTALK | false | 21904006 | Failed to send the message because the appkey has no sender key. |
| ALIMTALK | false | 21904007 | Failed to send the message because the file size is less than {}. |
| ALIMTALK | false | 21904008 | Failed to send the message because the file size must be less than 20 MB but the limit was exceeded. |
| ALIMTALK | false | 21904009 | Failed to send the message because the file extension is invalid. |
| ALIMTALK | false | 21904010 | Failed to send the message because the file was not found. |
| ALIMTALK | false | 21904011 | Failed to send the message because the recipient list was not found. |
| ALIMTALK | false | 21904012 | Failed to send the message because the maximum recipient count of 10,000 has been exceeded. |
| ALIMTALK | false | 21904013 | Failed to send the message because only jpg/jpeg extensions can be uploaded, but a different extension was used. |
| ALIMTALK | false | 21904014 | Failed to send the message because the file has no recipient_no header. |
| ALIMTALK | false | 21904015 | Failed to send the message because requestId is invalid. |
| ALIMTALK | false | 21904016 | Failed to send the message because the data does not exist. |
| ALIMTALK | false | 21904017 | Failed to send the message because messages older than 90 days cannot be searched. |
| ALIMTALK | false | 21904018 | Failed to send the message due to an attachment upload error. |
| ALIMTALK | false | 21904019 | Failed to send the message due to an invalid recipient number. |
| ALIMTALK | false | 21904020 | Failed to send the message due to a file read failure. |
| ALIMTALK | false | 21904021 | Failed to send the message because the file size must be less than 10 MB but the limit was exceeded. |
| ALIMTALK | false | 21904022 | Failed to send the message because data export failed. |
| ALIMTALK | false | 21904023 | Failed to send the message because all senders must be deleted to deactivate the product, but the condition was not met. |
| ALIMTALK | false | 21904024 | Failed to send the message because reactivating the dormant template failed. |
| ALIMTALK | false | 21904025 | Failed to send the message because a maximum of 20 templates can be uploaded at one time. |
| ALIMTALK | false | 21904026 | Failed to send the message because the uploaded template header is invalid. |
| ALIMTALK | false | 21904027 | AD/MI type conversion failed: failed to send the message because the 'buttons' length exceeds the maximum. |
| ALIMTALK | false | 21904028 | AD/MI type conversion failed: failed to send the message because the template is not in an approved status. |
| ALIMTALK | false | 21904101 | Failed to send the message due to an invalid search parameter. |
| ALIMTALK | false | 21904103 | Failed to send the message because RequestId or startRequestDate/endRequestDate is invalid. |
| ALIMTALK | false | 21904104 | Failed to send the message because the RequestId value is empty. |
| ALIMTALK | false | 21904200 | Failed to send the message because the resend message is invalid. |
| ALIMTALK | false | 21905000 | Failed to send the message due to an invalid RecipientNo. |
| ALIMTALK | false | 21907000 | Failed to send the message due to a vendor API request failure. |
| ALIMTALK | false | 21908000 | Failed to send the message because 'imageSeq' is empty. |
| ALIMTALK | false | 21908001 | Failed to send the message because the uploaded image is invalid. |
| ALIMTALK | false | 21908002 | Failed to send the message because the required image (e.g., for carousel-feed or commerce) is missing. |
| ALIMTALK | false | 21908003 | Failed to send the message because image deletion failed. |
| ALIMTALK | false | 21908004 | Failed to send the message because the 'createUser' length exceeds 100 characters. |
| ALIMTALK | false | 21908005 | Failed to send the message because the project has no Plus Friend. (Register a Plus Friend first.) |
| ALIMTALK | false | 21908006 | Failed to send the message because the content does not include authentication guidance. |
| ALIMTALK | false | 21908007 | Failed to send the message because the storage settings are empty. |
| ALIMTALK | false | 21908008 | Failed to send the message because the content contains a prohibited word. |
| ALIMTALK | false | 21908009 | Failed to send the message because this project is already shared. |
| ALIMTALK | false | 21908010 | Failed to send the message because image upload failed due to an unexpected error. |
| ALIMTALK | false | 21908011 | Failed to send the message because the image type is invalid. |
| ALIMTALK | false | 21909993 | Failed to send the message because a required request part is missing. |
| ALIMTALK | false | 21909994 | Failed to send the
