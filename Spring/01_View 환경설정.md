## View 환경설정

#### Welcome 페이지

resources/static 폴더에 index.html 문서를 생성하고 다음과 같이 편집한다.

```html
<!DOCTYPE HTML>
<html>
<head>
    <title>Hello</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
    Hello
    <a href="/hello">hello</a>
</body>
</html>
```

#### 샘플 페이지

**controller**

```java
// hello.hellospring.controller.HelloController
package hello.hellospring.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HelloController {
    @GetMapping("hello")
    public String hello(Model model) {
        model.addAttribute("data", "Spring!!");	// data 자리에 "Spring!!"을 치환시킴
        return "hello";
    }
}
```

**View**

```html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Hello</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
</head>
<body>
<p th:text="'안녕하세요, ' + ${data}">안녕하세요, 손님</p>
</body>
</html>
```

- 컨트롤러에서 리턴 값으로 `문자`를 반환하면 viewResolver가 `문자.html` 파일을 찾아서 처리한다.

![](C:\Users\USER\Pictures\Screenshots\스크린샷_20230109_101845.png)

### 빌드하고 실행하기

1. Mac의 경우 콘솔, Windows의 경우 git bash 실행
2. 다음과 같은 명령어를 입력한다.
   - `./gradlew build` : 프로젝트 빌드
   - `cd build/libs` : build/libs 디렉토리로 이동
   - `java -jar hello-spring-0.0.1-SNAPSHOT.jar` : jar 파일 실행
