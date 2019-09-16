conventions
==
js通常用camelCase.

variables
- start with lowercase
- greenDuck 

objects and classes
- start with uppercase
- var date = Date()

constants
- all caps
- const = CONSTANT




javascript的加载
==
如果你想js在页面render之前执行，放在head里面，在render之后执行的话放在body之后。

- load right away
```
<script src="script.js"></script>
```

- asynchronize loading   用异步缓解堵塞， js的下载和html parsing同步进行,等下载完毕便停止html parsing,执行js,再继续html parsing。
```
<script src="script.js" async></script>
```

- deferred loading 也是异步，js的下载和html parsing同步进行， 但js的执行会在所有html parsing结束后进行。
```
<script src="script.js" defer></script>
```







run some code when window is loaded`
```
window.onload = function(){
    ...
}
```

var 全局变量

dom maniputation:
--
```
document.getEleentById("tabs")
document.getElementsByTagName("li");
document.getElementsByClassName("container");
```

ECMAScript是一种standard, JavaScript是一种符合ecmascript的语言，浏览器用ecmascript解释JavaScript，所以对我们而言，两者是一个东西。目前es6的某些功能还没被支持，所以我们需要用bable去把es6转换成es5. es6通常是指区别于es5的新的JavaScript。

jquery是一个js库。


数据类型data types
==
Number:整数和小数，但小数的运算是不准确的，所以一般先乘以10的n次方作整数运算后再转回小数。
String
Boolean:true | false
Null: null
Undefined


typeof 用来查类型
```
var a = 3;
console.log(typeof a)//gives number
```
js是弱类型，要小心数据类型。
例如+号可以用在字符串和算术。

用 == 比较两个参数的值，不测类型。
用 === 会比较类型和值。

compare and execute懒人写法之
ternary operator：
- 
condition ? trueExecution : falseExecution
```
a==b ? console.log("Match"): console.log("no match");

function getFee(isMember) {
  return (isMember ? "$2.00" : "$10.00");
}
```
arrays
--
```
var pens =["red","blue","green","orange"];

// PROPERTIES:
// Get a property of an object by name:
// console.log("Array length: ", pens.length); 4

// METHODS:
// Reverse the array:
// pens.reverse(); 

// Remove the first value of the array:
// pens.shift();

// Add comma-separated list of values to the front of the array:
// pens.unshift("purple", "black");

// Remove the last value of the array:
// pens.pop();

// Add comma-separated list of values to the end of the array:
// pens.push("pink", "prussian blue");

// The splice() method changes the contents of an array after the position by removing or replacing existing elements and/or adding new elements. 这里pos从1开始，0的话是指第一个数之前。
//pens.splice(pos,n)
//pens.splice(pos,n,replacement)
// pens.splice(2, 1) // at index 2, remove 1 element.
// pens.splice(2, 1,"gold") // at index 2, replace 1 element with "gold".

// The slice() method returns a shallow copy of a portion of an array into a new array object selected from begin to end (end not included) where begin and end represent the index of items in that array. The original array will not be modified.
// var newPens = pens.slice();

// Return the first element that matches the search parameter after the specified index position. Defaults to index position 0. Arguments: pens.indexOf(search, index):
// var result = pens.indexOf(search, index);
// console.log("The search result index is: ", result);

// Return the items in an array as a comma separated string. The separator argument can be used to change the comma to something else. Arguments: pens.join(separator):
// var arrayString = pens.join(separator);
// console.log("String from array: ", arrayString);
```

MDN documentation for Array:
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array

functions
==
named functions
is used when function needs to be run multiple times. named function is hoisted when they are declared alone. 作为值，也就是=号右边出现的话是不会被提升的。
```
whoIsTheBoyWhoLived('Harry'); // Harry Potter!

console.log(spell); // undefined

function whoIsTheBoyWhoLived(name) {

  console.log(name + ' Potter!');

}

var spell = 'accio';

console.log(spell); // accio
```
named fucntion也可以被called without (),直接显示function结构内容。如果
```
function b(){
    return 1;
}

a=b();

console.log(b);// function b(){ return 1;}

console.log(b());// 1
console.log(a);// 1
```

anonymous functions/function expressions
no names, needs to be tied to a variable or event to run. Function expressions are not hoisted.
```
whoIsTheBoyWhoLived('Harry'); // TypeError: not a function

var whoIsTheBoyWhoLived = function(name) {

  console.log(name + ' Potter!');

};

