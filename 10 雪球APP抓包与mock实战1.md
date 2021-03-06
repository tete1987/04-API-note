# 十、雪球APP抓包与mock实战1
## （一）接口抓包工具
1.忘了嗅探工具：tcpdump，wireshark

2.代理工具：fiddler，Charles，anyproxy，burpsuite，mitmproxy

3.分析工具：curl，postman，chromeDevtool

## （二）网络模型
![网络协议1](https://github.com/tete1987/picture_resource/blob/master/%E7%BD%91%E7%BB%9C%E5%8D%8F%E8%AE%AE1.png)

1.网络模型：

1）网络接口层：使用什么网卡，是无线网卡还是虚拟网卡

2）网络层：使用什么路由协议来转发数据包，ip

3）传输层：使用什么协议保障传输质量，tcp/udp

4）应用层：将用户的操作通过应用程序转换为服务，http

## （三）Charles的基本使用

1.设置http代理端口与socks代理端口，“Proxy——Proxy Setting”

![Charles01](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/Charles01.png)

2.在网络中也同样设置代理端口：

![Charles02](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/Charles02.png)

![Charles03](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/Charles03.png)

![Charles04](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/Charles04.png)


3.Charles面板功能：

1）File功能：主要以保存、导出、导出session功能为主，有多个session时会有多个窗口，可相互做比较使用。

2）Edit功能：主要是复制、粘贴、查找等功能。

3）View功能：有几个用着比较方便的功能。

① View Request As 和View Response As

- 两个功能主要是将接口的信息保存成各种类型的文件，以便在其他工具中进行分析。

②Highlight Rules功能：主要是将关注的接口以其他颜色标注出来，比较醒目。
![Charles05](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/Charles05.png)

③ Focused Hosts功能：将关注的接口以分类显示出来，其他不关注的接口都显示在“Other Hosts”中。

![Charles06](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/Charles06.png)

④Viewer Mappings：可设置一些跨语言开发时用到的规则等。


![Charles07](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/Charles07.png)


Proxy 菜单包含以下功能：
- Start/Stop Recording：开始/停止记录会话。
- Start/Stop Throttling：开始/停止节流。
- Enable/Disable Breakpoints：开启/关闭断点模式。
- Recording Settings：记录会话设置。
- Throttle Settings：节流设置。
- Breakpoint Settings：断点设置。
- Reverse Proxies Settings：反向代理设置。
- Port Forwarding Settings：端口转发。
- Windows Proxy：记录计算机上的所有请求。
- Proxy Settings：代理设置。
- SSL Proxying Settings：SSL 代理设置。
- Access Control Settings：访问控制设置。
- External Proxy Settings：外部代理设置。
- Web Interface Settings：Web 界面设置。

4.SSL的加密方式

1）对称秘钥算法：数据加密和解密时使用同样的密钥。
- 速度快：大量信息

![Charles08](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/Charles08.png)

2）非对称秘钥算法：数据加密和解密时使用不同的密钥。
- 速度慢：数字签名

![Charles09](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/Charles09.png)

3）仅验证server的ssl 握手


![Charles10](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/Charles010.png)


握手过程解析：

①发送支持的SSL版本号、加密算法、密钥交换算法、MAC算法等

②确定本次通信的SSL版本号和加密套件

③发送携带了公钥信息的数字证书

④版本号和加密套件协商结束。开始进行秘钥交换。

⑤验证SSL server的证书合法化后，利用证书公钥加密SSL client 随机生成的premaster secret并发送

⑥通知协商好的密钥和加密套件进行加密和MAC计算

⑦计算已交互的握手信息（除Change Cipher Spec消息全部已交互的信息）的Hash值，利用协商好的密钥和加密套件处理Hash值（计算并加入MAC值、加密等）

⑧通知SSL client 将采用协商好的密钥和加密套件进行加密和MAC计算

⑨计算已交互的握手消息的Hash值，利用协商好的密钥和加密套件处理Hash值（计算并加入MAC值、加密等）。并通过Finished消息发送给SSL client。SSL client利用相同的方法计算已交互的握手消息的Hash 值，并与Finished消息的解密结果比较，假设二者相同，且MAC值验证成功，则证密钥和加密套件协商成功。

4）Charles工作原理：

![Charles11](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/Charles011.png)
