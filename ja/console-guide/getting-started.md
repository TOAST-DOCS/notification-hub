<!-- pre-align:aligned sig=674d72b2ce04 -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a { 
    display: inline !important;
}
</style>
<h1>Notification Hubを始める</h1>

**Notification > Notification Hub > コンソール使用ガイド > Notification Hubを始める**

<span id="identity-verification"></span>

## 本人確認を行う

Notification Hubは有効化後、本人確認を完了する必要があります。本人確認の詳細については、**利用ポリシーおよび事前設定ガイド > 本人確認**の項目を参照してください。

* [本人確認ガイドへ移動](../service-policy-and-precondition/identity-verification)


<span id="manage-sender-info"></span>

<a id="sender-information-management"></a>

## 送信情報管理

<span id="manage-sender-phone-number"></span>

<a id="sender-number-management"></a>

### 発信番号管理

SMS、LMS、MMS メッセージを送信するには、発信番号を登録する必要があります。発信番号登録の審査をリクエストし、審査が承認されると発信番号が登録されます。

1. **[+ 発信番号登録]** をクリックし、**[個人情報収集・利用同意書]** に同意します。
2. 登録する発信番号タイプを選択し、発信番号を入力します。
3. 発信番号タイプに必要な書類を添付します。

発信番号事前登録制度の詳細については、**利用ポリシーおよび事前設定案内 > SMS > 発信番号事前登録制度の施行**を参照してください。

