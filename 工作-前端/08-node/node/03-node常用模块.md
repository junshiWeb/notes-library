## fs 模块

fs是 node 内置的模块，无序安装，使用中需要引用

```js
let fs = require("fs")
```

### 读文件

- 语法

```
let fs = require('fs')
fs.readFile(file,(error,data) => {  }) 
// 读文件,readFile函数接受两个参数：读取文件路径，回调函数（error，data两个参数），读取文件成功：data为文件内容，error为null，读取失败：error为错误对象，data为undefined
```

  读文件中常用的方法

```js
// 读取回来的默认是二进制的内容，所以需要调用toString()方法进行转换
data.toString()
```

### 写文件

- 语法

```
// 写文件。writeFile接受三个参数：写入文件路径，写入内容，回调函数。写入成功时候：error为null，写入失败时候：error为错误对象
fs.writeFile(path, fileName, (error) => {})
```

常用的方法

```js
trim()  // 去空格
```



### 删除文件

- 语法

以下为删除文件的语法格式：

```
fs.unlink(path, callback)
```

- 参数
  参数使用说明如下：

  - **path** - 文件路径。
  - **callback** - 回调函数，没有参数。

- 实例

### 创建目录

- 语法

```
fs.mkdir(path[, options], callback)
```

- 参数

  参数使用说明如下：

  - **path** - 文件路径。
  - options 参数可以是：
    - **recursive** - 是否以递归的方式创建目录，默认为 false。
    - **mode** - 设置目录权限，默认为 0777。
  - **callback** - 回调函数，没有参数。

- 实例

### 读取目录

- 语法

```
fs.readdir(path, callback)
```

- 参数

  参数使用说明如下：

  - **path** - 文件路径。
  - **callback** - 回调函数，回调函数带有两个参数err, files，err 为错误信息，files 为 目录下的文件数组列表。

- 实例

### 删除目录

- 语法

```
fs.rmdir(path, callback)
```

- 参数
  参数使用说明如下：
  - **path** - 文件路径。
  - **callback** - 回调函数，没有参数。

- 实例



### 输入输出

```
// 引入readline模块
var readline = require('readline');
    
//创建readline接口实例
var  rl = readline.createInterface({
    input:process.stdin,
    output:process.stdout
});

// question方法
rl.question("你的名字是？",function(answer){
    console.log("我的名字是："+answer);
    // 不加close，则程序不会结束
    rl.close();
});

// close事件监听
rl.on("close", function(){
   // 结束程序
    process.exit(0);
})
```

###  文件流

Stream 是一个抽象接口，Node 中有很多对象实现了这个接口。例如，对http 服务器发起请求的request 对象就是一个 Stream，还有stdout（标准输出）。

Node.js，Stream 有四种流类型：

- **Readable** - 可读操作。
- **Writable** - 可写操作。
- **Duplex** - 可读可写操作.
- **Transform** - 操作被写入数据，然后读出结果。

所有的 Stream 对象都是 EventEmitter 的实例。常用的事件有：

- **data** - 当有数据可读时触发。
- **end** - 没有更多的数据可读时触发。
- **error** - 在接收和写入过程中发生错误时触发。
- **finish** - 所有数据已被写入到底层系统时触发。

#### 读取流

- 语法

```js
var fs = require("fs");
var data = '';
// 创建可读流
var readerStream = fs.createReadStream('input.txt');
// 设置编码为 utf8。
readerStream.setEncoding('UTF8');
// 处理流事件 --> data, end, and error
readerStream.on('data', function(chunk) {
   data += chunk;
});
readerStream.on('end',function(){
   console.log(data);
});
readerStream.on('error', function(err){
   console.log(err.stack);
});
console.log("程序执行完毕");
```



#### 写入流

语法

```js
var fs = require("fs");
var data = 'www.sxt.com';
// 创建一个可以写入的流，写入到文件 output.txt 中
var writerStream = fs.createWriteStream('output.txt');
// 使用 utf8 编码写入数据
writerStream.write(data,'UTF8');
// 标记文件末尾
writerStream.end();
// 处理流事件 --> data, end, and error
writerStream.on('finish', function() {
    console.log("写入完成。");
});
writerStream.on('error', function(err){
   console.log(err.stack);
});
console.log("程序执行完毕");
```

#### 管道流

管道提供了一个输出流到输入流的机制。通常我们用于从一个流中获取数据并将数据传递到另外一个流中。

我们把文件比作装水的桶，而水就是文件里的内容，我们用一根管子(pipe)连接两个桶使得水从一个桶流入另一个桶，这样就慢慢的实现了大文件的复制过程。

语法

```js
var fs = require("fs");
// 创建一个可读流
var readerStream = fs.createReadStream('input.txt');
// 创建一个可写流
var writerStream = fs.createWriteStream('output.txt');
// 管道读写操作
// 读取 input.txt 文件内容，并将内容写入到 output.txt 文件中
readerStream.pipe(writerStream);
console.log("程序执行完毕");
```

#### 链式流

