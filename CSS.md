==css integration==

css is render blocking

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
\*using shorthand and longhand values may result in values being overwritten.
because shorthand 中没被设定的值会回到默认

```
body{
    width: 70%
    margin: 0, auto
}
```

这里的 margin 有 top,down, left, right 四个设置。
top 和 down 是 0, left 和 right 为 auto

# 权重

https://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048

同权重 css 后来的样式会覆盖先定义的。

*权重表 cssspecificity.com
*权重计算 specificity.keegan.st

# 选择器

,:和

空格：nested
\>: child (only immediate child, not all descendants)

+: adjacent sibling
~: later general siblings


a:visited => if href has been visited

:active => the moment you click on it
:hover =>悬停
:focus => selected by using tab on keyboard

:first-child =>指定父元素的第一个子元素，可以不指定父元素等同于*为父元素
:last-child =>指定父元素的最后一个子元素，可以不指定父元素*为父元素
:first-of-type =>指定父元素的第一个子类型（eg. `<p>`,`<a>`），可以不指定父元素*为父元素
:last-of-type =>指定父元素的最后一个子类型，可以不指定父元素*为父元素
:nth-child() => 括号内可以放 keyword 也就是 even 或 odd, 数字 或 algebraic formula
:nth-type() => 括号内可以放 keyword 也就是 even 或 odd, 数字 或 algebraic formula
 
- 这个 formula 的 pattern 是 an+b
- a= any number, n= 0~n , b= any number eg. 3n+2
- a= 每个数之间的距离 b=开始的数
  通常 type selectors 比较常用因为可以辨识不同的元素类型

:before
:after
这两个是用来生成元素插入进指定的元素前面和后面的，谨记生成的元素不会被加入到 dom，for display only. 生成的内容要用引号包围。里面可使用 unicode. 用/标记 unicode
eg.

```
element:before{
    content: "/2764";
}
element:after{
    content: '这是绝对内容';
}
```

https://www.growingwiththeweb.com/2012/08/pseudo-classes-vs-pseudo-elements.html
ccs3 用:来标识 pseudo-class,::标识 psudo-element

Pseudo-classes select regular elements but under certain conditions, like when their position relative to siblings or when they’re under a particular state. Here is a list of pseudo-classes in CSS3:

Dynamic pseudo-classes
:link
:visited
:hover
:active
:focus

UI element states pseudo-classes
:enabled
:disabled
:checked

Structural pseudo-classes
:first-child
:nth-child(n)
:nth-last-child(n)
:nth-of-type(n)
:nth-last-of-type(n)
:last-child
:first-of-type
:last-of-type
:only-child
:only-of-type
:root
:empty
Other pseudo-classes
:not(x)
:target
:lang(language)

Pseudo-elements
Pseudo-elements effectively create new elements that are not specified in the markup of the document and can be manipulated much like a regular element. This introduces huge benefits for creating cool effects with minimal markup, also aiding significantly in keeping the presentation of the document out of the HTML and in CSS where it belongs.

With the introduction of CSS3 the difference between pseudo-classes and pseudo-elements is a lot more clear as it is now the standard to use double colon (::) on pseudo-elements, however we should be using single colon until certain browsers are phased out (I’m looking at you IE8 and below). Here is a list of pseudo-elements in CSS3:

::before
::after
::first-letter
::first-line

选择器应用场景
type selector - used to select all or most instances of an element
eg. p {}

class - used for more specific styles that can also be applied to different elements
eg. .highlight{}

id - used for unique or global styles that are not repeated
eg. #global-foter{}

attribute selector

- use `[attr]` or `[attr=""]`
- [class*="example"] selects an element with a class of "example" anywhere within the value

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

# property 简写 short hand

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
|上，右，下，左| （顺时针）

# 字体 font

字体整理： www.fontsquirrel.com
网络字体资源：fonts.google.com

通常 2 到 3 个 font 就很足够了。

font options:
1.web-safe fonts: 普遍在系统已经预安装的,直接调用用户系统自身有的
2.web fonts: 引用网络上的有提供资源的字体
3.internal fonts: 字体文件放在项目源文件里.
在 css 文件里这样写：
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

