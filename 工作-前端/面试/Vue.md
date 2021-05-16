## 了解过（用过）react或者angular吗，他们有什么区别？

- angular： 模板和数据绑定技术
- react：组件化和虚拟` DOM` 技术

## 那首先谈谈你对Vue的理解吧？

- 关键点：渐进式框架，核心库加插件，动态创建用户界面（异步获取后台数据，展示在界面）
- 特点：MVVM模式，代码简洁，体积小，运行效率搞，使用于移动和PC端，只需要关注UI，可以引入Vue插件和第三方库进行开发
- 渐进式：可以只用我的一部分，而不是用了我这一点就必须用我的所有部分。



## 你刚刚说到了MVVM，能详细说说吗？

- Model-View-viewModel：model 数据模型，view UI视图，viewModel 为model和view的桥梁，model改变数据绑定到viewmodel并自动渲染到页面中，视图变化通知viewmModel层更新数据

## vue是如何实现响应式数据的呢？（响应式数据原理）❗

- vue2：Object.defindeProperty()  重新定义data中的所有数据，该方法中的get和set 方法可以对数据进行拦截，拦截后进行依赖收集，拦截属性的更新操作，进行通知
- 具体过程：首先Vue使用initData初始化用户传入的参数，然后使用new Observer 对数据进行观测，如果数据是一个对象类型就会调用 this.walk，内部使用defineReactive循环对象属性定义响应式的变化，核心就是使用 Object.defineProperty 重新定义数据
- vue3：通过代理的方式进行数据的拦截

🌸刚刚如果你说了对象的检测，然后又没说清楚数组的处理的话，我就会问下面这个问题

## 那vue中是如何检测数组变化的呢？

？？？

使用 defineProperty 重新定义数组的每一项，能引起数组变化的方法七种：pop，push，shift，unshift，splice，sort，reverse

1. 是用来函数劫持的方式，重写了数组方法，具体呢就是更改了数组的原型，更改成自己的，用户调数组的一些方法的时候，走的就是自己的方法，然后通知视图去更新。

2. 数组里每一项可能是对象，那么我就是会对数组的每一项进行观测，（且只有数组里的对象才能进行观测，观测过的也不会进行观测）




## 那你说说Vue的事件绑定原理吧

- 原生DOM绑定事件，创建真实DOM时调用 createElement，默认会调用` invokeCreateHooks` 。会遍历当前平台下相对的属性处理代码，其中就有` updateDOMListeners` 方法，内部会传入` add（）` 方法
- 组件绑定事件，原生事件，自定义事件；组件绑定之间是通过Vue中自定义的` $on` 方法实现的

## v-model中的实现原理及如何自定义v-model ❗

- v-model就是通过 value + input 方法的语法糖（组件），原生的 v-model，会根据标签的不同生成不同事件与属性
- 自定义：自己写 model 属性，里面放上 prop 和 event

如何实现一个v-model？

👍还行哟~知道响应式数据和数据绑定问完了，接着问问渲染呗：

## 为什么Vue采用异步渲染呢？

- Vue是组件级更新，如果不采用异步更新，每次更新数据就会进行重新渲染，影响性能，Vue会在本轮数据更新后，在异步更新视图，核心就是nextTick

🌸接着追问，要是你nextTick都能讲得很清楚的话那基本你是明白了。

## 了解nextTick吗？

异步方法，异步渲染最后一步，与JS事件循环联系紧密。主要使用了宏任务微任务（`setTimeout`、`promise`那些），定义了一个异步方法，多次调用`nextTick`会将方法存入队列，通过异步方法清空当前队列

- **当数据更新了，在dom中渲染后，自动执行该函数**

## 说说Vue的生命周期吧 ❗

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