* [発信番号事前登録制度の施行はこちら](../service-policy-and-precondition/sms#sender-phone-number-pre-registration)

<span id="manage-sender-brand"></span>

<a id="brand-management"></a>

### ブランド管理

RCS メッセージを送信するには、ブランド連携を完了する必要があります。RCS Biz Center での事前登録（ブランド承認）が完了したら、NHN Cloud コンソールとの連携を進めます。RCS Biz Center でのブランド作成については、**利用ポリシーおよび事前設定案内** > **RCS** を参照してください。

* [利用ポリシーおよび事前設定案内 > RCS はこちら](../service-policy-and-precondition/rcs)
* [RCS Biz Center はこちら](https://www.rcsbizcenter.com/main)

RCS Biz Center でブランド作成、代理店設定、チャットルーム（発信番号）登録、テンプレート登録が完了（承認）したら、コンソールでブランドを連携します。

* **[+ ブランド連携]** をクリックすると、同期が完了します。

<span id="manage-sender-domain"></span>

<a id="manage-domains"></a>

### ドメイン管理

メールを送信するには、所有するドメイン、SPF 認証、DKIM 認証、DMARC 認証が必要です。

送信ドメインおよび SPF、DKIM、DMARC の詳細については、**利用ポリシーおよび事前設定案内 > メール**を確認してください。

* [利用ポリシーおよび事前設定案内 > メールはこちら](../service-policy-and-precondition/email)

<a id="email-domain-registration-and-ownership-authentication"></a>

#### メールドメイン登録および所有権認証

ドメインを登録し、ドメインの所有権を確認する必要があります。Notification Hub から提供された値をメールドメインの DNS TXT レコードに登録します。提供された値が登録したドメインの TXT レコードと一致するかどうかで所有権を認証します。

1. **[+ ドメイン登録]** をクリックします。
2. 登録するルートドメインを入力し、**[検証]** をクリックします。
3. 検証に成功したら、**[登録]** をクリックして登録を完了します。
4. ドメイン一覧でドメイン所有認証ステータスの **[認証]** をクリックします。

ドメイン所有認証に成功すると、ドメイン認証ステータスが「完了」に変わります。

<a id="spf-authentication"></a>

#### SPF 認証

SPF（sender policy framework、送信者ポリシーフレームワーク）は、メール送信者と送信サーバーの信頼性を検証するためのメカニズムです。メール受信サーバーは、特定のドメインから送信されたメールが実際に許可されたメール送信サーバーから送られたものかどうかを確認します。メール受信サーバーは、送信者のメールドメイン DNS に登録された SPF レコードを確認し、登録されていない IP アドレスから送信されたメールをスパムとして処理します。

**SPF**
```
v=spf1 include:_spfblocka.toast.com ~all
```

1. 上記の **SPF** 項目の SPF レコードをドメインの TXT レコードに登録します。
2. 一覧からドメインを選択します。
3. **[SPF レコード認証ステータス]** 項目の **[ステータス確認]** をクリックして、SPF 認証を完了します。


!!! danger "注意事項"
    * ドメインの TXT レコードには、SPF レコードを 1 つだけ登録する必要があります。ドメインの TXT レコードに 2 つ以上の SPF レコードが登録されている場合、SPF 認証が失敗し、メール受信サーバーが受信を拒否する場合があります。
    * SPF レコードを検査する際に DNS 照会を発生させるメカニズム（include）と修飾子（redirect）の使用は最大 10 個に制限されており、これを超えるとメール受信サーバーで受信を拒否する場合があります。
    
SPF の詳細については、以下のドキュメントを参照してください。

* [メールセキュリティ強化機能の紹介（SPF）はこちら](https://meetup.nhncloud.com/posts/244)
* [RFC 4408 - 4.5 Selecting Records はこちら](https://datatracker.ietf.org/doc/html/rfc4408#section-4.5)
* [RFC 4408 - 10.1 Processing Limits はこちら](https://datatracker.ietf.org/doc/html/rfc4408#section-10.1)

<a id="dkim-authentication"></a>

#### DKIM 認証

DKIM（domainkeys identified mail、ドメインキー識別メール）は、メール送信サーバーがメールにデジタル署名を付与し、メール受信サーバーが送信者の正当性を確認することで、転送中にメッセージが偽造・改ざんされていないかを検証するメール認証方式です。DKIM を使用することで、スパム送信者やその他の悪意ある攻撃者によるメールの偽造・改ざんを防止できます。


1. ドメイン所有認証の完了後、一覧でドメインにチェックを入れ、**[DKIM 設定]** をクリックします。
2. DKIM 認証のために提供された DNS ホスト名に TXT レコードの値を設定し、下部の **[認証]** をクリックします。
    * 登録したドメインが `example.com` の場合、`toast._domainkey.example.com` の TXT レコードに値を設定する必要があります。
3. 認証が完了したら使用設定を行い、**[保存]** をクリックして DKIM 認証を完了します。

DKIM の詳細については、以下のドキュメントを参照してください。

* [メールセキュリティ強化機能の紹介 - ドメイン保護、DKIM、DMARC はこちら](https://meetup.nhncloud.com/posts/248)


<a id="dmarc-authentication"></a>

#### DMARC 認証

DMARC（domain-based message authentication reporting and conformance）は、メールセキュリティ強化の最終ステップです。メールスプーフィングを利用したフィッシング、詐欺などを防ぐためのドメインベースのメッセージ認証に関するレポートおよびコンプライアンスポリシーです。メール受信サーバーは、送信者アドレス（From）のドメインの DNS から DMARC レコードを照会します。DMARC レコードに定義されたポリシーに従い、受信サーバーは受信したメールを認証します。

**DMARC**
```
"v=DMARC1;p=none;sp=quarantine;pct=100;rua=mailto:${レポートを受信するメールアドレス}"
```

1. 上記の **DMARC** 項目の値に DMARC レポートを受信するメールアドレスを追加して、DMARC TXT レコードを完成させます。
2. `_dmarc.` が付加されたサブドメインの TXT レコードに登録します。
    * 例: ドメインが `example.com` の場合、`_dmarc.example.com` の TXT レコードに登録します。
3.  **[DMARC 認証ステータス]** 項目の **[ステータス確認]** をクリックして、DMARC 認証を完了します。

DMARC の詳細については、以下のドキュメントを参照してください。

* [メールセキュリティ強化機能の紹介 - ドメイン保護、DKIM、DMARC はこちら](https://meetup.nhncloud.com/posts/248)

##### ドメイン保護

ドメイン保護が有効になっているドメインは、他のプロジェクトで使用できません。保護されたドメインを他のプロジェクトで使用するには、同様にドメイン登録と所有権認証を取得する必要があります。

!!! danger "注意事項"
    ドメイン保護を無効にすると、他のプロジェクトからドメインが任意に使用される場合があります。すべての認証が完了したドメインの場合、他のプロジェクトから送信されるメールも同様にメール受信サーバーで正常に受信されます。このように送信されたメールがスパムまたはフィッシングである場合、受信者に被害が発生する可能性があり、ドメインの評判が低下してメール受信サーバーで受信を拒否される場合があります。

<span id="manage-sender-push-authorization"></span>

<a id="push-authentication-management"></a>

### Push 認証管理

Push 認証情報の発行方法については、**利用ポリシーおよび事前設定案内 > Push** を確認してください。

* [利用ポリシーおよび事前設定案内 > Push はこちら](../service-policy-and-precondition/push)

<a id="fcm-authentication-settings"></a>

#### FCM 認証設定
1. **[サービスアカウントキー登録]** を有効にします。
2. サービスアカウントキー（JSON）に、発行した FCM Service Account Credential ファイルの内容をコピーして貼り付けます。
3. **[検証]** > **[保存]** をクリックして設定を完了します。

<a id="pns-authentication-settings"></a>

#### APNS 認証設定
1. **[APNS JWT 証明書登録]** を有効にします。
2. **[チームID]** と **[キーID]** を入力します。
3. **[トピック]** を入力します。トピックはアプリのバンドル ID（Bundle ID）です。
4. **[秘密鍵]** ファイルの内容をコピーして貼り付けます。
5. **[検証]** > **[保存]** をクリックして設定を完了します。

<a id="adm-authentication-settings"></a>

#### ADM 認証設定
1. **[認証情報登録]** を有効にします。
2. **[クライアントID]** と **[クライアントキー]** を入力します。
3. **[検証]** > **[保存]** をクリックして設定を完了します。

<span id="manage-sender-profile"></span>

<a id="manage-outgoing-profiles"></a>

### 送信プロフィール管理

お知らせトーク、ブランドメッセージの送信には、送信プロフィールの作成および登録が必要です。

送信プロフィールの作成は Kakao ビジネスで行えます。

* [送信プロフィール作成ガイドはこちら](../service-policy-and-precondition/alimtalk-and-friendtalk)


Kakao ビジネスで送信プロフィールの作成が完了したら、次の手順で登録します。

1. **[+ 送信プロフィール登録]** をクリックし、送信プロフィール ID、管理者の携帯電話番号、カテゴリを設定してから **[トークンリクエスト]** をクリックします。
2. 管理者の携帯電話に送信されたトークンを入力し、**[確認]** > **[登録]** をクリックすると、送信プロフィールの登録が完了します。


<span id="manage-080-unsubscription-number"></span>

<a id="manage-opt-out-numbers"></a>

### 080 受信拒否番号管理

080 受信拒否番号は、広告メッセージ送信時に受信者が受信を拒否できるサービスです。広告性情報の送信時には、受信者が無料で受信拒否または受信同意の撤回ができるよう、無料受信拒否方法を必ず記載する必要があります。

<a id="apply-subscription"></a>

#### 加入申請

* **[+ 080 受信拒否番号申請]** をクリックし、会社名を入力します。入力した会社名は、080 受信拒否番号に電話をかけた際に案内される事業者名です。
* 加入申請が完了すると、登録予約ステータスに変わります。080 受信拒否サービスの開通には営業日基準で 3〜4 日かかり、開通が完了すると使用できます。
* 開通が完了すると、使用開始日時とステータスを確認できます。080 受信拒否サービスの登録予約・使用中ステータスでは、SMS 商品の利用終了はできません。解約後に商品の利用終了が可能です。解約するには、**[解約]** をクリックしてください。

<a id="set-080-unsubscription-number-when-advertising-texts"></a>

#### 広告性メッセージ送信時の 080 受信拒否番号設定

* 080 受信拒否番号が開通した状態でのみ、広告メッセージを送信できます。
* **[送信]** > **[SMS]** タブで送信目的を広告として選択すると、080 受信拒否番号の選択ウィンドウが表示されます。
* **[選択適用]** をクリックすると、広告性必須文言を追加できます。
* 広告性送信時、メッセージ本文に必ず広告性必須文言を含める必要があります。ルールは次のとおりです。
    * 開始文言: (광고)
    * 末尾文言: 무료수신 거부 {080受信拒否番号} または 무료거부 {080受信拒否番号}（当該文言には空白が含まれる場合があります。）

##### 例
```
(광고)

[무료 수신 거부]080XXXXXXX
```
```
(광고)

무료거부 080XXXXXXX
```