经典 generic font family for typefaces: - serif: have small decorative lines, some kind of shadowed bolded - Sans serif: nodecorative lines - script: 手写 - Decorative: distinct and ornamental - monospace: 间隙明显，平均

设置 typeface, 用 font-family
body{
font-family: 'Helvtica Neue';
}
不同系统的默认安装的 fonts 不一样，显示也不一定相同。
用 cssfontstact.com 查看 font 是适用性

使用 font stack,按优先顺序列举 fall back fonts。
```
h2{
font-family:'Helvetica Nenue', Arial, sans-serif;
}
```
* use similar fonts
* use generic font family as the last option
* always declare generic fonts without quotes, 非 generic 可以用'' 和""包含

a specific font family name in quotes, double or single, so Arial, "Arial", and 'Arial' are equivalent.

Only the CSS-defined generic font family names like sans-serif must be written without quotes.

recommended to quote font family names that contain white space, digits, or punctuation characters other than hyphens

## 大小

任意浏览器的默认字体高都是 16px

px=》px 像素（Pixel）。相对长度单位。像素 px 是相对于显示器屏幕分辨率而言的。
em =》 是按当前预设大小的比例，所以 font-size :2em 的意思就是当前设置 x2

- 使用 em 单位的元素字体大小根据它们来定。 但该元素可能继承其父元素的字体大小，而父元素又继承其父元素的字体大小，等等。 因此，以 em 为单位的元素字体大小可能会受到其任何父元素的字体大小影响。

- 为了简化 font-size 的换算，需要在 css 中的 body 选择器中声明 Font-size=62.5%，这就使 em 值变为 16px\*62.5%=10px, 这样 12px=1.2em, 10px=1em, 也就是说只需要将你的原来的 px 数值除以 10，然后换上 em 作为单位就行了。

- 所以我们在写 CSS 的时候，需要注意两点：

  1. body 选择器中声明 Font-size=62.5%；
  2. 将你的原来的 px 数值除以 10，然后换上 em 作为单位；
  3. 重新计算那些被放大的字体的 em 数值。避免字体大小的重复声明。
     也就是避免 1.2 \* 1.2= 1.44 的现象。比如说你在#content 中声明了字体大小为 1.2em，那么在声明 p 的字体大小时就只能是 1em，而不是 1.2em, 因为此 em 非彼 em，它因继承#content 的字体高而变为了 1em=12px。

rem是 root em, 相对 HTML 根元素的大小
- 除了 IE8 及更早版本外，所有浏览器均已支持 rem。对于不支持它的浏览器，应对方法也很简单，就是多写一个绝对单位的声明。这些浏览器会忽略用 rem 设定的字体大小。下面就是一个例子：p 的 font-size 是（20\*0.9）=18px

```
html{
    font-size:20px;
}

p {font-size:18px; font-size:.9rem;}
```

## font-weight 字重

取值从 100~900， lighter(400) normal(700) bold bolder

通常字体拥有的字重数量为 4 至 6 个。

normal 和 bold 对应的字重是每种字体必备的
常见的 Arial、Helvetica、Georgia 等等，只有 400(normal)和 700(bold)。

lighter 和 bolder 是相对当前继承 font-weight 的

若所指定字重不存在直接匹配，则会通过字体匹配算法匹配邻近可用字重。
匹配到同样字重特定字重时会看起来没有“生效”。

## font-style 字样式

italic oblique normal

In the purest (type designer) sense, an oblique is a roman font that has been skewed a certain number of degrees (8-12 degrees, usually). An italic is created by the type designer with specific characters (notably lowercase a) drawn differently to create a more calligraphic, as well as slanted version.

almost no font families in the wild specify both Italic and Oblique faces, and most rendering engines will supply the other face if the specified face is unavailable for that font.

## line-height 行高

文字之间的行距离
取值单位：px % em rem
相对单位或没有单位 相对 font-size。

# 颜色

选色：coolors.co

hex 表达：rgb, 3 色的值域是 0 到 255，十六进制，每个值都是 2 位数

3pair 特殊值的 shorthand notation 可以这样写：

```
background-color:#77d;
意思是
background-color:#7777dd;

background-color:#234;
意思是
background-color:#223344;
```

