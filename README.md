이 글은 내용을 정리하고 개인적인 사견을 첨가한 2차 창작물이며, 강의 및 강의자료(코드 등)에 대한 저작권은 [원본](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-2#) 및 원작자에게 있고 공유하지 않는다.

# 🗂 강의 자료

[수업 자료](https://www.notion.so/7e357e64c09041c99b80682c91676ab4)

# 🌈 강의 환경

- 

# 📝 강의 내용 정리

## 섹션 0. 소개

### 강의 소개

- (수업 소개)

### 수업 자료

- (수업자료 다운로드)

### 강의 소스 코드

- (실습 코드 다운로드)

## 섹션 1. 타임리프 - 기본 기능

## 섹션 2. 타임리프 - 스프링 통합과 폼

## 섹션 3. 메시지, 국제화

### 프로젝트 설정

- (실습 파일 사용법 설명, message-start 프로젝트 사용)

### 메시지, 국제화 소개

- 하드코딩 되어있는 문구들을 한곳에서 관리하기 위해 `message.properteis` 같은 관리용 파일로 처리하는 방법론을 말함
- 국제화는 메시지에서 한발 더 나아가서, 다른 언어를 셋팅했을 때 기존에 설정한 `meesage.properties` 를 언어별로 보여주도록 해주는 것
    - 어떤 언어로 접근했는지 확인하는 방법은 HTTP 의 “accept-language” 헤더를 사용하거나, 직접 언어를 선택하도록 제공 가능

### 스프링 메시지 소스 설정

- 스프링은 메시지 관리기능을 기본적으로 제공해줌, 또한 Spring boot 은 기본적인 설정도 다 되어있음 → 스프링부트를 쓰면 자동으로 `MessageSource` 를 빈으로 등록해줌
- 설정 파일의 위치는 `/resources/messages.properties` 가 기본
- 어떤 메시지 소스를 사용할지는 `application.properties` 에서 `spring.messages.basename=messages, config.i18n.message` 등으로 설정하면 됨
    - 기본값은 `spring.messages.basename=messages` 이고, 생략해도 됨(디폴트라)
    - 다른옵션은 [https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.core.spring.messages.basename](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.core.spring.messages.basename) 참조

### 스프링 메시지 소스 사용

- (간단한 `MessageSource` 사용법 실습)

### 웹 애플리케이션에 메시지 적용하기

- (타임리프에서 메시지 적용하는 방법 실습)
    - `th:text="#{label.item.name}"` 이런식으로 프로퍼티 값을 사용할 수 있음

### 웹 애플리케이션에 국제화 적용하기

- (타임리프에서 국제화 적용하는 방법 실습)
    - messages_en.properties 파일만 존재한다면, 언어 설정(Locale)만 변경하면 스프링이 자동으로 똑같은 라벨을 찾아줌
    - 테스트 한다면 크롬에서 설정 바꿔서 헤더에 Accept_Language 순서를 변경해주면 됨
    - 스프링은 언어를 선택할 때 기본적으로 Accept_Language 를 사용함 → 만약에 이방법 말고 설정과 무관하게 쿠키나 세션에 보관해서 언어를 변경해주려면 `LocaleResolver` 인터페이스를 사용해서 변경할 수 있음
    - LocaleResolver 방식을 변경하고 싶다면 “LocaleResolver” 의 구현체를 다른 방식으로 변경한다

### 정리

- (간단히 실습들 훑어보는 내용)

## 섹션 4. 검증1 - Validation

### 검증 요구사항

- 만약에 지금까지 만든 프로그램에 검증 로직이 필요해지면 요구사항에 맞게 검증 로직들을 추가해야함 → 지금 프로젝트는 에러페이지만 발생할 뿐 별다른 피드백이 없기때문에 좋은 경험이 아님
- 컨트롤러 계층의 중요한 역할 중 하나는 HTTP 요청이 정상인지 검증하는 것 이다
- 클라이언트 검증 vs 서버 검증
    - 클라이언트 검증은 조작이 가능함 → 그냥 Request 자체를 조작해버리면 되니까
    - 서버검증은 버튼이나 API 요청이 발생해야 알 수 있음 → 사용자 사용성이 별로임
    - 따라서 둘다 검증되어야 함

### 프로젝트 설정 V1

- (이전 프로젝트에 이어서 실습파일 validation-start → validation 으로 변경 후 사용하면 됨)

### 검증 직접 처리 - 소개

- 타임리프에선 사용자 요청이 발생했을 때 POST 요청에서 엉뚱한 데이터를 만들어 던졌다면, 서버 검증로직이 실패하고 실패한 데이터를 다시 담아서 던져서 알려줘야 함 (개발 전에 이미 이런 요구사항 정의가 이뤄져야 함)

### 검증 직접 처리 - 개발

- (기존의 타임리프 코드에 수동으로 검증로직 추가하는 실습)
- 타임리프를 사용할 때 `model.addAttribute` 에서 빈값을 넘기고, 에러발생시 해당 값에 데이터를 다시 채워주는 형태로 잘 재사용 할 수 있음
- 타임리프 사용중 SpringEL 문법에서 `<div th:if="errors?.containsKey('globalError')}"` 처럼 사용했을때 `errors?` 처럼 물음표를 사용하면 해당 값(errors) 가 `null` 일 때는 해당 문법을 실행하지 않고 그냥 null 을 던져버림 (?를 생략하면 null 값을 가지고 메서드를 실행하기때문에 NullPointException 이 터짐)
- 타임리프에서 `th:classappend` 를 사용하면 깔끔하게 뒤쪽으로 클래스를 추가할 수 있음

### 프로젝트 준비 V2

- (기존 프로젝트를 남겨주고 싶어서, 기존의 v1 화면을 패키지 복사해서 v2 를 만드는 방법 가이드 내용)

## 섹션 5. 검증2 - Bean Validation

# 📋 메모

- 

# 💡 팁 (단축키 등)

- 

# 🔗 레퍼런스

-
