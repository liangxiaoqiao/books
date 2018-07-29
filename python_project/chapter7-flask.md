#### Flask教程

##### 简单开始

1. 简单程序

   ```python
   # 安装 pip install flask
   
   # 导入
   from flask import Flask
   
   # 创建
   app = Flask(__name__)
   
   # 路由和视图函数
   @app.route("/")
   def index():
       return '<h1> Hello, World!</h1>'
   
   # 运行
   if __name__ == '__main__':
   	app.run(debug=True)
   ```

2. 路由和视图函数

   ```
   什么是路由？程序需要知道对每个URL请求运行哪些代码，所以保存了一个URL到python函数的映射关系。处理URL和函数之间关系的程序称为路由。
   
   如何定义一个路由？最简单的方法使用程序实例提供的app.route修饰器，把修饰的函数注册为路由。
   
   什么是视图函数？上边修饰的函数就是视图函数。
   ```

   ```python
   # 简单视图函数
   @app.route("/")
   def index():
       return '<h1> Hello, World!</h1>'
   # 支持可变URL的视图函数
   @app.route("/user/<name>")
   def hello_user(name):
       return '<h1>Hello, %s!</h1>' % name
   # 路由中的动态部分默认使用字符串
   # 不过也可也使用类型定义
   @app.route("/user/<int:user_id>")
   def hello_id(user_id):
       return '<h1>Hello, your ID is %d!</h1>' % user_id
   ```

3. 请求上下文

4. 请求调度

5. 请求钩子

   ```
   before_first_request
   before_request
   after_request
   teardown_request
   ```

6. 响应

##### 模板

1. 渲染模板
2. 变量
3. 控制结构
4. 自定义错误页面
5. 链接
6. 静态文件

##### 表单

