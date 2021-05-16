#### flex  弹性布局

- flex-direction 

  - `row`（默认值）：主轴为水平方向，起点在左端。
  - `row-reverse`：主轴为水平方向，起点在右端。
  - `column`：主轴为垂直方向，起点在上沿。
  - `column-reverse`：主轴为垂直方向，起点在下沿

- flex-wrap

  - ```css
     nowrap | wrap | wrap-reverse
    ```

- flex-flow

  - direction 和 wrap 简写

- justify-content

  - `flex-start`（默认值）：左对齐
  - `flex-end`：右对齐
  - `center`： 居中
  - `space-between`：两端对齐，项目之间的间隔都相等。
  - `space-around`：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

- align-items

  - `flex-start`：交叉轴的起点对齐。
  - `flex-end`：交叉轴的终点对齐。
  - `center`：交叉轴的中点对齐。
  - `baseline`: 项目的第一行文字的基线对齐。
  - `stretch`（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

- align-content

  - `flex-start`：与交叉轴的起点对齐。
  - `flex-end`：与交叉轴的终点对齐。
  - `center`：与交叉轴的中点对齐。
  - `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
  - `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
  - `stretch`（默认值）：轴线占满整个交叉轴。

- flex-item

  - flex  下面三个的简写

  - flex-grow  放大比例

  - flex-shrink  缩小比例

  - flex-basis  占据空间

  - order 排序

  - align-self 自身位置

    ```css
    auto | flex-start | flex-end | center | baseline | stretch;
    ```

#### grid  网格布局





```
-moz-transition: width 2s; /* Firefox 4 */
-webkit-transition: width 2s; /* Safari 和 Chrome */
-o-transition: width 2s; /* Opera *
```

#### 1. css 颜色属性

##### 1.1. 字体颜色

字体颜色相关属性设置：

color：red / #fff / rgb(0,0,0) / rgba(0,0,0, 透明度(0-1)

 

##### 1.2. 背景颜色

背景颜色相关属性设置：

background: red / #fff / rgb(0,0,0) / rgba(0,0,0, 透明度(0-1);

 

#### 2. 页面布局相关属性

##### 2.1. display

display

block 设置元素为块状元素

```
<div>、 <p>、<h1>、<form>、<ul> 和 <li>是块级元素
```

inline 设置元素为内联（又叫行内）

```
<span>、<a>、<label>、<input>、 <img>、 <strong> 和<em>是典型的内联
```

元素（行内元素）

inline-block 兼具两者

 有些html元素

```
默认是 inline-block （img, input, textarea, td, th）
```

none 隐藏 该元素不会显示，也不会占据空间

 

##### 2.2. position

2.2.1. position: relative

 相对定位

元素设置为相对定位之后，不会脱离文档流，不影响其他元素

可以通过 left、top、right、bottom给相对定位的元素设置位置

定位元素： 根据 原先默认的位置 去定位

2.2.2. position:absolute

绝对定位

元素绝对定位后，脱离文档流，影响后面的元素。 宽度默认会被内容撑开

可以通过 left、top、right、bottom给绝对定位的元素设置位置

定位规则： 根据第一个定位的祖先元素，如果没有定位的祖先元素，根据html元素。 祖先元素什么定位都可以

2.2.3. position:fixed

left/top/right/bottom: 长度单位；

根据屏幕进行定位

脱离文档流 （宽度默认变成内容撑开）

元素设置为固定定位或绝对定位之后，会变为块状元素

 

##### 2.2... z-index: number 

垂直高度，z是指向自己方向的，主要是为了调浮动的高度

为了让下面的元素能够浮到上面



##### 2.3. clear

消除元素对后面元素的影响， 在后面的元素设置 

clear:both/left/right



##### 2.4. float

1、 浮动元素会被自动设置成块级元素，相当于给元素设置了display:block（块级元素能设置宽和高，而行内元素则不可以）。

2、 浮动元素后边的非浮动元素显示问题。

3、 多个浮动方向一致的元素使用流式排列，此时要注意浮动元素的高度。

4、子元素全为浮动元素的元素高度自适应问题。



##### 2.5. visibility

visibility: visible/hidden

规定元素是否可见，就算不可见，元素依然会**占据一片空间**。



##### 2.6. overflow

