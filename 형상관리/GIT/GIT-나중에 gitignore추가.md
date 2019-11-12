### gitignore에 나중에 추가해서 히스토리를 제거하고 싶을때
- DB정보같은 비밀 문서가 open github에 올라갔을 때 필요


1. .gitignore파일에 해당 파일 추가하고 commit/push
2. 아래
~~~ shell
$ git rm -r --cached .
$ git add .
$ git commit -m ".gitignore 수정"
~~~
3. 마지막으로 push 해준다.