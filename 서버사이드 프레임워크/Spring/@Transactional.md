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

        throw new Exception("Exception for rollback");

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

### 참조
https://offbyone.tistory.com/405