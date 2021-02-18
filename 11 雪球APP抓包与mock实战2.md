# 十一.雪球APP抓包与mock实战2
## （一）Charles Socks
1.Socks：防火墙安全会话转换协议 （Socks: Protocol for sessions traversal across firewall securely） SOCKS协议提供一个框架，为在 TCP和UDP域中的客户机/服务器应用程序能更方便安全地使用网络防火墙所提供的服务。协议工作在OSI参考模型的第5层(会话层)，使用TCP协议传输数据，因而不提供如传递 ICMP信息之类的网络层网关服务。

![mock1](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock1.png)


2.socket：只是一个抽象接口，不是协议。
socket 的原意是“插座”，在计算机通信领域，socket 被翻译为“套接字”，它是计算机之间进行通信的一种约定或一种方式。通过 socket 这种约定，一台计算机可以接收其他计算机的数据，也可以向其他计算机发送数据。

我们把插头插到插座上就能从电网获得电力供应，同样，为了与远程计算机进行数据传输，需要连接到因特网，而 socket 就是用来连接到因特网的工具。

![mock2](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock2.png)


3.WebSocket：
WebSocket 协议在2008年诞生，2011年成为国际标准。现在所有浏览器都已经支持了。WebSocket 的最大特点就是，服务器可以主动向客户端推送信息，客户端也可以主动向服务器发送信息，是真正的双向平等对话。
HTTP 有 1.1 和 1.0 之说，也就是所谓的 keep-alive ，把多个 HTTP 请求合并为一个，但是 Websocket 其实是一个新协议，跟 HTTP 协议基本没有关系，只是为了兼容现有浏览器，所以在握手阶段使用了 HTTP 。

![mock3](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock3.png)

WebSocket 的其他特点：
- 建立在 TCP 协议之上，服务器端的实现比较容易。
- 与 HTTP 协议有着良好的兼容性。默认端口也是80和443，并且握手阶段采用 HTTP 协议，因此握手时不容易屏蔽，能通过各种 HTTP 代理服务器。
- 数据格式比较轻量，性能开销小，通信高效。
- 可以发送文本，也可以发送二进制数据。
- 没有同源限制，客户端可以与任意服务器通信。
- 协议标识符是ws（如果加密，则为wss），服务器网址就是 URL。 

4.总结：
- WebSocket是一种协议，应用层的协议。可以兼容Http协议。
- Socks代理是一种技术。
- Socket是抽象接口。

## （二）Charles map
1.map local

![mock4](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock4.png)

1）URL解析：

例：https://movie.douban.com/subject/26342391/?from=showing
- https： 使用的协议是https
- movie.douban.com：主机的地址（DNS域名解析）
- subject/26342391：目录地址
- ?from=showing：参数是from，值：showing
- 端口：http的默认端口是80，https的默认端口是443

2）在charls的 “Tools——Map Local”功能中进行设置

![mock5](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock5.png)

创建map1.json文件：

![mock6](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock6.png)

设置好的map local功能之后，页面就会显示创建的文件的内容。如图：

![mock7](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock7.png)

3）对map local 进行扩展：

①在本地文件新创建一个文件：token.json ，录入内容：

![mock8](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock8.png)

②在map local 中设置如下：

![mock9](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock9.png)

③使用curl 命令进行访问：
```
 curl https://movie.douban.com?get_token=aaaa -x 127.0.0.1:8888 -k -s
```

返回结果：

![mock10](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock10.png)


④再创建一个文件：sucess,json，内容如下：

![mock11](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock11.png)

④ 在map local中再设置一次，如图：

![mock12](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock12.png)

⑤ 再使用curl命令进行访问：
```
 curl https://movie.douban.com?token=adjkdjgladjkdjgl -x 127.0.0.1:8888 -k -s
```

结果：

![mock13](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock13.png)

以上步骤可以实现一个小型服务器。

2.map remote

把原本发给服务器1 的内容，发送给服务器2……或服务器n

![mock14](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock14.png)

1）Charles中设置方式：Tools——Map Remote

![mock15](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock15.png)

2） 使用curl命令进行访问：
```
curl https://huaban.com/ -x 127.0.0.1:8888 -k -s
```

结果如下：

![mock16](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock16.png)


3.Charles 弱网功能：Proxy——Throttle Setting

![mock17](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock17.png)

4.Charles 的mirror 功能：Tools——Mirror Settings 功能

![mock18](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock18.png)

该功能可以将Charles中测试的接口保存到本地，生成一个二进制文件。

![mock19](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock19.png)

可以配合使用jq命令进行查看，如图：

![mock20](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock20.png)

jq的几种使用方式：

1）只查看数据中包含的某一列表中嵌套的的第几个元素（字典）：

![mock21](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock21.png)

2）查看数据中包含的某一列表中嵌套的所有字典中的某一元素的值：

![mock22](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock22.png)

3）将数据中包含的某一列表中嵌套的所有字典中的某一元素的值重新组合成另一个新的字典：

![mock23](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock23.png)

4）继续增加value值

![mock24](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock24.png)

5）结合grep 进行筛选：

![mock25](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock25.png)

6）组成一个新的列表：

![mock26](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mock26.png)

