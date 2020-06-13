### webpack.config.js
- entry
  - 가장 대표가 되는 파일
- module
  - 
- plugins
- output

~~~ js
const path = require('path');
const VueLoaderPlugin = require('vue-loader/lib/plugin');
module.exports ={
    mode: 'development',
    devtool: 'evel',
    resolve:{
        extensions : ['.js', '.vue']
    },
    entry: {
        app: path.join(__dirname, './main.js')
    },
    module:{
        rules:[{
            test: /\.vue$/, // 파일명이 .vue로 끝나느 파일 
            loader: 'vue-loader' //처리할 모듈 loader 대신 use로 해도 된다
        },{
            test: /\.css$/, // 파일명이 .vue로 끝나느 파일 
            loader: [
                'vue-style-loader', 
                'css-loader'
                ] //처리할 모듈 loader 대신 use로 해도 된다
        }], //어떻게 합칠지
    },
    output:{
        filename: 'app.js', //하나로 합쳐질 파일 이름
        path: path.join(__dirname, './dist') , //파일이 생성될 경로
        publicPath: '/dist'
    }
}
~~~