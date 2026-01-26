<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Notification Hub Overview</h1>

**Notification > Notification Hub > Overview**

It is a cloud-based integrated messaging platform that sends and manages push, email, SMS, RCS, and AlimTalk messages. Notification Hub integrates various message channels to send and manage messages. Flow sending also allow multiple message channels to be sent sequentially in order of priority. By sharing settings and resources with other Notification products, existing Notification customers can quickly transition to Notification Hub.

![Overall structure](../img/overview_800.png)

## Multichannel messaging

* Sends messages to 6 messaging channels: SMS, Alim Talk, RCS, Email, and Push.
  * Uses a single API to integrate and manage multiple message channels for easy sending

## Address Book

* Organizes your receivers' contacts (email, phone number, token).
  * Categorizes receivers by group
  * You can prevent unnecessary sending of messages by managing receiver's Unsubscription history.

## Template

* Adds and manages templates for all message channels.
  * With templates, you can reduce repetitive message creation and easily send out messages consistently.

## Flow

* Creates a flow with pre-defined templates
  * Sends messages simultaneously to maximum 6 channels with a flow, and automatically sends messages to the next channel in the preset send order when a message fails to be received due to device status.
  * Depending on how the message channel is prioritized, it can be used for a variety of purposes, such as increasing reception ratio or saving delivery costs.

## Mass Delivery

* Sends messages to multiple receivers at once.
  * Uploads a receiver file
  * Uploads an Excel file with a list of receivers for sending.
  * Distinguishes between valid and invalid receivers of an uploaded Excel file.

## Guide to sharing resource and feature settings between Notification Services

* The resource and feature settings of NHN Cloud Notification's Push, SMS, RCS Bizmessage, KakaoTalk Bizmessage, and Email services are shared with the Notification Hub service. (For example, when SMS service registers a sender number, the sender number is shared by Notification Hub service.)
Existing NHN Cloud Notification users can easily switch to and use the Notification Hub service.
  * Sharing items
    * Resource
      * Address book
      * Sender information
      * Statistics Key
      * Identity verification
    *  Feature setting
      * Detailed settings (by message channel)

## Delivery volume Limit Guidance

* Some message channels limit the volume of delivery.
  * SMS
    * SMS limits the number of deliveries to 5,000 per month per organization.
      * Regardless of the type of delivery (SMS, LMS, MMS), it is calculated by summing both SMS and Notification Hub services.
      * Calculate the delivery volume based on delivery.
  * AlimTalk
    * AlimTalk limits the delivery volume to 1,000 per project per day.
* Monthly delivery volume can be seen in **Console**>**Organization**>**Project**>**Quarter Management**.
* Contact **Customer Center**>**1:1:1 Inquiry** if you need to adjust your monthly delivery volume.
  * [1:1 Inquiry Shortcut](https://www.nhncloud.com/kr/support/inquiry)
* For resource provision policies, see **User Guide**>**NHN Cloud**>**Resource Provision Policy**.
  * [ Resource Provision Policy Shortcut ](https://docs.nhncloud.com/ko/nhncloud/ko/resource-policy/)

## Information on Processing of Personal Information

In the process of using the Notification Hub service, customers can collect the user's personal information. Therefore, customers who use this service must inform users of legal notices and obtain consent in accordance with the Personal Information Protection Act.
In addition, this process may result in a consignment relationship between the customer and NHN Cloud regarding the processing of personal information. Customers in the position of a consignor can enter into a separate written consignment contract with the consignee, NHN Cloud, and can refer to the following information to notify the personal information processing policy operated by the customer.

* Consignee: NHN Cloud Corp.
* Contents of consignment work: Notification Hub service provision work

## Terms and Conditions

* [Notification Terms and Conditions Shortcut](https://kr1-0lodw5frr5-real.api.nhncloudservice.com/popup/terms)