reserved keyword: gold 等等
不同 browser 的 reserved color 值不一样

```
background-color:gold;
```

用 10 进制

```
backgrond: rgb(44,45,140);
```

# text-decoration 文字修饰

划线位置依次为 上 中 下 无
取值：
overline
line-through
underline
none

## text-transform 文字转换

取值： capitalize uppercase lowercase none

none vs visibility
display:none; 直接从 dom 移除
visibility: hidden; 空间一直占着，还在 dom 里面

# display: inline, block, inline block, grid

## block:

- 上下左右都可以加 padding margin
- height = content
- width = 100% of container
- elements start on a new line
- can wrap other block and inline elements
- div p h1

## inline:

- 左右可以加 padding margin 但上下不能改,要改的话需要用改 line-height.
- height and width = content
- elements align left, in a line.
- inline elements can only nest other inline elements(except \<a> tags in html5)
- a space is shown between elements in a line, we can remove it by setting parent's font size to 0.
- eg. a span strong

## inline block:

- inline elements with padding and margins added on all four sides
- makes inner elements have block for display.
- 也相当与一个可以和其它元素同行显示的 block。

## grid:

www.gridcalculator.dk

- conventionally consists of container and items
- define column widths and row heights in continer css, eg 3 columns and 2 rows
  - grid-template-columns: 200px 200px 200px;
  - grid-template-rows: 300px 175px;
  - grid 特有的新 unit， fr, 可代替 px, 用来设定比例 . eg.grid-template-columns: 2fr 1fr 1fr;
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

## flex
https://internetingishard.com/html-and-css/flexbox/
笔记整理：
属性：
在flexcontiner使用：
justify-content: flex-start|center|flex-end|space-around|space-btween 
align-items: flex-start|center|flex-end|strech|baseline
  * space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
  * space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
  * baseline是项目的第一行文字的基线对齐。
  * stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
flex-wrap:nowrap|wrap
flex-direction:row|column|row-reverse|column-reverse
  * direction默认row, column是把main和cross对调。
  * row-reverse和column-reverse使用时小心，因为reverse是对正常排序后的每一个row或column反序排列的。eg.321一行，54一行。

在flexitem使用：
- order属性定义flex item的排列顺序。数值越小，排列越靠前，默认为0。
-   align-self: auto | flex-start | flex-end | center | baseline | stretch;
    - align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。
- flex
    - 基础 https://www.youtube.com/watch?v=CFgeJq4l1YM
    - flex-grow属性定义item在extra space的增长占比，默认为0，即如果存在剩余空间，也不grow。
    - flex-shrink属性定义了item的缩小的速度，默认为1，即如果空间不足，该项目将缩小。
    - flex-basis属性定义了在分配多余空间之前，item占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
    - flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。
    - flex：initial等于 flex:0 1 auto
    - flex: auto等于 flex: 1 1 auto
        ```
        flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]

        .flex-item {
        /*原本*/
        flex: 0 1 100px;

        /* this */
        flex: 1 100px;

        /* is the same as */
        flex-grow: 1;
        flex-basis: 100px;

        /* and it leaves the flex-shrink property alone, which would be */
        flex-shrink: inherit; /* defaults to 1 */

        }
        ```

更多排版:
  cssreference.id/flexbox
- 在 flexitem 里面 set width，而不是在 container 定义。column height 是自动的对齐到最长的 column 的。
  
更多 grid vs flex:
  https://www.webdesignerdepot.com/2018/09/grid-vs-flexbox-which-should-you-choose/
- inline flex会让Flex container display inline




# box model:

- width and height: sets speciic size for the content box
- padding: space inside of the elementt
- margin: space outside of the element
- border: displays between the padding and margin

```
|m|b|p.content.p|b|m|
--
- convention is to use flex-container and flex-item as classes
```

## margin/外边距:

--

- convention is to use flex-container and flex-item as classes
  http://www.hicss.net/do-not-tell-me-you-understand-margin/

