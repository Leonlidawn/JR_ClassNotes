专门的node.js服务器框架。

##### Basic routing
相关文件：index主文件和routes路由文件
在文件中需要调用express实例的几个方法：
- const app = require('express');
- const studentRouter = app.Router();

在express中routing这是这个格式的:
app.METHOD(PATH, HANDLER)

- path是路径
  - 如果用RESTful 设计的话 path里面用例如:id/:course/:time这样的方式传递参数。参数是路由地址的一部分。
  - 旧时代设计使用?。如果用?，那么？xxx是不会被当做路由地址的一部分的。
  如果用?来带上参数,然后用querystring得到参数。
  
- handler负责返回结果，如果路径比较复杂，不能简单返回结果，而且有重复，我们可以使用router作为中间件。express实例可以调用方法use(baseurl,middleware)，去根据url后续作出不同的处理。

      //index.js 主文件

      const app = require('express');
      const studentRouter = require('./routes/student');

      app.get('/', function (req, res) {
        res.send('Hello World!')
      });
      app.get('/api/greeting/:name', (req, res) => {
           res.send(`hello ${req.params.name}`);
      });

      app.use('/students', studentRouter);
       
      app.listen(8080);

- express实例提供的router方法让我们可以把路径处理得比较容易。router可以看做express本身的一个阉割版迷你实例，专门用来处理请求的。例如.all .get .post 都有， 但是.listen这些全局把控的方法就没有了。
- 如果是关于数据库的处理，最好建立controller文件和model文件，分别对应逻辑处理和数据类型定义. controller文件内包含所有关于数据处理的函数，函数接受req 和res,处理过后直接res.send发回response.

      // routes/student.js router文件

      const app = require('express');
      const studentRouter = app.Router();
      const studentController = require('../controllers/student');//处理student 数据的逻辑
      const Student = require('../models/student');

      studentRouter.get('/:id', studentController.show);
      studentRouter.get('/', studentController.index);

      module.exports = studentRouter;

- 如果是handler是关于database的操作我们可以用一个建立controller文档专门处理. 数据库存的item是可以定义的，我们创建model文件来定义数据库数据映射的对象。 model带有关于数据库的正删改查方法。model会在controller文件中引用. (数据库api另外解释)

      //controller.js

      const Student = require('../models/student');
      const errorHandler = require('../helpers');
        create: async (req, res) => {
            try {
                const newStudent = new Student(req.body);
                await newStudent.save();
                res.status(201).send(newStudent);
            }
            catch (e) {errorHandler(req, res);}
        },
        show: async (req, res) => {
            const { id } = req.params;
            const student = await Student.findById(id).exec();
            res.status(200).send(student);
        }
      };

      module.exports = studentController;
  
  model文件涉及数据库，下面是以mongodb为例，需要引入mongoose包。 mongoose.model('student', studentSchema);
  https://mongoosejs.com/docs/models.html
  
      //model.js

      const mongoose = require('mongoose');
      const Schema = mongoose.Schema;
      const studentSchema = new Schema(
        {
          first_name: String,
          last_name: String,
          ID: String,
          email: {
            type: String, required: true, validate: () => {
              /.*@+.* /.test(email)
            }
          },
          contacts: [
            {
              phone_number: Number,
              type: String
            }
          ],
          password: String
        }
      );

      module.exports = mongoose.model('student', studentSchema);



