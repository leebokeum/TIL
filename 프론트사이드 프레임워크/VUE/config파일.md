### vue.config.js
- 루트 디렉토리(package.json 옆)에 vue.config.js 생성하면 vue-cli가 파일을 자동으로 로드한다.
- package.json 의 vue 필드에 설정 값 적을 수 있지만 웬만해서는 vue.config.js에 적는다.
- vue.config.js는 개발서버를 담당하는 @vue/cli-service에서 자동으로 로딩하는 파일로 vue cli의 환경 설정과 webpack 설정 등을 변경등을 할 수 있다. 일반적으로 webpack 사용시에는 webpack.config.js 를 직접 수정하지만, vue cli를 사용할 경우에는 vue.config.js를 통해 webpack까지 설정이 가능하다.

```js
module.exports = {
    devServer: {
        // 사용자 정의 환경 변수에서 VUE_APP_PORT가 있으면 사용하고
        // 없으면 3000 포트로 개발서버를 실행합니다.
        port: process.env.VUE_APP_PORT || 3000
    }
}
```


#### import 경로 alias @
```js
// 경로: 루트 디렉토리/vue.config.js
const path = require('path');

module.exports = {
    configureWebpack: {
        resolve: {
            alias: {
                '@': path.join(__dirname, 'src/')
            }
        }
    }
}
```
- 인텔리 제이에 설정
  - Preference > Languages&Frameworks > Javascript > Webpack 에 webpack.config.js 파일
  - node_modules/@vue/cli-service/webpack.config.js