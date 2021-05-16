[toc]

## 知识掌握程度

- 知道（了解）：只要知道它是怎么样的概念、理论就够了，不需要对它进行更多的讨论。
- 理解：不仅要知道概念，而且要知道来龙去脉。
- 掌握：不仅要知道概念，而且要知道能解决什么问题，甚至要知道在出现不同场景时，能够灵活运用。
- 应用：能够重复操作达成结果，或对某一个结论会用即可，而对这个概念本身的来龙去脉不做追究。

## 注释

- 注释是不会执行的

- 注释是对代码的解释说明,是让人看得

- 单行注释的快捷键/取消单行注释  `Ctrl /`,  可以一次选中多行,给其添加单行注释

  ```python
  # 注释
  """
  多行注释
  """
  ```

## 数据类型

1. 数字：number
   - int
   - float
   - complex
   - Boolean
2. 字符串：string
3. 列表：list  [1,2,3]
4. 元组：tuple (1,3,1,2)
5. 集合：set() {123,4}
6. 字典：dict {"id": "001"}

> 1. 可变数据类型和不可变数据类型
> 2. 常用的函数和方法
> 3. 类型转换和类型判断

## 输入输出

### 输入

```python
input('my name is:')
input('my name is %s student' %name)
```

### 输出

```python
print('str')
print(str)
print('str', str)
print('my name %s'% name)
# 格式化占位符，常见的s：字符串 d：数字
```



## 运算符[掌握]

### 算术运算符

```
+ - * / 
// 整除(求商)
% 取余数
** 指数,幂运算
() 可以改变优先级
```

### 赋值运算符

```python
= 将等号右边的结果赋值给等号左边的变量
等号左边,必须是变量,不能是具体的数字
```

### 符合赋值运算符

```python
+=  c+=a  ===> c = c + a
```

### 比较运算符

> 比较运算符的结果是 bool 类型, 即 True,或者是 False

```python 
== 判断是否相等, 相等是 True. 不相等是 False
!= 判断是否不相等, 不相等是 True, 相等 False
>
<
>=
<=
```

### 逻辑运算符

> 逻辑运算符可以连接连个表达式, 两个表达式共同的结果决定最终的结果是 True,还是 False

```python 
and  逻辑与, 连接的两个条件都必须为 True,结果为 True,  一假为假
	如果第一个条件为 False,就不会再判断第二个条件
or   逻辑或, 连接的两个条件都为 False,结果为 False,    一真为真
	如果第一个条件为 True,第二个条件就不会再判断了
not  逻辑非, 取反,原来是 True,变为 False,原来是 False,变为 True
```

## If 判断的基本格式

```
if 判断条件:
    判断条件为 True,会执行的代码
    ...
elif 判断条件:
	判断条件为 True,会执行的代码
	...
else:
	判断条件为 False
在 python 中使用缩进,代替代码的层级关系, 在 if 语句的缩进内,属于 if 语句的代码块
if 也可以嵌套的使用
```

## 循环的基本语法

```python
while 判断条件:
    判断条件成立,执行的代码
    
不在 while 的缩进内,代表和循环没有关系，循环也可以进行嵌套    

while 和 if 的区别:
    if 的代码块,条件成立,只会执行一次
    while 的代码块,只要条件成立,就会一直执行
```

## for 循环遍历

```python
for 变量 in 字符串:
    代码
for 循环也称为 for 遍历,会将字符串中的字符全部取到  
int i**2 for i in list:
    print (i)
```

> break 和 continue
>
> 1. break 和 continue 是 python 两个关键字
>
> 2. break 和 continue 只能用在循环中
> 3. break 是终止循环的执行, 即循环代码遇到 break,就不再循环了
> 	continue 是结束本次循环,继续下一次循环, 即本次循环剩下的代码不再执行,但会进行下一次循环

for else 的妙用，只会打印一次，不会打印多次

```python
for x in xx:
    if xxx:
        xx  # if 判断条件成立会执行
    else:
        xxx  # if 判断条件不成立,会执行
else:
    xxx  # for 循环代码运行结束,但是不是被 break 终止的时候会执行
```

## pass 占位符



## 字符串

带引号的就是字符串，不可变（地址不可变），python 中的字符串可以相乘

```python
# 字符串下标
print(str[3])
# 字符串切片
print(str[:])
print(str[::-1])

find() & rfind()
# find('target') 查找字符串，找到返回0，否则返回-1
# rfind('target') 从后到前查找，返回索引，否则返回-1
index() & rindex()
# index('target') 从前往后查找，返回索引
# rindex('target') 从后往前查找，返回
count('target', start_index, end_index)
# 查找字符串出现的次数，返回次数，三个参数，查找对象，开始索引，结束索引
replace()
# 替换字符串, 三个参数，原参数，新参数，替换的次数，默认全替换
split()
# 字符串分隔，两个参数，第一个按什么内容切割，第二个切割次数，默认按空白符，空格，tab键切割，替换所有，返回一个列表
join()
# 字符串拼接，只能对可迭代对象进行拼接
```

