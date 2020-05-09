### 바벨이란?
- Babel은 자바스크립트 컴파일러로서, 최신의 자바스크립트 코드를 아주 무난한 이전 단계의 자바스크립트 코드로 변환 가능하게 해주는 개발 도구,  즉 트랜스파일러(Transpiler)이다. 이와 같은 트랜스파일러(Transpiler)가 필요한 이유는, ES6+를 사용하여 프로젝트를 진행하려면 ES6+로 작성된 코드를 IE를 포함하여 모든 브라우저에서 문제 없이 작동할 만한 개발환경을 구축해야 하기 때문이다. 즉, Babel 패키지를 활용하면 자바스크립트 최신 문법으로 자유롭게 코딩하면, 그것과 웹브라우저간의 호환을 Babel 패키지가 책임져준다.   

### 기능
1. 구문(Syntax) 변환
- const something = (a, b) => a * b; 를 입력하면, 이를 Babel이 var something = function something(a,b) { return a * b}; 로 변환해준다. 
2. (당신의 현재 환경에 없는) Polyfill 기능 
3. 소스 코드 변환



### 바벨 사용하기
~~~ javascript
    npm install --save-dev @babel/cli @babel/core @babel/preset-env @babel/preset-stage-2
~~~