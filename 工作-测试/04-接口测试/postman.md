安装：直接官网下载



#### 工具功能简单介绍





#### 简单实例演示

get 请求

post 请求



#### 集合运行

接口集合的执行



#### 变量的使用

全局变量

环境变量



#### 关联

请求结果作为下个请求的参数

操作：

通过tests将获取的值，并将它设置成环境变量

```js
pm.test("设置变量", function () {
  // 获取value值，并且赋值给tokenId
  var tokenId = pm.response.json().value;
  // 设置全局变量,设置键值对
  pm.globals.set("global_name", tokenId);
  // 设置环境变量,设置键值对
  pm.collectionVariables.set("collect_name", tokenId);
});
```



#### mysql 数据库操作





#### 断言

什么是断言？

检查实际结果和预期结果是否一致的方法

```javascript
判断响应结果是否包含指定内容
response body:contains sting
pm.text('title', function() {
	pm.expect(pm.response.text().to.include('xxxx'))
})

判断响应内容是否和预期结果相等
Response body: is equal to a string
pm.text('title', function() {
	pm.response..to.have.body('xxxx')
})

判断某个字段是否正确
Response body: JSON value check
pm.text('title', function() {
    var jsonObj = pm.response.json()
	pm.expect(jsonObj.message).to.eql('注册成功')
})

判断返回数据的嵌套键值
Response body: JSON value check
js格式获取数据

判断状态码是否正确
status code:code is 200

判断接口返回数据类型
Response body: JSON value check
typeof 判断
```



#### 接口参数化

将数据放入txt/cvs 中，通过数据驱动的方式执行接口测试

**使用**

需要在body中使用？





#### 获取随机参数

```
{{$timestamp}} 获取档期你的时间戳，精确到秒，长度是10位
{{$randomInt}} 获取0-1000之间的随机整数
{{$guid}} 获取一个V4风格的GUID，如：12312asdasadasdasdasdasdsadads
```



#### 导入导出

右键export 导出

首页import 导入



#### 定时任务设置

monitor