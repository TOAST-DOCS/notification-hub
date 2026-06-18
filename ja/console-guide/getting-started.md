<!-- pre-align:aligned sig=674d72b2ce04 -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a { 
    display: inline !important;
}
</style>
<h1>Notification Hubを始める</h1>

**Notification > Notification Hub > コンソール使用ガイド > Notification Hubを始める**

<span id="identity-verification"></span>

## 本人認証を行う

Notification Hubは有効化後、本人認証を完了する必要があります。本人認証の詳細については、**利用ポリシーおよび事前設定案内 > 本人認証**の項目をご確認ください。

* [本人認証ガイドへ](../service-policy-and-precondition/identity-verification)


<span id="manage-sender-info"></span>

<a id="sender-information-management"></a>

## 発信情報管理

<span id="manage-sender-phone-number"></span>

<a id="sender-number-management"></a>

### 発信番号管理

SMS、LMS、MMS メッセージを送信するには、発信番号を登録する必要があります。発信番号登録の審査をリクエストし、審査が承認されると発信番号が登録されます。

1. **[+ 発信番号登録]** をクリックし、**[個人情報収集利用同意書]** に同意します。
2. 登録する発信番号のタイプを選択し、発信番号を入力します。
3. 発信番号タイプに必要な書類を添付します。

発信番号事前登録制の詳細については、**利用ポリシーおよび事前設定ガイド > SMS > 発信番号事前登録制施行**を参照してください。

