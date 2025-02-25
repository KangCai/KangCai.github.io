---
layout: post
title: "【Overall】语言总括"
author: "Kang Cai"
header-img: "img/post-bg-dreamer.jpg"
header-mask: 0.4
tags:
  - Overall

---

## WEB 开发相关

**PHP 全称是 “PHP: Hypertext Preprocessor”**，递归命名法。

**HTML 全称是 “Hypertext Markup Language”**，定义网页的内容。

**CSS 全称是 “Cascading Style Sheet”**，规定网页的布局。

**JavaScript，对网页行为进行编程**。

PHP 是动态生成 HTML 的语言，这一点从名称上也能看出。

**CGI 全称是 “Common Gateway Interface”，即公共网关接口**，可以用任何一种语言编写，只要这种语言具有标准输入、输出和环境变量。CGI 的作用是能够让浏览者与服务器进行交互。对于Python程序来说，每个请求都会启动一个新的Python解释器，这需要一些时间，因而整个服务只能用于低负载的情况。CGI 的优势在于它很简单，编写一个使用 CGI 的 Python 程序只需要大概3行代码。这种简单是有代价的，就是它对于开发者的支持不够。现在已经不再推荐编写 CGI 程序了。使用 WSGI 可以编写兼容 CGI 的程序，并作为 CGI 程序运行。

**FastCGI 和 SCGI 尝试通过另外一种方式解决 CGI 的性能问题**。它不再将解释器嵌入到 Web 服务器中，而是创建长时间运行的后台程序。Web 服务器中的一个模块使得其可以与后台进程通信。由于后台进程独立于服务器，因此它可以用任意语言进行编写，包括 Python。该语言只需要一个处理与 Web 服务器通信的库。FastCGi 和 SCGI的区别很小，因为 SCGI 本质上只是一个更简单的 FastCGI(simpler FastCGI)。支持SCGI的Web服务器不多，因此大多数人都使用FastCGI，现在 FastCGI 不再被直接使用了，它只用于部署 WSGI 应用程序。Apache、lighttpd、nginx 三个 web 服务器都支持 FastCGI。

**三大 web 服务器：Apache、lighttpd、nginx**。

|  | Apache | Nginx | Lighttpd |
| :-----------:| :----------: |:----------: | :----------: | 
| proxy代理 | **非常好** | **非常好** | 一般 |
| Rewriter | 好 | **非常好** | 一般 |
| Fastcgi | 不好 | 好 | **非常好** |
| 热部署 | 不支持 | **支持** | 不支持 |
| 稳定性 | 好 | **非常好** | 不好 |
| 安全性 | **好** | 一般 | 一般 |
| 技术支持 | **非常好** | 很少 | 一般 |
| 静态文件处理 | 一般 | **非常好** | 好 |
| 优点 | 1. Apache的兼容性和稳定性都是非常强；2. Apache 的模块比 Nginx/Lighttpd丰富；3. Apache在处理动态请求比Nginx/Lighttpd更有优势 | 1. 虚机的配置处理方式比 apache 直观，比Apache轻量；2. 轻量级web服务器，cpu占用低，效能好，模块丰富，对fastcgi支持非常好；3. 支持高并发，和Nginx差不多，比apache性能高很多 | 1. 轻量级，比 apache 占用更少的内存及资源；2. 抗并发，nginx 处理请求是异步非阻塞的，而apache 则是阻塞型的，在高并发下nginx 能保持低资源低消耗高性能；3. 高度模块化的设计，编写模块相对简单；4. 有Lighttpd的性能，且更稳定，没有其内存泄露问题；5. 处理静态文件，索引文件以及自动索引，打开文件描述符缓冲。|
| 缺点 | 1. 属于重量级web服务器，软件包的大小上比较大，软件的耦合度大；2. 在速度、性能不及其他轻量级web服务器，并且消费内存较高，消耗的cpu等服务器资源比较大 | 稳定性没有 Apache 和 Nginx 高，bug 相对较多 | nginx 处理动态请求是鸡肋，不如 Apache | 

建议方案：Apache 后台服务器（主要处理php及一些动态请求）；Nginx 前端服务器（高并发请求、静态资源、负载均衡、反向代理和前端Cache等）。

**Web 结构概况**

**Web服务器** 即用来接受客户端请求，建立连接，转发响应的程序。至于转发的内容是什么，交由 **Web框架** 来处理，即处理这些业务逻辑。Django 就是这个 web框架，还有一个和 Django 比肩的框架是 Flask。Web 结构概况如下所示，

<img src="https://kangcai.github.io/img/in-post/post-web/web-1.jpg"/>

可参考资料如下：

* [uWSGI+django+nginx的工作原理流程：https://blog.csdn.net/c465869935/article/details/53242126](https://blog.csdn.net/c465869935/article/details/53242126)
* [uwsgi 效率远超 fastcgi：https://www.cnblogs.com/QLeelulu/archive/2011/03/02/1969289.html](https://www.cnblogs.com/QLeelulu/archive/2011/03/02/1969289.html)
* [Django 与 Tomcat 的关系：https://www.imooc.com/wenda/detail/461888](https://www.imooc.com/wenda/detail/461888)
* [Web 架构图：https://www.zhihu.com/question/348410145/answer/857812199](https://www.zhihu.com/question/348410145/answer/857812199)