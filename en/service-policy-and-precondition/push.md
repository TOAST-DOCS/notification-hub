<style>
.gnb_inner {
    position: fixed !important;
}
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>이용 정책 및 사전 설정 안내 - Push</h1>

**Notification > Notification Hub > 이용 정책 및 사전 설정 안내 > Push**

Notification Hub에서 푸시 메시지를 발송하기 위해서는 푸시 서비스에서 발급하는 인증 정보가 필요합니다.

Notification Hub에서 지원하는 푸시 서비스는 다음과 같습니다.
* FCM(firebase cloud messaging): Android 기기 
* APNS(apple push notification service): iPhone
* ADM(amazon device messaging): Amazon Kindle, Fire 등

## 푸시 인증 정보 발급 방법

<span id="get-fcm-service-account-credential"></span>

### FCM Service Account Credential
Android 기기에 푸시 알림 메시지를 전송하기 위해서는 **Service Account Credential**이 필요합니다.
**Service Account**(서비스 계정)는 일반적으로 Google Cloud와  A2A(Application to Application) 통신 시 사용하는 특별한 유형의 계정입니다.

#### FCM Service Account Credential JSON 파일 얻기
1. [Google Firebase Console](https://console.firebase.google.com)에 접속합니다.
2. 프로젝트 추가를 통해 새로운 프로젝트를 생성합니다.
3. 생성된 프로젝트로 이동합니다.
4. 페이지 왼쪽 상단 프로젝트 개요 옆 톱니바퀴 아이콘을 클릭한 뒤 **프로젝트 설정**을 클릭합니다.
5. **서비스 계정**을 선택합니다.
6. Firebase Admin SDK 항목에서 **새 비공개 키 생성**을 클릭해 새로운 **Service Account Credential** JSON 파일을 다운로드합니다.

#### FCM Service Account Credential JSON 파일 등록
1. 콘솔에서 **Notification > Push > 인증서**를 클릭합니다.
2. 다운로드 받은 JSON 파일을 열어 내용을 복사합니다.
3. 복사한 내용을 **FCM Service Account Credential** 항목에 붙여 넣고 **등록**을 클릭합니다.

<span id="get-apns-jwt"></span>

### APNS JWT 인증 정보 얻기
iOS 기기에 푸시 알림 메시지를 전송하기 위해서는 Apple Developer 사이트에서 발급 받은 암호 키와 키 ID(Key ID), 팀 ID(Team ID, App ID Prefix), 토픽(Topic)이 필요합니다.

#### APNS 암호 키 얻기
1. **Apple Developer 콘솔**에서 **Certificates, IDs & Profiles**로 이동합니다.
2. **Keys**를 선택합니다.
3. **Create a key**를 선택합니다.
4. **Register a New Key**에서 키 이름 입력, **ENABLE** 항목에서 **Apple Push Notification service (APNs)** 선택 후 **Continue**로 계속 진행합니다.
5. 내용 확인 후 **Register**를 선택합니다.
6. **Download**를 선택해 암호 키 파일을 받습니다.

#### 키 ID 얻기
1. **Apple Developer 콘솔**에서 **Certificates, IDs & Profiles**로 이동합니다.
2. 발급 받은 키(Key)를 선택합니다.
3. **View Key Details** 항목에서 확인할 수 있습니다.

#### 팀 ID 얻기
1. **Apple Developer 콘솔**에서 **Certificates, IDs & Profiles**로 이동합니다.
2. **Identifiers**를 선택합니다.
3. **Edit your App ID Configuration** 항목에서 확인할 수 있습니다.

#### 토픽
JWT를 이용한 인증을 위해서는 토픽(Topic)이 필요한데, 토픽은 앱의 번들 아이디(Bundle ID)입니다.


* [인증 토큰을 사용하여 APNs와 커뮤니케이션하기](https://developer.apple.com/kr/help/account/configure-app-capabilities/communicate-with-apns-using-authentication-tokens)


<span id="get-adm-credential"></span>

### ADM 자격 증명

Kindle Fire 앱에 푸시 알림 메시지를 전송하기 위해서는 앱의 Client ID와 Client Secret이 필요합니다.

#### ADM 애플리케이션 및 프로파일 등록(Client Id, Client Secret 획득)
1. [ADM 개발자 콘솔](https://developer.amazon.com/home.html)에 접속합니다.
2. 페이지 왼쪽 상단에서 **APP & SERVICES**를 클릭한 후, 하단에 **Add a New App**을 클릭합니다.
3. 앱이 생성되면 중간 탭에 있는 **Device Messaging**을 클릭하고 **Create a New Security Profile**을 클릭합니다.
4. 프로필 생성 완료 후 중간 탭에 있는 **Security Profiles > View Security Profile**을 클릭합니다.
5. **General** 탭에서 Client ID와 Client Secret 값을 확인할 수 있습니다.

#### ADM Kindle 설정 정보 등록(API key 획득)
1. **Security Profiles** 탭을 클릭한 후 중간에 있는 **Android/Kindle Setting** 탭을 클릭합니다.
2. App Key Name, Package, MD5 Signature, SHA256 Signature 정보를 입력합니다.
3. 아래와 같은 명령어로 MD5, SHA256 정보를 조회할 수 있습니다.
    ```
    > keytool -list -v -keystore {keystoreFileName}
    
    키 저장소 비밀번호 입력:
    키 저장소 유형: JKS
    키 저장소 제공자: SUN
    
    키 저장소에 1개의 항목이 포함되어 있습니다.
    
    별칭 이름: androiddebugkey
    생성 날짜: 2018. 5. 9
    항목 유형: PrivateKeyEntry
    인증서 체인 길이: 1
    인증서[1]:
    소유자: C=US, O=Android, CN=Android Debug
    발행자: C=US, O=Android, CN=Android Debug
    일련 번호: 1
    적합한 시작 날짜: Wed May 09 19:59:46 KST 2018 종료 날짜: Fri May 01 19:59:46 KST 2048
    인증서 지문:
             MD5:  xxxx
             SHA1: xxxx
             SHA256: xxxx
    서명 알고리즘 이름: SHA1withRSA
    주체 공용 키 알고리즘: 1024비트 RSA 키
    버전: 1
    ```
4. 등록 완료 후 **Show**를 클릭하면 API key 정보를 조회할 수 있습니다.

