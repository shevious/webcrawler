# 전달사항
## 2020-01-03
울산_강좌정보 : organIdx, idx 중복되는 데이터가 31024건
ex) page만 틀림.
http://www.uill.or.kr/UR/info/lecture/view.do?rbsIdx=34&page=2953&organIdx=103&idx=L0027338
http://www.uill.or.kr/UR/info/lecture/view.do?rbsIdx=34&page=2954&organIdx=103&idx=L0027338
http://www.uill.or.kr/UR/info/lecture/view.do?rbsIdx=34&page=2955&organIdx=103&idx=L0027338
http://www.uill.or.kr/UR/info/lecture/view.do?rbsIdx=34&page=2957&organIdx=103&idx=L0027338
http://www.uill.or.kr/UR/info/lecture/view.do?rbsIdx=34&page=2956&organIdx=103&idx=L0027338

경북_강좌정보 :  url의 lecIdx만 course_id로 사용 시 중복되는건 240건발생  
ex)   
http://www.gile.or.kr/web/lecture/view.do?mId=72&page=121&organIdx=614000003&lecIdx=2016082500000024  
http://www.gile.or.kr/web/lecture/view.do?mId=72&page=144&organIdx=724600001&lecIdx=2016082500000024  

course_id 중복 처리:  
```py
>>> import hashlib
>>> header='GB'

>>> organIdx='614000003'
>>> lecIdx='2016082500000024'
>>> hash = hashlib.sha1(f'{organIdx}{lecIdx}'.encode('UTF-8')).hexdigest()
>>> hash
'7383a89a7588e80435904ce1f7afcfa49e0ab6e2'
>>> course_id = header + hash[:30]
>>> course_id
'GB7383a89a7588e80435904ce1f7afcf'
>>> course_id_org = header + oraganIdx + "_" + lecIdx
>>>> course_id_org
'GB614000003_2016082500000024'

>>> organIdx='724600001'
>>> lecIdx='2016082500000024'
>>> hash = hashlib.sha1(f'{organIdx}{lecIdx}'.encode('UTF-8')).hexdigest()
>>> hash
'7fcf48bb24f7741bb28ddd23b20804bc388929a7'
>>> course_id = header + hash[:30]
>>> course_id
'GB7fcf48bb24f7741bb28ddd23b20804'
>>> course_id_org = header + oraganIdx + "_" + lecIdx
>>> course_id_org
'GB724600001_2016082500000024'
```

강원_강좌정보 : list페이지가 안뜸  (151, 217, 239)  
ex)  
https://www.e-room.or.kr/gw/portal/org_lecture_info?mode=list&leccode=&page_no=151&selectRegion=&gubun=&studyKind=&searchKeyWord=&searchFromDate=&searchEndDate==  

⇒  **페이지 안뜨는 것은 크롤링에서 제외하도록 고객과 얘기하겠습니다.**  

강원 강좌정보 194페이지 [강좌정보 등록 테스트] 상세안나옴
https://www.e-room.or.kr/gw/portal/org_lecture_info?mode=read&leccode=2&page_no=194&selectRegion=&gubun=&studyKind=&searchKeyWord=&searchFromDate=&searchEndDate=

⇒  **상세 안나오는 것도 크롤링에서 제외하도록 고객과 얘기하겠습니다.** 

## 2019-12-31
경북_기관정보 INST_ID길이가 GB들어가면 16BYTE초과
http://www.gile.or.kr/web/organ/view.do?mId=71&organIdx=2019032800000178

강원_기관정보 기관소개에 FUNCTION들어가있는부분
https://www.e-room.or.kr/gw/portal/org_info?mode=read&orgcode=2199&page_no=24&selectRegion=&keyword=

울산_기관정보 화면안나오는 페이지
https://www.uill.or.kr/UR/info/organ/info.do?rbsIdx=35&organIdx=3258

# 변경사항

## 2019-12-24

1. table 변경
```sql
drop table crawl_inst_info;
drop table crawl_course_info;
drop table django_migrations;
```
신규 테이블 생성  스크립트:
`course_table.sql`  
`inst_table.sql`  
`con_log_table.sql`  
makemigration과 migration 필요 없음.   

