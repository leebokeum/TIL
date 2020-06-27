### SSH로 EC2 접속하기
- pem파일을 원하는 위치에 복사하고 퍼미션을 400으로 조정    
~~~ sh
chmod 400 keyfile.pem
~~~
- 접속
~~~ sh
ssh -i keyfile.pem ec2-user@[서버 아이피 또는 도메인]
~~~

### 참고
pem 파일이 아닌 ppk를 키파일로 사용하는 경우 : SSH 키 비밀번호를 입력을 요구하면서 인증 에러 발생
ssh접속 시 도메인에 아이디를 붙이지 않는 경우 : Permission denied (publickey) 에러 발생