overflow: hidden/auto/scroll/visible

规定当内容溢出元素框时发生的事情。

2.6.1. visible

默认值。内容不会被修剪，会呈现在元素框之外。

2.6.2. hidden

内容会被修剪，并且其余内容是不可见的

2.6.3. auto

如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容

2.6.4. scroll

内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容。

2.7. overflow-x 水平方向

2.8. overflow-y  垂直方向



2.9. padding (内边距)

2.10. margin (外边距)

#### 3. css字体属性

##### 3.1. font-family

font-family: Arial, Sans-serif;

##### 3.2. font-size

font-size: 2em / px /  %

##### 3.3. font-weight

font-weight: normal / bold / 0-800

##### 3.4. font-style

font-style: italic (斜体) / oblique (倾斜)

##### 3.5. font-varient

font-variant: small-caps 显示小型大写字母的字体

##### 3.6. font 复合属性

font: italic bold 12px/30px Georgia, serif;

```css
font：font-style  font-weight  font-size/line-height  font-family;
```

 

#### 4. css文本属性

##### 4.1. word-spacing

词的间距，通过空格来识别

##### 4.2. letter-spacing

字母间隔，可以为负值

##### 4.3. text-align

text-align:left/right/center  横向排列 

##### 4.4. vertical-align

vertical-align: middle/top/bottom 垂直对齐

##### 4.5. line-height

line-height 设置行间距离

让一行文字垂直居中。 line-height的值等于元素的高

内联元素(inline inline-block)

##### 4.6. text-decoration

text-decoration: underline(下划线) / overline （上划线）/ line-through（横穿） / none（默认为none）

##### 4.7. text-indent

text-indent:50px

设定首行文本缩进

##### 4.8. word-wrap

word-wrap: break-word 

允许长单词或url地址换到下一行

##### 4.9. overflow-wrap 

同word-wrap？？？没啥用

##### 4.10. white-space

white-space: pre / pre-wrap

对空白的处理方式

white-space :nowrap  文本不会换行，文本会在在同一行上继续，直到遇到 <br> 标签为止。

white-space:pre 空白会被浏览器保留。其行为方式类似 HTML 中的 <pre> 标签。

white-space:pre-wrap 保留空白符序列，但是正常地进行换行。

 

#### 5. 尺寸属性

5.1. width

width: max-width  min-width 设置最大宽度和设置最小宽度

5.2. height

height :max-height min-height

 

#### 6. 边框属性

6.1. border-style

border-style 边框风格 

solid 实线 / dotted 点线 / dashed 虚线 / double 双层 / none 无边框

6.2. border-width

border-width 边框宽度

6.3. border-color

border-color 边框颜色 

6.4. border复合属性

border 复合属性

border: 1px solid #ff6700;

 

#### 8. 背景颜色属性

##### 8.1. background-color

background-color 背景颜色 ">透明）

##### 8.2. background-image

背景图片 url()

##### 8.3. background-repeat

background-repeat 背景图片平铺 repeat/ no-repeat（不重复平铺）

repeat-x（水平方向重复平铺） repeat-y（竖直方向重复平铺）

##### 8.4. background-position

background-position 背景图片位置 10px,10px 根据坐标显示具体图片位置

坐标原点以盒子左上角为准

background-position : right center(右中) / center center 居中 

##### 8.5. background-attachment

background-attachment 背景图片固定 scroll / fixed

 scroll---滚动 fixed --固定

##### 8.6. background复合属性

background: #ccc url（) no-repeat 10px 10px；

background: color url postion/size repeat attachment；

##### 8.7. background-size

 规定背景图像的尺寸(css3新增)

background-size: cover / contain / 400px 300px / 100% 100%

cover:background-size: cover; 优先 铺满元素。 多余的图片裁掉 保证原图比例

contain:background-size: contain; 优先 保证图片显示完整，可能元素不能铺满。 保证原图比例

 

#### 9. 鼠标 cursor

pointer /  move / no-drop

cursor:move 表示对象可被移动

cursor:pointer 指示链接的指针为一双手

cursor:no-drop 无法释放 通常是一个禁止符号。

 

#### 10. 列表相关的css属性

适用于<ol>和<ul> 也可以设置给 <li>

##### 10.1. list-style-type

