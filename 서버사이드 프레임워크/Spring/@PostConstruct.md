### @PostConstruct
- 초기화 메소드는 오브젝트가 생성 되고, DI 작업을 마친 다음 실행 되는 메소드이다.
- 대부분 초기화 작업들은 생성자로 많이들 한다. 하지만 DI를 통해서 빈이 주입된 후에 초기화 할 작업이 있다면? 생성자로 하면 오류가 난다 그럴때 사용해서 초기화를 진행하면 된다.

``` java
@Controller
public class ItJava {

  @PostConstruct
  public void postConstruct() {
    System.out.println("postConstruct");
  }
}
```