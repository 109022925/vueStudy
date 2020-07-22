# VueCLI



> **CLI:** Command-Line Interface
>
> **NPM:** Node Package Manager
>
> vuecli -> webpack -> node

> 安装 vuecli 脚手架
>
> ```bash
> npm install -g @vue/cli
> ```
>
> > 如果需要使用**2.X**版本，需要拉取模板
> >
> > ```bash
> > npm install -g @vue/cli-init
> > ```
> >
> > <font color="#DE907B">Vue CLI2</font> 初始化项目
> >
> > ```bash
> > vue init webpack my-project
> > ```
> >
> > <font color="#DE907B">Vue CLI3 或 Vue CLI4</font> 初始化项目
> >
> > ```bash
> > vue create my-project
> > ```



> <font color="#DE907B">Vue CLI2</font> 目录架构
>
> build 和 config 是关于webpack的相关配置
>
> nude_modules 依赖的 node 相关的模块
>
> src 写代码的地方
>
> static 存放静态资源如图片
>
> .babelrc	对JS代码进行转换的配置
>
> .editorconfig	编辑配置
>
> .eslintignore	存放不需要严格代码规范的文件
>
> .gitignore	存放不需要上传到 git 的文件
>
> .postcssrc.js	css代码转换的相关配置
>



Vue程序运行过程

**<font color="#DE907B">runtimeCompiler 和 runtimeOnly</font>** 

> runtimeCompiler
>
> > template -> ast -> render -> vdom -> UI
>
> runtimeOnly
>
> > render -> vdom -> UI
>
> render	渲染

![Vue程序运行过程](D:\WebStorm程序\vueStudy\Vue程序运行过程.png)



```js
new Vue({
    render: h => h(App),
}).$mount('#app')		//$mount执行挂载任务
```



修改配置，在根目录下创建 vue.config.js ，这样这个文件的配置会和webpack的配置合并

```js
module.exports = {
    
}
```



