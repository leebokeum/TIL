### model1
- 모델 1은 뷰와 로직을 모두 JSP 페이지 하나에서 처리하는 구조를 말한다.
- JSP 페이지 내에 로직 처리를 위한 자바 코드가 출력을 위한 코드와 함께 섞여 삽입된다. 브라우져에서 요청이 들어오면 JSP 페이지는 자신이 직접 자바빈이나 따로 작성한 서비스 클래스를 이용하여 작업을 처리하고, 그 처리한 정보를 클라이언트에 출력한다. 

### 장점
- 구조가 단순하여 익히기가 쉽다.
- 위와 같은 이유로 숙련된 개발자가 아니더라도 구현이 용이하다.

### 단점
- 출력을 위한 뷰 코드와 로직 처리를 위한 자바 코드가 함께 섞이기 때문에 JSP 코드 자체가 복잡해진다.
- JSP 코드에서 백엔드와 프론트엔드가 혼재되기 때문에 분업이 용이하지 않다.
- 코드가 복잡해져 유지보수가 어렵다