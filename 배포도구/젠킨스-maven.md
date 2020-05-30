### maven으로 배포하는 방법(리눅스에 미리 maven은 설치해두도록한다)
1. 이미 새로운 item으로 git 설정은 끝낸상태
2. Jenkins관리 - Global Tool Configuration
3. maven - add 
4. name 설정(중요하다. 나중에 item설정에서 선택해야한다.)

![alt text](/image/젠킨스/tool-setting.PNG)

5. item - 구성으로 돌아와서 
6. Build - Invoke top-level Maven targets 추가
6. Maven Version은 위에서 셋팅한 name을 선택해준다.
7. goals
~~~ xml
clean:clean install
~~~
![alt text](/image/젠킨스/maven.PNG)

8. 빌드 후 조치 - Send Build artifacts over SSH 추가하기 전 Jenkins관리-설정으로 돌아간다.
9. SSH Servers 추가
![alt text](/image/젠킨스/ssh-server-setting.PNG)
10. connect test성공하면 item 구성으로 돌아간다.
11. 빌드 후 조치 - Send Build artifacts over SSH 추가
12. 위에서 설정한 ssh servers를 추가해주고 아래 이미지와 같이 설정해준다.(단 리눅스 경로에 해당 bash 스크립트는 있어야한다.)
![alt text](/image/젠킨스/maven-release.PNG)