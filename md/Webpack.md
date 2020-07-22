# Webpack



<font color="#DE907B">**what:**</font> 

> 前端模块化打包工具



**<font color="#DE907B">src:</font>** 存放源码

**<font color="#DE907B">dist:</font>** 存放打包文件

**<font color="#DE907B">build:</font>** 存放配置文件



## <font color="#DE907B">CommonJS导入语法：</font> 

```js
const application = require('application')

module.exports = {
    
}
```





## <font color="#DE907B">webpack.config.js</font> 

```js
const path = require('path')

module.exports = {
    entry: "./src/",		//入口
    output: {
        path: path.resolve(__dirname, 'dist'),		//动态获取路径
        filename: "bundle.js"
    },		//出口
    resolve: {		//指定发布版本
        alias: {	//alias：别名
            'vue$': 'vue/dist/vue.esm.js'
        }
    }
}
```

> --save-dev	开发时依赖
>
> --save	运行时依赖



> **webpack loader <font color="#DE907B">（未学）</font>** 
>
> loader是一种打包的方案，webpack默认只识别js结尾的文件，当遇到其他格式的文件后，webpack并不知道如何去处理。
>
> p78-p81

> **loader 和 plugin 的区别**
>
> loader 主要用于转换某些类型的模块，它是一个转换器
>
> plugin 是插件，它是对 webpack 本身的扩展，是一个扩展器

> **webpack plugin**
>
> 对 webpack 现有功能的各种扩展，如打包优化，文件压缩等
>
> 使用过程：
>
> > 通过 npm 安装需要使用的plugins
> >
> > 在 webpack.config.js 中的 plugins 中配置插件
>
> 添加版权声明，横幅插件 **<font color="#DE907B">（未学）</font>** 
>
> 打包 html 的插件，HtmlWebpackPlugin **<font color="#DE907B">（未学）</font>** 
>
> 压缩 js 文件的插件，uglifyjs-webpack-plugin **<font color="#DE907B">（未学）</font>**	//不建议使用



> vue在构建最终发布版本时，有两个版本	runtime-only 和 runtime-compiler	
>
> > <font color="#DE907B">runtime-only</font>	代码中不可以有任何 template
> >
> > <font color="#DE907B">runtime-compiler</font>	代码中可以有 template



##  <font color="#DE907B">package.json</font> 

> 通过 **<font color="#DE907B">npm init</font>** 生成
>
> 通过在这个文件中配置脚本来在终端中通过相应的命令运行webpack（这样就会首先使用本地的配置去打包项目而非全局）
>
> 如通过 
>
> ```bash
> run serve buil
> ```
>
> 运行 webpack
>
> ```json
> {
>  "name": "meetwebpack",
>  "version": "1.0.0",
>  "description": "",
>  "main": "index.js",
>  "script": {
>      "test": "echo \"Error: no test specified\" && exit 1",
>      "build": "webpack"		//配置，这样就可以通过 run serve build 来使用webpack进行打包
>  },
>  "author": "",
>  "license": "ISC",
> }
> ```
>



## <font color="#DE907B">webpack-dev-server</font> 

> 搭建本地服务器，实时监听文件内容
>
> 需要配置脚本才能启动，一般通过命令 
>
> ```bash
> webpack-dev-server
> ```
>
> 在用这个命令之前要先在 package.json 中进行脚本配置
>
> ```json
> devServer: {
>  contentBase: "./dist",		//检测文件夹
>  inline: true,		//是否实时监听
>  port: 8080,		//指定端口， 默认8080
> }
> ```
>



## <font color="#DE907B">配置文件的分离</font>

> **<font color="#DE907B">base.config</font>** 		基本配置文件
>
> **<font color="#DE907B">pro.config</font>** 		开发配置文件
>
> **<font color="#DE907B">dev.config</font>** 		生产配置文件
>
> > 开发环境（development）
> > 开发环境是程序猿们专门用于开发的服务器，配置可以比较随意， 为了开发调试方便，一般打开全部错误报告。(程序员接到需求后，开始写代码，开发，运行程序，看看程序有没有达到预期的功能；)
> >
> > 测试环境（testing）
> > 一般是克隆一份生产环境的配置，一个程序在测试环境工作不正常，那么肯定不能把它发布到生产机上。(程序员开发完成后，交给测试部门全面的测试，看看所实现的功能有没有bug，测试人员会模拟各种操作情况；)
> >
> > 生产环境（production）
> > 生产环境是指正式提供对外服务的，一般会关掉错误报告，打开错误日志。(就是线上环境，发布到对外环境上，正式提供给客户使用的环境。)
> >
> > 三个环境也可以说是系统开发的三个阶段：开发->测试->上线，其中生产环境也就是通常说的真实环境。

> ```bash
> npm install webpack-merge		
> ```
>
> /merge 合并
>
> ```js
> const webpackMerge = require('webpack-merge')
> const baseConfig = require('./base.config')
> 
> module.exports = webpackMerge(baseConfig, {
>  "生产配置"
> })
> ```
>
> 指定配置文件
>
> > 在 package.json 中更改脚本
> >
> > 如：
> >
> > ```json
> > "build": "webpack --config ./build/pro.config.js"
> > ```
> >

