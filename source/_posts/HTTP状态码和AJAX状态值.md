---
title: HTTP状态码和AJAX状态值hexo
date: 2018-11-29 15:01:52
toc: true
thumbnail: /blog/2018/11/29/HTTP状态码和AJAX状态值/http.jpg
categories: '笔记'
tags: 
	- js
	- 前端
---

>超文本传输协议（HTTP，HyperText Transfer Protocol)是互联网上应用最为广泛的一种网络协议。所有的WWW文件都必须遵守这个标准。设计HTTP最初的目的是为了提供一种发布和接收HTML页面的方法。1960年美国人Ted Nelson构思了一种通过计算机处理文本信息的方法，并称之为超文本（hypertext）,这成为了HTTP超文本传输协议标准架构的发展根基。Ted Nelson组织协调万维网协会（World Wide Web Consortium）和互联网工程工作小组（Internet Engineering Task Force ）共同合作研究，最终发布了一系列的RFC，其中著名的RFC 2616定义了HTTP 1.1。

<!-- more -->

## HTTP 超文本传输协议

>HTTP 是基于客户端/服务端（C/S）的架构模型，通过一个可靠的链接来交换信息，是一个无状态的请求/响应协议。
>&nbsp;
>一个HTTP "客户端"是一个应用程序（Web浏览器或其他任何客户端），通过连接到服务器达到向服务器发送一个或多个HTTP的请求的目的。
>一个HTTP "服务器"同样也是一个应用程序（通常是一个Web服务，如Apache Web服务器或IIS服务器等），通过接收客户端的请求并向客户端发送HTTP响应数据。
>&nbsp;
>HTTP 使用统一资源标识符（Uniform Resource Identifiers, URI）来传输数据和建立连接。
>HTTP 请求到服务器的请求消息包括以下格式：请求行（request line）、请求头部（header）、空行和请求数据四个部分组成。
>&nbsp;  
>HTTP1.0 定义了三种请求方法： `GET`, `POST` 和 `HEAD`方法。
>HTTP1.1 新增了五种请求方法： `OPTIONS`, `PUT`, `DELETE`, `TRACE` 和 `CONNECT` 方法。

---

## HTTP 请求方式

>|             请求方式            |                                                               请求中文说明                                                              |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| GET                             | 请求指定的页面信息，并返回实体主体。                                                                                                    |
| HEAD                            | 类似于`get`请求，只不过返回的响应中没有具体的内容，用于获取报头                                                                           |
| POST                            | 向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。`POST`请求可能会导致新的资源的建立和/或已有资源的修改。 |
| PUT                             | 从客户端向服务器传送的数据取代指定的文档的内容。                                                                                        |
| DELETE                          | 请求服务器删除指定的页面。                                                                                                              |
| CONNECT&nbsp;&nbsp;&nbsp;&nbsp; | HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。                                                                                |
| OPTIONS                         | 允许客户端查看服务器的性能。                                                                                                            |
| TRACE                           | 回显服务器收到的请求，主要用于测试或诊断。                                                                                              |

---

## AJAX 状态值 与 HTTP状态码

### AJAX状态值与状态码区别

>AJAX状态值是指，运行AJAX所经历过的几种状态，无论访问是否成功都将响应的步骤，可以理解成为AJAX运行步骤。如：正在发送，正在响应等，由AJAX对象与服务器交互时所得；使用`ajax.readyState`获得。

>AJAX状态码是指，无论AJAX访问是否成功，由HTTP协议根据所提交的信息，服务器所返回的HTTP头信息代码，该信息使用`ajax.status`所获得。

这就是我们在使用AJAX时为什么采用下面的方式判断所获得的信息是否正确的原因。
``` js
if( ajax.readyState == 4 && ajax.status == 200 ) {
	// do success
}
```

### AJAX状态值

>在《Pragmatic Ajax A Web 2.0 Primer 》
>&nbsp;
>>0: (Uninitialized) the send( ) method has not yet been invoked. 
>>1: (Loading) the send( ) method has been invoked, request in progress. 
>>2: (Loaded) the send( ) method has completed, entire response received.
>>3: (Interactive) the response is being parsed. 
>>4: (Completed) the response has been parsed, is ready for harvesting.
>&nbsp;
>>0 － （未初始化）还没有调用`send()`方法
>>1 － （载入）已调用`send()`方法，正在发送请求
>>2 － （载入完成）`send()`方法执行完成，已经接收到全部响应内容
>>3 － （交互）正在解析响应内容
>>4 － （完成）响应内容解析完成，可以在客户端调用了

### HTTP 状态码

>当浏览者访问一个网页时，浏览者的浏览器会向网页所在服务器发出请求。当浏览器接收并显示网页前，此网页所在的服务器会返回一个包含HTTP状态码的信息头（server header）用以响应浏览器的请求。
HTTP状态码的英文为HTTP Status Code。

>下面是常见的HTTP状态码：
>
>| 码值 |                描述               |
|------|-----------------------------------|
|  200 | 请求成功                          |
|  301 | 资源（网页等）被永久转移到其它URL |
|  404 | 请求的资源（网页等）不存在        |
|  500 | 内部服务器错误                    |

#### HTTP状态码分类

>HTTP状态码由三个十进制数字组成，第一个十进制数字定义了状态码的类型，后两个数字没有分类的作用。HTTP状态码共分为5种类型：
>
>| 分类 |                      描述                      |
|------|------------------------------------------------|
| 1**  | 信息，服务器收到请求，需要请求者继续执行操作   |
| 2**  | 成功，操作被成功接收并处理                     |
| 3**  | 重定向，需要进一步的操作以完成请求             |
| 4**  | 客户端错误，请求包含语法错误或无法完成请求     |
| 5**  | 服务器错误，服务器在处理请求的过程中发生了错误 |