2. task loglevel 변경됨 
`celery.py`   
```py
    configure_logging({'LOG_LEVEL': 'DEBUG'}) # scrapy 로그 레벨 설정
```

3. db에 update방식으로 변경  
기존에 course_id가 있는 경우 update하도록 변경됨.  
기존에 inst_id가 있는 경우 update하도록 변경됨.  
github.com/shev

# http://ownloads/windows/  
[Windows x86-64 executable installer](https://www.python.org/ftp/python/3.8.0/python-3.8.0-amd64.exe)  

설치 시:  
Install now  
 - [x] Add Python 3.8 to Path
 - Disable Path Length LImit 버튼 클릭

## 이슈사항

1. 경북 course_id 길이 문제

	예) git bash

https://www.gile.or.kr/web/lecture/view.do?mId=72&page=1&organIdx=2019111800000001&lecIdx=2019120900000002  
	leclid만 강좌id로 보내주세요. 

# To-do list

1. crawlproj 테스트 (완료)
2. `crawler/models.py`에 inst용 db 추가 (완료)
3. url에서 강좌id 기관 id추출 및 저장 (진행중)
4. 강좌정보 메타데이터 db저장
5. 기관정보 메타데이터 db저장
6. 강좌유형 코드

# crawlproj

## 설치

```bash
# ocacle client windows 설치(아래 내용 참고)
# virtualenv 사용
(venv)
# 작업 폴더 이동
cd workspace
# 프로젝트 복사
git clone http://ious/crawlproj.git
cd crawlproj/crawlproj
# 필요한 python 패키지 설치
pip install -r requirements.txt

# db ip 주소/id/password 설정
crawproj/settings.py

# db 생성 script 만들기 (필요없음)
#./manage.py makemigrations crawler

# db 생성 (oracle) (필요없음)
#./manage.py migrate --database=oracle crawler
# local file db 생성 (db.sqlite3 파일)
./manage.py migrate


# sample ulsan taks실행
./manage.py crawl
```

## database 초기화

oraclegitforwindows.org/  

설치 시:
 - [x] checkout as-is, commit as-is
 - [x] Use Window's default console window
 - [x] Enable Symbolic links sh
# 

# git bash

## openssh server windows

