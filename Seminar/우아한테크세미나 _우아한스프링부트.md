# 우아한테크세미나 (우아한 스프링 부트)

## 스프링부트와 스프링의 차이

- **스프링부트**: 스프링을 쉽게 쓰게 해주는 툴
- **스프링**: 자바 애플리케이션 개발을 쉽게 하게 해주는 프레임워크

## 스프링 부트 시작하는 법

1. start.spring.io 사이트

   - maven 또는 gradel 중에 사용할 프로젝트 선택
     -  `maven` 선택
   - 언어 선택
   - spring boot 버전 선택 - maven 선택시
     - `snapshot`은 개발 중인 것
     - `m2`는 배포된 것
     - `ga`는 아무것도 붙어 있지 않은 정식 배포 버전 - 선택
   - 프로젝트 메타데이터
     - 프로젝트를 식별할 수 있는 정보들 입력
     - 패키징에서는 `jar`, `war` 선택 가능. `war`는 웹 애플리케이션 아카이브.
   - 의존성
     - 스프링 웹, 타임리프 등
     - 구성요소는 그룹아이디, 아티팩트아이디, 버전

2. 스프링 프로젝트를 IDE에서 오픈

## 빌드: 의존성 관리

   - pom.xml에서 `dependencies`를 확인해 보면 버전이 적혀 있지 않은데 `spring boot starter parent`를 상속받고 있고, `spring boot starter parent`는 `spring boot dependencies`를 상속받고 있는 것을 알 수 있다.
   - `dependencyManagement`에 `spring boot dependencies`에 맞는 버전이 있으므로 굳이 찾아서 입력해주지 않아도 된다.
   - lombook에서 맞는 버전을 찾아서 가져와서 삽입해도 되지만 `dependencyManagement`에서 상속받아 사용되므로 그대로 놔두자.

## 빌드: 애플리케이션 실행

- mvn spring-boot: run - 메이븐 플러그인에서 선택해서 사용
- main 클래스 실행: 개발 시 가장 많이 사용하는 방법
- `jar` 패키징 & `java jar`
  - 메이븐의 `package`로 해당 프로젝트의 애플리케이션들을 모아서 `jar`파일을 생성할 수 있다.
    - fat jar 또는 uber jar라고 부르기도 한다.
- 스프링 부트에서는 톰캣이 내장되어 있다.
- 만약 8080포트가 이미 사용중이라는 에러가 뜨면 포트를 변경하거나 프로세스를 수동으로 강제로 끈다.

## 코딩: 개발 툴

- 템플릿을 수정한 경우에는 바로바로 변경사항을 확인할 수 없음
- pom.xml의 `dependencies`에서 `<groupId>org.springframework.boot</grounpId>`의 `<artifatId>spring-boot-devtools</artifactId>`를 추가하면 자동으로 리스타트(재기동)된다.
  - **빌드**: 해당 프로젝트를 jar파일로 묶어서 새로운 jar파일을 생성하는 것
  - **재기동**: 해당 jar파일을 실행하는 것
  - _해당 dependency는 포함한 채로 빌드 후 배포를 해도 상관없다._

## 코딩: 자동 설정

- 애플리케이션의 `@Configuration`에서 `@Bean`을 설정
- `@Bean`의 순서는 의존성이 없는 경우에는 그리 중요하지 않으며, 의존성이 있는 경우에는 의존성에 따라 순서대로 만들어진다.

## 코딩: 외부 설정 파일

- 예를 들어 application.properties에 message를 따로 뺄 수도 있다.
- config 디렉토리 안의 application.properties가 우선순위가 더 높다. (config 디렉토리 한정)
- application.properties는 가장 구체적이고 가까운 위치에 있는 설정이 우선순위가 더 높다.

## 배포: 도커 이미지

- 도커와 dive 설치 후 커맨드라인 dive 명령어로 계층 구조를 확인할 수 있다.

## 관리: Actuator

- dependency에 artifactID를 actuator로 넣어준다.
- endpoint를 확인할 수 있다.
- http localhost:8080/actuator/loggers를 커맨드창에 입력하면 log확인 가능
- 런타임 중에도 http POST localhost:8080/actuator/loggers/프로젝트 주소 DEBUG 를 커맨드창에 입력하면 모드를 DEBUG로 변경 가능
- 보안과 관련해서는 특정 사용자만 접근 가능하도록 따로 security를 걸면 된다.
- BUT 스프링 부트 어드민을 사용하게 되면 시각화되어 있으므로 버튼 하나만으로 모드 변경 즉시 적용 등 가능!!