var whoIsTheChosenOne = (name) => {

  console.log(name + ' Potter!');

}
```
Immediately invoked function expression
sometimes 我们想assign函数给出的结果 instead of the function，.(run as soon as the browser encounters it)
```
(function () {
    statements
})(参数);
```

variable scope
==

有一些补充内容参考了 https://segmentfault.com/a/1190000016678888
（面试要点）在js里面
- var is funtional scoped, var 值会被声明提升(hoisting)到funcitonal scope的顶端，声明提升只是提升声明，但赋值会留在原地

- const  and  let is blockScope

```
        function fScope(){
            // 声明提升到这里, 赋值留在原来位置
            // var a;
            // var b;
            if(true){
                var a = 1;
                var b = 2;
            }
            console.log(a+b); // 3
        }

        function bScope(){
            if(true){
                let a = 1;
                const b = 2;
            }
            console.log(a+b); // undefine
        }
```

object
==
creating a single object.
```
var onlyCourse = new Object();

var onlyCourse = {
    title: "jr1",
    level: 1,
    views: 0,
    updateViews: function(){
        return ++onlyCourse.views;
    }
}
```

writing a object constructor function
注意constructor要大写，by convention
注意使用new 来做binding，不然constructor function不返回任何东西导致undefined且内部的this binding会错乱，很可能bind to global or somewhere else.
关于这个有趣的文章
https://raganwald.com/2014/07/09/javascript-constructor-problem.html
```
function Course(title,level){
    this.title = title;
    this.level = level;
    this.views = 0;
    this.updateViews: function(){
        return ++onlyCourse.views;
    };
}

var course01 = new Course("Javascript",1);
console.log(course01);
var course02 = new Course("Advanced Javascript",2);
console.log(course02);

```

读取property的dot and bracket notetion
course.title 和 course["title"]的作用是一样的.
bracket notation可以用来读取带有非常规名字的property。
```
console.log(course["WP:image"]);
```



closure
==
要吃透
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures
- lexical scoping, which describes how a parser resolves variable names when functions are nested. The word "lexical" refers to the fact that lexical scoping uses the location where a variable is declared within the source code to determine where that variable is available. Nested functions have access to variables declared in their outer scope.
- A closure is the combination of a function and the lexical environment within which that function was declared. 
- A closure refers to a function using lexical environment for variable lookups.
- lexical environment 继承特质，被多次nested的函数可以access到所有祖先的variable.
```
function giveMeEms(pixels){
    var baseValue =16;
   
    function doTheMath(){
        return pixels/baseValues;
    }

    return doTheMath; //we are returning a funciton object
}

var smSize = giveMeEms(12);//we are getting a function object
var mdSize = giveMeEms(18);
var lgSize = giveMeEms(24);

console.log(smSize);
//ƒ doTheMath(){return pixels/baseValues;}  返回的是doTheMath的function结构

console.log("sm size:" smSize());//we now exacute the function object

```

make a function factory, making use of the lexical environment.
```
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

//add5 and add10 are closures. They share the same function body definition, but store different lexical environments. In add5's lexical environment, x is 5, while in the lexical environment for add10, x is 10.

var add5 = makeAdder(5); //passed 5 as x, get a function returned
var add10 = makeAdder(10);

console.log(add5(2));  // 7  //passed 2 as y 
console.log(add10(2)); // 12

```
一个运用closure的改变css设定的字体大小的example
html
```
<p>Some paragraph text</p>
    <h1>some heading 1 text</h1>
    <h2>some heading 2 text</h2>

    <a href="#" id="size-12">12</a>
    <a href="#" id="size-14">14</a>
    <a href="#" id="size-16">16</a>
```

css
```
body {
  font-family: Helvetica, Arial, sans-serif;
  font-size: 12px;
}

h1 {
  font-size: 1.5em;
}
h2 {
  font-size: 1.2em;
}
```

js
```
function makeSizer(size) {
  return function() {
    document.body.style.fontSize = size + 'px';
  };
}

var size12 = makeSizer(12);
var size14 = makeSizer(14);
var size16 = makeSizer(16);

document.getElementById('size-12').onclick = size12;
document.getElementById('size-14').onclick = size14;
document.getElementById('size-16').onclick = size16;

```
另外一个利用closure制造 封装好3个public method的counter的例子
```
var makeCounter = function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() { changeBy(1); },
    decrement: function() {changeBy(-1);},
    value: function() {return privateCounter;}
  }
};

var counter1 = makeCounter();
var counter2 = makeCounter();
alert(counter1.value()); /* Alerts 0 */
counter1.increment();
counter1.increment();
alert(counter1.value()); /* Alerts 2 */
counter1.decrement();
alert(counter1.value()); /* Alerts 1 */
alert(counter2.value()); /* Alerts 0 */
N
```
上面的例子也可以这样写,当然，只有利用function的closure特性才可以做到随时更新lexical environment 的数值。
```
var makecounter = function(){
    var num = 0;
    return {
        increment: function(){return ++num;} ,
        decrement: function(){return --num;} ,
        value: function(){
            return num;
        }

    };
};
```


