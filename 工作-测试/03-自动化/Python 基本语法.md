## Python 简介

**Python 是一个高层次的结合了解释性、编译性、互动性和面向对象的脚本语言**

- **Python 是一种解释型语言：** 这意味着开发过程中没有了编译这个环节。类似于PHP和Perl语言。
- **Python 是交互式语言：** 这意味着，您可以在一个 Python 提示符 **>>>** 后直接执行代码。
- **Python 是面向对象语言:** 这意味着Python支持面向对象的风格或代码封装在对象的编程技术。



**发展历史**

龟叔在89年圣诞时候无聊诞生的，用C+编写的，当前不火，随着人工智能和数据分析这些的发展慢慢火热起来

**特点**

1. 易于学习
2. 易于阅读
3. 易于维护
4. 有广泛的标准库
5. 互动模式
6. 可移植
7. 可扩展
8. 可嵌入
9. 数据库
10. GUI编程？



## 初识 Python

python有2.x和3.x两个版本，两个版本不兼容，2.x版本在2020.1.1停止更新了

安装：直接下载安装包安装，安装时需要勾选自动配置环境，否则需要自己配置环境

解释器：PyChrome（最好用的）

**三种执行方式**

```
// 1.直接在 cmd 中执行python可以执行命令

// 2.命令行执行 python xx.py

// 3.忘了？

```

#### 标准和注意项

**标识符合命名**：与大多数编程语言一致，常用下划线或驼峰命名

- 第一个字符必须是字母表中字母或下划线 **_** 。
- 标识符的其他的部分由字母、数字和下划线组成。
- 标识符对大小写敏感。

**保留字**

```shell
['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

**注释：`#`** `'''` `"""`

**行与缩进：**缩进可以代替代码块不需要`{}`，所以缩进需要一致

**多行语句：**可以使用 `\` 换行

**空行：**也是程序代码的一部分，不能随意空行

**同行显示多条语句：**可以使用 `;`分隔

**输出和输入：**

```
print(""，end="")
input("\n\n按下 enter 键后退出。")
```



#### 基础数据类型

**变量**

python 中变量不需要声明，每个变量在使用前都必须要赋值，变量赋值之后才会被创建

变量赋值中可以多个变量赋值，也可使用解构的方式

##### 标准数据类型

**六种标准的数据类型**：

**数字类型（number）：**四种数字类型，整数，布尔型，浮点数和复数（1+2j，1.1+2j）

**字符串（String）：**用`'` 或 `""` 括起来的，同时使用反

**列表（List）:**`[]`大多数集合类的数据结构，`+` 号可以进行列表拼接，`*` 表示重复操作

- 列表截取字符串有三个参数，最后一个参数代表步长，-1 代表逆向截取

**元组（Tuple）：**`()`元素和列表功能类似，不过元组中的数据不可以修改

**集合（Set）：**`set{}` 创建一系列元素的合集，自动删除重复数据，

**字典（Dictionary）：**`{}` 无序的数据集合，有键值对

> - **不可变数据（3 个）：**Number（数字）、String（字符串）、Tuple（元组）；
>
>   所谓的不可变意思是赋值之后创建一个内存空间，重新赋值后将重新分配内存
>
> - **可变数据（3 个）：**List（列表）、Dictionary（字典）、Set（集合）。

**数据类型转换**

```
str()
number()
list()
tuple()
dict()
set()
```



#### 运算符

- **算术运算符**

  ```
  + - * /
  % 取余
  ** 幂次方
  // 取整除，向下
  ```

- 比较（关系）运算符

  ```
  == != > < >= <=
  ```

  

- 赋值运算符

  ```
  = += -= *= /=  %= **= //=
  ```

  

- 逻辑运算符

  ```
  and 
  or
  not
  ```

  

- 位运算符

  将数字转换为二进制

  ```
  &  按位与运算符，两位为1为1，否则0
  |  按位或运算符，1位为1为1
  ^  安位异或运算符，两位不相异为1，
  ~  全部取反
  << 左移运算符
  >> 右移运算符
  ```

  

- 成员运算符

  ```
  if( a in list)  判断a在不在list内
  if( a not in list)
  ```

  

- 身份运算符

  ```
  if( a is b)  判断两个标识符是不是引用一个对象
  if( a is not b)
  ```

  

- 运算符优先级

| 运算符                   | 描述                                                   |
| :----------------------- | :----------------------------------------------------- |
| **                       | 指数 (最高优先级)                                      |
| ~ + -                    | 按位翻转, 一元加号和减号 (最后两个的方法名为 +@ 和 -@) |
| * / % //                 | 乘，除，求余数和取整除                                 |
| + -                      | 加法减法                                               |
| >> <<                    | 右移，左移运算符                                       |
| &                        | 位 'AND'                                               |
| ^ \|                     | 位运算符                                               |
| <= < > >=                | 比较运算符                                             |
| == !=                    | 等于运算符                                             |
| = %= /= //= -= += *= **= | 赋值运算符                                             |
| is is not                | 身份运算符                                             |
| in not in                | 成员运算符                                             |
| not and or               | 逻辑运算符                                             |



