---
title: vue2与vue3的区别
date: 2021-06-28
author: 夏明
---

## vue2和vue3双向数据绑定原理发生了改变

vue2的双向数据绑定是利用ES5的一个`API Object.definePropert()`对数据进行劫持结合发布订阅模式的方式来实现的。

vue3中使用了es6的`Proxy`API对数据代理。

> 相比于vue2.x，使用proxy的优势如下
>1. defineProperty只能监听某个属性，不能对全对象监听
>2. 可以省去for in、闭包等内容来提升效率（直接绑定整个对象即可）
>3. 可以监听数组，不用再去单独的对数组做特异性操作，vue3.x可以检测到数组内部数据的变化

##  Vue3支持碎片(Fragments)

就是说在组件可以拥有多个根节点。

### vue2

```html
<template>
  <div class='form-element'>
  <h2> {{ title }} </h2>
  </div>
</template>
```

### vue3

```html
<template>
  <div class='form-element'>
  </div>
   <h2> {{ title }} </h2>
</template>
```

## Composition API

Vue2与Vue3 最大的区别 — Vue2使用选项类型API（Options API）对比Vue3合成型API（Composition API）

> 旧的选项型API在代码里分割了不同的属性: data,computed属性，methods，等等。新的合成型API能让我们用方法（function）来分割，相比于旧的API使用属性来分组，这样代码会更加简便和整洁。

### vue2

```javascript
export default {
  props: {
    title: String
  },
  data () {
    return {
      username: '',
      password: ''
    }
  },
  methods: {
    login () {
      // 登陆方法
    }
  },
  components: {
            "buttonComponent": btnComponent
        },
  computed: {
	  fullName() {
	    return this.firstName + " " + this.lastName;     
	  }
  }
}
```

### vue3

```javascript
export default {
  props: {
    title: String
  },
  setup () {
    const state = reactive({ //数据
      username: '',
      password: '',
      lowerCaseUsername: computed(() => state.username.toLowerCase()) //计算属性
    })
     //方法
    const login = () => {
      // 登陆方法
    }
    return { 
      login,
      state
    }
  }
}
```

## 建立数据 data

### Vue2 - 这里把数据放入data属性中

```javascript
export default {
  props: {
    title: String
  },
  data () {
    return {
      username: '',
      password: ''
    }
  }
}
```

在Vue3.0，我们就需要使用一个新的setup()方法，此方法在组件初始化构造的时候触发。

使用以下三步来建立反应性数据:

1. 从vue引入reactive

2. 使用reactive()方法来声名我们的数据为响应性数据

3. 使用setup()方法来返回我们的响应性数据，从而我们的template可以获取这些响应性数据

```javascript
import { reactive } from 'vue'

export default {
  props: {
    title: String
  },
  setup () {
    const state = reactive({
      username: '',
      password: ''
    })

    return { state }
  }
}
```

template使用，可以通过state.username和state.password获得数据的值。

```html
<template>
  <div>
    <h2> {{ state.username }} </h2>
  </div>
</template>
```

## 生命周期钩子 — Lifecyle Hooks

```
Vue2--------------vue3
beforeCreate  -> setup()
created       -> setup()
beforeMount   -> onBeforeMount
mounted       -> onMounted
beforeUpdate  -> onBeforeUpdate
updated       -> onUpdated
beforeDestroy -> onBeforeUnmount
destroyed     -> onUnmounted
activated     -> onActivated
deactivated   -> onDeactivated
```

1. setup() :开始创建组件之前，在beforeCreate和created之前执行。创建的是data和method

2. onBeforeMount() : 组件挂载到节点上之前执行的函数。

3. onMounted() : 组件挂载完成后执行的函数。

4. onBeforeUpdate(): 组件更新之前执行的函数。

5. onUpdated(): 组件更新完成之后执行的函数。

6. onBeforeUnmount(): 组件卸载之前执行的函数。

7. onUnmounted(): 组件卸载完成后执行的函数

若组件被`<keep-alive>`包含，则多出下面两个钩子函数。

1. onActivated(): 被包含在中的组件，会多出两个生命周期钩子函数。被激活时执行 。

2. onDeactivated(): 比如从 A组件，切换到 B 组件，A 组件消失时执行。

## 父子传参不同，setup() 函数特性

### 总结

1、setup 函数时，它将接受两个参数：（props、context(包含attrs、slots、emit)）

2、setup函数是处于 生命周期函数 beforeCreate 和 Created 两个钩子函数之前的函数

3、执行 setup 时，组件实例尚未被创建（在 setup() 内部，this 不会是该活跃实例的引用，即不指向vue实例，Vue 为了避免我们错误的使用，直接将 setup函数中的this修改成了 undefined）

4、与模板一起使用：需要返回一个对象 (在setup函数中定义的变量和方法最后都是需要 return 出去的 不然无法再模板中使用)

5、使用渲染函数：可以返回一个渲染函数，该函数可以直接使用在同一作用域中声明的响应式状态

