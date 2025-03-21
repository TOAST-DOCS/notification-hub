<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>テンプレート</h1>

**Notification > Notification Hub > コンソール使用ガイド > テンプレート**


<span id="template"></span>

## テンプレート

よく使うメッセージや一定の形式を要求するメッセージをテンプレートとして保存しておき、送信時に保存しておいたテンプレートを設定してメッセージを送信できます。例えば、カスタマーサポート、お知らせ、通知、またはマーケティングメッセージなど、よく使うメッセージの形式をテンプレートにしておけば、毎回同じ内容を作成する必要がなく、一部の情報だけを修正して送信できます。

### カテゴリー
* まず、ルートカテゴリーを選択し、**+カテゴリーを追加**をクリックしてカテゴリーを作成します。
* カテゴリーは選択されたカテゴリーの下に作成されます。

### テンプレート
1. テンプレートが属するカテゴリーを選択し、**+テンプレート登録**をクリックします。テンプレート作成ページに移動し、選択されたメッセージチャンネルの追加設定が表示されます。
2. タイトルと内容及び各メッセージチャンネルで必要な設定を行い、**登録**をクリックします。

#### お知らせトークテンプレート

お知らせトークテンプレートは、登録申請後、カカオの検収承認を受けなければ使用できません。

* 登録可能なメッセージタイプには、チャンネル追加型、基本型、付加情報型、複合型があります。
* 登録可能な強調タイプには、強調表示型、画像型、アイテムリスト型があります。
* 希望のタイプを選択してテンプレートを作成してください。

