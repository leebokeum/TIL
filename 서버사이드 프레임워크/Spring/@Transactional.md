### @Transactional
- 스프링에서는 트랜잭션 처리를 지원하는데 그중 어노테이션 방식으로 @Transactional을 선언하여 사용하는 방법이 일반적이며, 선언적 트랜잭션이라 부른다.
- 클래스, 메서드위에 @Transactional 이 추가되면, 이 클래스에 트랜잭션 기능이 적용된 프록시 객체가 생성된다.

### 트랜잭션 특징
1. 원자성(Atomicity)
- 한 트랜잭션 내에서 실행한 작업들은 하나로 간주한다. 즉, 모두 성공 또는 모두 실패. 

2. 일관성(Consistency)
- 트랜잭션은 일관성 있는 데이타베이스 상태를 유지한다. (data integrity 만족 등.)

3. 격리성(Isolation)
- 동시에 실행되는 트랜잭션들이 서로 영향을 미치지 않도록 격리해야한다.

4. 지속성(Durability)
- 트랜잭션을 성공적으로 마치면 결과가 항상 저장되어야 한다.

### 트랜잭션 롤백 예외
- 선언적 트랜잭션에서는 런타임 예외가 발생하면 롤백한다.
- 반면에 예외가 전혀 발생하지 않거나 체크 예외가 발생하면 커밋한다.
    - 체크 예외를 커밋 대상으로 삼은 이유는 체크 예외가 예외적인 상황에서 사용되기보다는 리턴 값을 대신해서 비즈니스적인 의미를 담은 결과를 돌려주는 용도로 많이 사용되기 때문이다.
 - 스프링에서는 데이터 액세스 기술의 예외는 런타임 예외로 전환돼서 던져지므로 런타임 예외만 롤백 대상으로 삼은 것이다.

``` java
@Service
@Transactional
public class BoardService {
    @Autowired
    BoardRepository boardRepository;

    //정상 커밋
    public List<Board> saveCommitTransaction() {
        boardRepository.save(new Board(1, "hello"));
        boardRepository.save(new Board(2, "hello2"));
        boardRepository.save(new Board(3, "hello3"));
        boardRepository.save(new Board(4, "hello4"));
        boardRepository.save(new Board(5, "hello5"));
        return boardRepository.findAll();
    }

    // 데이터 이상으로 트랜젝션 중간에 exception 발생
    // 전부 롤백
    public List<Board> saveRollbackTransaction() {
        boardRepository.save(new Board(1, "hello"));
        boardRepository.save(new Board(2, "hello2"));
        //컬럼사이즈 초과 exception 발생 전부 롤백
        boardRepository.save(new Board(3, "abcdefghijklmnopqrstu123456"));
        boardRepository.save(new Board(4, "hello4"));
        boardRepository.save(new Board(5, "hello5"));
        return boardRepository.findAll();
    }

    // 임의적은 Default Exception 발생
    // 롤백이 되지 않는다.
    // Checked 예외는 롤백이 되지 않는다.
    public List<Board> saveDefaultExceptionTransaction() throws Exception {
        boardRepository.save(new Board(1, "hello"));
        boardRepository.save(new Board(2, "hello2"));

        throw new Exception("Checked Exception for No rollback");

    }

    // 임의적은 Runtime Exception 발생
    // 롤백이 된다.
    // Unchecked 예외는 롤백이 된다.
    public List<Board> saveRunTimeExceptionTransaction() throws Exception{
        boardRepository.save(new Board(1, "hello"));
        boardRepository.save(new Board(2, "hello2"));

        throw new RuntimeException("Exception for rollback");
    }
}
```

### 옵션
#### 1. isolation (격리수준)
- 트랜잭션에서 일관성이 없는 데이터를 허용하도록 하는 수준을 말한다. 

DEFAULT
 - 기본 격리 수준(기본설정, DB의 Isolation Level을 따름)

READ_UNCOMMITTED (level 0)
 - 커밋되지 않는(트랜잭션 처리중인) 데이터에 대한 읽기를 허용

READ_COMMITTED (level 1)
 - 트랜잭션이 커밋 된 확정 데이터만 읽기 허용
 - 어떠한 사용자가 A라는 데이터를 B라는 데이터로 변경하는 동안 다른 사용자는 해당 데이터에 접근할 수 없다.
 - Problem1 - Dirty Read 방지

REPEATABLE_READ (level 2)
 - 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 shared lock이 걸리므로 다른 사용자는 그 영역에 해당되는 데이터에 대한 수정이 불가능하다.
 - 선행 트랜잭션이 읽은 데이터는 트랜잭션이 종료될 때까지 후행 트랜잭션이 갱신하거나 삭제가 불가능 하기때문에 같은 데이터를 두 번 쿼리했을 때 일관성 있는 결과를 리턴한다.
 - Problem2 - Non-Repeatable Read 방지

SERIALIZABLE (level 3)
 - 데이터의 일관성 및 동시성을 위해 MVCC(Multi Version Concurrency Control)을 사용하지 않음
(MVCC는 다중 사용자 데이터베이스 성능을 위한 기술로 데이터 조회 시 LOCK을 사용하지 않고 데이터의 버전을 관리해 데이터의 일관성 및 동시성을 높이는 기술)

