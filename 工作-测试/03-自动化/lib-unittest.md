## unittest 工作原理

unittest最核心的四部分是：TestCase，TestSuite，TestRunner，TestFixture

**TestCase：**用户自定义的测试case的基类，调用run()方法，依次调用setUp方法、执行用例的方法、tearDown方法

```python
class Demo (unittest.TestCase):
  def setUp(self):
    print ('开始前置')
  def tearDown(self):
    print ('结束前置')
  def test_add(self)：
  	print ('用例方法')
```

**TestSuite：**测试用例集合，可以通过addTest()方法手动增加Test Case，也可以通过TestLoader自动添加Test Case，TestLoader在添加用例时，会没有顺序。

```python
suite = unittest.TestSuite()
suite.addTests(unittest.TestLoader().loadTestsFromTestCase(TestMathFunc))
```

TestRunner：运行测试用例的驱动类，可以执行TestCase，也可以执行TestSuite，执行后TestCase和TestSuite会自动管理TESTResult。

TestFixture：简单来说就是做一些测试过程中需要准备的东西，比如创建临时的数据库，文件和目录等，其中setUp()和setDown()是最常用的方法

整个的流程就是首先要写好TestCase，然后由TestLoader加载TestCase到TestSuite，然后由TestTestRunner来运行TestSuite，运行的结果保存在TextTestReusult中，整个过程集成在unittest.main模块中。



## unittest 单元测试框架

**优点**

- 提供用例的组织和管理
- 提供丰富的断言方法
      assertIn(a,b)
      assertEqual(a,b)
      assertTrue(a)
      assertIs(a,b)
  ..............
- 提供丰富的日志（执行的测试用例数量，通过数有多少，失败数量有多少，环境信息）

#### 测试框架使用

**基本使用**

```python
import unittest  # 导入unitest包
class Leimu(unittest.TestCase):  # 定义一个类，继承unittest.TestCase
  def test_Add(self):   # 测试用例必须以test开头
    self.asserEqual(3,3)  # 断言方法，判断a,b是否相等
  def test_Multiply(self):
    self.asserEqual(10,0)
    
if __name__ == "__main__":  # 用来运行整个模块的主函数
  unittest.main()  # unittest 提供的方法，执行测试用例中以test开头的测试用例
```

> 注意：
>
> 1. 执行顺序是以0-9优先--->其次A-Z大写字母 ---> 最后a-z小写字母，一个个字母进行比较

**前置条件和后置条件**

- 前置：setUp()
- 后置：tearDown()
- 前置指的是：比如打开浏览器、最大化窗口、休眠等一系列动作，都可以看做是前置。
- 后置指的是：执行完测试用例，数据还原，浏览器的关闭等操作。
- 前置和后置属于非必要条件，如果在前置条件和后置条件什么都不做，用pass 表示。但是一般写自动化测试脚本必须要有前置和后置。结构清晰、组织代码正常运行

#### unittest 中的断言

- assertEqual(a,b) ----------判断a是否等于b
- assertNotEqual(a,b)    --------判断a是否不等于b
- assertIn(a,b) -------- 判断a是否在b中
- assertNotIn(a,b)    --------判断a是否不在b中
- assertTrue(x)    --------判断x是否为真
- assertFalse(x)    --------判断x是否为假
- assertIs(a,b) -------- 判断a是否是b

### 小结：

1、unittest是python自带的单元测试框架，可以用来作为我们自动化测试框架的用例组织执行框架

2、unittest流程：写好TestCase，然后由TestLoader加载TestCase到TestSuite，然后由TextTestRunner来运行TestSuite，运行的结果保存在TextTestResult中，我们通过命令行或者unittest.main()执行时，main会调用TextTestRunner中的run来执行，或者我们可以直接通过TextTestRunner来执行用例。

3、一个class继承unittest.TestCase即是一个TestCase，其中以 test 开头的方法在load时被加载为一个真正的TestCase。

4、verbosity参数可以控制执行结果的输出，0 是简单报告、1 是一般报告、2 是详细报告。

5、可以通过addTest和addTests向suite中添加case或suite，可以用TestLoader的loadTestsFrom__()方法。

6、用 setUp()、tearDown()、setUpClass()以及 tearDownClass()可以在用例执行前布置环境，以及在用例执行后清理环境

7、我们可以通过skip，skipIf，skipUnless装饰器跳过某个case，或者用TestCase.skipTest方法。

8、参数中加stream，可以将报告输出到文件：可以用TextTestRunner输出txt报告，以及可以用HTMLTestRunner输出html报告。



## 案例

整合百度/有道测试用例

```python
import unittest,time
from selenium import webdriver

class Test_baidu_serach(unittest.TestCase):
    def setUp(self):
        self.driver = webdriver.Chrome()
        self.base_url = 'https://www.baidu.com'
        self.driver.implicitly_wait(30)
        self.driver.maximize_window()

    def test_baidu(self):
        '''百度测试用例'''
        print ('百度测试用例')
        driver = self.driver
        driver.get(self.base_url)
        driver.find_element_by_css_selector('#kw').send_keys('demo')
        driver.find_element_by_css_selector('#su').click()
        time.sleep(3)
        title = driver.title
        self.assertEqual(title,u'demo_百度搜索')

    def test_youdao(self):
        '''有道测试用例'''
        print ('有道测试用例')
        driver = self.driver
        driver.get('http://www.youdao.com/')
        driver.find_element_by_name('q').click()
        driver.find_element_by_name('q').send_keys('webdriver')
        driver.find_element_by_xpath("//*[@id='form']/button").click()
        time.sleep(3)
        driver.find_element_by_xpath('html/body/div[7]/i/a[1]').click()
        text01 = driver.find_element_by_css_selector("span[class='keyword']").text
        self.assertEqual(text01,'webdriver')

    def tearDown(self):
        self.driver.quit()

if __name__ == "__main__":
    unittest.main()


```



## 数据驱动

DDT



