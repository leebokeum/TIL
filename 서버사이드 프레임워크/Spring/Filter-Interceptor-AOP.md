### filter, intercptor, aop 차이
![alt text](/image/spring/filter-inter-aop.png )

- 실행순서를 보면 Filter가 가장 밖에 있고 그안에 Interceptor, 그안에 AOP가 있는 형태이다.
- 따라서 요청이 들어오면 Filter → Interceptor → AOP → Interceptor → Filter 순으로 거치게 된다.

1. 서버를 실행시켜 서블릿이 올라오는 동안에 init이 실행되고, 그 후 doFilter가 실행된다. 
2. 컨트롤러에 들어가기 전 preHandler가 실행된다
3. 컨트롤러에서 나와 postHandler, after Completion, doFilter 순으로 진행이 된다.
4. 서블릿 종료 시 destroy가 실행된다.


### Aop에 대해서만 추가 설명
- Interceptor나 Filter와는 달리 메소드 전후의 지점에 자유롭게 설정이 가능하다.
- Interceptor와 Filter는 주소로 대상을 구분해서 걸러내야하는 반면, AOP는 주소, 파라미터, 애노테이션 등 다양한 방법으로 대상을 지정할 수 있다.
- AOP의 Advice와 HandlerInterceptor의 가장 큰 차이는 파라미터의 차이다.
- Advice의 경우 JoinPoint나 ProceedingJoinPoint 등을 활용해서 호출한다.
- 반면 HandlerInterceptor는 Filter와 유사하게 HttpServletRequest, HttpServletResponse를 파라미터로 사용한다.

### AOP의 포인트컷
@Before: 대상 메서드의 수행 전
@After: 대상 메서드의 수행 후
@After-returning: 대상 메서드의 정상적인 수행 후
@After-throwing: 예외발생 후
@Around: 대상 메서드의 수행 전/후


### 참고
https://goddaehee.tistory.com/154 [갓대희의 작은공간]