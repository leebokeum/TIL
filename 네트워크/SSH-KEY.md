### ssh 사용시 암호 대신 SSH key로 인증하기
- SSH 서버는 여러가지 방법으로 클라이언트를 인증할 수 있다. 그 중 가장 기본적인 방법은 패스워드를 사용하는 것으로 사용하기 쉽지만 가장 안전한 인증방법은 아니다.
- 비록 패스워드는 암호화되어 서버로 보내지지만 꾸준하고 반복적인 해커의 공격에 안전할만큼 복잡하거나 길지 않은 경우가 거의 대부분이다.


### public key 와 private key
- SSH 키 페어는 두개의 암호키로 SSH 서버가 클라이언트를 인증하는데 사용될 수 있다. 각 키 페어는 public 키와 private 키로 이루어진다.
- Private 키는 클라이언트가 가지고 있고, 이 키는 절대적인 비밀(누구에게도 복사해 주거나 공개하면 안됨)로 해야만 한다. 어떤 식으로건 private 키가 알려지는 순간 공격자는 그 쌍이 되는 public 키로 설정된 서버에 아무 추가적인 인증 없이 로그인이 가능해진다. 추가적인 예방조치로 private 키를 passphrase로 암호화 해서 디스크에 저장할 수 있다.
- 쌍이 되는 public 키는 아무 걱정 없이 자유롭게 누구에게든 공유할 수 있다. Public 키로 메시지를 암호화 할 수 있는데, 그 암호화 된 메시지는 그 쌍이 되는 private 키로만 해석할 수 있다. (암호화에 사용한 public 키로도 암호화 된 메시지를 해석할 수 없다) 이런 특성이 키 페어를 사용한 인증방식에 사용된다.

### key는 클라이언트 어디에 저장되나?
- Public 키는 SSH로 로그인하길 원하는 원격 서버에 업로드된다. 이 키는 사용자 어카운트의 ~/.ssh/ 특별한 파일에 추가된다.

### 인증은 어떻게?
- 클라이언트가 SSH key를 사용해 인증하려고 시도하면, 서버는 클라이언트가 private 키를 가지고 있는지 여부를 테스트 할 수 있다. 클라이언트가 private 키를 가지고 있는걸 증명하면 쉘 세션이 생성되거나 요구된 명령을 실행한다.
이 전체적인 흐름은 다음과 같다.

![alt text](https://2.bp.blogspot.com/-KFIKbVe38GY/VRugz3LpcHI/AAAAAAAAEUY/_zcGcOwpp90/s1600/DB30E7AC-42F8-4876-9BA4-04CB4623571F.png)

1. 클라이언트가 서버에 SSH 연결을 요청한다.
2. 서버는 랜덤 챌린지(랜덤 데이터 스트링)를 생성해 클라이언트에게 보낸다.
3. 클라이언트는 서버로 부터 받은 챌린지(C)를 자신이 가지고 있는 private 키로 암호화해서 암호화 된 메시지를 서버로 보낸다.
4. 서버는 클라이언트에서 받은 암호화 된 메시지를 public 키로 해석한 후 그 결과를 2단계에서 자신이 클라이언트에게 보낸 랜덤 챌린지와 일치하는지 확인한다. (public 키로 해석할 수 있는 메시지는 그 쌍이 되는 private 키를 가진 사람만이 만들 수 있기 때문) 일치하면 클라이언트가 인증된 것이다.

### SSH key 만들기
- 서버가 SSH 키 인증을 사용하도록 설정하려면 가장 먼저 해야 하는 일은 클라이언트에서 키 페어를 만드는 것이다.
키 페어를 만들려면 OpenSSH에 포함되어 있는 ssh-keygen 유틸리티를 사용한다. 디폴트로 2048-bit RSA 키 페어를 만들게 되어 있는데, 대부분의 사용자에게 이 정도면 충분하다.

- 클라이언트에서 ssh-keygen을 실행해 SSH 키 페어를 만든다.

~~~ shell
$ ssh-keygen

Generating public/private rsa key pair.
Enter file in which to save the key (/home/test/.ssh/id_rsa):
~~~

- 프로그램이 생성될 키를 저장할 위치를 선택하도록 물어본다. 디폴트로 ~/.ssh 디렉토리에 저장하게 되어 있다. Private 키는 id_rsa라는 이름이고 public 키는 id_rsa.pub라는 이름을 사용한다.
일반적으로 디폴트를 그대로 사용하는게 좋다. 별도 디렉토리를 사용하려면 원하는 위치를 입력하고, 그냥 디폴트를 사용하려면 엔터를 누르면 된다.

- 만일 이전에 만들어 놓은 SSH 키가 있다면 다음과 같은 내용을 보게 될 것이다.
~~~ shell
/home/test/.ssh/id_rsa already exists.
Overwrite (y/n)?
~~~
- 덮어쓰기를 선택하면 이전 키를 사용하는 인증은 더 이상 사용할 수 없게 된다. 이 단계는 되돌릴 수 없으므로 yes를 선택하려면 매우 주의해야 한다.

### public key 원격서버에 넣어주기
- 로컬 머신 어카운트의 id_rsa.pub 키 파일 내용을 SSH로 로그인하길 원하는 서버 어카운트의 ~/.ssh/authorized_keys 파일에 복사해 넣어주면 된다.

예시
~~~ shell
$ cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCqql6MzstZYh1TmWWv11q5O3pISj2ZFl9HgH1JLknLLx44+tXfJ7mIrKNxOOwxIxvcBF8PXSYvobFYEZjGIVCEAjrUzLiIxbyCoxVyle7Q+bqgZ8SeeM8wzytsY+dVGcBxF6N4JS+zVk5eMcV385gG3Y6ON3EG112n6d+SMXY0OEBIcO6x+PnUSGHrSgpBgX7Ks1r7xqFa7heJLLt2wWwkARptX7udSq05paBhcpB0pHtA1Rfz3K2B+ZVIpSDfki9UVKzT8JUmwW6NNzSgxUfQHGwnW7kj4jp4AT0VZk3ADw497M2G/12N0PPB5CnhHf7ovgy6nL1ikrygTKRFmNZISvAcywB9GVqNAVE+ZHDSCuURNsAInVzgYo9xgJDW8wUw2o8U77+xiFxgI5QSZX3Iq7YLMgeksaO4rBJEa54k8m5wEiEE1nUhLuJ0X/vh2xPff6SQ1BL/zkOhvJCACK6Vb15mDOeCSq54Cr7kvS46itMosi/uS66+PujOO+xt/2FWYepz6ZlN70bRly57Q06J+ZJoc9FfBCbCyYH7U/ASsmY095ywPsBo1XQ9PqhnN1/YOorJ068foQDNVpm146mUpILVxmq41Cj55YKHEazXGsdBIbXWhcrRf4G2fJLRcGUr9q8/lERo9oxRm5JFX6TCmj6kmiFqv+Ow9gI0x8GvaQ== test@localhost
~~~


### SSH 키를 사용해 서버에 로그인하기
- 서버에 public 키를 카피해 놓았다면 원격 호스트에 로그인 할 어카운트의 암호 없이 로그인이 가능하다. 로그인 절차는 완전 동일하다.
- 만일 이 호스트에 SSH로 첫번째 접속하는 것이면 다음과 같은 메시지를 보게 될 것이다.

~~~ shell
The authenticity of host 'foo.bar.com (111.111.11.111)' can't be established.
ECDSA key fingerprint is fd:fd:d4:f9:77:fe:73:84:e1:55:00:ad:d6:6d:22:fe.
Are you sure you want to continue connecting (yes/no)? yes
~~~