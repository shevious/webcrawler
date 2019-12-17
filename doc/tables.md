

# 웹 크롤러 테이블 정의서


## 강좌 정보

|FIELD_NAME|COMMENT|비고|
|------|----|-----|
|COURSE_ID|강좌아이디| |
|INST_ID|기관아이디| 기관명? |
|TOTAL_CD|토탈코드| ? |
|SIDO_CD|시도코드| ? |
|SIGUNGU_CD|시군구코드| ? |
|COURSE_NM|강좌명| |
|COURSE_DESC_URL|강좌설명URL| |
|COURSE_PTTN_CD|강좌유형코드| 온라인/오프라인? |
|EXTRA_CHARGE_CONTENT|부대비용내용|X|
|EDU_CYCLE_CONTENT|교육주기내용| 3주? |
|EDU_QUOTA_CNT|교육인원수| |
|COURSE_START_DT|강좌시작일시| |
|COURSE_END_DT|강좌종료일시| |
|RECEIVE_START_DT|접수시작일시| |
|RECEIVE_END_DT|접수종료일시| |
|EDU_TM|교육시간설명| ? |
|EDU_LOCATION_DESC|교육장소설명| |
|INQUIRY_TEL_NO|문의전화번호| |
|TEACHER_PERNM|강사설명| X |
|INFO_MNG_INST_ID|정보관리기관아이디| X |
|INFO_INP_INST_ID|정보입력기관아이디| X |
|REG_USER_ID|등록회원아이디| X |
|REG_DT|등록일시| 날짜만? 시간은? |
|UPD_USER_ID|수정자아이디| X |
|UPD_DT|수정일시| |
|TAG|태그| |
|JOB_ABILITY_COURSE_YN|직업능력강좌여부| |
|CB_EVAL_ACCEPT_YN|학점은행제평가인정여부| |
|ALL_EVAL_ACCEPT_YN|평생학습계좌제평가인정여부| |
|LANG_CD|언어코드| |
|STUDY_OS_NM|학습운영제제명| |
|STUDY_WEB_BROWSER_NM|학습웹브라우저명| |
|STUDY_DEVICE_NM|학습장치명| |
|VSL_HANDICAP_SUPP_YN|시각장애지원여부| |
|HRG_HANDICAP_SUPP_YN|청각장애지원여부| |
|COURSE_CLASS1_CD|강좌분류1코드| |
|COURSE_CLASS2_CD|강좌분류2코드| |
|COURSE_THUMBNAIL_URL|강좌썸네일URL| |
|EDU_TARGET_CD|교육대상코드| |
|ENROLL_APPL_METHOD_CD|수강신청방법코드| |
|EDU_METHOD_CD|교육방법코드| |
|EDU_LVLDFF_TYPE_CD|교육난의도구분코드| |
|REF_BOOK_NM|참고도서명| |
|SOURCE_DESC|출처설명| X |
|LINK_URL|링크URL| |
|DEL_YN|삭제여부| N |
|COURSE_URL|강좌URL| |
|COURSE_URL_CALL_METHOD|강좌URL호출방법코드| |
|MOBILE_URL|모바일URL| |
|MOBILE_URL_CALL_METHOD|모바일URL호출방법코드| |
|COURSE_DESC|강좌설명| |
|ENROLL_AMT|수강금액| |
|PAGE_CNT|카운팅 페이지 개수| |
|PAGE_NO|페이지 번호| |
|TOTAL_CNT|총 강좌 개수| |

## 기관 설명

|FIELD_NAME|COMMENT|NULL 여부|
|----|----|----|
|INST_ID|기관아이디|NOT NULL|
|TOTAL_CD|토탈코드| |
|SIDO_CD|시도코드| |
|SIGUNGU_CD|시군구코드| |
|INST_NM|기관명| |
|INST_CEO_PERNM|기관대표자성명| |
|INST_SET_UP_MAIN_AGENT_CD|기관설립주체코드| |
|INST_OPERATION_FORM_CD|기관운영형태코드| |
|ZIPCODE|우편번호| |
|ADDR1|주소1| |
|ADDR2|주소2| |
|STREET_CD|도로코드| |
|STREET_NM|도로명| |
|BUILDING_NO|건물번호| |
|DETAIL_ADDR|상세주소| |
|MANAGER_PERNM|담당자성명| |
|TEL_NO|전화번호| |
|FAX_NO|팩스번호| |
|EMAIL|이메일| |
|HOMEPAGE_URL|홈페이지URL| |
|INST_DESC|기관설명| |
|ESTABLISHMENT_DT|설립일시| |
|INST_OPERATION_STATUS_CD|기관운영상태코드| |
|LONGITUDE_VAL|경도값| |
|LATITUDE_VAL|위도값| |
|INFO_MNG_INST_ID|정보관리기관코드| |
|INFO_INP_INST_ID|정보입력기관코드| |
|TAG|태그| |
|LOC_LEIC_APPNT_YN|지역평생교육정보센터지정여부| |
|LIFE_STUDY_CENTER_APPNT_CD|평생학습관지정코드| |
|INCUMBENTTRAIN_INST_YN|직업능력개발훈련기관여부| |
|CB_INST_YN|학점은행제평가인정기관여부| |
|LFLLR_INST_YN|평생학습센터지정기관여부| |
|PSDC_APPNT_INST_YN|학부모지원센터지정기관여부| |
|BASIC_LIT_EDU_YN|기초문해교육여부| |
|ACHV_SPPL_EDU_YN|학력보완교육여부| |
|JOB_ABILITY_EDU_YN|직업능력교육여부| |
|CULTURE_ART_EDU_YN|문화예술교육여부| |
|HUMAN_RFNMNT_EDU_YN|인문교양교육여부| |
|CITIZEN_JOIN_EDU_YN|시민참여교육여부| |
|INST_CLASS1_CD|기관분류1코드| |
|INST_CLASS2_CD|기관분류2코드| |
|INST_CLASS3_CD|기관분류3코드| |
|REG_USER_ID|등록자아이디| |
|REG_DT|등록일시| |
|UPD_USER_ID|수정자아이디| |
|UPD_DT|수정일시| |
|DEL_YN|삭제여부| |
|PAGE_CNT|카운팅 페이지 개수| |
|PAGE_NO|페이지 번호| |
|TOTAL_CNT|총 기관 개수| |

#  울산

## 기관 정보

![enter image description here](https://github.com/shevious/webcrawler/blob/master/screenshot/ulsan-inst.png?raw=true)

## 강좌 정보

![enter image description here](https://github.com/shevious/webcrawler/blob/master/screenshot/ulsan-course.png?raw=true)
# 경북

## 기관 정보
![enter image description here](https://github.com/shevious/webcrawler/blob/master/screenshot/gyeongbug-inst.png?raw=true)
## 강좌 정보
![enter image description here](https://github.com/shevious/webcrawler/blob/master/screenshot/gyeongbuk-course.png?raw=true)

# 강원

## 기관 정보
![enter image description here](https://github.com/shevious/webcrawler/blob/master/screenshot/gangwon-inst.png?raw=true)
## 강좌 정보

![enter image description here](https://github.com/shevious/webcrawler/blob/master/screenshot/gagnwon-course.png?raw=true)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTcxMDE1NTU2NCwtNzMwNDYwMTQwLC00OD
QyMTUyMDgsMTI0MzYxNzc4Nyw0NDAyMDQwMTNdfQ==
-->