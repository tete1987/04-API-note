# 07-Api接口测试
## 一、接口测试价值与体系
### 1.移动互联网公司技术架构

![接口1](https://github.com/tete1987/picture_resource/blob/master/%E6%8E%A5%E5%8F%A31.png)


![接口2](https://github.com/tete1987/picture_resource/blob/master/%E6%8E%A5%E5%8F%A32.png)


### 2.接口测试的必要性
![接口3](https://github.com/tete1987/picture_resource/blob/master/%E6%8E%A5%E5%8F%A33.png)

1）行业成熟方案

2）更早的发现问题

3）更快的质量反馈   

### 3.接口测试不能取代UI测试
1）接口测试虽然有很多优点，但是保证的是后端工程师的产出质量，不能解决移动端的质量。

2）大前端工程师的产出质量只能通过UI测试保证。


3）大前端研发团队：
- 前端工程师：HTML 、JS、CSS、Vue、React
- 移动开发工程师：Java、Kotlin
- 跨前端研发工程师：React  Native  Flutter Weex

4）后端研发团队：spring boot


## 二、网络协议介绍

![网络协议1](https://github.com/tete1987/picture_resource/blob/master/%E7%BD%91%E7%BB%9C%E5%8D%8F%E8%AE%AE1.png)


### 1.TCP与UDP的区别
1）TCP：面向连接，错误重传，拥塞控制，适用于可靠性高的场景

2）UDP：不需要提前建立连接，实现简单，适用于实时性高的场景

![网络协议2](https://github.com/tete1987/picture_resource/blob/master/%E7%BD%91%E7%BB%9C%E5%8D%8F%E8%AE%AE2.png)

### 2.Restful 软件架构风格
1）Restful：Representational State Transfer

2）借助于http协议的基本请求方法代表资源的状态切换

3）post：新增或者更新

4）get：获取资源

5）put：更新资源

6）delete：删除资源

### 3.RPC协议
1）RPC协议：Remote Procedure Call，以本地代码调用的方式实现远程执行

2）Dubbo：
- Java上的高性能RPC协议，Apache开源项目，由阿里捐赠
- 底层应用层协议支持dubbo缺省tcp协议、http、hession、thrift、grpc

3）gRPC：
- 高性能通用RPC框架，基于Rrotocol Buffers
- PB是一个语音中立、平台中立的数据序列化框架。Google开源项目

4）Thrift：与gRPC类似的多语言RPC框架，Apache开源项目


## 三、接口协议分析
### 1.协议分析工具
1）网络监听：TcpDump + WireShark

2）代理Proxy：
- 推荐工具：手工测试Charles[全平台]、安全测试burpsuite[全平台 java]
- 自动化测试：mitmproxy
- 其他代理：fiddler[仅Windows]、AnyProxy[全平台]

3）协议客户端工具：curl、postman

2.tcpdump

1）参数：

-  -x： 十六进制展示
-  -w file：保存文件

2）表达式
- ip tcp：协议
- host：主机名
- port：80
- src：来源dst目的
- and or ()：逻辑表达式
- 
3）案例：抓取访问百度的数据包
`sudo tcpdump host www.baidu.com -w/tmp/tcpdump.log`

curl http://www.baidu.com

停止 tcpdump

使用wireshark 打开/tmp/tcpdump.log


示例：

1）在终端输入：(如果系统里没有tcpdump的话，还需要先安装，使用命令：yum install -y tcpdump)

`sudo tcpdump host www.baidu.com -w/tmp/tcpdump/log`

注：以上命令在linux服务器上执行之后未生成对应log文件，在网上找了另外一个命令，可正常生成：

`tcpdump -i ens33 -w test.pcap`

2）打开另一个终端输入： `curl http://www.baidu.com   `

3）回到第一个窗口停止tcpdump

4）使用wireShark打开log文件

![接口协议](https://github.com/tete1987/picture_resource/blob/master/%E6%8E%A5%E5%8F%A3%E5%8D%8F%E8%AE%AE.png)

#### 三次握手原理：

1）发送端首先发送一个带有SYN（synchronize）标志地数据包给接收方。

2）接收方接收后，回传一个带有SYN/ACK标志的数据包传递确认信息。

3）最后，发送方再回传一个带有ACK标志的数据包，表示’握手‘结束。

#### 四次挥手：

4）第一次挥手：Client发送一个FIN，用来关闭Client到Server的数据传送，Client进入FIN_WAIT_1状态。

5） 第二次挥手：Server收到FIN后，发送一个ACK给Client，确认序号为收到序号+1（与SYN相同，一个FIN占用一个序号），Server进入CLOSE_WAIT状态。

6）第三次挥手：Server发送一个FIN，用来关闭Server到Client的数据传送，Server进入LAST_ACK状态。

7）第四次挥手：Client收到FIN后，Client进入TIME_WAIT状态，接着发送一个ACK给Server，确认序号为收到序号+1，Server进入CLOSED状态，完成四次挥手


# 其他笔记链接
- [04 Postman详解](https://github.com/tete1987/07-API/blob/master/04%20Postman%E8%AF%A6%E8%A7%A3.md)
- [05 开发、测试工程师必备工具-curl](https://github.com/tete1987/07-API/blob/master/05%20%E5%BC%80%E5%8F%91%E3%80%81%E6%B5%8B%E8%AF%95%E5%B7%A5%E7%A8%8B%E5%B8%88%E5%BF%85%E5%A4%87%E5%B7%A5%E5%85%B7-curl.md)
- [06 开发测试工程师必备工具charles](https://github.com/tete1987/07-API/blob/master/06%20%E5%BC%80%E5%8F%91%E6%B5%8B%E8%AF%95%E5%B7%A5%E7%A8%8B%E5%B8%88%E5%BF%85%E5%A4%87%E5%B7%A5%E5%85%B7charles.md)
- [07 Http协议讲解](https://github.com/tete1987/07-API/blob/master/07%20Http%E5%8D%8F%E8%AE%AE%E8%AE%B2%E8%A7%A3.md)
- [08 Get 与Post的区别](https://github.com/tete1987/07-API/blob/master/08%20Get%20%E4%B8%8EPost%E7%9A%84%E5%8C%BA%E5%88%AB.md)
- [09 Session Cookie Token区别](https://github.com/tete1987/07-API/blob/master/09%20Session%20Cookie%20Token%E5%8C%BA%E5%88%AB.md)
- [10 雪球APP抓包与mock实战1](https://github.com/tete1987/07-API/blob/master/10%20%E9%9B%AA%E7%90%83APP%E6%8A%93%E5%8C%85%E4%B8%8Emock%E5%AE%9E%E6%88%981.md)
