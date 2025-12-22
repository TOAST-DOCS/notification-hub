<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Statistics</h1>

**Notification > Notification Hub > Statistics**


## Statistics

You can collect various events that occur in Notification Hub and query them with statistical data.

### Query Statistics

You can view the reception results of the delivered message by receiver contacts.

* Check contact reception results by setting a combination of message channels, delivery time (immediate, schedule), delivery purpose, and delivered/received/query status.
* The query period is set as the date and time of the request.
    * The default range for setting the inquiry period is up to 7 days.
    * You can view the results up to 180 days in the past.
* You can select one of the additional detailed conditions to view the results of receiving of your contact.
    * message ID, template name, flow name, statistics key name, delivery information, receiver information

* Check statistical data by setting a combination of message channels, statistical criteria, statistical keys, and message IDs.
* Depending on the message channel you set, the statistical criteria you set can be varied.

#### Message Channel, Statistical Events by Statistical Criteria

| Message Channel | Statistical Criteria | Events                                                                                                       | Remarks | 
| - | - |----------------------------------------------------------------------------------------------------------| - | 
| Full | Message | Request (REQUESTED), Cancel Request (CANCED), Send (SENT), Send (SEND_FAILED), received (DELIVERED) Fail to Receive (DELIVERY_FAILED) | Events that occurred during the sending process | 
| SMS | Message | Request (REQUESTED), Cancel Request (CANCED), Send (SENT), Fail to Send (SEND_FAILED), received (DELIVERED) Fail to Receive (DELIVERY_FAILED)    | | 
| RCS | Message | Request (REQUESTED), Cancel Request (CANCED), Send (SENT), Fail to Send (SEND_FAILED), received (DELIVERED) Fail to Receive (DELIVERY_FAILED)    | | 
| AlimTalk| Message | Request (REQUESTED), Cancel Request (CANCED), Send (SENT), Fail to Send (SEND_FAILED), received (DELIVERED) Fail to Receive (DELIVERY_FAILED)    | |
| Push | Message | Request (REQUESTED), Cancel Request (CANCED), Send (SENT), Fail to Send (SEND_FAILED), received (DELIVERED) Fail to Receive(DELIVERY_FAILED), open(OPENED) | Events for opening messages are also collected. | 
| E-mail | Message | Request (REQUESTED), Cancel Request (CANCED), Send (SENT), Fail to Send (SEND_FAILED), received (DELIVERED) Fail to Receive(DELIVERY_FAILED), open(OPENED) | Events for opening messages are also collected. | 
| SMS | International Message | Request (REQUESTED), Cancel Request (CANCED), Send (SENT), Fail to Send (SEND_FAILED), received (DELIVERED) Fail to Receive(DELIVERY_FAILED  | |

### Manage Statistical Keys

If you set a statistics key when sending message, you can set the statistics key as a query condition in a statistics query to view the statistical data of messages sent with the same statistics key.

1. Click **+ Add Statistics Key**.
2. Sets the statistical key name, detailed description, and collection period.
    * You can set a collection period as unlimited.
    * This is the statistical key that is set for messages that require unscheduled announcements or periodic sending.
3. Events that occur with statistics keys that doesn’t yet reach the collection period or already passed the collection period are not collected.
    * For campaigns or events that run during a specific period of time, statistical events can be collected by setting a collection deadline.