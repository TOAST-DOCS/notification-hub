<!-- pre-align:aligned sig=d17b5d1143ac -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Statistics</h1>

**Notification > Notification Hub > Statistics**


## Statistics

You can collect various events generated in Notification Hub and retrieve them as statistical data.

<a id="query-statistics"></a>

### Query Statistics

You can retrieve the received results of sent messages by the recipient's contact unit.

* Set a combination of message channel, sending time (immediate or scheduled), message purpose, and send/receive/open status to retrieve contact received results.
* Set the period based on the request date and time when querying.
    * The default maximum query period range is 7 days.
    * You can query up to 180 days in the past.
* You can select one additional detailed condition to retrieve contact received results.
    * Message ID, template name, flow name, statistics key name, sender information, recipient information

* Set a combination of message channel, statistical criteria, statistics key, and message ID to retrieve statistical data.
* The statistical criteria that can be configured vary depending on the message channel that is set.

<a id="message-channel-statistical-events-by-statistical-criteria"></a>

#### Statistical Events by Message Channel and Statistical Criteria

| Message Channel | Statistical Criteria | Events | Notes |
| - | - | - | - |
| All | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED | Events generated during the sending process. |
| SMS | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED | |
| RCS | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED | |
| AlimTalk | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED | |
| Brand Message | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED | |
| Push | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED, OPENED | Open events for messages are also collected. |
| Email | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED, OPENED | Open events for messages are also collected. |
| SMS | International SMS Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED, CONCAT | CONCAT: The actual number of messages sent via the Concatenated message feature, applicable only to international SMS messages. |

<a id="manage-statistical-keys"></a>

### Manage Statistics Keys

When you set a statistics key when sending a message, you can use the statistics key as a query condition in the statistics query to retrieve statistical data for messages sent with the same statistics key.

1. Click **+ Add Statistics Key**.
2. Set the statistics key name, detailed description, and collection period.
    * You can set the collection period to unlimited.
    * This applies to statistics keys set for notices without an expiration date or messages that require periodic sending.
3. Events generated with a statistics key whose collection period has not yet started or has already ended are not collected.
    * For campaigns or events running during a specific period, you can set a collection deadline to collect statistical events.