## Node在一线企业中的运用

### 作为中间层

我们通常说前端和后端，前端负责用户界面，而后端负责提供数据和业务接口。现在我们在两者间加入一层，前端并不是直接去请求后端业务接口，而是请求到中间层。再由中间层去请求业务接口

整个流程可以描述为：客户端直接请求到中间层的Node服务，Node服务分析请求，看需要哪个页面，再去请求对应数据，拿到数据后和模版结合成用户看到页面，再给到客户端。

那么有的人可能会觉得，这种模式不是更麻烦了吗？其实不然，我们来看看 **中间层的优点** ：

1. 减轻客户端内存，项目用户体验好。不会像mvvm模式的项目把页面渲染和数据请求都压在客户端，而是在服务端完成。
2. SEO性好，不像mvvm模式页面由js生成，而是在服务器渲染好html 字符，有利于网页被搜索到。
3. 保持了前后端分离的优点和目的，即解放后端，后端可以继续以接口的形式写业务代码。
4. 前端可以操控的范围增多，甚至可以做服务器，数据库层面的优化，比如中间层中常常用nginx，redis来优化项目，应对高并发。

中间层模式是一种开发模式上的进步，为什么这么好的模式我从来没有听说过呢？因为这种模式成本过高，如果没有一定量级的项目没必要去采用。

### 做项目构建工具

这里说的项目构建工具，我相信大家都用过，我们的webpack，vue-cli都是输入项目构建工具。那么大家觉得这一类工具神奇好用方便的同时，有没有想过这些工具是拿什么语言写的？其实它们并不难，这些工具都是用Node来写的。

很多公司都会开发自己公司的项目构建工具，帮助公司项目做的更标准更方便，一个好的项目构建工具，会极大的加快整个公司的项目开发效率。

这一类的项目构建工具一般都要很多的文件操作，Node对于i/o流的操作，在目前的主流后端语言中数一数二。所以越来越多的公司选择用Node来做项目构建工具。

### 做一些小型网站后端

用Node做后端，可能是大多数人认为的Node作用。其实真正在企业之中，很少会让你去用Node去做后端。 所以一般来说都是做一些小型或者个人站的后端。

## Node

### Node.js 是什么

Node.js 诞生于 2009 年，由 Joyent 的员工 Ryan Dahl 开发而成。

Node.js是一个内置有chrome V8引擎的JavaScript运行环境，他可以使原本在浏览器中运行的JavaScript有能力跑后端，从而操作我们数据库，进行文件读写等

目前市面上高密集的I/O模型，比如 Web 开发，微服务，前端构建等都有做Node.js的身影。不少大型网站都是使用 Node.js 作为后台开发语言的，比如 淘宝 双十一、去哪儿网 的 PC 端核心业务等。另外我们一些前端工具譬如VSCode,webpack等也是有Node.js开发。

Node.js的包管理工具，npm已经成为世界开源包管理中最大的生态，功能强大，目前单月使用者接近1000万

### Node.js 特点

- 事件驱动
- 非阻塞IO模型（异步）
- 轻量和高效

### Node.js 安装

1. 官网下载
2. 测试安装是否成功

```js
// 打开终端，输入node
node
// 执行js代码
node Hello.js
```

​	可以直接在终端执行 JavaScript 代码

> node.js 是脱离浏览器窗口，在服务端运行的，所以没有 BOM，DOM的概念

### Node 中的工具

#### 实时监听服务 nodemon

1. 安装：

   ```js
    npm install -g nodemon
   ```

2. 使用 `nodemon` 运行项目

   ```js
   nodemon  [your app.js]
   ```

3. `nodemon`常见配置

   ```js
   // 在命令行指定应用的端口号
   nodemon ./server.js localhost 8080
   // 查看帮助，帮助里面有很多选项都是一目了然：
   nodemon -h 或者 nodemon --help
   // 运行 debug 模式：
   nodemon --debug ./server.js 80
   // 手动重启项目,Nodemon 命令运行的终端 窗口中输入 rs 两个字符
   rs 
   ```

### node 模块化

Node.js采用的是CommonJs规范，在NodeJS中，一般将代码合理拆分到不同的JS文件中，每一个文件就是一个模块，而文件路径就是模块名。 在编写每个模块时，都有require、exports、module三个预先定义好的变量可供使用。

Node.js中模块的分类：

- 核心模块（已经封装好的内置模块）；
- 自己定义的模块；
- 第三方的模块（npm下载下来的）；

语法

```js
// 引用模块
let module = require("main.js")
// 导出模块
// 指定导出
export.add = fn() {}
// 默认导出
module.exports = fn() {}
```

> 总结：
>
> 1. Node中每个模块都有一个`module`对象，`module`对象中的有一个`exports`属性为一个接口对象，我们需要把模块之间公共的方法或属性挂载在这个接口对象中，方便其他的模块使用这些公共的方法或属性。
> 2. Node中每个模块的最后，都会`return: module.exports`。
> 3. Node中每个模块都会把`module.exports`指向的对象赋值给一个变量`exports`，也就是说：`exports = module.exports`。
> 4. `module.exports = XXX`，表示当前模块导出一个单一成员，结果就是XXX。
> 5. 如果需要导出多个成员时必须使用`exports.add = XXX; exports.foo = XXX;`或者使用`module.exports.add = XXX; module.export.foo = XXX;`。

node模块查找机制

1. 优先在加载该包的模块的同级目录`node_modules`中查找第三方包，查找到该第三方包中的`package.json`文件，并且找到里面的`main`属性对应的入口模块，该入口模块即为加载的第三方模块
2. 如果在要加载的第三方包中没有找到`package.json`文件或者是`package.json`文件中没有`main`属性，则默认加载第三方包中的`index.js`文件
3. 如果在加载第三方模块的文件的同级目录没有找到`node_modules`文件夹，或者以上所有情况都没有找到，则会向上一级父级目录下查找`node_modules`文件夹，查找规则如上一致
4. 如果一直找到该模块的磁盘根路径都没有找到

### Npm常见命令

`npm`英文全称：`node package manager`，是世界上最大的软件注册表，每星期大约有 30 亿次的下载量，包含超过 600000 个 包

1. `npm -v`：查看npm版本。
2. `npm init`：初始化后会出现一个`package.json`配置文件。可以在后面加上`-y` ，快速跳过问答式界面。
3. `npm install`：会根据项目中的`package.json`文件自动下载项目所需的全部依赖。
4. `npm install 包名 --save-dev`(`npm install 包名 -D`)：安装的包只用于开发环境，不用于生产环境，会出现在`package.json`文件中的`devDependencies`属性中。
5. `npm install 包名 --save`(`npm install 包名 -S`)：安装的包需要发布到生产环境的，会出现在package.json文件中的`dependencies`属性中。
6. `npm list`：查看当前目录下已安装的node包。
7. `npm list -g`：查看全局已经安装过的node包。
8. `npm --help`：查看npm帮助命令。
9. `npm update 包名`：更新指定包。
10. `npm uninstall 包名`：卸载指定包。
11. `npm config list`：查看配置信息。
12. `npm 指定命令 --help`：查看指定命令的帮助。
13. `npm info 指定包名`：查看远程npm上指定包的所有版本信息。
14. `npm config set registry https://registry.npm.taobao.org`： 修改包下载源，此例修改为了淘宝镜像。
15. `npm root`：查看当前包的安装路径。
16. `npm root -g`：查看全局的包的安装路径。
17. `npm ls 包名`：查看本地安装的指定包及版本信息，没有显示empty。
18. `npm ls 包名 -g`：查看全局安装的指定包及版本信息，没有显示empty。