### 웹 서비스

#### 웹 프로그래밍

- 클라이언트 - 서버 방식
- 정적 웹 프로그래밍 - 데이터가 실시간으로 변화하는 것을 처리하거나 저장하기에 불가능
- 동적 웹 프로그래밍

#### 정적 웹 프로그래밍 

- 미리 보여줄 HTML 페이지, CSS, js 파일 등을 저장해놓고 브라우저가 요청할 경우 그대로 전달

- 화면 디자인을 구성하거나 클라이언트의 이벤트를 처리
- 실시간 데이터 처리/저장을 다루기에 부적합
- 구성 요소 - 클라이언트, 웹 서버, HTTP 프로토콜, HTML, 자바스크립트, CSS

#### 동적 웹 프로그래밍

- 정적 프로그래밍에서의 관리자의 역할을 웹 어플리케이션 서버가 수행(WAS)
- 클라이언트의 요청이 있을 때마다 데이터베이스(CRUD)에 접근해서 실시간으로 정보를 가져와 클라이언트에게 전송
- JSP, ASP, PHP 등
- 기능 재사용, 빠른 수행



#### 웹 서비스

- 웹 브라우저, 웹 서버, 웹 어플리케이션 서버(WAS), 테이터베이스로 구성

##### 웹 서버

- HTTP 프로토콜 기반
- 정적 콘텐츠(HTML, JPG, CSS) 제공
- 동적인 콘텐츠 요청은 웹 컨테이너에게 보내고, 웹 컨테이너가 처리한 결과를 클라이언트에게 응답

- Apache, IIS

##### 웹 컨테이너

- JSP와 Servlet을 실행시킬 수 있는 소프트웨어

- 웹 서버와 서블릿 사이이 서로 통신하도록 하고, WAS 내부에서 서블릿을 관리함(서블릿 컨테이너)
- 웹 어플리케이션 당 한 개의 ServletContext 생성

##### 웹 컨테이너의 작동

1. 클라이언트가 웹서버로 `HTTP request`를 전송
2. WAS(서블릿 포함)가 요청 데이터를 웹 컨테이너로 전송
3. 웹 컨테이너가 요청을 각 서블릿에게 전달(HttpServletRequest 객체와 HttpServletResponse  객체 생성)
4. 웹 컨테이너가 요청된 Servlet의 serive() 메소드를 호출하여 Servlet을 활성화
5. 웹 컨테이너가 서블릿이 생성한 `response`를 웹 서버(HTTP service)에 전송
6. 웹 서버가 `HTTP response`를 클라이언트에게 전송

##### 웹 어플리케이션 서버(WAS)

- 웹 서버로부터의 동적인 요청을 처리
- 웹 서버 + 웹 컨테이너
- 톰캣도 여기 포함

---

#### JSP 와 Servlet

##### JSP

- 서버 측 스크립트 언어
- HTML 내에 Java 언어를 삽입한 문서 형태
- .jsp

##### Servlet

- Java 언어로 이루어진 웹 프로그래밍 문서
- 자바 코드에 의존적
- .java

---

#### 서블릿(Servlet)

- 서버 측에서 실행되면서 클라이언트의 요청을 처리하고 반환(응답-HTML 형식)하는 서비스를 제공하는 자바 클래스
- 자바를 사용하여 동적 웹을 만들기 위해 필요한 웹 어플리케이션 프로그래밍 기술
- 컨테이너에서 실행

- 스레드를 이용하여 동작
- MVC 패턴에서 컨트롤러로 이용

##### 서블릿 처리 순서

1. 클라이언트 요청
2. 서버에서 서블릿 컨테이너를 만들고 스레드 생성
3. 서블릿 컨테이너가 스레드를 가동하여 HttpServletRequest, HttpServletResponse 객체 생성
4. Web.xml이 어느 서블릿에 대해 요청한 것인지 탐색 후 해당 서블릿에서 service() 메소드 호출 
5. doGet() 또는 doPost() 호출 하여 ServletResponse 객체에 응답 전송
6. 서블릿 실행 결과 웹 서버에 전송
7. 웹 서버가 웹 브라우저에게 결과 전송

##### 서블릿 라이프 사이클

1. Servlet 객체 생성
2. 초기화 : Init() 호출
3. 요청 작업 처리
   - doGet() / doPost()
   - service
   - 요청 시 매번 수행
4. 자원 해체 : destroy() 호출

##### 서블릿 생성 과정

1. 서블릿 클래스 생성
2. 서블리 생명주기 메소드 구현
3. 서블릿 매핑 작업 - web.xml에 추가하는 방식은 복잡하고 귀찮으니까 어노테이션 방식을 쓰자.
4. 웹 브라우저에서 서블릿 매핑 이름으로 요청

##### `<form>` 태그로 서블릿 요청

- `<form>` 태그를 사용해서 브라우저에서 서블릿으로 사용자의 요청이나 데이터를 전송
- action 속성 : 서블릿 또는 JSP 이름 지정
- method : GET 또는 POST 설정 (디폴트는 GET)
- 폼에 입력되어 서버로 전송되는 값을은 모두 **문자열**임. 연산 하려면 형변환 필요

