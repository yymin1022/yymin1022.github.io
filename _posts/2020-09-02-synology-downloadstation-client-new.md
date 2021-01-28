---
layout: post
title:  "[Windows/Linux] Synology Download Station 클라이언트 V1.1"
author: LR
categories: [ DEVELOPMENT, DIY, LINUX, PYQT5, PYTHON, SYNOLOGY, WINDOWS, XPENOLOGY ]
image: "/images/Thumbnails/200824 Synology DownloadStation Client.png"
featured: false
hidden: true
description: \#Development \#DIY \#Linux \#PyQt5 \#Python \#Synology \#Windows \#XPEnology
---
안녕하세요,<br>
대학생 1인 개발자로 활동중인 LR입니다!

지난 8월, Synology의 Download Station을<br>
PC에서 간단히 이용할 수 있는 클라이언트 프로그램을<br>
개발해 배포했었는데요,

미처 생각치 못한 문제가 있어<br>
해당 부분을 패치하고 업데이트를 진행하게 되었습니다!

지난 버전 배포글에서 사용법 등을 자세히 설명했던 만큼<br>
오늘 포스팅에서는 간략한 변경점만 언급하도록 하겠습니다.<br>
자세한 내용은 이전 배포글을 참고해주세요.

<a href="https://blog-lr.defcon.or.kr/200824-synology-downloadstation-client">이전 버전 포스팅 보러가기</a>

지난 버전의 경우, OTP 관련한 예외사항을 처리하지 않아,<br>
OTP를 이용중이신 유저분들은 서버오류 다이얼로그만이<br>
지속적으로 발생하는 문제가 있었습니다.

이번 버전에서는 OTP 로그인에 대응하여<br>
최초 로그인시 OTP 사용 여부를 묻고,<br>
이 경우 로그인시 OTP 인증코드를 입력하는 다이얼로그가<br>
먼저 표시되도록 하였습니다.

<center>
<img src="/images/PostImages/200902 Synology DownloadStation Client New/1_program_login.png" style="width: 50%;">
</center>

OTP를 이용중이신 유저분들은, 기존 로그인 다이얼로그에서<br>
하단의 체크박스만을 체크한 뒤 로그인 해주시면 됩니다.

<center>
<img src="/images/PostImages/200902 Synology DownloadStation Client New/2_program_otp.png" style="width: 50%;">
</center>

OTP 사용이 활성화된 경우,<br>
매 세션 로그인시마다 OTP코드 입력창이 표시됩니다.<br>​

OTP 사용을 해제하고자 하시는 경우에는<br>
account.uum 파일을 삭제하시고<br>
새로 로그인 정보를 작성해주시면 됩니다.

__!! 이전 버전에서 새로 업그레이드 하시는 경우,<br>__
__기존에 생성된 account.uum 파일을 삭제하신 뒤<br>__
__새 버전을 사용해주시기 바랍니다 !!__

다운로드는 아래 링크에서 진행하실 수 있습니다.<br>
Ver 1.1 디렉터리 내의 파일을 받아주시면 됩니다.

__!! 일부 브라우저에서 파일 다운로드 시<br>__
__손상된 파일이 다운로드되는 문제가 있습니다.<br>__
__이 경우, 폴더 전체를 다운받으신 뒤<br>__
__압축 해제하여 이용해주시면 감사하겠습니다. !!__

<a href="https://drive.defcon.or.kr/fsdownload/uZCx2TGQf/Ver%201.1" target="_sub">DownloadStation Client 다운로드</a>

지난 배포 버전에서 OTP 관련 의견 제시해주신<br>
클리앙의 쿠니s님께 감사의 말씀을 전하며<br>
오늘 배포 포스팅을 마무리하도록 하겠습니다.

지금까지,<br>
LR이었습니다!


__!! 2020년 9월 2일에 V1.1이 배포되었습니다.__

__본 게시글은 사용법 확인을 위해서만 읽어주시고,__

__다운로드는 새 버전의 포스팅을 이용해주세요 !!__

__<a href="https://blog-lr.defcon.or.kr/synology-downloadstation-client-new" target="_sub">새 버전 포스팅 확인하기</a>__

<br>
<br>

안녕하세요,<br>
대학생 1인 개발자로 활동중인 LR입니다!

오늘 포스팅도 평소 자주 작성하던 리뷰 포스팅이 아닌,<br>
제가 직접 개발한 프로그램을 공유하는 포스팅이 되었습니다.

저는 현재 ```ODroid H2``` 개발보드에<br>
```XPEnology``` 운영체제를 설치해<br>
개인 Nas로 활용하고 있습니다.

<a href="https://blog-lr.defcon.or.kr/200311-odroid-h2-xpenology-guide">ODroid H2 XPEnology 설치 가이드 포스팅</a>

```XPEnology``` 는 ```Synology``` 사의 Nas용 운영체제를<br>
다른 기기에서도 사용할 수 있도록 변조시킨 운영체제입니다.

이 ```Synology DSM``` 운영체제에서는<br>
URL이나 토렌트 파일을 이용해<br>
Nas로 간편하게 파일을 다운로드할 수 있는<br>
```Download Station``` 이라는 기능을 제공합니다.



용량이 큰 파일의 경우, ```Download Station``` 을 이용해 다운로드 하게되었을 때,<br>
지속적으로 안정적인 속도로 다운로드 작업을 진행하기 때문에<br>
오류 없이 빠른 속도로 다운로드를 할 수 있습니다.

