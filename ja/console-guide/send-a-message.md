<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>送信</h1>

**Notification > Notification Hub > コンソール使用ガイド > 送信**

<span id="message"></span>

!!! danger "注意"
 送信前に、送信するメッセージチャンネルの送信情報が登録されている必要があります。送信情報の詳細については、 **Notification** > **Notification Hub** > **コンソール使用ガイド** > **はじめる** > **発信情報管理**をご確認ください。


<span id="send-flow-message"></span>

## フローメッセージ送信

フロー送信をするためには、登録されたフローが必要です。


1. フローを選択します。
2. 受信者を設定します。受信者設定方法は、直接入力、アドレス帳から選択、ファイルアップロードがあります。
    * 直接入力、アドレス帳から選択の場合、受信者設定時にテンプレート置換子を一緒に入力します。
    * ファイルアップロードの場合、受信者情報とテンプレート置換子をファイルに入力する必要があります。
    * 受信者設定については、以下で詳しく説明します。
3. 統計キーを設定します。
4. 送信時期を設定します。予約送信の場合、送信日時を設定します。
    * 予予約送信の場合は、送信時点から最大30日以内に設定できます。
5. **送信**をクリックしてメッセージを送信します。


## 個別メッセージチャンネル送信

1. テンプレートの有無を選択し、テンプレートを使用する場合は、テンプレートを選択します。
    * お知らせトーク、カカともへのメッセージは発信プロフィールを選択し、発信プロフィールに登録されたテンプレートを選択します。
2. 受信者を設定します。受信者の設定方法は、直接入力、アドレス帳から選択、ファイルアップロードがあります。
    * 直接入力、アドレス帳から選択の場合、受信者設定時にテンプレート置換者を一緒に入力します。
    * ファイルアップロードの場合、受信者情報とテンプレート置換子をファイルに入力する必要があります。
    * 受信者設定については、以下で詳しく説明します。
3. テンプレートを使用しない場合、メッセージのタイトルと内容を作成します。
    * メッセージチャンネル別のタイトル、内容の作成方法は以下で詳しく説明します。
4. 送信タイミングを設定します。予約送信の場合、送信日時を設定します。
    * 予約送信の場合は、送信時点から最大30日以内に設定できます。
5. **送信**をクリックしてメッセージを送信します。

### 受信者の設定方法

#### 受信者直接入力とアドレス帳から受信者選択

* フロー送信は、フローに設定されたメッセージチャネルの連絡先が全て入力されている場合にのみ送信が可能です。
* フロー送信で直接入力は、フローに設定されたメッセージチャネルの受信者の連絡先を全て入力します。
* フロー送信でアドレス帳から受信者選択は、フローに設定されたメッセージチャネルの受信者の連絡先が全て設定されている受信者のみを選択できます。
* 個別メッセージチャンネル送信の場合メッセージチャンネルに該当する連絡先を入力します。
* プッシュトークンはプッシュタイプと端末で作成されたトークンを入力します。

#### ファイルアップロード

* 受信者連絡先リストファイルのテンプレートをダウンロードします。
* 行は受信者を意味し、列は受信者の連絡先です。
* プッシュトークン列は、連絡先タイプとトークンで構成されたJSONオブジェクトです。受信者一人当たり6個まで入力が可能です。


受信者連絡先リストファイルのテンプレート構造は次のとおりです。

| contactPhoneNumber | contactEmailAddress | contactTokenJson1..6 | 
| - | - | - | 
| 受信者の携帯電話番号 | 受信者のメールアドレス | {"contactType": "連絡先_タイプ", "contact": "プッシュ_トークン" } |

### メッセージのタイトルと内容作成方法

