<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>RCS</h1> 

**Notification > Notification Hub > 利用ポリシー及び事前設定案内 > RCS**

## ブランド作成及び登録

RCS Bizmessageサービスを利用するためには、RCS Biz Centerに登録後、ブランドを登録する必要があります。 [[RCS Biz Center]](https://www.rcsbizcenter.com/main)

### ブランド作成
1. RCS Biz Centerで**会員登録** > **企業担当者会員登録**をクリックして会員登録後、承認を受けます。
    * 会員登録の際、事業者登録証のコピーが必要です。
    * RCS担当者が承認し、会員登録処理まで2営業日程度かかります。
2. RCSブランドは企業プロフィールです。ブランドを開設した後、承認をリクエストします。
    * **ブランド開設ガイド**をクリックすると、関連ガイドを参照できます。
      * [ブランド開設ガイド](https://www.rcsbizcenter.com/GuideBrand)
    * RCS担当者が承認し、ブランド作成承認まで2営業日程度かかります。

### ブランド代理店設定
RCSブランド承認完了後、代理店を「엔이치엔클라우드」に設定します。

1. RCS Biz Centerで**企業ダッシュボード > ブランドダッシュボード > ブランド運営管理**に移動します。

2. **代理店権限追加**をクリックした後、代理店名から「엔이치엔클라우드」を検索して選択します。

### チャットルーム(発信番号)登録
メッセージアプリのチャットルームでメッセージを受信・確認できます。チャットルーム単位でメッセージを送信・確認できます。

1. **企業ダッシュボード > ブランドダッシュボード > チャットルーム登録**に移動して、発信番号でチャットルームを登録します。
    * **チャットルーム登録ガイド**で関連ガイドを参照できます。
      * [RCS Biz Center - チャットルーム登録ガイド](https://www.rcsbizcenter.com/Chatbot#section01)
    * 最近1か月以内に発行された通信サービス利用証明書が必要です。
    * RCS企業メッセージは010番号をサポートしません。
    * RCS担当者が承承認し、チャットルームの承認まで2営業日程度かかります。

2. チャットルーム登録が完了(承認)したら、**Notification Hub** > **発信情報** > **ブランド管理**タブでブランド連動が可能です。

### テンプレート登録
テンプレートは、ブランド別にメッセージの内容やスタイルをあらかじめ登録しておいて使用できるRCS企業メッセージです。
テンプレートメッセージを送信するには、RCS Biz Centerでテンプレートを登録する必要があります。 (RCS SMS/LMS/MMSメッセージで送信する場合には別途のテンプレートを登録する必要はありません)

1. **企業ダッシュボード > ブランドダッシュボード > テンプレート登録**に移動して、テンプレートを登録します。
    * **テンプレートガイド**をクリックして関連ガイドを参考できます。
      * [RCS Biz Center - テンプレートガイド](https://www.rcsbizcenter.com/RcsMessageType#section04)
    * テキスト/画像テンプレートのみ登録が可能です。下記の**サポートする送信タイプ**項目を参照してください。
    * RCS担当者が承認し、チャットルーム承認まで2営業日程度かかります。

2. テンプレート登録が完了(承認)したら、**Notification** > **RCS Bizmessage** > **RCS Bizmessage管理** > **ブランド管理**タブでNHN Cloudコンソールに連動が可能です。

### Notification Hubコンソールでブランド連動
ブランド作成及び代理店設定、チャットルーム(発信番号)登録、テンプレート登録が完了(承認)したら、コンソールでブランドを連動します。

**Notification Hub** > **発信情報** > **ブランド管理** タブで連動が可能です。連動後に変更がある場合には**+ブランド連動**ボタンを押すと同期が行われます。

## サポートする送信タイプ

<table class="custom-table" style="text-align: center">
    <tr>
        <td>NO</td>
        <td>商品</td>
        <td>商品名</td>
        <td>カードタイプ</td>
        <td>カード数</td>
        <td>メッセージ最大長さ</td>
        <td>カード別最大ボタン数</td>
        <td>ボタン名の最大長さ</td>
        <td>画像</td>
    </tr>
    <tr>
        <td>1</td>
        <td>SMS</td>
        <td>SMS</td>
        <td>Standalone</td>
        <td>1枚</td>
        <td>100文字</td>
        <td>1個</td>
        <td>17文字</td>
        <td>-</td>
    </tr>
    <tr>
        <td>2</td>
        <td rowspan="4">LMS</td>
        <td>LMS</td>
        <td>Standalone</td>
        <td>1枚</td>
        <td>1300文字</td>
        <td>3個</td>
        <td>17文字</td>
        <td>-</td>
    </tr>
    <tr>
        <td>3</td>
        <td>基本型</td>
        <td>Format</td>
        <td>1枚</td>
        <td>1300文字</td>
        <td>2個</td>
        <td>17文字</td>
    </tr>
    <tr>
        <td>4</td>
        <td>タイトル強調型</td>
        <td>Format</td>
        <td>1枚</td>
        <td>1300文字</td>
        <td>2個</td>
        <td>17文字</td>
    </tr>
    <tr>
        <td>5</td>
        <td>段落型</td>
        <td>Format</td>
        <td>1枚</td>
        <td>1300文字</td>
        <td>段落別2個</td>
        <td>7文字</td>
    </tr>
    <tr>
        <td>6</td>
        <td rowspan="4">MMS</td>
        <td>縦型(Tall)</td>
        <td>Standalone Media Top</td>
        <td>1枚</td>
        <td>1300文字</td>
        <td>2個</td>
        <td>17文字</td>
        <td>Tall(568x528)</td>
    </tr>
    <tr>
        <td>7</td>
        <td>縦型(Medium)</td>
        <td>Standalone Media Top</td>
        <td>1枚</td>
        <td>1300文字</td>
        <td>2個</td>
        <td>17文字</td>
        <td>Medium(568x336)</td>
    </tr>
    <tr>
        <td>8</td>
        <td>スライド型(Medium)</td>
        <td>Carousel Medium</td>
        <td>2枚 <br/> ～ 6枚</td>
        <td>1300文字</td>
        <td>2個</td>
        <td>13文字</td>
        <td>Medium(696x504)</td>
    </tr>
    <tr>
        <td>9</td>
        <td>スライド型(Small)</td>
        <td>Carousel Small</td>
        <td>2枚 <br/> ～ 6枚</td>
        <td>1300文字</td>
        <td>2個</td>
        <td>5文字</td>
        <td>Short(360x336)</td>
    </tr>
    <tr>
        <td>10</td>
        <td rowspan="5">テキスト<br/>テンプレート</td>
        <td>記述テンプレート_タイトル選択型</td>
        <td>Description</td>
        <td>1枚</td>
        <td>90文字</td>
        <td>2個</td>
        <td>17文字</td>
        <td rowspan="5">-</td>
    </tr>
    <tr>
        <td>11</td>
        <td>記述テンプレート_タイトル自由形</td>
        <td>Description</td>
        <td>1枚</td>
        <td>90文字</td>
        <td>2個</td>
        <td>16文字</td>
    </tr>
    <tr>
        <td>12</td>
        <td>スタイルテンプレート_タイトル選択型</td>
        <td>Cell</td>
        <td>1枚</td>
        <td>90文字</td>
        <td>2個</td>
        <td>17文字</td>
    </tr>
    <tr>
        <td>13</td>
        <td>スタイルテンプレート_タイトル自由形</td>
        <td>Cell</td>
        <td>1枚</td>
        <td>90文字</td>
        <td>2個</td>
        <td>16文字</td>
    </tr>
    <tr>
        <td>14</td>
        <td>基本テンプレート_タイトル自由形</td>
        <td>Free</td>
        <td>1枚</td>
        <td>90文字</td>
        <td>-</td>
        <td>-</td>
    </tr>
    <tr>
        <td>15</td>
        <td rowspan="8">画像<br/>テンプレート</td>
        <td>画像&タイトル強調型(3:4)</td>
        <td>Highlighted Image n Title</td>
        <td>1枚</td>
        <td>500文字</td>
        <td>2個</td>
        <td>16文字</td>
        <td>Long(900x1200)</td>
    </tr>
    <tr>
        <td>16</td>
        <td>画像&タイトル強調型(1:1)</td>
        <td>Highlighted Image n Title</td>
        <td>1枚</td>
        <td>500文字</td>
        <td>2個</td>
        <td>16文字</td>
        <td>Square(900x900)</td>
    </tr>
    <tr>
        <td>17</td>
        <td>画像強調型(3:4)</td>
        <td>Highlighted Image</td>
        <td>1枚</td>
        <td>500文字</td>
        <td>2個</td>
        <td>16文字</td>
        <td>Long(900x1200)</td>
    </tr>
    <tr>
        <td>18</td>
        <td>画像強調型(1:1)</td>
        <td>Highlighted Image</td>
        <td>1枚</td>
        <td>500文字</td>
        <td>2個</td>
        <td>16文字</td>
        <td>Square(900x900)</td>
    </tr>
    <tr>
        <td>19</td>
        <td>サムネイル型(縦)</td>
        <td>Thumbnail</td>
        <td>1枚</td>
        <td>500文字</td>
        <td>2個</td>
        <td>16文字</td>
        <td>Vertical(900x560)</td>
    </tr>
    <tr>
        <td>20</td>
        <td>サムネイル型(横)</td>
        <td>Thumbnail</td>
        <td>1枚</td>
        <td>500文字</td>
        <td>2個</td>
        <td>16文字</td>
        <td>Horizontal(900x560)</td>
    </tr>
    <tr>
        <td>21</td>
        <td>SNS型</td>
        <td>SNS</td>
        <td>1枚</td>
        <td>500文字</td>
        <td>2個</td>
        <td>16文字</td>
        <td>Square(900x900)</td>
    </tr>
    <tr>
        <td>22</td>
        <td>SNS型(中央ボタン)</td>
        <td>SNS</td>
        <td>1枚</td>
        <td>500文字</td>
        <td>2個</td>
        <td>16文字</td>
        <td>Rectangle(900x560)</td>
    </tr>
    <tr>
        <td>23</td>
        <td rowspan="6">LMS<br/>テンプレート</td>
        <td>明細書A型</td>
        <td>Description</td>
        <td>1枚</td>
        <td>1300文字</td>
        <td>2個</td>
        <td>17文字</td>
        <td rowspan="6">-</td>
    </tr>
    <tr>
        <td>24</td>
        <td>明細書B型</td>
        <td>Description</td>
        <td>1枚</td>
        <td>1300文字</td>
        <td>2個</td>
        <td>17文字</td>
    </tr>
    <tr>
        <td>25</td>
        <td>明細書C型</td>
        <td>Description</td>
        <td>1枚</td>
        <td>1300文字</td>
        <td>2個</td>
        <td>17文字</td>
    </tr>
    <tr>
        <td>26</td>
        <td>基本型</td>
        <td>Description</td>
        <td>1枚</td>
        <td>1300文字</td>
        <td>2個</td>
        <td>17文字</td>
    </tr>
    <tr>
        <td>27</td>
        <td>タイトル強調型</td>
        <td>Description</td>
        <td>1枚</td>
        <td>1300文字</td>
        <td>2個</td>
        <td>17文字</td>
    </tr>
    <tr>
        <td>28</td>
        <td>段落型</td>
        <td>Description</td>
        <td>1枚</td>
        <td>1300文字</td>
        <td>段落別2個</td>
        <td>7文字</td>
    </tr>
</table>
