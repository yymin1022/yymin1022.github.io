---
layout: post
title:  "[Synology/Linux] Docker Ubuntu 서비스 자동시작"
author: LR
categories: [ DIY, DSM, LINUX, NAS, OS, SERVER, SYNOLOGY, XPENOLOGY ]
image: "/images/Thumbnails/210101 Synology Reverse Proxy HSTS Fix.png"
featured: false
hidden: true
description: \#DIY \#DSM \#HardKernel \#Linux \#NAS \#ODroid \#OS \#Server \#Synology \#XPEnology
---
안녕하세요!<br>
대학생 1인 개발자로 활동중인 LR입니다!

저는 현재 ODroid H2에 XPEnology를 설치해<br>
개인 NAS로 활용하고 있습니다.

단순 파일 저장 목적 뿐만 아니라<br>
제가 소속한 팀의 웹 페이지 호스팅,<br>
미디어 스트리밍, VSCode 등<br>
각종 서비스들을 함께 구축해두고<br>
DSM의 기본 기능인 역방향 프록시를 이용해<br>
도메인과 연결하여 사용하고 있습니다.

그런데, Synology 역방향 프록시에는<br>
고질적인 버그가 하나 있습니다.

<center>
<img src="/images/PostImages/210101 Synology Reverse Proxy HSTS Fix/1_hsts_setting.png" style="width: 75%;">
</center>

위와 같이 외부에서 들어오는 접속을 https로 설정한 뒤<br>
HSTS를 적용한 상태이더라도<br>
http를 이용해서 도메인에 접속할 경우<br>
HSTS가 올바르게 작동하지 않아,<br>
도메인이 서버로 연결되지 않는 문제가 발생합니다.<br>

그래서 임시로 http 접속을 따로 역방향 프록시에 지정해주어<br>
연결은 되도록 해두었으나, 이렇게 할 경우<br>
https가 적용되지 않은 일반 프로토콜로 연결되어<br>
보안성이 사라지는 단점이 있습니다.

이 문제를 해결하고자 구글링을 하던 도중,<br>
해외 포럼에서 관련 해결 팁을 찾게되어<br>
한번 글로 정리해보고자 합니다.

간략하게 설명하자면 Apache를 이용해<br>
.htaccess 규칙을 작성해주어 http를 https로 리디렉션하게 한 뒤<br>
역방향프록시를 이 Apache 호스트에 연결시키는 방식입니다.

먼저, 다음 코드를 복사해 .htaccess파일을 생성해준 뒤<br>
NAS의 적절한 위치에 저장해줍니다.

```
RewriteEngine on
RewriteCond %{HTTPS} off
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}
```

저는 docker 공유폴더의 Apache_HSTS 디렉토리를 생성하고<br>
그 안에 .htaccess 파일을 위치시켰습니다.

​<center>
<img src="/images/PostImages/210101 Synology Reverse Proxy HSTS Fix/2_file_htaccess.png" style="width: 75%;">
</center>

다음으로 Synology 패키지 센터에서<br>
Apache 2.4와 Web Station을 설치해줍니다.

<center>
<img src="/images/PostImages/210101 Synology Reverse Proxy HSTS Fix/3_package_apache.png" style="width: 75%;">
</center>

<br>

<center>
<img src="/images/PostImages/210101 Synology Reverse Proxy HSTS Fix/4_package_webstation.png" style="width: 75%;">
</center>

설치가 완료되었다면 Web Station을 실행하고,<br>
좌측 메뉴 중 가상호스트 항목으로 이동해<br>
생성을 클릭해줍니다.

<center>
<img src="/images/PostImages/210101 Synology Reverse Proxy HSTS Fix/5_apache_setup.png" style="width: 75%;">
</center>

위와 같이 설정을 해준 뒤 확인을 클릭합니다.<br>
이때, HTTP 포트번호는 임의의 번호로 지정하셔도 무방하나,<br>
어떤 번호로 지정하셨는지는 꼭 기억해주셔야합니다.<br>
문서 루트의 경우는, .htaccess가 저장된 디렉토리를 선택해주시면 됩니다.

저장이 완료되었다면, 이제 역방향 프록시를 설정해줍니다.<br>
제어판의 응용 프로그램 포털 메뉴에서 역방향 프록시 탭으로 이동합니다.<br>
이제 역방향 프록시를 설정할 서비스를 각각 추가해 설정해주시면 됩니다.

<center>
<img src="/images/PostImages/210101 Synology Reverse Proxy HSTS Fix/6_reverse_proxy_setup.png" style="width: 75%;">
</center>

저는 3개의 서비스를 역방향 프록시로 연결해 사용하고 있습니다.<br>
각 항목의 http와 https 각각을 모두 역방향 프록시로 연결해주어야 하는데,

위 사진과 같이 http의 경우는 아까 WebStation에서 설정했던 8081번 포트로,<br>
https의 경우에는 곧바로 해당하는 서비스의 포트로 이동하게 설정해주면<br>
http로 접속할 경우 Apache의 .htaccess 규칙을 참고해<br>
https를 이용한 도메인으로 자동 리디렉션됩니다.

이처럼, Synology의 역방향 프록시의 HSTS가<br>
올바르게 작동하지 않는 문제를 해결하는 방법에 대해 알아보았습니다.

