# 五、开发、测试工程师必备工具 curl
## 1.Http协议组成 

1）target：url protocol host port

2）request：
- request：get  post put delete head
- header：host  cookie user-agent
- get query
- post body：json xml form

3）response：
- status line
- header
- body

2.copy as curl 功能

1）作用：
- 把浏览器发送的请求真是的还原出来
- 附带了认证信息，所以可以脱离浏览器执行
- 可以方便开发者重放请求、修改参数调试，编写脚本

2）客户端模拟请求工具介绍：
- nc：tcp/udp 协议发送
- curl：最常用的http请求工具
- postman：综合性的http协议测试工具
- 代理工具、IDE工具、浏览器插件工具

3）curl常见用法
- url=http://www.baidu.com
- get 请求：curl $url
- post 请求 ：curl -d 'xxx' $url
- Proxy 使用：curl -x 'http://127.0.0.1:8080' $url

4）重要参数
- -H：“Content-type：application/json” 消息投设置
- -u：username：password 用户认证
- -d：要发送的post数据 @file 表示来自于文件
- --data-urlencode ‘page_size=50’ 对内容进行url编码
- -G：把data数据当成get请求的参数发送，长与 --data-urlencoded结合使用
- -o：写文件
- -x：代理http代理  socks5 代理
- -v：verbose 打印更详细日志  -s关闭一些提示输出

5）更多示例介绍：
https://home.testing-studio.com/t/topic/1065

![curl](https://github.com/tete1987/picture_resource/blob/master/curl.png)


