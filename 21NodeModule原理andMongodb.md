==第一个45分钟==
nodejs module面试要点：
nodejs 在web,在terminal直接执行，在文件里被terminal调用不是一个概念。
JavaScript其实只是一个概念，实质是是没有模块的，就只有一个全局的使用环境。
所有独立文件的代码都是存在一个function里，是被函数包裹住的。那么，里面的this就取决于nodejs的引擎怎么处理了，
所以不要依赖this。
__filename和__dirname这两个形式参数只存在于函数里面，nodejs 里面独立模块的局部变量。

再用this的时候尽量用apply,call,bind等显式绑定比较清晰易读
在文件里暴露用module.exports

node目录下的lib和src分别放着它的core js和c代码。js本身不支持模块，所以不同文件的js代码会被拼接成一个字符串并被翻译成c代码，然后再被转换成二进制换取载入速度

==第二个45分钟==

mongo db（mac）
mongod 
    is the primary daemon process for the MongoDB system. 处理数据库后台命令的process。
查版本 --version 




mongodb compass 是官方的GUI mongodb client 
也可以用命令行作为client