---
title: 用R来给微博添把火
date: '2011-08-05T00:31:26+00:00'
author: 李舰
categories:
  - 数据分析
  - 数据挖掘与机器学习
  - 统计软件
  - 软件应用
tags:
  - RCurl
  - ROAuth
  - Rweibo
  - 微博
  - 社交网络
slug: fire-weibo-with-r
---

[<img class="aligncenter size-medium wp-image-4234" title="Rweibo配图" src="https://cos.name/wp-content/uploads/2011/09/Rweibo-300x300.png" alt="" width="300" height="300" srcset="https://cos.name/wp-content/uploads/2011/09/Rweibo-300x300.png 300w, https://cos.name/wp-content/uploads/2011/09/Rweibo-150x150.png 150w, https://cos.name/wp-content/uploads/2011/09/Rweibo-218x218.png 218w, https://cos.name/wp-content/uploads/2011/09/Rweibo-73x73.png 73w, https://cos.name/wp-content/uploads/2011/09/Rweibo-40x40.png 40w, https://cos.name/wp-content/uploads/2011/09/Rweibo.png 500w" sizes="(max-width: 300px) 100vw, 300px" />](https://cos.name/wp-content/uploads/2011/09/Rweibo.png)

近两年来微博这东西越来越火了，已经逐渐成了最主流的网络舆论平台。对于最近的网络热点问题大家一定是深有体会，作为统计门人，肯定很多人技痒不已，希望能进一步地探究很多事情背后的秘密……

好在几个主流的微博平台都提供了API，各种语言的SDK应运而生，而真正的分析利器R的SDK一直没有，这里不卖关子了，直接发布一个R的SDK，参见：<a href="http://jliblog.com/app/rweibo" target="_blank">Rweibo中文主页</a>。

本项目在R-Forge上开发（<https://r-forge.r-project.org/projects/rweibo/>），最新的信息发布在Rweibo中文主页上。目前的版本全部基于新浪微博，毕竟是现在最火的微博，其实几个微博的API平台大同小异，和twitter的也类似，都来自于同样的开源平台，略作改动也能支持腾讯微博等。本文就只拿新浪微博举例。

CRAN上有一个twitteR包，之前普通权限还可以用的时候有些接口可以和新浪的API通用，新浪废掉普通权限只留OAuth之后，我就放弃了twitteR，开始开发Rweibo（当前版本的twitteR已经可以支持OAuth，不过很多接口的细节和新浪微博还是不一样）。

在这里，我先介绍一下授权机制以及OAuth，这个搞定后整个微博的API就仅仅只是传一下参数调用GET和POST方法而已。最早的微博开放平台的授权方式是普通授权，通过HTTP的头信息来传递用户的信息，这种方式不是很安全，在非HTTPS的情况下密码可能会被窃听，对于开发者和使用者来说都是比较危险的。后来新浪就直接停用了这种方式，采用目前流行的OAuth。

OAuth看上去很玄乎，其实道理非常简单。拿微博开放平台来说，开发者希望能开发一个应用，让不同的用户使用，每个用户都有自己的微博帐号信息，他们不希望在使用的过程中被开发者知道，同时开发者的这个应用的帐号密码也不希望被别的用户知道，不然就会被同行拿去乱来。这样一来，就需要一种授权机制，能够使得开发者和用户都信得过，就好象在淘宝买东西一样，买家和卖家都基于一个可信的第三方平台。对于新浪微博来说，双方都信任新浪，只要能确认所处的网站是真的新浪微博，就不会有问题。先是开发者将自己的App Key和App Secret发送到一个请求地址，新浪微博验证无误后，返回请求的Token，其实相当于是加密过的开发者信息，将这个信息发送到授权地址，可以完成用户的授权。用户在授权的页面可以输入自己的微博帐号，这些信息只有新浪知道，然后会返回一个验证码，用户输入这个验证码之后进行再次确认。开发者将之前自己的Token信息以及用户的这个验证码一起发送到一个访问地址，经过确认后，新浪微博觉得双方都是可信的，而且彼此也都不知道对方的信息，就会返回一个访问的Token以及密码，这就好比是一把钥匙，开发者只要存着这把钥匙，下次如果再对该用户做某些操作时就不需要再征求他的同意了，除非用户主动废除这把钥匙。以上的过程就是OAuth授权的过程。

我最开始是利用JAVA版本的OAuth库，通过rJava实现，后来CRAN上的ROAuth成熟之后又改用ROAuth，在twitte上使用没问题，在新浪微博上调用POST时会有问题，而且对于中文的POST，新浪的开放平台需要编码两次，因此需要对这个包进行改写。当前版本的Rweibo已经不再依赖于ROAuth，直接使用RCurl实现整个授权过程，但是仍然借鉴了大部分的ROAuth包的内容，在这里对作者表示感谢。

安装Rweibo可以参见<a href="http://jliblog.com/app/rweibo" target="_blank">Rweibo中文主页</a>，里面有详细的介绍。使用时首先需要有一个微博帐号，点击“应用”，选定“微博开放平台”，在弹出页面选择“我是开发者”，然后创建一个普通应用，填好基本信息之后在应用的详情中填上相应的内容，就可以成功创建一个新的应用，将会得到一个App Key和App Secret，在Rweibo中使用registerApp函数，输入这两个信息以及该应用的名称（自己随便起个英文名字即可，不一定要与新浪应用的名字相同），就可以在R中注册该应用的信息。

利用createOAuth函数可以创建一个OAuth对象，如果是第一次使用，将会自动进行授权。比方说我注册了一个应用叫做test，我需要授权给我的微博帐号lijiao001或者我的马甲Rweibo，那么将会在R的界面中完成一个授权的交互过程，如果我用lijianoo1的帐号来操作，那么授权成功后，就可以调用各类函数读取这个帐号的信息或者用该帐号来发微博。一个简单的操作过程如下所示：

<pre class="brush: r">registerApp("GDdmIQH6jh", "MCD8BKwGdgPHv", app_name = "test")  # 在R中注册新的应用
roauth &lt;- createOAuth("test", "lijian001")  # 创建OAuth对象
timeline.Friends(roauth, list(count = 5))  # 获取好友及自己的前5条最新微博
timeline.CommentsList(roauth, list(id = 14762313082))  # 获取某条微博的评论列表
timeline.Comments(roauth, list(count = 5))  # 获取自己发送及收到的评论
timeline.Repost(roauth, list(id = 14761105585, count = 5))  # 获取某ID微博的转发情况
timeline.Mentions(roauth, list(count = 5))  # 获取@了当前用户的微博列表
timeline.User(roauth, list(screen_name = "rweibo", count = 5))  # 获取某用户的信息
access.update(roauth, list(status = "hello world"))  # 发一条微博
search.Content(roauth, list(q = "Rweibo"))  # 根据关键词搜索微博内容</pre>

目前版本的Rweibo实现了所有的timeline接口以及搜索、查询用户等接口，利用这些接口已经可以取到大部分能够用来分析的信息了。至于其他一些操作的接口，将会在后续的版本中实现。大家有什么建议也可以提给我，我将会在后续的版本中修改。

另外值得注意的是，我们申请的应用都是最低权限的，因为新浪目前对接口访问权限控制得比较严，只有成为合作开发者才能有很大的权限，而这些主要都是针对应用的需求而不是分析的需求。普通的权限一小时只能访问150次，其中发微博的操作只能在30次以内。对于一些操作，每次取出的信息条目也会有限制，20条到200条不等。没办法对某个关键词一次把所有的东西搜索出来或者将某条微博的转发信息一次抓取出来。但是这些难不倒我们，微博API是基于轮询的协议，两分钟左右取一次足矣，对于要分析的内容，我们完全可以设置一个任务，每隔两分钟取一下增量，时间一长就会得到我们想要的大量的数据了。

至于这些内容可以如何进行分析，就需要大家的聪明才智了。我最近想做的一件事情就是研究一下微博的转发规律。很多热点事件通常都会有几条转得极热的微博，如果能够得到转发的规律，就像传染病的规律一样，找到一些关键的节点，对于我们研究微博舆情是非常有用的。

&nbsp;

&nbsp;
