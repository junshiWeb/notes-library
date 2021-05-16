#### TypeScript 基础语法

TypeScript 程序由以下几个部分组成：

- 模块
- 函数
- 变量
- 语句和表达式
- 注释

tsc 命令可以执行多个 ts 文件

tsc 常用参数

| 参数                   | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| --help                 | 显示帮助信息                                                 |
| --module               | 显示扩展模块                                                 |
| --target               | 设置 ECMA 版本                                               |
| --declaration          | 额外生成一个 .d.ts 扩展名的文件                              |
| --removeComments       | 删除文件的注释                                               |
| --out                  | 编译多个文件并将他们合并生成一个文件                         |
| --sourcemap            | 生成一个 sourcemap（.map） 文件<br />map 是一个存储源代码和编译代码位置映射的文件 |
| --watch                | 监听输出文件                                                 |
| --module nolmplicitAny | 表达式声明有含 any 类型时报错                                |

Typescript 保留关键字

| break    | as         | catch      | switch   |
| -------- | ---------- | ---------- | -------- |
| case     | if         | throw      | else     |
| var      | number     | string     | get      |
| module   | type       | instanceof | typeof   |
| public   | private    | enum       | export   |
| finally  | for        | while      | void     |
| null     | super      | this       | new      |
| in       | return     | true       | false    |
| any      | extends    | static     | let      |
| package  | implements | interface  | function |
| new      | try        | yield      | const    |
| continue | do         |            |          |

> 1. 忽略程序中出现的空格、制表符和换行符
> 2. 区分大写和小写字符
> 3. 分号可选的，建议使用
> 4. 每段代码进行注释

TypeScript 是面向对象编程

- 对象：对象是类的一个实例，有状态和行为。
- 类：类是一个模板，它描述一类对象的行为和状态
- 方法：方法是类的操作和实现步骤

> 例如：狗是一个对象，他的状态有名字和颜色，行为有吃、喝、睡



#### TypeScript 基础类型

| 数据类型   | 关键字    | 描述                                                         |
| ---------- | --------- | ------------------------------------------------------------ |
| 任意类型   | any       | any 可以赋值任意类型                                         |
| 数字类型   | number    | bunber 双精度 64 位浮点值，二、八、十、十六进制              |
| 字符串类型 | string    | string   字符串系列，`'` `"`表示字符串<br />反引号`` `来定义多行文本和内嵌表达式 |
| 布尔类型   | boolean   | boolean  表示逻辑值                                          |
| 数组类型   | 无        | 声明变量为数组                                               |
| 元组       | 无        | 元组类型用来表示已知元素数量和类型的数组                     |
| 枚举       | enum      | 定义数值集合                                                 |
| void       | void      | 用于表示没有返回值类型的方法                                 |
| null       | null      | 表示对象缺失                                                 |
| undefined  | undefined | 用于初始化变量为一个未定义的值                               |
| never      | never     | 是其他类型的子类型，表示不会出现的值                         |

- 元组：无

  ```ts
  let x: [string, number];
  x = ['Runoob', 1];    // 运行正常
  x = [1, 'Runoob'];    // 报错
  console.log(x[0]);    // 输出 Runoob
  ```

- 枚举:：enum

  ```ts
  enum Color {Red, Green, Blue};
  let c: Color = Color.Blue;
  console.log(c);    // 输出 2
  ```

  ```ts
  const getValue = () => {
    return 0
  }
  
  enum List {
    A = getValue(),
    B = 2,  // 此处必须要初始化值，不然编译不通过
    C
  }
  console.log(List.A) // 0
  console.log(List.B) // 2
  console.log(List.C) // 3
  ```

  > 如果 A 的值是被计算出来的，后一位的成员必须要初始化

- void

  ```ts
  function hello(): void {
      alert("Hello Runoob");
  }
  ```

  

> 可以使用 `|` 来支持多个数据类型



#### TypeScript 变量声明

- 变量命名规则
  - 名称可以包含数字和字母
  - 除了下划线 **_** 和美元 **$** 符号外，不能包含其他特殊字符
  - 不能以数字开头
- 声明变量的四种方式

```ts
var [变量名] : [类型] = 值;
var [变量名] : [类型];
var [变量名] = 值;
var [变量名];
```

```ts
var uname:string = 'mmz';
var uname:string;
var uname = 'mmz';
var uname;
```

#### 类型断言（Type Assertion）

可以用来手动指定一个值的类型，允许变量从一种类型更改为另一种类型

语法

```ts
<类型> 值
值 as 类型
```

只有当 S 类型是 T 类型的子集时 S 才能被成功断言，如果想成功断言需要使用 any

类型断言纯粹是一个编译时语法



#### 类型推断

第一次赋值后会进行类型推断，之后再赋值其他类型会报错

#### 变量作用域

- **全局作用域** − 全局变量定义在程序结构的外部，它可以在你代码的任何位置使用。
- **类作用域** − 这个变量也可以称为 **字段**。类变量声明在一个类里头，但在类的方法外面。 该变量可以通过类的对象来访问。类变量也可以是静态的，静态的变量可以通过类名直接访问。
- **局部作用域** − 局部变量，局部变量只能在声明它的一个代码块（如：方法）中使用。

#### TypeScript运算符

TypeScript 主要包含以下几种运算：

- 算术运算符
- 逻辑运算符
- 关系运算符
- 位运算符
- 赋值运算符
- 三元/条件运算符
- 字符串运算符 
- 类型运算符

#### 短路运算符

```js
var result = ( a<10 && a>5)  第一个返回 false 则返回 false
var result = ( a>5 || a<10)  第一个返回 true 则返回 true
```

#### 位运算符

| 运算符 | 描述                                        |
| ------ | ------------------------------------------- |
| &      | AND，长度相同的二进制，相同位为1，不相同为0 |
| \|     | OR，长度相同的二进制，有1为1                |
| ~      | 取反，将二进制全部取反，符号也取反          |
| ^      | 异或，将两个二进制对比，相同为0，不相同为1  |
| <<     | 将二进制左移                                |
| >>     | 将二进制右移                                |
| >>>    | 无符号将二进制右移                          |

#### 类运算符

typeof 是一元运算符，返回操作数的数据类型

instanceof 运算符用于判断对应是否为指定类型

