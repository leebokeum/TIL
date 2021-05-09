### rewrite
``` sh
http://en.wikipedia.org/wiki/index.php?title=Semantic_URL

위 url을

http://en.wikipedia.org/wiki/Semantic_URL

이렇게 바꾸려면

rewrite ^/wiki/(.*)$ /wiki/index.php?title=$1?;

```

### 리다이렉션
``` sh
http://old_site.org/tutorials/javascript.html

을 http://opentutorials.org/course/48
로 보내고 싶다면

location ~ /tutorials/javascript.html {
    rewrite ^ http://opentutorials.org/course/48;
}
```

### 내부 리다이렉션
```sh
http://test.com/docs/readme.html
을
http://test.com/files/docs/readme.html
로 보내고 싶다면

location /docs/ {
    rewrite ^/docs/(.*)$ /files/docs/$1;
}
```

### www 제거
```sh
if ($host ~* ^www\.(.*)){
    set $host_without_www $1;
    rewrite ^/(.*)$ $scheme://$host_without_www/$1 permanent;
}
```

### favicon.ico 무시
```sh
location = /favicon.ico {
    return 204;
}
```