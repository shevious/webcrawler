
# 운영자 매뉴얼

## 업데이트 기록

- 2020-01-15: 최초 작성

## 개요

울산, 강원, 경북 평생학습관의 오프라인 강좌 정보 및 기관 정보를 크롤링하는 모듈

### 크롤링 통계 (누적 건수)

**2020-01-15 기준**

- 울산 기관: 309건
- 울산 강좌: 15154건
- 강원 기관: 351건 
- 강원 강좌: 4422건
- 경북 기관: 697건
- 경북 강좌: 5429건
- 기관 합계: 1357건
- 강좌 합계: 25005건

## 기동 및 중지

`kadm`계정으로 로그인  

-  기동: `/home/kadm/webcrawler/crawlproj/crawlproj/start.sh`
- 중지: `/home/kadm/webcrawler/crawlproj/crawlproj/stop.sh`

## 운영 환경

- python 3.7.5
- Django 1.11
- Oracle 11x

설치 폴더: 

- `/home/kadm/webcrawler`

로그 폴더:  

- celery worker: `/home/kadm/log/celery/worker*.log`
- celear beat: `/home/kadm/log/celery/beat*.log`
- supervisor log:  `/home/kadm/log/supervisor`

## 간이 모니터링 웹도구

### 접속

`http://203.235.44.145:18000/admin`


![enter image description here](https://github.com/shevious/webcrawler/blob/master/screenshot/adminmain.png?raw=true)
### 데몬 기동 시간 설정

Periodic Tasks ⇒ Clocked ⇒ 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyODQ2MjM1ODUsMTEzMDA5ODY1OSw1OT
E3NTQ2MzVdfQ==
-->