#### 2. propagation (전파옵션)
- 트랜잭션 동작 도중 다른 트랜잭션을 호출(실행)하는 상황에 선택할 수 있는 옵션이다.
- @Transactional의 propagation 속성을 통해 피호출 트랜잭션의 입장에서는 호출한 쪽의 트랜잭션을 그대로 사용할 수도 있고, 새롭게 트랜잭션을 생성할 수도 있다.

REQUIRED
 - 디폴트 속성, 부모 트랜잭션 내에서 실행하며 부모 트랜잭션이 없을 경우 새로운 트랜잭션을 생성한다.


SUPPORTS
 - 이미 시작된 트랜잭션이 있으면 참여하고 그렇지 않으면 트랜잭션 없이 진행하게 만든다. 

REQUIRES_NEW
 - 부모 트랜잭션을 무시하고 무조건 새로운 트랜잭션이 생성

MANDATORY
 - REQUIRED와 비슷하게 이미 시작된 트랜잭션이 있으면 참여한다. 
 - 반면에 트랜잭션이 시작된 것이 없으면 새로 시작하는 대신 예외를 발생시킨다. 
 - 혼자서는 독립적으로 트랜잭션을 진행하면 안 되는 경우에 사용한다.

REQUIRES_NEW
 - 항상 새로운 트랜잭션을 시작한다.
 - 이미 진행 중인 트랜잭션이 있으면 트랜잭션을 잠시 보류시킨다.

NOT_SUPPORTED
 - 트랜잭션을 사용하지 않게 한다.
 - 이미 진행 중인 트랜잭션이 있으면 보류시킨다.

NEVER
 - 트랜잭션을 사용하지 않도록 강제한다.
 - 0 이미 진행 중인 트랜잭션도 존재하면 안된다 있다면 예외를 발생시킨다.

NESTED
 - 이미 진행중인 트랜잭션이 있으면 중첩 트랜잭션을 시작한다.
 - 중첩 트랜잭션은 트랜잭션 안에 다시 트랜잭션을 만드는 것이다.
 - 하지만 독립적인 트랜잭션을 만드는 REQUIRES_NEW와는 다르다.
중첩된 트랜잭션은 먼저 시작된 부모 트랜잭션의 커밋과 롤백에는 영향을 받지만 자신의 커밋과 롤백은 부모 트랝개션에게 영향을 주지 않는다.

#### 3. readOnly 속성
- 트랜잭션을 읽기 전용으로 설정할 수 있다.
- 성능을 최적화하기 위해 사용할 수도 있고 특정 트랜잭션 작업 안에서 쓰기 작업이 일어나는 것을 의도적으로 방지하기 위해 사용할 수도 있다. 
- 일부 트랜잭션 매니저의 경우 읽기전용 속성을 무시하고 쓰기 작업을 허용할 수도 있기 때문에 주의해야 한다. 
- 일반적으로 읽기 전용 트랜잭션이 시작된 이후 INSERT, UPDATE, DELETE 같은 쓰기 작업이 진행되면 예외가 발생한다. 
- aop/tx 스키마로 트랜잭션 선언을 할 때는 이름 패턴을 이용해 읽기 전용 속성으로 만드는 경우가 많다. 보통 get이나 find 같은 이름의 메소드를 모두 읽기전용으로 만들어 사용하면 편리하다.
- @Transactional 의 경우는 각 메소드에 일일이 읽기 전용 지정을 해줘야 한다.
- read-only 애트리뷰트 또는 readOnly 앨리먼트로 지정한다.
- true인 경우 insert, update, delete 실행 시 예외 발생, 기본 설정은 false


#### 트랜잭션 롤백 예외 (rollback-for, rollbackFor, rollbackForClassName)
- 선언적 트랜잭션에서는 런타임 예외가 발생하면 롤백한다.
- 반면에 예외가 전혀 발생하지 않거나 체크 예외가 발생하면 커밋한다.
   체크 예외를 커밋 대상으로 삼은 이유는 체크 예외가 예외적인 상황에서 사용되기보다는 리턴 값을 대신해서 비즈니스적인 의미를 담은 결과를 돌려주는 용도로 많이 사용되기 때문이다.

- 스프링에서는 데이터 액세스 기술의 예외는 런타임 예외로 전환돼서 던져지므로 런타임 예외만 롤백 대상으로 삼은 것이다.
- 하지만 기본 동작방식을 바꿀 수도 있다.
ex ) 체크 예외지만 롤백 대상으로 삼아야 하는 것이 있다면 XML의 rolback-for 애트리뷰트나 애노테이션의 rollbackFor 또는 rollbackForClassName 앨리먼트를 이용해서 예외를 지정하면 된다. 
rollback-for 나 rollbackForClassName 은 예외 이름을 넣으면 되고, rollbackFor 는 예외 클래스를 직접 넣는다.

- @Transactional 에서는 다음과 같이 클래스 이름 대신 클래스를 직접 사용해도 된다.
- @Transactional(readOnly=true, rollbackFor=NoSuchMemberException.class)

rollbackFor 속성
- 특정 예외가 발생 시 강제로 Rollback
- 설정 예: @Transactional(rollbackFor=Exception.class)

noRollbackFor 속성
- 특정 예외의 발생 시 Rollback 처리되지 않음
- 설정 예: @Transactional(noRollbackFor=Exception.class)



### 참조
https://offbyone.tistory.com/405
https://goddaehee.tistory.com/167