[Windows Server 2019 및 Windows 10용 OpenSSH 설치](https://docs.microsoft.com/ko-kr/windows-server/administration/openssh/openssh_install_firstuse)  

[Setting to use git-bash as default shell when connecting remotely via OpenSSH to Windows Server 2016](https://superuser.com/questions/1332346/setting-to-use-git-bash-as-default-shell-when-connecting-remotely-via-openssh-to)  

powershell:

```sql
drop table TBTNS_COURSE_INFO_TRANS;
drop table TBTNS_INSTITUTE_INFO_TRANS;
drop table TBTNS_CON_LOG;
```
local db: (optional)  
`db.sqllite3`파일 삭제  
`./manage.py migrate`  실행

# GIT

github 계정 생성  
id 송부 

https://github.com/shevious/crawlproj/invitations  

## git 사용법
:
```bash
#owsCapability -Online | ? Name -like 'OpenSSH*'


# Install the OpenSSH Server
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

Start-Service sshd
# 프로젝트 복사
git clone https://github.com/shevious/crawlproj.git
# remote origin 확인
git remote -v

# 상태
git status

# 사용자 정보 등록
git config user.email "shevious@yahoo.com"
git config user.name shevious

git add <filename>
git commit -m "커밋 내용"

# 서버에 업로드
git puOPTIONAL but recommended:
Set-Service -Name sshd -StartupType 'Automatic'
# Confirm the Firewall rule is configured. It should be created automatically by setup. 
Get-NetFirewallRule -Name *ssh
*
# 서버의 update 다운로드
git pull
```
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
 - Disable Path Length LImit 버튼 클릭There should be a firewall rule named "OpenSSH-Server-In-TCP", which should be enabled
# If the firewall does not exist, create one
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22

## git bash

https://gitforwindows.org/  

설치 시:
 - [x] checkout as-is, commit as-is
 - [x] Use Window's default console window
 - [x] Enable Symbolic links를 default 값으로
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Program Files\Git\bin\bash.exe" -PropertyType String -Force
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
vi ~/venv/Scripts/activate
#VIRTUAL_ENV="C:\Users\shevious\venv"
VIRTUAL_ENV="/c/Users/shevious/venv"
source venv/Scripts/activate
# command
venv\Scripts\activate.bat

# virtualenv 나가기
deactivate
```

## ~~visual studio 설치~~ (설치 필요없음)

## ocacle client windows

[Instant Client Downloads for Microsoft Windows (x64) 64-bit](https://ww.oracle.com/database/technologies/instant-client/winx64-64-downloads.html#ic_winx64_inst)  
Basic Package 다운로드  
zip압축 해제 `C:\oracleistantclient_19_5`  

PATH에 등록  
제어판 => 시스템 및 보안 => 시스템 => 고급 시스템 설정  =>  
환경변수 => 사용자 환경변수 => PATH에 `C:\oracle\instantclient_19_5` 추가
저장후 `cmd`나 `git bash` 재시작path 에 등록

## pip 사용방법

```
pip list
```

## scrapy 설치

tswwtdod.uci.edu/~gohlke/pythonlibs/  
download `Twisted-19.10.0-cp38-cp38-win_amd64.whl `
https://download.lfd.uci.edu/pythonlibs/t7epjj8p/Twisted-19.10.0-cp38-cp38-win_amd64.whl  

virtualenv에서  
```bash
curl -LO https://download.lfd.uci.edu/pythonlibs/t7epjj8p/Twisted-19.10.0-cp38-cp38-win_amd64.whl  
pip install Twisted-19.10.0-cp38-cp38-win_amd64.whl
p install apy
pip install dateparser
#

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

울산
http://www.uill.or.kr/UR/info/lecture/list.do?rbsIdx=34&page=1  

울산 작업분:  
http://gofile.me/2P1jS/xgKiuo8al  

경북  경북
http://www.gile.or.kr/web/lecture/list.do?mId=72&page=1  
 
강원  
강좌 목록:  
https://www.e-room.or.kr/gw/portal/org_lecture_info  
상세:  
https://www.e-room.or.kr/gw/portal/org_lecture_info?mode=read&leccode=4647&page_no=1&selectRegion=&gubun=&studyKind=&searchKeyWord=&searchFromDate=&searchEndDate=  
기관목록:  

2019-12-16작업분(강원):  
http://gofile.me/2P1jS/3rRqhWb6V  


# portia

### portia sample site

http://52.78.43.27:9001

### basics

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

## pycharm project

file⇒ settings⇒ project⇒ project interpreter ⇒ existing ...
venv안에 있는 python.exe 추가

`sc.py`

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

# 테이블 목록
SELECT * FROM USER_OBJECTS WHERE OBJECT_TYPE='TABLE' ORDER BY CREATED asc;
describe django_session;

# hr 유저 사용하기
alter user hr account unlock;
alter user hr identified by hr; /* 비밀번호: hr */
connect hr;
# or
# rlwrap sqlplus hr/hr@localhost/xe

# drop tables
drop table DJANGO_CELERY_BEAT_CLOCKEDD0E8 CASCADE CONSTRAINT;
drop table DJANGO_CELERY_BEAT_SOLARSC1DCE CASCADE CONSTRAINT;
drop table DJANGO_CELERY_BEAT_PERIODI50C5;
drop table DJANGO_CELERY_BEAT_PERIODI5B67;
drop table DJANGO_CELERY_BEAT_INTERVAC469;
drop table DJANGO_CELERY_RESULTS_TASK0CC3;
drop table DJANGO_SESSION;
drop table DJANGO_ADMIN_LOG;
drop table AUTH_USER_GROUPS;
drop table AUTH_USER_USER_PERMISSIONS;
drop table AUTH_GROUP_PERMISSIONS;
drop table AUTH_PERMISSION;
drop table DJANGO_CONTENT_TYPE;
drop table AUTH_GROUP;
drop table AUTH_USER;
drop table DJANGO_MIGRATIONS;


# timezone
alter database set time_zone='+09:00';
ALTER SESSION SET NLS_DATE_FORMAT = 'DD-MON-YYYY HH:MI:SS PM';  
ALTER SESSION SET NLS_DATE_FORMAT = 'DD-MON-YYYY HH24:MI:SS';
/* docker 재기동 */
select dbtimezone from dual;


```


## django 1.11

cx_oracle 버전 문제:  
https://code.djangoproject.com/ticket/29759  
```bash
pip install django==1.11.26
pip install cx_oracle==6.4.1
django-admin.py startproject myproj
cd myproj
./manage.py migrate
# ⇒ migrate 성공

./manage.py startapp myapp

./manage.py createsuperuser
```
https://deelp.oralcom/sl/siie-dangohtl  

`myproj/requirements.txt`
```
django==1.11.26
django-timezone-field==2.1
celery==4.3.0
cx-oracle==6.4.1
celery -A myproj beat -l info --scheduler django-_celery-results==1.1.2
django-celery-beat==1.5.0
```
```bash
pip install -r requirements.txt
pip install pypiwin32==223 # 윈도우에서만 필요함.
```
`myproj/settings.py`
```py
ALLOWED_HOSTS = ['*']

broker_dir = os.path.join(BASE_DIR, 'broker')

CELERY_BROKER_URL = 'filesystem://'
CELERY_BROKER_TRANSPORT_OPTIONS = {
    "data_folder_in": os.path.join(broker_dir, "out"),
    "data_folder_out": os.path.join(broker_dir, "out"),
    "data_folder_processed": os.path.join(broker_dir, "processed"),
}

import os
for f in [CELERY_BROKER_TRANSPORT_OPTIONS['data_folder_in'],
          CELERY_BROKER_TRANSPORT_OPTIONS['data_folder_processed']]:
    if not os.path.exists(f):
        os.makedirs(f)_beat.schedulers:DatabaseScheduler

```
https://developer.oracle.com/dsl/vasiliev-django.html  

`myproj/settings.py`
```py
USE_TZ = True
TIME_ZONE = 'Asia/Seoul'
CELERY_RESULT_BACKEND = 'django-db'


INSTALLED_APPS = [
    ...,
    'django_celery_results',
    'django_celery_beat',
    'myapp.apps.MyappConfig',
]

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.oracle',
        'NAME': 'xe',
        'USER': 'hr',
        'PASSWORD': 'hr',
        'HOST': 'localhost',
        'PORT': '1521',
    }
}

