### @EntityListeners
- 엔티티를 DB에 적용하기 이전 이후에 커스텀 콜백을 요청할 수 있는 어노테이션이다.

### 종류
- PreUpdate : 업데이트 이전에 실행
- PostUpdate : 업데이트 이후에 실행
- PreRemove : 삭제되기전 실행
- PostRemove : 삭제 후에 실행
- PrePersist : 저장 전에 실행
- PostPersist : 저장 이후에 실행

``` java
@Entity
@Table(name = "product_item")
@EntityListeners(ProductListener.class)
public class Product {
...
}
```

``` java
@Slf4j
public class ProductListener {
    @PreUpdate
    void onPreUpdate(Product product) {
        log.info("이벤트 발생 : {}", "update 실행전");
        log.info("이벤트 : {}", product);
    }

    @PostUpdate
    void onPostUpdate(Product product) {
        log.info("이벤트 발생 : {}", "update 실행후");
        log.info("이벤트 : {}", product);
    }

    @PrePersist
    void onPrePersist(Product product) {
        log.info("이벤트 발생 : {}", "insert 실행전");
        log.info("이벤트 : {}", product);
    }

    @PostPersist
    void onPostPersist(Product product) {
        log.info("이벤트 발생 : {}", "insert 실행후");
        log.info("이벤트 : {}", product);
    }

    @PreRemove
    void onPreDelete(Product product) {
        log.info("이벤트 발생 : {}", "delete 실행전");
        log.info("이벤트 : {}", product);
    }

    @PostRemove
    void onPostDelete(Product product) {
        log.info("이벤트 발생 : {}", "delete 실행후");
        log.info("이벤트 : {}", product);
    }
}
```


### 주의 사항
- 이벤트는 repository 호출 시점이 아니다. 트랜잭션 종료 후 실제 COMMIT이 되고 난 후다.
Listener Class는 스프링 기반이 아니라 javax.persistence 를 이용하는 것이므로 빈이 아니다.
빈이 아니라는 말은 Listener 안에서 @Autowired 같은 어노테이션으로 빈을 주입받을 수 없다는 말을 의미한다. 그래서 Listener안에서 빈을 사용하고 싶다면 애플리케이션 컨텍스트에서 직접 빈을 얻어와야한다.

