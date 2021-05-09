### NGINX설정 후 크롬 주의요함
- ssl 설정 후 크롬에서 주의요함이 뜨는 현상
- console에 아래와 같은 문가 뜸
```
The connection used to load resources from https://dove.ildong.com used TLS 1.0 or TLS 1.1, which are deprecated and will be disabled in the future. Once disabled, users will be prevented from loading these resources. The server should enable TLS 1.2 or later.
```
- tls 버전이 1.2 이하이기 때문에 발생
- 서버에서 nginx 버전 확인
``` shell
curl -I localhost
```
- nginx conf파일 안에 tls 버전을 1.2로 바꿔준다.