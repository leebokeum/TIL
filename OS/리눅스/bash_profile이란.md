### .bash_profile 이란?
- 환경변수를 추가하는 도구
- 긴 명령어를 단 1글자 혹은 2글자를 입력하여 실행할수 있다면 가독성이 높아지겠지?
- 리눅스에서 너무 긴 명령어 이거나 특정파일을실행하게 될때 보다 간결, 보다 쉽게 사용하기 위해서 명령어를 명명하기 위해 사용하는 파일이 .bash_profile 이다.


#### .bash_profile의 주의사항
1. 각 파일의 맨 아랫부분에 실행 코드를 추가할 떄의 기준입니다
2. 특별히 코드를 변경하지 않았다면 이 순서대로 실행 됩니다
3. 실행코드를 하단에 추가하는 것이 보편적입니다


### 예제
~~~ shell
# cd
($HOME 경로로 이동)

# vi .bash_profile
(.bash_profile을 vi편집기로 실행)

PATH=$PATH:HOME/bin:/usr/app/mysql/bin
(위와 같이 PATH로 된 부분에서 실행하고자 하는 파일이 있는 경로를 콜론으로 붙여서 추가한다)

:wq
(편집 중인 vi편집기를 저장하고 종료한다)

# source .bash_profile
(.bash_profile이 적용되도록 한다)

# mysql
(기존에는 /usr/mysql/bin/mysql 이라고 실행하던 것을, 위와 같이 손쉽게 실행할 수 있게 된다.)
~~~