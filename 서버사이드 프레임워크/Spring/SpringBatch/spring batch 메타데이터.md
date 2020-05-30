### spring batch 메타데이터
- 이전에 실행한 Job이 어떤 것들이 있는지
- 최근 실패한 Batch Parameter가 어떤것들이 있고, 성공한 Job은 어떤것들이 있는지
- 다시 실행한다면 어디서 부터 시작하면 될지
- 어떤 Job에 어떤 Step들이 있었고, Step들 중 성공한 Step과 실패한 Step들은 어떤것들이 있는지
- 이 테이블들이 있어야만 Spring Batch가 정상 작동
- MySQL이나 Oracle과 같은 DB를 사용할때는 개발자가 직접 생성해야한다.


#### BATCH_JOB_INSTANCE
- BATCH_JOB_INSTANCE 테이블은 Job Parameter에 따라 생성되는 테이블
- 예를 들어, 특정 날짜를 Job Parameter로 넘기면 Spring Batch에서는 해당 날짜 데이터로 조회/가공/입력 등의 작업을 할 수 있다.
- 같은 Batch Job 이라도 Job Parameter가 다르면 Batch_JOB_INSTANCE에는 기록되며, Job Parameter가 같다면 기록되지 않는다.


#### BATCH_JOB_EXECUTION
- JOB_EXECUTION와 JOB_INSTANCE는 부모-자식 관계
- JOB_EXECUTION은 자신의 부모 JOB_INSTACNE가 성공/실패했던 모든 내역을 갖고 있다.



### 참조
https://jojoldu.tistory.com/326?category=635883