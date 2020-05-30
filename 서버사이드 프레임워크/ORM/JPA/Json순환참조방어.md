### Json 순환참조
- JPA는 ORM이기 때문에 RDB를 관리하는데 있어서 양방향 참조를 필요로 한다.
- RESTFul API 서버를 구현하는데 있어서 문제가 생긴다.


### @JsonIgnore, @JsonManagedReference, @JsonBackReference
- @JsonIgnore를 사용하는 방법이 있고 @JsonManagedReference와 @JsonBackReference를 사용하는 방법이 있다. 표면적으로 두 방법 모두 순환참조를 방어하는 형태이지만 본질적으로 약간의 차이가 있다. @JsonIgnore의 경우는 실제로 property에 null을 할당하는 방식이고 @JsonManagedReference와 @JsonBackReference는 본질적으로 순환참조를 방어하기 위한 Annotation이다. 
- json serialize 과정에서 null로 세팅하고자 하면 @JsonIgnore 사용하면 되고, 순환참조에 대한 문제를 해결하고자 한다면 부모 클래스측에 @JsonManagedReference를, 자식측에 @JsonBackReference를 Annotation에 추가해주면 된다.

 
 ## 참조
 http://stackoverflow.com/a/37393711