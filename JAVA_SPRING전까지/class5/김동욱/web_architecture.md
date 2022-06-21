# 1. Web_architecture

- 3월 22일 자바 전공 강의
- web-backend

#### 1.1. web architecture

![image-20220614165500479](web_architecture.assets/image-20220614165500479.png)

- 브라우저가 해석할수있는 언어 (markup language - html, xml(데이터의 표현, 데이터 전달용 문서), CSS, JS)

- parameter를 가지고 요청함(request)
- client가 서버에 접속(**using http**)
- web server(http server, 클라이언트의 접속을 도와줌, 접속, 응답 처리)
- Application server(program language사용가능(**java사용**), client 요청에 대한 logic 처리)
  - 1. data get
    2. logic - business logic(db와 관련없는 모든 로직), db logic(dao)
    3. 응답(html)
  - java + web => Servlet, JSP
- 요즘은 web server와 application server가 합쳐서 많이 쓰임 -> Web Application Server(WAS, ex- web logic, web Sphere, JEUS, **Tomcat**)
- RDBMS(Oracle, MySQL, MsSQL, mariaDB)

#### 1.2 servelet

![image-20220615000204523](web_architecture.assets/image-20220615000204523.png)

#### 1-4. servlet parameter

![image-20220615131731773](web_architecture.assets/image-20220615131731773.png)

- 파라미터를 어떻게 처리할것인가..

#### 1-5. JSP(Java Server Page)

- HTML에 안에 JAVA코드가 들어감
- ![image-20220615160149947](web_architecture.assets/image-20220615160149947.png)
- 최초에 한번만 jsp -> servlet으로 바뀜
- compile(servlet), script(jsp) 의 장점을 둘 다 가지고 있음

- 스크립트보다 자바가 먼저 실행됨
