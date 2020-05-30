### ESLint란
ESLint란, 2013년 6월에 Nicholas C. Zakas가 처음 만든 오픈소스 JavaScript Linting 유틸리티이다. 코드 Linting 이란 특정 스타일 규칙을 준수하지 않는 문제가 있는 소스코드를 찾는데 사용되는 방식을 말하며, Linter 는 이러한 Linting 을 수행하는 도구이다.
대부분의 프로그래밍 언어에는 컴파일하는 과정이 있어서 컴파일시 수행되는 Linter 가 내장되어있다.
그러나 역동적이고 느슨한 언어인 JavaScript는 이러한 Linter 가 존재하지 않는다. JavaScript는 별도의 컴파일 과정이 없고, Node나 Browser에서 바로 실행되기 때문이다.
따라서 일반적인 JavaScript 개발시 구문 오류나 기타 오류를 찾기 위해서는 실제 실행까지 시켜봐야한다.
하지만 ESLint 같은 Linting 도구를 사용하면 JavaScript를 실행하지 않고도 기본적인 문제를 발견할 수 있다.