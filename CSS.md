
==css integration==

inline style:
```
<h2 style = "color:red";>

in style tag in head section:

<head>
    ...
    <style>
    h2{ color: red;}
    </style>
</head>

<body>
    ...
</body>
```

external file:
```
<head>
   ...
     <link href="_css/styles.css" rel="stylesheet" type="text/css">
</head>

<body>
    ...
</body>
```



==short hand notation==
https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties
*using shorthand and longhand values may result in values being overwritten.
because shorthand中没被设定的值会回到默认
```
body{
    width: 70%
    margin: 0, auto
}
```
这里的 margin 有 top,down, left, right 四个设置。
top 和 down是0, left 和 right为auto

权重
===

同权重css后来的样式会覆盖先定义的。

*权重表 cssspecificity.com
*权重计算 specificity.keegan.st

选择器
==
,:和

空格：nested
\>: child     (only immediate child, not all descendants)

+: adjacent sibling
~: later general siblings



pseudo-class selectors:
用来选择不explicitly属于DOM里面的元素
创建出来的pseudo-elements do not be ome part of the dom

a:visited  => if href has been visited

:active => the moment you click on it
:hover =>悬停
:focus => selected by using tab on keyboard


:first-child =>指定父元素的第一个子元素，可以不指定父元素等同于*为父元素
:last-child =>指定父元素的最后一个子元素，可以不指定父元素*为父元素
:first-of-type =>指定父元素的第一个子类型（eg. `<p>`,`<a>`），可以不指定父元素*为父元素
:last-of-type =>指定父元素的最后一个子类型，可以不指定父元素*为父元素
:nth-child() => 括号内可以放keyword也就是even或odd, 数字 或 algebraic formula
:nth-type() => 括号内可以放keyword也就是even或odd, 数字 或 algebraic formula
- 这个formula 的pattern是 an+b
- a= any number, n= 0~n , b= any number  eg. 3n+2
- a= 每个数之间的距离 b=开始的数
通常 type selectors比较常用因为可以辨识不同的元素类型


:before 
:after
这两个是用来生成元素插入进指定的元素前面和后面的，谨记生成的元素不会被加入到dom，for display only. 生成的内容要用引号包围。里面可使用unicode. 用/标记unicode
eg.
```
element:before{
    content: "/2764";
}
element:after{
    content: '这是绝对内容';
}
```


ccs3用::来标识pseudo-class

选择器应用场景
type selector - used to select all or most instances of an element
eg. p {}

class - used for more specific styles that can also be applied to different elements
eg.  .highlight{}

id - used for unique or global styles that are not repeated
eg. #global-foter{}

attribute selector - use `[attr]` or `[attr=""]`
eg.
```
 input <input type="search">

    <style>
    [type="search"]{
        border: solid red 1px;
    }

    [type]{
      margin: 1px;   
    }

    </style>
```

- avoid going more than 3 levels deep for descendant selectors, or just use BEM naming stye.

父子元素继承：some properties can be inherited and some are not


property 简写 short hand 
==
```
h1{
    font-family:Georgia, "Times New Roman", Sans serif
    font-size 2em;
    font-weight: normal;
    font-style: italic;
    margin 1em 0 .4em;
}
这里margin的简写设置了top1 左右:0 bottom:.4
```
|所有|
|上下， 左右|
|上，左右，下|
|上，右，下，左|   （顺时针）

字体font
=====
字体整理： www.fontsquirrel.com
网络字体资源：fonts.google.com

通常2到3个font就很足够了。

font options:
    1.web-safe fonts: 普遍在系统已经预安装的,直接调用用户系统自身有的
    2.web fonts: 引用网络上的有提供资源的字体
    3.internal fonts: 字体文件放在项目源文件里.
        在css文件里这样写：
        ```
        @font-face{
            font-family:'Museo Sans';
            src: url(museo-sans.ttf);
        }

        body{
            font-family: 'Museo Sans', Arial, sans-serif;
        }
        ```




Typography: the study of the design and use of type for communication

typeface: a set of fonts, designed with common characteristics and composed of glyphs

font family:a broad class of similar fonts used in a prioritized list of fonts. 

font: individual files that are part of a typeface

