### @Async Callback 비동기 처리
1. @EnableAsync
``` java
@Configuration
@EnableAsync
public class AsyncConfig extends AsyncConfigurerSupport {

	@Override
	public Executor getAsyncExecutor() {
		ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
		executor.setCorePoolSize(10);
		executor.setMaxPoolSize(100);
		executor.setQueueCapacity(50);
		executor.initialize();
		return executor;
	}

}
```
- corePoolSize : 미리 스레드를 만들어 놓아 요청이 들어오면 바로 수행
- maxPoolSize : corePoolSize가 꽉차면 이후에는 스레드를 생성하여 수행, maxPoolSize만큼 스레드 증가
- queueCapacity : maxPoolSize가 꽉차면 이후에는 큐에 등록하여 순차적으로 수행, queueCapacity가 꽉차면 예외 발생

### 주의사항
- 반드시 public 으로 메서드를 선언해야한다.
- 같은 클래스의 메서드에 @Async 설정하여 호출할 경우 동작하지 않는다.
- 리턴 타입은 void나 Future<V> 인터페이스만 가능하다.

### ex) void
``` java
@Async
public void logger() throws InterruptedException {
	Thread.sleep(1000);
	logger.info("서비스");
}

testService.logger();
logger.info("컨트롤러");
```

### ex) Future<V>
- 비동기 처리 후 리턴 값을 받아서 처리하는 방법
``` java
@Async
public Future<String> logger() throws InterruptedException {
	Thread.sleep(1000);
	logger.info("서비스");
	return new AsyncResult<>("결과");
}

Future<String> future = testService.logger();
logger.info("컨트롤러");
while (true) {
	if (future.isDone()) 
		return future.get();
}
```

### ex) ListenableFuture<T> extends Future<T>
``` java
@Async
public ListenableFuture<String> logger() throws InterruptedException {
	Thread.sleep(1000);
	logger.info("서비스");
	return new AsyncResult<>("결과");
}

testService.logger().addCallback((result) -> {
	logger.info(result);
}, (e) -> {
	logger.error(e.getMessage(), e);
});
logger.info("컨트롤러");
```

### ex)  CompletableFuture implements Future, CompletionStage
``` java
CompletableFuture<String> future
  = CompletableFuture.supplyAsync(() -> "Hello");


//Combining Futures
CompletableFuture<String> completableFuture 
  = CompletableFuture.supplyAsync(() -> "Hello")
    .thenCompose(s -> CompletableFuture.supplyAsync(() -> s + " World"));

completableFuture.get();
```

.thenRun : Runnable 을 파라미터로 하여, 정상실행후 CompletableFuture 리턴, 다음스테이지 실행에 반환값 없음
.supplyAsync : Supplier 을 파라미터로 하며, 정상실행후  CompletableFuture 리턴, 다음스테이로 반환값 전달
.thenAccept(Async) : Consumer 형태의 파이프라인 실행 , 인자가 Consumer 이기때문에 다음 스테이지로 결과값을 넘겨줄수 없다.
.thenApply(Async)  : Function 형태의 파이프라인 실행, 인자가 Function 이기때문에 다음 스테이지로 결과값을 넘겨줄수 있다.
.thenCompose : CompletableFuture 를 반환하는 Method Chain으로 실행하고자 할때. 
.exceptionally : 예외 사항 처리 
.allOf : 동시에 N개의 요청을 호출하고 나서 모든 스테이지가 완료되면 다음 스테이지를 실행한다.
.anyOf : 동시에 N개의 요청을 호출하고 나서 하나라도 호출이 완료되면 다음 스테이지를 실행한다.
