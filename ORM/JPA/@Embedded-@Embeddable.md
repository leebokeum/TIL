### @Embedded, @Embeddable
- 자바의 기본타입외에 사용자가 정의한 타입을 엔티티의 필드로 넣어야 할때 @Embedded를 사용한다.
- 예를 들어서 주소라는 값을 하나의 엔티티에 매핑하고 싶은데, 도시명,구,동 이렇게 세가지의 기본타입(String)의 값을 매핑해야한다면 과연 3개를 쭉 나열하는 것이 객체지향적인 것인지 3개를 하나의 객체로 묶어서 하나의 객체로 값을 매핑하는 것이 객체지향적인 것인지 고민을 하자만 바로 후자일 것이다

``` java
@Entity
@Table(name = "user")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long uid;
​
    private String name;
​
    private String phoneNum;
​
    @Embedded
    private Address address;
}

@Embeddable
public class Address {
    private String zipCode;
    private String address1;
    private String address2;
}
```
![alt text](/image/ORM/embedded2.png )


### @AttributeOverride
- @Embedded를 이용해 객체로 Entity의 Column을 표현한다면, Column 이름이 중복되는 문제가 발생하기도 한다. 예를 들어 앞서 생성한 주소(Address) 객체 필드를 여러개를 생성한다면 이럴 때는 @AttributeOverride 를 사용한다.

``` java
@Embedded
@AttributeOverride(name = "zipCode", column = @Column(name = "home_zipCode"))
@AttributeOverride(name = "address1", column = @Column(name = "home_address1"))
@AttributeOverride(name = "address2", column = @Column(name = "home_address2"))
private Address homeAddress;
​
@Embedded
@AttributeOverride(name = "zipCode", column = @Column(name = "company_zipCode"))
@AttributeOverride(name = "address1", column = @Column(name = "company_address1"))
@AttributeOverride(name = "address2", column = @Column(name = "company_address2"))
private Address companyAddress;
```
![alt text](/image/ORM/embedded.png )
