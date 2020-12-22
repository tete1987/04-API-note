# 九.Session Cookie Token区别
## 1.session与cookie 的区别
1）cookie：浏览器接收服务器的Set-Cookie指令，并把cookie保存到电脑上，每个网站保存的cookie只作用于自己的网站。

2）seesion：数据存储到服务端，只把关联数据的一个加密串放到cookie中标记。

## 2.token应用场景

1）凭借认证信息获取token，或者通过后台配置好token

2）在相关请求中使用token，多数是以query参数的形态提供

- 参考OAuth认证、企业微信、微信、GitHub、gitlab等相关认证

## 3.session与token的区别
1）token是一个用户请求时附带的请求字段，用于验证身份与权限

2）seseion可以基于cookie，也可以基于query参数，用于关联用户相关数据

3）跨端应用的时候，比如android原生系统不支持cookie
- 需要用token识别用户
- 需要用把sessionid保存到http请求中的header 或者query 字段中

