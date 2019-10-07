#### @Bean vs @Component
- Bean과 Component 모두 spring(ioc) container에 bean을 등록하여 메타데이터를 등록하는 어노테이션이다.

#### @Bean
- Bean은 method 위에 선언 
- @Bean은 @Configuration으로 선언된 클래스 내에 있는 메소드를 정의할 때 사용한다. 이 메소드가 반환하는 객체가 bean이 된다.
- @Bean어노테이션의 경우 개발자가 직접 제어가 불가능한 외부 라이브러리등을 Bean으로 만들려할 때 사용된다
~~~ java
@Configuration
public class ApplicationConfig {    
    @Bean
    public ArrayList<String> array(){
        return new ArrayList<String>();
    }   
}
~~~
- 위와 같이 ArrayList같은 라이브러리등을 Bean으로 등록하기 위해서는 별도로 해당 라이브러리 객체를 반환하는 Method를 만들고 @Bean어노테이션을 붙혀주면 된다. 위의 경우 Bean어노테이션에 아무런 값을 지정하지 않았으므로 Method 이름을 CamelCase로 변경한 것이 Bean id로 등록된다. (ex. 메소드 이름이 arrayList()인 경우 arrayList가 Bean id)

~~~ java
@Configuration
public class ApplicationConfig {    
    @Bean(name="myarray")
    public ArrayList<String> array(){
        return new ArrayList<String>();
    }   
}
~~~
- 위와 같이 @Bean어노테이션에 name이라는 값을 이용하면 자신이 원하는 id로 Bean을 등록할 수 있다. 어노테이션 안에 값을 입력하지 않을 경우 메소드의 이름을 CamelCase로 변경한것이 Bean의 id가 된다.


#### @Component 
- Component는 class 위에 선언
- @Component 어노테이션의 경우 개발자가 직접 작성한 Class를 Bean으로 등록하기 위한 어노테이션이다. 

~~~ java
@Component
public class Student {
    public Student() {
        System.out.println("hi");
    }
}
~~~
- Student Class는 개발자가 사용하기 위해서 직접 작성한 Class이다 이러한 클래스를 Bean으로 등록하기 위해 상단에 @Component어노테이션을 사용한것을 볼 수 있다.
- @Component를 사용한 Bean의 의존성 주입은 @AutoWired 어노테이션을 이용하여 할 수 있다.
- @Autowired 어노테이션의 경우 형(타입)을 통해 해당 자리에 들어올 객체를 판별하여 주입해준다. 따라서 해당 자리에 들어올 수 있는 객체가 여러개인 경우, 즉 다형성을 띄고있는 객체타입에 @Autowired를 사용한 경우에는 @Qualifier("Bean이름") 을 이용하여 해당 자리에 주입될 Bean을 명시해주어야 한다. 





### 참조
https://galid1.tistory.com/494