## 列表

存储多个不同类型的数据，用[] 表示

1. 支持下标和切片

2. 遍历

   ```python
   for i in list:
   	print(i)
   while i < len(list):
       print(i)
       i += 1
   ```

3. 列表数据操作

   ```python
   list.append('a')
   # 向尾部追加数据，返回None
   list.insert(0, 'insert')
   # 指定下标添加数据, 返回None
   list.extend(list2)
   # 列表合并，将迭代数据添加到逐个添加到列表末尾
   list.remove()
   # 删除指定数据
   list.pop()
   # 删除下标数据,默认删除最后一个
   del list[1]
   # 删除指定下标数据
   list.index('target')
   # 查找元素下标
   list.count('target’)
   # 统计元素出现的次数
   str in list
   # 判断元素是否存在in not in
   ```

4. 列表的排序

   ```python
   # 默认升序，reverse 为True为从降序
   list.sort(reverse = True)
   # 逆序
   list.reverse()
   list = list[::-1]
   ```

5. 嵌套列表

   ```
   list[0][1]...
   ```

   

## 元组

元组和列表非常相似，不同的地方就是元组不可修改，使用定义的方式不同

```python
tup = ()
print(type(tup))
```

## 集合

一系列不重复数据的集合，用{}表示，当为空的时候表示字典，为空时需要用set() 表示，不可修改

## 字典

字典用{}定义，由键值对组成（key-value），字典的key可以是字符串和数字类型，不可以是列表类型，value可以是任意的类型

```python
# 字典的定义和访问
dict = {"id"：001, "name": "zzm", "data": [1, 3, 4]}
dict['id']
# 嵌套访问
dict['data'][1]
# 访问不存在的key值时会报错，通过get 访问，不会报错
dict.get['id']
```

**字典数据的操作**

```python
# 添加，直接添加键值对即可
dict['add'] = '新增'
# del 删除
del dict['add']
# pop 删除，返回删除的值
dict.pop('add')
# 清空字典
dict.clear()
# 遍历字典
for key in dict:
	print(key, dict[key])
# 字典.keys()，获取key值
# 字典.values()，获取value值
# 字典.items()，获取键值对
# 将列表转换为键值对的形式, i 为一个元组的键值对
for i in enumerate(list):
    dict[i[0]] = i[1]
```

> 常用方法
>
> - `+`  支持 字符串、列表、元组进行操作， 得到一个新的容器
> - `* 整数` 复制， 支持 字符串、列表、元组进行操作， 得到一个新的容器
> - `in/not in`  判断存在或者是不存在，支持 字符串、列表、元组、字典进行操作， 注意： ==如果是字典的话，判断的是 key 值是否存在或不存在==
>
> - `max/min` 对于字典来说，比较的字典的 key值的大小

## 函数

1. 函数的定义 def

2. 函数的参数（形参，实参）

   1. 函数传参的形式：按位置传参，按关键字参数传参

      ```python
      def func(a,b,c):
      	return a,b,c
      func(1,2,3)
      func(c=3,b=2,a=1)
      ```

   2. 缺省参数（默认参数）

      ```python
      def func(a=0)
      	return a
      # 当没有传递参数的时候默认为0
      func()
      ```

   3. 不定长参数

      ```
      # 不定长参数有两种表现形式，*arg 表示接入一个不定长元组，接收所有位置实参。**arg 变为不定长字典接收关键字参数
      ```

3. 函数的返回值

4. 全局变量和局部变量的含义

5. 函数的嵌套使用

```python
def func(a, *arg, b=1, **args):
    print(arg)
    print(args)
    return a + b
func(1,3,45,b=10)
# 指定名称传参需要在最后参数的时候传递，*和**不能一起用
```

## 拆包

```
# 将多个数据组成元组得到一个变量（组包）
a = 1，2，3
print(a) #(1,2,3)
a, b = b, a
# 拆包：将容器的数据分别给到多个变量，需要保持数据的数量和个数一致
b, c, d = a
a, b = list
a, b = dict
```

## 引用

id() 可以查看数据的引用，查看内存中的地址

可变参数： list, dict, set

不可变参数：number, tuple, str,

## 递归函数

函数调用自身

## 匿名函数

使用 `lambda` 关键字定义函数就称作匿名函数，只有传入参数和返回值

```python
lambda 参数列表: 表达式
```

> 1. 无参数无返回值
> 2. 无参数有返回值
> 3. 有参数无返回值
> 4. 有参数有返回值

常见运用

1. 作为函数的参数

2. 可以对字典中的键值进行排序

   ```
   list1.sort(key = lambda x:x['name'])
   # 根据键的字符串长度，进行列表排序
   list2.sort(key = lamvda x: len(x))
   ```

   

## 列表推导式

```
# 创建一个列表
my_list = [i for i in range(5)]
# 生成有规则的列表
my_list = [i for i in range(5) if i%2 ==0]
# 生成一个元组列表，二阶列表
my_list = [(i,j) for i in range(3) for j in range(3)]
```

