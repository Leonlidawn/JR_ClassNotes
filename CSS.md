
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



==short hand notation==
https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties
```
body{
    width: 70%
    margin: 0, auto
}
```
这里的 margin 有 top,down, left, right 四个设置。
top 和 down是0, left 和 right为auto

1
====

同权重css后来的样式会覆盖先定义的。

*权重表 cssspecificity.com
*权重计算 specificity.keegan.st
pseudo-class selectors:
a:visited  => if href has been visited

:active => the moment you click on it
:hover =>悬停
:focus => selected by using tab on keyboard

选择器应用场景
type selector - used to select all or most instances of an element
eg. p {}

class - used for more specific styles that can also be applied to different elements
eg.  .highlight{}

id - used for unique or global styles that are not repeated
eg. #global-foter{}

*  avoid going more than 3 levels deep for descendant selectors, or just use BEM naming stye.

父子元素继承：some properties can be inherited and some are not

===字体font=====
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

==大小==
em =》 是按当前预设大小的比例，所以font-size :2em 的意思就是当前设置x2

==颜色==
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