#### SMS
* 発信番号、送信目的を選択します。送信目的が広告の場合、080受信拒否番号を選択します。
* 送信タイプを選択します。送信タイプはSMS(短文)、LMS(長文)、MMS(メディア長文)があります。
* SMS、LMS、MMSに共通して入力できる文字セットはEUC-KRです。
    * [ウィキペディアEUC-KR](https://ko.wikipedia.org/wiki/EUC-KR)
* SMSは最大90bytesで、ハングル45文字、英字90文字まで入力できます。
* LMSとMMSは最大2,000bytesで、ハングル1,000文字、英字2,000文字まで入力できます。
* MMSは画像を添付できます。
* 発信番号ブロックでメール送信に失敗した場合は、「番号盗用メールブロックサービス」をご確認ください。
    * [番号盗用メールブロックサービスガイドへ](./preconditions/preconditions-sms#fraud-number)
* 送信結果は成功だが、メールを受信できない場合は「サービスプロバイダースパムブロックサービス」をご確認ください。
    * [サービスプロバイダースパムブロックサービスガイドへ](./preconditions/preconditions-sms#spam-number)
* 認証用SMSメッセージの場合認証文言が必ず含まれている必要があります。
      * 認証文言: auth, password, verify、にんしょう、認証、パスワード、認証
      
##### MMS添付可能な画像規格

* MMS最大サイズ: 1000*1000以下のファイル
* MMSサポート規格: 1つにつき300KB以下、画像の数が3つの場合、合計800KB以下/ .jpg, .jpegファイル


#### 国際SMS
国際SMSはエンコードと文字数によって連結されたメッセージ(Concatenated Message)で送信されます。

* 連結メッセージとは、国際SMS送信で送信できる文字数制限を克服するために、国内LMSのように端末に1つの長い文字で繋がって見えるようにするサービスです。
 本文文字数、エンコード及び海海外通信会社のサポートの有無により、連結メッセージ機能が提供されるか、制限されます。
* 連結メッセージがサポートされていない場合、短文メッセージが複数件で端末に受信されることがあります。
* 連結メッセージが作成される過程で追加されるヘッダがメッセージ接続のためにメッセージ本文のスペース(約6 bytes)を占有し、入力可能な文字数が減少します。
* 料金は連結メッセージの数に応じて課金されます。

| エンコード | 1件課金 | 2件課金 | 3件課金 | 4件課金 | 5件課金 |
| --- | --- | --- | --- | --- | --- |
| UCS-2<br>(Unicode) | 70文字 | 134文字<br>(=67*2) | 201文字<br>(=67*3) | 268文字<br>(=67*4) | 335文字<br>(=67*5) |
| GSM-7bit | 160文字 | 306文字<br>(=153*2) | 459文字<br>(=153*3) | 612文字<br>(=153*4) | 765文字<br>(=153*5) |


#### RCS

1. 発信ブランドとチャットルーム(発信番号)を選択します。
2. 送信目的を選択します。広告の場合080受信拒否番号を選択します。
3. 送信タイプを選択します。RCS Biz Centerテンプレートを使用するには、テンプレートの使用有無を**使用**に選択する必要があります。そのほかの場合、MS、LMS、MMSのみ選択可能です。
    * SMSは最大ハングル/英字100文字まで入力でき、ボタン1つを設定できます。
    * 認証用SMSメッセージの場合、認証文言を必ず含める必要があります。
      * 認証文言: auth, password, verif、にんしょう、認証、パスワード、認証
    * 認証用SMSメッセージの場合ボタンを追加できません。
    * LMSスタンダード型はハングル、英字の区別なく本文タイトルを最大30文字、本文内容を最大1,300文字まで入力することができ、ボタンは最大3個まで設定できます。
    * LMSフォーマット型のうち、基本型、タイトル強調型の場合、メインタイトルは最大17文字、本文タイトルは最大30文字、本文内容は最大1,300文字まで入力することができ、ボタンは最大2個まで設定できます。    
    * LMSフォーマット型のうち、段落型の場合、メインタイトルは最大17文字、本文タイトルは最大30文字、本文内容は最大1,300文字まで入力することができ、本文内のボタンは最大2個まで設定できます。 
        * また、本文は最大3個まで追加することができ、全ての本文タイトルと本文内容を合わせて最大1,300文字まで入力できます。    
    * MMSはカードごとにハングル、英字の区別なく、タイトルを最大30文字、内容を最大1,300文字まで入力することができ、画像1つ、ボタンは最大2つまで設定できます。
        * MMSは詳細設定で横型、縦型、スライド型を選択できます。
        * スライド型を選択した場合、スライドを最小3個から最大6個まで追加できます。
    * RCS Biz Centerテンプレートでフリーテンプレートを選択した場合、最大90文字までメッセージ入力が可能です。
    * RCS Biz CenterテンプレートはRCS Biz Centerで事前登録が必要です。

##### RCSボタンタイプ
* チャットルームを開く
    * 設定した電話番号に設定したメッセージを送信します。
    * ボタン名を入力した後、メッセージを送信する電話番号を入力します。
    * 送信するメッセージ内容を入力します。
* コピーする
    * 設定した値がコピーされます。
    * ボタン名を入力した後、ボタンをクリックした時にコピーされる値を入力します。
* 電話をかける
    * 設定した電話番号に電話をかけます。
    * ボタン名を入力した後、ボタンをクリックしたときに電話する電話番号を入力します。
* マップを表示する/マップを検索する
    * 設定した位置をマップアプリで表示します。
    * ボタン名を入力した後位置の緯度、経度を入力します。
    * 位置名及びマップURLを入力します。(<span>https://</span>を含むURL)
* 現在位置共有
    * 受信者が発信者に受信者の現在位置をメッセージで送信します。
    * ボタン名を入力します。
* URL接続
    * Webリンクに接続されます。
    * ボタン名を入力後、ボタンをクリックしたときに接続するリンクを入力します。
    * リンク入力時、'http://', 'https://'を必ず入力する必要があります。
* スケジュール登録
    * 受信者のスケジュールアプリにスケジュールを登録します。
    * ボタン名を入力後、スケジュール開始日、終了日を選択します。
    * スケジュールタイトルとスケジュール内容を入力します。


#### お知らせトーク

* 発信プロフィールと発信プロフィールに登録されたテンプレートを選択します。
* お知らせトークはテンプレート送信のみ可能で、内容入力は必要ありません。

#### カカともへのメッセージ
1. 送信する内容に広告性情報(特価、割引、イベント、プロモーション広報など)がある場合、送信目的を「広告」に設定します。
2. メッセージタイプを選択します。タイプ別の詳細ガイドは[カカともへのメッセージ送信サポートタイプ](./preconditions/preconditions-ktb#ktb-supported-types)でご確認ください。
    * 基本型(テキスト/画像/ワイド画像)
        * テキスト:全角/半角の区別なく、空白を含めて1,000文字テキスト+リンクボタン最大5(縦配置)
        * 画像:全角/半角の区別なく、空白を含めて400文字テキスト+画像1枚+リンクボタン最大5(縦配置)
        * ワイド画像:全角/半角の区別なく、空白を含めて76文字テキスト+画像1枚+リンクボタン1個
    * ワイドアイテムリスト
        * 1つのタイトルに3～4個のリスト(画像+アイテム)を追加できる広告タイプの商品です。
        * 全角/半角の区別なく、空白を含めてテキスト最初のアイテムタイトル25文字、 2～4番目のアイテムタイトル30文字+画像アイテム3～4個+リンクボタン最大2個(横並び)
    * カルーセルフィード
        * 最大10個の画像と様々なテキスト情報を入れることができる広告タイプの商品です。
        * 全角/半角の区別なく、空白を含めて「タイトル」20文字テキスト+「文言」180文字テキスト+「画像+リンクボタン2個(横並び)」で構成されたアイテム最大10個
    * プレミアム動画
        * 添付した動画が吹き出しに自動的に再生されるタイプです。
        * 動画リンクはカカオTVにアップロードされた映像のみ使用可能です(例： https://tv.kakao.com/v/#{数字} / https://tv.kakao.com/channel/#{数字}/cliplink/#{数字})。
        *全角/半角の区別なく、空白を含めて「ヘッダ」20文字テキスト+「文言」76文字テキスト+「カカオTVにアップロードされた映像」1個+リンクボタン1個
    * コマース
        * 商品の価格や割引情報を強調して表示できる吹き出しです。
        * 全角/半角の区別なく、空白を含めて「タイトル」 20文字テキスト+「付加情報」34文字テキスト+リンクボタン最大2個(横並び)
    * カルーセルコマース
        * 様々な商品の情報をカタログ形式で構成できる吹き出しです。
        * 全角/半角の区別なく、空白を含めて「タイトル」 30文字テキスト+「付加情報」34文字テキスト+リンクボタン最大2個(横並び)で構成されたアイテム最大10個
        * カルーセルコマースに使用される全ての画像は同じ比率でなければなりません。
3. 画像がある場合、画像を選択します。
    * メッセージに画像を添付するには、まず**詳細設定 > 添付ファイル管理**タブで画像を登録する必要があります。
    * 画像リンク:画像をクリックしたときに接続されるリンクを入力します(http://, https://を含むURL)。
    * カルーセルコマースに使用される全ての画像は同じ比率でなければなりません。
4. Webリンク、アプリリンク、 Botキーワード、メッセージ伝達、相談トーク切り替え、Bot切り替え、ビジネスフォームボタンを挿入できます。
    * 基本型最大5個、カルーセル/ワイドアイテムリスト最大2個
5. メッセージでクーポンを強調する必要がある場合、ボタンを使用してそのボタンをクリックすると、添付したクーポンに移動するようにできます。

#### メール

1. 送信目的を選択します。
    * 送信目的を広告に選択した場合、追加入力が必要です。
        * タイトルの先頭に「(広告)」文言が必要です。
        * 本文に送信者の名称、メールアドレス、電話番号及びアドレスを表示する必要があります。
        * 受信拒否リンクがハングル/英語の形で必ず入っていなければならず、受信を拒否することができる技術的な措置をしなければなりません。
        * 受信拒否とすして登録されたユーザーには、広告性メールは送信されません。
        * 送信目的を広告に選択すると、通知ポップアップが表示され、受信拒否案内文言を設定します。
2. 発信アドレスを入力します。名前形式で作成すると、送信者名とメールアドレスを入力できます。
    * "発信者名<発信メール>"の形式で送信すると、メールを受信する人に送信者名とメールアドレスの形式で表示されます。
3. 添付ファイルは直接アップロードするか、登録されたファイルを選択して添付します。
    * 添付ファイルは最大10個までアップロード可能で、30MB以下のファイルのみ可能です。
    * 添付ファイルの合計は30MBを超えることはできません。
    * 最大30MBまで添付可能ですが、受信するメールシステム(gmail.com, naver.comなど)の添付ファイル制限ポリシーにより`制限超過`で拒否されたり、スパム判定率が高くなる可能性があるため、10MB以内で添付することを推奨します。


##### 広告メール送信時の注意事項

情報通信網法に基づき、商業性広告メールや企業広報メールを送信する場合、以下の事項を遵守する必要があります。([韓国インターネット振興院関連内容確認](https://spam.kisa.or.kr/spam/cm/cntnts/cntntsView.do?mi=1061&cntntsId=1086)) <br>


1. 広告性メールは、明示的に受信同意をした受信者にのみ送信しなければなりません。これに違反して紛争が発生した場合、責任は広告メール送信者にあります。
2. タイトルが始まる部分に「(広告)」文言が必須です。
3. 本文に送信者の名称、メールアドレス、電話番号及び住所を含む送信者情報を表示しなければなりません。
4. 本文に受信者が受信拒否または受信同意を撤回する意思を容易に表示できるようにするための案内文を明明示する必要があります。
5. 受信者が本文内に[受信拒否]などを押して受信拒否または受信同意の撤回を簡単に選択できるように技術的な措置をしなければならず、この場合、その案内文と技術的な措置はハングルと英字で明示する必要があります。

```
メール受信を希望しない場合は[受信拒否]をクリックしてください。
If you do not want to receive it, please click a [Unsubscription].
```

NHN Cloudは、情報通信網法を遵守できるように、「広告メール」に対して以下のような技術的措置を講じています。

- タイトルに(広告)文言を挿入します。
- 受信者が受信拒否を選択できるようにハングルと英語の形で受信拒否機能を提供します。
- 受信拒否対象メールアドレスには広告メールを送信しません。

##### 受信拒否リンクで提供しているキー

| キー | 文言 | 使用例 |
|-------------------------| - |-------------------------------------------------------------------------------------------------------------------------------|
| BLOCK_RECEIVER_LINK | [受信拒否](#) | メールの受信を希望しない場合は ##BLOCK_RECEIVER_LINK##をクリックしてください。 |
| EN_BLOCK_RECEIVER_LINK | [Unsubscription](#) | If you no longer wish to receive these emails, please click the ##EN_BLOCK_RECEIVER_LINK##. |
| JA_BLOCK_RECEIVER_LINK | [受信拒否](#) | メールの受信を希望しない場合、##JA_BLOCK_RECEIVER_LINK##をクリックしてください。 |
| BLOCK_RECEIVER_LINK_URL | - | If you no longer wish to receive these emails, please `<a href='##BLOCK_RECEIVER_LINK_URL##' target='_blank'>click here</a>`. |


### Push

1. 送信目的を選択します。
2. 送信目的を広告に選択した場合、追加入力が必要です。
    * 送信連絡先に代表番号を入力します。
    * 受信同意撤回ガイドにはアプリからプッシュメッセージの受信を拒否する方法を入力します。
        * 例：受信拒否:設定 > 通知設定
3. 入力タイプを選択します。入力タイプをJSONに選択した場合、全ての内容をJSON形式に合わせて入力する必要があります。
4. HTMLスタイルを使用するかどうかを選択します。
    * HTMLスタイルを使用すると、Android端末にHTMLを表現できます。
    * iPhone(iOS)はHTMLスタイルをサポートしません。
    * HTMLスタイルを使用してメッセージを送信する場合、AndroidとiPhoneのメッセージを別々に作成して送信する必要があります。
5. プッシュメッセージにボタン、画像などを入れて様々な形で送信できます。
    * 端末で受信したプッシュメッセージのボタン、画像を正常に表示するためには、アプリにSDKを適用する必要があります。
        * [Android SDK](https://docs.nhncloud.com/ko/nhncloud/ko/nhncloud-sdk/push-android/)
        * [iOS SDK](https://docs.nhncloud.com/ko/nhncloud/ko/nhncloud-sdk/push-ios/)


#### ボタン

|名前| 内容                                                            |
|---|------------------------------------------------------------------|
| 名前 | ボタンの名前                                                        |
| タイプ | ボタンのタイプ、レスポンス(REPLY)、アプリを開く(OPEN_APP)、URLを開く(OPEN_URL)、閉じる(DISMISS) |
| 送信ボタン名 | ボタンタイプがレスポンスボタンの場合、iOSで送信ボタン名を設定できます。                       |
| リンク | ボタンを押したときに移動または実行するリンクです。ボタンタイプが「URLを開く」の場合、該当します。                |
| ヒント | ボタンの説明です。                                                    |

#### ボタンのタイプ
- レスポンス
    - ダイレクト返信機能を実行します。
    - ユーザーが送信ボタンをタッチすると、アクションリスナーにユーザーが入力したテキストが伝達されます。
- アプリを開く
    - アプリが実行されます。
    - アクションリスナーを通じてメッセージの全文が伝達されます。メッセージ内に情報を入力して特定のページに移動するなどの機能を実装できます。
- URLを開く
    - リンク項目に入力されたURL(https://...)またはScheme(scheme://...)を実行します。
    - URLを入力すると、Webブラウザが実行され、そのURLを読み込みます。
    - スキーム(Scheme)を入力すると、アプリにあらかじめ定義しておいたスキームを実行します。
- 閉じる
    - 該当通知を閉じます。

#### メディア

|名前| 内容                                             |
|---|---------------------------------------------------|
| 位置 | メディアがある場所、'REMOTE'または'LOCAL'                   |
| アドレス | メディアがあるアドレス、 URL、URIなど。                |
| タイプ | 画像、GIF、動画、音声を選択できます。 (Androidは画像のみ可能) |
| 拡張子 | メディアの拡張子                                       | .png, .aviなどメディアの拡張子です。 |
| 展開 | メディア展開機能、 Androidのみ可能です。                      |

#### メディアファイル指定
- 外部
    - 入力したURLに該当するメディアファイルをダウンロードして使用します。
    - Android
        - Android Pie以上でHTTPを使用するには <a href="http://docs.toast.com/ko/TOAST/ko/toast-sdk/push-android/#android-p">network-security-config</a>を設定する必要があります。
    - iOS
        - iOS 9以上でHTTPを使用するにはInfo.plistファイル内にATS(app transport security)を設定する必要があります。
        - 実際のメディアファイルの拡張子情報をextension項目に入力する必要があります。 (例：jpg, png, mp4, wav, ...)
- 内部
    - アプリ内に含まれているリソースを使用します。
    - Android
        - ファイルは'res > drawable'にあらかじめ追加する必要があります。
        - リソース識別子でアクセスするため、メッセージ作成時に'richMessage.media.source'に拡張子を除いたファイル名を入力します。
        - Androidではファイル名がリソースの識別子として使用されるため、拡張子が違っても同じファイル名を使用することはできません。
       サポートする画像フォーマットはpng, jpg, gifです。 (現在ビデオ、オーディオ形式のメディアはサポートしません。)
    - iOS
        - リソースはリッチメッセージを作成する <a href="http://docs.toast.com/ko/TOAST/ko/toast-sdk/push-ios/#notification-service-extension">Notification Service Extension</a> プロジェクトにあらかじめ追加する必要があります。
        - Xcodeでファイルまたはディレクトリを'NotificationServiceExtension'プロジェクトに追加します。
        - 'Build Phases > TARGETS'でファイルが正常に追加されたか確認します。
        - バンドルリソースでアクセスするため、拡張子を含めた完全なファイル名が必要です。
        - メッセージ作成時'richMessage.media.source'に追加したファイル名を入力します。

#### メディアタイプ
- 画像

| | Android | iOS |
| - | - | - |
| サポート形式 | JPEG, PNG, GIF | JPEG, PNG, GIF |
| GIFアニメーション | サポートしない | サポートする |
| ファイルサイズ | 制限なし | 10MB |
| 推奨事項 | 2:1比率の横画像推奨<br>Small: 512x256<br>Medium: 1024x512<br>Large: 2048x1024 | 横画像推奨<br>最大サイズ: 1038x1038 |

- 動画

| | Android | iOS |
| - | - | - |
| サポート形式 | サポートしない | MPEG, MPEG3Video, MPEG4, AVIMovie |
| ファイルサイズ | サポートしない | 50MB |

- 音声

| | Android | iOS |
| - | - | - |
| サポート形式 | サポートしない | WaveAudio, MP3, MPEG4Audio |
| ファイルサイズ | サポートしない | 5MB |

#### 大きなアイコン
Androidのみ提供する機能です。通知に大きなアイコンを指定します。ファイルの指定方法は、メディアファイルの指定方法と同じです。

|名前| 内容                              |
|---|------------------------------------|
| 位置 | 位置する場所、'REMOTE'または'LOCAL'         |
| アドレス | 画像が位置するアドレス、 URL, URIなど。 |

#### グループ
Androidのみ提供する機能です。通知にグループを設定し、グループキーが同じ通知はまとめて表現します。

|名前| 内容     |
|---|-----------|
| キー | グループのキー   |
| 説明 | グループの説明 |

#### 通知音
| | Android | iOS |
| - | - | - |
| サポート形式 | MP3, PCM/WAVE, Vorbis | Linear PCM, MP4(IMA/ADPCM), μ-law, aLaw |
| 拡張子 | .mp3, .wav, .ogg | .aiff, .wav, .caf |
| プレイ時間 | 制限なし | 30秒 |

- アプリ内に含まれているリソースのみ指定可能です。 (外部URL使用不可)
- Android
    - リソースは'res > raw'フォルダにあらかじめ追加する必要があります。
    - リソース識別子でアクセスするため、ファイル拡張子は無視されます。
    - Android Oreo未満でのみ動作します。
- iOS
    - リソースはアプリプロジェクトのバンドルリソースとしてあらかじめ追加する必要があります。
    - バンドルリソースでアクセスするため、拡張子を含めた完全なファイル名が必要です。
