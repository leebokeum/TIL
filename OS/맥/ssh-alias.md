### ssh alias 적용하여 쉽게 접속하기

~~~ c
// Config 파일을 생성합니다.
$ touch ~/.ssh/config
$ chmod 600 ~/.ssh/config
~~~

~~~ c
// config을 열어서 아래와 같이 넣어준다.
Host theeye
  HostName theeye.pe.kr
  User eye
~~~


~~~ c
// 아래처럼 접속할 수 있다.
ssh theeye
~~~