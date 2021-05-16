## Node.js 连接 MySQL

介绍如何使用 Node.js 来连接 MySQL，并对数据库进行操作。

**安装驱动**

使用 [淘宝定制的 cnpm 命令](https://www.runoob.com/nodejs/nodejs-npm.html#taobaonpm)进行安装：

```
$ cnpm install mysql
```

**连接数据库**

在以下实例中根据你的实际配置修改数据库用户名、及密码及数据库名：

**test.js 文件代码：**

```javascript
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'root',
  password : '123456',
  database : 'test'
});
 
connection.connect();
 
connection.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results[0].solution);
});
```

执行以下命令输出结果为：

```
$ node test.js
The solution is: 2
```

#### **连接参数**

- host：连接的数据库地址。（默认:localhost）
- port：连接地址对应的端口。（默认:3306）
- localAddress: 源IP地址使用TCP连接。（可选）
- socketPath:当主机和端口参数被忽略的时候，可以填写一个Unix的Socket地址。
- user: mysql的连接用户名。
- password: 对应用户的密码。
- database: 所需要连接的数据库的名称。（可选）
- charset: 连接的编码形式。这就是mysql中的整理。（例如：utf8_general_ci）如果被指定，则作为默认的整理排序规则。（默认：utf8_general_ci）
- timezone:用来保存当前本地的时区。（默认：local）
- connectTimeout: 设置在连接的时候，超过多久以后未响应则返回失败。（默认：10000）
- stringifyObjects: stringify对象代替转换值。issue# 501。（默认：false）
- insecureAuth：使用旧（不安全）的连接方式去连接MySQL。（默认：false）
- typeCast: 确定列值是否需要转换为本地JavaScript类型。（默认：true）
- queryFormat:自定义查询的方式。地址：[Custom format](https://github.com/mysqljs/mysql#custom-format).
- supportBigNumbers: 如果你使用了BIGINT和DECIMAL格式的表列，那么需要开启这个参数来支持。（默认：false）只有当他们超过JavaScript所能表达的最长的字节的时候，如果没有设置这个参数，则会将过长的数字作为字符串传递。否则，返回对象的长度。如果supportBigNumbers参数被忽略，则这个参数也会被忽略。
- dateStrings:一些日期类型(TIMESTAMP, DATETIME, DATE)会以Strings的类型返回，然后转换成JavaScript的日期对象。（默认：false）
- debug:是否把连接情况打印到文件。（默认：false）
- trace: 生成错误的堆栈跟踪，包括库入口的调用位置（“长堆栈的轨迹”）。一般会造成轻微的性能损失。（默认：true）

#### 终止连接

```js
connection.end(function(err) {
  // 连接终止
});
// 和end()方法不同，destroy()方法不使用回调参数
connection.destroy();
```

#### **更换用户并且改变连接状态**

```js
connection.changeUser({user : 'john'}, function(err) {
  if (err) throw err;
});
```

- user: 新的用户名 (默认前一次使用的用户名).
- password: 新用户的密码(默认前一次使用的密码).
- charset: 新的字符集 (默认前一次使用的字符集).
- database: 新的数据库名称(默认前一次使用的数据库名).

有时有用的是这个功能的副作用,即会重置任何连接的状态

#### **执行查询**

方法一：

.query(sqlString, callback)  

第一个参数是一条SQL字符串，第二个参数是回调

```js
connection.query('SELECT * FROM `books` WHERE `author` = "David"', function (error, results, fields) {
  // error 返回错误信息，无返回 null
  // results 返回执行结果
  // fields 返回字段信息
});
```

方法二：

 .query(sqlString, values, callback) 

带有值的占位符 

```sql
connection.query('SELECT * FROM `books` WHERE `author` = ?', ['David'], function (error, results, fields) {
  // error 返回错误信息，无返回 null
  // results 返回执行结果
  // fields 返回字段信息
});
```

方法三：

 .query()形式是 .query(options, callback)

在查询时带有大量的高级可选项

比如 [转义查询值(escaping query values)](https://github.com/mysqljs/mysql#escaping-query-values)，[联结重叠列名(joins with overlapping column names)](https://github.com/mysqljs/mysql#joins-with-overlapping-column-names)，超时(timeouts), 和 [类型转换(type casting)](https://github.com/mysqljs/mysql#type-casting)

```sql
connection.query({
  sql: 'SELECT * FROM `books` WHERE `author` = ?',
  timeout: 40000, // 40s
  values: ['David']
}, function (error, results, fields) {
  // error 返回错误信息，无返回 null
  // results 返回执行结果
  // fields 返回字段信息
});
```

## 数据库操作( CURD )

在进行数据库操作前，你需要将本站提供的 Websites 表 SQL 文件[websites.sql](https://static.runoob.com/download/websites.sql) 导入到你的 MySQL 数据库中。

本教程测试的 MySQL 用户名为 root，密码为 123456，数据库为 test，你需要根据自己配置情况修改。

## 查询数据

将上面我们提供的 SQL 文件导入数据库后，执行以下代码即可查询出数据：

```javascript
var mysql  = require('mysql');  
 
var connection = mysql.createConnection({     
  host     : 'localhost',       
  user     : 'root',              
  password : '123456',       
  port: '3306',                   
  database: 'test' 
}); 
 
connection.connect();
 
var  sql = 'SELECT * FROM websites';
//查
connection.query(sql,function (err, result) {
        if(err){
          console.log('[SELECT ERROR] - ',err.message);
          return;
        }
 
       console.log('------SELECT------');
       console.log(result);
       console.log('------------------');  
});
 
connection.end();
```

执行以下命令输出就结果为：

```
$ node test.js
--------------------------SELECT----------------------------
[ RowDataPacket {
    id: 1,
    name: 'Google',
    url: 'https://www.google.cm/',
    alexa: 1,
    country: 'USA' },
  RowDataPacket {
    id: 2,
    name: '淘宝',
    url: 'https://www.taobao.com/',
    alexa: 13,
    country: 'CN' }
]
------------------------------------------------------------
```

## 插入数据

我们可以向数据表 websties 插入数据：

```javascript
var mysql  = require('mysql');  
 
var connection = mysql.createConnection({     
  host     : 'localhost',       
  user     : 'root',              
  password : '123456',       
  port: '3306',                   
  database: 'test' 
}); 
 
connection.connect();
 
var  addSql = 'INSERT INTO websites(Id,name,url,alexa,country) VALUES(0,?,?,?,?)';
var  addSqlParams = ['工具', 'https://c.sxb.com','23453', 'CN'];
//增
connection.query(addSql,addSqlParams,function (err, result) {
        if(err){
         console.log('[INSERT ERROR] - ',err.message);
         return;
        }        
 
       console.log('------INSERT------');
       //console.log('INSERT ID:',result.insertId);        
       console.log('INSERT ID:',result);        
       console.log('--------------\n\n');  
});
 
connection.end();
```

执行以下命令输出就结果为：

```
$ node test.js
--------------------------INSERT----------------------------
INSERT ID: OkPacket {
  fieldCount: 0,
  affectedRows: 1,
  insertId: 6,
  serverStatus: 2,
  warningCount: 0,
  message: '',
  protocol41: true,
  changedRows: 0 }
-----------------------------------------------------------------
```

执行成功后，查看数据表，即可以看到添加的数据

## 更新数据

我们也可以对数据库的数据进行修改：



```javascript
var mysql  = require('mysql');  
 
var connection = mysql.createConnection({     
  host     : 'localhost',       
  user     : 'root',              
  password : '123456',       
  port: '3306',                   
  database: 'test' 
}); 
 
connection.connect();
 
var modSql = 'UPDATE websites SET name = ?,url = ? WHERE Id = ?';
var modSqlParams = ['移动站', 'https://m.sxt.com',6];
//改
connection.query(modSql,modSqlParams,function (err, result) {
   if(err){
         console.log('[UPDATE ERROR] - ',err.message);
         return;
   }        
  console.log('--------UPDATE--------');
  console.log('UPDATE affectedRows',result.affectedRows);
  console.log('----------\n\n');
});
 
connection.end();
```

执行以下命令输出就结果为：

```
--------------------------UPDATE----------------------------
UPDATE affectedRows 1
-----------------------------------------------------------------
```

执行成功后，查看数据表

## 删除数据

我们可以使用以下代码来删除 id 为 6 的数据: 

**回调函数只有两个参数 err res**

```javascript
var mysql  = require('mysql');  
 
var connection = mysql.createConnection({     
  host     : 'localhost',       
  user     : 'root',              
  password : '123456',       
  port: '3306',                   
  database: 'test' 
}); 
 
connection.connect();
 
var delSql = 'DELETE FROM websites where id=6';
//删
connection.query(delSql,function (err, result) {
        if(err){
          console.log('[DELETE ERROR] - ',err.message);
          return;
        }        
 
       console.log('-----DELETE-------');
       console.log('DELETE affectedRows',result.affectedRows);
       console.log('----------------\n\n');  
});
 
connection.end();
```

执行以下命令输出就结果为：

```
--------------------------DELETE----------------------------
DELETE affectedRows 1
-----------------------------------------------------------------
```

执行成功后，查看数据表