# 十二、接口测试工具——mitmproxy
## （一）工具安装
- pip install pipx
- pipx install mitmproxy
- https://docs.mitmproxy.org/stable/overview-installation

## （二）工具组成
- mitmproxy ->gives you an interactive TUI
- mitmdump ->gives you a plain and simple terminal output （核心工具）
- mitmweb ->gives you a browsr-based GUI (类似 chrome浏览器的F12)

## （三）mitmdump 使用
1.安装完成之后在命令行输入：mitmdump

![mitmproxy1](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mitmproxy1.png)

- 默认启动 8080端口。

如果需要修改对应的端口可使用：mitmdump -p 8888

![mitmproxy2](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mitmproxy2.png)

对应需要修改本机网络的代理端口：


![mitmproxy3](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mitmproxy3.png)

开始获取接口信息：

![mitmproxy4](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mitmproxy4.png)


2. 安装证书

在开启mitmdump的情况下，在浏览器中输入：mitm.it

![mitmproxy5](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mitmproxy5.png)

根据情况进行下载，下载完成之后，一步步安装。在安装时需要安装到“受信任的根证书颁发机构”中，如图：

![mitmproxy6](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mitmproxy6.png)

手机端同样也需要安装证书（在浏览器中输入 mitm.it）：

![mitmproxy7](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mitmproxy7.png)


3.录制文件

1）录制文件使用命令：mitmdump -p 8888 -w .\Desktop\tmp
- 将录制的文件保存下来。
2）回放录制的文件使用命令：mitmdump -p 8888 -nC .\Desktop\tmp
- -n ：不开启录制功能
- C：回放一个已录制的文件

其他的命令可以参考官方文档：https://docs.mitmproxy.org/stable/concepts-filters/

![mitmproxy8](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mitmproxy8.png)

4.内容过滤

1）过滤：mitmdump -nr tmp -w tmp2 "-s alibaba"

2）回放：mitmdump -nC tmp2


5.使用脚本，实现maplocal 功能

1）脚本内容可从官网进行复制：
```python
from mitmproxy import http


def request(flow: http.HTTPFlow) -> None:
    if flow.request.pretty_url == "https://www.baidu.com/":
        flow.response = http.HTTPResponse.make(
            200,  # (optional) status code
            b"Hello World",  # (optional) content
            {"Content-Type": "text/html"}  # (optional) headers

```

2）在pycharm中进行自行修改。修改完成之后在终端中进行执行：
```
mitmdump -p 8888 -s .\mitmproxy.py 
```

3）在网页中输入百度，可显示脚本内容：

![mitmproxy9](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mitmproxy9.png)


示例2（使用本地的文件，进行maplocal功能，像Charles那样的）：
脚本内容：
```python
from mitmproxy import http


def request(flow: http.HTTPFlow) -> None:
    if "get_token=aaaa" in flow.request.pretty_url:
        with open("C:/Users/Administrator/Desktop/token.json",encoding="utf-8") as f:

            flow.response = http.HTTPResponse.make(
                200,  # (optional) status code
                f.read(),  # (optional) content
                {"Content-Type": "application/json"}  # (optional) headers
            )
```

运行结果：

![mitmproxy10](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mitmproxy10.png)


6.实现mapresponse功能（与Charles的 mapremote功能相似）

官方文档：https://docs.mitmproxy.org/stable/addons-events/

1）编写脚本：
```python
import json

def response(flow):
    if "quote.json" in flow.request.pretty_url:
        data = json.loads(flow.response.content)
        data['data']['items'][0]['quote']['name'] = "tete"
        flow.response.text = json.dumps(data，indent=2)
        print(data)

```
注：loads 是反序列化函数。 indent是缩进。

2）执行：mitmdump -p 8888 -s .\mitmproxy.py 


结果：

![mitmproxy11](https://github.com/tete1987/picture_resource/blob/master/Http%E5%9B%BE/mitmproxy11.png)
