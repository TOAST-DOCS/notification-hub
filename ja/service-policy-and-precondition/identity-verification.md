<!-- pre-align:aligned sig=75402ddddaf2 -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>本人認証</h1>

**Notification > Notification Hub > 利用ポリシー及び事前設定案内 > 本人認証**

<a id="identity-verification"></a>
## 本人認証方法 { #identity-verification }

* Notification Hub を使用するには、**[Notification Hub]** > **[本人確認]** で本人確認を行った後に利用できます。（電気通信事業法関連告示の遵守）
    * [電気通信事業法施行令第37条の7](https://www.law.go.kr/LSW//lsInfoP.do?lsId=004708&ancYnChk=0#0000)
* 事業者会員は本人確認を通じて Notification Hub を利用できます。個人会員は本人確認が制限されます。
* 本人確認は基本的に、携帯電話による本人確認と、事業者登録証および在職証明書の書類審査が必要です。
* 会員登録時に入力した氏名と携帯電話番号が、本人確認時に入力する情報と一致した場合に、本人確認が承認されます。
* 事業者会員が作成した組織/プロジェクトに招待された NHN Cloud アカウント、または事業者会員が作成した組織に招待された IAM アカウントは、サービスを利用するために本人確認を行う必要があります。
    * 招待された NHN Cloud アカウントおよび IAM アカウントは、本人確認が承認された際に、会員種別が事業者として分類されます。
* 在職証明書は、**発行日が記載され、職印が押印された書類**のみ有効です。在職証明書内の住民登録番号の後ろ 6 桁は**必ずマスキング（非表示）処理**してください。例：000000-0\*\*\*\*\*\*

<a id="identity-verification-status"></a>
### 本人認証状態 { #identity-verification-status }

| 状態    | 説明 |
|----------| --- |
| **審査中** | 登録した本人認証に対する認証書類を管理者が確認している状態 |
| **拒否**   | 本人認証が拒否され、書類の再登録が必要な状態 |
| **承認**   | 本人認証承認完了状態 |
