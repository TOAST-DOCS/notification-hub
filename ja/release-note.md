<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Notification Hubリリースノート</h1>

**Notification > Notification Hub > リリースノート**

## 2025. 04. 15.
### 機能追加
* [API/Console]サービスで発生する様々なイベント履歴をCloudTrailで確認できます。
    * 確認可能なイベントリストは[[CloudTrail > 収集されるイベントリスト]](../../../Governance%20&%20Audit/CloudTrail/ko/event-list)を参照してください。
* [API/Console] RCS認証用メッセージ送信が追加されました。
* [API]連絡先別受信結果リスト照会APIにレスポンスフィールドが追加されました。
  * 詳細は[[API v1.0使用ガイド > 連絡先別受信結果 > 連絡先別受信結果リスト照会]](./api-guide-v1x0/contact-delivery-result/#_1)を参照してください。
* [Console] RCS BizCenter LMSフォーマット型サポート
  * RCSメッセージ送信時、LMSフォーマット型で送信できます。
  * テンプレート作成時にLMSフォーマット型を選択できます。

### 機能改善
* [API/Console] Pushチャンネルの受信、開封イベントが統計に収集されるように改善しました。

## 2024. 11. 12.

### Notification Hubベータ(beta)リリース

### バグ修正
* [Console]エラー修正
    * 送信、フロー、テンプレート、統計機能のエラーを修正しました。
* [API]認証エラー修正
    * 一部のAPIリクエスト時に認証が正常に処理されない問題を修正しました。
    
## 2024. 10. 29.

### Notification Hubアルファ(alpha)リリース
* 使い方案内
    * アルファでリリースされた商品は**サポート > 1:1お問い合わせ**を通じて使用できます。
* [Console]コンソール公開
    * 送信、送信照会、アドレス帳、テンプレート、フロー、詳細設定、統計、本人認証タブを追加しました。
* [API] API v1.0追加
    * メッセージ、連絡先受信結果リスト照会、テンプレート、フローAPI v1.0を追加しました。
