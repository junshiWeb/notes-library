### 前言

ndoe.js，一个基于 javsscript 运行环境的服务器语言，它的出现使得javascript有能力去实现服务器操作。基于 node.js 的 Express 则把原先的许多操作变的简单灵活，一系列强大特性帮助你创建各种 Web 应用，和丰富的 HTTP 工具。使用 Express 可以快速地搭建一个完整功能的网站。

express官方网址：[www.expressjs.com.cn](http://www.expressjs.com.cn)

### Express的安装方式

Express的安装可直接使用 npm 包管理器上的项目

安装淘宝镜像：

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

使用 cnpm 的来代替 npm，提升下载速度，其次你需要在你项目目录下运行以下指令来初始化 npm，期间所有提示按 enter 键即可，这会生成package.json，它是用于描述项目文件和依赖包。

```
cnpm init  // 初始化
cnpm install   // 安装依赖包
```

这下项目目录中又会多出一个叫node_modules文件夹，里面是node.js为我们提供的模块，当然现在没有。

安装express了，执行：

```
cnpm install express --save
```

这时，我们看到node_modules文件夹多了许多不同版本的应用文件夹，接下来执行

4.0之后的express将命令工具进行拆分需要执行才能查看版本

```
npm install -g express-generator
```

查看 express 版本号

```
express --version
```

### Express脚手架的安装

安装Express脚手架有两种方式：

#### **1、使用express-generator安装**

使用命令行进入项目目录，依次执行：

```
cnpm i express-generator
```

可通过express -h查看命令行的指令含义

```
express -h
```

 express 常见命令

```
Usage: express [options] [dir]
```

 可选项

```
Options:
    --version        输出版本号
-e, --ejs            添加对 ejs 模板引擎的支持
    --pug            添加对 pug 模板引擎的支持
    --hbs            添加对 handlebars 模板引擎的支持
-H, --hogan          添加对 hogan.js 模板引擎的支持
-v, --view <engine>  添加对视图引擎（view） <engine> 的支持 (ejs|hbs|hjs|jade|pug|twig|vash) （默认是 jade 模板引擎）
    --no-view        创建不带视图引擎的项目
-c, --css <engine>   添加样式表引擎 <engine> 的支持 (less|stylus|compass|sass) （默认是普通的 css 文件）
    --git            添加 .gitignore
-f, --force          强制在非空目录下创建
-h, --help           输出使用方法
```

创建了一个名为 app 的 Express 应用，并使用ejs模板引擎

```
express --view=ejs app
```

进入app，并安装依赖

```
cd myapp
npm install
```

**在Windows 下，使用以下命令启Express应用：**

```
set DEBUG=app:* & npm start
```

**在 MacOS 或 Linux 下，使用以下命令启Express应用：**

```
DEBUG=app:* npm start
```

 打开

```
127.0.0.1：3000  访问创建的应用
```



#### 2、使用 express 命令 来快速从创建一个项目目录

express 项目文件夹的名字 -e 如 使用命令行进入项目目录，依次执行：

```
express app -e
cd app
cnpm install
```

 

这时，你也可以看到在app文件夹下的文件结构；

```
bin: 启动目录 里面包含了一个启动文件 www 默认监听端口是 3000 (直接node www执行即可)
node_modules：依赖的模块包
public：存放静态资源
routes：路由操作
views：存放ejs模板引擎
app.js：主文件
package.json：项目描述文件
```

### 第一个Express应用“Hello World”

在这里，我们不使用npm构建的脚手架，而是向最开始那样直接在主目录中新建一个app.js文件。

在app.js中输入

```
const express = require('express');     //引入express模块
var app= express();     //express()是express模块顶级函数

app.get('/',function(req,res){      //访问根路径时输出hello world
    res.send(`<h1 style='color: blue'>hello world</h1>`);
});

app.listen(8080);       //设置访问端口号

```

命令行进入项目文件夹后，键入

```
node app.js
```

即已开启服务器，接下来只需在浏览器中运行 http://localhost:8080/ 就可以访问到服务器得到响应后的数据