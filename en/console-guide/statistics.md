<!-- pre-align:aligned sig=d17b5d1143ac -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Statistics</h1>

**Notification > Notification Hub > Statistics**


## Statistics

You can collect various events that occur in Notification Hub and view them as statistical data.

<a id="query-statistics"></a>

### Query Statistics

You can view the received results of sent messages by recipient contact unit.

* You can query contact received results by combining multiple conditions: message channel, sending time (immediate or scheduled), message purpose, and send/receive/open status.
* Set the query period based on the request date and time.
    * The default maximum query period is 7 days.
    * You can query data up to 180 days in the past.
* You can additionally select one of the detailed conditions to query contact received results.
    * Message ID, template name, flow name, statistics key name, sender information, recipient information

* You can query statistical data by combining multiple conditions: message channel, statistics criteria, statistics key, and message ID.
* The statistics criteria that can be set vary depending on the message channel that you select.

<a id="message-channel-statistical-events-by-statistical-criteria"></a>

#### Statistical Events by Message Channel and Statistics Criteria

| Message Channel | Statistics Criteria | Events | Notes |
| - | - |---------------------------------------------------------------------------------------------------------------------|------------------------|
| All | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED | Events that occur during the sending process. |
| SMS | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED | |
| RCS | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED | |
| AlimTalk | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED | |
| Brand Message | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED | |
| Push | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED, OPENED | Open events for messages are also collected. |
| Email | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED, OPENED | Open events for messages are also collected. |
| SMS | International SMS Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED, CONCAT | CONCAT: The actual number of messages sent via the Concatenated Message feature, applicable only to international SMS messages. |

<a id="manage-statistical-keys"></a>

### Manage Statistics Keys

When you set a statistics key during message sending, you can use that key as a query condition in the statistics view to retrieve statistical data for all messages sent with the same statistics key.

1. Choose **+ Add Statistics Key**.
2. Set the statistics key name, detailed description, and collection period.
    * You can set the collection period to unlimited.
    * This applies to statistics keys set for notices with no expiration date or messages that require periodic sending.
3. Events generated with a statistics key whose collection period has not started or has already ended are not collected.
    * For campaigns or events that run for a specific period, you can define a collection period to collect statistical events.