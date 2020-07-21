# Vue



创建vue对象

```js
var app = new Vue({
    
})
```



## vue属性：

**el:** 挂载html元素

**data:** 存放数据，如常量变量列表等

**methods:** 定义方法

**computed:** 计算属性

> 需要对属性进行某种变换后再显示使用计算属性
>
> 因为计算属性会缓存，所以比methods高效
>
> computed是值调用，methods是方法调用
>
> filter/map/reduce（高阶函数）

**filters:** 过滤器

> {{需要过滤的东西 | 过滤器}}
>
> {{price | showPrice}}

**key:** 绑定给item，提高插入效率

**components:** 组件

```js
components: {
    mycpn: cpnConstructor		//前者是标签名， 后者是组件构造器
}
```

**watch:** 监听





## vue指令：

**v-for:** 循环

> v-for="item in list"
>
> 遍历数组，同时获取索引		(item, index) in list
>
> 遍历对象，如果只获取一个值，那么获取到的是value；同时获取key 和 value用(key, value)

**v-if、v-else和v-else-if:** 条件判断

**v-on:** 事件监听

> v-on:click="const++"
>
> 缩写@
>
> 参数：
>
> > ①如果调用方法没有参数，可以直接写参数名
> >
> > ②如果调用方法需要参数，但是没有传入，参数就会显示为 undefine
> >
> > ③如果调用方法需要参数，但是写方法时省略了小括号，vue会默认将浏览器生成的 event对象作为参数传给方法
> >
> > ④手动获取浏览器生成的 event 对象，需要用 $event
>
> 修饰符：
>
> > .stop		阻止事件
> >
> > .prevent		阻止默认事件
> >
> > .keyCode / .keyAlias		当特定键触发时才会回调
> >
> > > keyCode 键盘编码
> > >
> > > keyAlias 键盘别名
> >
> > .once		只触发一次回调
> >
> > .native		监听组件根元素的原生事件

**v-once:** 表示元素或组件只渲染一次，不会随着数据的改变而改变

> 直接在标签后面添加v-once

**v-html:** 解析html

> v-html="url"

**v-text:** 展示文本（会覆盖原标签内容）

> v-text="str"

**v-pre:** 转义（原封不动展示标签内容）

> 直接在标签后面添加v-pre

**v-bind:** 动态绑定属性

> v-bind:src="url"
>
> 缩写：
>
> :src="url"

动态绑定对象

> v-bind:class="{key1: value1, key2:valu2}"
>
> v-bind:class="{类名1:boolean, 类名2:boolean}"
>
> v-bind:class="{类名1:true. 类名2:false }"		类一会被绑定，类二不会被绑定

**v-show:** 判断是否显示

> 如果为false，给元素添加一个行内样式：display : none

**v-model:** 表单元素和数据双向绑定

​		修饰符：（v-model**.**lazy / number / trim）

> **lazy**
>
> > 默认情况下，v-model在 input 事件中同步输入框的数据，一旦数据发生改变，对应的 data 中的数据就会自动发生改变
> >
> > lazy修饰符可以让数据在失去焦点或者回车时才会更新
>
> **number**
>
> > 默认情况下，在输入框中无论我们输入的是字母还是数字，都会被当作字符串类型进行处理
> >
> > number修饰符可以让输入框中输入的内容自动转成数字类型
>
> **trim**
>
> > 如果输入的内容首尾有很多空格
> >
> > 通过 trim 修饰符可以过滤内容左右两边的空格



## vue组件：

### 构造组件

- 调用 Vue.extend() 方法创建组件构造器

```html
const cpnConstructor = Vue.extend({
    template: `
	<div>
		<h2>我是标题</h2>
	</div>
`
})
```



- 调用 Vue.component ()方法注册组件

```js
Vue.component('mycpn', cpnConstructor)		//前一个参数是标签名， 后一个参数是组件构造器
```



- 使用组件

> 要在Vue实例作用范围内



### 父子组件

- 在一个组件里面注册另外一个组件，这样就是父子组件

```html
const cpnConstructor1 = Vue.extend({
    template: `
	<div>
		<h2>我是父组件</h2>
	</div>
`,
    components: {
        cpn2: cpnConstructor2
    }
})

const cpnConstructor2 = Vue.extend({
    template: `
	<div>
		<h2>我是子组件</h2>
	</div>
`
})
```



### 组件data

