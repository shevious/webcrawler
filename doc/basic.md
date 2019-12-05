
# GIT

github 계정 생성  
id 송부 

공통 작업자 승낙  
https://github.com/shevious/webcrawler/invitations  

## stackedit

stackedit.io
우측 상단 클릭
workspace => add a github workspace
https://github.com/shevious/webcrawler/
ok->ok


# windows

## python

https://www.python.org/downloads/windows/  
[Windows x86-64 executable installer](https://www.python.org/ftp/python/3.8.0/python-3.8.0-amd64.exe)  
설치 시:  
Install now  
 - [x] Add Python 3.8 to Path
 - Disable Path Length LImit 버튼 클릭

## git bash

https://gitforwindows.org/  

설치 시:
 - [x] checkout as-is, commit as-is
 - [x] Use Window's default console window
 - [x] Enable Symbolic links

## openssh server windows

[Windows Server 2019 및 Windows 10용 OpenSSH 설치](https://docs.microsoft.com/ko-kr/windows-server/administration/openssh/openssh_install_firstuse)  

[Setting to use git-bash as default shell when connecting remotely via OpenSSH to Windows Server 2016](https://superuser.com/questions/1332346/setting-to-use-git-bash-as-default-shell-when-connecting-remotely-via-openssh-to)  

powershell:

```bash
#check
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'


# Install the OpenSSH Server
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

Start-Service sshd
# OPTIONAL but recommended:
Set-Service -Name sshd -StartupType 'Automatic'
# Confirm the Firewall rule is configured. It should be created automatically by setup. 
Get-NetFirewallRule -Name *ssh*
# There should be a firewall rule named "OpenSSH-Server-In-TCP", which should be enabled
# If the firewall does not exist, create one
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22

# git bash를 default 값으로
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Program Files\Git\bin\bash.exe" -PropertyType String -Force
```

## pycharm

https://www.jetbrains.com/ko-kr/pycharm/download/#section=mac  
프로페셔널 버전

설치:  

 - [x] Don't send
 - 테마선택: black or white
 - [x] Evaluation for Free

크랙:  
```
 Usage:
 0. Download the zip package and get jetbrains-agent.jar first
    Download page: https://zhile.io/2018/08/17/jetbrains-license-server-crack.html
 1. Run the IDE and evalutate for free
 2. Click IDE menu "Configure" or "Help" -> "Edit Custom VM Options..."
    See: https://intellij-support.jetbrains.com/hc/en-us/articles/206544869
 3. Append -javaagent:/absolute/path/to/jetbrains-agent.jar to end line
    eg:
      mac:      -javaagent:/Users/neo/jetbrains-agent.jar
      linux:    -javaagent:/home/neo/jetbrains-agent.jar
      windows:  -javaagent:C:\Users\neo\jetbrains-agent.jar
    Rescue: https://intellij-support.jetbrains.com/hc/en-us/articles/206544519
 4. Restart IDE
 5. Click IDE menu "Help" -> "Register..." or "Configure" -> "Manage License..."
    Support "License server" and "Activation code":
    1). Entry license server address: http://jetbrains-license-server (maybe autofill)
        Or click the button: "Discover Server" to fill automaticly
    2). Active offline with the activation code file: ACTIVATION_CODE.txt
        If the activation window always pops up(error 1653219), remove jetbrains' domains from hosts file
        If you need a custom license name, visit: https://zhile.io/custom-license.html
```

## virtualenv

```bash
# virutalenv 만들기
cd ~
python -m venv venv

# virtualenv 진입
# git bash
source venv/Scripts/activate
# command
venv\Scripts\activate.bat

# virtualenv 나가기
deactivate
```

## visual studio 설치

https://visualstudio.microsoft.com/ko/downloads/  
커뮤니티 에디션 설치  
설치시 C++ desktop만 선택  

## pip 사용방법

```
pip list
```

## scrapy 설치

virtualenv에서  
```bash
pip install scrapy
pip install scrapyd
```

https://docs.scrapy.org/en/latest/intro/tutorial.html  

```bash
scrapy startproject tutorial
```

# 크롤 사이트

http://www.uill.or.kr/UR/info/lecture/list.do?rbsIdx=34&page=1  


# portia

project folders:

/app/data/projects

```html
<a href="#" onclick="fn_applCheck2(\'view.do?rbsIdx=34&page=1&organIdx=3175&idx=EX18645\');return false;" onkeypress="this.onclick;" style="color:#ff8c23;">(\xec\xa3\xbc\xea\xb0\x84)\xeb\xb0\x94\xeb\x94\x94\xeb\x9d\xbc\xec\x9d\xb8 \xec\x9a\x94\xea\xb0\x80&\xed\x95\x84\xeb\x9d\xbc\xed\x85\x8c\xec\x8a\xa4</a>
```

https://stackoverflow.com/questions/42989774/scrapy-spider-cant-find-urls-that-load-on-click  

response.x를 사용해 보자

## 

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg3NjkwMjU4NSwxMjgzNjU0Njk3LC0xMj
MwODIyNzI4LDc2MDk0Mjk4MiwtNjM4Mjc4MTI1LC0xNTI3MzU0
Njg0LC0xMjM0MDgxNTg5LDE5ODk4OTM1OTcsMTEwNDMxMTQ5NC
wyMTIyNzc5ODU5LC0yMDU4ODg1MTE3LDE5MTcyMDMzMjQsLTg1
NTI3MTM0OV19
-->