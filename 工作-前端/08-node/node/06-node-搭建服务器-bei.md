## 搭建本地服务器

开启一个本地服务器需要Node.js中`http`核心模块

1. http--模块提供了搭建本地服务器的API,首先我们在项目中引入；

```
let http = require('http')
```

引入之后我们利用http.createServer()方法得到一个服务器实例。

```js
let server = http.createServer() // createServer()方法返回一个server实例，所以我们需要一个变量来接收

```

1. 经过以上两步，我们已经搭建好了一个服务器实例，然后我们给服务器实例绑定接收`request`的事情处理函数，代码如下：

```js
server.on('request', (req, res) => {
  console.log(req.url) // 获取到请求的路径（请求路径永远以“/”开头）
})

// 给服务器绑定接收请求的处理事件，当服务器接收到客户端发送的请求后，会调用后面的处理函数，处理函数接收两个参数：请求信息对象，响应信息对象。
```

1. 绑定监听端口号，开启服务器。代码如下：

```
server.listen(3000, () => {
  console.log('服务器开启成功，可以通过访问http://127.0.0.1:3000/来获取数据~~')
})

// server.listen()用来绑定监听的端口号，可以传入第二个参数，当服务器开启成功后，触发后面的回调函数

```

1. 最后看到的效果如下图所示：

![node演示](C:/Users/Administrator/Desktop/重头再来/08-node/node学习图片资源/07.png)

我们看到请求路径被打印在了CMD窗口中。

好了，经过这简单的操作是不是已经完成了一个服务器的简单搭建，接下来我们来实现一个需求：

- 当我们访问“http://127.0.0.1:3000/login”, 服务器返回 “login page”
- 当我们访问“http://127.0.0.1:3000/register”, 服务器返回 “register page”
- 当我们访问“http://127.0.0.1:3000/”, 服务器返回 “index page”
- 当我们访问“http://127.0.0.1:3000/product”, 服务器返回 **产品信息列表**

我们实现这个需求，只需要在绑定服务器监听的事件处理函数中获取到用户的请求路径，然后根据不同路径返回不同数据即可，这个也不难。详情代码看下：

```
let http = require('http')
let server = http.createServer()

server.on('request', (req, res) => {
  let url = req.url //得到请求的路径 （请求的路径永远以‘/’开头）
  if (url === '/') {
    res.end('index page')
  } else if (url === '/login') {
    res.end('login page')
  } else if (url === '/register') {
    res.end('register page')
  } else if (url === '/product'){
    let arr = [
      {
        name: 'iphone X',
        price: 8888
      },
      {
        name: 'iphone 7',
        price: 4320
      }
    ]
    // 响应的数据类型必须是字符串或者二进制数据
    res.end(JSON.stringify(arr))
  } else {
    res.end('404 NOT found')
  }
})

server.listen(3000, () => {
  console.log('服务器启动成功了，，可以访问http://127.0.0.1:3000/啦')
})
```

最后实现的效果图如下：

![node演示](C:/Users/Administrator/Desktop/重头再来/08-node/node学习图片资源/08.gif)

我们看到我们请求不同的路径，服务器给我们返回了不同的内容，并且显示在了网页中。

### 设置状态码和响应头

```
response.writeHead(200, { 'Content-Type': 'text/plain' });
```

### 设置响应头

```
response.setHeader('Content-Type', 'text/html');
```

### 写入内容

```
response.write(fileData);
```

### 结束响应

```
response.end();
```

## 静态服务器

能够根据需要请求的文件，原封不动的将服务器磁盘中的数据直接返回给到浏览器。

1. 根据设定的目录，判断用户是否请求的文件时静态文件

```
//解析路径
let urlObj = path.parse(req.url)
//判断是否请求静态文件
urlObj.dir=='/static'
```

1. 从磁盘读取静态文件并返回

```
//根据请求的后缀名，返回文件的类型
res.setHeader("content-type",getContentType(urlObj.ext))
//从服务器磁盘中读取文件，并输出到响应对象中
let rs = fs.createReadStream('./static/'+urlObj.base)
rs.pipe(res)
```

1. 如何 根据后缀名返回文件类型

```
function getContentType(extName){
    switch(extName){
        case ".jpg":
            return "image/jpeg";
        case ".html":
            return "text/html;charset=utf-8";
        case ".js":
            return "text/javascript;charset=utf-8";
        case ".json":
            return "text/json;charset=utf-8";
        case ".gif":
            return "image/gif";
        case ".css":
            return "text/css"
    }
}
```

### 完整案例

