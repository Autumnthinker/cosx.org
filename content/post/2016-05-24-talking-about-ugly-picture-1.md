---
title: 丑图百讲｜好看的统计图都是相似的，难看的统计图各有各的丑
date: '2016-05-24T10:46:18+00:00'
author: COS编辑部
categories:
  - 推荐文章
  - 统计之都
tags:
  - 数据可视化
  - 水妈
  - 统计图形
slug: talking-about-ugly-picture-1
---

**作者：**水妈

大家好，我是水妈，在大学工作，主要教统计学。今天代表狗熊会，发起一个新的系列，**丑图百讲**。这个系列不讲炫酷的、高大上的统计图，而是给大家分享如何画好**最基础的统计图**。

读者可能会问，为什么要分享统计画图？熊大说了，数据分析的第一步，是梳理业务目标，接下来才是分析数据。水妈认为，在分析数据环节，第一步是做描述分析。这里的描述分析，包括三个内容：一、明确行业背景和变量含义；二、用统计图、统计表以及各种统计指标对数据进行描述；三、适当的解读描述的结果，发现问题，支撑后续的建模。其中，第二个环节尤为重要，因为**统计图是最容易给人留下深刻印象的**。做好了，能给你的报告或者展示加分，帮助你发现数据当中的问题。做不好，那就是一场灾难。

读者可能又要问，最基础的统计图有什么好讲的啊。我看过太多学生的报告，学生看自己画的图，就像是看自己家孩子，越看越喜欢，殊不知别人早就受不了你在朋友圈天天晒娃娃了。大家不要觉得画最最基础的统计图这件事情非常简单容易，可谓不画不知道，一画吓一跳。真的自己动手去画，才知道自己画出来的图有多丑。<!--more-->

今天是这个系列的第一期，我们先开个头，我要概括性的讲讲，如何画好统计图。 总的来说，我看统计图，有四个标准：**准确、有效、简洁、美观！**这次的分享，从这四个方面谈一谈如何让大家画的统计图成为**实力派（准确****&****有效）+****偶像派（简洁&****美观）。**

**成为实力派，至少要做到“准确”+****“有效”。这事儿跟穿衣服挺像，为什么这么说呢？   ** 

首先说**“准确”**。这是对于初学者最基本的要求，**能够使用正确的统计图去描述不同类型的数据**。比如，对于离散型的变量（性别、职业等），可以画饼图或者柱状图；对于连续型的变量（年龄、工资等），可以画直方图或者箱线图；对于时间序列变量（GDP、CPI等），可以画折线图。**这就好比不同的季节，要穿不同的衣服**。春天穿风衣，冬天穿羽绒服。你非要冬天穿比基尼，这不是好不好看的问题，而是会被冻死。因此大家**在画图之前，要先弄清变量的类型，再去选择合适的统计图**。

