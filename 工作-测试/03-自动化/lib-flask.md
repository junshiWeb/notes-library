## Flask

Flask 是一个Python编写的Web 微框架，让我们可以使用Python语言快速实现一个网站或Web服务。本文参考自[Flask官方文档](https://dormousehole.readthedocs.io/en/latest/)，大部分代码引用自官方文档。



## 安装

安装Flask，直接使用 pip 安装即可

```
pip install flask
```



## 快速使用

```python
from flask import Flask
# 创建实例
app = Flask(__name__)

# route装饰器
@app.route('/')
def hello_word():
    return 'Hello Flask'

if __name__ == '__main__':
    app.run()
```

启动方式：

1. 直接在pycharm启动，无法进行实时监控，需要重新启动应用

2. 通过命令行方式启动

   ```shell
   # 配置运行文件
   export FLASK_APP=main.py
   # 运行 需要在文件目录下执行 flask run
   flask run
   # 启动调试模式可以进行实时监控(一般不用于生产环境)
   export FLASK_ENV=development
   ```

## 路由

现在web应用使用有意义的URL，路由用于常用于页面的跳转，用route()装饰器来绑定URL

```python
@app.route('/')
def hello_word():
    return 'Hello Flask'
@app.route('/login')
def login():
    return "请登录"
```



## 变量规则

路由中可以添加变量，进行标记，标记部分会通过关键字参数传递给函数

```python
# escape 对字符串进行编码
from markupsafe import escape
@app.route('/user/<username>')
def show_user(username):
    # 显示用户信息
    return 'User %s' % escape(username)

@app.route('/post/<int:post_id>')
def show_post(post_id):
    # 显示id，id是一个数字类型
    return 'Post %d' % post_id

@app.route('/path/<path:subpath>')
def show_path(subpath):
    # 显示path后面的子路径
    return 'subpath %s' % escape(subpath)
```

转换器类型：

| `string` | （缺省值） 接受任何不包含斜杠的文本 |
| -------- | ----------------------------------- |
| `int`    | 接受正整数                          |
| `float`  | 接受正浮点数                        |
| `path`   | 类似 `string` ，但可以包含斜杠      |
| `uuid`   | 接受 UUID 字符串                    |

唯一的URL/重定向行为

```python
# 结尾带有/ 的访问/project 会自动添加一个斜杠，进行重定向
@app.route('/project/')
def project():
    return 'the project page'
```

## URL构建

url_for() 函数用于构建指定函数的URL？

解析路径？



## HTTP 方法

使用 router() 装饰器提供的 methods 参数来处理不同的HTTP方法

request 模块可以获取请求

```python
from flask import Flask, request
app = Flask(__name__)

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        return 'post'
    else:
        return 'get'
```

## 静态文件



## 渲染模板

python 内部生成的HTML比较笨拙，Flask 自动为你配置 Jinja2 模板引擎

使用 render_template() 方法可以渲染模板，提供模板文件和参数变量即可进行渲染

```
@app.route('/index')
@app.route('/index/<name>')
def hello(name):
    return render_template('index.html', name=name)
```

