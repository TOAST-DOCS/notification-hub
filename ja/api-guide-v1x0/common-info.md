<style>
.gnb_inner {
    position: fixed !important;
}
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Notification Hub API 공통 정보</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > Notification Hub API 공통 정보**

<span id="notification-hub-api-common-information"></span>

## Notification Hub API 공통 정보

!!! danger "주의 사항"
    * Notification Hub v1.0 API는 현재 알파(alpha) 상태로, 안정화되지 않았으며, 실험적인 기능이 추가되거나 제거될 수 있습니다. 
    * API는 언제든지 변경될 수 있으며, 변경 시 사전 공지 없이 변경될 수 있습니다.
    * Notification Hub가 GA(General Availability) 상태로 전환 후 공식 버전으로 변경됩니다.
    * 변경 가능한 부분은 이 문서에서 설명하는 API 엔드포인트, 인증, 요청 제한, 요청, 응답, 필드 등 모든 항목이 포함됩니다.

<span id="api-endpoint"></span>

### API 엔드포인트

| 리전     | 엔드포인트 |
|--------| ----- |
| Global | https://notification-hub.api.nhncloudservice.com |

* Notification Hub는 리전 구분 없이 Global 엔드포인트를 사용합니다.

<span id="authentication-and-permissions"></span>

### 인증 및 권한

```
X-NHN-Authorization: {accessToken}
```

* 인증 토큰을 발급 받아 Notification Hub API 호출 시 **X-NHN-Authorization** 요청 헤더에 인증 토큰을 설정합니다.

#### 인증 토큰 발급 예시

##### IntelliJ HTTP

```http
POST https://oauth.api.gov-nhncloudservice.com/oauth2/token/create
Content-Type: application/x-www-form-urlencoded
Authorization: Basic {{oauthAuthorization}}
```

##### cURL

```curl
curl -X POST "https://oauth.api.gov-nhncloudservice.com/oauth2/token/create" \
     -H "Content-Type: application/x-www-form-urlencoded" \
     -H "Authorization: Basic {{oauthAuthorization}}"
```

* **oauthAuthorization**은 **User Access Key ID**와 **Secret Access Key**를 **USER_ACCESS_KEY_ID:SECRET_ACCESS_KEY**로 합쳐 Base64 인코딩한 값입니다.
* **User Access Key ID**와 **Secret Access Key**는 로그인 후 **오른쪽 상단의 메일 주소** > **API 보안 설정**에서 생성 및 관리할 수 있습니다.
* 인증 토큰 발급에 대한 자세한 내용은 **사용자 가이드** > **NHN Cloud** > **Public API** > **API 인증** > **인증 토큰** 항목을 확인 부탁드립니다.

<span id="date-time-format"></span>

### 날짜와 시간 형식

