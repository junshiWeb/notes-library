#### 1. 创建项目

```js
express --view=ejs app

express app -e    

-e == --view=ejs
```



#### 2. express 路由

路由中的回调函数可以有多个，也可以以数组函数的形式存储

多个函数中只能有一个响应否则报错

常见响应如下：

| 方法                                                         | 描述                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [res.download()](http://www.expressjs.com.cn/en/4x/api.html#res.download) | 提示要下载的文件。                                     |
| [res.end（）](http://www.expressjs.com.cn/en/4x/api.html#res.end) | 结束响应过程。                                         |
| [res.json（）](http://www.expressjs.com.cn/en/4x/api.html#res.json) | 发送JSON响应。                                         |
| [res.jsonp（）](http://www.expressjs.com.cn/en/4x/api.html#res.jsonp) | 发送带有JSONP支持的JSON响应。                          |
| [res.redirect（）](http://www.expressjs.com.cn/en/4x/api.html#res.redirect) | 重定向请求。                                           |
| [res.render（）](http://www.expressjs.com.cn/en/4x/api.html#res.render) | 渲染视图模板。                                         |
| [res.send（）](http://www.expressjs.com.cn/en/4x/api.html#res.send) | 发送各种类型的响应。                                   |
| [res.sendFile（）](http://www.expressjs.com.cn/en/4x/api.html#res.sendFile) | 将文件作为八位字节流发送。                             |
| [res.sendStatus（）](http://www.expressjs.com.cn/en/4x/api.html#res.sendStatus) | 设置响应状态代码，并将其字符串表示形式发送为响应正文。 |

```js
app.get('/route', (req, res, next) => {
    req.method()   // 请求对象方法
    res.method()   // 响应对象方法
    next()   // 匹配下一路由或方法
},fn,fn,fn)
app.get('/route'. [fn1,fn2,fn3,....])
```

匹配路由的方式

```js
app.get('/router')  // 字符串的方式
app.get('/ab?cd')  // 连接字符串的方式
app.get('/.*\.jpg$/)  // 正则的方式
app.get('/user/:userID)  // 动态路由
```

模块化路由

```js
// --- app.js 
let express = require('express')
// 引入路由
let books = require('./books')
// 安装路由
app.use('./books/', books)

// --- books.js
const express = require("express")
var app = express.Router()
......
module.exports = app
```

中文文档： http://expressjs.jser.us/3x_zh-cn/api.html#res.download

项目文件说明

```js
bin     //  执行程序文件
node_modules     //  模块包
public     //  静态文件
    --img
    --js
    --css
routes     //  路由文件
views     // 模板文件
```

> 注意：
>
> 1. 渲染视图时默认路径为 views
>
> 2. 

#### 3. ejs 模板

通过创建 express 项目会自动创建依赖关系

只需要创建对应路由，在配置相关 ejs 文件即可

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<% for(var i=0;i<10;i++){ %>
			<%= i %>
		<% } %>
		<!-- 获取变量 -->
		<div class="datas">
			<p>获取变量：</p>
			<%- title %>
			<%= title %>
		</div>
	</body>
</html>
```

<% xxx %>：里面写入的是js语法，

<%= xxx %>：里面是服务端发送给ejs模板转义后的变量，输出为原html

<%- xxx %>：里面也是服务端发送给ejs模板后的变量，不过他会把html输出来

<%# 注释标签，不执行、不输出内容

#### 4. 请求

##### get 请求

get 都用作数据获取和查询，类似于数据库中的查询操作

当服务器解析前台资源后即传输相应内容；而查询字符串是在URL上进行的

- 表单提交请求  action 表示表单提交的位置

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<form action="http://localhost:8080/login" method="get">
			用户：
			<input type="text" name="user" id="user" placeholder="用户名"/>
			<br>
			密码：
			<input type="password" name="password" id="password" placeholder="密码"/>
			<br>
			<input type="submit" value="提交"/>
		</form>
	</body>
</html>
```

- 设置请求响应  req.query

```js
app.get('/login', (req, res) => {
  console.log('req.query')
})
```

##### post 请求

post 方法作为 http 请求很重要的一部分，几乎所有的网站都有用到它，与get不同，post 请求更像是在服务器上做修改操作，它一般用于数据资源的更新。
相比于get请求，post所请求的数据会更加安全

表单设置 POST 请求

获取 POST 请求数据需要引入中间件

```js
//解析post提交的数据
app.use(express.urlencoded())
```

请求

```js
app.post('/login', (req, res) => {
  console.log(req.body);
  let username = req.body.username
  let password = req.body.password
  let result = users.some(item => {
    return item.username == username && item.password == password
  })
  if (result) {
    res.send("登陆成功")
  } else {
    res.send("登陆失败")
  }
})
```

#### 5.中间件

中间代理操作，类似于前端请求中的拦截器

**会调用中间件的操作**

1. 浏览器发送请求
2. express 接收请求
3. 路由函数处理渲染
4. 渲染模板  res.render()

**中间件可以执行的操作**

1. 执行任务请求
2. 对请求和响应进行修改
3. 结束请求/响应循环
4. 调用堆栈中的下一个中间件函数

调用中间件的过程一定要记得调用 next() 方法，否则会中断请求

中间件的分类

##### 应用层中间件

在每次调用应用之前调用该中间件

```js
app.use((req, res, next) => {  })
```

##### 路由中间件

每次调用该路由时会调用

```js
router.use("/",(req, res, next) => { })
```

##### 错误处理中间件

一般把错误处理放在最下面，集中处理

```js
app.use((err, req, res, next) => { 
	res.sendStatus(err.httpStatusCode).json(err);
})
```

##### 内置中间件

从版本4.x开始，Express不再依赖Content，也就是说Express以前的内置中间件作为单独模块，express.static是Express的唯一内置中间件。

```
express.static(root, [options]);
```

通过express.static我们可以指定要加载的静态资源

##### 第三方中间件

形如之前我们的body-parser，采用引入外部模块的方式来获得更多的应用操作。如后期的cookie和session。

```js
var express = require('express');
var app = express();
var cookieParser = require('cookie-parser');
```


以上就是关于express中间件类型，在实际项目中，中间件都是必不可少的，因此熟悉使用各种中间件会加快项目的开发效率。

#### 6. cookie

##### 基本使用

cookie：储存在用户本地终端上的数据，关闭浏览器失效，也可自动设置失效时间

**特点**

1. cookie保存在浏览器本地，只要不过期关闭浏览器也会存在。
2. 正常情况下cookie不加密，用户可轻松看到
3. 用户可以删除或者禁用cookie
4. cookie可以被篡改
5. cookie可用于攻击
6. cookie存储量很小，大小一般是4k
7. 发送请求自动带上登录信息

**使用**

```js
// 安装
cnpm install cookie-parser --save
// 引入
const cookieParser=require("cookie-parser");
// 设置中间件
app.use(cookieParser());
// 设置 cookie  res.cookie(名称,值,{配置信息})
// maxAge: 时间 httpOnly 防止跨站脚本攻击 xss
res.cookie("name",'zhangsan',{maxAge: 900000, httpOnly: true});
// 获取cookie
res.cokie.name
```

关于设置cookie的参数说明：

1. domain: 域名  
2. name=value：键值对，可以设置要保存的 Key/Value，注意这里的 name 不能和其他属性项的名字一样 
3. Expires： 过期时间（秒），在设置的某个时间点后该 Cookie 就会失效，如 expires=Wednesday, 09-Nov-99 23:12:40 GMT。
4. maxAge： 最大失效时间（毫秒），设置在多少后失效 。
5. secure： 当 secure 值为 true 时，cookie 在 HTTP 中是无效，在 HTTPS 中才有效 。
6. Path： 表示 在那个路由下可以访问到cookie。
7. httpOnly：是微软对 COOKIE 做的扩展。如果在 COOKIE 中设置了“httpOnly”属性，则通过程序（JS 脚本、applet 等）将无法读取到COOKIE 信息，防止 XSS 攻击的产生 。
8. singed：表示是否签名cookie, 设为true 会对这个 cookie 签名，这样就需要用 res.signedCookies 而不是 res.cookies 访问它。被篡改的签名 cookie 会被服务器拒绝，并且 cookie 值会重置为它的原始值。

##### 加密 cookie

```js
const crypto = require('crypto')

module.exports = {
  MD5_SUFFIX: 's5w84&&d4d473885s2025s5*4s2',
  md5: function (str) {
    var obj = crypto.createHash('md5')
    obj.update(str)
    return obj.digest('hex')
  }
}

// 使用 引入文件
const common = require('./md5')
common.md5(str + 's5w84&&d4d473885s2025s5*4s2')
```



#### 7. session

session是另一种记录客户状态的机制，与cookie保存在客户端浏览器不同，session保存在服务器当中

**使用**

```js
// 安装
cnpm install express-session --save
// 引入
const session=require("express-session");
// 设置中间件
app.use(session({
	secret: "keyboard cat",
	 resave: false,
	 saveUninitialized: true,
	 cookie: ('name', 'value',{maxAge:  5*60*1000,secure: false})
}));
// 常用方法
// 设置session
req.session.username="张三"
// 获取session
req.session.username
// 重新设置cookie的过期时间
req.session.cookie.maxAge=1000;
// 销毁session 退出登录
req.session.destroy(function(err){
	
})
```



#### 8. 文件上传

安装

```shell
npm install multer --save
```

##### **form 上传**

html

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<form action="http://localhost:8080/" method="post" enctype="multipart/form-data">
      <!--单文件上传-->
			<input type="file" name="files" value="指定文件">
       <!--多文件上传-->
      <input type="file" name="files" value="指定文件" multiple>
			<br><br>
			<input type="submit" value="上传">
		</form>
	</body>
</html>
```

node

```js
const express=require("express");
const multer=require('multer');
//初始化上传对象
var upload=multer({dest:'./upload/',limits:{fileSize: 1024 * 1024 * 20,files: 5}});
// limits 限制文件
var fs = require('fs');
var app=express();
// 单文件上传
app.use("/",upload.single("files"),function(req,res){	//files为input type="file"的name值
	var oldFile=req.file.destination+req.file.filename;	//指定旧文件
	var newFile=req.file.destination + req.file.originalname;	//指定新文件
	fs.rename(oldFile,newFile,function(err){
    err ? res.send('上传失败！') : res.send('上传成功！')
	});
});
// 多文件上传
app.use("/",upload.array("files",5),function(req,res,next){
	req.files.forEach(function(ele,index){
    
  }
app.listen(8080);
```

##### **ajax 上传**

```js

```



#### 9. 下载

通过路由的方式下载

```html
<form action="http://localhost:8080/download" method="get" enctype="application/x-www-form-urlencoded">
	<input type="file" name="files" value="选择下载的文件"><br><br>
	<input type="submit" value="下载">
</form>
```

form 下载

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<form action="http://localhost:8080" method="POST" enctype="application/x-www-form-urlencoded">
			<input type="file" name="files" value="选择下载的文件"><br><br>
			<input type="submit" value="下载">
		</form>
	</body>
</html>
```

node

```js
const express = require("express");
const bodyParser = require("body-parser");
const path = require('path');
const { dirname } = require("path");
var app = express();

// 核心
var jsonParser = bodyParser.json();
var urlencodedParser = bodyParser.urlencoded({ extended: false });

app.post('/', urlencodedParser, function (req, res) {
  res.download("./upload/" + req.body.files, err => {
    err ? res.send("下载失败！") : res.send("下载成功！")
  });
});

app.listen(8080);
```