margin 始终是透明的。
外边距的 margin-width 的值类型有：auto | length | percentage
1、如果 margin 只有一个值，表示上右下左的 margin 同为这个值。
2、如果 margin 只有两个值，第一个值表示上下 margin 值，第二个值为左右 margin 的值。
3、如果 margin 有三个值，第一个值表示上值，第二个值表示左右值，第三个值表示下值。例如：margin:10px 20px 30px; 就等于 margin:10px 20px 30px 20px;
4、如果 margin 有四个值，分别对应上右下左 margin 值。

有关使用负值布局的
https://www.jianshu.com/p/6e4f5de683ae
https://www.cnblogs.com/2050/archive/2012/08/13/2636467.html#2457812

margin 的负值：
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
  负值可以让 margin 往相反方向移动。

- 自动居中: 先设定 width,再设 margin 为 auto
- max-width 是 width 的最大值， 小于这个数的话默认自动改变。
- min-width 是 width 的最小值， 大于这个数的话默认自动改变。
- max-height height 的最大值， 小于这个数的话默认自动改变。
- min-height 是 height 的最小值， 大于这个数的话默认自动改变。

```
block {
    max-width: 950px;
    margin: auto;
}
```

## padding 内边距

## Float 浮动

变更文档流 让元素浮起，后面的元素会绕开浮起的元素继续以文档流占据位置。（影响 stacking order）
float 会把 inline 元素变成 block
不对 float 元素设置宽的话，宽是 content 的宽

用 clear 终止 float 对文档流的影响。
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

带有 float 的元素会脱离父元素的文档流，若父元素只有 float 元素，默认父元素本身 height 是 0.

父元素要适应高度就要对 float 的 clear 处理(self-clearing floats):

第一种方法是 overflow
overflow:auto | overflow | hidden
overflow 是带有 float 的元素 的 父元素用来处理 float 元素超出父元素边框的情况的。

auto 是增加一个 scroll bar

hidden 是直接隐藏超出部分

overflow 是直接显示。

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

## box-sizing 盒子模型的大小计算

box-sizing：content-box|border-box
默认是 content-box,size 等于 c, p b m 的设定会增加 size
border-box 就是 p 和 b 不会影响总 size，设置 p b 会把 content 缩小
由于 border-box 比较流行，我们可以用 box model fix:
html{
box-sizing: border-box;
}
_,_:beore,\*:after{
box-sizing: inherit;
}

## nav (只有 html5 有)

html5 前后对比

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

## position

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

relative=>该关键字下，元素先放置在未添加定位时的位置，再在不改变页面布局的前提下调整元素位置（因此会在此元素未添加定位时所在位置留下空白）。position:relative 对 table-\*-group, table-row, table-column, table-cell, table-caption 元素无效。

absolute=>不为元素预留空间，通过指定元素相对于最近的非 static 定位祖先元素的偏移，来确定元素位置。若全都是 static 祖先，那就以 document body 定位。 绝对定位的元素可以设置外边距（margins），且不会与其他边距合并。

fixed=>不为元素预留空间，而是通过指定元素相对于屏幕视口（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变。打印时，元素会出现在的每页的固定位置。fixed 属性会创建新的层叠上下文。当元素祖先的 transform 属性非 none 时，容器由视口改为该祖先。

sticky =>盒位置根据正常流计算(这称为正常流动中的位置)，然后相对于该元素在流中的 flow root（BFC）和 containing block（最近的块级祖先元素）定位。 在不超出 containing block 的情况下向指定方向保持定义的距离，表现为被视口推移的效果。在所有情况下（即便被定位元素为 table 时），该元素定位均不对后续元素造成影响。当元素 B 被粘性定位时，后续元素的位置仍按照 B 未定位时的位置来确定。position: sticky 对 table 元素的效果与 position: relative 相同。

## z-index: the stacking context. z 值只对 position 不是 static 的元素有用

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

写 css 之前通常会确保浏览器的样式环境是干净的。
reset stylesheet 是指 prewritten stylesheet containing rules that override all the default browser styles to an unstyled baseline. 重置 html 样式到无样式一样

normalize 是指 prewritten stylesheet containing rules that aim to create consistent default styles, rather than removing them. 统一 html 样式到 html5

## Icon-font

https://fontawesome.com
http://fontawesome.dashgame.com/
font-awesome 是字体图标库
从 font-awesome 找到文件源，引用后就可以开始用了。
看似图像其实是特殊符号。