* 날짜와 시간은 **ISO 8601 확장 형식**을 사용합니다.
    * [ISO 8601 - 날짜와 시간 표기법](https://ko.wikipedia.org/wiki/ISO_8601)
* 사용 가능한 **ISO 8601** 형식은 다음과 같습니다.
    * YYYY-MM-DDThh:mm+hh:mm
    * YYYY-MM-DDThh:mmZ
    * YYYY-MM-DDThh:mm:ss+hh:mm
    * YYYY-MM-DDThh:mm:ssZ
    * YYYY-MM-DDThh:mm:ss.sss+hh:mm
    * YYYY-MM-DDThh:mm:ss.sssZ
* **T**는 날짜와 시간을 구분하는 구분자입니다.
* **+hh:mm** 또는 **Z**는 표준 시간대 지정자(Time Zone Designator) 를 나타냅니다.
* Notification Hub API 및 기능에서 초와 밀리초 단위는 사용되지 않습니다.
* API 응답에서 날짜와 시간은 **YYYY-MM-DDThh:mm:ss.sss+09:000** 형식으로 표기합니다.

<span id="response"></span>

### 응답 공통 정보

<span id="succeed-response"></span>

#### 실패 응답 본문

성공 응답의 HTTP 상태 코드는 **200 OK**입니다.

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    }
}
```

<span id="failed-response"></span>

#### 실패 응답 본문

실패 응답의 HTTP 상태 코드는 **4xx**와 **5xx**입니다.

```json
{
    "header": {
        "isSuccessful": false,
        "resultCode": 400629,
        "resultMessage": "실패에 대한 정보를 담고 있습니다."
    }
}
```

| 이름 | 타입 | 설명 |
| --- | --- | --- |
| header.isSuccessful | Boolean | API 호출 성공 여부입니다. |
| header.resultCode | Integer | 결과 코드입니다. 성공은 0, 실패는 400000 이상의 값을 가집니다. |
| header.resultMessage | String | 결과 메시지입니다. 실패에 대한 정보를 담고 있습니다. |

* **resultCode** 앞자리 3자리는 HTTP 상태 코드와 동일하며, 뒷자리 3자리는 상세 코드입니다.
* 결과 메시지는 언제든지 변경될 수 있습니다. 결과 메시지를 비즈니스 로직에 사용하는 것은 권장하지 않습니다.
* 결과 메시지는 **Accept-Language** 요청 헤더에 따라 한국어, 영어, 일본어로 제공됩니다..
* API 호출 시 **X-NC-ALWAYS-200-OK** 요청 헤더에 값을 **true**로 설정하면, 실패 응답에도 HTTP 상태 코드 **200 OK**로 응답합니다.

<span id="rate-limit"></span>

### 요청 수 제한
* Notification Hub에서는 특정 클라이언트가 과도한 리소스 점유를 막고 서비스의 안정성을 보장하기 위해 API 요청 수를 제한합니다.
* API 요청 수는 초당 요청 수. 300RPS(Requests Per Second)으로 제한됩니다.

!!! danger "주의 사항"
    * 요청 수 계산은 클라이언트, 서버간 시간 차이, 네트워크 지연에 따라 다르게 측정되어 계산된 값이 다를 수 있습니다.
    * 300RPS가 넘으면 서버는 HTTP 상태 코드 429(Too Many Requests) 응답으로 클라이언트의 요청을 거부합니다.
    * 요청이 거부되었을 때 클라이언트가 즉시 재시도하면 서버의 요청 거부가 오랜 시간 동안 유지될 수 있습니다.
    * 클라이언트는 요청이 거부되면 지수 백오프(Exponential Backoff) 처럼 재시도 간격을 늘려가며 호출하는 것을 권장합니다.

<span id="example-api-calls"></span>

### API 호출 예시

Notification Hub API 사용 가이드에서는 **IntelliJ HTTP**, **cURL**로 API 호출 예시를 제공합니다.

#### IntelliJ HTTP
* 본 API 가이드 문서에서 API를 호출하는 예시를 IntelliJ HTTP, cURL로 제공합니다.
* IntelliJ HTTP는 IntelliJ IDEA의 HTTP 클라이언트 플러그인으로 JetBrains IDEs 또는 명령줄에서 실행할 수 있습니다.
    * [JetBrains - IntelliJ HTTP Client](https://www.jetbrains.com/help/idea/http-client-in-product-code-editor.html)
        * IntelliJ HTTP Client 사용 방법, 문법에 대한 가이드 문서입니다.
    * [JetBrains Marketplace - IntelliJ HTP Client](https://plugins.jetbrains.com/plugin/13121-http-client)
        * IntelliJ HTTP Client 플러그인 링크입니다.
    * [JetBrains - IntelliJ HTTP Cient CLI](https://blog.jetbrains.com/idea/2022/12/http-client-cli-run-requests-and-tests-on-ci/)
        * IntelliJ가 없는 환경에서 IntelliJ HTTP(*.http) 파일을 실행시키는 CLI에 대한 소개 문서입니다.
    * [Docker - IntelliJ HTTP Client Image](https://hub.docker.com/r/jetbrains/intellij-http-client)
        * IntelliJ HTTP Client 도커 이미지 링크입니다.
    * [JetBrains - Define environment variables](https://www.jetbrains.com/help/idea/http-client-in-product-code-editor.html#environment-variables)
        * IntelliJ HTTP Client 환경 변수 설정 방법에 대한 가이드 문서입니다.
        * 다음 Notification Hub API 호출 예시에서 사용하는 기본적인 환경 변수입니다.
          ```json
          {
            "default": {
              "endpoint": "https://notification-hub.api.nhncloudservice.com",
              "appKey": "앱키",
              "accessToken": "인증 토큰"
            }
          }
          ```

#### cURL

* cURL은 명령줄에서 실행할 수 있는 커맨드 라인 도구로, 다양한 프로토콜을 지원합니다.
    * [cURL](https://curl.se/)
        * cURL 공식 홈페이지입니다.
    * [cURL - Wikipedia](https://ko.wikipedia.org/wiki/CURL)
        * cURL에 대한 Wikipedia 문서입니다.
* 다음 Notification Hub API 호출 예시에서 사용하는 기본적인 환경 변수입니다.
```
ENDPOINT=https://notification-hub.api.nhncloudservice.com
APP_KEY=앱키
ACCESS_TOKEN=인증 토큰
```
