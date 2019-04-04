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
非关系型数据库
以类似JSON format储存数据 (key value pairs),数据灵活易读
不需要schema

mongod
     : Mongod is the "Mongo Daemon" it's basically the host process for the database. Starting mongod means "start the MongoDB process and run it in the background". 
    By default stores data in /data/db and runs on port 27017.
    The server.

    brew services start mongodb-community@4.0//以服务形式在后台开启
    monod //直接开启

查版本 --version 

配config文件 --config <filename>

配tcp端口 --port <port>
- Default: 27017

配host --bind_ip <hostnames|ipaddresses|Unix domain socket paths>
- Default: localhost ,可以用多个

设置在log中显示的时间format --timeStampFormat <string>
- ctime  Displays timestamps as Wed Dec 31 18:17:54.811.

配秘钥 --keyFile <file>


mongo
    : Mngo is the javascript shell that connects to a specific instance of mongod. When you run mongo with no parameters it defaults to connecting to the localhost on port 27017. If you run mongo against an invalid machine:port combination then it will fail to connect (and tell you as much).
    The client.
    mongodb compass 是官方的GUI mongodb client 

    mongo


显示数据库实例 show dbs


==第二个45分钟==

很多数据库都可以是web service
但是SQlite不是，只存于本地，不需要启动server。

NO-sql
- doc  文档数据库
    - MongoDB
    - DynamoDB
- k/v 无格式，无嵌套，一key对一value的。
    - Redis 最流行，多用于缓存，性能高
    - levelDB
目前web开发标配是doc 数据库加一个redis, 复杂关系的用mysql


Database server: SQLite 不用server,其它数据库有。 是数据库实例的仓库，管理权限，

数据库的不同层面的数据:
databases
- show dbs
- use <dbname>

collections(对应relational db的table)
- show collections
- db.classes.insertOne({name: 'first class'})
  db.classes.insertOne({time: '1'})
- 因为没有schema限制，所以同一个collection里面可以有结构不同的documents
- 如果对结构有要求，可以用中间件校验

documents(对应rdb的row)
 - db.classes.find()
- db.classes.findOne()


fields(对应rdb的 column)
- _id是自动插上的field
-data types: object, text, array, boolean,Number(int32, int64, float),Date(ISODate,timestamp)

