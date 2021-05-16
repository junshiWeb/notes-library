> cheerio是jquery核心功能的一个快速灵活而又简洁的实现，主要是为了用在服务器端需要对DOM进行操作的地方

### 简介

```
cheerio是nodejs的抓取页面模块，为服务器特别定制的，快速、灵活、实施的jQuery核心实现。适合各种Web爬虫程序。
```

### 安装

```
npm install cheerio
```

### 特点

- ***熟悉的语法\***：cheerio实现了jQuery的一个子集，去掉了jQuery中所有与DOM不一致或者是用来填浏览器的坑的东西，重现了jQuery最美妙的API
- ***快到没朋友\***：cheerio使用了及其简洁而又标准的DOM模型， 因此对文档的转换，操作，渲染都极其的高效。基本的端到端测试显示它的速度至少是JSDOM的8倍
- ***极其灵活\***：cheerio使用了[@FB55](https://link.jianshu.com?t=https://github.com/FB55)编写的非常兼容的[htmlparser2](https://link.jianshu.com?t=https://github.com/fb55/htmlparser2)，因此它可以解析几乎所有的HTML和XML

### 关于JSDOM

cheerio产生的原因是出于对JSDOM的失望，主要体现在以下三点：

- ***JSDOM的解析规则太过于严格\***：JSDOM的解析器无法处理现在许多的流行网站的内容
- ***JSDOM太慢了\***：解析大的网站甚至可以产生可察觉的延迟
- ***JSDOM太过于重量级\***：JSDOM的目标是提供与浏览器一样的DOM环境，但是我们往往不需要这样。我们需要的只是一种简单，熟悉的方式来操作我们的HTML

### 什么时候你应该用JSDOM

cheerio并非万能，当你需要一个浏览器一样的环境时，你最好还是用JSDOM，尤其是你需要进行自动化的功能测试时

### API

后面的例子中用到的HTML模板如下：

```
<ul id="fruits">
  <li class="apple">Apple</li>
  <li class="orange">Orange</li>
  <li class="pear">Pear</li>
</ul>
```

#### 1. 解析html（load）

首先你需要先加载你的HTML。jQuery会自动完成这一步，因为jQuery操作的DOM是固定的。但是在使用cheerio时我们要手动加载我们的HTML文档

首选的方式如下：

```js
var cheerio = require('cheerio'),
$ = cheerio.load('<ul id = "fruits">...</ul>');
```

其次，直接把HTML字符串作为上下文也是可以的：

```js
$ = require('cheerio');
$('ul', '<ul id = "fruits">...</ul>');
```

或者把HTML字符串作为root

```js
$ = require('cheerio');
$('li', 'ul', '<ul id = "fruits">...</ul>');
```

如果你需要自定义一些解析选项，你可以多传递一个对象给load方法：

```js
$ = cheerio.load('<ul id = "fruits">...</ul>', {
    ignoreWhitespace: true,
    xmlMode: true
});
```

更多的解析选项可以参考[domhandler](https://link.jianshu.com?t=https://github.com/fb55/domhandler)和[parser-options](https://link.jianshu.com?t=https://github.com/fb55/htmlparser2/wiki/Parser-options)

#### 2. 选择器（selectors）

cheerio的选择器几乎和jQuery一模一样，所以语法上十分相像

```
$( selector, [context], [root] )
```

**selector**在**context**的范围内搜索，**context**的范围又包含在**root**的范围内。**selector**和**context**可以是一个字符串，DOM元素，DOM数组或者cheerio实例。**root**一般是一个HTML文档字符串

选择器是文档遍历和操作的起点。如同在jQuery中一样，它是选择元素节点最重要的方法，但是在jQuery中选择器建立在CSS选择器标准库上。cheerio的选择器实现了大部分的方法

```js
$('.apple', '#fruits').text()
//=> Apple

$('ul .pear').attr('class')
//=> pear

$('li[class=orange]').html()
//=> <li class = "orange">Orange</li>
```

#### 3. 属性操作（atrributes）

用来获取和更改属性的方法：

**.attr(name, value)**

这个方法用来获取和设置属性。获取第一个符合匹配的元素的属性值。如果某个属性值被设置成null，那么该属性会被移除。你也可以把**map**和**function**作为参数传递进去，就像在jQuery中一样

```js
$('ul').attr('id')
//=> fruits

$('.apple').attr('id', 'favorite').html()
//=> <li class = "apple" id = "favorite">Apple</li>
```

**.removeAtrr(name)**

移除名为name的属性

```js
$('.pear').removeAttr('class').html()
//=> <li>Pear</li>
```

**.hasClass(className)**

检查元素是否含有此类名

```js
$('.pear').hasClass('pear')
//=> true

$('apple').hasClass('fruit')
//=> false

$('li').hasClass('pear')
//=> true
```

**.addClass(className)**

添加类名到所有的匹配元素，可以用函数作为参数

```js
$('.pear').addClass('fruit').html()
//=> <li class = "pear fruit">Pear</li>

$('.apple').addClass('fruit red').html()
//=> <li class = "apple fruit red">Apple</li>
```

**.remoteClass([className])**

移除一个或者多个（空格分隔）的类名，如果className为空，则所有的类名都会被移除，可以传递函数作为参数

```js
$('.pear').removeClass('pear').html()
//=> <li class = "">Pear</li>

$('.apple').addClass('red').removeClass().html()
//=> <li class = "">Apple</li>
```

#### 4. 遍历

**.find(selector)**

在当前元素集合中选择符合选择器规则的元素集合

```js
$('#fruits').find('li').length
//=> 3
```

**.parent()**

获取元素集合第一个元素的父元素

```js
$('.pear').parent().attr('id')
//=> fruits
```

**.next()**

选择当前元素的下一个兄弟元素

```js
$('.apple').next().hasClass('orange')
//=> true
```

**.prev()**

同**.next()**相反

**.siblings()**

获取元素集合中第一个元素的所有兄弟元素，不包含它自己

```js
$('.pear').siblings().length
//=> 2
```

**.children( selector )**

**.each( () => (index, element) )**

遍历函数返回false即可终止遍历

```js
var fruits = [];

$('li').each((i, elem) => {
  fruits[i] = $(this).text();
});

fruits.join(', ');
//=> Apple, Orange, Pear
```

**.map( () => (index, element) )**

遍历数据，对每个数据进行修改后返回

```js
$('li').map(function(i, el) {
  // this === el
  return $(this).attr('class');
}).get().join(', ');
//=> apple, orange, pear
```

**.filter( selector )**

过滤某个类的属性，返回其他的

```js
$('li').filter('.orange').attr('class');
//=> orange
```

**.filter( function(index) )**

过滤传入的参数，返回其他

```js
$('li').filter(function(i, el) {
  // this === el
  return $(this).attr('class') === 'orange';
}).attr('class')
//=> orange
```

**.first()**

查找第一个

```js
$('#fruits').children().first().text()
//=> Apple
```

**.last()**

查找最后一个

```js
$('#fruits').children().last().text()
//=> Pear
```

**.eq( n )**

指定元素号数，缩小元素集合，可以用负数表示倒数第 i 个元素被保留

```js
$('li').eq(0).text()
//=> Apple

$('li').eq(-1).text()
//=> Pear
```

#### 5. 操作DOM

操作DOM结构的方法

**.append( content, [content, ...] )**

用于在**被选元素的结尾**插入元素

**.prepend( content, [content, ...] )**

用于在**被选元素的开头**插入元素

**append** 和 **prepend** 在元素内部添加

**.after( content, [content, ...] )**

用于在被选**元素之后**插入内容

```js
$('.apple').after('<li class = "plum">Plum</li>')
$.html()
//=>  <ul id = "fruits">
//      <li class = "apple">Apple</li>
//      <li class = "plum">Plum</li>
//      <li class = "orange">Orange</li>
//      <li class = "pear">Pear</li>
//    </ul>
```

**.before( content, [content, ...] )**

用于在被选**元素之前**插入内容

```js
$('.apple').before('<li class = "plum">Plum</li>')
$.html()
//=>  <ul id = "fruits">
//      <li class = "plum">Plum</li>
//      <li class = "apple">Apple</li>
//      <li class = "orange">Orange</li>
//      <li class = "pear">Pear</li>
//    </ul>
```

**.remove( [selector] )**

删除所有选中内容

```js
$('.pear').remove()
$.html()
//=>  <ul id = "fruits">
//      <li class = "apple">Apple</li>
//      <li class = "orange">Orange</li>
//    </ul>
```

**.replaceWith( content )**

替换所有选中内容

```js
var plum = $('<li class = "plum">Plum</li>')
$('.pear').replaceWith(plum)
$.html()
//=> <ul id = "fruits">
//     <li class = "apple">Apple</li>
//     <li class = "orange">Orange</li>
//     <li class = "plum">Plum</li>
//   </ul>
```

**.empty()**

只删除选中元素内部内容

```js
$('ul').empty()
$.html()
//=>  <ul id = "fruits"></ul>
```

**.html( [htmlString] )**

用于设定HTML内容的值

```js
$('.orange').html()
//=> Orange

$('#fruits').html('<li class = "mango">Mango</li>').html()
//=> <li class="mango">Mango</li>
```

**.text( [textString] )**

用于设置元素内容的文本

```js
$('.orange').text()
//=> Orange

$('ul').text()
//=>  Apple
//    Orange
//    Pear
```

#### 6. 解析和渲染

```js
$.html()
//=>  <ul id = "fruits">
//      <li class = "apple">Apple</li>
//      <li class = "orange">Orange</li>
//      <li class = "pear">Pear</li>
//    </ul>
```

输出包含自己在内的HTML（outer HTML）

```
$.html('.pear')
//=> <li class = "pear">Pear</li>
```

#### 7.其他

**.toArray()**

得到所有选中的元素数组

```js
$('li').toArray()
//=> [ {...}, {...}, {...} ]
```

**clone([Even[,deepEven]])**

1:一个布尔值（true 或者 false）指示事件处理函数是否会被复制。

2:一个布尔值，指示是否对事件处理程序和克隆的元素的所有子元素的数据应该被复制。

```js
var moreFruit = $('#fruits').clone()
```

**$.root()**

选择文档的根元素

```js
$.root().append('<ul id="vegetables"></ul>').html();
//=> <ul id="fruits">...</ul><ul id="vegetables"></ul>
```

**$.contains( container, contained )**

匹配包含给定文本的元素

