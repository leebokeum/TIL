#### REST API
- Representational State Transfer라는 용어의 약자
    - 자원(RESOURCE) - URI
    - 행위(Verb) - HTTP METHOD
    - 표현(Representations)


#### REST API 디자인 설계
- **URI는 정보의 자원을 표현해야 한다.**
    - 자원에 대한 행위는 URI에 포함하지 않는다.
- **자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)으로 표현한다.**
    - POST: 리소스 추가
    - GET: 리소스 조회
    - PUT: 리소스 변경
    - DELETE: 리소스 삭제

- 자원을 표현하는 **Colllection** 과 **Document**
    - Collection과 Document에 대해 알면 URI 설계가 한 층 더 쉬워진다. DOCUMENT는 단순히 문서로 이해해도 되고, 한 객체라고 이해해도 무방하다. 컬렉션은 문서들의 집합, 객체들의 집합이라고 생각하면 된다. 컬렉션과 도큐먼트는 모두 리소스라고 표현할 수 있으며 URI에 표현된다.
        ~~~ java
        http:// restapi.example.com/sports/soccer
        위 URI를 보면 sports라는 컬렉션과 soccer라는 도큐먼트로 표현되고 있다고 생각하면 된다.
        http:// restapi.example.com/sports/soccer/players/13
        sports, players 컬렉션과 soccer, 13(13번인 선수)를 의미하는 도큐먼트로 URI가 이루어지게 된다. 여기서 중요한 점은 컬렉션은 복수로 사용하고 있다는 점이다. 좀 더 직관적인 REST API를 위해서는 컬렉션과 도큐먼트를 사용할 때 단수 복수도 지켜준다면 좀 더 이해하기 쉬운 URI를 설계할 수 있다.
        ~~~

- 리소스명은 명사를 사용
    - 사용자 정보를 가져올때
        ~~~ java
        안좋은 예시
        GET /users/show/1 (x)
        ~~~

        ~~~ java
        좋은 예시
        GET /users/1 (o)
        ~~~
        - GET이라는 method로 충분히 표현가능 하다.


- URI 뒤에 붙는 쿼리스트링은
    - URI쿼리 부분으로 컬렉션이나 스토어를 필터링할 때 사용
        ~~~ java
        GET /users
        GET /users?role=admin
        ~~~

    - URI쿼리는 컬렉션이나 스토어의 결과를 페이지로 구분하여 나타내는데 사용
        ~~~ java
        /resources?pageSize=10&pageStartIndex=0
        페이징을 위한 정보 전달
        /dogs?color=red&state=running&location=park
        구체적인 검색 제약사항 전달
        ~~~
 
- 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용
    ~~~ java
    http://restapi.example.com/houses/apartments
    http://restapi.example.com/animals/mammals/whales
    ~~~
- 하이픈(-)은 URI 가독성을 높이는데 사용
- 밑줄(_)은 URI에 사용하지 않는다.
- URI에는 소문자가 적합하다. 
    - RFC 3986은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문이다.
        ~~~ java
        http://api.example.restapi.org/my-folder/my-doc
        HTTP://API.EXAMPLE.RESTAPI.ORG/my-folder/my-doc

        위의 두 URI는 같은 URI입니다. 호스트에서는 대소문자를 구별하지 않기 때문.

        http://api.example.restapi.org/my-folder/my-doc
        http://api.example.restapi.org/My-Folder/my-doc

        하지만 위의 두 URI는 다른 URI입니다. 뒤에 붙는 path가 대소문자로 구분되기 때문.
        ~~~
- 파일 확장자는 URI에 포함시키지 않는다.
    ~~~ java
    http://restapi.example.com/members/soccer/345/photo.jpg (X)
    ~~~
- Device 환경과 버전정보에 따라서 구분할 때
    - Header의 User-Agent 값을 참조
    - Header의 Accept 헤더를 이용해서 요청 환경에서 정보의 버전과 포맷을 지정
        - 클라이언트가 정보를 json으로 받을지, xml로 받을지 선택

#### What about actions that don't fit into the world of CRUD operations?
##### (CRUD와 같은 세계관에 맞지 않는 행위는 어떻게 표현하나?)
This is where things can get fuzzy. There are a number of approaches:
1. Restructure the action to appear like a field of a resource. This works if the action doesn't take parameters. For example an activate action could be mapped to a boolean activated field and updated via a PATCH to the resource.

2. Treat it like a sub-resource with RESTful principles. For example, GitHub's API lets you star a gist with PUT /gists/:id/star and unstar with DELETE /gists/:id/star.

3. Sometimes you really have no way to map the action to a sensible RESTful structure. For example, a multi-resource search doesn't really make sense to be applied to a specific resource's endpoint. In this case, /search would make the most sense even though it isn't a resource. This is OK - just do what's right from the perspective of the API consumer and make sure it's documented clearly to avoid confusion.
 

#### 참조
https://meetup.toast.com/posts/92
https://spoqa.github.io/2012/02/27/rest-introduction.html
https://restful-api-design.readthedocs.io/en/latest/methods.html
https://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api#restful