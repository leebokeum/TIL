### webpack 사용법
- webpack으로 어디를 번들링해서 패키징을 할지 설정을 해줘야 한다.
- 프로젝트 경로 가장 상단에 webpack.config.js 라는 파일을 만들어 준다.

~~~ js
const path = require('path');

module.exports = {
    entry: path.resolve(__dirname, 'src', 'index.js'), 
    output: { 
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    }
}
~~~
![alt text](https://steemitimages.com/DQmWBpBVNtyGzAXUa9CaHnTdnKEW5xkAYKhVb4kBD4deEm5/image.png)
- entry로 지정된 파일을 읽어 들이기 시작하며 import 혹은 require 등 다른파일을 불러오고 있는 파일들을 추적해서 하나의 파일로 만들어 준다.
- 번들링 된 파일은 output에 설정한대로 파일이 생성되어 진다.
  
### plugins
- 소스코드가 번들링 될 때 추가적인 작업을 더 진행하는 개념

~~~ js
const webpack = require('webpack');
  entry: ..,
  output: ..,
  plugins: [
        new webpack.optimize.UglifyJsPlugin()
  ]
}
~~~