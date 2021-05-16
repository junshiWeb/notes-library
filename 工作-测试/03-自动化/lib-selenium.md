## 原理

当使用Selenium 2.0启动浏览器时,后台会同时启动基于WebDriver Wire协议的Web Service 作为Selenium 的 Remote Server，并与浏览器绑定。

之后，Remote Server就开始监听Client端的操作请求;执行测试时，测试用例会作为Client端，将需要执行的页面操作请求以Http Request的方式发送给Remote Server 。该Http Request的body ,是以 WebDriver Wire协议规定的JSON格式来描述需要浏览器执行的具体操作;

Remote Server接收到请求后，会对请求进行解析，并将解析结果发给WebDriver，由WebDriver 实际执行浏览器的操作;WebDriver 可以看做是直接操作浏览器的原生组件(Native Component)，所以搭建测试环境时，通常都需要先下载浏览器对应的WebDriver。

## Selenium 环境搭建

1. 安装selenium

   ```
   pip install selenium==3.141.0  不指定版本号默认最新版
   pip show selenium  查看安装信息
   ```

2. 安装浏览器和浏览器驱动 chromedriver.exe 

   谷歌浏览器驱动下载地址：
   http://chromedriver.storage.googleapis.com/index.html

   谷歌浏览器驱动及版本对应匹配参考表：
   https://www.cnblogs.com/sophia201552/p/13476075.html

   将驱动放到 python36 安装目录下

3. 测试是否安装成功

   ```python
   from selenium import webdriver
   driver = webdriver.Chrome()
   driver.get('https://www.baidu.com')
   ```

PyCharm开发环境部署及快捷键

地址：https://www.jetbrains.com/pycharm/download/#section=windows

```
1.注释 ctrl + /
2.取消注释 在次ctrl + / 
3.运行 右键点击Run按钮 或者使用快捷键 ctrl + shift + F10 
4.创建python文件 
1.点击编辑器主项目工程文件目录->file->python file 
2.在windows下面的主项目工程文件目录里面->创建一个pyhton文件 如demo.txt ---->demo.py
5.替换    ctrl＋ｒ　　替换单个或者替换多个　replace replace all 　　
6.回退 shift+table
7.缩进 table 
8.#coding=utf-8 （中文编码的声明 允许在编辑中写入中文注释 否则报错）
```

## 2.元素定位

1. 前端知识：HTML，CSS，JavaScript

2. 八大定位元素

   ```python
   driver.find_element_by_id('id的属性值') #必须掌握
   driver.find_element_by_name('name的属性值') #必须掌握
   driver.find_element_by_class_name('class的属性值') #必须掌握
   driver.find_element_by_link_text('文本链接') #必须掌握
   driver.find_element_by_partial_link_text('部分文本链接') #了解
   driver.find_element_by_tag_name('标签名') #了解
   driver.find_element_by_xpath('很多') #超级重点
   driver.find_element_by_css_selector('很多') #超级重点
   ```

3. xpath 定位

   ```python
   定位的优缺点：
   优点： 定位语法丰富 当元素没有属性时可以通过xpah的路径定位
   缺点：1.抗变性弱 2.不稳定 3.查找速度慢（相对于CSS定位）
   a.绝对路径定位（不稳定，从根一级级往里找）
   driver.find_element_by_xpath('html/body/div[1]/div[1]/div/div[1]/div/form/span[1]/input').send_keys('demo')
   
   b.相对路径定位（层级和属性结合定位，经常用）
   driver.find_element_by_xpath("//input[@id='kw']").send_keys('demo')
   
   c.父类属性和层级关系定位(很强大，很实用)
   driver.find_element_by_xpath("//span[@class='bg s_ipt_wr quickdelete-wrap']/input").send_keys('demo')
   
   d.爷爷类属性和层级关系定位（一定能定位）
   driver.find_element_by_xpath("//form[@id='form']/span/input").send_keys('demo')
   
   e.使用逻辑运算符定位 and 
   driver.find_element_by_xpath("//input[@name='wd' and @autocomplete='off']").send_keys('demo')
   
   f.文字定位
   driver.find_element_by_xpath("//*[text()=’文字内容‘]")
   
   ```

4. CSS定位

   ```python
   CSS是层叠样式表，用于美化web页面的一种技术，我们主要使用CSS中的选择器作为我们元素定位的一种策略。
   CSS定位优缺点：
   优点：1.语法简洁 2.定位速度快 3.抗变性强
   1CSS使用id class定位百度文本框
   driver.find_element_by_css_selector("#kw").send_keys('demo')
   driver.find_element_by_css_selector(".s_ipt").send_keys('demo')
   
   2CSS使用属性定位（很常用）
   driver.find_element_by_css_selector("input[id='kw']").send_keys('demo')
   
   3CSS的父类属性和层级定位方法（和xpath区分开 用的也比较多）
   driver.find_element_by_css_selector("span#s_ipt_wr>input.s_ipt").send_keys('demo')
   
   4CSS的爷爷属性和层级定位方式
   driver.find_element_by_css_selector("form#form>span>input").send_keys('demo')
   
   ```

