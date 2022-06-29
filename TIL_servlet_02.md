## 웹 서비스와 서블릿-2

##### 백엔드 2일차
---

#### 자바스크립트로 서블릿에 요청

- DOM 사용 
- name 속성 사용 



### 서블릿 포워딩

#### 포워딩 

- 서블릿에서 다른 서블릿이나 JSP 페이지로 요청을 전달하는 기능

#### 포워딩 

- 요청에 대한 추가작업을 다른 서블릿에서 수행
- 요청에 포함된 정보를 다른 서블릿이나 JSP 페이지와 공유
- 요청에 정보를 포함시켜 다른 서블릿으로 전달
- 컨트롤러에서 뷰로 데이터 전달

#### 포워딩 방법

1. redirect 방법

   - 웹 브라우저에 재요청
   - HttpServletResponse 객체의 sendRedirect() 메소드 이용
   - `sendRedirect("포워드할 서블릿/JSP");`

2. Refresh 방법

   - 웹 브라우저에 재요청
   - HttpServletResponse 객체의 addHeader() 메소드 이용
   - `addHeader("Refresh","경과시간(초); url=요청할 서블릿/JSP");`

3. location 방법

   - 자바스크립트에서 재요청
   - 자바스크립트 location 객체의 href 속성 이용
   - `location.href="요청할 서블릿/JSP"`

4. dispatch 방법 (일반적인 의미의 포워딩 기능. 가장 많이 사용)

   - 서블릿이 직접 요청

   - URL이 바뀌지 않음(클라이언트 측에서는 포워드 진행 여부를 알 수 없음)

   - ```javascript
     RequestDipatcher dis = request.getRequestDispatcher(“포워드할 서블릿 또는 JSP);
     
     dis.forward(request, response);
     ```

     

### 바인딩(binding)

- 많은 양의 정보를 전달해야 할 경우

- 서블릿에서 다른 서블릿 또는 JSP로 대량의 데이터를 공유하거나 전달할 때바인딩 사용
- 포워딩 가능 중 `dispatch`만 바인딩 기능 사용 가능 - 다른 포워딩 방법들은 웹 브라우저를 거치기 전과 후의 객체가 서로 다른 객체이기 때문

```javascript
	
// 보내는 서블릿
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

		request.setAttribute("name", "홍길동");
		request.setAttribute("address", "서울시");	
		RequestDispatcher dis = request.getRequestDispatcher("second06?name=lee");
		dis.forward(request,response);
	}

// 받는 서블릿
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");

		// 바인딩된 데이터 추출
		String name = (String)(request.getAttribute("name"));
		String address = (String)(request.getAttribute("address"));
		
		// 클라이언트 웹 페이지로 출력
		PrintWriter out = response.getWriter();
		
		out.println("<html><body>");
		
		out.println("이름 : "+name+"<br>");
		out.println("주소 : "+address);
		out.println("<br>dispatch를 이용한 포워딩");
		
		out.println("</html></body>");   // url 주소가 바뀌지 않는다
	}
```

