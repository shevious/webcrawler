
# GIT

공통 작업자 승낙  
https://github.com/shevious/webcrawler/invitations  

# windows

## python

https://www.python.org/downloads/windows/  
[Windows x86-64 executable installer](https://www.python.org/ftp/python/3.8.0/python-3.8.0-amd64.exe)  
설치 시:  
Install now  
 - [x] Add Python 3.8 to Path
 - Disable Path Length LImit 버튼 클릭

## git bash

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

## scrapy 설치

virtualenv에서  
```bash
pip install scrapy
pip install scrapyd
```

https://docs.scrapy.org/en/latest/intro/tutorial.html  

```bash

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNTg4ODUxMTcsMTkxNzIwMzMyNCwtOD
U1MjcxMzQ5XX0=
-->