#### Vue 介绍

Vue 是声明式编程，所有内容都是响应式的

**命令式编程**

命令式编程的主要思想是关注计算机执行的步骤，即**一步一步告诉计算机**先做什么再做什么

**声明式编程**

声明式编程是以数据结构的形式来表达程序执行的逻辑。它的主要思想是告诉计算机**应该做什么**，但**不指定具体要怎么做**。

**函数式编程**

函数式编程和声明式编程是有所关联的，因为他们思想是一致的：即只关注做什么而不是怎么做。

函数式编程最重要的特点是“函数第一位”，即函数可以出现在任何地方，比如你可以把**函数作为参数**传递给另一个函数，不仅如此你还可以将**函数作为返回值**

**渐进式框架**

主张更少，做的更多

#### 使用

直接引入文件

```html
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

#### 脚手架

Command-Line Interface （命令 行 接口）

**安装**

```shell
// 安装最新版
npm install -g @vue/cli
// 安装2.0
npm install -g @vue/cli-init
```

**使用**

```shell
// 最新  名字不识别大小写
vue create my-project
// 2.0
vue init webpack my-project
```

**文件名说明*

```shell
├── build              构建脚本目录
│  ├── build-server.js         运行本地构建服务器，可以访问构建后的页面
│  ├── build.js            生产环境构建脚本
│  ├── dev-client.js          开发服务器热重载脚本，主要用来实现开发阶段的页面自动刷新
│  ├── dev-server.js          运行本地开发服务器
│  ├── utils.js            构建相关工具方法
│  ├── webpack.base.conf.js      wabpack基础配置
│  ├── webpack.dev.conf.js       wabpack开发环境配置
│  └── webpack.prod.conf.js      wabpack生产环境配置
├── config             项目配置 cli3 以上不存在该目录
│  ├── dev.env.js           开发环境变量
│  ├── index.js            项目配置文件
│  ├── prod.env.js           生产环境变量
│  └── test.env.js           测试环境变量
├── src               源码目录 
│  ├── main.js             入口js文件
│  ├── app.vue             根组件
│  ├── components           公共组件目录
│  ├── assets             资源目录，这里的资源会被wabpack构建
│  ├── routes             前端路由
│  ├── store              应用级数据（state）
│  └── views              页面目录
├── static             纯静态资源，不会被wabpack构建。
└── test              测试文件目录（unit&e2e）
  └── unit              单元测试
    ├── index.js            入口脚本
    ├── karma.conf.js          karma配置文件
    └── specs              单测case目录
├── README.md            项目介绍
├── index.html           入口页面
├── package.json          npm包配置文件，里面定义了项目的依赖npm脚本，依赖包等信息
├── .babelrc babel编译参数，vue开发需要babel编译
├── .gitignore 用来过滤一些版本控制的文件，比如node_modules文件夹
```

#### **runtime-compiler和runtime-only**

创建项目时选择类型模式

**runtime-compiler**

​	template会被解析 => ast(抽象语法树) => 然后编译成render函数 => 渲染成虚拟DOM（vdom）=> 真实dom(UI)

```js
import Vue from 'vue'
import App from './App'

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  components: { App },
  template: '<App/>'
})
```

**runtime-only**

render => vdom => UI

1.性能更高，2.需要代码量更少

```js
import Vue from 'vue'
import App from './App'

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  render: h => h(App)
})
```

