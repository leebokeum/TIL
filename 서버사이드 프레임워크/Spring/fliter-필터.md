### filter
- 필터는 'HTTP 요청과 응답을 변경할 수 있는 재사용가능한 코드'이다.
- 필터는 객체의 형태로 존재하며 클라이언트로부터 오는 요청(request)과 최종 자원(서블릿/JSP/기타 문서) 사이에 위치하여 클라이언트의 요청 정보를 알맞게 변경할 수 있으며, 또한 필터는 최종 자원과 클라이언트로 가는 응답(response) 사이에 위치하여 최종 자원의 요청 결과를 알맞게 변경할 수 있다. 이를 그림으로 표현하면 다음과 같다.

![alt text](/image/spring/filter1.gif )

- 그림에서 자원이 받게 되는 요청 정보는 클라이언트와 자원 사이에 존재하는 필터에 의해 변경된 요청 정보가 되며, 또한 클라이언트가 보게 되는 응답 정보는 클라이언트와 자원 사이에 존재하는 필터에 의해 변경된 응답 정보가 된다. 위 그림에서는 요청 정보를 변경하는 필터와 응답 정보를 변경하는 필터를 구분해서 표시했는데 실제로 이 둘은 같은 필터이다. 단지 개념적인 설명을 위해 그림1과 같이 분리해 놓은 것 뿐이다.



### filter 체인
- 필터는 클라이언트와 자원 사이에 1개가 존재하는 경우가 보통이지만, 여러 개의 필터가 모여 하나의 체인(chain; 또는 사슬)을 형성할 수도 있다. 그림은 필터 체인의 구조를 보여주고 있다.

![alt text](/image/spring/filter2.gif )

 - 여러 개의 필터가 모여서 하나의 체인을 형성할 때 첫번째 필터가 변경하는 요청 정보는 클라이언트의 요청 정보가 되지만, 체인의 두번째 필터가 변경하는 요청 정보는 첫번째 필터를 통해서 변경된 요청 정보가 된다. 즉, 요청 정보는 변경에 변경에 변경을 거듭하게 되는 것이다. 응답 정보의 경우도 요청 정보와 비슷한 과정을 거치며 차이점이 있다면 필터의 적용 순서가 요청 때와는 반대라는 것이다.
 - 필터는 변경된 정보를 변경하는 역할 뿐만 아니라 흐름을 변경하는 역할도 할 수 있다. 즉, 필터는 클라이언트의 요청을 필터 체인의 다음 단계(결과적으로는 클라이언트가 요청한 자원)에 보내는 것이 아니라 다른 자원의 결과를 클라이언트에 전송할 수 있다. 필터의 이러한 기능은 사용자 인증이나 권한 체크와 같은 곳에서 사용할 수 있다.

### Filter 인터페이스

- public void init(FilterConfig filterConfig) throws ServletException
  - 필터를 웹 콘테이너내에 생성한 후 초기화할 때 호출한다.
- public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws java.io.IOException, ServletException
  - 체인을 따라 다음에 존재하는 필터로 이동한다. 체인의 가장 마지막에는 클라이언트가 요청한 최종 자원이 위치한다.
- public void destroy()
  - 필터가 웹 콘테이너에서 삭제될 때 호출된다
- 위 메소드에서 필터의 역할을 하는 메소드가 바로 doFilter() 메소드이다. 서블릿 콘테이너는 사용자가 특정한 자원을 요청했을 때 그 자원 사이에 필터가 존재할 경우 그 필터 객체의 doFilter() 메소드를 호출하며, 바로 이 시점부터 필터가 작용하기 시작한다.

~~~ java
public class FirstFilter implements javax.servlet.Filter {
  
     public void init(FilterConfig filterConfig) throws ServletException {
        // 필터 초기화 작업
     }
     
     public void doFilter(ServletRequest request,
                          ServletResponse response,
                          FilterChain chain)
                          throws IOException, ServletException {
        // 1. request 파리미터를 이용하여 요청의 필터 작업 수행
        // 2. 체인의 다음 필터 처리
        chain.doFilter(request, response);        // 3. response를 이용하여 응답의 필터링 작업 수행
     }
     
     public void destroy() {
        // 주로 필터가 사용한 자원을 반납
     }
  }
~~~