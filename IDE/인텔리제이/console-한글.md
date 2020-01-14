#### 콘솔에 한글이 깨져서 나오는 문제
- 인터넷을 찾아보니 ide.exe.vmoptions에 -Dfile.encoding=UTF-8을 삽입하거나 톰캣 vm 옵션에 -Dfile.encoding=UTF-8을 삽입하라고 나온다. 하지만 나의 경우 여전히 한글은 깨졌다. 

#### 해결
- settings - file encodings에 global/project encoding을 euc-kr로 모두 변경하였다.
- 이렇게 하니 한글이 깨지는 문제가 해결됨은 물론 console에 color도 생겨서 가독성이 더 좋아진것을 확인할 수 있었다.


#### 참조
https://intellij-support.jetbrains.com/hc/en-us/community/posts/206868775-Change-properties-file-encoding-disabled