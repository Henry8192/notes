# 2022 Intern Prep Notes

## TikTok
[TikTok 测试开发工程师面经](https://www.jianshu.com/p/350734131a70)
[大佬整理的面试知识](https://hit-alibaba.github.io/interview/basic/network/TCP.html)

### 1. HTTP VS HTTPS
**HTTP** (Hyper Text Transfer Protocol): 80端口，明文传输，无连接无状态
- 很多运营商之前在用户浏览网页的时候还会劫持网页夹带私货放广告（比如中国联不通，吃相真的难看)
- HTTP的包你甚至直接用burpsuite抓都可以

**HTTPS** (Hyper Text Transfer Protocol over Secure Socket Layer): 443端口，协议其实早就升级成TLS协议了，但是还是很多人习惯之前的SSL名字所以（）。TLS层存在于HTTP层与TCP层之间，负责加密数据。

**HTTP** 请求报文
三部分：状态行、请求头、消息主体
```html
<method> <request-URL> <version>
<headers>

<entity-body>
```
交互方法: **GET POST PUT DELETE**