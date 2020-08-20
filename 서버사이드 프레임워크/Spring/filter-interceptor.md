### filter 와 interceptor 차이

![alt text](/image/spring/spring-request-lifecycle.jpg )

- Filter와 Interceptor는 실행되는 시점이 다르다.
- Filter는 Web Application에 등록을 하고, Interceptor는 Spring의 Context에 등록을 한다.

- tomcat의 경우 deployment descriptor(/WEB-INF/web.xml)에 사용할 Filter를 등록한다. 때문에 애플리케이션 전역에 영향을 주는 작업은 Filter로 한다는 의견이 있다. 하지만 사실은 그렇지 않다. Filter도 Interceptor도 모두 요청에 대한 전후 처리라고 하는 역할을 수행한다. 또한 uri기반으로 언제 실행할 것인지를 조정 가능하며, 직접 request의 내용을 파악해서 원하는 조건에 부합할 때 로직을 수행할 수 있다는 점에서 차이가 없다.

- 실행 시점이 다르기 때문에 가장 큰 영향을 받는 것. 예외 처리(Exception Handling)다.
- filter에서 예외가 발생하면 Web Application에서 처리해야 한다. tomcat을 사용한다면 <error-page>를 잘 선언하든가 아니면 Filter 내에서 예외를 잡아 request.getRequestDispatcher(String)으로 마치 핑퐁 하듯이 예외 처리를 미뤄야 한다. 하지만 Interceptor에서 예외가 발생하면? Interceptor의 실행 시점을 보자, Spring의 ServletDispatcher 내에 있다. 즉 @ControllerAdvice에서 @ExceptionHandler를 사용해서 예외를 처리를 할 수 있다.


### interface

Filter
~~~ java
public interface Filter {
  void doFilter(ServletRequest request, ServletResponse response, FilterChain chain);
}
~~~

HandlerInterceptor
~~~ java
public interface HandlerInterceptor {
  boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler);
  void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView mav);
  void afterCompletion(HttpServletRequest request, HttpServeletResponse response, Object handler, Exception ex);
}
~~~

- Filter는 Servlet에서 처리하기 전후를 다룰 수 있다.
- Interceptor는 Handler를 실행하기전(preHandle), Handler를 실행한 후(postHandle), view를 렌더링한 후(afterCompletion) 등, Servlet내에서도 메서드에 따라 실행 시점을 다르게 가져간다.

### Interceptor에서만 할 수 있는 것
- AOP 흉내를 낼 수 있다. @RequestMapping 선언으로 요청에 대한 HandlerMethod(@Controller의 메서드)가 정해졌다면, handler라는 이름으로 HandlerMethod가 들어온다. HandlerMethod로 메서드 시그니처 등 추가적인 정보를 파악해서 로직 실행 여부를 판단할 수 있다.
- View를 렌더링하기 전에 추가 작업을 할 수 있다. 예를 들어 웹 페이지가 권한에 따라 GNB(Global Navigation Bar)이 항목이 다르게 노출되어야 할 때 등의 처리를 하기 좋다.

### Filter에서만 할 수 있는 것
- ServletRequest 혹은 ServletResponse를 교체할 수 있다.