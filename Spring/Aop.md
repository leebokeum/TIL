### Aspect Oriented Programing
- 관점 지향 프로그래밍

### 장점
- 주 업무 외에 부가 업무를 쉽게 구현할 수 있다.
- Core Concern / Cross-cutting을 통하여

### Ex
- 로그처리
- 보안처리
- 트랜젝션 처리

### Advice
- 이전(before) - 메서드가 호출되기 전
- 이후(after) - 결과에 상관없이 메서드가 완료된 후
- 반환 이후(after-returning) - 메서드가 성공적으로 완료된 후
- 예외 발생 이후(after-throwing) - 메서드가 예외를 던진 후
- 주위(around) - 어드바이스가 메서드를 감싸서 호출 전과 후


### Pointcut, JoinPoint, weaving