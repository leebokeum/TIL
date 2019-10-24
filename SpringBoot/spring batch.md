#### 스프링 배치
- 스프링 부트는 배치 스케쥴러를 제공하지 않는다. 따라서 배치 처리 기능만 제공하여 스케쥴링 기능은 스프링에서 제공하는 쿼치 프레임워크 등을 이용해야한다.

![alt text](../image/springboot/batch.png)


### 특징
- Transaction management
- Chunk based processing
- Declarative I/O to read and write resources
- Start/Stop/Restart
- Retry/Skip
- Web based administration interface (With Spring Batch Admin)

### 적용
`@EnableBatchProcessing` 어노테이션을 필수로 선언해야 spring batch기능이 활성화 된다.

~~~ java
@SpringBootApplication
@EnableBatchProcessing
public class SchedulerApplication {
    public static void main(String[] args) {
        SpringApplication.run(SchedulerApplication.class, args);
    }
}
~~~

### Job 설정
- Spring Batch에서 Job은 하나의 배치 작업 단위를 얘기하는데요.
Job 안에는 아래처럼 여러 Step이 존재하고, Step 안에 Tasklet 혹은 Reader & Processor & Writer 묶음이 존재한다.

### Step
- 읽기(read) : 데이터 저장소(일반적으로 데이터베이스)에서 특정 데이터 레코드를 읽는다.
- 처리(processing) : 원하는 방식으로 데이터 가공/처리 한다.
- 쓰기(write) : 수정된 데이터를 다시 저장소(데이터베이스)에 저장한다.

![Prunus](https://t1.daumcdn.net/cfile/tistory/99E8E3425B66BA2713)

- Tasklet 하나와 Reader & Processor & Writer 한 묶음이 같은 레벨

~~~ java
@Slf4j // log 사용을 위한 lombok 어노테이션
@RequiredArgsConstructor // 생성자 DI를 위한 lombok 어노테이션
@Configuration //Spring Batch의 모든 Job은 @Configuration으로 등록해서 사용합니다.
public class JobConfiguration {
    private final JobBuilderFactory jobBuilderFactory; // 생성자 DI 받음
    private final StepBuilderFactory stepBuilderFactory; // 생성자 DI 받음

    @Bean
    public Job simpleJob() {
        return jobBuilderFactory.get("simpleJob") //simpleJob 이란 이름의 Batch Job을 생성합니다.
                .start(simpleStep1())
                .build();
    }

    @Bean
    public Step simpleStep1() {
        return stepBuilderFactory.get("simpleStep1") //simpleStep1 이란 이름의 Batch Step을 생성합니다.
                .tasklet((contribution, chunkContext) -> {
                    log.info(">>>>> This is Step1");
                    //Step 안에서 수행될 기능들을 명시합니다.
                    //Tasklet은 Step안에서 단일로 수행될 커스텀한 기능들을 선언할때 사용합니다.
                    //여기서는 Batch가 수행되면 log.info(">>>>> This is Step1") 가 출력되도록 합니다.

                    return RepeatStatus.FINISHED;
                })
                .build();
    }
}
~~~

### 참조
https://cheese10yun.github.io/spring-batch-basic/
https://jojoldu.tistory.com/325