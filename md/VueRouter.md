# <font color="#BF473E">Vue-Router</font> 



<font color="#BF473E">routing</font> 

> 通过互联的网络把信息从源地址传输到目的地址的活动



## <font color="#BF473E">前端渲染、后端渲染</font> 

> <font color="#CCA6A3">后端渲染</font> 
>
> > 服务器端已经渲染好，直接发送给浏览器
> >
> > html+css+java
> >
> > java代码的作用是从数据库中读取数据，并将其动态放在页面中
>
> <font color="#CCA6A3">后端路由</font> 
>
> > 后端处理URL和页面之间的映射关系

> <font color="#CCA6A3">前端渲染</font> 
>
> 前后端分离，后端只负责提供数据，不负责提供任何阶段的内容
>
> > 浏览器中显示的网页中的大部分内容，都是由前端写的 js 代码在浏览器中执行，最终渲染出来的网页
> >
> > ![前端渲染](..\jpg\前端渲染.png)
> >
> > 1. 浏览器得到URL向静态服务器请求，得到HTML+CSS+JS
> > 2. 浏览器执行JS代码，JS代码中包含ajax，ajax向后端接口发起请求
> > 3. 后端服务器接收到请求，向前端发送数据
> > 4. 浏览器接收到数据，JS代码对数据进行处理
>
> <font color="#CCA6A3">前端路由</font> 
>
> > 单页富应用	整个网页只有一个HTML页面
> >
> > 通过JS代码进行判断，寻找资源，进行渲染
> >
> > URL ->页面



<font color="#CCA6A3">URL的hash</font>  

> URL的 hash 也就是锚点（#），本质上是改变 window.location 的 href 属性
>
> 可以直接赋值 location.hash 来改变 href，但是页面不发生刷新

<font color="#CCA6A3">HTML5的history模式</font> 

> <font color="#CCA6A3">pushState</font>
>
> 调取URL，实质是将要调取的URL压入栈
>
> ```js
> history.pushState({data}, 'title', '?url')
> ```
>
> <font color="#CCA6A3">back</font>
>
> 类似于出栈，顶部URL弹出，返回上一级
>
> ```js
> history.back()
> ```
>
> <font color="#CCA6A3">replaceState</font> 
>
> 用新的页面取代现有页面，不能返回上一级
>
> ```js
> history.replaceState({}, '', '')
> ```
>
> <font color="#CCA6A3">go</font> 
>
> pushState中有东西之后才能用这个方法
>
> ```js
> history.go(-1)	=>	history.back()
> history.go(1)	=>	history.forward()
> ```



## <font color="#BF473E">配置路由</font> 

一般在src文件夹中创建route目录存放路由配置信息

1. 导入路由对象，并且调用 Vue.use(VueRouter)
2. 创建路由实例，并且传入路由映射配置
3. 在Vue实例中挂载创建的路由实例

```js
//配置路由相关的信息
import VueRouter from 'vue-router'
import Vue from 'vue'

// 1、通过Vue.use（插件），安装插件
Vue.use(VueRouter)

// 2、创建VueRouter对象
const routes= [
    
]

const router = new VueRouter({
  // 配置路由和组件之间的应用关系
  routes,
  mode: 'history'		//将路由模式设置为history模式
})

// 3、将VueRouter对象传入Vue实例
export default router
```



## <font color="#BF473E">使用路由</font> 

1. 创建路由组件
2. 配置路由映射：组件和路径映射的关系

```js
const routes= [
  {
    path: '/home',
    component: Home
  },
  {
    path: '/about',
    component: About
  },
]
```

3. 使用路由：通过**<font color="#CCA6A3"> \<router-link> 和 \<router-view></font>** 

> **<font color="#CCA6A3">router-link</font>** 最终被渲染成 **\<a>** 标签
>
> **<font color="#CCA6A3">router-view</font>** 决定渲染出来的组件放在哪里

```html
  <div>
    <router-link to="/home">首页</router-link>
    <router-link to="/about">关于</router-link>
    <router-view></router-view>
  </div>
```



**<font color="#CCA6A3"> 设置默认路径</font>**  

```js
{
    path: '',
    redirect: '/home',		// 重定向
    component: Home
  }
```



## <font color="#BF473E">router-link属性</font> 

**<font color="#CCA6A3"> to：</font>**  

> 用于指定跳转路径

**<font color="#CCA6A3"> tag：</font>**  

> 指定 **\<router-link>** 之后渲染成什么组件

**<font color="#CCA6A3"> </font>**  **<font color="#CCA6A3"> replace：</font>** 

>  指定为 replace 模式



## <font color="#BF473E">通过代码修改路由 vue-router</font> 

**this.$router** 

```js
homeClick() {
    this.$router.push('/home')
}
```

