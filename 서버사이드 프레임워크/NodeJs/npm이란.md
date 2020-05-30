### npm(Node Pacackage Manager)이란
- Node.js pakage(module)을 관리해주는 툴
- Node.js로 만들어진 모듈을 웹에서 받아서 설치하고 관리해주는 프로그램
- Java랑 비교를 하자면 메이븐과 비슷한 역할

#### package.json
- 설치한 패키지들을 관리하는 파일이 package.json(모듈의 의존성을 한꺼번에 관리)
- npm init을 실행하면 생긴다.
~~~ javascript
{
  "name": "application-study",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "dependencies": {
    "http-server": "0.9.0",
    "rimraf": "2.6.1",
    "webpack": "2.2.1",
    "worker-loader": "0.8.0"
  },
  "scripts": {
    "prebuild": "rimraf dist",
    "build": "webpack --config webpack/webpack.config.js",
    "http-server": "http-server -c-1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/aaa/bbb.git"
  },
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/aaa/bbb/issues"
  },
  "homepage": "https://github.com/aaa/bbb#readme"
}
~~~
- package name : 패키지의 이름이다.
- version : 패키지의 버전이다.
- entry porint : 자바스크립트 실행 파일 진입점이다. 보통 마지막으로 module.exports를 하는 파일을 지정한다.
- test command : 코드를 테스트할 때 입력할 명령어를 의미한다.
- git repository : 코드를 저장해둔 git 저장소 주소를 의미한다.
- keywords : 키워드는 npm 공식 홈페이지에서 패키지를 쉽게 찾을 수 있게 해 준다.
- license : 해당 패키지의 라이선스를 넣어주면 된다.
- script는 run 명령어를 통해서 실행할 명령어 명시
- dependencies의 경우는 설치할 모듈을 의미


#### 패키지 설치하기
- package.json 파일이 정리되면 배포를 해야 할 때  파일만 같이 배포를 한다면 해당 프로그램 개발에 사용되었던 모듈을 그대로 인스톨할 수 있게 된다.
- npm install

### 단일 패키지 설치
- npm install 패키지명