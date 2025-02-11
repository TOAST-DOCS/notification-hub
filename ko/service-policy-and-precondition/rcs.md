<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>RCS</h1> 

**Notification > Notification Hub > 이용 정책 및 사전 설정 안내 > RCS**

## 브랜드 생성 및 등록

RCS Bizmessage 서비스를 이용하기 위해서는 RCS Biz Center 가입 후 브랜드를 등록해야 합니다. [[RCS Biz Center 바로 가기]](https://www.rcsbizcenter.com/main)

### 브랜드 생성
1. RCS Biz Center에서 **회원가입** > **기업 담당자 회원가입**을 클릭해 회원 가입 후 승인을 받습니다.
    * 회원가입 시 사업자등록증 사본이 필요합니다.
    * RCS 담당자가 승인하며 회원가입 처리까지 2 영업일 정도 소요됩니다.
2. RCS 브랜드는 기업 프로필입니다. 브랜드를 개설한 뒤 승인을 요청합니다.
    * **브랜드 개설 가이드**를 클릭해 관련 가이드를 참고할 수 있습니다.
        * [브랜드 개설 가이드 바로 가기](https://www.rcsbizcenter.com/GuideBrand)
    * RCS 담당자가 승인하며 브랜드 생성 승인까지 2 영업일 정도 소요됩니다.

### 브랜드 대행사 설정
RCS 브랜드 승인 완료 후, 대행사를 ‘㈜ NHN Cloud’로 설정합니다.

1. RCS Biz Center에서 **기업 대시보드 > 브랜드 대시보드 > 브랜드 운영 관리**로 이동합니다.

2. **대행사 권한 추가**를 클릭한 뒤 대행사명에서 '㈜ NHN Cloud'를 검색해 선택합니다.

### 대화방(발신 번호) 등록
메시지 앱의 대화방에서 메시지를 받고 확인할 수 있습니다. 대화방 단위로 메시지를 보내고, 확인할 수 있습니다.

1. **기업 대시보드 > 브랜드 대시보드 > 대화방 등록**으로 이동하여, 발신 번호로 대화방을 등록합니다.
    * **대화방 등록 가이드**에서 관련 가이드를 참고할 수 있습니다.
      * [RCS Biz Center - 대화방 등록 가이드 바로 가기](https://www.rcsbizcenter.com/Chatbot#section01)
    * 최근 1개월 이내 발행된 통신서비스 이용증명원이 필요합니다.
    * RCS 기업 메시지는 010 번호를 지원하지 않습니다.
    * RCS 담당자가 승인하며 대화방 승인까지 2 영업일 정도 소요됩니다.

2. 대화방 등록이 완료(승인)되었다면, **Notification Hub** > **발신 정보** > **브랜드 관리** 탭에서 브랜드 연동이 가능합니다.

### 템플릿 등록
템플릿은 브랜드별로 메시지의 내용 및 스타일을 미리 등록해 두고 사용할 수 있는 RCS 기업 메시지입니다.
템플릿 메시지를 발송하려면 RCS Biz Center에서 템플릿을 등록해야 합니다. (RCS SMS/LMS/MMS 메시지로 발송하는 경우에는 별도의 템플릿을 등록하지 않아도 됩니다.)

1. **기업 대시보드 > 브랜드 대시보드 > 템플릿 등록**으로 이동하여, 템플릿을 등록합니다.
    * **템플릿 가이드**를 클릭해 관련 가이드를 참고할 수 있습니다.
      * [RCS Biz Center - 템플릿 가이드 바로 가기](https://www.rcsbizcenter.com/RcsMessageType#section04)
    * 텍스트/이미지 템플릿 한해서 등록이 가능합니다. 아래 **지원하는 발송 유형** 항목을 참고하세요.
    * RCS 담당자가 승인하며 대화방 승인까지 2 영업일 정도 소요됩니다.

2. 템플릿 등록이 완료(승인)되었다면, **Notification** > **RCS Bizmessage** > **RCS Bizmessage 관리** > **브랜드 관리** 탭에서 NHN Cloud 콘솔에 연동이 가능합니다.

### Notification Hub 콘솔에서 브랜드 연동
브랜드 생성 및 대행사 설정, 대화방(발신 번호) 등록, 템플릿 등록이 완료(승인)되었으면 콘솔에서 브랜드를 연동합니다.

**Notification Hub** > **발신 정보** > **브랜드 관리** 탭에서 연동이 가능합니다. 연동 후에 변경 사항이 있는 경우에는 **+ 브랜드 연동** 버튼을 누르면 동기화가 진행됩니다.

## 지원하는 발송 유형

<table class="custom-table" style="text-align: center">
    <tr>
        <td>NO</td>
        <td>상품</td>
        <td>상품명</td>
        <td>카드 타입</td>
        <td>카드 수</td>
        <td>메시지 최대 길이</td>
        <td>카드별</td>
        <td>버튼</td>
        <td>이미지</td>
    </tr>
    <tr>
        <td>1</td>
        <td>SMS</td>
        <td>SMS</td>
        <td>Standalone</td>
        <td>1</td>
        <td>100</td>
        <td>1</td>
        <td>17</td>
        <td>-</td>
    </tr>
    <tr>
        <td>2</td>
        <td>LMS</td>
        <td>LMS</td>
        <td>Standalone</td>
        <td>1</td>
        <td>1300</td>
        <td>3</td>
        <td>17</td>
        <td>-</td>
    </tr>
    <tr>
        <td>3</td>
        <td rowspan="2">MMS</td>
        <td>세로형(Tall)</td>
        <td>Standalone Media Top</td>
        <td>1</td>
        <td>1300</td>
        <td>2</td>
        <td>17</td>
        <td>Tall(568x528)</td>
    </tr>
    <tr>
        <td>4</td>
        <td>세로형(Medium)</td>
        <td>Standalone Media Top</td>
        <td>1</td>
        <td>1300</td>
        <td>2</td>
        <td>17</td>
        <td>Medium(568x336)</td>
    </tr>
    <tr>
        <td>5</td>
        <td rowspan="5">텍스트<br/>템플릿</td>
        <td>서술 템플릿_타이틀 선택형</td>
        <td>Description</td>
        <td>1</td>
        <td>90자</td>
        <td>2</td>
        <td>17</td>
        <td rowspan="5">-</td>
    </tr>
    <tr>
        <td>6</td>
        <td>서술 템플릿_타이틀 자유형</td>
        <td>Description</td>
        <td>1</td>
        <td>90자</td>
        <td>2</td>
        <td>16</td>
    </tr>
    <tr>
        <td>7</td>
        <td>스타일 템플릿_타이틀 선택형</td>
        <td>Cell</td>
        <td>1</td>
        <td>90자</td>
        <td>2</td>
        <td>17</td>
    </tr>
    <tr>
        <td>8</td>
        <td>스타일 템플릿_타이틀 자유형</td>
        <td>Cell</td>
        <td>1</td>
        <td>90자</td>
        <td>2</td>
        <td>16</td>
    </tr>
    <tr>
        <td>9</td>
        <td>기본 템플릿_타이틀 자유형</td>
        <td>Free</td>
        <td>1</td>
        <td>90자</td>
        <td>0</td>
        <td>0</td>
    </tr>
    <tr>
        <td>10</td>
        <td rowspan="8">이미지<br/>템플릿</td>
        <td>이미지 & 타이틀 강조형(3:4)</td>
        <td>Highlighted Image n Title</td>
        <td>1</td>
        <td>500자</td>
        <td>2</td>
        <td>16</td>
        <td>Long(900x1200)</td>
    </tr>
    <tr>
        <td>11</td>
        <td>이미지 & 타이틀 강조형(1:1)</td>
        <td>Highlighted Image n Title</td>
        <td>1</td>
        <td>500자</td>
        <td>2</td>
        <td>16</td>
        <td>Square(900x900)</td>
    </tr>
    <tr>
        <td>12</td>
        <td>이미지 강조형(3:4)</td>
        <td>Highlighted Image</td>
        <td>1</td>
        <td>500자</td>
        <td>2</td>
        <td>16</td>
        <td>Long(900x1200)</td>
    </tr>
    <tr>
        <td>13</td>
        <td>이미지 강조형(1:1)</td>
        <td>Highlighted Image</td>
        <td>1</td>
        <td>500자</td>
        <td>2</td>
        <td>16</td>
        <td>Square(900x900)</td>
    </tr>
    <tr>
        <td>14</td>
        <td>섬네일형(세로)</td>
        <td>Thumbnail</td>
        <td>1</td>
        <td>500자</td>
        <td>2</td>
        <td>16</td>
        <td>Vertical(900x560)</td>
    </tr>
    <tr>
        <td>15</td>
        <td>섬네일형(가로)</td>
        <td>Thumbnail</td>
        <td>1</td>
        <td>500자</td>
        <td>2</td>
        <td>16</td>
        <td>Horizontal(900x560)</td>
    </tr>
    <tr>
        <td>16</td>
        <td>SNS형</td>
        <td>SNS</td>
        <td>1</td>
        <td>500자</td>
        <td>2</td>
        <td>16</td>
        <td>Square(900x900)</td>
    </tr>
    <tr>
        <td>17</td>
        <td>SNS형(중간 버튼)</td>
        <td>SNS</td>
        <td>1</td>
        <td>500자</td>
        <td>2</td>
        <td>16</td>
        <td>Rectangle(900x560)</td>
    </tr>
</table>