## find - 현재 폴더 하위의 특정 문자 파일 검색
- find 파일 찾을 위치 지정 -name 찾을 파일 이름
~~~ shell
find ./ -name aaa.txt
~~~
> ./(현재 폴더 부터, 하위 폴더 포함) aaa.txt 파일을 찾아라

## grep - 파일 내부 문자열을 검색하는 명령어
- grep은 파일 내부 문자열 검색만을 위해서 쓰이는 건 아님
- grep -r "찾을 문자열" ./*
~~~ shell
grep -r "aaa" ./*
~~~
> ./(현재 폴더 아래 모든 파일에서) aaa라는 문자열이 있는지 검색

## 참조
https://ngee.tistory.com/83