> 定位注意事项
>
> 定位先思考
>
> - 有id属性优先使用id定位。没有id的尽量使用css、xpath定位
> - Xpath/CSS/定位的灵活运用
> - 一个定位方式行不通，可以多尝试其他的定位方式
> - 元素的属性值如果数字、动态变化的，你应该放弃使用该属性
>
> 脚本中检查
>
> - 脚本的上下文是否引入sleep 增强脚本稳定性
> - 元素的属性值是否唯一
> - 元素的属性值是否真实可见 is_displayed()
> - 元素是否在iframe框架中？
> - 元素定位方式需要改变
> - 元素是否真正定位到是真正的元素
> - 网络环境是否良好
> - Web页面操作前后页面关联是否是否检查过？思考过？
> - 定位元素的代码是否是正常的 比如代码敲错了 或者是否引入了相关的模块 没加相关的声明 #coding=utf-8？
> - 认真检查控制台的报错信息 代码报错行数

## 3.Webdriver api 

1. 控制浏览器

   ```
   .maximize_window() 最大化浏览器窗口
   .set_window_size(a,b) a、b代表的浏览器的长宽
   .forword()    前进操作
   .back() 后退操作
   .refresh() 模拟F5刷新
   ```

2. 常用操作方法

   ```
   .click() 单击事件
   .send_keys() 向文本框输入内容
   .quit() 关闭所有浏览器窗口
   .close() 只关闭当前窗口
   .clear() 清空
   .screenshot(file)
   ```

3. 鼠标操作

   ```python
   # 引入
   from selenium.webdriver.common.action_chains import ActionChains
   ActionChains(driver).xxx
   context_click() # 右击
   double_click() # 双击
   drag_and_drop() # 拖拽
   move_to_element() # 鼠标停在一个元素上
   click_and_hold() # 按下鼠标左键在一个元素上
   ```

4. 键盘常见事件

   | 代码                          | 描述              |
   | ----------------------------- | ----------------- |
   | `send_keys(Keys.BACKSPACE)`   | 删除键(BackSpace) |
   | `send_keys(Keys.SPACE)`       | 空格键(Space)     |
   | `send_keys(Keys.TAB)`         | 制表键(Tab)       |
   | `send_keys(Keys.ESCAPE)`      | 回退键(Esc)       |
   | `send_keys(Keys.ENTER)`       | 回车键(Enter)     |
   | `send_keys(Keys.CONTROL,'a')` | 全选（Ctrl+A）    |
   | `send_keys(Keys.CONTROL,'c')` | 复制（Ctrl+C）    |

   

5. 常用接口方法

   ```
   .size  元素尺寸
   .text  元素文本
   .is_displayed()  是否可显示
   .is_enabled()  元素是否可使用
   .is_selected()  元素是否选中
   验证信息，也叫断言
   .url  由句柄提供URl
   .title  由句柄提供窗口标题
   .get_attribute(name)
   ```

6. 元素等待

   ```
   sleep(S)  由time模块提供的方法，强制等待 
   .implicityly_wait(S)  隐式等待，用轮询的方式判断元素是否出现
   显示等待，自己封装函数方法进行判断
   ```

7. 上传文件

   ```
   driver.find_element_by_name('file').send_keys("上传文件路径")
   只有input标签才能使用该方法上传
   ```

8. JS 操作滚动条

   ```
   执行JS代码 excute_script()
   excute_script('window.scrollTo(0, 2500)')
   ```

9. 窗口句柄

   ```
   获取窗口句柄
   .window_handles()
   切换窗口
   .switch_to.window(.window_handle[1])
   ```

10. 下拉框处理

   ```python
# 1.引入一个select类
from selenium.webdriver.support.select import Select
Select(demo).select_by_index(2)  # 通过索引
Select(demo).select_by_value('2')  # 通过value
Select(demo).select_by_visible_txt(u'文本描述') # 通过文件描述
# 2.链式定位
第一步：先拿到大标签，将定位的结构给一个变量demo
第二步：拿到第一步中赋值好的demo，直接操作下拉框里的选项
demo = driver.find_element_by_name('select')
demo.find_element_by_css_selector('option[value='1']').click()
   
# 3.一步到位法
driver.find_element_by_name('select').find_element_by_css_selector('option[value='1']').click()
定位下拉框.定位里面的选项
   
   ```

11. 警告框的处理

    ```
    有三种表现形式
    .alert  只有一个确认按钮
    .confirm  有确认和取消按钮
    .prompt() 有一个确认，取消和文本框
    统一定位方式
    句柄.switch_to.alert.accept() 接收弹窗
    句柄.switch_to.alert.dismiss() 拒绝弹窗
    ```

12. 多框架 iframe 处理

    平行框架和嵌套框架

    ```python
    1.iframe 标签本身有id/name 情况
    句柄.switch_to.frame('id或者name的属性值') 
    
    2.iframe 标签本身有id/name 情况
    第一步：先等位到iframe，赋值给一个demo
    第二步：定位好的框架执行 句柄.switch_to.frame(demo)
    demo=driver.find_element_by_xpath('//*[@id='ifame1']') # 定位大框架
    driver.switch_to.frome('demo')
    demo=driver.find_element_by_xpath('//*[@id='ifame2']') # 定位小框架
    driver.switch_to.frome('demo')
    
    3.针对平行框架
    句柄.switch_to.default_content()  ??
    ```



## 面向对象（封装，继承，多态）