```
//引入http模块
let http = require('http');
//创建server对象
let server = http.createServer()
//引入path模块
let path = require('path')
//引入文件模块
let fs = require('fs')
//监听客户端发送过来的请求
//req请求对象包含了请求的相关的信息
//res对象用于响应内容，可以通过这个对象帮助我们快速实现HTTP响应
server.on('request',function(req,res){
    //解析路径
    let urlObj = path.parse(req.url)
    //识别请求的路径
    //console.log(urlObj)
    //进入首页，返回首页的内容
    if(req.url=="/"){
        res.setHeader("content-type","text/html;charset=utf-8")
        res.end(`<link rel="stylesheet" href="./static/style.css"><h1>首页</h1><img src='./static/cxk.jpg'>`)
    }else if(urlObj.dir=='/static'){
        res.setHeader("content-type",getContentType(urlObj.ext))
        let rs = fs.createReadStream('./static/'+urlObj.base)
        rs.pipe(res)
    }else{
        
        res.setHeader("content-type","text/html;charset=utf-8")
        res.end("<h1>404页面找不到</h1>")
    }
    
})


function getContentType(extName){
    switch(extName){
        case ".jpg":
            return "image/jpeg";
        case ".html":
            return "text/html;charset=utf-8";
        case ".js":
            return "text/javascript;charset=utf-8";
        case ".json":
            return "text/json;charset=utf-8";
        case ".gif":
            return "image/gif";
        case ".css":
            return "text/css"
    }
}



//启动服务器，监听服务端口
server.listen(80,function(){
    console.log("服务已启动：http:127.0.0.1")
})
```

##  根据数据和模板动态生成页面

1. 根据规则去解析链接，并且获取ID或者时索引值

```
//请求路径：http://127.0.0.1/movies/0
let index = req.pathObj.base;
```

1. 根据索引获取数据

```
let movies = [
         {
            name:"雪暴",
            brief:"电影《雪暴》讲述了在一座极北的边陲小镇，一伙穷凶极恶、作案手法老到的悍匪为抢夺黄金，打劫运金车，并借助大雪掩盖了所有犯罪痕迹。为了探求真相，警察王康浩暗地里搜集证据，熟悉地形，终于在一场灾难级的暴雪降临时，与谋财害命的悍匪发生了惊心动魄的正面对决……",
            author:"张震"
         },{
             name:"少年的你",
             brief:"陈念（周冬雨 饰）是一名即将参加高考的高三学生，同校女生胡晓蝶（张艺凡 饰）的跳楼自杀让她的生活陷入了困顿之中。胡晓蝶死后，陈念遭到了以魏莱（周也 饰）为首的三人组的霸凌，魏莱虽然表面上看来是乖巧的优等生，实际上却心思毒辣，胡晓蝶的死和她有着千丝万缕的联系。",
             author:"周冬雨 "
         }
     ]
let pageData = movies[index]
```

1. 根据模板渲染页面

```
res.render(movies[index],'./template/index.html')
```

1. 底层需要实现渲染函数，通过正则匹配，找到需要修改的地方进行一一的修改。

```
function render(options,path){
    fs.readFile(path,{encoding:"utf-8",flag:"r"},(err,data)=>{
        if(err){
            console.log(err)
        }else{
            console.log(data)
            let reg = /\{\{(.*?)\}\}/igs
            let result;
            while(result = reg.exec(data)){
                //去除2边的空白
                let strKey = result[1].trim()
                let strValue = options[strKey]
                data = data.replace(result[0],strValue)
            }

            this.end(data)
        }
    })
}
```

##  列表的动态渲染

### 1. 定义了列表循环的标记

```
{%for {stars} %}
<li>
<h4>姓名：{{item}}</h4>
</li>
{%endfor%}
```

### 2. 正则匹配标记

```
let reg = /\{\%for \{(.*?)\} \%\}(.*?)\{\%endfor\%\}/igs
```

匹配到2个组

1. 第一个组时匹配出变量的key值
2. 第二个组匹配出需要生成的每一项的内容

### 3. 匹配替换每一项的内容

```javascript
while(result = reg.exec(data)){
    let strKey = result[1].trim();
    //通过KEY值获取数组内容
    let strValueArr = options[strKey]
    let listStr = ""
    strValueArr.forEach((item,i)=>{
    //替换每一项内容里的变量
    	listStr = listStr + replaceVar(result[2],{"item":item})
    })
    data = data.replace(result[0],listStr)
}
```

### 4. 通过eval函数，将字符串的表达式计算出来

```
let strValue = eval('options.'+strKey);
```

# 正则路由的设定

要求：可以根据自己设定的正则匹配路径来执行相对应的函数来响应用户的内容。

### 1.设定正则的匹配路径和响应的执行函数