## background 常用

background-color
background-image
background-repeat:no-reppeat
background-position:top right;
background-attachment: fixed;//fixed position to viewport
background-size //1 value for width, and will take percentage, keep ratios.2 values for width and hight. "cover" 按比例放大覆盖全部。

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

透明色 rbga, a 从 0 到 1: rgba(199,21,133,0.5);

渐变色: linear-gradient(color,color) //可以把透明色放进括号

应用例子，图上放透明渐变层
background:linear-gradient(rgba(255,255,255,0.8),rgba(199,21,133,0.5)),
rgba(199,21,133,0.5)),
url(image.png);

# responsive design

https://mediaqueri.es/
http://www.liquidapsive.com/
参考响应式排版

graceful degradation:浏览器效果优先，用降级功能来保证老版浏览器对基本功能支持。
progressive enhancement:内容调用优先，先保证最低体验，再逐步升级。mobile-first design 能有效减少多余区块

一般设计 flexible layouts 流程：

- 先设计流动 css(fluid css),然后加入 responsive css. fluid 是单纯宽窄调整，responsive 是根据屏幕改变位置。
- 内容与容器位置绑定
- 不依赖 defined devices sizes
- 主要区块用百分比宽度 eg.用 max-width 和百分比 width

这一句非常重要的，它确保浏览器的 width 跟 device 一样

```
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
```

## media queries

当浏览器视窗设定值大就 apply css, 无论当前条件符合与否都一定会下载 css。

media types:
print: match 打印
speech: match screen reader
screen: match 不是 print 或 speech
all: match all, 但不设置默认也是 all

media features:
描述对 device 的要求
设置 device 的 feature 例如 width, height, device orientation

media queries:
media queries 可以用在 html 的<link> tag to 在特定情况下加入指定的 CSS 文件 to HTML page.

```
<link media="screen and (max-width: 400px) rel="stylesheet" href="mobile.css">

```

也可以在 css 中直接用 @media 和{}， 加条件用`and`

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

## width vs. min- and max-width

viewport 的 width 包含了 scroll bar 的 width

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

当 min-width 和 max-width 取值相同，后 deined 的优先生效。因此在 640px,max-width 那个生效。

# image 图像格式

- pixel density: the number of pixels within a space.
  eg. units are PPI(pixels per inch) or DPI(dots per inch)
- retina displays 比正常的屏幕 ppi/dpi 多了一倍。

## Raster images(bitmap images):

composed of tiny squares called pixels
can become blury when it is zoomed in

- jpeg: Joint Photographic Experts Group. 16bit format - blends reds, greens. and blues to create millions of colors. normally used for photographs.
- Gif: graphics interchange format.j can be animated. 256 colors and supoorts transparency. giphy.com , getcloudapp.com is for making gifs
- PNG: portable network graphics, png-8 has 256 colors with no transpency, png-24 has millions of colors and supports transparency.
  -Canvas，顾名思义，是画布，通过 JavaScript 来绘制 2D 图形。Canvas 是逐像素进行渲染的。在 canvas 中，一旦图形被绘制完成，它就不会继续得到浏览器的关注。如果其位置发生变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象。

## vector images:

composed of lines and curves called paths

- svg:Scalable Vector Graphics (SVG) is an XML-based vector image format for two-dimensional graphics with support for interactivity and animation. composed of lines and paths. edges of vectore image are always smooth

- html uses predefined tags, and xml uses custom tagas
- thenounproject.com
- svg 可以通过 css 修改。可以 zai file content 里面的 css 修改，也可以给 svg 加一个 class 通过外部的 css 修改。
- 目前最好的加载 svg 的方法： https://vecta.io/blog/best-way-to-embed-svg
- svg file content :

