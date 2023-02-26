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

### BindingResult1

- (v2 코드로 기존에 수작업으로 작성했던 에러 처리를 `BindingResult` 로 변경하는 실습)
- BindingResult 는 굳이 모델에 안담아도 자동으로 View 로 전달됨
- 주의) BindingResult 의 매개변수 위치는 반드시 `@ModelAttribute` 다음에 와야 정상적으로 인식함
- 타임리프에서 사용할때는 `th:if="${#fields.hasGlobalErrors()}"` 이런식으로 사용하면 된다
- 타임리프에서 검증오류를 표현하는 기능을 사용할 수 있도록 스프링과 통합되어있음 (e.g. BindingResult)
- `th:errors` 는 `th:if` 의 편의버전이라고 생각하면 됨 (필드명과 그대로 에러가 있는지 없는지 확인하고, 있을때만 렌더링 됨)

### BindingResult2

- BindingResult 는 스프링이 제공하는 검증 오류를 보관하는 객체
- BindingResult 가 있을때는 에러 자체가 BindingResult 에 담기기때문에 무조껀 에러를 담고  컨트롤러까지는 호출이 됨 (에러페이지로 넘어가지 않음) → BindingResult 가 없으면 에러에 담고 할곳이 없어서 일단 400으로 컨트롤러를 타지않고 일단 에러페이지를 던져버림
- BindingResult 에 검증오류를 적용하는 3가지 방법
    - 개발자가 수기로 넣어주기
    - `Validator` 사용
    - `@ModelAttribute` 객체의 타입오류 등으로 바인딩이 실패하면 자동으로 스프링이 BindingResult 에 해당 오류를 담아준다
- 중요) 매개변수 순서가 중요함 → 반드시 ModelAttribute 바로 뒤에 와야함
- `BindingResult` 는 결국 `Errors` 인터페이스의 확장 인터페이스기때문에 (추가적인 기능이 있음) 그래서 사실 뭘사용해도 상관은 없는데 관례상 BindingResult 를 많이 사용

### FieldError, ObjectError

- (사용자가 입력했을 때 데이터가 남아있어야 사용성이 좋으므로, 값이 남도록 유지하고, FieldError, ObjectError 에 대한 자세한 설명)
- `bindingResult.addError(new FieldError()` 를 사용할 때 FieldError 에러 생성자를 중간에 `rejectedValue` 가 있는 생성자를 사용하면 됨
- 스프링은 FieldError type error 등이 발생하면 자동으로 BindingResult 에 담아주고 그 후에 컨트롤러 로직을 실행함
- 타임리프는 `th:field` 사용시 만약에 필드에 에러가 발생했다면, 기존의 값이 아닌 에러에서 발생한 `rejectedValue` 값을 담아준다 (ㄷㄷ;)

### 오류 코드와 메시지 처리1

- 기존의 `new FieldError()` 의 매개변수가 많은 생성자에서 `codes` 와 `arguments` 를 활용하면 에러 메시지를 효과적으로 사용할 수 있음
- 스프링의 resources 폴더에 `errors.properties` 를 만들어서 쓸껀데, 스프링 기본은 messages.properties 만 읽어서 사용하므로, 설정에서 `spring.messages.basename=messages, errors` 로 추가해준다 (위에도 적었지만 안적어두면 messages 만 default 로 사용한다

### 오류 코드와 메시지 처리2

- FieldError 와 ObjectError 가 다루기가 너무 복잡함 (일일이 만들어줘야해서)
- 근데 사실, BindingResult 는 항상 ModelAttribute 뒤에 와야하므로 BindingResult 는 항상 자신의 target 을 알고있음 (앞에있는 매개변수임)
- BindingResult 의 `bindinResult.rejectValue()` 를 사용하면 좀더 효율적으로 기존의 `new Field()` 를 대체할 수 있다

### 오류 코드와 메시지 처리3

- 오류 코드를 만들 때는 `required.item.itemName` 처럼 자세하게도 할 수 있지만, `required` 라고 정의해서 범용성 있게 사용할 수도 있다 → 근데 매번 모든 메시지를 세세하게 설계할 수 없음
- (중요) 에러 메시지는 배열로 들어가므로, 상위에러부터 범용메시지까지 모든 메시지 타입을 넣어주면 이후에 코드수정 없이 properties 만 수정해서 에러 메시지를 효율적으로 관리할 수 있음 → 스프링은 MessageCodesResolver 에서 이걸 다 구현 해놨음

### 오류 코드와 메시지 처리4

- 스프링의 `MessageCodesResolver codesResolver = new DefaultMessageCodesResolver();` 를 사용하면 이미 내부적으로(메소드로) 에러 하나만 넣으면 배열로 해당 타입의 모든 에러코드를 만들어준다.

### 오류 코드와 메시지 처리5

- 오류코드의 관리 전략은 “구체적인 것부터 덜구체적인것 순서로” 한다
- 팁) 스프링에서 `ValidationUtils` 를 사용하면 기본적인 검증처리는 한줄로 처리할수도 있음

### 오류 코드와 메시지 처리6

- 검증 오류코드는 “개발자가 만든코드” 와 “스프링이 만든코드” 가 있음 → 스프링이 만든건 “타입체크” 등 이 있음
- 그럼 스프링이 만든건 어떻게 해줘야 하나? → 스프링이 `typeMismatch` 를 넣어주므로, 우리가 errors.properties 에 추가해주면 된다
- 중요한건 이해도와 왜 이렇게 설계됐는지를 파악하고, 다른걸 설계할 때 참고하는것 (인사이트를 얻는 것)

### Validator 분리1

- 지금 검증로직을 컨트롤러에 때려박아서 코드가 지저분하므로, 검증기(Validator) 와 원래 컨트롤러 로직으로 나누는게 좋음, 유지보수에도 좋음
- 코드 자체는 `public class ItemValidator implements Validator { }` 로 확장해서 만들면 됨
- 굳이 왜 Validator 를 쓰는가? → 스프링 인터페이스를 사용했으니 스프링이 해도록 수정 할 예정 (다음강의)

### Validator 분리2

- 스프링의 `Validator` 인터페이스를 사용하면 스프링의 추가적인 방법론들을 사용할 수 있음

```java
@InitBinder
public void init(WebDataBinder dataBinder) {
	dataBinder.addValidators(itemValidator);
}
```

- 위 코드같이 컨트롤러에 적용해버리면, 요청이 넘어올 때 항상 먼저 검증기를 넣어줘서 바로 적용할 수 있게 됨
- 이제 위에 `@InitBinder` 의 검증기를 사용하려면 `@ModelAttribute` 앞에 `@Validated` 를 적용해줘야함 → main 클래스에 글로벌로 설정해줄수도 있음
- `@Validated` 어노테이션을 사용하면 “검증기를 사용하라”라는 뜻임
- 검증할 때 `@Validated` 와 `@Valid` 둘다 사용할 수는 있음
    - `@Validated` 는 스프링이고
    - `@Valid` 는 자바임

### 정리

- 검증이 개념적으로 굉장히 중요함
- (중요) 저장하는 검증이 실패하면 반드시 에러정보를 포함해서 다시 던져줘야 함
- 에러 메시지는 구체적인것 → 범용적인것 순서로 작성하는 습관이 좋음

## 섹션 5. 검증2 - Bean Validation

# 📋 메모

- 

# 💡 팁 (단축키 등)

- 

# 🔗 레퍼런스

-