```
app.on('^/$',(req,res)=>{
    res.setHeader("content-type","text/html;charset=utf-8");
    res.end("<h1>这是首页</h1><img src='./abc/cxk.jpg'>")
})
```

### 2. 获取正则路径创建正则对象

```
let reg = new RegExp(regStr,'igs');
```

### 3.匹配路径，并调用相对应的函数

```
if(reg.test(req.url)){
    this.reqEvent[key](req,res)
    resState = true
    break;
}
```

### 4.判断是否正则路径响应过，如果响应过，将不再响应，不能重复响应，会报错

```javascript
if(!resState){
    if(pathObj.dir==this.staticDir){
        res.setHeader("content-type",this.getContentType(pathObj.ext))
        let rs = fs.createReadStream('./static/'+pathObj.base)
        rs.pipe(res)
    }else{
        res.setHeader("content-type","text/html;charset=utf-8")
        res.end("<h1>404!页面找不到</h1>")
    }
}
```

# 梳理框架流程

### 1浏览器发送请求

	1. 用户输入网址地址

```
http://127.0.0.1/
```

	2. 浏览器根据请求转变成HTTP的请求包

```
GET / HTTP/1.1
Host: 127.0.0.1
Connection: keep-alive
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/76.0.3809.132 Safari/537.36
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3
Sec-Fetch-Site: none
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
```

### 2服务器接受到请求

​	1. http模块里中实例化的server对象，server对象监听每一次浏览器发送过来的请求，每次的请求都会触发`request`事件

```
this.server.on('request',(req,res)=>{})
```

	2. 将HTTP的请求包转化成req的请求对象，并且传入到请求事件触发的函数中。

      	3. 会创建生成1个res响应对象，这个对象可以帮助我们快速的实现HTTP的响应

### 3解析请求路径，调用不同的页面渲染函数

	1. 正则匹配方式进行对路径的匹配

      	2. 以匹配的正则字符串作为KEY，找到需要调用执行的渲染函数

```javascript
//循环匹配正则路径
for(let key in this.reqEvent){

    let regStr = key
    let reg = new RegExp(regStr,'igs');
    console.log(regStr,reg)
    if(reg.test(req.url)){
        this.reqEvent[key](req,res)
        resState = true
        break;
    }
}
```

3. 调用页面的执行函数

```
app.on('/movies/[01]',(req,res)=>{})//这里的箭头函数即为真正匹配到的页面时执行的函数
```

4. 调用模板的渲染函数

```
res.render(movies[index],'./template/index0.html')
```

5. 执行渲染函数

```javascript
function render(options,path){
    fs.readFile(path,{encoding:"utf-8",flag:"r"},(err,data)=>{
        if(err){
            console.log(err)
        }else{
            //数组变量的替换
            data = replaceArr(data,options)
            //单个变量的替换
            data = replaceVar(data,options)
            //最终输出渲染出来的HTML
            this.end(data)
        }
    })
}
```

6. 数组变量的替换

```javascript
function replaceArr(data,options){
    //匹配循环的变量，并且替换循环的内容
    let reg = /\{\%for \{(.*?)\} \%\}(.*?)\{\%endfor\%\}/igs
    while(result = reg.exec(data)){
        let strKey = result[1].trim();//提取变量时，去掉左右两边的空格
        //通过KEY值获取数组内容
        let strValueArr = options[strKey]
        let listStr = ""
        strValueArr.forEach((item,i)=>{
            //替换每一项内容里的变量
            listStr = listStr + replaceVar(result[2],{"item":item})
        })
        data = data.replace(result[0],listStr)
    }
    return data;
}
```

7. 单个变量的替换

```javascript
function replaceVar(data,options){
    let reg = /\{\{(.*?)\}\}/igs
    let result;
    console.log(options)
    while(result = reg.exec(data)){
        //去除2边的空白
        let strKey = result[1].trim()
        
        console.log(strKey)// item,item.abc
        let strValue = eval('options.'+strKey);//执行字符串作为JS表达式，并将计算出来的结果返回
        data = data.replace(result[0],strValue)
    }
    return data
}
```



### 4如果是请求静态文件，那么就按照静态文件的形式输出

1. 首先判断是否响应过，如果没有响应过，可以判断是否为静态文件，如果是静态文件就正常的输出
2. 否则，就输出404

```javascript
if(!resState){
    if(pathObj.dir==this.staticDir){
        res.setHeader("content-type",this.getContentType(pathObj.ext))
        let rs = fs.createReadStream('./static/'+pathObj.base)
        rs.pipe(res)
    }else{
        res.setHeader("content-type","text/html;charset=utf-8")
        res.end("<h1>404!页面找不到</h1>")
    }
}
```

