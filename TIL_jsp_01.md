## JSP(Java Server Page)

##### 백엔드 2일차

---

- 서버 사이드 스크립트 언어
- Java 기반으로 HTML 문서 내에 자바 코드를 삽입
- Servlet을 보완한 스크립트 방식 표준(Servlet +α)
- View를 담당하는 페이지로 사용

### JSP 페이지 구조

- 정적 페이지 + 동적 페이지
- 정적 페이지 구현 : HTML 태그
- 동적 페이지 구현 : 스크립트 사용

### JSP 페이지 구성

- ##### 지시어 

  - page
  - include
  - taglib

- ##### 스크립트 요소

  - 선언문
  - 표현식
  - 스크립트릿

- ##### 액션 태그

| 구분       | 태그 표기법                     | 설명                                 |
| ---------- | ------------------------------- | ------------------------------------ |
| 지시어     | <%@   %>                        | JSP 페이지의 속성 지정               |
| 선언부     | <%!      %>                     | 변수 선언 및 메소드 정의             |
| 표현식     | <%=     %>                      | 계산식, 함수 호출 결과 등 출력       |
| 스크립트릿 | <%      %>                      | 자바 코드 기술                       |
| 주석       | <%--  --%>                      | JSP 페이지에 설명 추가               |
| 액션 태그  | <<jsp:액션>><br /><</jsp:액션>> | 자바 빈, include / forward/ param 등 |

### 지시어

#### page 지시어

- `<%@ page ...%>`

- JSP 페이지에 대한 속성 설정

#### include 지시어

- `<%@ include file="포함될 파일의 url"%>`
- 파일을 해당 JSP 페이지 내에 삽입하는 기능 제공
- 복사&붙여넣기 방식으로 두 개의 파일이 하나의 파일로 합쳐진 후 변환되고 컴파일

#### taglib 지시어

- <%@ taglib prefix="c" uri="http:..."%>
- 표현 언어(EL), JSTL을 JSP 페이지 내에서 사용할 때 씀

### 스크립트 요소 

#### 선언문

- JSP 페이지의 멤버 필드 선언 도는 메소드를 정의할 때 사용
- 선언문에서 선언된 변수는 전역 변수 역할 - 페이지 전체 사용 가능
- `<%! int a=10; %>`

#### 표현식

- 변수 값, 계산 결과, 함수 호출 결과를 출력하기 위해 사용
- `<%= 3*5 %>`
- `<%= name %>`

#### 스크립트릿

- 자유롭게 자바 코드를 기술할 수 있는 영역
- 스크립트릿 내에서 선언된 변수는 지역 변수
- `<% 자바코드 %>`

---

### JSP 내장 객체

#### 내장 객체

- 클라이언트에서 웹 서버에게 JSP 페이지를 요청하면 자동 생성
- 객체 생성하지 않고 바로 사용 가능

#### 내장 객체 종류

- 입출력 : request / response / out
- 서블릿 : page / config
- 컨텍스트 : session / application / pageContext
- 예외 처리 : exception

##### request 객체 예제

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Insert title here</title>
	</head>
	<body>
		<div id="wrap">
	        <h3 align="center">회원 가입</h3>
	        <hr>
	        <form id="newMemberForm" name="newMemberForm" method="post" action="requestFormOk.jsp">
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

```javascript
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Insert title here</title>
	</head>
	<body>
		
			<%
			request.setCharacterEncoding("utf-8"); 
			
			String name = request.getParameter("name");
			String id = request.getParameter("id");
			String pwd = request.getParameter("pwd");
			String hp = request.getParameter("hp1")+"-"+request.getParameter("hp2")+"-"+request.getParameter("hp3");
			String year = request.getParameter("year");
			String interests[] = request.getParameterValues("interest");
			String department = request.getParameter("department");
				
		
		%>
		
		<!--  변수에 저장된 값 출력 -->
		<h3>회원 가입 내용</h3>
		성명 : <%= name %><br>
		아이디 : <%= id %><br>
		비밀번호 : <%= pwd %><br>
		휴대폰 번호 : <%= hp %><br>
		학년 : <%= year %><br>
		관심분야:

		<%for(String interest : interests){  %>
			<%= interest + " " %>
		<% } %>
		학과: <%=department%>
		

	
	</body>
</html>
```

