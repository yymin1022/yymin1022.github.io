---
layout: post
title:  "[Windows/Linux] Synology Download Station 클라이언트 V1.1"
author: LR
categories: [ DEVELOPMENT, DIY, LINUX, PYQT5, PYTHON, SYNOLOGY, WINDOWS, XPENOLOGY ]
image: "/images/Thumbnails/200824 Synology DownloadStation Client.png"
featured: false
hidden: false
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

<a href="https://blog-lr.defcon.or.kr/synology-downloadstation-client">이전 버전 포스팅 보러가기</a>

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

<a href="https://drive.defcon.or.kr/fsdownload/pFi9wgI6c/Ver%201.1" target="_sub">DownloadStation Client 다운로드</a>

지난 배포 버전에서 OTP 관련 의견 제시해주신<br>
클리앙의 쿠니s님께 감사의 말씀을 전하며<br>
오늘 배포 포스팅을 마무리하도록 하겠습니다.

지금까지,<br>
LR이었습니다!