### 1.2 JSP(JavaServer Pages)의 특징
1. **HTML 문서 내에 자바 코드를 삽입**
    - `.jsp` 파일은 HTML 문서에 자바 코드를 삽입하는 형태
    - WAS(Web Application Server)에서 JSP를 최초 요청 시 서블릿(.java)으로 변환 후 컴파일하여 실행
2. **뷰(View) 역할**
    - 주로 사용자에게 보여지는 화면(프레젠테이션 로직)을 담당
    - 자바 코드를 직접 쓰는 대신, EL(Expression Language) 또는 JSTL/JSP 태그 등을 사용하여 로직을 간결화하고 유지보수를 쉽게 함
3. **MVC 구조**에서 **View** 역할
    - 서블릿(Controller)에서 전달받은 데이터(모델)를 화면에 표시
4. **내장 객체** 사용 가능
    - `request`, `response`, `session`, `application`, `out`, `pageContext` 등
    - JSP 페이지 내에서 기본적으로 제공되는 객체이므로 별도의 선언 없이 바로 사용 가능
5. **자동 컴파일**
    - JSP 파일은 최초 요청 시 서블릿 클래스로 변환 → 컴파일 → 실행
    - 이후에는 클래스 파일로서 동작(수정 시 다시 변환)
![[Pasted image 20250331051312.png]]
![[Pasted image 20250331051347.png]]
## directive - jsp 페이지 실행시 필요한 정보 지정
\<%@ \[directive] 속성="값" %>
![[Pasted image 20250331051403.png]]![[Pasted image 20250331051718.png]]![[Pasted image 20250331051744.png]]![[Pasted image 20250331051811.png]]

## 내장 객체
- .jsp 파일의 \_jspService 메서드 내부에 로컬  변수로 선언 된 객체
![[Pasted image 20250331051855.png]]![[Pasted image 20250331051926.png]]![[Pasted image 20250331051951.png]]