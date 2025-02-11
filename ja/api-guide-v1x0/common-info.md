<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Notification Hub API v1.0共通情報</h1>

**Notification > Notification Hub > API v1.0使用ガイド > 共通情報**

<span id="notification-hub-api-common-information"></span>

!!! danger 「注意事項」
    * Notification Hub v1.0 APIは現在アルファ(alpha)状態であり、安定しておらず、実験的な機能が追加または削除される可能性があります。
    * APIはサービス改善のためにいつでも変更される可能性があり、変更された場合、事前告知なしに変更されることがあります。
    * Notification HubがGA(General Availability)状態に移行後、公式バージョンに変更されます。
    * 変更可能な部分は、この文書で説明するAPIエンドポイント、認証、リクエスト制限、リクエスト、レスポンス、フィールドなどの全ての項目が含まれます。

<span id="api-endpoint"></span>

## APIエンドポイント

| リージョン   | エンドポイント |
|--------| ----- |
| Global | https://notification-hub.api.nhncloudservice.com |

* Notification Hubはリージョン区分なくGlobalエンドポイントを使用します。

<span id="authentication-and-permissions"></span>

## 認証及び権限

```
X-NHN-Authorization: Bearer {accessToken}
```

* 認証トークンを発行し、Notification Hub APIを呼び出す際、**X-NHN-Authorization** リクエストヘッダに認証トークンを設定します。

### 認証トークン発行例

#### IntelliJ HTTP

```http
POST https://oauth.api.nhncloudservice.com/oauth2/token/create
Content-Type: application/x-www-form-urlencoded
Authorization: Basic {{oauthAuthorization}}
```

#### cURL

```curl
curl -X POST "https://oauth.api.gov-nhncloudservice.com/oauth2/token/create" \
     -H "Content-Type: application/x-www-form-urlencoded" \
     -H "Authorization: Basic {{oauthAuthorization}}"
```

* **oauthAuthorization**は**User Access Key ID**と **Secret Access Key**を **USER_ACCESS_KEY_ID:SECRET_ACCESS_KEY**としてBase64エンコードした値です。
* **User Access Key ID**と**Secret Access Key**はログイン後、**右上のメールアドレス** > **APIセキュリティ設定**で作成・管理できます。
* 認証トークン発行の詳細については、**ユーザーガイド** > **NHN Cloud** > **Public API** > **API認証** > **認証トークン**の項目をご確認ください。

<span id="date-time-format"></span>

## 日付と時間形式

