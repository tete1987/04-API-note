# 六、开发测试工程师必备工具charles
## （一）常用代理工具
- 代理工具：Charles  burpsuit  fiddler  mitmproxy
- 高性能代理服务器：squid  dante
- 反向代理：Nginx
- 流量转发与复制：em-proxy  gor iptable  Nginx
- socks5 代理：ssh -d  参数
## （二）优秀代理工具必备特性
- 代理功能：http/https  socks5
- 请求模拟工具：拼装请求、重放请求、重复请求
- 网络环境模拟：限速、超时、返回异常
- mock：请求修改、响应修改
- fake：用测试环境替代真实环境
## （三）推荐工具
- Charles：开发/测试工程师必备
- mitmproxy：测试开发工程师必备
- zap：测试工程师安全测试工具
- burpsuite：黑客必备渗透测试工具
- fiddler：跨平台支持不好，不推荐
- postman：代理功能太弱，不推荐
## （四）http/https 抓包分析
1.配置代理

1）先关闭Proxy——WindowsProxy，不然会自动监听所有流量

![proxy1](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/proxy1.png)


2）配置一个监听端口
![proxy2](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/proxy2.png)

3）配置SSL，默认添加全部即可（即什么都不填写，直接确定）
![proxy3](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/proxy3.png)


4）在浏览器中安装SwitchyOmega插件（不错的代理工具）
![proxy4](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/proxy4.png)

5）增加Charles的
![proxy5](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/proxy5.png)


2.获取证书——PC端配置

1）点击 Help——SSL Proxing——Install Charles Root Certificate 进行安装
![proxy6](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/proxy6.png)

2）在弹出的窗口中点击“安装证书”
![proxy7](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/proxy7.png)

3）选择存储目录
![proxy8](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/proxy8.png)

3.获取证书——移动端端配置

1）打开移动设备的网络配置，选择修改（如果是模拟器，长按名称即可弹出修改窗口）
![proxy9](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/proxy9.png)

2）在“代理”中选择“手动”，并填写要配置的服务器名称（如果无法确定，可点击 Charles中的”Help——SSL Proxing——Install Charles Root Certificate On MObile Device or Remote Browser“进行查看提示信息）

![proxy10](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/proxy10.png)

3）上一步完成之后，在浏览器中输入“chls.pro/ssl”下载证书

![proxy11](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/proxy11.png)

4）下载完成之后，安装即可完成配置。Charles可对移动设备进行抓包。


## （五）mock实践——数据加倍演示
1.雪球股票展示测试

2.数据加倍演示

示例：
```bash
1）先找到对应的接口，将返回值复制出来进行修改（本次测试的接口是雪球app中的“最近浏览”页面中的内容，原内容只有3条数据）
#1.新建一个文件，将接口返回值内容复制进去
vim stock2

#2.赋值给一个变量
raw=$(cat stock2)
#3.将变量中的值进行翻倍，执行一次命令，翻一次倍（测试时已达到48条数据）
raw=$(echo "$raw"|jq '.data.items+=.data.items'|jq '.data.items_size+=.data.items_size')

#4.将翻倍的内容重定向到一个新的文件中
echo "$raw" > ./mock.json 

```
2）回到Charles ，在对应的接口中点击“Tools——Map Local”，新增一条记录

![proxy12](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/proxy12.png)

注：Path是接口的地址，复制下来即可。Local path是新的文件路径。


3）完成之后，在模拟器中进行刷新，原先的3条记录已变成48条，如图：
![proxy13](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/proxy13.png)

接口的返回值也已变更，如图：
![proxy14](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/proxy14.png)

3.使用总结
- rewrite：简单mock
- map local：复制mock
- map remote：整体测试环境