经典generic font family for typefaces:
    - serif: have small decorative lines, some kind of shadowed bolded
    - Sans serif: nodecorative lines
    - script: 手写
    - Decorative: distinct and ornamental
    - monospace: 间隙明显，平均

设置typeface, 用font-family
body{
    font-family: 'Helvtica Neue';
}
不同系统的默认安装的fonts不一样，显示也不一定相同。
用cssfontstact.com查看font是适用性

使用font stack,按优先顺序列举fall back fonts。
h2{
    font-family:'Helvetica Nenue', Arial, sans-serif;
}
*use similar fonts
*use generic font family as the last option
*always declare generic fonts without quotes, 非generic可以用'' 和""包含

a specific font family name in quotes, double or single, so Arial, "Arial", and 'Arial' are equivalent.

Only the CSS-defined generic font family names like sans-serif must be written without quotes.

recommended to quote font family names that contain white space, digits, or punctuation characters other than hyphens

大小
--
任意浏览器的默认字体高都是16px

px=》px像素（Pixel）。相对长度单位。像素px是相对于显示器屏幕分辨率而言的。
em =》 是按当前预设大小的比例，所以font-size :2em 的意思就是当前设置x2
- 使用 em 单位的元素字体大小根据它们来定。 但该元素可能继承其父元素的字体大小，而父元素又继承其父元素的字体大小，等等。 因此，以 em 为单位的元素字体大小可能会受到其任何父元素的字体大小影响。

- 为了简化font-size的换算，需要在css中的body选择器中声明Font-size=62.5%，这就使em值变为 16px*62.5%=10px, 这样12px=1.2em, 10px=1em, 也就是说只需要将你的原来的px数值除以10，然后换上em作为单位就行了。

- 所以我们在写CSS的时候，需要注意两点：

    1. body选择器中声明Font-size=62.5%；
    2. 将你的原来的px数值除以10，然后换上em作为单位；
    3. 重新计算那些被放大的字体的em数值。避免字体大小的重复声明。
    也就是避免1.2 * 1.2= 1.44的现象。比如说你在#content中声明了字体大小为1.2em，那么在声明p的字体大小时就只能是1em，而不是1.2em, 因为此em非彼em，它因继承#content的字体高而变为了1em=12px。


rem=》 root em, 相对HTML根元素的大小。
        
- 除了IE8及更早版本外，所有浏览器均已支持rem。对于不支持它的浏览器，应对方法也很简单，就是多写一个绝对单位的声明。这些浏览器会忽略用rem设定的字体大小。下面就是一个例子：p的font-size是（20*0.9）=18px

```
html{
    font-size:20px;  
}

p {font-size:18px; font-size:.9rem;}
```
font-weight 字重
--
取值从100~900， lighter(400) normal(700) bold bolder

通常字体拥有的字重数量为4至6个。

normal和bold对应的字重是每种字体必备的
常见的 Arial、Helvetica、Georgia等等，只有400(normal)和700(bold)。

lighter和bolder 是相对当前继承font-weight的

若所指定字重不存在直接匹配，则会通过字体匹配算法匹配邻近可用字重。
匹配到同样字重特定字重时会看起来没有“生效”。

font-style 字样式
--
italic oblique normal

In the purest (type designer) sense, an oblique is a roman font that has been skewed a certain number of degrees (8-12 degrees, usually). An italic is created by the type designer with specific characters (notably lowercase a) drawn differently to create a more calligraphic, as well as slanted version.

almost no font families in the wild specify both Italic and Oblique faces, and most rendering engines will supply the other face if the specified face is unavailable for that font. 

line-height 行高
--
文字之间的行距离
取值单位：px % em rem 
相对单位或没有单位  相对font-size。


颜色
==
选色：coolors.co

hex表达：rgb, 3色的值域是0到255，十六进制，每个值都是2位数

3pair特殊值的shorthand notation可以这样写：
```
background-color:#77d;
意思是
background-color:#7777dd;

background-color:#234;
意思是
background-color:#223344;
```

reserved keyword: gold 等等
不同browser 的reserved color值不一样
```
background-color:gold;
```
用10进制
```
backgrond: rgb(44,45,140);
```