```
<?xml version="1.0" encoding="utf-8"?>
<svg version="1.1" id="Vrstva_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
	 viewBox="0 0 595 595" style="enable-background:new 0 0 595 595;" xml:space="preserve">
<style type="text/css">
	.st0{fill-rule:evenodd;clip-rule:evenodd;fill:#FFFFFF;}
	.st1{fill-rule:evenodd;clip-rule:evenodd;}
</style>
<g>
	<rect x="0.5" y="-0.8" class="st0" width="595.3" height="595.3"/>
	<path class="st1" d="M308.8,443.1c17,0,30.9,11.8,31.4,26.6c0.2,5.3-4,9.7-9.3,9.7h-31.4c-47.9,0-109.2,11.7-146.3-25.5
		c-19.1-19.2-30.2-45.8-28.7-74.1c1.4-26.4,15.3-50.7,36.5-65.2c7.1-4.9,14.7,5.8,7.8,10.9c-16,11.8-26.6,30.2-27.7,51
		c-1.2,22.6,7.6,43.9,23,59.1c-6.2-79.2,73.7-106.7,99.3-162.1c2.8-6.2,4.6-12,5.5-17.8c39.1,8.5,87.4-18.7,44.8-95.9
		c64.7,144.9-167.6,91.6-47.8-10c20.2-37.5,74.2-52.9,115.9-16.5c13,11.4,22.8,18.1,40.7,17c7.3-0.5,15.7-0.6,22.7,1.1
		c2.3-4.5,7.1-7.6,12.5-7.6c7.8,0,14.1,6.3,14.1,14.1c0,6.9-5,12.6-11.5,13.9c-0.5,3.7-1.8,8.1-4,13.1
		c-16.6,37.9-43.9,47.2-78.9,54.3c-27.8,5.7-7.1,23.9,1.9,51.9c14.3,44.5-5.6,72.7-10.6,104.9c-2.5,16.2-5.5,47.2,18.5,47.2
		c17,0,30.9,11.8,31.4,26.6c0.2,5.3-4,9.7-9.3,9.7h-44.3c-15.7,0-28.9-30.6-35.3-57.9c6.3-12.5,8-26.2,3.8-39
		c-9.5-29.3-46.4-42.6-82.4-29.7c-7.7,2.7-14.6,6.5-20.8,10.9c7.4-4.4,15.8-7.8,24.9-9.6c35-7.1,67.3,10.1,72.2,38.5
		c3.5,20.1-8,39.3-24.1,51.1C305.2,443.3,307,443.1,308.8,443.1L308.8,443.1z M368.2,150.2c3.8,0.6,6.7,3.5,7.5,7.2
		c0-0.1,0-0.3,0.1-0.4c1.1-7.6-3.9-14.6-11.2-15.7c-7.3-1.1-14,4.3-15.2,11.9c-1.1,7.6,3.9,14.6,11.2,15.7c1.4,0.2,2.8,0.2,4.2-0.1
		c-4.6-1-7.6-5.6-6.9-10.5C358.6,153.1,363.2,149.5,368.2,150.2z"/>
</g>
</svg>
```

- Png

## suportting hight pixel density display:

- use icon fonts or svgs because they are vector based and scalable format. Allow css to make changes to them. But these are not suitable for photographs.
- image replacement, use suitable image base on the type of diplay. JS requiared to detect the resolution and dynamically replace html images. Retina.Js is a liabrary for this.
- background image replacement with media queries.

```
header{
    background: url(img.jpg);
}
@media(min-resolution:192 dpi){
    /*using a larger image for retina display*/
    header{
        background: url(image@2x.jpg);
    }
}
```

```
Canvas | SVG
------------ | -------------
依赖于分辨率 | 不依赖于分辨率（矢量）
不支持事件处理器 |  支持事件处理器
弱的文本渲染能力 | 最适合带有大型渲染区域的应用程序（比如说 Google 地图）
能够以.png 或 .jpg 格式保存结果图像 | 复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）
最适合图像密集型的游戏，其中的许多对象会被频繁绘制 | 不适合游戏应用
```

# 兼容性

https://caniuse.com
里面有说不同浏览器的写法。

## vender prefix

先写带 prefix 的，不带 prefix 的放到最后。浏览器会从上到下 scan 直到找到对应的 prefix

- android, ios,chrome and safari: -webkit-
- internet Explorer: -ms-
- firefox: -moz-
- opera: -o-

# 动画

## transition

简单特效动画，从起点到终点两个形态的转换。
用法， 放在原始状态
longhand:
transition-property: color;
transition-duration: 1s;
transition-timing-function: linear;
transition-delay: 0.5;

