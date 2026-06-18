<!-- pre-align:aligned sig=d17b5d1143ac -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>統計</h1>

**Notification > Notification Hub > 統計**


## 統計

Notification Hub で発生するさまざまなイベントを収集し、統計データとして照会できます。

<a id="query-statistics"></a>

### 統計照会

送信されたメッセージの受信結果を、受信者の連絡先単位で照会できます。

* メッセージチャンネル、送信タイミング（即時、予約）、送信目的、送信/受信/開封状態を組み合わせて設定し、連絡先の受信結果を照会します。
* 照会時の期間はリクエスト日時を基準に設定します。
    * 照会期間の設定可能範囲は、デフォルトで最大 7 日間です。
    * 最大 180 日前まで照会できます。
* 詳細条件のいずれか 1 つを追加で選択し、連絡先の受信結果を照会できます。
    * メッセージ ID、テンプレート名、フロー名、統計キー名、発信情報、受信者情報

* メッセージチャンネル、統計基準、統計キー、メッセージ ID を組み合わせて設定し、統計データを照会します。
* 設定したメッセージチャンネルによって、設定できる統計基準が異なります。

<a id="message-channel-statistical-events-by-statistical-criteria"></a>

#### メッセージチャンネル・統計基準別の統計イベント

| メッセージチャンネル | 統計基準 | イベント | 備考 |
| - | - |---------------------------------------------------------------------------------------------------------------------|------------------------|
| 全体 | メッセージ | リクエスト済み(REQUESTED)、リクエスト取消(CANCELED)、送信済み(SENT)、送信失敗(SEND_FAILED)、受信済み(DELIVERED)、受信失敗(DELIVERY_FAILED) | 送信プロセスで発生したイベントです。 |
| SMS | メッセージ | リクエスト済み(REQUESTED)、リクエスト取消(CANCELED)、送信済み(SENT)、送信失敗(SEND_FAILED)、受信済み(DELIVERED)、受信失敗(DELIVERY_FAILED) | |
| RCS | メッセージ | リクエスト済み(REQUESTED)、リクエスト取消(CANCELED)、送信済み(SENT)、送信失敗(SEND_FAILED)、受信済み(DELIVERED)、受信失敗(DELIVERY_FAILED) | |
| お知らせトーク | メッセージ | リクエスト済み(REQUESTED)、リクエスト取消(CANCELED)、送信済み(SENT)、送信失敗(SEND_FAILED)、受信済み(DELIVERED)、受信失敗(DELIVERY_FAILED) | |
| ブランドメッセージ | メッセージ | リクエスト済み(REQUESTED)、リクエスト取消(CANCELED)、送信済み(SENT)、送信失敗(SEND_FAILED)、受信済み(DELIVERED)、受信失敗(DELIVERY_FAILED) | |
| Push | メッセージ | リクエスト済み(REQUESTED)、リクエスト取消(CANCELED)、送信済み(SENT)、送信失敗(SEND_FAILED)、受信済み(DELIVERED)、受信失敗(DELIVERY_FAILED)、開封済み(OPENED) | メッセージ開封に関するイベントも収集されます。 |
| Email | メッセージ | リクエスト済み(REQUESTED)、リクエスト取消(CANCELED)、送信済み(SENT)、送信失敗(SEND_FAILED)、受信済み(DELIVERED)、受信失敗(DELIVERY_FAILED)、開封済み(OPENED) | メッセージ開封に関するイベントも収集されます。 |
| SMS | 国際 SMS メッセージ | リクエスト済み(REQUESTED)、リクエスト取消(CANCELED)、送信済み(SENT)、送信失敗(SEND_FAILED)、受信済み(DELIVERED)、受信失敗(DELIVERY_FAILED)、実送信(CONCAT) | 実送信：国際 SMS メッセージに限り、Concatenated message（連結）機能を通じて送信された実際のメッセージ送信件数 |

<a id="manage-statistical-keys"></a>

### 統計キー管理

メッセージ送信時に統計キーを設定すると、統計照会において統計キーを照会条件として指定し、同じ統計キーで送信されたメッセージの統計データを照会できます。

1. **[+ 統計キー追加]** をクリックします。
2. 統計キー名、詳細説明、収集期間を設定します。
    * 収集期間を無制限に設定できます。
    * 期限のないお知らせや定期的な送信が必要なメッセージに設定する統計キーが該当します。
3. 収集期間前または収集期間が過ぎた統計キーで発生したイベントは収集されません。
    * 特定の期間中に実施するキャンペーンやイベントの場合、収集期限を設定して統計イベントを収集できます。
