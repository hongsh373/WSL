# WSL
## A guide to setup VSCode C using WSL

### 2026년 WSL 설치법(최종수정 2026.03.12)

[Windows 기능 켜기/끄기] 실행 - Win+R - [optionalfeatures] 실행(확장자 없음)
[가상 머신 플랫폼] 체크 설정 (Virtual Machine Platform)

관리자 권한으로 PowerShell 실행
  Enable-WindowsOptionalFeature -Online -Featurename Microsoft-Windows-Subsystem-Linux
예상된 결과값: [Path:, Online:, RestartNeeded:]

Ubuntu 24.04 설치(MS Store) - 만약 안된다면 Win+R - [wsreset.exe] 실행 / user과 password 설정하기
Ubuntu를 관리자 권한으로 실행 후
```
$ sudo apt update
$ sudo apt upgrade
$ sudo apt-get install build-essential gdb
```

이 단계에서 systemd, etc/passwd 관련 에러 발생 시 CMD 창을 새로 열고(Ubuntu 창 아님) WSL 2로 업데이트

VS CODE 설치 [https://code.visualstudio.com/] 실행, 다운로드, 설치
```
$ pwd		→ /home/(user) 출력됨
$ mkdir hands-on
$ cd hands-on
$ code .		→ 설치되고 VS CODE 실행됨
```

VS CODE Welcome 창 켜짐
좌측 [EXPLORER] - [v PROJECTS] 호버링 시 왼쪽에서 1번째 [New File..] 클릭
helloworld.cpp 입력
우하단 알림창 Install 클릭

Extension 설치 : CODE 좌측 상단 6개 아이콘 중 제일 아래 네모 4개 아이콘(Extensions) 실행
@id:ms-vscode.cpptools	→ 설치
WSL			→ 설치

코드 입력
``` C
#include <stdio.h>
void main() {
  printf("Hello, World!");
}
```

메뉴 - [Terminal] - [Configure Default Build Task...] - 위에 뜬 창 중 2번째 [C/C++: g++ build active file] 실행
tasks.json 파일 생성됨.(build 환경 설정하는 파일) - Ctrl+S(저장) 후 닫고, helloworld.cpp Ctrl+Shift+B 통해 build
Ctrl+J 통해 Terminal 실행
./helloworld	→ Build된 helloworld 실행됨.

--------------------------예상되는 문제--------------------------
1. Windows 기능 켜기/끄기 - 가상 머신 플랫폼 check


2. WSL 2 설치법 - 에러 로그에 systemd나 etc/passwd같은 내용들이 언급됨

CMD창에서 wsl -l -v 실행 시
Ubuntu-24.04	Running	2 라고 나와야 함

2가 아닌 1로 뜬다면
(계속 cmd에서)
```
wsl -l -v
wsl --update
wsl --set-version Ubuntu-24.04 2
wsl --set-default-version 2
```
이 순서로 입력하여 해결
