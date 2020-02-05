### mount
- 보조기억장치(HDD, FDD, CD-ROM 등)나 파일 시스템이 다른 디스크를 /의 하위 디렉터리로 연결하여 사용 가능하게 해주는 명령어

### 사용법
```shell
# mount [option] [device] [directory]
```
### 예제

```shell
mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-d23e44b3.efs.ap-northeast-2.amazonaws.com:/ /IDOPEFS

## 해제 할때
umount /IDOPEFS
```

