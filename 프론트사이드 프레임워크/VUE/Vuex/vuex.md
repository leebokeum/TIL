### vuex를 왜 사용하나
- 무수히 많은 컴포넌트의 데이터를 관리하기 위한 상태 관리 패턴이자 라이브러리
- React의 Flux 패턴에서 기인함

### Flux란?
- MVC 패턴의 복잡한 데이터 흐름 문제를 해결하는 개발 패턴 - Undirectional data flow
    - 아래의 순서로 단일 방향으로만 흐름이 흘러간다.
    1. actions : 화면에서 발생하는 이벤트 또는 사용자의 입력
    2. dispatcher : 데이터를 변경하는 방법, 메서드(model을 바꾸기 위한 역할)
    3. model : 화면에 표시할 데이터
    4. view : 사용자에게 비춰지는 화면, 화면에서 다시 action을 호출하게 된다. 그러면 다시 1->2->3->4 한 방향 흐름.



#### 참조
https://steemit.com/kr/@stepanowon/vuex