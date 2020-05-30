### mappedBy 와 @JoinColumn 의 차이

### @JoinColumn
@JoinColumn 어노테이션은 외래 키를 매핑 할 때 사용한다. name 속성에는 매핑 할 외래 키 이름을 지정한다.

- 단방향은 한 쪽의 엔티티가 상대 엔티티를 참조하고 있는 상태이다.

@ManyToOne - 단방향
``` java
@Entity
@Table( name="book")
public class Book {
	@Id
	@Column(name="no")
	@GeneratedValue( strategy = GenerationType.IDENTITY )
	private Integer no;
	
	@Column(name="title", nullable=false, length=200)
	private String title;
	
	@ManyToOne
	@JoinColumn(name ="category_no")
	private Category category;
	
	// getter , setter 생략
	
}
```

### mappedBy
데이터베이스 테이블의 N:1, 1:N 관계에서는 항상 N 쪽이 외래키를 가진다. N 쪽인 @ManyToOne은 항상 연관관계의 주인이 되므로 mappedBy를 설정할 수 없다. 따라서 @ManyToOne에는 mappedBy 속성이 없다.

-  주인은 mappedBy 속성을 사용하지 않는다.
-  주인이 아니면 mappedBy 속성을 사용해서 속성의 값으로 연관관계의 주인을 정할 수 있다.

@OnetoMany로 양방향 맺기
```  java
@Entity
@Table(name="category")
public class Category {
	@Id
	@Column(name="no")
	@GeneratedValue(strategy=GenerationType.IDENTITY)
	private Integer no;
	
	@Column( name="name", nullable=false, length=100 )
	private String name;

	@OneToMany(mappedBy="category")
	private List<Book> books = new ArrayList<Book>();
	
	// getter , setter 생략
	
}
```