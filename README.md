## 파스타 클라우드에 mysql용 스프링프로젝트 배포하기

***
### 파스타 클라우드 활용(공통)
파스타 클라우드 활용.
1. 스프링프로젝트 jangeunhwa-mysql 변경(도메인의 호스트네임으로 사용)
2. 이클립스에서 jangeunhwa-mysql 프로젝트를 파스타에 배포(Hsql용)
3. jangeunhwa-mysq 로컬 mysql서버와 연동처리.
4. 파스타 클라우드에서 Mysql서비스 생성.(원격접속이름과 암호를 확인가능)
5. 원격 phpmyadmin 툴(워크벤치와 비슷)을 파스타 클라우드에 PHP앱 생성 후 배포.
6.jangeunhwa-mysql 프로젝트를클라우드용 DB사용으로 변경 후 파스타에 재배포.
7. jangeunhwa_egov 프로젝트 이름변경: jangeunhwa-egov 파스타에 배포(Mysql클라우드사용)
***
### 20200812(수) 작업내역
- 4. 스프링mysql프로젝트를 로컬Mysql 설정 -> 클라우드 파스타용으로 변경

```
- 3). 작업결과확인: 이클립스에서 파스타서버 더블클릭-> Application and Service 탭에서 -> 오른쪽에 Update and Restart 버튼을 클릭해서 클라우드 배포-수정사항 적용.
- 2). root-context.xml 파일에 DB커넥션 설정을 클라우드용으로 추가
- 1). 메이블 pom.xml 파일에 클라우드용 모듈 추가
```
- 3. 로컬에서 테스트OK된 후 클라우드에 Mysql서비스를 생성

```
- 4). http://jangeunhwa-myadmin.paas-ta.org 접속 후 edu 데이터베이스 생성 및 더미 데이터 입력. 
- 3). 아래 php프로젝트를 파스타에 푸시(manifest.yml사용): 클라우드파운더리 cf cli(커맨드라인인터페이스) 설치.
- 2). 생성된 Mysql 서비스를 웹으로 제어하는 php 프로젝트를 이클립스로 임포트. (jangeunhwa-myadmin)
- 1). 온라인 파스타 클라우드에서 kimilguk-mysql-db 이름의 Mysql 서비스를 생성.
```
- 2. jangeunhwa-mysql 프로젝트를 hsql -> Mysql 변경(아래)

```
- 2). wamp 실행 후 톰캣서버로 확인.
- 1). root-context.xml 수정. (HSQLDB FILE기반, 초기1회 주석처리/ 로컬 mysql log4jdbc 설정후  주석해제)
```
- 1. 어제한 내용 리뷰(아래)
- 파스타 클라우드에 접속할 때 https://api.paas-ta.org 주소사용
- RestAPI 서버가 https://api.paas-ta.org
- RestAPI 서버에 Json 데이터를 보내서, 앱을 생성+실행하게 됨.


```
매니페스트 야믈파일(manifest.yml)
---
applications:
- name: jang03-mysql
  memory: 1024M
  disk_quota: 1024M
  instances: 1
  host: jang03-mysql
  domain: paas-ta.org
```

