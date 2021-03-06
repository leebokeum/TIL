### Spring과 SpringBoot의 차이
- 스프링 기반 애플리케이션은 많은 환경설정을 포함한다.
- 스프링 프레임워크는 기능이 많은만큼 환경설정이 복잡한 편이다. 
- 스프링부트는 자동설정(AutoConfiguration)을 이용하였고 어플리케이션 개발에 필요한 모든 내부 디펜던시를 관리한다. 개발자가 해야하는건 단지 어플리케이션을 실행할 뿐이다. 스프링의 jar파일이 클래스 패스에 있는 경우 Spring Boot는 Dispatcher Servlet으로 자동 구성한다. 마찬가지로 만약 Hibernate의 jar파일이 클래스 패스내에 존재한다면 이를 datasource로 자동설정하게 된다. 스프링부트는 미리설정된 스타터 프로젝트를 제공한다.

- 스프링 부트는 의존성의 복잡도를 줄이기 위해서 SpringBoot Starter라고 불리는 것을 도입했다.
- 스프링부트는 별도의 서버 설치 없이 embeded tomcat이 자동으로 실행한다.
- 통합된 설정파일인 application.yml으로 쉽게 간단하게 사용할 수 있다.