---

#### HTTP状态码列表

>HTTP状态码列表:
>
>|          码值         |             英文名称            |                                                                             中文描述                                                                             |
|-----------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 100&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Continue&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;            | 继续。客户端应继续其请求                                                                                                                                         |
| 101                   | Switching Protocols             | 切换协议。服务器根据客户端的请求切换协议。只能切换到更高级的协议，例如，切换到HTTP的新版本协议                                                                   |
|                       |                                 |                                                                                                                                                                  |
| 200                   | OK                              | 请求成功。一般用于GET与POST请求                                                                                                                                  |
| 201                   | Created                         | 已创建。成功请求并创建了新的资源                                                                                                                                 |
| 202                   | Accepted                        | 已接受。已经接受请求，但未处理完成                                                                                                                               |
| 203                   | Non-Authoritative Information   | 非授权信息。请求成功。但返回的meta信息不在原始的服务器，而是一个副本                                                                                             |
| 204                   | No Content                      | 无内容。服务器成功处理，但未返回内容。在未更新网页的情况下，可确保浏览器继续显示当前文档                                                                         |
| 205                   | Reset Content                   | 重置内容。服务器处理成功，用户终端（例如：浏览器）应重置文档视图。可通过此返回码清除浏览器的表单域                                                               |
| 206                   | Partial Content                 | 部分内容。服务器成功处理了部分GET请求                                                                                                                            |
|                       |                                 |                                                                                                                                                                  |
| 300                   | Multiple Choices                | 多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于用户终端（例如：浏览器）选择                                                           |
| 301                   | Moved Permanently               | 永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替                                   |
| 302                   | Found                           | 临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI                                                                                               |
| 303                   | See Other                       | 查看其它地址。与301类似。使用GET和POST请求查看                                                                                                                   |
| 304                   | Not Modified                    | 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源 |
| 305                   | Use Proxy                       | 使用代理。所请求的资源必须通过代理访问                                                                                                                           |
| 306                   | Unused                          | 已经被废弃的HTTP状态码                                                                                                                                           |
| 307                   | Temporary Redirect              | 临时重定向。与302类似。使用GET请求重定向                                                                                                                         |
|                       |                                 |                                                                                                                                                                  |
| 400                   | Bad Request                     | 客户端请求的语法错误，服务器无法理解                                                                                                                             |
| 401                   | Unauthorized                    | 请求要求用户的身份认证                                                                                                                                           |
| 402                   | Payment Required                | 保留，将来使用                                                                                                                                                   |
| 403                   | Forbidden                       | 服务器理解请求客户端的请求，但是拒绝执行此请求                                                                                                                   |
| 404                   | Not Found                       | 服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面                                                     |
| 405                   | Method Not Allowed              | 客户端请求中的方法被禁止                                                                                                                                         |
| 406                   | Not Acceptable                  | 服务器无法根据客户端请求的内容特性完成请求                                                                                                                       |
| 407                   | Proxy Authentication Required   | 请求要求代理的身份认证，与401类似，但请求者应当使用代理进行授权                                                                                                  |
| 408                   | Request Time-out                | 服务器等待客户端发送的请求时间过长，超时                                                                                                                         |
| 409                   | Conflict                        | 服务器完成客户端的PUT请求是可能返回此代码，服务器处理请求时发生了冲突                                                                                            |
| 410                   | Gone                            | 客户端请求的资源已经不存在。410不同于404，如果资源以前有现在被永久删除了可使用410代码，网站设计人员可通过301代码指定资源的新位置                                 |
| 411                   | Length Required                 | 服务器无法处理客户端发送的不带Content-Length的请求信息                                                                                                           |
| 412                   | Precondition Failed             | 客户端请求信息的先决条件错误                                                                                                                                     |
| 413                   | Request Entity Too Large        | 由于请求的实体过大，服务器无法处理，因此拒绝请求。为防止客户端的连续请求，服务器可能会关闭连接。如果只是服务器暂时无法处理，则会包含一个Retry-After的响应信息    |
| 414                   | Request-URI Too Large           | 请求的URI过长（URI通常为网址），服务器无法处理                                                                                                                   |
| 415                   | Unsupported Media Type          | 服务器无法处理请求附带的媒体格式                                                                                                                                 |
| 416                   | Requested range not satisfiable | 客户端请求的范围无效                                                                                                                                             |
| 417                   | Expectation Failed              | 服务器无法满足Expect的请求头信息                                                                                                                                 |
|                       |                                 |                                                                                                                                                                  |
| 500                   | Internal Server Error           | 服务器内部错误，无法完成请求                                                                                                                                     |
| 501                   | Not Implemented                 | 服务器不支持请求的功能，无法完成请求                                                                                                                             |
| 502                   | Bad Gateway                     | 作为网关或者代理工作的服务器尝试执行请求时，从远程服务器接收到了一个无效的响应                                                                                   |
| 503                   | Service Unavailable             | 由于超载或系统维护，服务器暂时的无法处理客户端的请求。延时的长度可包含在服务器的Retry-After头信息中                                                              |
| 504                   | Gateway Time-out                | 充当网关或代理的服务器，未及时从远端服务器获取请求                                                                                                               |
| 505                   | HTTP Version not supported      | 服务器不支持请求的HTTP协议的版本，无法完成处理                                                                                                                   |