# 타임존 변경
#TIME_ZONE = UTC
TIME_ZONE = 'Asia/Seoul'
```
`myproj/__init__.py`
```py
from __future__ import absolute_import, unicode_literals
  
# This will make sure the app is always imported when
# Django starts so that shared_task will use this app.
from .celery import app as celery_app

__all__ = ('celery_app',)
```
`myproj/celery.py`
```py
from __future__ import absolute_import, unicode_literals
import os
from celery import Celery

# set the default Django settings module for the 'celery' program.
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'myproj.settings')

app = Celery('myproj',
             #broker='amqp://',
             #backend='amqp://',
            )

# Using a string here means the worker doesn't have to serialize
# the configuration object to child processes.
# - namespace='CELERY' means all celery-related configuration keys
#   should have a `CELERY_` prefix.
app.config_from_object('django.conf:settings', namespace='CELERY')

# Load task modules from all registered Django app configs.
app.autodiscover_tasks()

@app.task(bind=True)
def debug_task(self):
    print('Request: {0!r}'.format(self.request))
```
`myapp/tasks.py`
```py
# Create your tasks here
from __future__ import absolute_import, unicode_literals
from celery import shared_task

@shared_task
def add(x, y):
    return x + y

@shared_task
def mul(x, y):
    return x * y

@shared_task
def xsum(numbers):
    return sum(numbers)
```
```bash
# celery worker 기동
cd myproj
# 윈도우용
celery -A myproj worker -l info --pool=solo
# linux용
celery -A myproj worker -l info

# celery beat 데몬 기동
celery -A myproj beat -l info --scheduler django_celery_beat.schedulers:DatabaseScheduler

