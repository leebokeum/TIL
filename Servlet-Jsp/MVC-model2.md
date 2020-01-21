### model2
- 모델 2는 모든 처리를 JSP 페이지 하나가 담당하는것과는 달리 JSP페이지와 서블릿, 그리고 로직을 위한 클래스가 나뉘어 브라우저 요청을 처리한다.
- 요청이 들어오면 요청에 대한 로직 처리는 이를 처리할 모델(Model)인 서비스클래스 혹은 자바빈이 담당하고, 요청 결과는 유저에게 결과를 보여줄 뷰(View)단인 JSP에 출력되며,  이를 위한 모든 흐름 제어는 컨트롤러(Controller)인 서블릿에서 담당한다.

### 장점
- 출력을 위한 뷰 코드와 로직 처리를 위한 자바 코드를 분리하기 때문에 JSP 모델1에 비해 코드가 복잡하지 않다.
- 뷰, 로직처리에 대한 분업이 용이하다.
- 기능에 따라 분리되어있기 때문에 유지보수가 용이하다.

### 단점
- 구조가 복잡하여 습득이 어렵고 작업량이 많다.
- JAVA에 대한 깊은 이해가 필요하다.