然后说**“有效”**。什么叫做有效的描述，我举一个例子。现在我有两个变量，一个是性别，一个是年龄，我想比较男性和女性的年龄，选择什么样的统计图才好呢？大家可以先自己思考一下。我给大家展示一组我的学生画的图。[<img class="aligncenter size-full wp-image-12143" src="https://cos.name/wp-content/uploads/2016/05/pan_1-1.png" alt="pan_1" width="498" height="596" srcset="https://cos.name/wp-content/uploads/2016/05/pan_1-1.png 498w, https://cos.name/wp-content/uploads/2016/05/pan_1-1-251x300.png 251w, https://cos.name/wp-content/uploads/2016/05/pan_1-1-418x500.png 418w" sizes="(max-width: 498px) 100vw, 498px" />](https://cos.name/wp-content/uploads/2016/05/pan_1-1.png)[
  
](https://cos.name/wp-content/uploads/2016/05/pan_1-2.png) [
  
](https://cos.name/wp-content/uploads/2016/05/pan_1.png) 

学生的选择是对男女性分别画了两个直方图。我的评语是：看出来区别了，男性是绿色，女性是粉色！这虽然是句玩笑话，但我真的看不出明显的对比。你可能要问，年龄不是连续型变量么，你刚才不是说画直方图么？分组画直方图，只能够满足刚才说的“准确”，但却达不到“有效”。大家看我下面画的分组箱线图，无论在平均水平，还是波动程度上，都比分组直方图更加有效的体现了不同性别的年龄对比。所以，画图的时候，在满足了“准确”的前提下，我们要多动脑筋，如何能让统计图更加有效的展示你的数据。说白了，**“有效”这事儿，好比在不同场合穿不同的衣服。**上班时候穿职业装，毕业典礼的时候穿学士服。你非要在跑步的时候穿婚纱，虽然也能跑，但那能跑得快么！[<img class="aligncenter size-full wp-image-12131" src="https://cos.name/wp-content/uploads/2016/05/pan_2.png" alt="pan_2" width="592" height="591" srcset="https://cos.name/wp-content/uploads/2016/05/pan_2.png 592w, https://cos.name/wp-content/uploads/2016/05/pan_2-150x150.png 150w, https://cos.name/wp-content/uploads/2016/05/pan_2-300x300.png 300w, https://cos.name/wp-content/uploads/2016/05/pan_2-500x500.png 500w" sizes="(max-width: 592px) 100vw, 592px" />](https://cos.name/wp-content/uploads/2016/05/pan_2.png)

“准确”和“有效”，不是那么容易达到的。你得平时多画图，各种数据都摸索着画。就跟演员演戏似的，各种角色都演演，才有可能成为实力派。**下面再讲讲，如何让大家画的统计图成为偶像派。这事儿跟化妆挺像，包括“简洁”和“美观”这两点。**

先说说**“简洁”**。还是举一个例子。我想对年龄这个变量做统计图。下面还是这个学生画的图。你说这没什么问题啊，连续型变量，画直方图啊。然而我一下就被每个柱子底下的黑色线段吸引了注意力。学生告诉我，这叫轴须图。我心想这什么鬼啊。但是作为一个学了十几年统计的人，不能在学生面前露怯呀，我就淡定的说，你给我解释解释。结果学生就说不上来了。大家想象一下，如果这件事情发生在做展示的现场，就很悲剧，但凡有一个人提出这种问题，听众的注意力就集中在这个不必要的环节上面了。在画图阶段，过于技术的细节，如果一句话说不清，就不要展示。**这就好比你画了个妆，眼线唇膏都画的不错，最后你非得用马克笔把两条眉毛描的老粗，谁还能看到你的明媚双眸和樱桃小口啊，全都看你的眉毛了。[<img class="aligncenter size-full wp-image-12132" src="https://cos.name/wp-content/uploads/2016/05/pan_3.png" alt="pan_3" width="1132" height="663" srcset="https://cos.name/wp-content/uploads/2016/05/pan_3.png 1132w, https://cos.name/wp-content/uploads/2016/05/pan_3-300x176.png 300w, https://cos.name/wp-content/uploads/2016/05/pan_3-768x450.png 768w, https://cos.name/wp-content/uploads/2016/05/pan_3-500x293.png 500w" sizes="(max-width: 1132px) 100vw, 1132px" />](https://cos.name/wp-content/uploads/2016/05/pan_3.png)**

最后谈谈**“美观”**。说了半天，你要问，到底什么样的统计图在水妈心中是好看的啊。我展示三个在我心目中，非常美观的图。它们也同时满足准确、有效和简洁的标准。第一个是非常普通的饼图，统计的是电影《速度与激情7》里面，主演范迪塞尔开的车的品牌的分布，我从www.concavebt.cn这个网站上看到的。这个饼图干干净净，标注清楚，“饼”上还贴心的印了车的logo。第二个属于一种树图（tree map），来自谷歌的一份报告，我从一个时尚博主那里看到的。描述的是在谷歌上面搜索某种裙子的关键词当中，出现的各种质地的搜索频数的分布。这个图做的非常巧妙，每个格子直接用裙子的质地当作背景，格子的面积就代表搜索这种质地的占比，可以说是赏心悦目。第三个是我常玩的游戏里面出现的统计图，一个非常简单的柱状图。它的配色与游戏背景配合的天衣无缝，出现的恰到好处。**所以说，“美观”这事儿，考验的是你化妆的整体技术，以及对于细节的把握。浓妆淡抹总相宜，让人瞅着舒服就是你的本事。**

<table>
  <tr>
    <td width="234">
       <a href="https://cos.name/wp-content/uploads/2016/05/pan_4.png"><img class="aligncenter size-full wp-image-12133" src="https://cos.name/wp-content/uploads/2016/05/pan_4.png" alt="pan_4" width="489" height="470" srcset="https://cos.name/wp-content/uploads/2016/05/pan_4.png 489w, https://cos.name/wp-content/uploads/2016/05/pan_4-300x288.png 300w" sizes="(max-width: 489px) 100vw, 489px" /></a>
    </td>
    
    <td width="334">
       <a href="https://cos.name/wp-content/uploads/2016/05/pan_5.png"><img class="aligncenter size-full wp-image-12134" src="https://cos.name/wp-content/uploads/2016/05/pan_5.png" alt="pan_5" width="862" height="432" srcset="https://cos.name/wp-content/uploads/2016/05/pan_5.png 862w, https://cos.name/wp-content/uploads/2016/05/pan_5-300x150.png 300w, https://cos.name/wp-content/uploads/2016/05/pan_5-768x385.png 768w, https://cos.name/wp-content/uploads/2016/05/pan_5-500x251.png 500w" sizes="(max-width: 862px) 100vw, 862px" /></a>
    </td>
  </tr>
  
  <tr>
    <td colspan="2" width="568">
      <a href="https://cos.name/wp-content/uploads/2016/05/pan_6.png"><img class="aligncenter size-full wp-image-12135" src="https://cos.name/wp-content/uploads/2016/05/pan_6.png" alt="pan_6" width="413" height="278" srcset="https://cos.name/wp-content/uploads/2016/05/pan_6.png 413w, https://cos.name/wp-content/uploads/2016/05/pan_6-300x202.png 300w" sizes="(max-width: 413px) 100vw, 413px" /></a>
    </td>
  </tr>
</table>

总结一下今天的分享，想画好统计图，要做到四点。**头两点是准确****+****有效，先让你的统计图成为实力派。后面两点是简洁+****美观，在实力派的基础上，做一个偶像派**。希望大家多去发现美的统计图，欣赏美的统计图，画出美的统计图。谢谢大家！

原文请[戳这里](http://mp.weixin.qq.com/s?__biz=MzA5MjEyMTYwMg==&mid=2650236457&idx=1&sn=bc5e2211367afa950358cc67a7f38ce8&scene=4#wechat_redirect)。

p.s. 水妈在教学过程中，精心积累了一个丑图库，我会在丑图百讲这个系列，不断跟大家分享丑图库中的精品。敬请期待！

**水妈简介**

  * 毕业于北京大学光华管理学院商务统计系，女博士一枚
  * 师从王汉生教授，狗熊会熊孩子一只
  * 现任职于中央财经大学统计与数学学院，年轻讲师一个
  * 在理论研究方面，关注高维数据和社交网络数据，在JASA和Annals上均有发表
  * 在业界实践方面，关注车联网行业的数据分析

&nbsp;

如果您对我们的内容感兴趣，请关注微信公众号“狗熊会”，或扫描下面的二维码

[<img class="aligncenter size-full wp-image-12142" src="https://cos.name/wp-content/uploads/2016/05/gouxionghui.jpg" alt="gouxionghui" width="1280" height="1280" srcset="https://cos.name/wp-content/uploads/2016/05/gouxionghui.jpg 1280w, https://cos.name/wp-content/uploads/2016/05/gouxionghui-150x150.jpg 150w, https://cos.name/wp-content/uploads/2016/05/gouxionghui-300x300.jpg 300w, https://cos.name/wp-content/uploads/2016/05/gouxionghui-768x768.jpg 768w, https://cos.name/wp-content/uploads/2016/05/gouxionghui-500x500.jpg 500w" sizes="(max-width: 1280px) 100vw, 1280px" />](https://cos.name/wp-content/uploads/2016/05/gouxionghui.jpg)
