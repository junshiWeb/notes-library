## JavaScript

### **输出**

- alert(msg)  浏览器弹出警示框   
- console.log(msg)  浏览器控制台打印输出信息    
- prompt(info)  浏览器弹出输入框，用户可以输入

### 关键字和保留字段

```
关键字：是指 JS本身已经使用了的字，不能再用它们充当变量名、方法名。

包括：break、case、catch、continue、default、delete、do、else、finally、for、function、if、in、instanceof、new、return、switch、this、throw、try、typeof、var、void、while、with 等。

保留字：实际上就是预留的“关键字”，意思是现在虽然还不是关键字，但是未来可能会成为关键字，同样不能使用它们当变量名或方法名。

包括：boolean、byte、char、class、const、debugger、double、enum、export、extends、fimal、float、goto、implements、import、int、interface、long、mative、package、private、protected、public、short、static、super、synchronized、throws、transient、volatile 等。

注意：如果将保留字用作变量名或函数名，那么除非将来的浏览器实现了该保留字，否则很可能收不到任何错误消息。当浏览器将其实现后，该单词将被看做关键字，如此将出现关键字错误。
```

- operator 运算符

### 基本数据类型和引用数据类型

- string
- number
- boolean
- null
- undefined
- bigInt
- symbol

**引用类型**

- array
- object
- date

### Math 对象

| 属性、方法名          | 功能                                         |
| --------------------- | -------------------------------------------- |
| Math.PI               | 圆周率                                       |
| Math.floor()          | 向下取整                                     |
| Math.ceil()           | 向上取整                                     |
| Math.round()          | 四舍五入版 就近取整   注意 -3.5   结果是  -3 |
| Math.abs()            | 绝对值                                       |
| Math.max()/Math.min() | 求最大和最小值                               |
| Math.random()         | 获取范围在[0,1)内的随机值                    |

### Date 对象