- beforeCreate：实例初始化之后
- created：实例创建完成之后调用，实例完成：数据观测、属性和方法的运算、` watch/event` 事件回调。无` $el`
- beforeMount：在挂载之前调用，相关` render` 函数首次被调用
- mounted：新创建的`vm.$el`替换
- beforeUpdate：数据更新前调用，发生在虚拟DOM重新渲染和打补丁
- updated：发生在虚拟DOM重新渲染和打补丁
- beforeDestroy：实例销毁前调用，实例仍然可用
- destroyed：实例销毁之后调用，调用后，Vue实例指示的所有东西都会解绑，所有事件监听器和所有子实例都会被移除

**每个生命周期内部可以做什么？**

- created：实例已经创建完成，因为他是最早触发的，所以可以进行一些数据、资源的请求。
- mounted：实例已经挂载完成，可以进行一些DOM操作。
- beforeUpdate：可以在这个钩子中进一步的更改状态，不会触发重渲染。
- updated：可以执行依赖于DOM的操作，但是要避免更改状态，可能会导致更新无线循环。
- destroyed：可以执行一些优化操作，清空计时器，解除绑定事件。

**ajax放在哪个生命周期？**：一般放在` mounted` 中，保证逻辑统一性，因为生命周期是同步执行的，` ajax` 是异步执行的。单数服务端渲染` ssr` 同一放在` created` 中，因为服务端渲染不支持` mounted` 方法。 

**什么时候使用beforeDestroy？**：当前页面使用` $on` ，需要解绑事件。清楚定时器。解除事件绑定，` scroll mousemove` 。




## 父子组件生命周期调用顺序（简单）

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

- 渲染、更新和销毁顺序都是先父后子，完成是先子后父

## Vue组件通信 ❗

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

- 父子间通信:父亲提供数据通过属性` props`传给儿子；儿子通过` $on` 绑父亲的事件，再通过` $emit` 触发自己的事件（发布订阅）
- 获取数据：利用父子关系` $parent` 、` $children` ，

**获取父子组件的实例**

- 父组件提供数据，子组件注入。` provide` 、` inject` ，插件用得多

- ` ref` 获取组件实例，调用组件的属性、方法

- 跨组件通信` Event Bus`  其实基于$on与$emit

- vuex  状态管理实现通信

  

## Vuex 工作原理

vuex 是专门为 vue.js 设计的状态管理模式

- 状态自管理应用？包含以下几个部分：
  - state，驱动应用的数据源；
  - view，以声明方式将 state 映射到视图；
  - actions，响应在 view 上的用户输入导致的状态变化。

- vuex，多组件共享状态，因-单向数据流简洁性很容易被破坏：

  - 多个视图依赖于同一状态。
  - 来自不同视图的行为需要变更同一状态。

  - state：
  - mutations：
  - actions：

问虚拟` DOM` 吧，看你能不能讲清楚从真实` DOM` 到虚拟` DOM` ，再和我说说` diff`

## 如何从真实DOM到虚拟DOM

1. 将模板转换成` ast` 树，` ast` 用对象来描述真实的JS语法（将真实DOM转换成虚拟DOM）
2. 优化树
3. 将` ast` 树生成代码

## 用VNode来描述一个DOM结构

虚拟节点就是用一个对象来描述一个真实的DOM元素。首先将` template` （真实DOM）先转成` ast` ，` ast` 树通过` codegen` 生成` render` 函数，` render` 函数里的` _c` 方法将它转为虚拟dom

## diff算法

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

--- 问完上面这些如果都能很清楚的话，基本O了 ---

以下的这些简单的概念，你肯定也是没有问题的啦😉

## Computed watch 和 method

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

## v-if 和 v-show 区别

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

## v-for和v-if为什么不能连用

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

## v-html 会导致哪些问题（简单）

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

## 描述组件渲染和更新过程

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

## 组件中的data为什么是函数

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

## 为什么要使用异步组件？

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

## action 与 mutation 的区别

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

## 插槽与作用域插槽的区别

### 插槽

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

### 作用域插槽

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

## vue中相同逻辑如何抽离

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

## 谈谈对keep-alive的了解

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

## Vue性能优化

<details style="display: block;"><summary style="display: block;"><b style="font-weight: 700;">答案</b></summary></details>