### 注意事项

1、setup函数中不能使用this。Vue 为了避免我们错误的使用，直接将 setup函数中的this修改成了 undefined）

2、setup 函数中的 props 是响应式的，当传入新的 prop 时，它将被更新。但是，因为 props 是响应式的，你不能使用 ES6 解构，因为它会消除 prop 的响应性。

如果需要解构 prop，可以通过使用 setup 函数中的`toRefs`来完成此操作：

#### 父传子，props

```javascript
import { toRefs } from 'vue'
 
setup(props) {
	const { title } = toRefs(props)
 
	console.log(title.value)
	 onMounted(() => {
      console.log('title: ' + props.title)
    })

}
```

#### 子传父，事件 - Emitting Events

举例，现在我们想在点击提交按钮时触发一个login的事件。

在 Vue2 中我们会调用到this.$emit然后传入事件名和参数对象。

```javascript
login () {
      this.$emit('login', {
        username: this.username,
        password: this.password
      })
 }
```

在setup()中的第二个参数content对象中就有emit，这个是和this.$emit是一样的。那么我们只要在setup()接收第二个参数中使用分解对象法取出emit就可以在setup方法中随意使用了。

然后我们在login方法中编写登陆事件

另外：context 是一个普通的 JavaScript 对象，也就是说，它不是响应式的，这意味着你可以安全地对 context 使用 ES6 解构

```javascript
setup (props, { attrs, slots, emit }) {
    // ...
    const login = () => {
      emit('login', {
        username: state.username,
        password: state.password
      })
    }

    // ...
}
```

3、setup()内使用响应式数据时，需要通过.value获取

```javascript
import { ref } from 'vue'
 
const count = ref(0)
console.log(count.value) // 0
```

4、从 setup() 中返回的对象上的 property 返回并可以在模板中被访问时，它将自动展开为内部值。不需要在模板中追加 .value

5、setup函数只能是同步的不能是异步的

## vue3 Teleport瞬移组件

Teleport一般被翻译成瞬间移动组件,实际上是不好理解的.我把他理解成"独立组件",他可以拿你写的组件挂载到任何你想挂载的DOM上,所以是很自由很独立的

以一个例子来看:编写一个弹窗组件

```html
<template>
<teleport to="#modal">
  <div id="center" v-if="isOpen">
    <h2><slot>this is a modal</slot></h2>
    <button @click="buttonClick">Close</button>
  </div>
</teleport>
</template>
<script lang="ts">

export default {
  props: {
    isOpen: Boolean,
  },
  emits: {
    'close-modal': null
  },
  setup(props, context) {
    const buttonClick = () => {
      context.emit('close-modal')
    }
    return {
      buttonClick
    }
  }
}
</script>
<style>
  #center {
    width: 200px;
    height: 200px;
    border: 2px solid black;
    background: white;
    position: fixed;
    left: 50%;
    top: 50%;
    margin-left: -100px;
    margin-top: -100px;
  }
</style>
```

在app.vue中使用的时候跟普通组件调用是一样的

```html
<template>
<div id="app">
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <HooksDemo></HooksDemo>
  <button @click="openModal">Open Modal</button><br/>
<modal :isOpen="modalIsOpen" @close-modal="onModalClose"> My Modal !!!!</modal>
</div>
  
</template>
<script>
import HelloWorld from './components/HelloWorld.vue'
import HooksDemo from './components/HooksDemo.vue'
import Modal from './components/Modal.vue'
import{ref} from 'vue'
export default {
  name: 'App',
  components: {
    HelloWorld,
    HooksDemo,
    Modal
  },
  setup() {
    const modalIsOpen = ref(false)
    const openModal = () => {
      modalIsOpen.value = true
    }
    const onModalClose = () => {
      modalIsOpen.value = false
    }
    return {
      modalIsOpen,
      openModal,
      onModalClose
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

要是在app.vue文件中使用的时候,modal是在app的 DOM节点之下的,父节点的dom结构和css都会给modal产生影响

于是产生的问题

1. modal被包裹在其它组件之中，容易被干扰

2. 样式也在其它组件中，容易变得非常混乱

Teleport 可以把modal组件渲染到任意你想渲染的外部Dom上,不必嵌套在#app中,这样就可以互不干扰了,可以把Teleport看成一个传送门,把你的组件传送到任何地方

使用的时候 to属性可以确定想要挂载的DOM节点下面

```html
<template>
  <teleport to="#modal">
    <div id="center">
      <h2>夏明</h2>
    </div>
  </teleport>
</template>
```

在public文件夹下的index.html中增加一个节点

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <link rel="icon" href="<%= BASE_URL %>favicon.ico">
    <title><%= htmlWebpackPlugin.options.title %></title>
  </head>
  <body>
    <noscript>
      <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>
    <div id="app"></div>
    <div id="modal"></div>
    <!-- built files will be auto injected -->
  </body>
</html>
```

这样可以看到modal组件就是没有挂载在app下,不再受app组件的影响了
