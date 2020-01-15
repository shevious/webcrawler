
# 늘배움 크롤러 운영자 매뉴얼

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

`http://203.235.44.154:18000/admin`


![enter image description here](https://github.com/shevious/webcrawler/blob/master/screenshot/adminmain.png?raw=true)
### 데몬 기동 시간 설정

Periodic Tasks ⇒ Crontabs ⇒ Crontab 추가 혹은 변경

![enter image description here](https://github.com/shevious/webcrawler/blob/master/screenshot/admincron.png?raw=true)
- Minutes: 0분  
- Hour: 02시  
- Day(s) of The Week: 0 (일요일)   
- Time Zone: Asia/Seoul  

### 크롤러 목록

![enter image description here](https://github.com/shevious/webcrawler/blob/master/screenshot/admintasklist.png?raw=true)
- ulsan_course: 울산 강좌
- ulsan_inst: 울산 기관
- gangwon_course: 강원 강좌
- gangwon_inst: 강원 기관
- gyeongbuk_course: 경북 강좌
- gyeongbuk_inst: 경북 기관

## 설치 방법 (centos 6.5기준)

1. python 3.7.5 virtualenv 이용
2. 
3. 

## 특이사항 목록

### 2020-01-03

울산_강좌정보 : organIdx, idx 중복되는 데이터가 31024건. page만 틀림.  
ex)  
http://www.uill.or.kr/UR/info/lecture/view.do?rbsIdx=34&page=2953&organIdx=103&idx=L0027338  
http://www.uill.or.kr/UR/info/lecture/view.do?rbsIdx=34&page=2954&organIdx=103&idx=L0027338  
http://www.uill.or.kr/UR/info/lecture/view.do?rbsIdx=34&page=2955&organIdx=103&idx=L0027338  
http://www.uill.or.kr/UR/info/lecture/view.do?rbsIdx=34&page=2957&organIdx=103&idx=L0027338  
http://www.uill.or.kr/UR/info/lecture/view.do?rbsIdx=34&page=2956&organIdx=103&idx=L0027338  


### 2019-12-31

강원_기관정보 기관소개에 FUNCTION들어가있는부분
https://www.e-room.or.kr/gw/portal/org_info?mode=read&orgcode=2199&page_no=24&selectRegion=&keyword=

울산_기관정보 화면안나오는 페이지
https://www.uill.or.kr/UR/info/organ/info.do?rbsIdx=35&organIdx=3258  

### 2020-01-10

울산_기관 :  309건저장. 23건 중복. 1건 상세없음. 총 333건.  
울산_강좌: 15154건 저장. 31024건 중복.   총 46178건.  
경북_기관: 697건 저장. 1건 상세없음. 총 698건.  
ex) 상세data없는페이지  
http://www.gile.or.kr/web/organ/view.do?mId=71&page=20&organIdx=2019032800000283
경북_강좌 : 5429건 저장. 총 5433건이라고 화면에 표시되지만 272page에 가보면 4건이 빠지고 5번부터시작함.
강원_기관: 351건저장. function들어가는 8건제외. 총 359건.
강원_강좌: 4422건 저장. 리스트, 상세안나오는 46건, 중복1건, course_nm에 꺽쇠들어가는부분 scrapy key error 1건. 총 4470건.
ex) course_nm꺽쇠들어가는부분
[https://www.e-room.or.kr/gw/portal/org_lecture_info?mode=read&leccode=4116&page_no=26&selectRegion=&gubun=&studyKind=&searchKeyWord=&searchFromDate=&searchEndDate=](https://www.e-room.or.kr/gw/portal/org_lecture_info?mode=read&leccode=4116&page_no=26&selectRegion=&gubun=&studyKind=&searchKeyWord=&searchFromDate=&searchEndDate=)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzAwNTM1NTQsLTEyODAyNzM3ODEsLTEyOD
Q2MjM1ODUsMTEzMDA5ODY1OSw1OTE3NTQ2MzVdfQ==
-->