* [発信番号事前登録制施行へ移動](../service-policy-and-precondition/sms#sender-phone-number-pre-registration)

<span id="manage-sender-brand"></span>

<a id="brand-management"></a>

### ブランド管理

RCS Bizmessage を送信するには、ブランド連携を完了する必要があります。RCS Biz Center で事前登録事項が完了（ブランド承認）している場合は、NHN Cloud コンソールとの連携を進めます。RCS Biz Center でのブランド作成については、**利用ポリシーおよび事前設定ガイド** > **RCS** を参照してください。

* [利用ポリシーおよび事前設定ガイド > RCS へ移動](../service-policy-and-precondition/rcs)
* [RCS Biz Center へ移動](https://www.rcsbizcenter.com/main)

RCS Biz Center でブランド作成および代理店設定、チャットルーム（発信番号）登録、テンプレート登録が完了（承認）したら、コンソールでブランドを連携します。

* **[+ ブランド連携]** をクリックすると、同期が完了します。

<span id="manage-sender-domain"></span>

<a id="manage-domains"></a>

### ドメイン管理

メールを送信するには、自身が所有するドメイン、SPF 認証、DKIM 認証、DMARC 認証が必要です。

発信ドメインおよび SPF、DKIM、DMARC の詳細については、**利用ポリシーおよび事前設定ガイド > メール**を確認してください。

* [利用ポリシーおよび事前設定ガイド > メールへ移動](../service-policy-and-precondition/email)

<a id="email-domain-registration-and-ownership-authentication"></a>

#### メールドメイン登録および所有権認証

ドメインを登録し、ドメインの所有権を確認する必要があります。Notification Hub が提供した値をメールドメインの DNS TXT レコードに登録します。提供された値と登録済みドメインの TXT レコードが一致するかどうかで所有権を認証します。

1. **[+ ドメイン登録]** をクリックします。
2. 登録するルートドメインを入力し、**[検証]** をクリックします。
3. 検証に成功したら、**[登録]** をクリックして登録を完了します。
4. ドメイン一覧でドメイン所有認証状態の **[認証]** をクリックします。

ドメイン所有認証に成功すると、ドメイン認証状態が「完了」に変更されます。

<a id="spf-authentication"></a>

#### SPF 認証

SPF（sender policy framework、送信者ポリシーフレームワーク）は、メール送信者と送信サーバーの信頼性を検証するためのメカニズムです。メール受信サーバーが特定のドメインから送信されたメールが、実際に許可されたメール送信サーバーから届いたものかどうかを確認します。メール受信サーバーは、送信者のメールドメイン DNS に登録された SPF レコードを確認し、登録されていない IP アドレスから送信されたメールをスパムとして処理します。

**SPF**
```
v=spf1 include:_spfblocka.toast.com ~all
```

1. 上記 **SPF** 項目の SPF レコードをドメインの TXT レコードに登録します。
2. 一覧からドメインを選択します。
3. **[SPF レコード認証状態]** 項目の **[状態確認]** をクリックして、SPF 認証を完了します。


!!! danger "注意事項"
    * ドメインの TXT レコードには、SPF レコードを 1 つだけ登録する必要があります。ドメインの TXT レコードに 2 つ以上の SPF レコードが登録されている場合、SPF 認証が失敗し、メール受信サーバーが受信を拒否する可能性があります。
    * SPF レコードを検査する際に DNS 照会が発生するメカニズム（include）および修飾子（redirect）の使用は最大 10 個に制限されており、これを超えるとメール受信サーバーで受信を拒否する可能性があります。

SPF の詳細については、以下のドキュメントを参照してください。

* [メールセキュリティ強化機能紹介（SPF）へ移動](https://meetup.nhncloud.com/posts/244)
* [RFC 4408 - 4.5 Selecting Records へ移動](https://datatracker.ietf.org/doc/html/rfc4408#section-4.5)
* [RFC 4408 - 10.1 Processing Limits へ移動](https://datatracker.ietf.org/doc/html/rfc4408#section-10.1)

<a id="dkim-authentication"></a>

#### DKIM 認証

DKIM（domainkeys identified mail、ドメインキー識別メール）は、メール送信サーバーがメールにデジタル署名を行い、メール受信サーバーが送信者の真正性を確認することで、転送中にメッセージが偽造・改ざんされていないかどうかを検証するメール認証方式です。DKIM を使用することで、スパム送信者およびその他の悪意ある攻撃者によるメールの偽造・改ざんを防ぐことができます。

1. ドメイン所有認証の完了後、一覧からドメインをチェックし、**[DKIM 設定]** をクリックします。
2. DKIM 認証のために提供された DNS ホスト名に TXT レコードの値を設定し、下部の **[認証]** をクリックします。
    * 登録したドメインが `example.com` の場合、`toast._domainkey.example.com` の TXT レコードに値を設定する必要があります。
3. 認証完了後、使用設定を行い **[保存]** をクリックして DKIM 認証を完了します。

DKIM の詳細については、以下のドキュメントを参照してください。

* [メールセキュリティ強化機能紹介 - ドメイン保護、DKIM、DMARC へ移動](https://meetup.nhncloud.com/posts/248)


<a id="dmarc-authentication"></a>

#### DMARC 認証

DMARC（domain-based message authentication reporting and conformance）は、メールセキュリティ強化機能の最終ステップです。メールスプーフィングを利用したフィッシングや詐欺などを防ぐための、ドメインベースのメッセージ認証に関するレポートおよび準拠ポリシーです。メール受信サーバーは、送信者アドレス（From）ドメインの DNS から DMARC レコードを照会します。DMARC レコードに定義されたポリシーに従い、受信サーバーは受信したメールを認証します。

**DMARC**
```
"v=DMARC1;p=none;sp=quarantine;pct=100;rua=mailto:${보고서를_수신할_이메일_주소}"
```

1. 上記 **DMARC** 項目の値に DMARC レポートを受信するメールアドレスを追加し、DMARC TXT レコードを完成させます。
2. `_dmarc.` が追加されたサブドメインの TXT レコードに登録します。
    * 例：ドメインが `example.com` の場合、`_dmarc.example.com` の TXT レコードに登録します。
3. **[DMARC 認証状態]** 項目の **[状態確認]** をクリックして、DMARC 認証を完了します。

DMARC の詳細については、以下のドキュメントを参照してください。

* [メールセキュリティ強化機能紹介 - ドメイン保護、DKIM、DMARC へ移動](https://meetup.nhncloud.com/posts/248)

##### ドメイン保護

ドメイン保護が有効化されたドメインは、他のプロジェクトで使用することができません。保護されたドメインを他のプロジェクトで使用するには、同様にドメイン登録と所有認証を受ける必要があります。

!!! danger "注意事項"
    ドメイン保護を無効化すると、他のプロジェクトで任意にドメインを使用できるようになります。すべての認証を完了したドメインの場合、他のプロジェクトから送信するメールも同様にメール受信サーバーで正常に受信されます。このように送信されたメールがスパムやフィッシングである場合、受信者に被害が発生する可能性があり、ドメインの評判が低下してメール受信サーバーで受信を拒否される可能性があります。

<span id="manage-sender-push-authorization"></span>

<a id="push-authentication-management"></a>

### Push 認証管理

Push 認証情報の発行方法については、**利用ポリシーおよび事前設定ガイド > Push** を確認してください。

* [利用ポリシーおよび事前設定ガイド > Push へ移動](../service-policy-and-precondition/push)

<a id="fcm-authentication-settings"></a>

#### FCM 認証設定
1. **[サービスアカウントキー登録]** を有効にします。
2. サービスアカウントキー（JSON）に、発行した FCM Service Account Credential ファイルの内容をコピーして貼り付けます。
3. **[検証 > 保存]** をクリックして設定を完了します。

<a id="pns-authentication-settings"></a>

#### APNS 認証設定
1. **[APNS JWT 証明書登録]** を有効にします。
2. **[チーム ID]** と **[キー ID]** を入力します。
3. **[トピック]** を入力します。トピックはアプリのバンドル ID（Bundle ID）です。
4. **[秘密鍵]** ファイルの内容をコピーして貼り付けます。
5. **[検証 > 保存]** をクリックして設定を完了します。

<a id="adm-authentication-settings"></a>

#### ADM 認証設定
1. **[認証情報登録]** を有効にします。
2. **[クライアント ID]** と **[クライアントキー]** を入力します。
3. **[検証 > 保存]** をクリックして設定を完了します。

<span id="manage-sender-profile"></span>

<a id="manage-outgoing-profiles"></a>

### 発信プロフィール管理

お知らせトーク、ブランドメッセージを送信するには、発信プロフィールの作成および登録が必要です。

発信プロフィールの作成はカカオビジネスで行うことができます。

* [発信プロフィール作成ガイドへ移動](../service-policy-and-precondition/alimtalk-and-friendtalk)


カカオビジネスで発信プロフィールの作成が完了したら、次の手順に従って登録します。

1. **[+ 発信プロフィール登録]** をクリックし、発信プロフィール ID、管理者の携帯電話番号、カテゴリを設定してから **[トークンリクエスト]** をクリックします。
2. 管理者の携帯電話に送信されたトークンを入力し、**[確認 > 登録]** をクリックすると、発信プロフィールの登録が完了します。


<span id="manage-080-unsubscription-number"></span>

<a id="manage-opt-out-numbers"></a>

### 080 受信拒否番号管理

080 受信拒否番号は、広告メッセージ送信時に受信者に受信拒否手段を提供するサービスです。広告性情報を送信する際は、受信者が受信拒否または受信同意の撤回を無料で行えるよう、無料の受信拒否方法を必ず記載する必要があります。

<a id="apply-subscription"></a>

#### 加入申請

* **[+ 080 受信拒否番号申請]** をクリックし、会社名を入力します。入力した会社名は、080 受信拒否番号に電話をかけた際に案内される業者名として使用されます。
* 加入申請を完了すると、登録予約状態に変更されます。080 受信拒否サービスの開通には営業日基準で 3〜4 日かかり、開通が完了すると使用できるようになります。
* 開通が完了すると、使用開始日時と状態を確認できます。080 受信拒否サービスが登録予約・使用中の状態では、SMS 商品の利用終了はできません。解約後に商品利用終了が可能です。解約するには **[解約]** をクリックしてください。

<a id="set-080-unsubscription-number-when-advertising-texts"></a>

#### 広告性メッセージ送信時の 080 受信拒否番号設定

* 080 受信拒否番号が開通済みの状態でのみ広告メッセージを送信できます。
* **[送信 > SMS]** タブで送信目的を「広告」に選択すると、080 受信拒否番号の選択ウィンドウが表示されます。
* **[選択適用]** をクリックすると、広告性必須文言を追加できます。
* 広告性送信時は、メッセージ本文に必ず広告性必須文言を含める必要があります。ルールは次のとおりです。
    * 開始文言：(광고)
    * 末尾文言：무료수신 거부 {080수신 거부번호} または 무료거부 {080수신 거부번호}（当該文言には空白が含まれる場合があります。）

##### 例
```
(광고)

[무료 수신 거부]080XXXXXXX
```
```
(광고)

무료거부 080XXXXXXX
```
