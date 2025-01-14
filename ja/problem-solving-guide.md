<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Notification Hubトラブルシューティング</h1>

**Notification > Notification Hub > トラブルシューティング**

<span id="sms-delivery-failure"></span>

## 本人認証を進行できません。

Notification Hubは事業者会員のみ本人認証を行うことで使用できます。個人会員の場合、本人認証を行うことができません。事業者会員として再入会後、本人認証を行ってください。

## 事業者会員として登録しましたが、本人認証ができません。

Notification Hubで事業者会員の基準は、有効化したプロジェクトの組織のオーナー(OWNER)会員のタイプに従います。組織のオーナー会員が個人会員の場合、事業者会員として本人認証を行うことができません。組織のオーナー会員を事業者会員に変更した後、本人認証を行ってください。

## 送信したメールが一部の受信者端末で受信されません。

受信者の端末でメールが届かない場合、受信者の番号が**番号盗用メールブロックサービス**または**通信会社の迷惑メールブロックサービス**に加入している可能性があります。サービスを解除して再度送信してください。**番号盗用メールブロックサービス**と**通信会社の迷惑メールブロックサービス**の詳細については、以下のリンクをご確認ください。

* [番号盗用メールブロックサービス案内](service-policy-and-precondition/2-sms#about-phone-scam-blocking-services)
* [サービスプロバイダースパムブロックサービス案内](service-policy-and-precondition/2-sms#about-phone-scam-blocking-services)

## iPhoneでプッシュメッセージが受信されず、登録したトークンが削除されます。

iPhoneアプリでトークンを登録し、プッシュメッセージを送信したが、プッシュメッセージが受信されず、登録されたトークンが削除される場合は、以下の事項をご確認ください。

* **APNS JWT認証情報の不一致**
    * Notification Hubに登録されたAPNS JWT認証情報とアプリが不一致の場合、プッシュメッセージが受信されません。 APNS JWT認証情報とアプリのバンドルIDが一緒に使用できるか確認してください。
* **アプリのビルドタイプと登録されたトークンの連絡先タイプ(Contact Type)不一致**
    * アプリのビルドタイプと登録されたトークンの連絡先タイプが一致しない場合、プッシュメッセージが受信されません。連絡先タイプとビルドモードをご確認ください。
    * 開発(Development)アプリのトークンは連絡先タイプがTOKEN_APNS_SANDBOX、またはTOKEN_APNS_SANDBOX_VOIPで登録する必要があります。
    * 運営(Production)アプリのトークンは連絡先タイプがTOKEN_APNS、またはTOKEN_APNS_VOIPで登録する必要があります。
    * 各連絡先タイプはSDKでは次のとおりです。
        * TOKEN_APNS: APNS
        * TOKEN_APNS_SANDBOX: APNS_SANDBOX
        * TOKEN_APNS_VOIP: APNS_VOIP
        * TOKEN_APNS_SANDBOX_VOIP: APNS_SANDBOXVOIP

## Android端末でプッシュメッセージが受信されず、登録されたトークンが削除されます。
  
Androidアプリでトークンを登録し、プッシュメッセージを送信したが、プッシュメッセージが受信されず、登録されたトークンが削除される場合は、以下の事項を確認してください。

* **FCMサービスアカウントキー(JSON)とアプリの発信者ID(Sender ID)不一致**
    * Notification Hubに登録されたFCMサービスアカウントキー(JSON)とアプリの送信者ID(Sender ID)が不一致の場合、プッシュメッセージを受信できません。 FCMサービスアカウントキー(JSON)とアプリの送信者ID(Sender ID)を一緒に使用できるか確認してください。
        * [FCM - 発信者IDの説明](https://firebase.google.com/docs/cloud-messaging/concept-options#credentials)
        * [FCM - サービスアカウントキー(JSON)作成ガイドへ](https://firebase.google.com/docs/cloud-messaging/http-server-ref)
        ```
            A registration token is tied to a certain group of senders. 
            When a client app registers for FCM, it must specify which senders are allowed to send messages. 
            You should use one of those sender IDs when sending messages to the client app. 
            If you switch to a different sender, the existing registration tokens won't work.
        ```


!!! tip 「問題が解決しない場合」
    * オンライン1:1お問い合わせ: [https://www.nhncloud.com/kr/support/inquiry?alias=tab5_03](https://www.nhncloud.com/kr/support/inquiry?alias=tab5_03)
    * 代表電話: 1588-7967 (運営時間:月～金10:00-19:00)
