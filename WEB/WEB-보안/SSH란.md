### SSH란?
- ssh는 public key 암호방식을 사용한다. public key 암호방식은 비대칭 암호방식으로 public key와 private key를 사용한다. 암호를 걸 때와 풀 때 사용하는 키가 다르기 때문에 비대칭 암호방식이라고 불린다. public key는 평문을 암호화한다면, private key는 암호문을 다시 평문으로 변환한다.

- public key는 네트워크 환경에서 전달하게 된다. private key가 외부에 노출될 위험이 없기에 public키를 맘놓고 노출시키는 것이다.
두 키가 온전히 있어야 암호/복호가 가능하다.

###  private / public 키 만드는 방법

~~~ shell
$ ls ~/.ssh
known_hosts
디렉토리 확인 및 key 존재여부 확인
~~~

키생성 명령어
~~~ shell
$ ssh-keygen -t rsa -b 4096 -C "leebokeum@hanmail.net"

-t 옵션으로 암호화 타입을 정함
-b로 생성할 키의 비트수를 지정
-C는 주석을 입력
git hub에서는 사용자의 로그인 ID를 적어놓으라고 가이드한다.
~~~

- private 키는 디폴트로 ~/.ssh/id_rsa 파일에 저장한다.
- public 키는 같은 위치에 id_rsa.pub이란 이름으로 생성된다.
- passphrase는 키에 접근할 때마다 추가로 암호를 요구하게 할 수 있다.

이제 ssh public키를 서버에 공유하면 된다.


### 출처
https://storycompiler.tistory.com/112 [아프니까 개발자다]