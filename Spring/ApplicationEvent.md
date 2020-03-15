### ApplicationEvent
Spring에는 ApplicationContext를 활용해서 Event를 발생 시킬수 있다. ApplicationEvent를 구현하기 위해서는 세가지만 알면 된다.

1. 이벤트 발신자 : ApplicationEventPublisher 인터페이스 혹은 ApplicatonContext의 publishEvent를 활용해서 이벤트를 발생시킨다. (ApplicationContext는 ApplicationEventPublisher 상속받고 있다.)
2. 이벤트 수신자 : ApplicationListener 인터페이스를 통해 이벤트를 수신할 수 있다.
3. 이벤트 : ApplicationEvent를 상속받아 구현하면 된다.


### 1. 이벤트 발신자(ApplicationEventPublisher)
``` java
public class EventPublisher implements ApplicationEventPublisherAware {
    private List<String> blackList;
    private ApplicationEventPublisher publisher;

    public void setBlackList(List<String> blackList) {
        this.blackList = blackList;
    }

    public void setApplicationEventPublisher(ApplicationEventPublisher publisher) {
        this.publisher = publisher;
    }

    public void publishEvent(String address, String text) {
        if (blackList.contains(address)) {
            BlackListEvent event = new BlackListEvent(this, address, text);
            publisher.publishEvent(event);
            return;
        }
    }
}
```

### 2. 이벤트 수신자(ApplicationListener)
``` java
//ApplicationListener를 구현한 리스너
@Slf4j
public class EventListener implements ApplicationListener<BlackListEvent> {

    @Order(3)
    @Override
    public void onApplicationEvent(BlackListEvent event) {
        log.info("이벤트 발생 시간 : {}", event.getTimestamp());
        log.info("관리자에게 알리자 : {} " , "블락 리스트 이벤트 발생!!");
    }
}

//어노테이션을 활용한 리스너
@Slf4j
public class AnnotationListener {

    //@EventListener 만 선언해주면 된다. 인터페이스를 구현하지 않아도 된다.
    //event안에 text가 foo인 것만 리스너를 호출한다.
    //이벤트 리스너의 순서도 정할 수 있다.
    @EventListener(condition = "#event.text == 'test'")
    @Order(1)
    public void processBlackListEvent(BlackListEvent event) {
        log.info("이벤트 발생 시간 : {}", event.getTimestamp());
        log.info("관리자에게 알리자 : {} " ,"test가 들어간 단어 블락리스트 이벤트 발생!!");
    }

    @EventListener
    @Async
    @Order(2)
    public void processBlackListEventAsync(BlackListEvent event) {
        log.info("이벤트 발생 시간 : {}", event.getTimestamp());
        log.info("관리자에게 알리자 : {} " ,"블락 리스트 비동기 이벤트 발생!!");
    }
```

### 3. 이벤트(ApplicationEvent)
``` java
public class BlackListEvent extends ApplicationEvent {
    private final String address;
    public final String text;

    /**
     * Create a new {@code ApplicationEvent}.
     *
     * @param source the object on which the event initially occurred or with
     *               which the event is associated (never {@code null})
     */
    public BlackListEvent(Object source, String address, String text) {
        super(source);
        this.address = address;
        this.text = text;
    
```

### 실행
``` java
@SpringBootApplication
public class SpringbootEventlistenerExampleApplication {

    @Bean
    public EventPublisher eventPublisher(){
        EventPublisher eventPublisher = new EventPublisher();
        eventPublisher.setBlackList(Arrays.asList("test@test.com", "wonwoo@test.com", "5151@test.com"));
        return eventPublisher;
    }

    @Bean
    public EventListener eventListener(){
        EventListener eventListener = new EventListener();
        return eventListener;
    }

    @Bean
    public AnnotationListener annotationListener(){
        AnnotationListener annotationListener = new AnnotationListener();
        return annotationListener;
    }

    public static void main(String[] args) {
        ApplicationContext run = SpringApplication.run(SpringbootEventlistenerExampleApplication.class, args);
        //Spring 4.2 이전에는 어노테이션이 없어서 직접 상속받아 구현
        EventPublisher bean = run.getBean(EventPublisher.class);
        bean.publishEvent("wonwoo@test.com", "hi wonwoo");
        bean.publishEvent("wonwoo@test.com", "test");
    }
}
```

## 참조
http://wonwoo.ml/index.php/post/1070