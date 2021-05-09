### alias와 root의 차이
- alias 는 특정 URL이 서빙할 파일 경로를 변경하는 역할을 한다. root와는 역할이 다르다.
- root: location 으로 넘어온 부분을 root로 설정한 경로에 추가한다.
- alias: location 에 매칭된 부분을 제거하고, alias 로 설정한 경로에서 찾는다.
``` conf
 location /static/ {
    root /var/www/app/static;
    autoindex off;
  }
# /var/www/app/static/static 경로에서 찾는다.

  location /static/ {
    alias /var/www/app/static/;
    autoindex off;
  }
# /var/www/app/static/ 에서 찾는다.
```

```sh
location /images/something/ {
    alias /var/www/something/;
}
```
- 이 상태에서 http://example.com/images/something/somepath/myfile.png의 실제 파일상 경로는 /var/www/something/sompath/myfile.png가 된다. 중간에 location에 기술된 /images/something은 경로를 구성할 때 빠진다.
반면에 root /var/www/something 으로 구성했다면 실제 파일상 경로는 /var/www/something/images/something/somepath/myfile.png가 된다.