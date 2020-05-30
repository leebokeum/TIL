#### Layered Architecture
- User Interface
    - 사용자에게 정보 출력
    - 사용자의 요청을 해석하여 하위 레이어에 전달
- Application
    - 어플리케이션의 상태를 관리 / Thin Layer
    - 비즈니스 로직/객체 상태를 포함하지 않음
    - 실제 비즈니스 처리는 도메인에 요청
- Domain
    - 도메인에 대한 정보를 포함
    - 비즈니스 객체의 상태를 포함
    - 비즈니스 로직을 제공
- Infrastructure
    - 다른 레이어를 위한 지원 라이브러리 영속성 구현



#### 참조
https://www.slideshare.net/madvirus/ddd-final
