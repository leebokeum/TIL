### Servlet-Context
- Servlet 단위로 생성되는 context
- Spring에서 servlet-context.xml 파일은 DispatcherServlet 생성 시에 필요한 설정 정보를 담은 파일 (Interceptor, Bean생성, ViewResolver등..)
- URL설정이 있는 Bean을 생성 (@Controller, Interceptor)
- Application Context를 자신의 부모 Context로 사용한다.
- Application Context와 Servlet Context에 같은 id로 된 Bean이 등록 되는 경우, Servlet Context에 선언된 Bean을 사용한다.
- 