##### `<input>` 태그

- 데이터를 입력받아서 전송
- name 속성 사용
- name 속성명과 속성값 쌍으로 전송

#### 서블릿에서 클라이언트 요청 받기

HttpServletRequest 클래스의 여러가지 메소드를 이용해서 전송된 데이터를 받음

- `String getParameter(String name)` : name의 값을 알고 있을 때, name에 대한 전송값을 **하나** 받아오는 데 사용

- `String[] getParameterValues` : 같은 name에 대해 여러 개의 값을 얻을 때. 배열 값으로 반환됨

  - 체크 박스 값을 받을 때

  - 라디오버튼의 경우 name은 모두 같지만 마지막 전송 값은 하나이므로 `getParameterValues`가 아닌 `getParameter`로 받음

- `Enumeration getParameterNames()` : name 값을 모를 때

#### doHandel() / doProcess()

- doGet() / doPost() 방식 둘 다 처리 가능

- doGet() 또는 doPost() 방식으로 요청이 들어오면 doGet() 또는 doPost() 메소드에서 doHandle()을 호출하여 request와 response 객체 전달

- doHandle() 메소드에서 처리

- ```java
  protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  		doHandle(request, response);	}
  
  protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  		doHandle(request, response);	}
  	
  protected void doHandle(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { ... }
  ```

  

##### 실습

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>회원가입 폼</title>
		<style>			
			#id, #pwd { width: 100px;}
			table { margin:0 auto; width:600px; }
		</style>
			
	</head>
	<body>
		<div id="wrap">
	        <h3 align="center">회원 가입</h3>
	        <hr>
	        <form id="newMemberForm" name="newMemberForm" method="post" action="newMember">
	          <table>
	          	<tr><td> 성명</td><td><input type="text" id="name" name="name"></td></tr>
	            <tr><td> ID</td><td><input type="text" id="id" name="id"></td></tr>
	            <tr><td>비밀번호</td><td><input type="password" id="pwd" name="pwd"></td></tr>
	            <tr><td>휴대폰 번호</td><td><input type="text" id="hp1" name="hp1" size="3"> 
	                    - <input type="text" id="hp2" name="hp2" size="4">
	                    - <input type="text" id="hp3" name="hp3" size="4"></td></tr>   
	            <tr><td>학년</td><td><input type="radio" id="year1" name="year" value="1" >1학년
	                                     <input type="radio" id="year2" name="year" value="2">2학년
	                                     <input type="radio" id="year3" name="year" value="3">3학년
	                                     <input type="radio" id="year4" name="year" value="4">4학년</td></tr>
	            <tr><td>관심분야</td>
	                  <td><input type="checkbox"  id="web" name="interest" value="웹 프로그래밍">웹 프로그래밍
	                         <input type="checkbox"  id="design" name="interest" value="파이썬">파이썬
	                         <input type="checkbox"  id="bigdata" name="interest" value="빅데이터">빅데이터
	                         <input type="checkbox"  id="java" name="interest" value="자바">자바 프로그래밍</td></tr>
	            <tr><td>학과</td>
	                  <td><select id="department" name="department">
	                               <option value="">선택하세요</option>
								   <option value="경영학과">경영학과</option>
								   <option value="산업공학과">산업공학과</option>
								   <option value="경제학과">경제학과</option>
								   <option value="전자공학과">전자공학과</option>
								   <option value="컴퓨터학과">컴퓨터학과</option>
	                          </select></td></tr>
	             <tr>
	                <td colspan="2" align="center">
	                    <br><input type="submit" value="완료">
	                    <input type="reset" value="취소">
	                </td>
	            </tr>             
	          </table>
      		</form>	
      	 </div>            
    </body>
</html>
```

```java
package sec02;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class NewMemberServlet
 */
@WebServlet("/newMember")
public class NewMemberServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public NewMemberServlet() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doHandle(request, response);	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		doHandle(request, response);
	}
	
	protected void doHandle(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		request.setCharacterEncoding("utf-8");   // 데이터 인코딩
		String name = request.getParameter("name");
		String id = request.getParameter("id");
		String pwd = request.getParameter("pwd");
		String hp1 = request.getParameter("hp1");
		String hp2 = request.getParameter("hp2");
		String hp3 = request.getParameter("hp3");
		String year = request.getParameter("year");
		String interest[] = request.getParameterValues("interest");
		String department = request.getParameter("department");
			
		
		response.setContentType("text/html; charset=utf-8");
		PrintWriter out = response.getWriter();
		
		//html 문서 형식으로 테이터 작성해서 전송
		out.println("<html><head></head><body>");
		out.println("이름 : "+name+"<br>");
		out.println("아이디 : "+id+"<br>");
		out.println("비밀번호 : "+pwd+"<br>");
		out.println("휴대폰 번호 : "+hp1+"-"+hp2+"-"+hp3);
		out.println("학년 : "+year+"<br>");
		out.println("관심분야: : ");
		

		for(int i=0; i<interest.length; i++) {
			System.out.print(interest[i]+" ");
		}
		
		out.println("<br>학과: : "+department);
		
		out.println("</body></html>");
	}

}
```

