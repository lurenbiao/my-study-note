# webpack的使用

### webpack的下载命令

 cmd全局安装webpack。-g:全局安装 

```css
npm install webpack@4 -g
```

 cmd全局安装webpack-cli包 

```css
npm install webpack-cli@3
```

再安装webpack。-D：开发环境依赖

```css
npm install webpack@4 -D
```

安装webpack-cli

```css
npm install webpack-cli@3
```

 

### webpack配置文件	

​	webpack.config.js为文件名

```js
const path = require('path')  //使用node.js中的导出语法，向外导出一个webpack的配置对象

module.exports = {
    //代表webpack的运行模式，可选择的有development和production
    //结论：开发的时候一定要用development,因为追求的是打包速度，而不是体积
    //开发上线的时候一定要使用production,因为追求体积小，而不是打包速度
    mode: 'development',

    // 自定义打包出口和入口
    // entry:'指定要处理哪个文件'
    entry: part.join(__dirname, './src/index.js'), //打包入口文件路径

    //指定生成的文件存放哪里
    output: {
        path: path.join(__dirname, 'dist'), //存放目录
        filename: 'boudle.js' //生成的文件名

    }
}

```





### webpack的默认约定

- 默认打包入口文件为 src ->index.js

- 默认输出文件路劲为 dist ->main.js

- 注意：可以在bebpack.config.js中修改打包的默认约定

  **自定义打包的入口与出口**

  在webpack.config.js 配置文件中，通过entry节点指定打包入口，通过output节点指定打包的出口。

  

### webpack中的插件

#### 	1.webpack插件的作用

 通过安装和配置第三方的插件,可以拓展webpack的能力,从而让webpack用起来更方便。最常用的webpack 插件有如下两个: 

1.  **webpack-dev-server** 

-  类似于node.js阶段用到的nodemon工具 
-  每当修改了源代码,webpack会自动进行项目的打包和构建 

2. **html-webpack-plugin** 

-  webpack 中的HTML 插件(类似于一个模板引擎插件) 

-  可以通过此插件自定制index.html页面的内容 

  

  #### 2.1安装webpack-dev-serve

运行如下命令，即可在项目中安装此插件：

```javascript
npm install webpack-dev-server --save-dev 
```

#### 	2.2配置webpack-dev-server

1. 修改package.json->script中的dev命令如下：

   ```
    "scripts": {
   
     "dev": "webpack serve"   //
   
    },
   ```

   

2. 再次允许npm run dev 命令，重新进行项目打包

3. 在流浪器中访问htttp://localhost:8080地址，查看自动打包效果	

   注意：webpack-dev-server会启动一个实时打包的http服务器