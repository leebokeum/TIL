### Source 명령 실행불가 (if: Expression Syntax)

~~~ c
// 아래 오류 메시지 출격
# source .bash_profile
if: Expression Syntax.
~~~

#### 원인
- csh쉘에서는 실행이 안되는 것이라고함

#### 현재 쉘 확인
~~~ c
# echo $SHELL
/bin/csh
~~~

#### 해결
~~~ c
# exec bash
(bash쉘로 수정)
~~~


source ~/.cshrc