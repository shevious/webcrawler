
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

경북
http://www.gile.or.kr/web/lecture/list.do?mId=72&page=1

# portia

project folders:

/app/data/projects

```html
<a href="#" onclick="fn_applCheck2(\'view.do?rbsIdx=34&page=1&organIdx=3175&idx=EX18645\');return false;" onkeypress="this.onclick;" style="color:#ff8c23;">(\xec\xa3\xbc\xea\xb0\x84)\xeb\xb0\x94\xeb\x94\x94\xeb\x9d\xbc\xec\x9d\xb8 \xec\x9a\x94\xea\xb0\x80&\xed\x95\x84\xeb\x9d\xbc\xed\x85\x8c\xec\x8a\xa4</a>
```

https://stackoverflow.com/questions/42989774/scrapy-spider-cant-find-urls-that-load-on-click  

response.x를 사용해 보자

## xpath tutorial

https://docs.scrapy.org/en/xpath-tutorial/topics/xpath-tutorial.html  

selectors: 
https://exposingtheinvisible.org/guides/scraping/  

## 강원

dhe 문제:  
https://github.com/scrapy/scrapy/pull/3442  

해결 방법:    

1. 명령줄 옵션 방식(1)  
    ```bash
    scrapy shell "https://www.e-room.or.kr/gw/portal" -s DOWNLOADER_CLIENT_TLS_CIPHERS='DEFAULT:!DH'
    ```
2. `settings.py`에 추가 방식

    ```py
    DOWNLOADER_CLIENT_TLS_CIPHERS='DEFAULT:!DH'
    ```

## Oracle 11g 

```bash
docker run --name oracle11g -d -p 8080:8080 -p 1521:1521 jaspeen/oracle-xe-11g

docker exec -it oracle11g sqlplus
system / oracle

http://192.168.33.10:8080/apex/
workspace: INTERNAL
user: ADMIN
password: oracle
```
create database:  
```sql
CONNECT SYS AS SYSDBA
select USERNAME, DEFAULT_TABLESPACE from DBA_USERS;
/* or */
select USERNAME, DEFAULT_TABLESPACE from DBA_USERS where 
DEFAULT_TABLESPACE = 'DEV_DB';
/* or */
select distinct tablespace_name from user_tables;
```


## django 1.11

https://code.djangoproject.com/ticket/29759

```
pip install django==1.11.26
pip install cx_oracle==6.4.1
django-admin.py startproject myproj
cd myproj
./manage.py migrate
# ⇒ migrate 성공

./manage.py startapp myapp
```
https://developer.oracle.com/dsl/vasiliev-django.html  


## django 3 (oracle 11g안됨)
`myproj/settings.py`
```py
INSTALLED_APPS = [
    'myapp.apps.MyappConfig', # add this line
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

]

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.oracle',
        'NAME': 'xe',
        'USER': 'system',
        'PASSWORD': 'oracle',
        'HOST': 'localhost',
        'PORT': '1521',
    }
}
```
`myapp/models.py`
```py
from django.db import models

class employees(models.Model):
    employee_id = models.IntegerField(primary_key=True)
    first_name = models.CharField(max_length=20, null = True)
    last_name = models.CharField(max_length=25)
    email = models.CharField(max_length=25)
    class Meta:
         db_table = "employees"

class departments(models.Model):
    department_id = models.IntegerField(primary_key=True)
    department_name = models.CharField(max_length=30)
    manager = models.ForeignKey(employees, null = True, on_delete=models.CASCADE)
    class Meta:
         db_table = "departments"
```
`myapp/views.py`
```py
from django.template import Context, loader
from django.http import HttpResponse
from myapp.models import employees, departments

def index(request):
    department_list = departments.objects.exclude(manager__employee_id__exact = None).order_by('manager__employee_id')
    tmpl = loader.get_template("index.html")
    cont = Context({'departments': department_list})
    return HttpResponse(tmpl.render(cont))

from django.shortcuts import get_object_or_404
from django.db import transaction

@transaction.atomic
def newdept(request, emp_id, dept_name, dept_id):
    new_dept = departments(department_id = dept_id, department_name = dept_name, manager = None)
    new_dept.save()
    emp = get_object_or_404(employees, employee_id__exact = emp_id)
    new_dept.manager = emp
    new_dept.save()
    return HttpResponse("The %s department record has been inserted." %dept_name )
```
`myapp/templates/index.html`
```html
<h1>Managers of departments</h1>
<table border = 1px cellpadding="3" style="font-family:Arial">
<tr>
<th>empid</th>
<th>first name</th>
<th>first name</th>
<th>email</th>
<th>department name</th>
</tr>
{% for department in departments %}
<tr>
<td>{{department.manager.employee_id}}</td>
<td>{{department.manager.first_name}}</td>
<td>{{department.manager.last_name}}</td>
<td>{{department.manager.email}}</td>
<td>{{department.department_name}}</td>
{% endfor %}
</table>
```
`myproj/urls.py`
```py
from django.urls import path, include
    path('myapp/', include('myapp.urls')),
```
`myapp/urls.py`
```py
from django.contrib import admin
from django.urls import path
from myapp.views import index, newdept

urlpatterns = [
    path('', index),
    path(r'^(?P<emp_id>\d+)/(?P<dept_name>\w+)/(?P<dept_id>\d+)/$' , newdept),
]
```


https://stackoverflow.com/questions/49229664/configure-the-django-with-oracle-11g-data-base-issue  



## openssl 

cipher list
https://www.openssl.org/docs/man1.0.2/man1/ciphers.html  

## 작업중

#### oracle instant client on ubuntu

https://www.oracle.com/database/technologies/instant-client/linux-x86-64-downloads.html  

```bash
sudo apt install alien -y

wget https://download.oracle.com/otn_software/linux/instantclient/195000/oracle-instantclient19.5-basic-19.5.0.0.0-1.x86_64.rpm
sudo alien --scripts oracle-instantclient19.5-basic-19.5.0.0.0-1.x86_64.rpm
sudo dpkg -i oracle-instantclient19.5-basic_19.5.0.0.0-2_amd64.deb
brew install libaio

# sqlplus
wget https://download.oracle.com/otn_software/linux/instantclient/195000/oracle-instantclient19.5-sqlplus-19.5.0.0.0-1.x86_64.rpm
sudo alien --scripts oracle-instantclient19.5-sqlplus-19.5.0.0.0-1.x86_64.rpm
sudo dpkg -i oracle-instantclient19.5-sqlplus_19.5.0.0.0-2_amd64.deb

# optional
wget https://download.oracle.com/otn_software/linux/instantclient/195000/oracle-instantclient19.5-devel-19.5.0.0.0-1.x86_64.rpm



```

#### migrate 이후에 table확인해보자


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk3Njc0NjA2NCwxMjM0Nzg3NjMsLTE2Mj
Q2ODE0OTAsMTYyNTc3OTUyOCwxNzUyODU4NDcsMTc1NzAyNjUw
MCwtMzg4NjA4NjE3LC0xODExNjk2MTIzLC0xMjk0Mzk1MDIyLD
E0NTI4NTI2MjcsMTAwMjUwODU4NCwxNzgyMTEwMzQwLC0xODM5
MzQ4MzMwLDI3MDMzODcyOCwxMTk0MjI2NDA5LDE1ODU3MTQ1Mi
wtMTg5OTUwMzEzMSwtMTk4MTgxMTI4NiwtMTM5OTAyMTM1Mywx
MTQ5NDA3NzUzXX0=
-->