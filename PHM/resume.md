
# 박형민 | 성장하는 즐거움

<img width="200" alt="Screen Shot 2021-12-30 at 2 43 45 AM" src="https://user-images.githubusercontent.com/42319300/155941568-dd34b2a6-7d5b-47a5-8046-d2b55c341150.jpg">

📧 **이메일** : **thalsal@naver.com**

📬 **Phone  : 010-4147-1796**

**✏️ 블로그 : [힘차게, 열심히 공대생! 블로그](https://thalals.tistory.com/)**

📓 **Github** : **[Park Hyeongmin](https://github.com/thalals)**


<br>


## 안녕하세요, 개발자 박형민입니다!

- 취미는 운동! 특기는 기록입니다!

  하루하루 쌓아가는 가치를 가장 중요하게 생각합니다!

  
    💡 My Tech Blog : [힘차게, 열심히 공대생! 블로그](https://thalals.tistory.com/)



- 5년뒤,  명확한 한 사람의 역할을, 동료가 기댈 수 있는 개발자가 되기위해 노력중입니다!

- “이거 너가 만들었어?”의 **“너”** 이고 싶은 개발자입니다.
  사용자가 만족하며 사용하는 서비스를 만드는 것을 목표로 나아가는 중입니다!

<br>

## 🖥️ 팀/개인 프로젝트

### 🐶 강.만.다(강아지를 만나다)

2021.11.19 ~ 2021.12.31(5주, 4명)

**프로젝트 설명**
 - 반려견을 키우는 반려인들을 위한 커뮤니티 사이트

**주요기능**

- 게시판에 글을 남기고, 댓글로 소통 / 유저들의 반려동물들 자랑
- 사용자가 만남을 원하는 지역을 등록하면, 반려인들을 위한 장소 추천(KaKao Map Api)

**내가 담당한 기능**

- JPA Pageable 서브쿼리 이용해 외부참조 엔티티 Size로 정렬
- 만남 희망 장소 주위, 카테고리 별 장소 추천 기능 구현
- AWS EB(Elastic Beanstalk) 백엔드 배포
- RDS(MySql) 연동
- Git Action을 이용한 무중단 서비스 배포
- AWS ECR/Docker 스크립트를 이용한, 배포 버전 관리
- 게시글(posts) 카테고리 CRUD
- 좋아요, 댓글, 검색, 페이지네이션

**기술 스택**

- 어플리케이션 API 서버 : Spring Boot / Mysql / JPA(Spring Data JPA, Fomula) / Java 8
- DevOps : GitActions(CI/CD), AWS(EC2, S3, RDS, Eb), Docker
- Open Api
    - KaoKao Map Api : 지도, 카테고리 검색
    - Daum Api : 도로명 주소 검색
- API 문서 관리 : Swagger
- 프로젝트 관리 : Git issue, Git Project

<img src="https://img.shields.io/badge/Github-%230A0A0A.svg?&style=flat-square&logo=Github&logoColor=white"> [Project: 강만다](https://github.com/thalals/MaruMaru_sparta_ver.Spring)

<br>


### 🌍 안전보행길 탐색 지도 (학술제 대상 수상작 ✨)

2021.01 ~ 2021.07(약 6달, 1인 졸업작품 - 학업 중 프로젝트 진행)

**프로젝트 설명**
 - 어두운 밤, 가족들이 “조금더 안전하게 거리를 다니면 좋겠다” 라는 생각에서 시작했습니다.

사용자에게 최단경로와 안전경로를 제공하는 Django 프로젝트입니다.

**구현한 기능**

- 경로 탐색 범위, 육각형 2차원 맵 구현
- 위치평가 값 수정 후, Astar 알고리즘을 사용해 안정경로 탐색
- 최단경로와, 안전경로의 거리 및 보행 시간을 사용자에게 제공
- 데이터는 공공데이터 포털, 경기도 데어터셋, 도로명주소 전자지도를 이용

**기술 스택**

- 어플리케이션 API 서버 : Django / Mysql / Python
- Data 추출 : QGIS - 도로명 주소 shp 파일 (Line to Point)
- Open Api
    - Daum Api : 도로명 주소 검색
    - Tmap Api : 최단경로
- Library
    - Leaflet.js : Js 기반 지도 라이브러리
    - hexgrid-py : 실제 좌표 기준, 육각형 타일 구축
    - geocoder : 현재 사용자 위치 추출
    - haversine : 실제 좌표간 거리 측정

<img src="https://img.shields.io/badge/Github-%230A0A0A.svg?&style=flat-square&logo=Github&logoColor=white"> [Project: 안전보행길 탐색지도](https://github.com/thalals/SafetyMap-Graduation-Project)

<br>


## 💁🏻대외 활동

**대학생 멋쟁이사자처럼 8기** (2020.03 ~ 2020.10)

- 순천향 대학교 멋쟁이사자차럼 멤버로 활동
- Git, Github, Bootstrap, Django에 대한 스터디 및 프로젝트 진행
- 롯데&대학생 멋쟁이사자차럼 해커톤 은상 수상

<img src="https://img.shields.io/badge/Github-%230A0A0A.svg?&style=flat-square&logo=Github&logoColor=white"> [Project: 바로바롯](https://github.com/thalals/Project_barobarot)

<br>


## 🏫 교육 이력

**스파르타코딩클럽 내일배움캠프** (2021.09 ~ 2022.01)

- 교육내용 : Java/Spring 백엔드 개발자 과정
    - Flask, Mongodb - 1차 POC 프로젝트 진행
    - Spring Boot, JPA, Mysql - 2차 프로젝트 진행 (Flask 프로젝트를 Spring으로 Converting)
    - DevOps - AWS, GitActions, Docker
- 대표 프로젝트 : 반려인을 위한 웹 커뮤니티 강.만.다 프로젝트([https://github.com/thalals/MaruMaru_sparta_ver.Spring](https://github.com/thalals/MaruMaru_sparta_ver.Spring))

**순천향대학교 컴퓨터소프트웨어공학과 졸업 예정** (2016.03 ~ 2022.02)

- 2021 SCH SW 졸업 학술제 대상 수상
- 2020 3학년 학과대표

<br>


## 💡 자격 정보

### 정보처리기사

- 취득 일자 : 2021.08
- 발행 기관 : 한국산업인력공단
- 공부법 : 4학년 1학기 학업 병행하며, 자격증 취득

### 네트워크 관리사 2급

- 취득 일자 : 2018.12
- 발행 기관 : 한국정보통신자격협회
- 공부법 : 군 복무 중, IT관련 자격증 취득 기회가 생겨, 밤새 연등을해가며 필기와 실기 모두 복무 중 합격

<br>


## 🔫 병역

2017.09.04 ~ 2019.05.27 육군, 통신 만기전역
