### tomcat


### 포트
- 톰캣은 일반적으로 2개 내지 3개 이상의 포트를 사용한다. 첫 번째는 관리용 Server Port 로 8005 를 사용하며  프로토콜 커넥터마다 개별 포트를 사용하게 된다. 서비스용으로는 "HTTP Connector" 와 "AJP Connector" 를 사용하므로 3개가 되며 SSL Connector 까지 사용하면 총 4개의 포트를 쓰게 된다.

### 종료과정
- 톰캣의 종료 명령어인 shutdown.sh 는 org.apache.catalina.startup.Bootstrap 클래스의 stop() 메소드를 호출하며 이 메소드는 Server Port 에 연결하여 종료 명령을 전송한다.