하지만 이런 편리한 기능을 제공하는 ```Download Station``` 이지만,<br>
매번 DSM에 웹상으로 접속해 이용해야 한다는 점이 불편하게 느껴졌습니다.​

```Android``` 와 ```iOS``` 의 경우, DS Get 또는 기타 서드파티 애플리케이션을 이용해서<br>
굳이 DSM에 접속하지 않고도 ```Download Station``` 에<br>
다운로드 작업을 등록하거나 기존 작업을 제어하는 것이 가능합니다.

다만, ```Windows``` 는 이러한 클라이언트 프로그램이 거의 존재하지 않기에<br>
이 기회에 직접 한번 만들어보게 되었습니다.

<center>
<img src="/images/PostImages/200824 Synology DownloadStation Client/2_client_login.png" style="width: 50%;">
</center>

프로그램을 최초 실행하게 되면,<br>
위와 같은 로그인 창이 보이게됩니다.<br>
위에서부터 순차적으로 사용중인 DSM의 주소와 계정을 입력해줍니다.<br>
이때, DSM의 주소의 경우 ```http://hello.synology.me``` 와 같이<br>
http 또는 https로 시작하는 형태로 입력해주셔야 합니다.​

이때 입력하는 계정 정보는 별도의 서버에 저장되지 않고,<br>
Login 버튼을 클릭하는 순간 프로그램을 실행하신 위치에 설정파일이 생성되며<br>
해당 파일에 암호화되어 기록됩니다.<br>
이후 실행시에는 해당 파일을 읽어들여<br>
지정된 DSM에 로그인하는 용도로만 활용됩니다.

DSM의 주소와 계정 정보를 올바르게 입력했다면,<br>
Login 버튼을 클릭했을 때<br>
프로그램의 메인 화면으로 진입하게 됩니다.

<center>
<img src="/images/PostImages/200824 Synology DownloadStation Client/3_client_main.png" style="width: 50%;">
</center>

맨 위에는 리스트를 새로 불러오기 위한 새로고침 버튼,<br>
그리고 현재 등록되어있는 작업 리스트가 위치합니다.<br>
그 아래로는 다운로드 작업을 추가로 등록하기 위한 입력란과<br>
입력된 작업들을 DSM으로 전송해 다운로드를 시작하는<br>
버튼이 위치합니다.

```Python``` 으로 작성된 프로그램의 특성상,<br>
반복적으로 리스트의 새로고침을 구현하는 것이 사실상 불가능 하였기에,<br>
부득이하게 수동 새로고침 형태로 버튼을 추가하게 되었습니다.<br>
다만, 다운로드 작업을 추가하거나 기존 작업을 제어하는 경우<br>
자동적으로 새로고침을 하도록 해두었기에,<br>
큰 불편함은 없으리라 생각됩니다.

상단 리스트에서 작업을 클릭할 경우,<br>
해당 작업을 제어할 수 있는 메뉴가 표시됩니다.

<center>
<img src="/images/PostImages/200824 Synology DownloadStation Client/4_client_main_manage.png" style="width: 50%;">
</center>

일시정지 또는 이어받기를 클릭할 경우,<br>
진행중인 작업을 일시적으로 정지시키거나<br>
일시정지 상태인 작업을 이어서 진행하도록 합니다.

삭제 버튼을 클릭할 경우, 진행중인 작업은 취소되며<br>
목록에서 해당 작업이 삭제됩니다.

다운로드 작업을 추가하고자 할 경우,<br>
해당 파일의 URL 또는<br>
토렌트 파일명을 입력해줍니다.<br>
이때, 토렌트 파일의 경우 프로그램을 실행한 위치에 저장해 두어야 합니다.

<center>
<img src="/images/PostImages/200824 Synology DownloadStation Client/5_client_main_register.png" style="width: 50%;">
</center>

이처럼, 한 줄당 하나의 다운로드 작업을 입력해<br>
한번에 여러 작업을 등록하는 것이 가능합니다.<br>​

## 다운로드

<a href="https://drive.defcon.or.kr/fsdownload/uZCx2TGQf/Ver%201.0" target="_sub">DownloadStation Client 다운로드</a>

다운로드는 위 링크에서 가능하며,<br>
```Windows``` 용 exe 파일과 ```Linux``` 용 바이너리 파일을<br>
모두 배포합니다.<br>
사용중인 운영체제에 맞는 프로그램을 받아 이용하시면 되겠습니다.

## 소스코드 및 공유

<a href="https://github.com/yymin1022/Synology_DownloadStation_Client" target="_sub">소스코드 보러가기</a>

본 프로젝트의 모든 소스코드는 제 ```Github``` 를 통해 공개합니다.<br>
단, 소스코드를 활용하고자 하시는 경우,<br>
제 원본 ```Github``` 링크를 남겨주시기 바라며,<br>
혹시나, 본 프로그램을 공유하고자 하실 경우,<br>
새로운 글을 작성하거나 파일을 직접 첨부하지 마시고,<br>
본 포스팅의 링크를 첨부해주시면 감사하겠습니다.

규모가 큰 그런 프로그램은 아니지만,<br>
```Synology``` 의 ```DownloadStation``` 에서 제공하는 중심적인 기능들은<br>
대부분 지원하기 때문에, 어느정도 불편함을 해소할 수 있는<br>
그런 프로그램이라고 생각합니다.

많은 사용자를 바라고 개발한 프로그램이라기보다는<br>
제가 편하게 이용하고자 개발하기 시작한 프로그램이다 보니<br>
개발하고 나서의 뿌듯함이 배가 되는 듯 싶습니다.

지금까지,<br>
LR이었습니다!