저는 처음에 XPEnology에서만 발생하는 보안 관련 문제로 생각했는데,<br>
기성품 Synology를 사용하고 있는 지인에게서도 같은 문제가 발생한다고 해서<br>
구글링을 해보니 이미 해외 포럼에서는 유명한 문제점이었습니다.

하지만 언제나와 같이 어떻게든 문제를 해결할 방법은 존재했고,<br>
그 방법을 한번 소개해보았습니다.

혹시 진행 과정에서 문제가 발생하거나<br>
잘 되지 않을 경우 댓글로 남겨주시면<br>
아는 선에서 답변드리도록 하겠습니다.

지금까지,<br>
LR이었습니다!




안녕하세요,<br>
대학생 1인 개발자로 활동중인 LR입니다!​

저는 현재 개인 Nas 서버로<br>
```XPEnology OS``` 를 설치해서,<br>
```Synology``` 인 척 하며 사용하고 있습니다.

여기서 동시에,<br>
```Docker``` 를 이용해 ```Ubuntu``` 를 구동하며<br>
```Apache2``` 로 구성한 웹 서버도 동시에 실행하고 있는데요,<br>
```Synology``` 에서 기본적으로 제공하는 ```Docker``` 패키지의 경우,<br>
GUI 형태로 구현되어 있어<br>
일반적인 ```Linux``` 등에서 구동하는 ```Docker``` 명령과는<br>
조금 사용법이 다릅니다.

<center>
<img src="/images/PostImages/200814 Synology Docker Ubuntu Service Startup/1_docker_list.png" style="width: 75%;">
</center>

```Ubuntu``` 에서 특정 서비스에 대해<br>
부팅시 자동시작을 활성화하기 위해서는<br>
다음 명령을 실행해주면 됩니다.

```bash
ubuntu@desktop: $ sudo update-rc.d apache2 defaults
```

위 코드를 실행하게 되면<br>
```defaults```, 즉 ```Initialize Run Level```이 3, 5일 경우<br>
해당 서비스의 ```start``` 명령이 실행됩니다.

하지만 ```Docker``` 에서 구동하는 ```Ubuntu``` 의 경우는,<br>
별도의 ```Run Level``` 을 고려하지 않고,<br>
스냅샷 형태로 구동되기에<br>
위 방법으로는 자동시작 활성화가 불가합니다.

Stackoverflow 등을 참고하면,<br>
일반적인 ```Docker``` 에서 특정 서비스를 자동시작 하기 위해서는<br>
다음 링크들에서 확인할 수 있는 별도의 조치를 취해주어야 한다고 합니다.

<a href="https://askubuntu.com/questions/1054664/run-script-when-dockercontainer-starts" target="_sub">관련 쓰레드 1 : AskUbuntu.com</a>

<a href="https://stackoverflow.com/questions/26938684/docker-io-init-d-script-not-working-on-start-container" target="_sub">관련 쓰레드 2 : Stackoverflow</a>

하지만 ```Synology``` 의 ```Docker``` 의 경우,<br>
컨테이너 실행 명령을 별도로 편집할 수가 없기에,<br>
위 방법도 활용할 수 없습니다.

그래서 저는, 약간의 편법을 이용하여 서비스 자동시작을 구현하였습니다.<br>
먼저, 제가 서비스를 수동으로 실행할 때 입력하는 명령은 다음과 같습니다.

```bash
ubuntu@desktop: $ sudo service apache2 start
ubuntu@desktop: $ sudo /etc/init.d apache2 start
```

두 명령 중 하나를 실행할 경우, ```apache2``` 서비스의 스크립트가 실행되며<br>
서비스가 시작됩니다.

```Docker``` 의 ```Ubuntu``` 가 구동되면,<br>
기본적으로 실행되는 명령은<br>
```root``` 계정의 ```Bash Shell Initialize``` 명령입니다.

<center>
<img src="/images/PostImages/200814 Synology Docker Ubuntu Service Startup/2_docker_main.png" style="width: 75%;">
</center>

```Linux``` 의 특성상, ```Bash Shell``` 이 ```Initialize```  될 경우,<br>
해당 계정의 홈 폴더에 위치한 ```.bashrc``` 파일이 실행되며,<br>
해당 파일 내에 기록한 명령들이 순차적으로 실행됩니다.

그래서 저는 수동으로 서비스를 시작할 때 입력하던 명령을<br>
```.bashrc``` 파일의 맨 하단에 입력해줌으로써,<br>
```root``` 계정의 ```Bash Shell``` 이 ```Initialize``` 되는 시점에<br>
서비스도 함께 시작되도록 해주었습니다.

<center>
<img src="/images/PostImages/200814 Synology Docker Ubuntu Service Startup/3_docker_command.png" style="width: 50%;">
</center>

이렇게 해주면, GUI 환경만으로 제공되는<br>
```Synology``` 의 ```Docker``` 에서도 ```Ubuntu``` 의 서비스 자동시작 기능을<br>
활용해 구동시킬 수 있습니다.

편법이긴 하지만<br>
이것저것 삽질해보던 중 찾아낸<br>
가장 간단하다고 생각되는 방법인데,<br>
혹시 더 좋은 방법이 있다면<br>
댓글로 조언 남겨주시면 감사하겠습니다.

지금까지,<br>
LR이었습니다!