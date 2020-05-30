#### 클린 아키텍처(The Clean Architecture) By Uncle Bob
- 프레임워크에 독립적이어야 한다.
    - 아키텍처는 프레임워크에 의존하면 안된다! 최소한의 노력으로 새로운 프레임워크를 적용할 수 있어야 한다.
- 테스트가 용이해야 한다.
- UI에 독립적이어야 한다.
- 데이터베이스에 독립적이어야 한다.
- 외부 기능에 독립적이어야 한다.
- Entity 와 Use Case
    - Entity 와 Use Case 가 어플리케이션의 핵심이다. 아키텍처에 대해서 얘기할 때 이 것들이 존재하는 레이어가 가장 중요하다. 
- Adapter 와 Converter 의 필요성
    - Adapter 와 Converter 는 각각의 레이어가 협력을 할 때 레이어 내부의 세부 사항이 다른 레이어로 전파되지 않도록 하는 역할을 한다. 
- 의존성이 역전되면 안된다.
    - 고수준의 모듈이 저수준 모듈에 의존성을 가지면 안된다는 것을 말한다.



#### 참조
https://medium.com/@younghyun/%ED%81%B4%EB%A6%B0-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98-%ED%8C%8C%ED%8A%B81-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-vs-%EB%8F%84%EB%A9%94%EC%9D%B8-236c7008ac83