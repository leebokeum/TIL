### Entity
Entity 클래스는 DB의 테이블내에 존재하는 컬럼만을 속성(필드)으로 가지는 클래스를 말한다. 엔티티 클래스는 상속을 받거나 구현체여서는 안되며, 테이블내에 존재하지 않는 컬럼을 가져서도 안된다.

``` java
@Entity
class Article {
    private String title;
    private String contents;
    private String writer;
}
```

### VO(Value Object)
VO(Value Object)는 말 그대로 값 객체라는 의미를 가지고 있다. VO의 핵심 역할은 equals()와 hashcode() 를 오버라이딩 하는 것이다. 즉, VO 내부에 선언된 속성(필드)의 모든 값들이 VO 객체마다 값이 같아야, 똑같은 객체라고 판별한다.

```java
@Getter @Setter
@Alias("article")
class ArticleVO {
    private Long id;
    private String title;
    private String contents;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Article article = (Article) o;
        return Objects.equals(id, article.id);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }
}
```

### DTO(Data Transfer Object)
DTO(Data Transfer Object)는 데이터 전송(이동) 객체라는 의미를 가지고 있다. DTO는 주로 비동기 처리를 할 때 사용한다. 비동기 처리에서도 JSON 데이터 타입으로 변환해야하는 경우, Spring Boot에서 Jackson 라이브러리를 제공하는데, Jackson은 ObjectMapper를 사용해서 별다른 처리 없이도 객체를 JSON 타입으로 변환시켜 준다.

```java
@Getter @Setter
class ArticleDTO {
  private String title;
  private String content;
  private String writer;
}
```



## 참조
https://medium.com/webeveloper/entity-vo-dto-666bc72614bb