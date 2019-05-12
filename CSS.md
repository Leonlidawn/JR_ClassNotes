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

选色：coolors.co

父子元素继承：some properties can be inherited and some are not