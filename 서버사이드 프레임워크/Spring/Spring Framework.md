### Spring Framework란
- 자바 엔터프라이즈 개발을 편하게 해주는 오픈소스 경량급 애플리케이션 프레임워크

#### DI(Dependency Injection, 의존성 주입)
- 객체 자체가 아니라 Framework에 의해 객체의 의존성이 주입되는 설계 패턴
    - Framework에 의해 동적으로 주입되므로 여러 객체 간의 결합이 줄어든다.
    - Dependency Injection은 Spring Framework에서 지원하는 IoC의 형태 
- 스프링의 모토는 결국 "기본으로 돌아가자"이다. 자바의 기본인 객체지향에 충실한 설계가 가능하도록 단순한 오브젝트로 개발할 수 있고, 객체지향의 설계 기법을 잘 적용할 수 있는 구조를 만들기 위해 DI 같은 유용한 기술을 편하게 적용하도록 도와주는 것이 스프링의 기본 전략

#### IoC(제어의 역전)
- 프로그램 제어권을 framework가 가져가는 것 
    - 개발자가 모든 제어의 중심이지만 코드 전체에 대한 제어는 framework가 한다.
    - 개발자가 설정(xml, annotation 등)만 하면 Container가 알아서 처리한다.
    - 즉, 우리는 Framework 속에서 프로그래밍을 하는 것. 

Dependency Injection(의존성 주입)과 Inversion Of Control(제어의 역전)은 같은 의미로 사용된다.


#### Spring Container
- Spring Framework의 핵심 컴포넌트
    - Container는 DI를 사용하여 응용 프로그램을 구성하는 bean 객체를 관리한다.
- bean을 관리하는 책임이 있다.
    - 객체(bean)를 생성하고
    - 객체들을 함께 묶고
    - 객체들을 구성하고
    - 객체들의 전체 수명주기(lifecycle)를 관리
    
#### Spring Container 설정 방법 
1. XML
    - 빈 객체 정의 (Bean Definition)
    - 의존성 주입 (Dependency Injection)
2. Java Annotations
3. Java Code


#### 키워드
경량, DI, AOP, Container, framework


### 참조
https://12bme.tistory.com/157
https://gmlwjd9405.github.io/2018/11/09/dependency-injection.html