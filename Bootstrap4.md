Styles 层面
Browser styles
bootstrap css
custom css

BS uses a set of resets commands called reboot, 放在reboot.css里面. Reboot makes styles consistent across different browsers and platforms。 It uses rem instead of picels. 1 rem = 16px. 

Basic Typogrphy:
- Reboot.css styles
    - 先用reboot统一所有基本style.
- Rems instead of Ems
- Avoid margin-top
    - bootstrap only adds margin at the bottom of element. 所有不用margin top
- inherit when possible
- border-box sizing
- native font stacks
    - uses default fonts in different platform

text alignmnent utilities:
- text-justify
- text-nowrap
- text(-BREAKPOINT)-POS
    - BREAKPOINT:sm >576px md > 768px lg > 992px > xl > 1200px
        - breakpoint defines the condition of available width for the element. the set style is triggered when condition is true.
    - POS: left center right   
text formmat:
- text-uppercase
- text-lowercase
- text-capitalize
- font-weight-bold
- font-weight-normal
- font-italic
- blockquote
    - 引用来源可以用下面的Bootstrap class
        - blockquote-footer
    - blockquote-reverse 可以使blockquote和blockquote-foote right aligned 

text colors:
- text-success 蓝色
- text-danger 红色
- text-warning 黄色
- text-info 浅蓝色
- text-primary 深蓝色
- text-secondary 灰色
- text-dark 黑色
- text-light 深灰色
- text-white 白色

bg colors:
same as text

lists format:
- list-unstyled => no bullets, left aligned
- list-inline => on ul element
    - list-inline-itemm => on each li element


basic images:
- img-fluid =>responsive image, 随着borderbox缩放大小。
- rounded,rounded-DIR
    -DIR: top right bottom left circle rounded-0(don't round) 
- img-thumbnail => add boarder line and round
- float-left   float-right
- text-center =>center the image and text.
- max-auto => makes the image block and center it 
- figure => css figure class makes the text font look a bit smaller and neat

(new feature, not supported by all browsers)
variables:


var()
:root=>redefine