* カカオお知らせトークガイド
    * [[お知らせトーク制作ガイド]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/content-guide), [[お知らせトーク審査ガイド]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit), [[お知らせトークホワイトリスト]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit/white-list), [[お知らせトークブラックリスト]](https://kakaobusiness.gitbook.io/main/ad/bizmessage/notice-friend/audit/black-list)
* 発信プロフィール/グループ
    * テンプレートを登録する発信プロフィールまたは発信プロフィールグループを選択します。グループに登録する場合、グループに含まれる全ての発信プロフィールが該当テンプレートを使用できます。
    * 発信プロフィール/グループに同じテンプレートコードが存在する場合、発信プロフィールに登録されたテンプレートが優先的に送信されます。
    * 発信プロフィールグループの場合、メッセージタイプのうち「チャンネル追加型」、「複合型」ではテンプレートを登録できません。
* テンプレートコード/テンプレート名
    * 1つの発信プロフィール/グループに同じテンプレートコードとテンプレート名を重複して登録することはできません。
* テンプレート内容
    * お知らせトークは、全角/半角の区別なく変数及びURL、空白、ボタン名を含めて1,000文字まで作成可能です。変数を入力して登録する場合、置換される内容も考慮してテンプレートを作成してください。<br/> 文字数の詳細ガイドは[お知らせトークテンプレートの注意事項](https://docs.nhncloud.com/ko/Notification/KakaoTalk%20Bizmessage/ko/alimtalk-overview/#_3)でご確認ください。
    * 変数を #{変数}の形で作成します。 (例：#{ホン・ギルドン}さんの荷物が本日(#{09:50})お届け予定です。)
    * ボタン登録時、ボタン名には変数入力はできませんが、ボタンURLには変数入力が可能です。 (例 http://kakao.com/#{変数})
    * ボタンurl登録時、url_mobile, url_pcリンクには'http://', 'https://''が含まれている必要があり、scheme_ios, scheme_androidリンクはスキーム形態に合わせて登録する必要があります。そうでない場合、テンプレート登録はできません。
* セキュリティテンプレート
    * テンプレートセキュリティの場合、モバイル以外のデバイスでメッセージ内容が表示されません。(「モバイルでご確認ください」文言表示)
    * 一般メッセージの場合、検収時に設定値が変更されることがあり、OTP、認証番号、パスワード、信用情報/等級変更案内テンプレートは必ずセキュリティをチェックしてください。

#### お知らせトークテンプレートボタン
* テンプレートごとに最大5つのボタンを登録できます。
* クイック接続
    * 配送照会及びプラグインタイプを使用できませんが、その他のタイプはボタンと同じように使用できます。
    * 1つのテンプレートに最大10個まで使用することができ、クイック接続を使用する場合、ボタンの数は2個に制限されます。

| ボタン種類 | 説明 |
| --- | --- |
| 配送照会 | - 宅配会社の配送照会ページに移動します。<br/> - 配送照会ボタンをサポートする宅配会社、宅配会社別の伝票番号パターンを確認します。 [[お知らせトーク配送照会伝票番号パターン案内]](https://www.nhncloud.com/kr/support/notice/detail/1455)|
| Webリンク | - モバイルまたはPC Webページに移動します。<br/> - URLリンクを変数として設定できます。 |
| アプリリンク | - カスタムスキームでアプリを実行します。<br/> - AndroidとiOSで実行するカスタムスキームをそれぞれ設定する必要があります。 |
| Botキーワード | - ボタン名が担当者に伝達されます。<br/> - 相談トークをサポートしないチャンネルが該当ボタンを追加すると、お知らせトークの送信ができません。 |
| メッセージ伝達 | - ボタン名、メッセージ本文が担当者に伝達されます。<br/> - 相談トークをサポートしないチャンネルが該当ボタンを追加すると、お知らせトークの送信ができません。 |
| 相談トーク切り替え | - 相談トークに接続されます。<br/> - 相談トークをサポートしないチャンネルが該当ボタンを追加すると、お知らせトークの送信ができません。 |
| Bot切り替え | - チャットボットが呼び出されます。<br/> - 相談トークをサポートしないチャンネルが該当ボタンを追加すると、お知らせトークの送信ができません。 |
| チャンネル追加 | - お知らせトークを送信したチャンネルを追加します。表示位置は最初のボタンとしてのみ使用可能です。<br/> - すでにチャンネルが追加されている場合、受信者に表示されません。 |
| 画像セキュリティ送信プラグイン | - チャットウィンドウ内で機密情報を含む画像を暗号化して送信します。<br/> - ビズプラグイン作成が必要です。 [[ビズプラグインガイド]](https://business.kakao.com/info/talkbizplugin/) |
| 個人情報利用プラグイン | - チャットウィンドウ内で会員登録なしでサービス提供に必要な個人情報収集同意を受けます。<br/> - ビズプラグインの作成が必要です。 [[ビズプラグインガイド]](https://business.kakao.com/info/talkbizplugin/) |
| ワンクリック決済プラグイン | - チャットウィンドウ内で画面遷移なしでユーザーが商品を決済できます。<br/> - 決決済プラグインは、プラットフォームで直接登録をサポートしていないため、[カカオお客様センター](https://cs.kakao.com/helps?service=127&category=572&locale=ko)にお問い合わせください。 | 
| ビジネスフォーム | - ビジネスフォームを作成して現在チャンネルと接続した場合、ボタンをクリックすると、設定したビジネスフォームが呼び出されます。<br/> - ビジネスフォームの作成が必要です。 [[ビジネスフォームガイド]](https://business.kakao.com/info/talkbizform/) |

#### テンプレート検収
通知トークテンプレートの検収及び審査はカカオが直接行い、検収要請後、2営業日以内に順次処理されます。

* テンプレートお問い合わせ登録
    * 検収要請前にカカオ検収担当者に伝えたい意見がある場合、お問い合わせ登録欄に内容を入力します。要請/承認状態のテンプレートは問い合わせができません(**検収中/拒否**状態のテンプレートのみ問い合わせ登録が可能です)。
    * 登録した問い合わせは検収結果に追加され、カカオの検収担当者が確認します。
    * 検収結果にテンプレートの用途に関する問い合わせ、拒否理由の内容が追加されます。
    * テンプレートが拒否された場合、**問い合わせ登録**及び**修正**をクリックして再検収できます。

#### テンプレート状態
* テンプレート登録時、**リクエスト > 検収中 > 承認/拒否**状態の順に更新されます。
* テンプレート登録後、1年間同じ状態が維持されるか、追加送信がない場合、**休眠**状態に切り替わります。関連ガイドは[お知らせトークテンプレート注意事項](https://docs.nhncloud.com/ko/Notification/KakaoTalk%20Bizmessage/ko/alimtalk-overview/#_3)でご確認ください。

#### テンプレート修正
* **承認/拒否**状態のテンプレートのみ修正できます。
* 承認されたテンプレートを修正した後、検収が完了すると、既存のテンプレートの内容が修正した内容に置き換えられます。
* 発信プロフィール/グループ及びテンプレートコードは修正できません。
* 修正したテンプレートは**検収中**状態から再度検収が行われます。

#### テンプレート削除
* 要請/拒否状態のテンプレートのみ削除できます。
* 拒否されたテンプレートは**削除**後、再登録できます。
* 削除されたテンプレートコードは再使用できます。