链式是通过连接输出流到另外一个流并创建多个流操作链的机制。链式流一般用于管道操作

用管道和链式来压缩和解压文件

语法

```js
// 压缩文件
var fs = require("fs");
var zlib = require('zlib');
// 压缩 input.txt 文件为 input.txt.gz
fs.createReadStream('input.txt')
  .pipe(zlib.createGzip())
  .pipe(fs.createWriteStream('input.txt.gz'));
console.log("文件压缩完成。");
```

```js
// 解压文件
var fs = require("fs");
var zlib = require('zlib');
// 解压 input.txt.gz 文件为 input.txt
fs.createReadStream('input.txt.gz')
  .pipe(zlib.createGunzip())
  .pipe(fs.createWriteStream('input.txt'));
console.log("文件解压完成。");
```



## path 模块

### path.parse() 解析路径

`path.parse(path)` 解析路径方法会返回一个对象

返回的对象具有以下属性：

- `dir`：原路径  -- 去除当前路径
- `root` ：根目录
- `base` ：当前文件名称+后缀
- `name`：文件名称
- `ext` ：后缀名称

### path.format(pathObject)

反解析路径，与 parse() 相反，将对象解析成路径

### path.resolve([...paths])

返回当前路径的绝对路径

### path.join([...paths])

拼接路径，返回拼接后的结果

### path.dirname(path)

返回路径名

### path.extname(path)

返回文件后缀名

### path.relative(from, to)

解析 from，to 中的相对路径不同，返回 to 不同的结果

## http 模块

本地服务





**server.listen( port ，() =>{} ) 启动http服务，创建链接**

回调函数中的参数：

**request**: 请求对象

```javascript
req.url // 请求地址及问号后边参数

req.method // 请求方式

req.headers // 请求头 [object]
```

**response**：响应对象

```javascript
res.write() // 向客户端返回信息

res.end() // 结束响应，返回结果必须为string 或 buffer, 内容有中文，会有乱码，需要配置响应头+ utf-8，如下：

// 设置响应头 重写响应头，参数一为：状态码（必传参数）

res.writeHead(status, {
    'content-type': 'text/plan;charset=utf-8' // 内容类型 通常会： res.end() 在end里边直接返回数据，最后结束响应

})
```

 **实例**

```js
let http = require("http")
let server = http.createServer((request, response) => {
  
})

req.url // 请求地址及问号后边参数
req.method // 请求方式
req.headers // 请求头 [object]
res.write() // 向客户端返回信息
res.end() // 结束响应，返回结果必须为string 或 buffer, 内容有中文，会有乱码，需要配置响应头+ utf-8，如下：
// 设置响应头 重写响应头，参数一为：状态码（必传参数）
res.writeHead(status, {
    'content-type': 'text/plan;charset=utf-8' // 内容类型 通常会： res.end() 在end里边直接返回数据，最后结束响应
})
```



## url 模块

```
http://www.aspxfans.com:8080/news/index.asp?boardID=5&ID=24618&page=1#name
```

协议部分 | 域名部分 | 端口部分 | 虚拟目录部分 | 文件名部分 | 参数部分 |锚部分

http | www.aspxfans.com | 8080 | /news/ | index.asp | ?...# | #...

### `new URL(input[, base])`

- `input`：要解析的绝对或相对的 URL。如果 `input` 是相对路径，则需要 `base`。 如果 `input` 是绝对路径，则忽略 `base`。
- `base` ：如果 `input` 不是绝对路径，则为要解析的基本 URL

> new URL 不需要导入模块
>
> 打印的结果为 url 各类数据
>
> - [`url.hash`](http://nodejs.cn/api/url.html#url_url_hash) 哈希
> - [`url.host`](http://nodejs.cn/api/url.html#url_url_host) 域名+端口
> - [`url.hostname`](http://nodejs.cn/api/url.html#url_url_hostname) 域名名称
> - [`url.href `](http://nodejs.cn/api/url.html#url_url_href) 获取及设置序列化的 URL 协议 + 域名 + 虚拟目录
>   -  `href` 属性的值等同于调用 [`url.toString()`]
> - [`url.origin`](http://nodejs.cn/api/url.html#url_url_origin) 协议 + 域名
> - [`url.pathname`](http://nodejs.cn/api/url.html#url_url_pathname) 虚拟目录
> - [`url.port`](http://nodejs.cn/api/url.html#url_url_port) 端口
> - [`url.search`](http://nodejs.cn/api/url.html#url_url_search) 参数部分
> - [`url.toString()`](http://nodejs.cn/api/url.html#url_url_tostring) 方法将返回序列化的 URL
> - [`url.toJSON() `](http://nodejs.cn/api/url.html#url_url_tojson) 
>   - 在 `URL` 对象上调用 `toJSON()` 方法将返回序列化的 URL
>   - 当 `URL` 对象使用 [`JSON.stringify()`](http://nodejs.cn/s/bmLTNS) 序列化时将自动调用该方法

### url.parse()

解析 url，返回url 各类数据

### url.format(path)

解析对象，返回 url