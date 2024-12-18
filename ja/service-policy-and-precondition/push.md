<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Push</h1>

**Notification > Notification Hub > 利用ポリシー及び事前設定案内 > Push**

Notification Hubでプッシュメッセージを送信するためには、プッシュサービスで発行する認証情報が必要です。

Notification Hubでサポートするプッシュサービスは次のとおりです。
* FCM(firebase cloud messaging): Android端末 
* APNS(apple push notification service): iPhone
* ADM(amazon device messaging): Amazon Kindle, Fireなど

## プッシュ認証情報の発行方法

<span id="get-fcm-service-account-credential"></span>

### FCM Service Account Credential
Android端末にプッシュ通知メッセージを送信するためには、**Service Account Credential**が必要です。
**Service Account**(サービスアカウント)は、一般的にGoogle CloudとA2A(Application to Application)通信時に使用する特別なタイプのアカウントです。

#### FCM Service Account Credential JSONファイルを取得
1. [Google Firebase Console](https://console.firebase.google.com)に接続します。
2. プロジェクトの追加で新しいプロジェクトを作成します。
3. 作成されたプロジェクトに移動します。
4. ページ右上プロジェクト概要の横にある歯車アイコンをクリックし、**プロジェクト設定**をクリックします。
5. **サービスアカウント**を選択します。
6. Firebase Admin SDK項目で**新しい秘密鍵の作成**をクリックして、新しい**Service Account Credential**JSONファイルをダウンロードします。

#### FCM Service Account Credential JSONファイル登録
1. コンソールで**Notification > Push > 証明書**をクリックします。
2. ダウンロードしたJSONファイルを開いて内容をコピーします。
3. コピーした内容を**FCM Service Account Credential** 項目に貼り付けて**登録**をクリックします。

<span id="get-apns-jwt"></span>

### APNS JWT認証情報を取得する
iOS端末にプッシュ通知メッセージを送信するためには、Apple Developerサイトで発行された暗号鍵とキーID(Key ID)、チームID(Team ID, App ID Prefix)、トピック(Topic)が必要です。

#### APNS暗号鍵を取得する
1. **Apple Developerコンソール**で**Certificates, IDs & Profiles**に移動します。
2. **Keys**を選択します。
3. **Create a key**を選択します。
4. **Register a New Key**でキー名を入力、 **ENABLE**項目で**Apple Push Notification service (APNs)**を選択し、**Continue**に進みます。
5. 内容を確認した後、**Register**を選択します。
6. **Download**を選択し、パスワードキーファイルを取得します。

#### キーIDを取得する
1. **Apple Developerコンソール**で**Certificates, IDs & Profiles**に移動します。
2. 発行されたキー(Key)を選択します。
3. **View Key Details**項目で確認できます。

#### チームIDを取得する
1. **Apple Developerコンソール**で**Certificates, IDs & Profiles**に移動します。
2. **Identifiers**を選択します。
3. **Edit your App ID Configuration** 項目で確認できます。

#### トピック
JWTを利用した認証のためにはトピック(Topic)が必要ですが、トピックはアプリのバンドルID(Bundle ID)です。


* [認証トークンを使用してAPNsとコミュニケーションする](https://developer.apple.com/kr/help/account/configure-app-capabilities/communicate-with-apns-using-authentication-tokens)


<span id="get-adm-credential"></span>

### ADM認証情報

Kindle Fireアプリにプッシュ通知メッセージを送信するためには、アプリのClient IDとClient Secretが必要です。

#### ADMアプリケーション及びプロファイルの登録(Client Id, Client Secret取得)
1. [ADM開発者コンソール](https://developer.amazon.com/home.html)に接続します。
2. ページ右上の**APP & SERVICES**をクリックした後、下部にある**Add a New App**をクリックします。
3. アプリが作成されたら、中央のタブにある**Device Messaging**をクリックし、**Create a New Security Profile**をクリックします。
4. プロフィール作成完了後、中央のタブにある**Security Profiles > View Security Profile**をクリックします。
5. **General**タブでClient IDとClient Secret値を確認できます。

#### ADM Kindle設定情報登録(API key取得)
1. **Security Profiles**タブをクリックした後、中央にある**Android/Kindle Setting**タブをクリックします。
2. App Key Name, Package, MD5 Signature, SHA256 Signature情報を入力します。
3. 下記のコマンドでMD5, SHA256情報を照会できます。
    ```
    > keytool -list -v -keystore {keystoreFileName}
    
 キーストアパスワード入力:
 キーストアタイプ: JKS
 キーストア提供者: SUN
    
 キーストアに1つの項目が含まれています。
    
 エイリアス名: androiddebugkey
 作成日: 2018. 5. 9
 項目タイプ: PrivateKeyEntry
 証明書チェーンの長さ: 1
 証明書[1]:
 所有者: C=US, O=Android, CN=Android Debug
 発行者: C=US, O=Android, CN=Android Debug
  シリアル番号: 1
  適切な開始日: Wed May 09 19:59:46 KST 2018終了日: Fri May 01 19:59:46 KST 2048
 証明書指紋:
             MD5:  xxxx
             SHA1: xxxx
             SHA256: xxxx
 署名アルゴリズム名: SHA1withRSA
 主体共用鍵アルゴリズム: 1024ビットRSAキー
 バージョン: 1
    ```
4. 登録完了後、**Show**をクリックするとAPI key情報を照会できます。
