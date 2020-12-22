# 八.Get 与Post的区别
1.演示环境搭建 ：https://ceshiren.com/t/topic/3653

为了避免其他因素的干扰，使用 Flask 编写一个简单的 Demo Server。

1）安装flask

`pip install flask`

2）创建一个 hello.py 文件
```python
hello.py
from flask import Flask, request


app = Flask (__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

@app.route("/request", methods=['POST', 'GET'])
def hellp():
    #拿到request参数
    query = request.args
    #El request form
    post = request.form
    #分别打印拿到的参数和form
    return f"query: {query}\n"\
           f"post: {post}"
```
3）启动服务

`export FLASK_APP=hello.py flask run`

提示下面信息则表示搭建成功。
```
* Serving Flask app "hello.py" 
* Environment: production 
  WARNING: Do not use the development server in a production environment. Use a production WSGI server instead. 
* Debug mode: off 
* Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

2.CURL 命令发起 GET／POST 请求

1）发起 GET 请求，a、b参数放入 URL 中发送，并保存在 get 文件中：

`curl 'http://127.0.0.1:5000/request?a=1&b=2' -V -S &>get`


2）发起 POST 请求,a、b参数以 form-data格式发送,并保存在post 文件中:

`curl 'http://127.0.0.1:5000/request?' -d "a=1&b=2" -V -S &>post`


将得到的文件进行比对：

![对比](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/%E5%AF%B9%E6%AF%94.png)

3.get与post的区别总结：

1）http的method字段不同

2）post可以附加body，可以支持form、json、xml、binary等各种数据格式

3）行业通用的规范：
- 无状态变化的建议使用get请求
- 数据的写入与状态修改建议用post
