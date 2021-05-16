## 介绍

Page Object 页面对象模型，就是将脚本进行分离，把页面定位元素和行为封装成一个单独的Page类

|        | PO 模式    | 直接逻辑 |
| ------ | ---------- | -------- |
| 代码量 | 多，两三倍 | 少       |
| 复杂度 | 较复杂     | 简单明了 |
| UI变化 | 修改简单   | 修改简单 |



## 思想

对代码逻辑进行分层，不同层面做不同的事，让代码结构清晰，增强代码复用性

常见分层：

- **两层：**对象逻辑层+业务数据层。
- **三层：**对象库层+逻辑层+业务层。
- **四层：**对象库层+逻辑层+业务层+数据层。



## 案例

简单的一个登陆功能

```python
from selenium import webdriver
from time import sleep
def test_user_login():
    driver = webdriver.Chrome()
    base_url = 'https://passport.bilibili.com/login'
    username = '1825932xxx'
    password = 'zxc1xxxx'
    driver.get(base_url)
    driver.find_element_by_id('login-username').send_keys(username)
    driver.find_element_by_id('login-passwd').send_keys(password)
    driver.find_element_by_class_name('btn-login').click()
    sleep(2)

if __name__ == "__main__":
    test_user_login()
```

PO模式下的登陆

```python
from selenium import webdriver
from time import sleep
# 基础类
class BasePage(object):
    def __init__(self,driver):
        self.base_url = 'https://passport.bilibili.com/login'
        self.driver = driver
        self.timeout = 30
    def _open(self):
        url = self.base_url
        self.driver.get(url)
    def open(self):
        self._open()
    def find_element_id(self, *loc):
        return self.driver.find_element_by_id(*loc)
    def find_element_class_name(self, *loc):
        return self.driver.find_element_by_class_name(*loc)

# 登陆类
class LoginPage(BasePage):
    username_loc = 'login-username'
    password_loc = 'login-passwd'
    login_loc =('btn-login')
    def type_username(self, username):
        self.find_element_id(self.username_loc).send_keys(username)
    def type_password(self, password):
        self.find_element_id(self.password_loc).send_keys(password)
    def type_login_button(self):
        self.find_element_class_name(self.login_loc).click()

# 逻辑层
def user_login(driver, username, password):
    login_page = LoginPage(driver)
    login_page.open()
    login_page.type_username(username)
    login_page.type_password(password)
    login_page.type_login_button()
    sleep(2)

# 业务层
def test_user_login():
    driver = webdriver.Chrome()
    username = '110110'
    password = 'asdas'
    user_login(driver, username, password)

if __name__ == "__main__":
    test_user_login()
```







## 分析对比

#### 一、代码量大



#### 二、分层后易于维护嘛

元素发生改变时

1. **效率高** 

   - 普通模式下直接查找对应的元素，在代码量复杂的时候只能通过注释等方式去找
   - PO模式下的任何元素都有对应的意思，更方面查找

   > 随着代码量的越来越大，case 用例不断增大，可能就不是那么方便查找了

2. **复用性大**

   - 当某个元素多次被引用的时候，普通模式需要一个个的去修改元素
   - PO模式下只需要修改一次代码就可以了

业务流程或界面需求发送变化

1. **效率高**：PO模式只需要修改业务层面的内容，而普通模式需要一个个去查找
2. **复用性大**：逻辑越复杂收益越大

> 总结：
>
> - case 越多使用 PO 模式结构越清晰
> - 元素/逻辑/数据复用越多使用 PO 模式维护容易

|          | PO 模式 | 直接逻辑 |
| -------- | ------- | -------- |
| 代码量   | 2N+     | N        |
| 可阅读性 | 强      | 很差     |
| 维护性   | 强      | 差       |

pytest 实现

```python
from selenium import webdriver
from time import sleep
import pytest
import os
class Test_user_login:
    def setup(self):
        self.driver = webdriver.Chrome()
        self.driver.maximize_window()
        self.base_url = 'https://passport.bilibili.com/login'
    def teardown(self):
        self.driver.quit()
    def test_login1(self):
        username = '1825932xxx'
        password = 'zxcassd'
        title = self.driver.title
        self.driver.get(self.base_url)
        # assert title ,'哔哩哔哩弹幕视频网 - ( ゜- ゜)つロ 乾杯~ - bilibili'
        self.driver.find_element_by_id('login-username').send_keys(username)
        self.driver.find_element_by_id('login-passwd').send_keys(password)
        self.driver.find_element_by_class_name('btn-login').click()
        sleep(2)
        dom = self.driver.find_element_by_class_name('geetest_panel_next')
        sleep(2)
        assert dom.get_attribute('style'),'display: block;'
    def test_login2(self):
        username = 'xxxxx'
        password = 'asdasdas'
        title = self.driver.title
        self.driver.get(self.base_url)
        # assert title ,'哔哩哔哩弹幕视频网 - ( ゜- ゜)つロ 乾杯~ - bilibili'
        self.driver.find_element_by_id('login-username').send_keys(username)
        self.driver.find_element_by_id('login-passwd').send_keys(password)
        self.driver.find_element_by_class_name('btn-login').click()
        sleep(2)
        dom = self.driver.find_element_by_class_name('geetest_panel_next')
        sleep(2)
        assert dom.get_attribute('style'),'display: block;'

if __name__ == "__main__":
   pytest.main(['--alluredir=report','test_bilibili_login.py'])
   os.system('allure generate --claer report')
```

PO+pytest 下实现

```python
from selenium import webdriver
from time import sleep
import pytest
import os

# 基础类
class BasePage:
    def __init__(self, driver):
        self.base_url = 'https://passport.bilibili.com/login'
        self.driver = driver
    def open(self):
        url = self.base_url
        self.driver.get(url)
    def find_element(self, loc): # location
        if(loc[0] == 'id'):
            return self.driver.find_element_by_id(loc[1])
        elif(loc[0] == 'class'):
            return self.driver.find_element_by_class_name(loc[1])
        else:
            return 0

# 登陆定位类
class LoginPage(BasePage):
    username_loc = ('id', 'login-username')
    password_loc = ('id', 'login-passwd')
    btn_login_loc = ('class', 'btn-login')
    def type_username(self, username):
        self.find_element(self.username_loc).send_keys(username)
    def type_password(self, password):
        self.find_element(self.password_loc).send_keys(password)
    def type_btn_login(self):
        self.find_element(self.btn_login_loc).click()
# 逻辑层
def user_login(driver, username, password):
    login_page = LoginPage(driver)
    login_page.open()
    login_page.type_username(username)
    login_page.type_password(password)
    login_page.type_btn_login()
    sleep(2)

# 业务层
class Test_user_login:
    def setup(self):
        self.driver = webdriver.Chrome()
    def teardown(self):
        self.driver.close()
    def test_user_login1(self):
        username = '111111111'
        password = 'heiasdasd'
        user_login(self.driver, username, password)
    def test_user_login2(self):
        username = '222222'
        password = 'heiasdasd'
        user_login(self.driver, username, password)
    def test_user_login3(self):
        username = '3333333'
        password = 'heiasdasd'
        user_login(self.driver, username, password)

if __name__ == '__main__':
    pytest.main(['--alluredir=reportPO','test_bilibili_PO.py'])
    os.system('allure generate --claer reportPO -o allure-reportPO')
```

