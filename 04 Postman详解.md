# 四、Postman详解
官网地址：https://www.postman.com
## （一）安装
1.安装过程：下载安装包一步步即可。 

2.页面功能详解

1）主页面字段介绍：

![postman1](https://github.com/tete1987/picture_resource/blob/master/postman1.png)

① 输入需要测试的接口地址，即URL，选择对应的方式（get、post、delete、put）等请求

② Params：输入需要发送的请求参数

③ Authorization：主要输入鉴权信息

④ Header：输入接口的头信息内容

⑤ Body：输入需要测试的内容

⑥ Pre-request Script：设置环境变量或全局变量

⑦ Tests：设置断言

⑧ Send：发送请求

⑨ Cookie：保存接口的cookie信息

⑩ Code：将测试脚本已代码形式展示

⑪ New Collection：创建新的用例集

⑫ 已创建的用例集


2）Body 功能字段详解：

![postman2](https://github.com/tete1987/picture_resource/blob/master/postman2.png)

① form-date：等价于http请求中的multipart/form-data,它会将表单的数据处理为一条消息，以标签为单元，用分隔符分开。既可以上传键值对，也可以上传文件。当上传的字段是文件时，会有Content-Type来表名文件类型；content-disposition，用来说明字段的一些信息。

② x-www-form-urlencoded：等价于http请求中的application/x-www-from-urlencoded,会将表单内的数据转换为键值对

③ raw：可以上传任意格式的文本，可以上传text、json、xml、html等。

④ binary：只可以上传二进制数据，通常用来上传文件，由于没有键值，所以，一次只能上传一个文件。

## （二）发送请求
1.发送get请求

1）填写请求方式：get

2）填写请求URL

3）填写请求参数

示例：
![postman3](https://github.com/tete1987/picture_resource/blob/master/postman3.png)

2.发送Post请求

Post请求可以发送Key-value，json，，file等格式的数据

案例：
1）请求URL：https://httpbin.testing-studio.com/post

2）请求方式：Post

![postman4](https://github.com/tete1987/picture_resource/blob/master/postman4.png)



## （三）断言
Tests主要用来做断言，比如要测试返回结果是否含有某一字符串，就可以用Tests

1）断言，就是结果和预期对比

2）如果一致，用例通过，返回Pass

3）如果不一致，用例失败，返回Fail


postman预置的常用断言：

1）Status Code：Code is 200——判断响应状态码为200

![postman5](https://github.com/tete1987/picture_resource/blob/master/postman5.png)


"Status code is 200"：此处的文字信息可以任意定义（填写）

2）Response body：Cantains String——返回的响应值包含某字符串

![postman6](https://github.com/tete1987/picture_resource/blob/master/postman6.png)

"Body matches string"：此处的文字信息可以任意定义（填写），只要能够方便我们自己辨别是什么意思就可以了

"string_you_want_to_search"：此处填写的时我们需要判断的字段的值

3）Response body:Json value check——判断某个返回值是否正确

![postman7](https://github.com/tete1987/picture_resource/blob/master/postman7.png)


"Your test name"中的文字信息可任意定义，在.eq()的值中输入需要判断的值。

4）Response body：Content-type header check——判断头信息

![postman8](https://github.com/tete1987/picture_resource/blob/master/postman8.png)


5）Response time is less than 200ms——判断响应时间少于多少毫秒

![postman8-1](https://github.com/tete1987/picture_resource/blob/master/postman8-1.png)

（四）变量
1.环境变量与全局变量
1）增加环境变量：

![postman9](https://github.com/tete1987/picture_resource/blob/master/postman9.png)

2.变量引用法：{{variableName}}

先选择创建的变量环境，然后使用{{}} 将变量名括起来。

![postman10](https://github.com/tete1987/picture_resource/blob/master/postman10.png)

3.有时也需要清除环境变量，进行重置，可在脚本中进行添加，如下：

![postman11](https://github.com/tete1987/picture_resource/blob/master/postman11.png)

重置环境变量之后可以进行查看，如图：

![postman12](https://github.com/tete1987/picture_resource/blob/master/postman12.png)

4.添加Cookie
1）cookie可以用来鉴权
2）Postman可以自动保存Cookie信息

![postman13](https://github.com/tete1987/picture_resource/blob/master/postman13.png)

## （五）参数传递

1.获取需要的值

2.将获取到的值设置为环境变量

（在Tests中编写）
```
var jsonData = pm.response.json();
var token=jsonData.json.token;
pm.environment.set("token",token);
```

3.在需要验证的接口中引用环境变量中保存的值


![postman14](https://github.com/tete1987/picture_resource/blob/master/postman14.png)

![postman15](https://github.com/tete1987/picture_resource/blob/master/postman15.png)

## （六）用例集
1.选择环境变量
1）首先模拟一个post请求

![postman16](https://github.com/tete1987/picture_resource/blob/master/postman16.png)

2）增加断言：

![postman17](https://github.com/tete1987/picture_resource/blob/master/postman17.png)

3）将文件保存到一个用例集中


![postman18](https://github.com/tete1987/picture_resource/blob/master/postman18.png)


2.选择执行次数

![postman19](https://github.com/tete1987/picture_resource/blob/master/postman19.png)


3.选择测试数据

数据驱动：

1）json


![postman20](https://github.com/tete1987/picture_resource/blob/master/postman20.png)

2）csv

csv格式通过Excel表格进行转换即可。


3）在postman中选择数据文件：

先修改body中的内容，改为变量模式：
![postman21](https://github.com/tete1987/picture_resource/blob/master/postman21.png)

然后在执行用例时选择数据文件：

![postman22](https://github.com/tete1987/picture_resource/blob/master/postman22.png)

4.点击Run按钮即可开始执行
![postman23](https://github.com/tete1987/picture_resource/blob/master/postman23.png)

（七）代码导出
![postman24](https://github.com/tete1987/picture_resource/blob/master/postman24.png)

