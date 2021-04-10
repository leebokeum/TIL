### 변수와 echo
```sh
water="삼다수" // 쉘 변수를 터미널내에 선언
echo $water // 변수를 출력
unset water // 변수 선언 해제
```


### evn
```sh
env // 운영체제 변수들을 출력
```

### export

``` sh
export water // 쉘 변수를 환경변수로 저장

vi ~/.bashrc // 매번 쉘을 실행할 때마다 쉘 변수를 환경변수로 자동으로 설정하고 싶다면 .bashrc 파일에 변수를 저장
export water="삼다수"
export TEMP_DIR=/tmp
export BASE_DIR=$TEMP_DIR/backup
```