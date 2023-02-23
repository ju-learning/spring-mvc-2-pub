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

## 섹션 5. 검증2 - Bean Validation

### 유닛

- 

# 📋 메모

- 

# 💡 팁 (단축키 등)

- 

# 🔗 레퍼런스

-
