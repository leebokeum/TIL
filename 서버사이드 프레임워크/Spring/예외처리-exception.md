### 스프링에서 예외처리하는 방법
1. Controller 레벨에서 처리
2. Global 레벨에서 처리
3. HandlerExceptionResolver를 이용한 처리


### Controller 레벨에서 처리
- @ExceptionHandler 어노테이션을 통해 Controller의 메소드에서 throw된 Exception에 대한 공통적인 처리를 할 수 있도록 지원하고 있다.

~~~ java
@Controller
public class DemoController {

    @GetMapping(path="/exception/demo")
    public String occurDemoException() {
        //강제로 DemoException을 발생 시켜 보았다.
        throw new DemoException(); //occur DemoException (RuntimeException)
    }
    
    @GetMapping(path="/exception/demo2")
    public String occurDemoException2() {
        //강제로 DemoException을 발생 시켜 보았다.
        throw new DemoException(); //occur DemoException (RuntimeException)
    }

    @ExceptionHandler(value=DemoException.class)
    public String handleDemoException(DemoException e) {
        log.error(e.getMessage());
        return "/error/404";
    }
}
~~~

### Global 레벨에서 처리
- Controller 별로 @ExceptionHandler 어노테이션이 붙은 메소드를 만들게 된다면, 중복코드가 양산 될 것이고 결국 유지보수의 비용이 증가하게 될 것이다. Spring 에서는 이런 상황을 위해 Web Application 전역적으로 @ExceptionHandler를 사용할 수 있도록 지원한다.

~~~ java
@ControllerAdvice
public class DemoControllerAdvisor {

    //모든 Controller에서 일어나는 DemoException에 대해 전역적으로 예외처리
    @ExceptionHandler(value = DemoException.class)
    public String handleDemoExceptionForGlobal(DemoException e) {
        log.error(e.getMessage());
        return "/error/404";
    }
}
~~~

### Controller 클래스 내에 @ExceptionHandler, @ControllerAdvice 클래스 내의 @ExceptionHandler 둘 중 뭐가 먼저 실행 될까? 그리고 둘 다 실행 될까?

- @Controller내의 @ExceptionHandler로 예외처리를 하게 되면 거기서 예외처리가 끝난다. 더 상위로 Exception을 throw하더라도 @ControllerAdvice의 @ExceptionHandler에서 예외처리를 하지 않는다.


### HandlerExceptionResolver를 이용한 처리

- DispatcherServlet내에서 예외 발생 시, resolverException 메소드를 구현한 HandlerExceptionResolver들이 실행 계획에 따라 처리 되며 예외를 처리 하게 된다. 사실 위에서 본 2가지 방식의 예외처리도 HandlerExceptionResolver를 이용한 예외 처리 방법이다.

~~~ java
public interface HandlerExceptionResolver {
    @Nullable
    ModelAndView resolveException(HttpServletRequest var1, HttpServletResponse var2, @Nullable Object var3, Exception var4);
}
~~~