# Comcigan-API

> 컴시간알리미 시간표 조회 Java 라이브러리

컴시간알리미(comci.net) 서버가 내려주는 JSON 응답을 웹 페이지를 긁지 않고 직접 파싱해 학교 검색, 일과 시간, 학생·교사 시간표를 Java 객체로 돌려주는 라이브러리다. JitPack으로 배포한다. 2023년에 만들었고, 제천고 코딩 동아리의 교사용 시간표 앱 티플 서버가 이 라이브러리를 쓴다.

## 주요 기능
- 학교 이름으로 검색해 학교 코드·이름·지역을 반환
- 학교별 교시 시작 시각(일과 시간) 조회
- 학생용: 학년·반 기준 교시·일·주간(월~금) 시간표 조회, 원래 시간표와 달라진 교시는 `isModify`와 원래 수업을 함께 반환
- 교사용: 교사 목록 조회, 교사별 주간 시간표(과목·학년-반) 조회

## 기술 스택
| 영역 | 기술 |
|---|---|
| 언어 | Java, Gradle 8.0 |
| 라이브러리 | OkHttp 4.12.0, Gson 2.11.0, Lombok 1.18.34 |
| 인프라 | JitPack |

## 구조
```
src/main/java/com/github/son_daehyeon/
├── ComciganBaseApi.java      학교 검색, 일과 시간, 원본 JSON 요청
├── student/                  ComciganStudentApi, 학생용 시간표 모델
├── teacher/                  ComciganTeacherApi, 교사 목록·교사용 시간표 모델
├── data/School.java          학교 모델
└── util/                     comci.net 요청, EUC-KR·Base64 인코딩
```

## 실행
```groovy
repositories {
    maven { url 'https://jitpack.io' }
}

dependencies {
    implementation 'com.github.son-daehyeon:Comcigan-API:2.0.0'
}
```

```java
ComciganStudentApi.searchSchool("서울");            // [School(code=20449, name=..., location=서울), ...]
ComciganStudentApi.getRange(20449);                 // {1=08:35, 2=09:25, ...}
ComciganStudentApi.getWeeklyTimeTable(20449, 1, 1); // 1학년 1반 월~금 시간표
ComciganTeacherApi.getTeacherList(20449);           // [Teacher(id=1, name=...), ...]
ComciganTeacherApi.getWeeklyTimeTable(20449, 1);    // 교사 id 1의 주간 시간표
```

## 관련 저장소
- [JCHS-Teacher-Plan-Server](https://github.com/son-daehyeon/JCHS-Teacher-Plan-Server) — 이 라이브러리로 시간표를 불러오는 티플 서버

---
2023 · 개인 프로젝트 · 보관됨
