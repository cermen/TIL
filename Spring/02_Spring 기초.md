# Spring 기초

### 정적 콘텐츠

- 실시간으로 변화가 없는 데이터
- static 디렉토리에 저장한다.

### MVC 템플릿 엔진

#### MVC

> Model-View-Controller의 약자

- Model : 데이터를 담는 객체 - DB 테이블
- View : 데이터를 보여주는 방식 - 웹페이지 화면
- Controller : 비즈니스 로직

<img src="https://developer.mozilla.org/en-US/docs/Glossary/MVC/model-view-controller-light-blue.png" width=700>

(이미지 출처: https://developer.mozilla.org/ko/docs/Glossary/MVC)

#### 템플릿 엔진

> 템플릿 양식과 특정 데이터 모델에 따른 입력 자료를 합성하여 결과 문서를 출력하는 소프트웨어 또는 소프트웨어 컴포넌트

##### Spring의 템플릿 엔진

- FreeMarker
- Groovy
- Thymeleaf - 주로 이것을 사용한다.
- Mustache

### 샘플 코드

**controller**

```java
@Controller
public class HelloController {
    // 앞부분 생략

    @GetMapping("hello-mvc")
    public String helloMvc(@RequestParam(name = "name", required = false) String name, Model model) {
        model.addAttribute("name", name);
        return "hello-template";
    }
}
```

**View**

```html
<!-- hello-template.html -->
<html xmlns:th="http://www.thymeleaf.org">
<body>
<p th:text="'hello ' + ${name}">hello! empty</p>
</body>
</html>
```

### API

> Application Programming Interface(응용 프로그램 프로그래밍 인터페이스)

- 프로그램들과 데이터베이스, 그리고 기능들의 상호 통신 방법을 규정하고 도와주는 매개체

#### @ResponseBody

- `@ResponseBody`를 사용하면 `viewResolver`를 사용하지 않으며, 대신에 HTTP의 BODY에 문자 내용을 직접 반환
- `@ResponseBody`를 사용하고 객체를 반환하면 객체가 JSON으로 변환됨

```java
@Controller
public class HelloController {
    // 앞부분 생략

    @GetMapping("hello-string")
    @ResponseBody
    public String helloString(@RequestParam("name") String name) {
        return "Hello " + name; // "hello spring"
    }

    @GetMapping("hello-api")
    @ResponseBody
    public Hello helloApi(@RequestParam("name") String name) {
        Hello hello = new Hello();
        hello.setName(name);
        return hello;
    }

    static class Hello {
        private String name;

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }
    }
}
```

