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



## <font color="#BF473E">动态路由</font>  

```html
<router-link :to="'/user' + userId"></router-link>
```



$route

> 拿到当前活跃路由
>
> 获取路由中的参数

```js
this.$route.params.userId
```



## <font color="#BF473E">路由懒加载</font> 

>  当打包构建应用时，JS包会变得非常大，影响页面加载
>
> 把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件



  **<font color="#CCA6A3"> 懒加载的方式</font>** 

```js
const Home = () => import('../components/Home')

{
    path: '/home',
    component: Home
}
```



## <font color="#BF473E">嵌套路由</font> 

> 在路由映射中配置对应的子组件

```js
const Home = () => import('../components/Home')
const HomeNews = () => import('../components/HomeNews')

{
    path: '/home',
    component: Home,
    children: [
        {
            path: 'news',
            component: news
        },
        {
            
        }
    ]
}
```



## <font color="#BF473E">参数传递</font>  

  **<font color="#CCA6A3"> URL: scheme://host/path?query#fragment</font>** 

> 第一种方法：通过配置动态路由传递参数
>
> > params
> >
> > /router/123
>
> 第二种方法：通过query中的key作为传递方式
>
> > query
> >
> > /router?id=123
>
> ```html
> <router-link :to="{path: '/profile' query: {id: '123'}}"></router-link>
> ```



## <font color="#BF473E">全局导航守卫</font>  

> 监听全局页面跳转
>
> ```js
> // 前置钩子	执行前回调
> router.beforeEach((to, next, from) => {
>     // to和next都是route类型，从from跳转至to
>     document.title = to.matched[0].meta.title
>     next()		// 必须要主动调用next函数
> })
> ```
>
> ```js
> // 后置钩子	执行后回调
> // 不需要主动调用next函数
> route.afterEach((to, from) => {
>     
> })
> ```

 **<font color="#CCA6A3"> 路由独享守卫</font>** 

```js
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
})
```

 **<font color="#CCA6A3"> 组件内的守卫</font>** 

```js
const Foo = {
  template: `...`,
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    // 不！能！获取组件实例 `this`
    // 因为当守卫执行前，组件实例还没被创建
  },
  beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
  },
  beforeRouteLeave (to, from, next) {
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例 `this`
  }
}
```



---

---

---



# <font color="#BF473E">Keep-alive</font> 

> keep-live 是Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染
>
> router-view 也是一个组件，如果直接被包在keep-alive 里面，所有路径匹配到的视图组件都会被缓存



**属性：** 

> include
>
> > 字符串或正则表达式，只有匹配的组件会被缓存
>
> exclude
>
> > 字符串或正则表达式，任何匹配的组件都不会被缓存



