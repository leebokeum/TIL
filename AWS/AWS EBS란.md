#### AWS에 EBS 란
1. EBS는 elastic block store의 약자이다.
2. 한마디로 외장 하드라고 보면 된다.
3. 기본적을 EC2 인스턴스를 하나 생성하면 8기가 EBS 볼륨이 기본으로 생성된다.
~~~ shell
$ df -hT /dev/xvda1
Filesystem     Type  Size  Used Avail Use% Mounted on
/dev/xvda1     ext4  7.8G  2.6G  5.1G  34% /
~~~
- 위 내용을 보면 /dev/xvda1이란 파일시스템은 약 8기가 볼륨을 가지고 있고 2.6G를 사용중이라는것을 볼 수 있다. 여기서 중요한것은 mounted on이 기본 root인 / 로 되어 있다는 것이다. 즉 기본으로 제공되는 EBS볼륨에 리눅스 OS구성요소와 USER HOME 데이터가 모두 올라가 있다는 것이다.

#### AWS에 EBS 볼륨 추가로 생성 후 EC2에 연결하기
1. EC2 대쉬보드 - EBS 볼륨 - 볼륨생성
    - 반드시 인스턴스와 같은 가용영역(zone)으로 설정하여야 연결이 가능하다.
2. 볼륨생성 후 경로명(/dev/xvdf)을 정하고, 인스턴스를 선택하여 완료한다.
3. 인스턴스 접속 후 확인
~~~ shell
$ df -h
~~~
4. 추가한 EBS 포맷(추가한 EBS의 경로는 /dev/xvdf이다.)
~~~ shell
$ sudo mkfs.ext4 /dev/xvdf
~~~
5. files라는 폴더를 만들고 추가한 EBS를 마운트 시킨다.
~~~ shell
$ sudo mkdir /files
$ sudo mount /dev/xvdf /files
~~~

#### EC2 인스턴스에서 EBS 볼륨 떼어내기
~~~ shell
$ sudo umount /dev/xvdf
~~~