| 方法                                                         | 描述                                               |
| :----------------------------------------------------------- | :------------------------------------------------- |
| get和set都是方法                                             |                                                    |
| [getDate()](https://www.runoob.com/jsref/jsref-getdate.html) | 从 Date 对象返回一个月中的某一天 (1 ~ 31)。        |
| [getDay()](https://www.runoob.com/jsref/jsref-getday.html)   | 从 Date 对象返回一周中的某一天 (0 ~ 6)。           |
| [getFullYear()](https://www.runoob.com/jsref/jsref-getfullyear.html) | 从 Date 对象以四位数字返回年份。                   |
| [getHours()](https://www.runoob.com/jsref/jsref-gethours.html) | 返回 Date 对象的小时 (0 ~ 23)。                    |
| [getMilliseconds()](https://www.runoob.com/jsref/jsref-getmilliseconds.html) | 返回 Date 对象的毫秒(0 ~ 999)。                    |
| [getMinutes()](https://www.runoob.com/jsref/jsref-getminutes.html) | 返回 Date 对象的分钟 (0 ~ 59)。                    |
| [getMonth()](https://www.runoob.com/jsref/jsref-getmonth.html) | 从 Date 对象返回月份 (0 ~ 11)。                    |
| [getSeconds()](https://www.runoob.com/jsref/jsref-getseconds.html) | 返回 Date 对象的秒数 (0 ~ 59)。                    |
| [getTime()](https://www.runoob.com/jsref/jsref-gettime.html) | 返回 1970 年 1 月 1 日至今的毫秒数。               |
| [parse()](https://www.runoob.com/jsref/jsref-parse.html)     | 返回1970年1月1日午夜到指定日期（字符串）的毫秒数。 |
| toDataString()                                               | 把Date对象日期转字符串                             |
| toJSON()                                                     | JSON格式返回日期字符串  数据库存储的时间？         |
| toLocaleString()                                             | 根据本地时间格式，把Date对象转换为字符串           |
| toLocaleDateString()                                         | 日期转字符串                                       |
| toLocaleTimeString()                                         | 时间转字符串                                       |
| toString()                                                   | Date 对象转字符串                                  |
| toTimeString()                                               | Date 对象时间转字符串                              |
| valueOf()                                                    | 返回 Date 对象的原始值  时间戳                     |

### Array 对象

字面量 /  new Array()

- instanceof   运算符 检测构造函数的实例 判断是否为数组
- Array.isArray()  检测是否为数组
- Array.from()  创建数组

#### 数组的属性

- constructor 构造函数， 返回数组原型函数
- length   长度，返回数组个数
- prototype  原型，数组对象添加属性和方法

#### 数组中的方法

- push
- pop
- unshift
- shift
- sort
- reverse
- toString
- join
- concat
- copyWthin    拷贝
- slice   切
- splice  拼接
- every  每一个
- fill  填充
- filter  过滤器
- find    查找元素，回调函数，返回  undefined
- findIndex  查找元素，回调函数，返回  -1
- forEach
- includes  包含
- indexOf  查找元素，返回索引-1
- lastIndexOf  从后查找
- map  映射
- reduce   数组合并
- reduceRight  从右开始合并
- some   
- entries
- keys
- valueOf  返回原始值

### 字符串对象

属性与数组一直

'str' / new String()

**方法**

- charAt   返回指定字符的位置  0 >
- concat   合并

- indexOf    查找
- lastIndexOf  查找
- includes 包含
- repeat  重复，照着说，复制字符串
- slice  切
- startsWidth  查看字符串开头
- substr  字符串截取，通过索引+指定数目截取字符串
- subString  通过索引+索引截取字符串
- toLowerCase  小写
- toUpperCase  大写
- trim  切除，去字符空格
- valueOf  返回某个字符串对象的原始值
- toString   返回一个字符串
- split   分离，字符串转数组
- match   匹配
- replace   替换
- search  查找



### Number 对象

**属性**

- constructor
- MAX_VALUE
- MIN_VALUE
- NaN
- prototype

**方法**

- ifFinite
- toFixed  去小数点
- toPrecision   精度，格式化指定长度
- toString  转换字符串
- valueOf  返回一个Number 对象



### Error 对象

- name
- message



### RegExp 对象

- i：ignorCase忽略大小写
- m：mutiple允许多行匹配
- g：globle进行全局匹配，指匹配到目标串的结尾

**属性**

- constructor
- global   全局，判断是否g
- ignoreCase  忽略大小写，判断是否i
- multiline  多行，判断是否m修饰符
- lastIndex  下次匹配其实位置
- source  来源，返回匹配模式

**方法**

对象方法

| [exec](https://www.runoob.com/jsref/jsref-exec-regexp.html)  | 执行，检索字符串中指定的值。返回找到的值，并确定其位置。 |
| ------------------------------------------------------------ | -------------------------------------------------------- |
| [test](https://www.runoob.com/jsref/jsref-test-regexp.html)  | 检验，检索字符串中指定的值。返回 true 或 false。         |
| [toString](https://www.runoob.com/jsref/jsref-regexp-tostring.html) | 返回正则表达式的字符串。                                 |

字符串方法

| [search](https://www.runoob.com/js/jsref-search.html)   | 搜索，检索与正则表达式相匹配的值。     |
| :------------------------------------------------------ | :------------------------------------- |
| [match](https://www.runoob.com/js/jsref-match.html)     | 匹配，找到一个或多个正则表达式的匹配。 |
| [replace](https://www.runoob.com/js/jsref-replace.html) | 替换，替换与正则表达式匹配的子串。     |
| [split](https://www.runoob.com/js/jsref-split.html)     | 分离，把字符串分割为字符串数组。       |



### 全局属性

**属性**

- infinity  无限的，无穷大
- NaN  非数字
- undefined  未定义

**函数**

- decodeURI   解码URI

- encodeURI   字符串编码位URI
- escape   字符串进行编码
- unEscape   对exacpe进行解码
- eval  评估，解析字符串，当成脚本执行
- isFinite
- isNaN
- Number  把对象的值转换为数字
- parseFloat  解析字符串返回浮点数
- parseInt  解析字符串返回整数
- String  对象转换为字符串



### Object 对象

| 方法                        | 描述                                                         |
| :-------------------------- | :----------------------------------------------------------- |
| create()                    | 创建一个对象，其原型为prototype，同时可添加多个属性。        |
| assign()                    | 把一个或多个源对象的可枚举、自有属性值复制到目标对象中，返回值为目标对象。 |
| defineProperty()            | 在一个对象上定义一个新属性或修改一个现有属性，并返回该对象。 |
| defineProperties()          | 在一个对象上定义一个或多个新属性或修改现有属性，并返回该对象。 |
| getOwnPropertyDescriptor()  | 获取目标对象上某自有属性的配置特性（属性描述符），返回值为配置对象。 |
| getOwnPropertyDescriptors() | 获取目标对象的所有自身属性的描述符，如果没有任何自身属性，则返回空对象。 |
| getOwnPropertyNames()       | 获取目标对象上的全部自有属性名（包括不可枚举属性）组成的数组。 |
| getOwnPropertySymbols()     | 返回目标对象自身的所有 Symbol 属性的数组。                   |
| getPrototypeOf()            | 获取指定对象的原型，即目标对象的prototype属性的值。          |
| setPrototypeOf()            | 设置目标对象的原型为另一个对象或null，返回该目标对象。       |
| seal()                      | 密封对象，阻止其修改现有属性的配置特性，即将对象的所有属性的configurable特性设置为false（也就是全部属性都无法重新配置，唯独可以把writable的值由true改为false，即冻结属性），并阻止添加新属性，返回该对象。 |
| freeze()                    | 完全冻结对象，在seal的基础上，属性值也不可以修改，即每个属性的wirtable也被设为false。 |
| preventExtensions()         | 使某一对象不可扩展，也就是不能为其添加新属性。               |
| is()                        | 判断两个值是否是相同的值                                     |
| isSealed()                  | 用于判断目标对象是否被密封，返回布尔值。                     |
| isFrozen()                  | 用于判断目标对象是否被冻结，返回布尔值。                     |
| isExtensible()              | 用于判断一个对象是否可扩展，即是否可以添加新属性。           |
| keys()                      | 获取目标对象上所有可枚举属性组成的数组。                     |
| entries()                   | 返回目标对象可枚举属性的键值对的数组。                       |
| fromEntries()               | 把目标键值对列表转换为一个对象。                             |
| values(obj)                 | 返回目标对象自身的所有可枚举属性值的数组，值的顺序与使用for...in循环的顺序相同 ( 区别在于 for-in 循环枚举原型链中的属性 )。 |

### web API

#### 元素操作

```js
语法：document.getElementById(id)
作用：根据ID获取元素对象
参数：id值，区分大小写的字符串
返回值：元素对象 或 null

语法：document.getElementsByTagName('标签名') 或者 element.getElementsByTagName('标签名') 
作用：根据标签名获取元素对象
参数：标签名
返回值：元素对象集合（伪数组，数组元素是元素对象）

document.getElementByClassName('类名')  // 返回对象集合
document.querySelector('选择器')   // 根据选择器返回第一个元素对象
document.querySelectorAll('选择器')  // 根据指定选择器返回
document.body  // 返回body元素对象
document.documentElement  // 返回html元素对象

element.innerText	// 获取html内容，去空格
element.innerHtml	// 获取html所有内容

// 元素属性操作
ele.src
ele.href
ele.id/alt/title
ele.type/value/checked/selected/disabled

// 样式
ele.style/className  //	样式/类名  style.width/background
// 自定义属性
ele.getAttribute('属性')
ele.setAttribute('属性', '值')
ele.moveAttribute('属性')
// 获取自定义属性
ele.datase.index  ele.datase['index']


```

#### 鼠标事件

```js
onclick   // 鼠标单击
onmouseover   // 鼠标经过
onmouseout   // 鼠标离开
onfocus  // 触发焦点
onblur	//	失去焦点
onmousemove	// 鼠标移动
onmouseup	// 鼠标按下
onmousedown	// 鼠标弹起
onmouseenter	// 鼠标经过不会触发冒泡
onmouseleave	// 鼠标离开不会触发冒泡
```





### window 对象

#### Location 对象

**属性**

| 属性                                                         | 描述                          |
| :----------------------------------------------------------- | :---------------------------- |
| [hash](https://www.runoob.com/jsref/prop-loc-hash.html)      | 返回一个URL的锚部分           |
| [host](https://www.runoob.com/jsref/prop-loc-host.html)      | 返回一个URL的主机名和端口     |
| [hostname](https://www.runoob.com/jsref/prop-loc-hostname.html) | 返回URL的主机名               |
| [href](https://www.runoob.com/jsref/prop-loc-href.html)      | 返回完整的URL                 |
| [pathname](https://www.runoob.com/jsref/prop-loc-pathname.html) | 返回的URL路径名。             |
| [port](https://www.runoob.com/jsref/prop-loc-port.html)      | 返回一个URL服务器使用的端口号 |
| [protocol](https://www.runoob.com/jsref/prop-loc-protocol.html) | 返回一个URL协议               |
| [search](https://www.runoob.com/jsref/prop-loc-search.html)  | 返回一个URL的查询部分         |

**方法**

| [assign()](https://www.runoob.com/jsref/met-loc-assign.html) | 载入一个新的文档       |
| ------------------------------------------------------------ | ---------------------- |
| [reload()](https://www.runoob.com/jsref/met-loc-reload.html) | 重新载入当前文档       |
| [replace()](https://www.runoob.com/jsref/met-loc-replace.html) | 用新的文档替换当前文档 |

#### History 对象

属性： length  返回历史网页数

**方法**

| 方法                                                         | 说明                              |
| :----------------------------------------------------------- | :-------------------------------- |
| [back()](https://www.runoob.com/jsref/met-his-back.html)     | 加载 history 列表中的前一个 URL   |
| [forward()](https://www.runoob.com/jsref/met-his-forward.html) | 加载 history 列表中的下一个 URL   |
| [go()](https://www.runoob.com/jsref/met-his-go.html)         | 加载 history 列表中的某个具体页面 |

#### window 对象

**属性**

| 属性                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [closed](https://www.runoob.com/jsref/prop-win-closed.html)  | 返回窗口是否已被关闭。                                       |
| [defaultStatus](https://www.runoob.com/jsref/prop-win-defaultstatus.html) | 设置或返回窗口状态栏中的默认文本。                           |
| [document](https://www.runoob.com/jsref/dom-obj-document.html) | 对 Document 对象的只读引用。(请参阅[对象](https://www.runoob.com/jsref/dom-obj-document.html)) |
| [frames](https://www.runoob.com/jsref/prop-win-frames.html)  | 返回窗口中所有命名的框架。该集合是 Window 对象的数组，每个 Window 对象在窗口中含有一个框架。 |
| [history](https://www.runoob.com/jsref/obj-history.html)     | 对 History 对象的只读引用。请参数 [History 对象](https://www.runoob.com/jsref/obj-history.html)。 |
| [innerHeight](https://www.runoob.com/jsref/prop-win-innerheight.html) | 返回窗口的文档显示区的高度。                                 |
| [innerWidth](https://www.runoob.com/jsref/prop-win-innerheight.html) | 返回窗口的文档显示区的宽度。                                 |
| [localStorage](https://www.runoob.com/jsref/prop-win-localstorage.html) | 在浏览器中存储 key/value 对。没有过期时间。                  |
| [length](https://www.runoob.com/jsref/prop-win-length.html)  | 设置或返回窗口中的框架数量。                                 |
| [location](https://www.runoob.com/jsref/obj-location.html)   | 用于窗口或框架的 Location 对象。请参阅 [Location 对象](https://www.runoob.com/jsref/obj-location.html)。 |
| [name](https://www.runoob.com/jsref/prop-win-name.html)      | 设置或返回窗口的名称。                                       |
| [navigator](https://www.runoob.com/jsref/obj-navigator.html) | 对 Navigator 对象的只读引用。请参数 [Navigator 对象](https://www.runoob.com/jsref/obj-navigator.html)。 |
| [opener](https://www.runoob.com/jsref/prop-win-opener.html)  | 返回对创建此窗口的窗口的引用。                               |
| [outerHeight](https://www.runoob.com/jsref/prop-win-outerheight.html) | 返回窗口的外部高度，包含工具条与滚动条。                     |
| [outerWidth](https://www.runoob.com/jsref/prop-win-outerheight.html) | 返回窗口的外部宽度，包含工具条与滚动条。                     |
| [pageXOffset](https://www.runoob.com/jsref/prop-win-pagexoffset.html) | 设置或返回当前页面相对于窗口显示区左上角的 X 位置。          |
| [pageYOffset](https://www.runoob.com/jsref/prop-win-pagexoffset.html) | 设置或返回当前页面相对于窗口显示区左上角的 Y 位置。          |
| [parent](https://www.runoob.com/jsref/prop-win-parent.html)  | 返回父窗口。                                                 |
| [screen](https://www.runoob.com/jsref/obj-screen.html)       | 对 Screen 对象的只读引用。请参数 [Screen 对象](https://www.runoob.com/jsref/obj-screen.html)。 |
| [screenLeft](https://www.runoob.com/jsref/prop-win-screenleft.html) | 返回相对于屏幕窗口的x坐标                                    |
| [screenTop](https://www.runoob.com/jsref/prop-win-screenleft.html) | 返回相对于屏幕窗口的y坐标                                    |
| [screenX](https://www.runoob.com/jsref/prop-win-screenx.html) | 返回相对于屏幕窗口的x坐标                                    |
| [sessionStorage](https://www.runoob.com/jsref/prop-win-sessionstorage.html) | 在浏览器中存储 key/value 对。 在关闭窗口或标签页之后将会删除这些数据。 |
| [screenY](https://www.runoob.com/jsref/prop-win-screenx.html) | 返回相对于屏幕窗口的y坐标                                    |
| [self](https://www.runoob.com/jsref/prop-win-self.html)      | 返回对当前窗口的引用。等价于 Window 属性。                   |
| [status](https://www.runoob.com/jsref/prop-win-status.html)  | 设置窗口状态栏的文本。                                       |
| [top](https://www.runoob.com/jsref/prop-win-top.html)        | 返回最顶层的父窗口。                                         |

**方法**

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [alert()](https://www.runoob.com/jsref/met-win-alert.html)   | 显示带有一段消息和一个确认按钮的警告框。                     |
| [atob()](https://www.runoob.com/jsref/met-win-atob.html)     | 解码一个 base-64 编码的字符串。                              |
| [btoa()](https://www.runoob.com/jsref/met-win-btoa.html)     | 创建一个 base-64 编码的字符串。                              |
| [blur()](https://www.runoob.com/jsref/met-win-blur.html)     | 把键盘焦点从顶层窗口移开。                                   |
| [clearInterval()](https://www.runoob.com/jsref/met-win-clearinterval.html) | 取消由 setInterval() 设置的 timeout。                        |
| [clearTimeout()](https://www.runoob.com/jsref/met-win-cleartimeout.html) | 取消由 setTimeout() 方法设置的 timeout。                     |
| [close()](https://www.runoob.com/jsref/met-win-close.html)   | 关闭浏览器窗口。                                             |
| [confirm()](https://www.runoob.com/jsref/met-win-confirm.html) | 显示带有一段消息以及确认按钮和取消按钮的对话框。             |
| [createPopup()](https://www.runoob.com/jsref/met-win-createpopup.html) | 创建一个 pop-up 窗口。                                       |
| [focus()](https://www.runoob.com/jsref/met-win-focus.html)   | 把键盘焦点给予一个窗口。                                     |
| getSelection()                                               | 返回一个 Selection 对象，表示用户选择的文本范围或光标的当前位置。 |
| [getComputedStyle()](https://www.runoob.com/jsref/jsref-getcomputedstyle.html) | 获取指定元素的 CSS 样式。                                    |
| [matchMedia()](https://www.runoob.com/jsref/met-win-matchmedia.html) | 该方法用来检查 media query 语句，它返回一个 MediaQueryList对象。 |
| [moveBy()](https://www.runoob.com/jsref/met-win-moveby.html) | 可相对窗口的当前坐标把它移动指定的像素。                     |
| [moveTo()](https://www.runoob.com/jsref/met-win-moveto.html) | 把窗口的左上角移动到一个指定的坐标。                         |
| [open()](https://www.runoob.com/jsref/met-win-open.html)     | 打开一个新的浏览器窗口或查找一个已命名的窗口。               |
| [print()](https://www.runoob.com/jsref/met-win-print.html)   | 打印当前窗口的内容。                                         |
| [prompt()](https://www.runoob.com/jsref/met-win-prompt.html) | 显示可提示用户输入的对话框。                                 |
| [resizeBy()](https://www.runoob.com/jsref/met-win-resizeby.html) | 按照指定的像素调整窗口的大小。                               |
| [resizeTo()](https://www.runoob.com/jsref/met-win-resizeto.html) | 把窗口的大小调整到指定的宽度和高度。                         |
| scroll()                                                     | 已废弃。 该方法已经使用了 [scrollTo()](https://www.runoob.com/jsref/met-win-scrollto.html) 方法来替代。 |
| [scrollBy()](https://www.runoob.com/jsref/met-win-scrollby.html) | 按照指定的像素值来滚动内容。                                 |
| [scrollTo()](https://www.runoob.com/jsref/met-win-scrollto.html) | 把内容滚动到指定的坐标。                                     |
| [setInterval()](https://www.runoob.com/jsref/met-win-setinterval.html) | 按照指定的周期（以毫秒计）来调用函数或计算表达式。           |
| [setTimeout()](https://www.runoob.com/jsref/met-win-settimeout.html) | 在指定的毫秒数后调用函数或计算表达式。                       |
| [stop()](https://www.runoob.com/jsref/met-win-stop.html)     | 停止页面载入。                                               |