shorthand:
transition-property:color 1s linear 0.5;

can only work between when 2 properties have inbetween state.

transition-property: color;
transition-duration: 1s;
transition-timing-function: linear | ease-out （先快后慢）| ease-in （先慢后快）|Ease-in-out （慢快慢）
transition-delay: 0.5;

```
div{
    backgroud-color: light-blue;
    margin-left:0;
    transition-property: color;
    transition-duration: 1s;
    transition-timing-function: linear;
    transition-delay: 0.5;
}
div:hover{
    background-color: white;
    margin-lect:100
}
```

## @keyframes

相对比 transition 复杂的动画，可以定义多个属性一起变化.animation 就是由多个 keyframe 组成的。
3 个部分：

- name of animation
- break point
- css property to be animated
  属性：
  animation-name: keyframe 组名字;
  aniamtion-duration: 时长;
  animation-timing-funciotn:linear|ease-in|ease-out|ease-in-out;
  animation-delay: 延时时长;
  animation-interation-count: 重复次数 | infinite;

```
@keyframes bounceRed{
    0%{
        top:0px;
    }
    50%{
        top:250px;
    }
    100%{
        top:0px;

    }
}

.ball{
    width:50px;
    height:50px;
    position:absolute;
    border-radius: 50%;
    animation-name: bounceRed;
    aniamtion-duration:1.5s;
    animation-timing-funciotn:ease;
    animation-dekat:1s;
    animation-interation-count: 3;
}
```

# 形状属性

改变默认 float 的文档流方框形状
可以用 百分比值
位置从方框  左上角开始算
eg.
shape-outside:circle();
clip-path:circle();

circle(半径 at 横向位置 纵向位置)

polygon(x-axis y-axis, x-axis y-axis, x-axis y-axis， 其它点..)

inset
https://tympanus.net/codrops/css_reference/inset/

# Responsive design tips

www.ia.net/topics/responsive-typography-the-basics/

## Absolute font size

commonly used and good for learning
great for accuracy and control

```
body{
    font-size: 20px;
}
h1{
    font-size: 35px;
}
h2{
    font-size: 30px;
}
.footnote{
    font-size: 15px;
}

@media(max-width: 800px){
    body{
        font-size: 16px;
    }
    h1{
        font-size: 28px;
    }
    h2{
        font-size: 24px;
    }
    .footnote{
        font-size: 12px;
    }
}
```

## relative font size

use rem , just neet to change root element for overall changes.

```
html{
    font-size: 1rem;
}
body{
    font-size: 1.25rem;
}
h1{
    font-size:2.1875rem;
}
h2{
    font-size:1.1875rem;
}
.footnote{
    font-size:0.9375rem;
}

@media(max-width: 600px){
    html{
           font-size: 0.75rem;
    }
}

@media(max-width: 600px){
    html{
           font-size: 0.75rem;
    }
}
```

# viewport units

viewport 是浏览器的窗口
viewport units 是
vw: viewport width
vh: viewport height
vmin: 宽或高两者中最小的
vmax: 宽或高两者中最大的

## 使用 viewport units 做 fluid typography

不使用 mediaqueries 也可以做

设置 html 的 fontsize 为 viewport units，通常用 vw 然后其它再用 rem。

```
html{
    font-size: 2vw;
}
body{
    font-size: 1.25rem;
}
h1{
    font-size:2.1875rem;
}
h2{
    font-size:1.1875rem;
}
.footnote{
    font-size:0.9375rem;
}
```

以下是一些额外的关于字体大小比例的讨论
https://www.smashingmagazine.com/2016/05/fluid-typography/

## accessibilities

webaim.org 测试 accessibilities

visual

- avoid adding text to image files, use an alt attribute.
- random11y.com for color contrast

motor

- 可以 use tabindex to control the tab flow.

# 起名

- use funcitional names
  eg. alert button 比 redbutton 好， except grid is ok to have grid1 grid2
- use lowercase letters only
- use - not \_
- css comment

```
/*---------
section comment block
----------*/

/*
sub section comment block
----------*/


```

# refactoring
