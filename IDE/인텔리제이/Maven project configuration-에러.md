#### Error:Maven Resources Compiler: Maven project configuration required for module 'delivery' isn't available. Compilation of Maven projects is supported only if external build is started from an IDE.

- 인텔리제이에서 위와같은 compiler-Build project automatically를 체크 했을 때 위와 같은 에러가 problems에 나타나면서 live recompile이 되지 않는 현상이 발생했다.
- 하루종일 저걸 잡아보려고 별짓을 다했다.

#### Solution
1. maven을 다운받아 특정경로에 압축을 풀고
2. Build Tools - Maven 에서 home directory와 setting, repository 경로를 따로 설정해준다.
3. Rebuild Module을 해준다.
4. 해결되었다.

- 핵심은 Rebuild Module 에 있는거 같다.