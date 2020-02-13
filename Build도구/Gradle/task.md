### gradle 테스크란?
- gradle은 명령에의해 테스크(Task)를 수행하는 프로그램이다
- gradle compileJava , gradle run 등 명령어를 통해 실행하는 것들이 모두 테스크 이다.

### 정의
- 테스크는 사용자가 정의할 수 있다. 
- build.gradle에 테스크를 기술해두면 그것을 gradle 명령으로 호출시켜 실행 가능하다.

### 정의 방법
1. 
task 테스크명 {
... 수행할 문장 ...
}

2. 
task (테스크명) {
... 수행할 문장...
}


3.
task ('테스크명') {
... 수행할 문장...
}

ex) 
task hello {
println('hello 테스크')
}

실행 => $ gradle hello