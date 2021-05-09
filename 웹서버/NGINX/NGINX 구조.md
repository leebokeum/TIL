### 구조

#### worker_process
- worker_process는 워커 프로세스를 몇개 생성할 것인지를 지정하는 지시어다. 이 값이 1이라면 모든 요청을 하나의 프로세스로 실행하겠다는 의미인데, 여러개의 CPU 코어가 여러개 있는 시스템에서 이 값이 1이면 하나의 코어만으로 요청을 처리하게 되는 셈이다. 

#### worker_connections
- 로 몇개의 접속을 동시에 처리할 것인가를 지정하는 값이다. 이 값과 worker_process의 값의 조합을 계산해서 하나의 머신이 처리 할 수 있는 커넥션의 양을 산출할 수 있다. 예를들어 worker_process의 값이 4이고, worker_connections의 값이 1024라면 4 X 1024 = 4096개의 커넥션을 맺을 수 있다. 

#### client_max_body_size
- 이 값은 업로드 할 수 있는 용량의 크기를 지정한다. 이 지시자의 기본값은 1MB인데, 더 많은 파일의 업로드를 허용하려면 이 값을 늘려줘야 한다. 아래의 설정은 10MB까지 업로드를 허용한다.

```sh
client_max_body_size 10M;
```

#### http 블록
- http, server, location 블록은 계층구조를 가지고 있다. 

#### server 블록
- server 블록은 하나의 웹사이트를 선언하는데 사용된다. 가상 호스팅(Virtual Host)의 개념이다. 예를들어 하나의 서버로 http://opentutorials.org 과 http://egoing.net 을 동시에 운영하고 싶은 경우 사용할 수 있는 방법이다. 
- server_name : server_name 지시어에는 (주로 도메인인) 호스트 명이 온다. server_name이 속해있는 server 블록이 해당 호스트명에 대한 설정이라는 것을 의미한다.
- include : include는 별도의 파일에 설정을 기록해서 설정의 그룹핑, 재활용성을 높이는 방법


#### location 블록
- location 블록은 server 블록 안에 등장하면서 특정 URL을 처리하는 방법을 정의한다. 이를테면 http://opentutorials.org/course/1 과 http://opentutorials.org/module/1 로 접근하는 요청을 다르게 처리하고 싶을 때 사용한다. 