
#####const bodyParser = require('body-parser';

- JSON body parser
- Raw body parser
- Text body parser
- URL-encoded form body parser

用法：作为中间件处理接收到的请求的body

    const express = require('express');
    const app = express();
    app.use(bodyParser.json());

#####require('dotenv').config();
用法：可以在.env里面定义常量，然后通过process.env.<常量> 调用.可以配合gitignore在repo用来隐藏数据

    //.env
    PORT=8080
 
  .

    //app.js
    require('dotenv').config();
    console.log("Listen:" + process.env.PORT);

