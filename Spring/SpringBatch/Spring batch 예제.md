### Spring batch 예제

~~~ java
@Configuration
public class SimpleConfiguration {

    @Autowired
    private JobBuilderFactory jobBuilderFactory;

    @Autowired
    private StepBuilderFactory stepBuilderFactory;

    @Bean
    public Job job() {
        return jobBuilderFactory.get("simple-job")
                .start(step())
                .build();
    }

    @Bean
    public Step step() {
        return stepBuilderFactory.get("simple-step")
                .<String, StringWrapper>chunk(10)
                .reader(itemReader())
                .processor(itemProcess())
                .writer(itemWriter())
                .build();
    }

    private ItemReader<String> itemReader() {
        List<String> list = new ArrayList<>();

        for (int i = 0; i < 100; i++) {
            list.add("test" + i);
        }

        return new ListItemReader(list);
    }

    private ItemProcessor<String, StringWrapper> itemProcess() {
        return StringWrapper::new;
    }

    private ItemWriter<StringWrapper> itemWriter() {
        return System.out::println;
    }

    private class StringWrapper {
        private String value;

        StringWrapper(String value) {
            this.value = value;
        }

        public String getValue() {
            return value;
        }

        @Override
        public String toString() {
            return String.format("i'm %s", getValue());
        }
    }
}
~~~

- 위 예제는 아주 단순한 batch다.

1. Job은 하나의 Step을 갖고 있으며, Step의 ItemReader는 ArrayList에 100개의 String value를 담고 있다. (읽기)

2. ItemProcessor는 ItemReader에서 반환된 String List를 StringWrapper 클래스로 wrapping 한다. (가공)

3. ItemWriter는 ItemProcessor를 통해 StringWrapper로 반환된 List를 System.out.println으로 로그를 찍는다. (쓰기)



### 참조
https://blog.woniper.net/357