#### 数字（Number）

赋值后生成数据类型，不可以在改变，可是使用del 删除数据

支持三种不同的数值类型

- **整型(Int)** - 通常被称为是整型或整数，是正或负整数，不带小数点。长整型
- **浮点型(float)** - 浮点型由整数部分与小数部分组成，科学计数法表示（2.5e2 = 2.5 x 102 = 250）
- **复数( (complex))** - 复数由实数部分和虚数部分构成，可以用a + bj,或者complex(a,b)表示， 复数的实部a和虚部b都是浮点型。

##### **数字类型转换**

- **int(x)** 将x转换为一个整数。
- **float(x)** 将x转换到一个浮点数。
- **complex(x)** 将x转换到一个复数，实数部分为 x，虚数部分为 0。
- **complex(x, y)** 将 x 和 y 转换到一个复数，实数部分为 x，虚数部分为 y。x 和 y 是数字表达式。

##### **数学函数**

| 函数                                                         | 返回值 ( 描述 )                                              |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [abs(x)](https://www.runoob.com/python3/python3-func-number-abs.html) | 返回数字的绝对值，如abs(-10) 返回 10                         |
| [ceil(x)](https://www.runoob.com/python3/python3-func-number-ceil.html) | 返回数字的上入整数，如math.ceil(4.1) 返回 5                  |
| [exp(x)](https://www.runoob.com/python3/python3-func-number-exp.html) | 返回e的x次幂(ex),如math.exp(1) 返回2.718281828459045         |
| [fabs(x)](https://www.runoob.com/python3/python3-func-number-fabs.html) | 返回数字的绝对值，如math.fabs(-10) 返回10.0                  |
| [floor(x)](https://www.runoob.com/python3/python3-func-number-floor.html) | 返回数字的下舍整数，如math.floor(4.9)返回 4                  |
| [log(x)](https://www.runoob.com/python3/python3-func-number-log.html) | 如math.log(math.e)返回1.0,math.log(100,10)返回2.0            |
| [log10(x)](https://www.runoob.com/python3/python3-func-number-log10.html) | 返回以10为基数的x的对数，如math.log10(100)返回 2.0           |
| [max(x1, x2,...)](https://www.runoob.com/python3/python3-func-number-max.html) | 返回给定参数的最大值，参数可以为序列。                       |
| [min(x1, x2,...)](https://www.runoob.com/python3/python3-func-number-min.html) | 返回给定参数的最小值，参数可以为序列。                       |
| [modf(x)](https://www.runoob.com/python3/python3-func-number-modf.html) | 返回x的整数部分与小数部分，两部分的数值符号与x相同，整数部分以浮点型表示。 |
| [pow(x, y)](https://www.runoob.com/python3/python3-func-number-pow.html) | x**y 运算后的值。                                            |
| [round(x [,n\])](https://www.runoob.com/python3/python3-func-number-round.html) | 返回浮点数 x 的四舍五入值，如给出 n 值，则代表舍入到小数点后的位数。**其实准确的说是保留值将保留到离上一位更近的一端。** |
| [sqrt(x)](https://www.runoob.com/python3/python3-func-number-sqrt.html) | 返回数字x的平方根。                                          |

**随机数: **random()  随机生成下一个实数，它在[0,1)范围内。

**三角函数**

**数字常量：** pi  e

#### 字符串

##### 访问字符串

```
str[1]
str[1:3]
str[::3]
```



##### 字符串更新

```
str = str[:3] + 'update'
```



##### 转义字符

| 转义字符      | 描述                                                         |
| :------------ | :----------------------------------------------------------- |
| `\`(在行尾时) | 续行符                                                       |
| `\\`          | 反斜杠符号                                                   |
| `\'`          | 单引号                                                       |
| `\"`          | 双引号                                                       |
| \a            | 响铃                                                         |
| \b            | 退格(Backspace)                                              |
| \000          | 空                                                           |
| \n            | 换行                                                         |
| \v            | 纵向制表符                                                   |
| \t            | 横向制表符                                                   |
| \r            | 回车，将 **\r** 后面的内容移到字符串开头，并逐一替换开头部分的字符，直至将 **\r** 后面的内容完全替换完成。 |
| \f            | 换页                                                         |
| \yyy          | 八进制数，y 代表 0~7 的字符，例如：\012 代表换行。           |
| \xyy          | 十六进制数，以 \x 开头，y 代表的字符，例如：\x0a 代表换行    |
| \other        | 其它的字符以普通格式输出                                     |

##### 字符串运算符

| 操作符 | 描述                                                         |
| :----- | :----------------------------------------------------------- |
| +      | 字符串连接                                                   |
| *      | 重复输出字符串                                               |
| []     | 通过索引获取字符串中字符                                     |
| [ : ]  | 截取字符串中的一部分，遵循**左闭右开**原则，str[0:2] 是不包含第 3 个字符的。 |
| in     | 成员运算符 - 如果字符串中包含给定的字符返回 True             |
| not in | 成员运算符 - 如果字符串中不包含给定的字符返回 True           |
| r/R    | 原始字符串 - 原始字符串：所有的字符串都是直接按照字面的意思来使用 |
| %      | 格式字符串                                                   |

##### 字符串格式化

| 符  号 | 描述                                 |
| :----- | :----------------------------------- |
| %c     | 格式化字符及其ASCII码                |
| **%s** | 格式化字符串                         |
| **%d** | 格式化整数                           |
| %u     | 格式化无符号整型                     |
| %o     | 格式化无符号八进制数                 |
| %x     | 格式化无符号十六进制数               |
| %X     | 格式化无符号十六进制数（大写）       |
| %f     | 格式化浮点数字，可指定小数点后的精度 |
| %e     | 用科学计数法格式化浮点数             |
| %E     | 作用同%e，用科学计数法格式化浮点数   |
| %g     | %f和%e的简写                         |
| %G     | %f 和 %E 的简写                      |
| %p     | 用十六进制数格式化变量的地址         |



##### 格式化辅助指令

| 符号  | 功能                                                         |
| :---- | :----------------------------------------------------------- |
| *     | 定义宽度或者小数点精度                                       |
| -     | 用做左对齐                                                   |
| +     | 在正数前面显示加号( + )                                      |
| <sp>  | 在正数前面显示空格                                           |
| #     | 在八进制数前面显示零('0')，在十六进制前面显示'0x'或者'0X'(取决于用的是'x'还是'X') |
| 0     | 显示的数字前面填充'0'而不是默认的空格                        |
| %     | '%%'输出一个单一的'%'                                        |
| (var) | 映射变量(字典参数)                                           |
| m.n.  | m 是显示的最小总宽度,n 是小数点后的位数(如果可用的话)        |

#### 列表

有序数列的集合

```
list = [1,3,4]
```

**函数**

| 函数                                                         |
| :----------------------------------------------------------- |
| [len(list)](https://www.runoob.com/python3/python3-att-list-len.html) 列表元素个数 |
| [max(list)](https://www.runoob.com/python3/python3-att-list-max.html) 返回列表元素最大值 |
| [min(list)](https://www.runoob.com/python3/python3-att-list-min.html) 返回列表元素最小值 |
| [list(seq)](https://www.runoob.com/python3/python3-att-list-list.html) 将元组转换为列表 |

**方法**

| 方法                                                         |
| :----------------------------------------------------------- |
| [list.append(obj)](https://www.runoob.com/python3/python3-att-list-append.html) 在列表末尾添加新的对象 |
| [list.count(obj)](https://www.runoob.com/python3/python3-att-list-count.html) 统计某个元素在列表中出现的次数 |
| [list.extend(seq)](https://www.runoob.com/python3/python3-att-list-extend.html) 在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表） |
| [list.index(obj)](https://www.runoob.com/python3/python3-att-list-index.html) 从列表中找出某个值第一个匹配项的索引位置 |
| [list.insert(index, obj)](https://www.runoob.com/python3/python3-att-list-insert.html) 将对象插入列表 |
| [list.pop([index=-1\])](https://www.runoob.com/python3/python3-att-list-pop.html) 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值 |
| [list.remove(obj)](https://www.runoob.com/python3/python3-att-list-remove.html) 移除列表中某个值的第一个匹配项 |
| [list.reverse()](https://www.runoob.com/python3/python3-att-list-reverse.html) 反向列表中元素 |
| [list.sort( key=None, reverse=False)](https://www.runoob.com/python3/python3-att-list-sort.html) 对原列表进行排序 |
| [list.clear()](https://www.runoob.com/python3/python3-att-list-clear.html) 清空列表 |
| [list.copy()](https://www.runoob.com/python3/python3-att-list-copy.html) |

#### 元组tuple

元组和数组非常相似，不一样的地方是元组使用`()`，并且值是不可以修改的

函数和列表一致，但是没有方法，因为不可以修改

#### 字典

一系列键值对的集合



**函数**

| 函数及描述                                                   |
| :----------------------------------------------------------- |
| len(dict) 计算字典元素个数，即键的总数。                     |
| str(dict) 输出字典，以可打印的字符串表示。                   |
| type(variable) 返回输入的变量类型，如果变量是字典就返回字典类型。 |

**方法**

| 函数及描述                                                   |
| :----------------------------------------------------------- |
| [dict.clear()](https://www.runoob.com/python3/python3-att-dictionary-clear.html) 删除字典内所有元素 |
| [dict.copy()](https://www.runoob.com/python3/python3-att-dictionary-copy.html) 返回一个字典的浅复制 |
| [dict.fromkeys()](https://www.runoob.com/python3/python3-att-dictionary-fromkeys.html) 创建一个新字典，以序列seq中元素做字典的键，val为字典所有键对应的初始值 |
| [dict.get(key, default=None)](https://www.runoob.com/python3/python3-att-dictionary-get.html) 返回指定键的值，如果键不在字典中返回 default 设置的默认值 |
| [key in dict](https://www.runoob.com/python3/python3-att-dictionary-in.html) 如果键在字典dict里返回true，否则返回false |
| [dict.items()](https://www.runoob.com/python3/python3-att-dictionary-items.html) 以列表返回可遍历的(键, 值) 元组数组 |
| [dict.keys()](https://www.runoob.com/python3/python3-att-dictionary-keys.html) 返回一个迭代器，可以使用 list() 来转换为列表 |
| [dict.setdefault(key, default=None)](https://www.runoob.com/python3/python3-att-dictionary-setdefault.html) 和get()类似, 但如果键不存在于字典中，将会添加键并将值设为default |
| [dict.update(dict2)](https://www.runoob.com/python3/python3-att-dictionary-update.html) 把字典dict2的键/值对更新到dict里 |
| [dict.values()](https://www.runoob.com/python3/python3-att-dictionary-values.html) 返回一个迭代器，可以使用 list() 来转换为列表 |
| [pop(key[,default\])](https://www.runoob.com/python3/python3-att-dictionary-pop.html) 删除字典给定键 key 所对应的值，返回值为被删除的值。key值必须给出。 否则，返回default值。 |
| [popitem()](https://www.runoob.com/python3/python3-att-dictionary-popitem.html) 随机返回并删除字典中的最后一对键和值。 |



#### 集合 

一个无序的不重复序列，用 `{}` 或 `set()` 表示，空集合只能用`set()`

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [add()](https://www.runoob.com/python3/ref-set-add.html)     | 为集合添加元素                                               |
| [clear()](https://www.runoob.com/python3/ref-set-clear.html) | 移除集合中的所有元素                                         |
| [copy()](https://www.runoob.com/python3/ref-set-copy.html)   | 拷贝一个集合                                                 |
| [difference()](https://www.runoob.com/python3/ref-set-difference.html) | 返回多个集合的差集                                           |
| [difference_update()](https://www.runoob.com/python3/ref-set-difference_update.html) | 移除集合中的元素，该元素在指定的集合也存在。                 |
| [discard()](https://www.runoob.com/python3/ref-set-discard.html) | 删除集合中指定的元素                                         |
| [intersection()](https://www.runoob.com/python3/ref-set-intersection.html) | 返回集合的交集                                               |
| [intersection_update()](https://www.runoob.com/python3/ref-set-intersection_update.html) | 返回集合的交集。                                             |
| [isdisjoint()](https://www.runoob.com/python3/ref-set-isdisjoint.html) | 判断两个集合是否包含相同的元素，如果没有返回 True，否则返回 False。 |
| [issubset()](https://www.runoob.com/python3/ref-set-issubset.html) | 判断指定集合是否为该方法参数集合的子集。                     |
| [issuperset()](https://www.runoob.com/python3/ref-set-issuperset.html) | 判断该方法的参数集合是否为指定集合的子集                     |
| [pop()](https://www.runoob.com/python3/ref-set-pop.html)     | 随机移除元素                                                 |
| [remove()](https://www.runoob.com/python3/ref-set-remove.html) | 移除指定元素                                                 |
| [symmetric_difference()](https://www.runoob.com/python3/ref-set-symmetric_difference.html) | 返回两个集合中不重复的元素集合。                             |
| [symmetric_difference_update()](https://www.runoob.com/python3/ref-set-symmetric_difference_update.html) | 移除当前集合中在另外一个指定集合相同的元素，并将另外一个指定集合中不同的元素插入到当前集合中。 |
| [union()](https://www.runoob.com/python3/ref-set-union.html) | 返回两个集合的并集                                           |
| [update()](https://www.runoob.com/python3/ref-set-update.html) | 给集合添加元素                                               |



## 语法

#### 条件判断

```python
if (true):
    print('ss')
elif (true):
    print('ss')
else :
    print('ss')
```



#### 循环语句

```python
while 判断条件(condition)：
    执行语句(statements)……
    
for i in range(5)/list/dict:
    
break # 跳出
continue # 继续
```



#### 迭代器和生成器

- iter

- next


**生成器**

- yield