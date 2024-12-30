<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Push</h1>

**Notification > Notification Hub > Usage Policy and Preset Guide > Push**

To send push messages from Notification Hub, you need the Credentials issued by the push service.

The push services supported by Notification Hub are as follows.
* FCM(firebase cloud messaging): Android device 
* APNS(apple push notification service): iPhone
* ADM(amazon device messaging): Amazon Kindle, Fire etc.

## How to issue push Credentials

<span id="get-fcm-service-account-credential"></span>

### FCM Service Account Credential
**Service Account Credential** is required to send push notification messages to Android devices.
**Service Account** (Service Account) is a special type of account that is commonly used to communicate with Google Cloud for Application to Application (A2A).

#### Obtain FCM Service Account Credential JSON file
1. Access to [Google Firebase Console](https://console.firebase.google.com).
2. Create a new project by adding a project.
3. Move to the created project.
4. Click the gear icon next to the project overview at the top left of the page, and then click **Project Settings**.
5. Select **Service Account**.
6. In the Firebase Admin SDK entry, click **Create a new private key** to download the new **Service Account Credential** JSON file.

#### Register FCM Service Account Credential JSON file
1. Click **Notification > Push > certificates** on the console.
2. Open the downloaded JSON file and copy the content.
3. Paste the copy into the **FCM Service Account Credential** entry and click **Register**.

<span id="get-apns-jwt"></span>

### Obtain APNS JWT credentials
To send push notification messages to iOS devices, you need an encryption key and key ID (Key ID), Team ID (App ID Prefix), and Topic issued by the Apple Developer site.

#### Getting an APNS encryption key
1. From **Apple Developer Console** go to **Certificates, IDs & Profiles**.
2. Select **Keys**.
3. Select **Create a key**.
4. Enter the key name in **Register a New Key**, select **Apple Push Notification Service (APNs)** in **ENABLE** and continue to **Continue**.
5. Select **Register** after checking the contents.
6. Select **Download** to receive the encryption key file.

#### Obtain Key ID
1. From **Apple Developer Console** go to **Certificates, IDs & Profiles**.
2. Select the issued key.
3. You can find it in **View Key Details** item.

#### Obtain team ID
1. From **Apple Developer Console** go to **Certificates, IDs & Profiles**.
2. Select **Identifiers**.
3. You can find it in **Edit your App ID Configuration** section.

#### Topic
For authentication using JWT, Topic is required, and the topic is the Bundle ID of App.


* [Communicating with APNs using authentication tokens](https://developer.apple.com/kr/help/account/configure-app-capabilities/communicate-with-apns-using-authentication-tokens)


<span id="get-adm-credential"></span>

### ADM credentials

App's Client ID and Client Secret are required to send push notification messages to Kindle Fire app.

#### Register ADM Application and Profile (ClientId, Obtain Client Secret)
1. Access to [ADM Developer Console](https://developer.amazon.com/home.html).
2. Click **APP & SERVICS** at the top left of the page, and then click **Adda New App** at the bottom.
3. Once the app is created, click **Device Messaging** on the middle tab and click **Create a New Security Profile**.
4. After the profile is created, click **Security Profiles > View Security Profile** on the middle tab.
5. You can check the Client ID and Client Secret values on **General** tab.

#### Register ADM Kindle setting information (acquire API key)
1. Click **Security Profiles** tab, and then click **Android/KindleSetting** tab in the middle.
2. Enter the App Key Name, Package, MD5 Signature, and SHA256 Signature information.
3. You can query MD5 and SHA256 information with the following commands.
    ```
    > keytool -list -v -keystore {keystoreFileName} 
     
    Enter key storage password: 
    Key storage type: JKS 
    Key storage provider: SUN 
     
    Key storage contains 1 entry.
     
    Alias name: androidebugkey 
    Date Created: May 9, 2018 
    Item Type: PrivateKeyEntry 
    Certificate chain length: 1 
    Certificate [1]: 
    Owner: C=US, O=Android, CN=Android Debug 
    Publisher: C=US, O=Android, CN=Android Debug 
    Serial Number: 1 
    Suitable Start Date: Wed May 09 19:59:46 KST 2018; End Date: Fri May 01 19:59:46 KST 2048
    Certificate Fingerprint: 
             MD5:  xxxx 
             SHA1: xxxx 
             SHA256: xxxx 
    Signature Algorithm Name: SHA1withRSA 
    Subject Public Key Algorithm: 1024-bit RSA key 
    Version: 1
    ```
4. Click **Show** after you complete the registration to view the API key information.