# django 서버
./manage.py runserver 0.0.0.0:8000
```

django admin  
http://192.168.33.10:8000/admin/  
clocked (시작 시간 등록)  
periodic task 등록




## openssl 

cipher list
https://www.openssl.org/docs/man1.0.2/man1/ciphers.html  

## rabbitmq

`/home/vagrant/rabbitmq.conf`
```
#listeners.tcp.1 = 0.0.0.0:15672 # not working for brew rabbitmq-server
#loopback_users = none # comment out for guest/guest login
```
기본 포트: 15672  ==> 방화벽 등록
```bash
#celery broker 서버 기동
# see /home/linuxbrew/.linuxbrew/Cellar/rabbitmq/3.8.2/sbin/rabbitmq-server file
RABBITMQ_NODE_IP_ADDRESS=0.0.0.0 \
RABBITMQ_CONFIG_FILE=/home/vagrant/rabbitmq.conf \
rabbitmq-server -detached
or
rabbitmq-server
```


## 작업중

#### celery broker filesystem

[Using filesystem transport with Celery](https://ondergetekende.nl/using-filesystem-transport-with-celery.html)  
[An incredibly simple no-frills Celery setup](https://www.distributedpython.com/2018/07/03/simple-celery-setup/)  

```py
#CELERY_BROKER_URL = 'amqp://kotech:kotech@13.209.192.128'
# This assumes you have defied BASE_DIR, which is the case if you're using 
# a generated project. If not, just set it to wherever you think
broker_dir = os.path.join(BASE_DIR, 'broker')

CELERY_BROKER_URL = 'filesystem://'
CELERY_BROKER_TRANSPORT_OPTIONS = {
    "data_folder_in": os.path.join(broker_dir, "out"),
    "data_folder_out": os.path.join(broker_dir, "out"),
    "data_folder_processed": os.path.join(broker_dir, "processed"),
}

import os
for f in [CELERY_BROKER_TRANSPORT_OPTIONS['data_folder_in'],
          CELERY_BROKER_TRANSPORT_OPTIONS['data_folder_processed']]:
    if not os.path.exists(f):
        os.makedirs(f)
```

#### celery on windows

[Hack: 2 Ways to make Celery 4 run on Windows](https://www.distributedpython.com/2018/08/21/celery-4-windows/)  
Celery 4 does no longer support Windows. Here are two workarounds  


#### oracle instant client on ubuntu

https://www.oracle.com/database/technologies/instant-client/linux-x86-64-downloads.html  

```bash
sudo apt install alien -y

wget https://download.oracle.com/otn_software/linux/instantclient/195000/oracle-instantclient19.5-basic-19.5.0.0.0-1.x86_64.rpm
sudo alien --scripts oracle-instantclient19.5-basic-19.5.0.0.0-1.x86_64.rpm
sudo dpkg -i oracle-instantclient19.5-basic_19.5.0.0.0-2_amd64.deb

#brew install libaio

# client zip

wget https://download.oracle.com/otn_software/linux/instantclient/195000/instantclient-basic-linux.x64-19.5.0.0.0dbru.zip

mkdir -p $HOME/local/oracle
cd $HOME/local/oracle
unzip ~/instantclient-basic-linux.x64-19.5.0.0.0dbru.zip

export LD_LIBRARY_PATH=$HOME/local/oracle/instantclient_19_5:$LD_LIBRARY_PATH

# sqlplus
wget https://download.oracle.com/otn_software/linux/instantclient/195000/oracle-instantclient19.5-sqlplus-19.5.0.0.0-1.x86_64.rpm
sudo alien --scripts oracle-instantclient19.5-sqlplus-19.5.0.0.0-1.x86_64.rpm
sudo dpkg -i oracle-instantclient19.5-sqlplus_19.5.0.0.0-2_amd64.deb
#sudo apt install libaio1 -y

# sqlplus zip
wget https://download.oracle.com/otn_software/linux/instantclient/195000/instantclient-sqlplus-linux.x64-19.5.0.0.0dbru.zip

# centos 6.5에서 GLIBC_2.14 없음 오류가 남.
# glibc_2.14 설치
wget http://ftp.gnu.org/gnu/glibc/glibc-2.14.tar.gz
tar zxvf glibc-2.14.tar.gz
cd glibc-2.14
mkdir build
cd build
../configure --prefix=$HOME/local/glibc-2.14
make -j4
make install
export LD_LIBRARY_PATH=$HOME/local/glibc-2.14:$LD_LIBRARY_PATH



