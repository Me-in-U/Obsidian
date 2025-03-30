---
aliases: []
---
### 서블릿(Servlet)의 특징
1. **자바 클래스 기반**
	- 자바 언어로 작성된 서버사이드 프로그램
	- `javax.servlet` 패키지와 `javax.servlet.http` 패키지에 있는 인터페이스/클래스를 구현(또는 상속)하여 작성
2. **HTTP 요청/응답 처리**
	- `HttpServlet` 클래스를 상속받아 `doGet()`, `doPost()` 메서드 등을 오버라이딩하여 HTTP 요청을 처리
3. **비즈니스 로직 처리에 적합**
	- 요청을 받고, 처리(비즈니스 로직) 후 결과를 뷰(JSP 등)에 전달
4. **MVC 구조**에서 **Controller** 역할을 주로 담당
	- JSP는 화면 처리(뷰)에 집중
	- 서블릿은 요청을 받아 로직을 수행한 뒤 필요한 데이터를 JSP에 넘기는 경우가 일반적
5. 장점
	   - OOP 기반: 유지 보수성, 재활용성 우수, 플랫폼 독립적
	   - 멀티스레딩 지원
6.  장점
	- business logic과 presentation logic(HTML code)가 섞여서 나타남
	- -> Servlet + JSP Medel 2 방식으로 처리

## URL 매핑
어노테이션(@WebServlet) 사용 (Servlet 3.0 이상)
```java
@WebServlet("/example")
public class ExampleServlet extends HttpServlet {
    // ...
}
```
- **`/example`** : 특정 경로
- **`/example/*`** : 하위 모든 경로
- **`*.do`** : 특정 확장자로 끝나는 요청 처리 (예: `login.do`, `logout.do` 등)

## 3. 주요 Servlet 객체와 JSP 내장 객체/메서드

### 3.1 주요 Servlet 객체

1. **`HttpServletRequest`** (`request`)
    - 클라이언트 요청 정보를 담고 있는 객체
    - 요청 파라미터, 헤더, 쿠키, 세션 정보 등 접근 가능
    - 메서드 예시
        - `getParameter(String name)` : 요청 파라미터 값 반환
        - `getSession()` : `HttpSession` 객체 반환
        - `getRequestDispatcher(String path)` : 요청 디스패치(포워딩/인클루드) 기능
        - `getHeader(String name)` : 요청 헤더 가져오기
2. **`HttpServletResponse`** (`response`)
    - 서버가 클라이언트로 응답할 때 사용하는 객체
    - 응답 헤더, 쿠키, 상태 코드, 콘텐츠 타입 등을 설정
    - 메서드 예시
        - `sendRedirect(String location)` : 클라이언트를 특정 URL로 리다이렉트
        - `setContentType(String type)` : 응답 콘텐츠 타입 설정
        - `getWriter()` : 출력 스트림(`PrintWriter`) 획득해 HTML/text 직접 출력
3. **`HttpSession`** (`session`)
    - 클라이언트별로 세션을 유지하기 위한 객체
    - 사용자별로 일정 시간 동안 상태를 저장 가능
    - 메서드 예시
        - `setAttribute(String name, Object value)` : 세션 속성 저장
        - `getAttribute(String name)` : 세션 속성 가져오기
        - `invalidate()` : 세션 무효화(로그아웃 시)
4. **`ServletContext`** (`application`)
    - 웹 애플리케이션 전역에서 사용 가능한 컨텍스트 정보
    - 메서드 예시
        - `setAttribute(String name, Object value)`, `getAttribute(String name)` : 애플리케이션 범위 속성 저장/조회
        - `getRequestDispatcher(String path)` : 애플리케이션 레벨에서 포워딩 가능
        - 웹 애플리케이션 초기화 파라미터, 리소스 접근 등 가능

### 3.2 JSP 내장 객체

JSP에서는 아래와 같은 내장 객체가 기본으로 제공됩니다:
1. **`request`**
    - `HttpServletRequest` 객체와 동일
2. **`response`**
    - `HttpServletResponse` 객체와 동일
3. **`session`**
    - `HttpSession` 객체
4. **`application`**
    - `ServletContext` 객체
5. **`out`**
    - `JspWriter` 객체(서블릿의 `PrintWriter`와 유사)
    - JSP에서 HTML 등을 출력할 때 사용
6. **`pageContext`**
    - JSP 페이지 전반에 대한 정보를 제공하는 컨텍스트
    - 다른 내장 객체에 접근 가능
7. **`page`**
    - 현재 JSP 페이지 자체를 가리키는 객체 (this와 유사)
8. **`config`**
    - `ServletConfig` 객체 (서블릿 설정 정보를 담음)
9. **`exception`**
    - 에러 페이지에서 예외 정보를 담고 있는 객체 (errorPage 지정을 통해 사용)

#### 주요 메서드 예시
- `request.getParameter("paramName")` : 파라미터 값 획득
- `session.setAttribute("key", value)` : 세션 범위로 데이터 저장
- `application.getAttribute("key")` : 애플리케이션 범위로 공유된 데이터 조회
- `out.print("text")` : 직접 화면에 텍스트 출력