### ESLint란
- ESLint는 ES 와 Lint를 합친 것
- ES는 Ecma Script로서, Ecma라는 기구에서 만든 Script, 즉, 표준 Javascript를 의미하고 Lint는 에러가 있는 코드에 표시를 달아놓는 것을 의미한다.
- 따라서, ESLint는 자바스크립트 문법에서 에러를 표시해주는 도구이다. 정말 문제가 되는 부분만을 지정할 수도 있고, 아니면 전반적인 코딩스타일(ex. tab 설정, ; 여부 등)까지 지정할 수도 있다.

* 미리 스타일과 규칙이 정해진 rule 을 적용시킬 수 있다.
* 개발자가 자신만의 스타일과 규칙을 유동적으로 정해서 적용할 수 있다.


### ESLint 사용법
.eslintrc.js 파일을 생성하고 정해진 rule 혹은 자신만의 rule 을 적용할 수 있다.
ESLint 의 세부 설정은 package.json 파일의 eslintConfig 부분에서 설정하거나 또는 .eslintrc.js 파일에서 rule 을 json 형식으로 설정할 수 있다.

1. 설치
npm install -D eslint
2. ESLint를 초기화
.\node_modules\.bin\eslint --init

3. 모든 파일의 에러를 보고 싶다면,
.\node_modules\.bin\eslint [파일명|디렉토리]
4. 모든 파일 fix하고 싶다면,
.\node_modules\.bin\eslint ** --fix
5. 확장자 .js 파일만 fix하고 싶다면,
.\node_modules\.bin\eslint **/*.js --fix


.eslintrc 형식
~~~ js
env: {
    browser: true,
    es6: true,
    node: true
  },
	( 사용 환경 )
  extends: ["airbnb-base", "prettier"],
	( 확장 설정 )
  globals: {
    Atomics: "readonly",
    SharedArrayBuffer: "readonly"
  },
	( 전역 변수 )
  parserOptions: {
    ecmaVersion: 2018,
    sourceType: "module"
  },
( 버전과 모듈 사용 여부 )
  rules: {
    "no-console": 0,
    "func-names": 0
  }
( 세부 설정 )
};
~~~