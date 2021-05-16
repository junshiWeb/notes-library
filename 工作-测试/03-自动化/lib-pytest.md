https://www.cnblogs.com/wxcx/p/13709570.html

### 概述

pytest是一个非常成熟的全功能的Python测试框架，主要特点有以下几点：

1、简单灵活，容易上手，文档丰富；

2、支持参数化，可以细粒度地控制要测试的测试用例；

3、能够支持简单的单元测试和复杂的功能测试，还可以用来做selenium/appnium等自动化测试、接口自动化测试（pytest+requests）;

4、pytest具有很多第三方插件，并且可以自定义扩展，比较好用的如pytest-selenium（集成selenium）、pytest-html（完美html测试报告生成）、pytest-rerunfailures（失败case重复执行）、pytest-xdist（多CPU分发）等；

5、测试用例的skip和xfail处理；

6、可以很好的和CI工具结合，例如jenkins

### 使用

官方文档：https://docs.pytest.org/en/latest/contents.html

**安装**

```
pip install pytest
```

**编写规则**

编写pytest测试样例非常简单，只需要按照下面的规则：

- 测试文件以`test_`开头（以`_test`结尾也可以）
- 测试类以Test开头，并且不能带有 **init** 方法
- 测试函数以test_开头
- 执行pytest命令会自动从当前目录及子目录中寻找符合上述约束的测试函数来执行

#### **基本使用**

```python
import pytest
def test_a():
  print ('---输出 test_a')
  assert 1 # 断言成功
def test_b():
  print ('---输出 test_b')
	assert 0 # 断言失败
if __name__ == "__main__":
  pytest.main(['param','filename'])  # 调用pytest中mian函数执行测试用例，传入列表[参数，文件名]
```

**pytest.mian()  执行逻辑**

1. 直接执行，没有参数，自动查找当前目录下 `test_` 开头或 `_test` 结尾的文件
   - 运行目录及子包下的所有用例 pytest.main([``'目录名'``])
   - 运行指定模块所有用例 pytest.main([``'test_reg.py'``])
   - 运行指定模块指定类指定用例 pytest.main([``'test_reg.py::TestClass::test_method'``]) 冒号分割
2. 设置 pytest 的执行参数
   - ``m``=``xxx: 运行打标签的用例``
   - `-reruns`=``xxx，失败重新运行``
   - ``-``q: 安静模式, 不输出环境信息
   - -``v: 丰富信息模式, 输出更详细的用例执行信息``
   - ``-``s: 显示程序中的``print``/``logging输出
     ``
   - ``-``-``resultlog``=``.``/``log.txt 生成log （无效）
   - `--html`=./report.html  生成html文件（无效）
   - ``-``-``junitxml``=``.``/``log.xml 生成xml报告

#### Exit Code 含义

- Exit code 0 所有用例执行完毕，全部通过
- Exit code 1 所有用例执行完毕，存在Failed的测试用例
- Exit code 2 用户中断了测试的执行
- Exit code 3 测试执行过程发生了内部错误
- Exit code 4 pytest 命令行使用错误
- Exit code 5 未采集到可用测试用例文件



### **命令行方式执行**

```shell
pytest 文件路径/测试文件名称 # 会执行文件夹下所有的
pytest [-option]
参数：
pytest -x  # 第01次失败就停止测试
pytest --maxfail=2   # 出现2个失败就终止测试
执行指定用例	
pytest test_xx1.py::test_func1：<br> pytest test_xx2.py::test_func2
pytest 文件名::方法名 换行 文件名::方法名
执行指定方法
pytest test_xxa.py::Test_Class::test_def
pytest 文件名::类名::方法名
标记表达式执行
pytest -m slow # 执行被装饰器 @pytest.mark.slow 装饰的所有用例
执行包测试用例
pytest --pyargs pkg.testing
```



#### 多线程执行用例

安装 pytest-xdist

```
pip install -U pytest-xdist
```

运行

```
pytest test_name -n NUM  # NUM 为程序并发数
```



#### 网络波动处理

安装 pytest-rerunfailures

```
pip install -U pytest-rerunfailures
```

运行

```
pytest test_name --reruns NUM  # 失败重试次数
```

**其他命令行参数**

```
-K  # 通过匹配的方式执行用例 expression
--maxfail=num # 错误出现指定次数，结束测试
-m # 用于执行标记过的测试用例 @pytest.mark.marker
-v # 详细结果 verbose
-q # 简化控制输出（感觉差不多？）
-s # 输出打印信息
-V # 输出用例更加详细的执行信息，比如用例所在的文件及用例名称等
--junit-xml=path # 输出xml文件格式，在与jenkins做集成时使用
--result-log=path # 将最后的结果保存到本地文件中
```



### setup 和 teardown函数

- setup和teardown主要分为：模块级,类级，功能级，函数级。存在测试类内部

只要运行了一次函数，就会执行setup和teardown，表示，开始前置和结束后置

使用

```python
import pytest
class Test_A:
  def setup(self):
    print ('开始前执行')
  def teardown(self):
    print ('结束前执行')
  def test_func:
    print ('执行函数')
  .......
if __name__ == '__main__':
  pytest.main([test_up_down.py])
```



### pytest 配置文件

配置放在测试目录下，名称为 pytest.int，执行命令后使用该配置文件执行

```ini
#配置pytest命令行运行参数
   [pytest]
    addopts = -s ... # 空格分隔，可添加多个命令行参数 -所有参数均为插件包的参数配置测试搜索的路径
    testpaths = ./scripts  # 当前目录下的scripts文件夹 -可自定义
#配置测试搜索的文件名称
    python_files = test*.py
#当前目录下的scripts文件夹下，以test开头，以.py结尾的所有文件 -可自定义
配置测试搜索的测试类名
    python_classes = Test_* 
   #当前目录下的scripts文件夹下，以test开头，以.py结尾的所有文件中，以Test开头的类 -可自定义
配置测试搜索的测试函数名
    python_functions = test_*
#当前目录下的scripts文件夹下，以test开头，以.py结尾的所有文件中，以Test开头的类内，以test_开头的方法 -可自定义
```

### Pytest 常用插件

插件列表网址：https://plugincompat.herokuapp.com/

前置条件

文件路径：

```
-Test_App  test_abc.py  pytest.ini
```

pyetst.ini配置文件内容：

```
[pytest]
# 命令行参数
addopts = -s
# 搜索文件名
python_files = test_*.py
# 搜索的类名
python_classes = Test_*
#搜索的函数名
python_functions = test_*
```

#### 测试报告

pytest-HTML 是一个插件，pytest用于生成测试结果的HTML报告

安装

```
pip install pytest-html
```

运行



allure

安装

```
pip install allure2
```

执行

```
allure generate --clear report(directory)
allure generate 需要执行的目录 -o 生成目录
```

