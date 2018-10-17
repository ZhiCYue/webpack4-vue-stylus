# webpack4+vue+stylus


## 运行
- 安装依赖  
```npm install```  
- 本地运行  
```npm run dev```  
- 生产环境  
```npm run build```  

## 附：从零基础配置过程

- 初始化项目  
```mkdir my-project && cd my-project```  
```npm init```
```txt
my-project
  package.json                  #引导页面 
```
- vue

- 安装vue webpack  
```npm i webpack webpack-cli vue vue-router vue-loader```  
Tip: webpack4 版本需要安装webpack-cli  
根据提示继续安装相应依赖  
```npm i css-loader vue-template-compiler```

- 配置文件webpack  
  1. 新建webpack.config.js  
  ```js
  const path = require('path')

  module.exports = {
    entry: path.join(__dirname, 'src/index.js'),
    output: {
      filename: 'bundle.js',
      path: path.join(__dirname, 'dist')
    }
  }
  ```

  2. src/index.js
  ```js
  import Vue from 'vue'

  const root = document.createElement('div')
  document.body.appendChild(root)

  new Vue({
    render: (h) => h(App)
  }).$mount(root)

  ```

## 附：搭建坑点
- webpack添加loader时，配置stylus预处理器编写正则表达式时，`test: /\.styl$/` 的写法会出错，需要去掉后面的正则结束符号($)
- webapck4 废弃了CommonChunkPlugin，改为optimization; 同时废弃了css提取插件，改为MiniCssExtractPlugin插件


