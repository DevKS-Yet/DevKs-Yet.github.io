---
title: "2025년 04월 1주"

excerpt: "Week-Summary"

categories:
  - Week-Summary

tags:
  - Week-Summary

---

# 공부한 내용

### 프로젝트 생성 시

- 예전에는 스프링을 빌드할 때 Maven으로 많이 하였으나 지금은 Gradle로 넘어오는 추세.
- Maven과 Gradle은 빌드 라이브러리를 도와주는 툴
- 스프링 버전을 선택 시 M? 또는 SNAPSHOP이 있는 것은 정식 버전이 아님으로 주의
- group 에는 기업명을 적음 (예: net.daum)
- artifact는 해당 프로젝트의 이름 (예: games)

---

### 프로젝트 구조

- gradle -> gradle 설정
- src -> 예전엔 main만 있었지만 지금은 test도 같이 생성되면서 main/test가 표준화. 그만큼 테스트 코드가 중요해졌다는 것을 보여줌
- resource -> 자바 파일을 제외한 모든 것
- build.gradle -> 예전 스프링은 개발자가 여기저기 설정 파일을 생성하고 설정을 했야해서 불친절하였다면 스프링 부트부터는 매우 친화적이다.

---

### Gradle 빌드 방법

- ./gradlew build -> for man
- ./gradle.bat build -> for windows
- 이후에 생성된 jar 파일을 `java -jar ~.jar`로 실행하면 스프링 부트 경우 내장 톰캣이 탑재되어있어서 jar 파일 하나로 웹이 구동됨

---

### API 형식

- 예전에는 xml 형식으로 반환을 하였는데 현대에는 json으로 반환
- @ResponseBody의 반환 타입을 객체로 하였을 시 스프링에서 해당 객체를 자동적으로 json으로 치환하여 전송
- controller -> ResponseBody -> HttpMessageConverter -> 문자경우: StringConverter (StringHttpMessageConverter) / 객체: JsonConverter (MappingJackson2HttpMessageConverter)

---

### 스프링 어노테이션

- @RequestParam 변수타입 변수명
- Model
- @ResponseBody -> 이때 body는 메서드 body를 말하는 것이 아닌 http body를 뜻하며 body에 return 타입을 그대로 넣겠다라는 뜻

---

### 스프링 간단 구조

- 컨트롤러: 웹 MVC의 컨트롤러 역할
- 서비스: 핵심 비즈니스 로직 구현
- 리포지토리: 데이터베이스에 접근, 도메인 객체를 DB에 저장하고 관리
- 도메인: 비즈니스 도메인 객체 (예: 회원, 주문, 쿠폰 등등 주로 데이터베이스에 저장하고 관리됨)

---

### 기타

- 실무에서는 동시성 이슈가 있을 수 있기에 일반적인 HashMap보다는 ConcurrentHashMap을 사용함
- 테스트 코드를 작성할 시 assertj를 추천
- 테스트 전체 진행 시 각 테스트별에 대해 순서를 보장하지 않음으로 @AfterEach 어노테이션을 통해 각 테스트별 테스트가 종료되었을 시 실행해주는 메서드를 구현해두자
- 예외처리 확인으로는 assertThat이 아닌 assertThrows를 사용

---

### 스프링 빈 등록방법 2가지 및 의존성 주입 타입

- 컴포넌트 스캔과 자동 의존관계 설정 (@Compoenent, @Controller, @Service, @Repository, @Autowired)
- 자바 코드로 직접 스프링 빈 등록하기 (@Configuration, @Bean)
- 필드/Setter/생성자 주입

---