list-style-type: disc/circle/square.../none 列表项前面的符号

 none常用（去掉前面图标）

##### 10.2. list-style-position

list-style-position: outside/inside

 加个边框就能看到明显的效果inside前面的点在边框里

##### 10.3. list-style-image

list-style-image: url()  

把符号变成图片 最好是小的图片，可以显示完整。

##### 10.4. list-style: 复合属性

```css
list-style:square inside url('/i/arrow.gif');
```

#### 11. 表格相关的css属性

##### 11.1. table-layout

table-layout: auto / fixed  

 列宽固定(相等)

##### 11.2. border-collapse

border-collapse: separate/ collapse

collapse:合并单元格边框

seperate:分开单元格边框

##### 11.3. border-spacing

border-spacing: 长度;  单元格和单元格之间的间隙 

单元格不能合并的前提下，才可以设置border-spacing

##### 11.4. caption-side

caption-side: top/bottom  标题的位置

##### 11.5. empty-cells

empty-cells:hide/show  空的单元格显示/隐藏 单元格不能合并

 

#### 12. css3新增属性

##### 12.1. box-sizing

重新设置 盒子模型的规则

box-sizing: content-box(默认) / border-box （width/height盒子的宽高）

border-box：ie 模型

content-box: 标准模型

##### 12.2. outline

外轮廓 在border的外面 不算盒子

outline:

outline-style

outline-color

outline-width

##### 12.3. opacity 

不透明度

opacity 0~1 小数

##### 12.4. border-radius

边框圆角，值超过一定范围就会整个变成圆形

##### 12.6. box-shadow

阴影 

box-shadow:水平偏移 垂直偏移;  偏移可以负值

box-shadow:水平偏移 垂直偏移 颜色;

box-shadow:水平偏移 垂直偏移 模糊值 颜色; /*最常见的*/

box-shadow:水平偏移 垂直偏移 模糊值 外延值 颜色;

 

##### 12.7. transform 转换

下面是属性值：

translatex()  水平移动，括号里是长度单位

translatey() 垂直方向移动

translate(x, y) 先水平后垂直移动

rotate()  括号里单位：角度 deg

比如：transform:rotate(60deg)  翻转

skewx()  括号里单位角度deg

skewy()

skew(x, y)  扭曲

12.7.1. transform-origin

transform-origin:left top;

设定左上角为变换原点

transform-origin 变换的原点。 对translate没有意义。 对rotate影响大

##### 12.8. transition 过渡

```css
transition： property timing-function duration delay;
// 过渡：属性 过渡的线性效果 持续时间 过渡延迟
transition： all/width/heigth, ease, .8s, 1s;
```

12.8.1. transition-property

transition-property  指定要过渡的属性 用,隔开。默认是 all

12.8.2. transition-duration

transition-duration  过渡持续时间

12.8.3. transition-timing-function

transition-timing-function  过渡线性效果 默认 ease

12.8.4. transition-delay

transition-delay  过渡延迟



##### 12.9. animation  动画

```css
@keyframes mymove {
  from { // 起始位置 from / 0%
    top: 0;
  }
  to {  // 结束位置 to / 100%
    top:200px;
  }
}

animation： name, duration, timing-function, delay, iteration-count, direction
animation： 名称，执行时间，执行速度，等待时间，循环次数，交替播放方式
animation: mymove 2s linear 2s infinite alternate;
动画：动画名称，执行时间， 均匀播放， 等待时间，无限播放， 正反交替
```



12.9.1. animation-name

animation-name  指定动画的名字 @keyframes name 

12.9.2. animation-duration

animation-duration  动画的执行时间，以秒或毫秒计。

12.9.3. animation-timing-function

animation-timing-function  执行效果速度，规定动画的速度曲线。

linear:动画从头到尾的速度是相同的。

ease:默认。动画以低速开始，然后加快，在结束前变慢。

12.9.4. animation-delay

animation-delay  延迟

规定在动画开始之前的延迟。

12.9.5. animation-iteration-count

animation-iteration-count  

 循环次数 infinite(无限)

规定动画应该播放的次数。

12.9.6. animation-direction

animation-direction:  alternate （正向 反向 交替）\ reverse（反向）

规定是否应该轮流反向播放动画。

12.9.7. animation-play-state

animation-play-state: running / paused

规定动画的播放状态