text-decoration 文字修饰
==
划线位置依次为 上 中 下 无
取值：
 overline
 line-through
 underline
 none

text-transform 文字转换
--
取值： capitalize uppercase lowercase none


display: inline, block, inline block, grid
====
block:
--
- 上下左右都可以加padding margin
- height = content
- width = 100% of container
- elements start on a new line
- can wrap other block and inline elements
- div p h1

inline:
--
-  左右可以加padding margin 但上下不能改。
- height and width = content
- elements align left, in a line.
- inline elements can only nest other inline elements(except \<a> tags in html5)
- a space is shown between elements in a line, we can remove it by setting parent's font size to 0.
- eg. a span strong


inline block:
--
- inline elements with padding and margins added on all four sides
- makes inner elements have block for display. 
- 也相当与一个可以和其它元素同行显示的block。

grid:
--
www.gridcalculator.dk
- conventionally consists of container and items
- define column widths and row heights in continer css, eg 3 columns and 2 rows
    - grid-template-columns: 200px 200px 200px;
    - grid-template-rows: 300px 175px; 
    - grid特有的新unit， fr, 可代替px, 用来设定比例  . eg.grid-template-columns:  2fr 1fr 1fr;
- then the gaps
    - grid-column gap: 10px;
    - grid-row gap: 20px;

html
```
<div class="grid-container">
    <div class="grid-item">
    
    </div>
    <div class="grid-item">
    
    </div>
    <div class="grid-item">
    
    </div>
</div>
```
css
```
.grid-container{
    display:grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 300px 175x;
    grid-column-gap: 10px;
    grid-row-gap: 10px;
}

.grid-item{
    border: 1px solid #222;
    text-align:center;
}

```

flex
--
- convention is to name classes with flex-container and flex-item
- 比grid更加简洁
- 在flexitem里面set width，而不是在container定义。column height是自动的对齐到最长的column的。
- 展示方向flex-direction: column|row-reverse
- 排版 flex-flow: row wrap;
- 排版 justify-content: flex-end|center|space-btween|space-around;
更多排版:
cssreference.id/flexbox
更多grid vs flex:
https://www.webdesignerdepot.com/2018/09/grid-vs-flexbox-which-should-you-choose/


box model:
==
- width and height: sets speciic size for the content box
- padding: space inside of the elementt
- margin: space outside of the element
- border: displays between the padding and margin

```
|m|b|p.content.p|b|m|
--
- convention is to use flex-container and flex-item as classes
```
 
 
margin/外边距:
--
--
- convention is to use flex-container and flex-item as classes
http://www.hicss.net/do-not-tell-me-you-understand-margin/

margin始终是透明的。
外边距的 margin-width 的值类型有：auto | length | percentage
1、如果margin只有一个值，表示上右下左的margin同为这个值。
2、如果 margin 只有两个值，第一个值表示上下margin值，第二个值为左右margin的值。
3、如果margin有三个值，第一个值表示上值，第二个值表示左右值，第三个值表示下值。例如：margin:10px 20px 30px; 就等于 margin:10px 20px 30px 20px;
4、如果margin有四个值，分别对应上右下左margin值。

有关使用负值布局的
https://www.jianshu.com/p/6e4f5de683ae
https://www.cnblogs.com/2050/archive/2012/08/13/2636467.html#2457812

margin的负值：
通常情况下负值会使边距向内收缩。负边距对这些由文档流控制的元素的作用是，会使它们在文档流中的位置发生偏移。 一切只要是由文档流决定的东西，负边距就能起作用了。
当边距收缩超过元素本身的宽的时候，该元素在网页上不占位置，其它元素会重叠。
但是，当元素没有固定宽度的时候（或者 width:auto;），负值会增加自身宽度，视觉上向两边拉开！


垂直(上下)外边距合并:
两个相遇的垂直外边距，包括自身的外边距相遇的情况，会合并为一，值大的外边距会吞噬小的。
外边距合并指的是，当两个垂直外边距相遇时，会合并为一。
正正边距：合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。
正负边距：合并后的外边距的高度等于 正负相加后的值，0

只有普通文档流中块框的垂直外边距才会发生外边距合并。行内框、浮动框或绝对定位之间的外边距不会合并。



