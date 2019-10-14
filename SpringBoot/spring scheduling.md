### spring에서 Scheduling 간단하게 사용하기
- Spring에서는 일정한 주기마다 작업을 실행할 수 있는 Schedule기능이 포함되어있다.
- 간략한 설정과 어노테이션만으로 편리하게 설정이 가능한 장점을 가지고 있다. 

- @EnableScheduling 먼저 선언해준다.
~~~ java
@EnableScheduling
@SpringBootApplication
public class Application {
	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}
}
~~~

- spring에서는 @Scheduled 어노테이션을 bean scanning 과정에서 자동으로 찾아서 해당 설정대로 주기적으로 실행해준다.

~~~ java
// 1초마다 호출 
@Scheduled(fixedDelay = 1000)
public void simplePrintln(){
    System.out.println(new Date());
} 
~~~

- 아래와같이 cron식을 넣어줄 수도 있다.
~~~ java
@Scheduled(cron = "${job.cron.rate}")
public void simplePrintln(){
    System.out.println(new Date());
}
~~~