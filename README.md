[TOC]

# flask_web

This is a abc of flask_web

## 一、知识扫盲

### WSGI 接口

了解了HTTP协议和HTML文档，我们其实就明白了一个Web应用的本质就是：

1. 浏览器发送一个HTTP请求；
2. 服务器收到请求，生成一个HTML文档；
3. 服务器把HTML文档作为HTTP响应的Body发送给浏览器；
4. 浏览器收到HTTP响应，从HTTP Body取出HTML文档并显示。

所以，最简单的web就是先把HTML用文件保存好，用一个现成的HTTP服务器软件，接受用户请求，从文件中读取HTML，返回。Apache，Ngnix，Lighttp等这些常见的静态服务器就是干这些事情的。

如果要动态生成HTML，就需要把上述步骤自己来实现。不过，接收HTTP请求、解析HTTP请求、发送HTTP响应都是苦力活，如果我们自己来写这些底层代码，还没开始写动态HTML呢，就得花个把月去读HTTP规范。

正确的做法是底层代码由专门的服务器软件实现，我们用Pyhton专注于生成HTML文档。因为我们不需要接触到TCP连接、HTTP原始请求和响应格式，所以，需要一个统一的接口，让门专门用Python编写Web业务。

这个接口就是WSGI：web server Gateway Interface。
>参考:[廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001386832689740b04430a98f614b6da89da2157ea3efe2000)
>
>参考:[浅析WSGI](https://blog.csdn.net/baidu_35085676/article/details/80184874)

***WSGI是作为Web服务器与Web应用程序或应用框架之间的一种低级别的接口，以提升Web应用开发的共同点。WSGI是基于现存的CGI标准而设计的。***

> 参考:[CGI与Servlet的区别和联系](https://www.cnblogs.com/MuyouSome/p/3938203.html)

### 与Tornado、Django、web.py的对比

Django：1个重武器，包含了web开发中常用的功能、组件的框架；(ORM、Session、Form、Admin、分页、中间件、信号、缓存、ContentType...);

Tornado：2大特性就是**异步非阻塞**、**原生支撑webSocket协议**；

Flask：**封装功能不及Django完善，性能不及Tornado**，但是Flask的[第三方开源组件](http://flask.pocoo.org/extensions/)比较丰富；



## 二、Flask入门项目（windows下开发）

>  参考：[Flask大型教程项目](http://www.pythondoc.com/flask-mega-tutorial/)
### 2.1 新建虚拟环境
```powershell
C:\Windows\system32>virtualenv flask
Using base prefix 'c:\\users\\suntiansheng2\\appdata\\local\\continuum\\anaconda3'
New python executable in C:\Windows\system32\flask\Scripts\python.exe
Installing setuptools, pip, wheel...
done.
```
### 2.2 导入pip包
这些命令行将会下载以及安装我们将会在我们的应用程序中使用的所有的包。

```powershell
# 在虚拟环境的目录下执行
pip install flask
pip install flask-login
pip install flask-openid
pip install flask-mail
pip install flask-sqlalchemy
pip install sqlalchemy-migrate
pip install flask-whooshalchemy
pip install flask-wtf
pip install flask-babel
pip install guess_language
pip install flipflop
pip install coverage
```
### 2.3 目录结构及代码
目录结构

```
D:\MICROBLOG

├─microblog
    ├─app
    │  ├─static
    │  ├─templates
    │  ├─views.py
    │  └─__init__.py
    ├─flask 
    ├─tmp
    └─run.py

```

(1) init.py

```python
from flask import Flask

app = Flask(__name__)
from app import views
```

(2)views.py

```python
from app import app

@app.route('/')
@app.route('/index')
def index():
	return "Hello,World！"
```

(3)

```python
#!flask/bin/python
from app import app
app.run(debug=True)
```


### 2.4 启动项目
在D:\MICROBLOG目录下执行

python run.py

在浏览器中访问：

```
http://127.0.0.1:5000/
```

## 三、web表单

[Flask-WTF](https://flask-wtf.readthedocs.io/en/stable/)：Flask 的简单 WTForms 集成，包含 CSRF、文件上传和 Recaptcha 集成。

[WTForms](https://wtforms.readthedocs.io/en/latest/)：WTForms是一个支持多个web框架的form组件，主要用于对用户请求数据进行验证。

## 四、数据库

[Flask-SQLAlchemy](http://flask-sqlalchemy.pocoo.org/2.3/)：Flask-SQLAlchemy是Flask的SQLAlchemy扩展。