- use of margin
负值可以让margin往相反方向移动。

- 自动居中: 先设定width,再设margin 为auto
- max-width是 width 的最大值， 小于这个数的话默认自动改变。
- min-width是 width 的最小值， 大于这个数的话默认自动改变。
- max-height height 的最大值， 小于这个数的话默认自动改变。
- min-height是 height 的最小值， 大于这个数的话默认自动改变。

```
block {
    max-width: 950px;
    margin: auto;
}
```

padding 内边距
--




Float 浮动
--
变更文档流 让元素浮起，后面的元素会绕开浮起的元素继续以文档流占据位置。（影响stacking order）
float会把inline元素变成block
不对float元素设置宽的话，宽是content 的宽

用clear终止float对文档流的影响。
例子：
```
img{
    float:left;
}

//在遇到h1的时候结束float的影响。
h1{
    clear:both；//clears both left and right float
}

```
带有float的元素会脱离父元素的文档流，若父元素只有float元素，默认父元素本身height是0.

父元素要适应高度就要对float的clear处理(self-clearing floats): 

第一种方法是overflow
overflow:auto | overflow | hidden
overflow是带有float的元素 的 父元素用来处理float 元素超出父元素边框的情况的。

auto是增加一个scroll bar

hidden是直接隐藏超出部分

overflow是直接显示。

```

第二种方法
.clearfix:after{
    content:"";
    display: table;
    clear: both;
}

<div class="parent clearfix">
    <p>floated element</p>
    <p>floated element</p>
</div>
```


box-sizing 盒子模型的大小计算
--

box-sizing：content-box|border-box
默认是content-box,size等于c, p b m的设定会增加size
border-box就是 p 和 b 不会影响总size，设置p b会把content缩小
由于border-box比较流行，我们可以用box model fix:
html{
    box-sizing: border-box;
}
*,*:beore,*:after{
box-sizing: inherit;
}


nav (只有html5有)
---
html5前后对比
```
<div class ="nav">
    <ul>
        <li><a href="#"> Home </a></li>
        <li><a href="#"> about </a></li>
        <li><a href="#"> contact </a></li>
    </ul>
</div>

<nav>
    <a href="#"> Home </a>
    <a href="#"> about </a>
    <a href="#"> contact </a>
</nav>
```

position
--
- used to arrange elements relative to the default page flow or browser viewport.
- 取值：relative, absolute,ixed,static & inherit.
- position is also used with a combination of offset properties: top, right, bottom, left.
eg.
```
.box{
    position: relative;
    top: 10px;
}
```
static=>该关键字指定元素使用正常的布局行为，即元素在文档常规流中当前的布局位置。此时 top, right, bottom, left 和 z-index 属性无效。

relative=>该关键字下，元素先放置在未添加定位时的位置，再在不改变页面布局的前提下调整元素位置（因此会在此元素未添加定位时所在位置留下空白）。position:relative 对 table-*-group, table-row, table-column, table-cell, table-caption 元素无效。

absolute=>不为元素预留空间，通过指定元素相对于最近的非 static 定位祖先元素的偏移，来确定元素位置。若全都是static祖先，那就以document body 定位。 绝对定位的元素可以设置外边距（margins），且不会与其他边距合并。

fixed=>不为元素预留空间，而是通过指定元素相对于屏幕视口（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变。打印时，元素会出现在的每页的固定位置。fixed 属性会创建新的层叠上下文。当元素祖先的 transform  属性非 none 时，容器由视口改为该祖先。

sticky =>盒位置根据正常流计算(这称为正常流动中的位置)，然后相对于该元素在流中的 flow root（BFC）和 containing block（最近的块级祖先元素）定位。 在不超出containing block的情况下向指定方向保持定义的距离，表现为被视口推移的效果。在所有情况下（即便被定位元素为 table 时），该元素定位均不对后续元素造成影响。当元素 B 被粘性定位时，后续元素的位置仍按照 B 未定位时的位置来确定。position: sticky 对 table 元素的效果与 position: relative 相同。

