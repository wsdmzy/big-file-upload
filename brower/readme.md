# 从输入URL到页面展示，这中间发生了什么？越细越好
1. 多进程架构
2. IPC（Inter-Process Communication，进程间通信）

1. 注重细节
2. 从想当然到理所应当 v8 引擎以及浏览器架构
3. 全面考察前端是否具有完整计算机本科学习能力的代表题
  web开发  网络  操作系统  
4. 如何规范的回答这道题  分水岭
  有条理， 进程  是主脉络  

动手demo  
1. 浏览器  proxy  通过浏览器来代理我们访问网页的
  可以当搜索框来用  默认的搜索引擎
  url
  juejin.im  补全为 https://juejin.im/  用户体验做的很好  补全协议
2. 浏览器中 操作系统里的进程
  细节  像代码架构分层  流程细化
  web 访问 浏览器chrome 多进程的架构模式， 最流畅， 用更多的内存 比IE优秀
  打开一个页面 至少有4个进程  
  主进程 管家 chrome 浏览器
  子进程
    GPU进程  渲染进程  GPU加速  3d渲染  canvas  three.js  css  transform 3d
    NetWork Service
    标签页
  chrome 多进程架构带来现代浏览器的快速访问的体验  chrome就是代表
  - 浏览器主进程  并发
    启动浏览器  提供交互(输入url)  子进程管理(进程间通信 IPC)
    文件存储功能  文件缓存  cookie  localStorage。。。BOM Browser Object Model
  - 网络进程  提供下载功能
  - 渲染进程  html,css,js 图片  可交互的页面
  执行过程
    访问过程  问题回答清楚  执行流程  进程间的流程
    1. 浏览器进程就收到用户输入的URL 请求时  在主进程，IPC 将url交给网络进程
    2. 网络进程中发起真正的URL的请求， url请求是由c++模块 node -> c++
      2.1 request

      2.2 response
    3. 网络进程进程响应头数据，(头 + body)通知 渲染进程开始准备干活
      text/html test/json image/img 提前通知渲染？ 
      浏览器进程  提交导航信息(CommitNavigation) 消息到渲染进程
      网络协议 TCP HTTP 
      1. DNS解析 DNS服务器  Domain Name Server  domain -> ip 
    4. 渲染进程受到导航信息后，开始准备接受html 直接和网络进程建立数据通道
    5. 渲染进程会向浏览器进程发送"确认提交",准备好接受和解析页面数据
    6.  if/else  移除之前的页面   body到了 渲染进程渲染。页面的重绘和重排 提交 确定文档信息  完成

  并行执行
2. 发出请求？  
  是




以chrome浏览器为例
用户在浏览器中输入url， 补全协议 
首先要将url转为ip地址，先会查看本地缓存解析url，如果没有找到就会去DNS服务器里进行域名解析，然后将解析的ip地址返回
浏览器是多进程的，浏览器进程是主进程，浏览器进程接受到ip地址后，会通过ICP将ip地址交给网络进程
网络进程发起真正的请求，  
TCP建立连接  发送HTTP请求 ，然后服务器进行对应的处理，然后返回响应首部字段
接着网络进程收到了响应头数据，便解析响应头数据，并将数据转发给浏览器进程
浏览器进程接收到网络进程的响应头数据之后，发送 “提交导航(CommitNavigation)” 消息给渲染进程
渲染进程收到导航信息后，开始准备接受html 直接和网络进程建立数据通道
接着渲染进程会向浏览器进程发送"确认提交",准备好了接受和解析页面数据
浏览器进程接收到渲染进程 “提交文档” 的消息之后，然后判断是否移除之前的页面，然后渲染进程根据响应体渲染页面













看掘金面试相关技能点文章的列表  问自己问题  回答 搜 学习
思考！！  文章