* 日付と時間は **ISO 8601拡張形式**を使用します。
    * [ISO 8601 - 日付と時間表記法](https://ko.wikipedia.org/wiki/ISO_8601)
* 使用可能な**ISO 8601**形式は次のとおりです。
    * YYYY-MM-DDThh:mm+hh:mm
    * YYYY-MM-DDThh:mmZ
    * YYYY-MM-DDThh:mm:ss+hh:mm
    * YYYY-MM-DDThh:mm:ssZ
    * YYYY-MM-DDThh:mm:ss.sss+hh:mm
    * YYYY-MM-DDThh:mm:ss.sssZ
* **T**は日付と時間を区分するセパレータです。
* **+hh:mm** または **Z**は標準タイムゾーン指定子(Time Zone Designator)を表します。
* Notification Hub API及び機能では、秒とミリ秒単位は使用されません。
* APIレスポンスで日付と時間は **YYYY-MM-DDThh:mm:ss.sss+09:000**形式で表記します。

## プレフィックス及び単一文字ワイルドカード検索

リスト照会では個人情報以外の照会条件に対して、プレフィックス及び単一文字ワイルドカード検索がサポートされます。

### プレフィックス(Prefix)検索

* **プレフィックス検索**は特定文字列で始まる値を検索します。
* リクエスト例
    * テンプレート名が`広告_`で始まるテンプレートを検索します。
      ```
      GET /message/v1.0/templates?templateName=広告
      ``` 
    * 検索結果:広告-1、広告-2、広告-3など
### 単一文字ワイルドカード(Single Character Wildcard)検索
* **単一文字ワイルドカード検索**は特定位置にどんな文字でも関係なく検索します。
* リクエスト例
    * テンプレート名が`-1`で終わるテンプレートを検索します。
      ```
      GET /message/v1.0/templates?templateName=__-1
      ``` 
    * 検索結果:広告-1、一般-1、告知-1など
    
<span id="response"></span>

## レスポンス共通情報

<span id="succeed-response"></span>

### 失敗レスポンス本文

成功レスポンスのHTTPステータスコードは**200 OK**です。

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

### 失敗レスポンス本文

失敗レスポンスのHTTPステータスコードは**4xx**と **5xx**です。

```json
{
    "header": {
        "isSuccessful": false,
        "resultCode": 400629,
        "resultMessage": "失敗に関する情報が含まれています。"
    }
}
```

| 名前 | タイプ | 説明 |
| --- | --- | --- |
| header.isSuccessful | Boolean | API呼び出し成否です。 |
| header.resultCode | Integer | 結果コードです。成功は0、失敗は400000以上の値を持ちます。 |
| header.resultMessage | String | 結果メッセージです。失敗に関する情報が含まれています。 |

* **resultCode**前3桁はHTTPステータスコードと同じで、後3桁は詳細コードです。
* 結果メッセージはいつでも変更できます。結果メッセージをビジネスロジックに使用することは推奨しません。
* 結果メッセージは**Accept-Language** リクエストヘッダに基づいて韓国語、英語、日本語で提供されます。
* API呼び出し時、**X-NC-ALWAYS-200-OK** リクエストヘッダに値を**true**に設定すると、失敗レスポンスにもHTTPステータスコード **200 OK**でレスポンスします。

<span id="rate-limit"></span>

## リクエスト数制限
* Notification Hubでは、特定のクライアントによる過度のリソース占有を防ぎ、サービスの安定性を確保するため、APIリクエスト数を制限しています。
* APIリクエスト数は1秒あたりのリクエスト数。300RPS(Requests Per Second)に制限されます。

!!! danger 「注意事項」
    * リクエスト数の計算は、クライアント、サーバー間の時間差、ネットワーク遅延によって異なる測定を行い、計算された値が異なる場合があります。
    * 300RPSを超えると、サーバーはHTTPステータスコード429(Too Many Requests)レスポンスでクライアントのリクエストを拒否します。
    * リクエストが拒否された場合、クライアントが即時再試行すると、サーバーのリクエスト拒否が長い時間維持されることがあります。
    * クライアントは、リクエストが拒否されたら、指数バックオフ(Exponential Backoff)のように再試行間隔を増やして呼び出すことを推奨します。

<span id="example-api-calls"></span>

## 呼び出し例

Notification Hub API使用ガイドでは、**IntelliJ HTTP**、**cURL**でのAPI呼び出し例を提供します。

### IntelliJ HTTP
* IntelliJ HTTPはIntelliJ IDEAのHTTPクライアントプラグインで、JetBrains IDEsまたはコマンドラインから実行できます。
    * [JetBrains - IntelliJ HTTP Client](https://www.jetbrains.com/help/idea/http-client-in-product-code-editor.html)
        * IntelliJ HTTP Clientの使い方、文法についてのガイド文書です。
    * [JetBrains Marketplace - IntelliJ HTP Client](https://plugins.jetbrains.com/plugin/13121-http-client)
        * IntelliJ HTTP Clientプラグインリンクです。
    * [JetBrains - IntelliJ HTTP Cient CLI](https://blog.jetbrains.com/idea/2022/12/http-client-cli-run-requests-and-tests-on-ci/)
        * IntelliJがない環境でIntelliJ HTTP(*.http)ファイルを実行させるCLIの紹介記事です。
    * [Docker - IntelliJ HTTP Client Image](https://hub.docker.com/r/jetbrains/intellij-http-client)
        * IntelliJ HTTP Clientドッカーイメージリンクです。
    * [JetBrains - Define environment variables](https://www.jetbrains.com/help/idea/http-client-in-product-code-editor.html#environment-variables)
        * IntelliJ HTTP Client環境変数設定方法についてのガイド文書です。
      

**IntelliJ HTTP環境変数設定ファイル例(htt-client.env.json)**

```json
{
   "default": {
     "endpoint": "https://notification-hub.api.nhncloudservice.com",
     "appKey": "アプリキー",
     "accessToken": "認証トークン"
   }
}
```

### cURL

* cURLはコマンドラインで実行できるコマンドラインツールで、様々なプロトコルをサポートします。
    * [cURL](https://curl.se/)
        * cURL公式Webサイトです。
    * [cURL - Wikipedia](https://ko.wikipedia.org/wiki/CURL)
        * cURLにういてのWikipedia文書です。

**cURL環境変数設定例**

```
ENDPOINT=https://notification-hub.api.nhncloudservice.com
APP_KEY=アプリキー
ACCESS_TOKEN=認証トークン
```