> 组件不能访问 vue 实例中的数据，所以组件必须拥有自己的data
>
> 这个data不能是对象，只能是函数，而且该函数必须返回一个对象
>
> > 使各个模板的数据相互独立，防止连锁



### 父子组件通信

1. 通过props向子组件传递数据
2. 通过事件向父组件发送信息



**props（父传子）:**

> 在组件中，使用选项props来声明需要从父级接收到的数据
>
> > 字符串数组，数组中的字符串就是传递时的名称
> >
> > 对象，对象可以设置传递时的类型，也可以设置默认值等
>
> 如果需要保存输入控件的值，不能直接修改props，而是在data中创建变量保存输入的值

```html
<div id="app">
  <cpn :cmovies="movies" :cmessage="content" >{{cmovies}}</cpn>
</div>

<template id="cpn">
  <div>
    <h2>{{cmovies}} {{cmessage}}</h2>
  </div>
</template>

<script>
  const cpn = {
    template: '#cpn',
    props: ["cmovies", "cmessage"],
    props: {
    cmovies: array,
    cmessage: {
        type: String,
        default: [],
        required: true,
    }
    },
    data() {
      return {
      }
    }
  }
</script>
```

**属性:**

> type		规定参数类型
>
> default		定义默认值
>
> required		是否必须（boolean类型）



**子传父：**

> 子组件响应，自定义事件传给父组件
>
> 父组件监听，收到事件做出回应

```html
<div id="app">
  <cpn @itemclick="cpnclick"></cpn>
</div>

<template id="cpn">
  <div>
    <button v-for="item in categories" @click="btnclick">{{item.name}}</button>
  </div>
</template>

<script>
  // noinspection JSAnnotator
  const cpn = {
    template: "#cpn",
    data() {
      return {
        categories: [
          {id:"aaa", name:"热门推荐"},
          {id:"bbb", name:"手机数码"},
          {id:"ccc", name:"家用电器"},
          {id:"ddd", name:"电脑办公"},
        ]
      }
    },
    methods: {
      btnclick(item) {
        this.$emit("itemclick", item)
      }
    }
  }

  const app = new Vue({
    el: '#app',
    data: {
    },
    components: {
      cpn
    },
    methods: {
      cpnclick(item) {
        console.log("cpnclick")
      }
    }
  })
</script>
```



**属性：** 

#### $children 和 $refs

> 通过$children可以获得子组件
>
> > $children是一个数组，包含该父组件下的所有子组件
>
> ```js
> this.$children[0]		//获取第一个子组件
> ```

> ref 给子组件编号，再通过$refs 既可以获取组件
>
> ```js
> <cpn ref="aaa"></cpn>
> 
> this.$refs.aaa		//获取编号为aaa的组件
> // $refs => 对象类型，默认是空的对象
> ```

#### $parent 和 $root

用的比较少

> 通过 $parent 获取父组件
>
> ```js
> console.log(this.$parent)
> ```

> 通过 $root 访问根组件
>
> ```js
> console.log(this.$root)
> ```



### 组件高级

**slot:** 预留空间

```html
<div id="app">
  <cpn>
    <h2>替换元素</h2>		//替换元素，会替换掉插槽中的默认元素
  </cpn>
</div>

<template>
  <div>
    <h2>我是组件</h2>
    <slot>
        <button>button</button>
    </slot>
  </div>
</template>
```





## 数组方法：

**push:** 进栈，响应式

**pop:** 出栈，响应式

**shift:** 进队列，响应式

**unshift:** 出队列，响应式

**splice:** （开始索引，删除数量，替换值），响应式

**sort:** 排序，响应式

**reverse:** 反转，响应式



**通过数组索引更改元素是非响应式的**



## JS高阶函数：

```js
for (let item of list)
```



**filter:** 

> filter中的回调函数必须返回一个boolean值
>
> 当返回 true时，函数内部会自动将这次回调的 n 加入新的数组
>
> 当返回 false时，函数内部会过滤掉这次的n

```js
let newnums = nums.filter(function(n) {
    return n < 100
})
```



**map:** 

```js
let newnums = nums.map(function(n) {
    return n * 2
})
```



**reduce:** （汇总）

```js
let newnums = nums.reduce(function(prevalue, n) {
    return prevalue + defaultvalue
}, defaultvalue)
```



## 其他：

> 在 ES6 中，常量所指向的对象不可修改，但是对象的属性可以进行修改---除非对象需要更改，否则一般定义对象都用 const