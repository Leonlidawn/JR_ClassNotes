==第一个45分钟==
nodejs最新文档参照早期linux版本的文档写的，因为很多api是在linux上开发的，很相似。
nodejs版本号：
奇数：快速开发版本，api有可能被修改，通常用来体验新特性的  
偶数：长期支持版本，api非常稳定
先有奇数版本在有偶数版本

node写代码使用路径的时候使用path模块来自动选择路径的表达方式：window和Linux斜杠就不一样。

assert模块
中文是断式
assert()是assert.ok()简写
assert.ok(<判断式>,<error_message>)

buffer模块是用来处理二进制数据流,初级比较少用

Child Processes 模块通常在服务端使用处理进程，大部分情况是已经封装好的。因为与系统有关，通常是从这个模块的文档找到Linux原版互相对照,还有读系统文档。

==第二个45分钟==
cluster模块，负责load balance的
线程是运行在进程里的，
一个进程只能在一个cpu核心上运行，
因为javascript是单线程的，所以只开一个进程的话单线程是不能充分利用cpu的，所以启动多个进程。
现在的操作系统对进程的处理是分时复用，短时间内切换多个进程在cpu执行。
切换进程本身是cpu从内存数据copy到cpu缓存，启动运算。过多的进程会让cpu浪费资源进行切换。最好的配比是多少个cpu配多少个进程。
负载均衡， elastic node balance
计算节点，进程的分发的策略通常是round loading = 轮询：
    + 将除了loadbalance本身以外的进程编号
    + 重复分配
cluaster模块里面的loadbalance默认为Master。
cluster.isMaster是是判断当前进程是不是Master进程

cluster.fork()是代表要分出一个工作进程

nodejs关于代码是比较脆弱的，进程如果出error但在全局没有被捕获，整个进程就是崩溃停止，因此需要代码收到捕获并且用fork重新制造一个进程出来。

    + 题外话： kubernete(k8s)是 一个高级的进程管理 技术。用于管理docker，docker容器自己不要管进程崩溃处理，k8s帮助接受请求，然后自主分配进程给容器，k8s会监控容器健康，并将其在必要时重启.

用计时器看函数调用的时间：
console.time([label])//放在开头
console.timeEnd([label])//放在末尾

debugger模块
断点测试，但实际开发断点测试效果不太好

DNS模块
对域名解析系统DNS的操作

Errors模块
error本身也是对象，也有不同的类 例如AssertionError和TypeError,因此你也可以自己创建或继承Error class，这样你用instanceof就可以知道error的类别了。

Events模块
事件监测机制，但现在async await出现后比较少见

globals模块
不知道往哪里放的东西就在这放

HTTP模块
nodejs的最火模块

Inspector模块
也是调试用的

Modules模块
__dirname:动态获取当前目录路径
__filename:当前文件名称，包括路径
export:用来暴露模块
module:用来暴露模块
require(): 
    模块都需要先引入才能使用，除了global模块
    引入js代码
    引入json文件

Net模块
TCP的封装

os模块
操作系统的概念

process模块
进程的操作
process.env: 当前进程背负的所有的环境变量

业界约定俗成在启动node的时候加入环境变量比较当前是开发环境还是production环境： NODE_ENV = dev node
process.env里面通常是
NODE_ENV： ‘dev’ 
或
NODE_ENV： ‘production’

querystring模块
处理URL里面的query pair

Readline模块
读入数据

REPL模块
命令行交换

Timers模块
setInterval 定时执行
setTimeout 延时执行

Util模块（还在试验状态）
用开多个javascript实例来实现多线程，比cluster的进程管理轻量，
workerthread不是跟thread,里面封装了v8实例

==第三个45分钟==
package.json里面的
"scripts":{
    "test": "node ./index.js"
}
里面的test是内置命令， 在terminal可以npm test这样用 

npm info express 这样可以查看express这个package的信息，例如dependency
然后再决定要不要Install

在主目录创建 .npmrc配置文件 可以在里面写configuration
例如 package-lock=false
npm install express //在新版本与 --save 一样
npm install express --save//储存安装记录到pakage.json的dependencies里
npm install express --save-dev //储存安装记录在pakage.json 的dev dependencies里
npm uninstall express
npm install --production 会安装除了在dev dependencies里面的包 
npm prune --productin 可以删除所有生产环境不需要的包（包括dev dependencies里面的包）
npm uninstall express

package.json 里的version 例子 
 major.minor.patch
 大版本是有重大改变，不保证无缝升级
 小版本是性能优化，可以无缝升级
 patch是修复bug
4.13.4
 的意思是锁定版本
^4.13.4
 的意思是在下次install的时候会下载 小版本更新
~4.13.4的意思是在下次install的时候会下载 patch更新 
 *的意思是直接最新的。

curl 
curl -i 显示header
curl -I 只显示header
curl -v 显示完整报文, tcp层面的

header 的x-power-by 会告诉你是什么框架发回来的,x-的意思是non-standard,也可以设置不显示

/etc/hosts 里面存有localhost以及其它host的地址，可修改。

wrk是一个压测工具
wrk -t4 -c100 -d10 http://127.0.0.1:8888
4个线程，100个链接，10秒
商业项目 qps 200以上就OK

