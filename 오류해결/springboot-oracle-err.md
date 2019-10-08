### spring batch mybatis 수행중 오라클 DB 오류 발생
- 분명 mybatis 설정은 제대로 되었고 H2DB기반으로 정상 작동하는것 확인함
- Database를 오라클로만 바꾸면 아래와 같은 에러 발생

~~~ console
java.lang.AbstractMethodError: Method oracle/jdbc/driver/OraclePreparedStatementWrapper.closeOnCompletion()V is abstract
	at oracle.jdbc.driver.OraclePreparedStatementWrapper.closeOnCompletion(OraclePreparedStatementWrapper.java)
	at com.zaxxer.hikari.pool.HikariProxyPreparedStatement.closeOnCompletion(HikariProxyPreparedStatement.java)
	at org.apache.ibatis.executor.SimpleExecutor.doQueryCursor(SimpleExecutor.java:74)
	at org.apache.ibatis.executor.BaseExecutor.queryCursor(BaseExecutor.java:178)
	at org.apache.ibatis.executor.CachingExecutor.queryCursor(CachingExecutor.java:89)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.selectCursor(DefaultSqlSession.java:123)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.selectCursor(DefaultSqlSession.java:116)
	at org.mybatis.spring.batch.MyBatisCursorItemReader.doOpen(MyBatisCursorItemReader.java:69)
	at org.springframework.batch.item.support.AbstractItemCountingItemStreamItemReader.open(AbstractItemCountingItemStreamItemReader.java:149)
	at org.springframework.batch.item.support.CompositeItemStream.open(CompositeItemStream.java:103)
	at org.springframework.batch.core.step.tasklet.TaskletStep.open(TaskletStep.java:311)
	at org.springframework.batch.core.step.AbstractStep.execute(AbstractStep.java:200)
	at org.springframework.batch.core.job.SimpleStepHandler.handleStep(SimpleStepHandler.java:148)
	at org.springframework.batch.core.job.AbstractJob.handleStep(AbstractJob.java:399)
	at org.springframework.batch.core.job.SimpleJob.doExecute(SimpleJob.java:135)
	at org.springframework.batch.core.job.AbstractJob.execute(AbstractJob.java:313)
	at org.springframework.batch.core.launch.support.SimpleJobLauncher$1.run(SimpleJobLauncher.java:144)
	at org.springframework.core.task.SyncTaskExecutor.execute(SyncTaskExecutor.java:50)
	at org.springframework.batch.core.launch.support.SimpleJobLauncher.run(SimpleJobLauncher.java:137)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.springframework.aop.support.AopUtils.invokeJoinpointUsingReflection(AopUtils.java:343)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.invokeJoinpoint(ReflectiveMethodInvocation.java:198)
	at org.springframework.aop.framework.ReflectiveMethodInvocat
~~~

- 오라클 driver 인식 문제
- 메이븐 오라클 ojdbc 버전을 아래와 같이 바꿈

~~~ xml
<dependency>
    <groupId>com.oracle</groupId>
    <artifactId>ojdbc6</artifactId>
    <version>11.2.0.1.0</version>
</dependency>
~~~
- 위에서 아래로 바꾸니 정상 작동함
~~~ xml
<dependency>
    <groupId>com.oracle</groupId>
    <artifactId>ojdbc6</artifactId>
    <version>RELEASE</version>
</dependency>
~~~