z-index: the stacking context. z值只对position不是static的元素有用
--
natural stacking order:
```
1. <html>
2. <body>
3. block level elements in the normal page flow
4. floated elements, not positioned
5. inline descendant elements in the normal fflow
6. positioned elements

z-index越高，stacking level越高, z-index只会在同z层面比较。先define的区块会被后define的区块覆盖。
eg.
```
Root
z1
z2
z3
    z4
    z5
    z6
z4
```
When no z-index property is specified, elements are rendered on the default rendering layer 0 (zero).
If several elements share the same z-index value (i.e., they are placed on the same layer), stacking rules explained in the section Stacking without z-index apply.
```


写css之前通常会确保浏览器的样式环境是干净的。
reset stylesheet 是指prewritten stylesheet containing rules that override all the default browser styles to an unstyled baseline. 重置html样式到无样式一样

normalize 是指 prewritten stylesheet containing rules that aim to create consistent default styles, rather than removing them. 统一html样式到html5

Icon-font
--
https://fontawesome.com
http://fontawesome.dashgame.com/
font-awesome是字体图标库
从font-awesome找到文件源，引用后就可以开始用了。
看似图像其实是特殊符号。

background常用
--
background-color
background-image
background-repeat:no-reppeat
background-position:top right;
background-attachment: fixed;//fixed position to viewport
background-size   //1 value for width, and will take percentage, keep ratios.2 values for width and hight.  "cover" 按比例放大覆盖全部。

using shorthand form for background

background-size must be included after background-position with '/'
if no use of background-pisition then just declare twice.
eg.
'''
selector{
    background: url(image.jpg) no-repeat fixed 0px 0px /cover;
}

或者

selector{
    background: url(image.jpg) no-repeat fixed;
    background-size: cover;
}

'''
多个背景图:
```
background: url(image1.png) no-repeat top right,
            url(image1.png) no-repeat top lef;

或者
background: url(image1.png) ，url(image1.png)
background-repeat: no-repeat,no-repeat；
background-position: top right, bottom left;

```

透明色rbga, a从0到1: rgba(199,21,133,0.5);

渐变色: linear-gradient(color,color) //可以把透明色放进括号

应用例子，图上放透明渐变层
background:linear-gradient(rgba(255,255,255,0.8),rgba(199,21,133,0.5)),
                            rgba(199,21,133,0.5)),
                            url(image.png);




responsive design
==
https://mediaqueri.es/
http://www.liquidapsive.com/
参考响应式排版

graceful degradation:浏览器效果优先，用降级功能来保证老版浏览器对基本功能支持。
progressive enhancement:内容调用优先，先保证最低体验，再逐步升级。mobile-first design 能有效减少多余区块

一般设计flexible layouts流程：
- 先设计流动css(fluid css),然后加入responsive css. fluid是单纯宽窄调整，responsive是根据屏幕改变位置。
- 内容与容器位置绑定
- 不依赖defined devices sizes
- 主要区块用百分比宽度 eg.用max-width和百分比width

这一句非常重要的，它确保浏览器的width跟device一样
```
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
```

media queries
--
当浏览器视窗设定值大就apply css, 无论当前条件符合与否都一定会下载css。

media types:
print: match 打印
speech: match screen reader
screen: match不是print或speech
all: match all, 但不设置默认也是all

media features:
描述对device的要求
设置device 的 feature 例如width, height, device orientation

media queries:
media queries可以用在html 的<link> tag to 在特定情况下加入指定的CSS文件 to HTML page.
```
<link media="screen and (max-width: 400px) rel="stylesheet" href="mobile.css">

```
也可以在css中直接用 @media 和{}， 加条件用`and`
```
@media all and (max-width: 400px){
    .selector{
        ...
    }
}
```
和下面的一样
```
@media (max-width: 400px){
    .selector{
        ...
    }
}

```

width vs. min- and max-width
--
viewport的width包含了scroll bar的width

```
@media(width:640px){
    /*targets a width of exactly 640px only*/
}
@media(min-width:640px){
    /*targets a width >= 640px */
}
@media(max-width:640px){
    /*targets a width of <= 640px /
}

@media(min-width:640px) and (max-width:940px){
    /*targets a width of <= 640px /
}
```
当min-width和max-width取值相同，后deined的优先生效。因此在640px,max-width那个生效。