stty erase ^H
sqlplus system/oracle@localhost/xe
#or
brew install rlwrap
rlwrap sqlplus system/oracle@localhost/xe

# optional
wget https://download.oracle.com/otn_software/linux/instantclient/195000/oracle-instantclient19.5-devel-19.5.0.0.0-1.x86_64.rpm

```

#### migrate 이후에 table확인해보자

#### scrapy from django

https://blog.theodo.com/2019/01/data-scraping-scrapy-django-integration/  
https://medium.com/@ali_oguzhan/how-to-use-scrapy-with-django-application-c16fabd0e62e  
djangoItem:  
https://docs.scrapy.org/en/0.24/topics/djangoitem.html  
https://github.com/scrapy-plugins/scrapy-djangoitem 
egg
https://stackoverflow.com/questions/47286690/how-do-i-create-and-load-an-egg-file-in-python  
https://bluese05.tistory.com/31  


# 참고용

##```




## django 3 (oracle 11g안됨)
`myproj/settings.py`
```py
INSTALLED_APPS = [
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

# crawlproj creation

```bash
git clone https://github.com/shevious/crawlproj.git
cd crawlproj
django-admin.py startproject crawlproj
cp ~/workspace/webstudy/django/.gitignore .
cd crawlproj
./manage.py startapp crawler
cp -r ~/workspace/webstudy/django/djangocelery/crawler .
cp ~/workspace/webstudy/django/djangocelery/djangocelery/settings.py crawlproj/settings.py
# change djangocelery => crawlproj
cp ~/workspace/webstudy/django/djangocelery/djangocelery/celery.py crawlproj
cp ~/workspace/webstudy/django/djangocelery/djangocelery/dbrouter.py crawlproj
cp -r ~/workspace/webstudy/django/djangocelery/Ulsan .

# for test and running
cp ~/workspace/webstudy/django/djangocelery/scrapy.cfg .
cp ~/workspace/webstudy/django/djangocelery/supervl 

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
#brew install libaio

# sqlplus
wget https://download.oracle.com/otn_software/linux/instantclient/195000/oracle-instantclient19.5-sqlplus-19.5.0.0.0-1.x86_64.rpm
sudo alien --scripts oracle-instantclient19.5-sqlplus-19.5.0.0.0-1.x86_64.rpm
sudo dpkg -i oracle-instantclient19.5-sqlplus_19.5.0.0.0-2_amd64.deb
sudo apt install libaio1 -y

stty erase ^H
sqlplus system/oracle@localhost/xe
#or
brew install rlwrap
rlwrap sqlplus system/oracle@localhost/xe

# optional
wget https://download.oracle.com/otn_software/linux/instantclient/195000/oracle-instantclient19.5-devel-19.5.0.0.0-1.x86_64.rpm

```

#### migrate 이후에 table확인해보자

#### scrapy from django

https://blog.theodo.com/2019/01/data-scraping-scrapy-django-integration/  
https://medium.com/@ali_oguzhan/how-to-use-scrapy-with-django-application-c16fabd0e62e  
djangoItem:  
https://docs.scrapy.org/en/0.24/topics/djangoitem.html  
https://github.com/scrapy-plugins/scrapy-djangoitem 
egg
https://stackoverflow.com/questions/47286690/how-do-i-create-and-load-an-egg-file-in-python  
https://bluese05.tistordy.conf .
# change djangocelery => crawlproj
```m/31  
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg4MTI0NjkzLC02MjExNDA4NzIsMjE0NT
UwNDU1OCwtNzkwNDM0MzM2LC0xNDU5MzI1NjkwLDExNzEwNDgy
MDgsMTc5NjgwMzkxLC02MjY0NTY1NjgsMTUyNTQ0MjY2MiwxMz
c2Njg5ODA5LDUwNDY0NjMwOSwxNDMxNTM1OTIxLC02Mzc2NDQ4
ODIsMTE0MzYxNjcxNiw2MTIzNzIzMTIsMTk2MzAwMjgyMCwxMD
Q1MDcwMDg1LC0xMjcxMTI2Njc5LDE4Njc4NDQxOTUsLTEyMTM2
MTk4OTJdfQ==
-->