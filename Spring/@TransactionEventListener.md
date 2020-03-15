### @TransactionEventListener
- @TransactionEventListener는 @Transactional이 붙은 메서드의 이벤트 퍼블리셔를 통해 발급된 이벤트를 리스닝한다.
- 이벤트가 발생한 트랜잭션이 종료되면 실행된다.
- @EventListener 는 트랜잭션 범위 내에서 동기적으로 실행되고, @TransactionalEventListener는 커밋 전/후 등을 자유롭게 지정할 수 있다

``` java
@Service
@Transactional
public class ProductService {
    @Autowired
    private ProductRepository productRepository;
    @Autowired
    private ApplicationEventPublisher eventPublisher;


    public void insert(){
        Product product = new Product("인서트 테스트");
        productRepository.save(product);
        eventPublisher.publishEvent(product);
    }

}
```
``` java
@Slf4j
@Component
public class ProductTransactionListener {

    /*
        phase : COMMIT 이후에 실행할 것인지 이전에 실행할 것인지 실행 순서를 제어할 수 있다
        fallbackExecution : 트랜잭션과는 무관하게 항상 실행할 것인지
        condition : 이벤트 리스너가 작동하는 조건 설정
     */

    @TransactionalEventListener(phase = TransactionPhase.BEFORE_COMMIT, fallbackExecution = true, condition = "#product.content == '인서트 테스트'")
    void listenBeforeEvent(Product product) {
        log.info("TransactionalEventListener 이벤트 발생 : {}", "BEFORE_COMMIT");
        log.info("이벤트 : {}", product);
    }

    @TransactionalEventListener(phase = TransactionPhase.AFTER_COMMIT, fallbackExecution = true)
    void listenAfterEvent(Product product) {
        log.info("TransactionalEventListener 이벤트 발생 : {}", "AFTER_COMMIT");
        log.info("이벤트 : {}", product);
    }
}
```