---
title: 从搜索序列文本看高端商务车
date: '2016-05-27T14:20:54+00:00'
author: COS编辑部
categories:
  - 统计之都
tags:
  - Logistic回归模型
  - 品牌忠诚度
  - 搜索引擎数据
  - 文本分析
slug: search-sequence-see-high-end-business-cars
---

朱雪宁(北京大学光华管理学院)               王汉生(北京大学光华管理学院)

摘要：本文对100万搜索引擎用户的13亿搜索序列文本进行探索分析，对高端车用户以及商学院人群做了描述对比，并针对用户搜索高端车品牌过程中的动态选择行为进行建模。首先，我们发现，在人群划分上，高端车用户和商学院用户表现出更加高端的属性，这主要表现在他们对生活、事业、学业上更卓越的追求。接下来，本文利用逻辑回归构建了忠诚模型，对用户在搜索过程中表现的忠诚和叛变行为进行了刻画，并对影响其忠诚行为的关键因素进行了逐一分析。根据模型的估计结果，我们发现，用户的搜索时间间隔、搜索关键词长度、搜索点击数等指标对用户忠诚行为有显著影响$^1$。最后，我们利用成本收益曲线对模型进行了评价，并得到了良好的效果。<!--more-->

#### ****一、********业务介绍****

##### ****（一）********中国汽车行业现状及高端乘用车市场****

汽车工业是我国国民经济的主导产业和支柱产业之一。自2001年中国加入世贸组织以来，我国私有车辆广泛普及，带来了汽车行业销售量连年增加。截止至2015年底，我国民用汽车保有量已达到16273万辆（如图 1所示）。近十年来，我国汽车销量由2004年的500万辆增加到2013年的2198万辆，增加了三倍有余（图 2$^2$）。另一方面，中国在世界汽车行业的地位日渐凸显，已成为全球车企的主要增长市场。据德勤公布的2014年中国汽车行业投资促进报告显示，截止至2013年，中国中国汽车产销量已连续五年稳居全球汽车产销量首位，约占全球总产销量的四分之一。以上产需数据表明，我国汽车产业蕴含着巨大的商业价值\[1\]\[10\]。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/808D.tmp_.png"><img class="aligncenter size-full wp-image-12155" src="https://cos.name/wp-content/uploads/2016/05/808D.tmp_.png" alt="808D.tmp" width="527" height="287" srcset="https://cos.name/wp-content/uploads/2016/05/808D.tmp_.png 527w, https://cos.name/wp-content/uploads/2016/05/808D.tmp_-300x163.png 300w, https://cos.name/wp-content/uploads/2016/05/808D.tmp_-500x272.png 500w" sizes="(max-width: 527px) 100vw, 527px" /></a>                    图1中国民用汽车保有量与年增长率时间序列图</pre>

另一方面，从销售结构上而言，相对于整体乘用车销量增幅，高端车辆销量增长不容小觑。据麦肯锡2013年发布的报告$^3$称，过去十年，中国高端汽车市场以年均36%的惊人速度持续增长，高于同期中国乘用车市场年均26%的整体增速。中国已然成为仅次于美国的全球第二大高端汽车市场。麦肯锡公司预计，从现在到2020年，中国高端汽车市场将保持年均12%的增长速度，预计到2020年，中国高端汽车年销售量将达到300万辆，基本与西欧市场销售量持平（图 3$^4$）。从销售价格而言，价格区间在42-70万之间乘用车销售量在2007年至2016年期间增长了近5倍$^5$。其中，高端乘用车领头品牌（奥迪、宝马、奔驰）销量不断上升，如图 4<sup>5</sup>所示，以奥迪销量增长最为突出。以上数据表明，在汽车行业中，高端车市场具有巨大增长潜力，随着整体消费水平的提升，我国高端车市场将进一步扩增<sup>[2]</sup>。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/C27E.tmp_.png"><img class="aligncenter size-full wp-image-12156" src="https://cos.name/wp-content/uploads/2016/05/C27E.tmp_.png" alt="C27E.tmp" width="554" height="227" srcset="https://cos.name/wp-content/uploads/2016/05/C27E.tmp_.png 554w, https://cos.name/wp-content/uploads/2016/05/C27E.tmp_-300x123.png 300w, https://cos.name/wp-content/uploads/2016/05/C27E.tmp_-500x205.png 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                       图 2 2004-2013 年中国汽车销量（万辆）</pre>

<pre><a href="https://cos.name/wp-content/uploads/2016/05/3520.tmp_.png"><img class="aligncenter size-full wp-image-12157" src="https://cos.name/wp-content/uploads/2016/05/3520.tmp_.png" alt="3520.tmp" width="480" height="276" srcset="https://cos.name/wp-content/uploads/2016/05/3520.tmp_.png 480w, https://cos.name/wp-content/uploads/2016/05/3520.tmp_-300x173.png 300w" sizes="(max-width: 480px) 100vw, 480px" /></a>                       图 3 全球高端汽车销售排名（千辆）</pre>

<pre><a href="https://cos.name/wp-content/uploads/2016/05/8305.tmp_.jpg"><img class="aligncenter size-full wp-image-12158" src="https://cos.name/wp-content/uploads/2016/05/8305.tmp_.jpg" alt="8305.tmp" width="555" height="241" srcset="https://cos.name/wp-content/uploads/2016/05/8305.tmp_.jpg 555w, https://cos.name/wp-content/uploads/2016/05/8305.tmp_-300x130.jpg 300w, https://cos.name/wp-content/uploads/2016/05/8305.tmp_-500x217.jpg 500w" sizes="(max-width: 555px) 100vw, 555px" /></a>               图 4 2007-2016 年中国奥迪、宝马、奔驰汽车销量（万辆）</pre>

##### ****（二）********高端车潜在购车人群业务背景分析****

高端车市场规模的迅速增长为高端车厂商带来了巨大的机遇，但同时，日益复杂的市场结构也对其营销战略提出了新的挑战。想要在激烈竞争的高端车销售行列中占据不败之地，必须准确洞察和把握消费者的诉求。这要求高端车生产厂商回答以下问题：高端车消费者的特征如何？他们购买高端车的关键因素有哪些？他们背后的心理诉求及偏好如何？各个地区市场划分有哪些差异？在准确刻画消费者画像的基础上，高端车生产厂商才能拥有独特的机会把握市场风向，改进产品设计，并推行精准的个性化营销<sup>[6]</sup>。

想要准确触及潜在购车群体，必须收集大量的用户行为数据。那么，如何大量的采集和分析用户数据？互联网技术的迅速发展为此提供了答案。据调查显示，近年来，互联网用户群体激增，已然成为主要消费群体寻求答案、表达核心诉求的主流媒体。这些媒体包括：搜索引擎、社交网络、门户网站、论坛、博客、贴吧等。

在众多互联网媒体中，搜索引擎（Search Engine）积累和展现的信息具有举足轻重的地位<sup>[3]</sup><sup>[7]</sup><sup>[9]</sup>。这主要是因为，用户在使用搜索引擎的过程中，往往带有明确的目的性。例如，如果一个用户频繁搜索“奥迪A6”，则表明他对于该车型相关信息有较强的兴趣，并极有可能转化为奥迪的购买用户。为了保有这些潜在用户，厂商往往会在搜索引擎上投放相关广告以吸引用户，如图 5示例为用百度（www.baidu.com）搜索车型“奥迪A6”之后的广告展示结果。如果用户对搜索结果表现出进一步的兴趣，那么他会选择点击其中一些链接，这更加进一步表明其兴趣。因此，分析用户的高端车搜索、点击数据对于挖掘用户兴趣有独特的意义<sup>[4]</sup><sup>[12]</sup>。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/C63E.tmp_.jpg"><img class="aligncenter size-full wp-image-12160" src="https://cos.name/wp-content/uploads/2016/05/C63E.tmp_.jpg" alt="C63E.tmp" width="554" height="336" srcset="https://cos.name/wp-content/uploads/2016/05/C63E.tmp_.jpg 554w, https://cos.name/wp-content/uploads/2016/05/C63E.tmp_-300x182.jpg 300w, https://cos.name/wp-content/uploads/2016/05/C63E.tmp_-500x303.jpg 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                         图 5 百度搜索“奥迪A6”结果</pre>

#### ****二、数据描述****

##### ****（一）********数据********概况****

本文数据来自某搜索引擎平台的100万在线用户的13亿搜索序列文本。数据时间跨度3个月，数据记录为每个Cookie在此期间的精确到秒级的搜索和点击数据。

原始数据格式如表 1所示，包含5个字段：Cookie、Query（检索词）、action（是否点击）、time（搜索时间）、url（点击的URL，如无点击则为空），具体见表 2中变量说明。以第一行数据为例，其表示Cookie为9的用户在2014年9月2日21点45分56秒搜索了“奔驰”关键词，并对地址为[http://www.hx2car.com](http://www.hx2car.com/)的网站产生了点击行为。另外需要说明的是，如果同一Cookie在相邻的搜索时间内Query一列对应的检索词相同（如图1-2行），则为同一搜索词下的多项点击。如图7中1-2行表明用户在搜索“奔驰”后对于搜索结果中的2个链接地址进行了点击。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/4A6D.tmp_.png"><img class="aligncenter size-full wp-image-12161" src="https://cos.name/wp-content/uploads/2016/05/4A6D.tmp_.png" alt="4A6D.tmp" width="641" height="435" srcset="https://cos.name/wp-content/uploads/2016/05/4A6D.tmp_.png 641w, https://cos.name/wp-content/uploads/2016/05/4A6D.tmp_-300x204.png 300w, https://cos.name/wp-content/uploads/2016/05/4A6D.tmp_-500x339.png 500w" sizes="(max-width: 641px) 100vw, 641px" /></a></pre>

<pre><a href="https://cos.name/wp-content/uploads/2016/05/91DA.tmp_.png"><img class="aligncenter size-full wp-image-12162" src="https://cos.name/wp-content/uploads/2016/05/91DA.tmp_.png" alt="91DA.tmp" width="661" height="435" srcset="https://cos.name/wp-content/uploads/2016/05/91DA.tmp_.png 661w, https://cos.name/wp-content/uploads/2016/05/91DA.tmp_-300x197.png 300w, https://cos.name/wp-content/uploads/2016/05/91DA.tmp_-500x329.png 500w" sizes="(max-width: 661px) 100vw, 661px" /></a></pre>

如果将一次搜索及其点击看做一步，那么如图7所示该用户经历了6步，其中，在第3-4步之间，该用户由搜索奔驰品牌“叛变”为搜索奥迪品牌。因此，我们关心的问题是用户在搜索过程中表现出的“忠诚”及“叛变”行为背后隐藏的关键因素。

###### ****（二）用户画像****

为了探索以上用户搜索行为，本文主要关注两个特定人群：高端车潜在用户，及商学院潜在用户，即在搜索过程中对高端车/商学院表现出浓厚兴趣的人群。具体地，基于搜索文本，我们做了以下处理。

首先，在对高端车潜在用户的筛选中，我们选定了市场份额较大，以奥迪、宝马、奔驰等品牌为代表的11个高端车品牌。并按照品牌关键字与用户搜索文本进行匹配，最终提取出在搜索过程中对高端车品牌表现出浓厚兴趣的人群（累积搜索高端车品牌次数超过5次），将他们定义为高端车潜在用户人群（以下简称高端车用户）。经过处理，在100万总样本中，我们最终得到高端车用户数目约为21万人。类似地，在对商学院潜在人群的定位中，我们首先提取了国内知名商学院关键词（如光华商学院、长江商学院等），然后利用关键词匹配在搜索过程中对商学院浓厚兴趣的用户（以下简称商学院用户），最终得到约1万6千名商学院用户。

基于以上用户划分，我们对其用户属性进行了描述。具体地，我们主要关注用户在生活、事业、学业表现出的“高端”属性（图 6）。为了总结这一特征，对于该属性的每一个维度，通过携程（www.ctrip.com）、大众点评（www.dianping.com）等第三方网站上的公开资源，获得相关关键词，并对其相应的消费等级分类打分。在此基础上对普通大众、高端车用户、商学院人群三类人做了对比分析。具体情况如下。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/BBE8.tmp_.png"><img class="aligncenter size-full wp-image-12163" src="https://cos.name/wp-content/uploads/2016/05/BBE8.tmp_.png" alt="BBE8.tmp" width="554" height="305" srcset="https://cos.name/wp-content/uploads/2016/05/BBE8.tmp_.png 554w, https://cos.name/wp-content/uploads/2016/05/BBE8.tmp_-300x165.png 300w, https://cos.name/wp-content/uploads/2016/05/BBE8.tmp_-500x275.png 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                     图 6 高端属性的三个维度：生活、事业、学业</pre>

首先，为了刻画用户对于品质生活的追求，本文考虑了住、吃、玩、用、出行等多个维度（图 7）。在住方面，通过借鉴携程、艺龙（www.elong.com）等多家旅游类垂直网站等公开资源，获得五星级及其以上的高档酒店列表。在吃方面，通过分析大众点评网等公开资源，获得人均消费单价远高于平均水平的高档餐厅列表。在玩方面，课题组关注以出国海岛游（例如：马尔代夫）、高级游轮为代表的高端旅游，以及相关的关键词。在用方面，课题组关注诸如iphone6、Vertu、高端单反相机等为代表的高科技产品，以及以LV、阿玛尼、香奈儿为代表的奢侈用品。在出行方面，课题组关注以高端酒店、私人包机等为代表的高端出行方式。通过对这些关键词的提取评估，我们对每个用户的生活方面打分。从中我们发现，高端车人群得分约为普通人群的两倍。清晰显示高端车人群对品质生活更高的追求。值得注意的是，商学院的得分更高，约是高端车人群的两倍，意味着商学院人群较之高端车人群，更加注重对于生活品质的追求。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/D553.tmp_.png"><img class="aligncenter size-full wp-image-12164" src="https://cos.name/wp-content/uploads/2016/05/D553.tmp_.png" alt="D553.tmp" width="554" height="320" srcset="https://cos.name/wp-content/uploads/2016/05/D553.tmp_.png 554w, https://cos.name/wp-content/uploads/2016/05/D553.tmp_-300x173.png 300w, https://cos.name/wp-content/uploads/2016/05/D553.tmp_-500x289.png 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                                图 7 高端属性（生活）</pre>

同时，在学习方面，本文主要考虑了抽取用户获取财经、科技等资讯信息的能力等信息（图 8）。首先，在财经方面，本文关注以和讯网（www.hexun.com）、中金在线（www.cnfol.com）、凤凰财经（finance.ifeng.com）等代表的一线财经新闻网站，认为点击这些网站较多的用户对财经、经济、金融等方面信息的敏锐嗅觉高；在科技前沿方面，本文关注以虎嗅网（www.huxiu.com）、36氪（36kr.com）等为代表的科技、互联网信息分享平台，认为关注这些网站较多的用户对前沿科技有着较深厚的兴趣和洞察力。同样利用综合打分的方式，我们同样发现高端车人群约是普通人群的2倍。这一点表示高端车人群在前沿资讯获取方面有着更加浓厚的兴趣。值得注意的是，商学院的得分则表现得更高，约是高端车人群的3倍，这意味着商学院人群相对高端车人群和普通用户人群有着更大的学习热情和兴趣。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/C687.tmp_.png"><img class="aligncenter size-full wp-image-12165" src="https://cos.name/wp-content/uploads/2016/05/C687.tmp_.png" alt="C687.tmp" width="554" height="337" srcset="https://cos.name/wp-content/uploads/2016/05/C687.tmp_.png 554w, https://cos.name/wp-content/uploads/2016/05/C687.tmp_-300x182.png 300w, https://cos.name/wp-content/uploads/2016/05/C687.tmp_-500x304.png 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                              图 8 高端属性（学业）</pre>

最后，在事业方面，本文主要关注以创业、金融资产管理、高端房地产、高端社交为代表的多个维度（图 9）。在创业方面，研究组主要关注一线风投、投资公司，如红杉资本、创新工场、真格基金等；在金融理财方面，主要关注以高端信用卡、信托私募、家族财富管理为代表的理财方式；在房地产方面，课题组关注主要高端房地产品牌，如保利国际、万达、华远等；在社交领域，主要关注高端商务社交方式，如高级酒庄、高尔夫球俱乐部、商务会所等。综合以上关键词提取信息，利用综合打分的方式，我们同样发现高端车人群约是普通人群的2倍，可以看出高端车人群在社会中更多的扮演着成功商务人士的角色。同时，商学院人群得分约是高端车人群的2倍，这意味着商学院人群相对高端车人群在事业方面有着更加卓越的品位和追求。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/CD7D.tmp_.png"><img class="aligncenter size-full wp-image-12166" src="https://cos.name/wp-content/uploads/2016/05/CD7D.tmp_.png" alt="CD7D.tmp" width="554" height="334" srcset="https://cos.name/wp-content/uploads/2016/05/CD7D.tmp_.png 554w, https://cos.name/wp-content/uploads/2016/05/CD7D.tmp_-300x181.png 300w, https://cos.name/wp-content/uploads/2016/05/CD7D.tmp_-500x301.png 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                               图 9 高端属性（事业）</pre>

##### ****（三）高端车市场****

接下来，我们利用搜索文本数据对高端车市场进行了分析。首先，我们根据高端车品牌关键词匹配了搜索文本数据，并提取了各大品牌的搜索量排名，如图 10所示。其中，奥迪、宝马、奔驰三个品牌摘取前三甲，占据了近七成高端车市场。其中以奥迪、宝马品牌遥遥领先。类似地，我们对主要汽车媒体的点击量进行了描述分析，点击量占据前三名的汽车媒体分别为：易车网、汽车之家、爱卡汽车（图 11）。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/9486.tmp_.png"><img class="aligncenter size-full wp-image-12167" src="https://cos.name/wp-content/uploads/2016/05/9486.tmp_.png" alt="9486.tmp" width="508" height="307" srcset="https://cos.name/wp-content/uploads/2016/05/9486.tmp_.png 508w, https://cos.name/wp-content/uploads/2016/05/9486.tmp_-300x181.png 300w, https://cos.name/wp-content/uploads/2016/05/9486.tmp_-500x302.png 500w" sizes="(max-width: 508px) 100vw, 508px" /></a>                            图 10 高端车搜索量统计</pre>

<pre><a href="https://cos.name/wp-content/uploads/2016/05/414A.tmp_.png"><img class="aligncenter size-full wp-image-12168" src="https://cos.name/wp-content/uploads/2016/05/414A.tmp_.png" alt="414A.tmp" width="504" height="321" srcset="https://cos.name/wp-content/uploads/2016/05/414A.tmp_.png 504w, https://cos.name/wp-content/uploads/2016/05/414A.tmp_-300x191.png 300w, https://cos.name/wp-content/uploads/2016/05/414A.tmp_-500x318.png 500w" sizes="(max-width: 504px) 100vw, 504px" /></a>                              图 11 汽车媒体点击量统计</pre>

接下来，我们对各大高端车品牌之间的竞争关系进行描述。首先我们计算用户在搜索各大品牌时从不同品牌之间的跳转概率。设系统中共有$i=1,2,\cdots,N$个高端车用户，对于第$i$个用户，我们保留其关于高端车品牌相关搜索（也就是说，搜索文本必须与高端车品牌信息相关），设其搜索$t=1,2,\cdots,T\_i$步（即发生了$T\_i$次搜索）。另外，我们假设系统中共有$j=1,2,\cdots,J$个品牌，设第个用户在第步搜索品牌为$Z\_{it} \in \{1,\cdots,J\}$。则我们可以得到用户从品牌$j\_1$跳转到$j_2$的经验转移概率：

$$P\_{j\_1j\_2}=\{\sum\_{i=1}^N \sum\_{t=1}^{T\_i-1}I(Z\_{i,t}=j\_1)\}^{-1}\{\sum\_{i=1}^N\sum\_{t=1}^{T\_i-1}I(Z\_{it}=j\_1,Z\_{I(t+1)}= j_2)\}$$

通过计算，11个高端车品牌间概率矩阵如图 12所示。其中，第行列的数据表示从品牌$j\_1$跳转到品牌$j\_2$的转移概率（即$P\_{j\_1j_2}$），该概率越大，则对应矩阵块的颜色越深$^6$。首先，矩阵对角线表示用户相邻两步搜索同一品牌的概率，这反应了品牌保有客户的能力，是品牌忠诚度的反应。数据统计显示，奥迪品牌保有客户的能力最强，用户搜索奥迪品牌后约七成的概率持续搜索，占据首位。另一方面，非对角线每一列元素代表对应品牌吸引客户的能力，该列数字越大，代表对应品牌的魅力越大，从这一指标看，宝马品牌吸引客户的能力较强，这主要表现在用户在搜索其他品牌后转移到宝马品牌的概率较大（图 12转移概率矩阵第二列）。

* * *

<pre><a href="https://cos.name/wp-content/uploads/2016/05/A4FE.tmp_.png"><img class="aligncenter size-full wp-image-12169" src="https://cos.name/wp-content/uploads/2016/05/A4FE.tmp_.png" alt="A4FE.tmp" width="554" height="333" srcset="https://cos.name/wp-content/uploads/2016/05/A4FE.tmp_.png 554w, https://cos.name/wp-content/uploads/2016/05/A4FE.tmp_-300x180.png 300w, https://cos.name/wp-content/uploads/2016/05/A4FE.tmp_-500x301.png 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                    图 12 用户搜索高端车品牌转移概率矩阵</pre>

最后，为了描述各个品牌之间的竞争关系，我们按照用户对品牌的搜索对高端车品牌进行了聚类分析。其基本思路是，如果两个品牌被用户频繁的同时搜索，则可以认为这些品牌经常被用于比对，因此，其之间的竞争关系较为激烈。为了测评高端车品牌之间的竞争关系，首先，我们以每个用户为观测，以11个高端车品牌为变量，形成样本矩阵$X=(X\_{ij})\in \mathbb{R}^{N \times J}$，其中，$X\_{ij}=1$表示第个$i$人搜索过第$j$个品牌，否则$X_{ij}=0$。根据上述定义可以计算变量和变量之间的距离，距离越短表示相关两个品牌被同时搜索的次数越多。基于该距离矩阵，进行层次聚类分析，结果如图 13所示。由结果可以看出11个高端车品牌可以大体被分为三类，其中，奥迪、宝马、奔驰位于层次聚类树的最低端，并可以被归入一个类别中。这表明，这三个品牌之间的竞争关系较为激烈，其中以奥迪和宝马之间的竞争关系尤为突出。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/A435.tmp_.png"><img class="aligncenter size-full wp-image-12170" src="https://cos.name/wp-content/uploads/2016/05/A435.tmp_.png" alt="A435.tmp" width="554" height="321" srcset="https://cos.name/wp-content/uploads/2016/05/A435.tmp_.png 554w, https://cos.name/wp-content/uploads/2016/05/A435.tmp_-300x174.png 300w, https://cos.name/wp-content/uploads/2016/05/A435.tmp_-500x290.png 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                         图 13 高端车品牌层次聚类分析结果</pre>

#### ****三、数据建模****

##### ****（一）********忠诚模型****

通过对数据的初步结构化及筛选，我们可以形成对每个用户高端车搜索序列的完整记录。接下来，我们拟建模分析用户在搜索过程中表现出的“忠诚”及“叛变”行为，其中，“忠诚”的定义为用户在第$t$步搜索了某品牌后，在第$t+1$步仍然继续搜索该品牌，“叛变”则定义为用户在$t+1$步转向搜索其他品牌。本文拟构建逻辑回归模型，探索影响用户“忠诚”及“叛变”的关键因素。定义$Y\_{ij}^{(t)}=1$代表第i个用户于第t步搜索了第j个品牌，否则$Y\_{ij}^{(t)}=0$。则构建以下逻辑回归模型（忠诚模型）：

$$P(Y\_{ij}^{(t+1)}=1|Y\_{ij}^{(t)}=1)=\frac{exp(\alpha\_j+X\_i^{(t)&#8217;}\beta)}{1+exp(\alpha\_j + X\_i^{(t)&#8217;}\beta)}$$

其中，$X\_i^{(t)}$为与解释叛变行为相关的自变量，$\beta$为相应的估计系数，$\alpha\_j$表示与品牌j相关的截距项，可以认为是控制了自变量$X_i^{(t)}$后度量品牌j的忠诚度指标。具体考虑指标如下节所示。

##### ****（二）********影响因素****

###### ****（********1********）****搜索品牌数

搜索品牌数，是指用户第t步之前搜索不同品牌的数目。描述性分析如图 14显示，叛变用户之前平均搜索平均搜索品牌数约是忠诚用户的1.5倍。也就是说，叛变用户之前对于品牌的搜索中更多表现出“花心”特征，也更容易导致“叛变”行为。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/7BA.tmp_.png"><img class="aligncenter size-full wp-image-12172" src="https://cos.name/wp-content/uploads/2016/05/7BA.tmp_.png" alt="7BA.tmp" width="554" height="308" srcset="https://cos.name/wp-content/uploads/2016/05/7BA.tmp_.png 554w, https://cos.name/wp-content/uploads/2016/05/7BA.tmp_-300x167.png 300w, https://cos.name/wp-content/uploads/2016/05/7BA.tmp_-500x278.png 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                             图 14 搜索品牌数</pre>

###### ****（2）****时间间隔

时间间隔，指这一步（第t+1步）与上一步（第t步）两步搜索之间的时间间隔。本文对两步搜索的时间间隔进行了log(1+x)变换。如图 15所示，我们的描述性分析结果显示，“叛变”行为对应的时间间隔更长，约为1小时，而忠诚行为对应的时间间隔更短，平均约为5分钟。这一指标说明如果两次搜索时间间隔过长，则容易“夜长梦多”，形成“叛变”行为。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/51E8.tmp_.png"><img class="aligncenter size-full wp-image-12173" src="https://cos.name/wp-content/uploads/2016/05/51E8.tmp_.png" alt="51E8.tmp" width="554" height="266" srcset="https://cos.name/wp-content/uploads/2016/05/51E8.tmp_.png 554w, https://cos.name/wp-content/uploads/2016/05/51E8.tmp_-300x144.png 300w, https://cos.name/wp-content/uploads/2016/05/51E8.tmp_-500x240.png 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                        图 15 log(1+x)变换后搜索时间间隔</pre>

###### ****（3）****连续搜索数

连续搜索数，是指用户之前连续搜索同品牌的次数。连续搜索同品牌次数越多，该用户越有可能是某品牌的深度用户，那么该用户可能更加忠诚。通过描述性分析的结果（图 16）也可以看出，“忠诚”行为对应之前的连续搜索步数约为 “叛变”用户的2倍，远小于忠诚用户。这说明，忠诚用户的搜索同一品牌的“惯性”更大。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/8E0F.tmp_.png"><img class="aligncenter size-full wp-image-12174" src="https://cos.name/wp-content/uploads/2016/05/8E0F.tmp_.png" alt="8E0F.tmp" width="554" height="288" srcset="https://cos.name/wp-content/uploads/2016/05/8E0F.tmp_.png 554w, https://cos.name/wp-content/uploads/2016/05/8E0F.tmp_-300x156.png 300w, https://cos.name/wp-content/uploads/2016/05/8E0F.tmp_-500x260.png 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                           图 16 同一品牌连续搜索数</pre>

###### ****（4）****搜索词长度

搜索词长度，是指用户上一步（第t步）的搜索关键词长度。从描述性分析来看（图 17），忠诚用户对应的搜索关键词长度稍长于“叛变”用户。搜索长尾关键词一定程度上意味着该用户在搜索过程中要付出更多的成本[11]，这也表明对应用户可能是深度用户，从而表现出更加忠诚的行为。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/A78A.tmp_.png"><img class="aligncenter size-full wp-image-12176" src="https://cos.name/wp-content/uploads/2016/05/A78A.tmp_.png" alt="A78A.tmp" width="554" height="282" srcset="https://cos.name/wp-content/uploads/2016/05/A78A.tmp_.png 554w, https://cos.name/wp-content/uploads/2016/05/A78A.tmp_-300x153.png 300w, https://cos.name/wp-content/uploads/2016/05/A78A.tmp_-500x255.png 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                                    图 17 搜索词长度</pre>

###### ****（5）****是否搜索配置信息

是否搜索配置信息，是指用户上一步（第t步）是否搜索了高端车品牌的配置信息（如发动机、轮胎、转轴等）。从描述性分析来看（图 18），忠诚用户对应的搜索配置信息的次数更多，显著高于“叛变”用户一倍。搜索配置信息表明了该用户可能进入到更加深入的信息检索层面，这也是“深度用户更加忠诚”的佐证。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/B9C4.tmp_.png"><img class="aligncenter size-full wp-image-12177" src="https://cos.name/wp-content/uploads/2016/05/B9C4.tmp_.png" alt="B9C4.tmp" width="554" height="269" srcset="https://cos.name/wp-content/uploads/2016/05/B9C4.tmp_.png 554w, https://cos.name/wp-content/uploads/2016/05/B9C4.tmp_-300x146.png 300w, https://cos.name/wp-content/uploads/2016/05/B9C4.tmp_-500x243.png 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                              图 18 是否搜索配置信息</pre>

###### ****（6）****点击数

点击数，是指用户上一步搜索后产生的点击次数。从描述性分析（图 19）可以看出，忠诚用户搜索后产生的平均点击高于“叛变”用户。点击越多说明用户在一次搜索之后了解信息的意愿更强，也是深度用户的侧面反映。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/A463.tmp_.png"><img class="aligncenter size-full wp-image-12178" src="https://cos.name/wp-content/uploads/2016/05/A463.tmp_.png" alt="A463.tmp" width="554" height="302" srcset="https://cos.name/wp-content/uploads/2016/05/A463.tmp_.png 554w, https://cos.name/wp-content/uploads/2016/05/A463.tmp_-300x164.png 300w, https://cos.name/wp-content/uploads/2016/05/A463.tmp_-500x273.png 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                                图 19 搜索后点击数</pre>

###### ****（7）****问答百科

问答百科，是指用户上一步搜索后是否点击了问答百科类网站。其中，问答百科类网站主要是为用户解惑答疑的知识性网站，例如，百度知道（zhidao.baidu.com），360百科（baike.so.com）等。从描述性分析（图 20）可以看出，忠诚用户搜索后点击问答百科网站的平均次数约为 “叛变”用户2倍。问答百科类网站上一般展示的是更加细节的问题和讨论，用户点击此类网站代表其对相关问题兴趣浓厚，可能是深度用户。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/5961.tmp_.png"><img class="aligncenter size-full wp-image-12179" src="https://cos.name/wp-content/uploads/2016/05/5961.tmp_.png" alt="5961.tmp" width="554" height="291" srcset="https://cos.name/wp-content/uploads/2016/05/5961.tmp_.png 554w, https://cos.name/wp-content/uploads/2016/05/5961.tmp_-300x158.png 300w, https://cos.name/wp-content/uploads/2016/05/5961.tmp_-500x263.png 500w" sizes="(max-width: 554px) 100vw, 554px" /></a>                       图 20 搜索后是否点击问答百科类网站</pre>

##### ****（三）********估计结果****

根据忠诚模型，利用Newton-Raphson算法迭代得到估计结果如表 3所示$^6$。可以看到，所有变量系数估计在95%置信度下显著。其中我们发现，搜索汽车配置信息越多、搜索后点击数越多、点击问答百科类网站次数越多，以及连续搜索某品牌次数越多的用户，在搜索行为上表现的更加忠诚；而两次搜索时间间隔越长、用户历史搜索的品牌数越多，其在搜索过程中更容易出现“叛变”行为。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/C38A.tmp_.png"><img class="size-full wp-image-12180 aligncenter" src="https://cos.name/wp-content/uploads/2016/05/C38A.tmp_.png" alt="C38A.tmp" width="602" height="362" srcset="https://cos.name/wp-content/uploads/2016/05/C38A.tmp_.png 602w, https://cos.name/wp-content/uploads/2016/05/C38A.tmp_-300x180.png 300w, https://cos.name/wp-content/uploads/2016/05/C38A.tmp_-500x301.png 500w" sizes="(max-width: 602px) 100vw, 602px" /></a></pre>

同时，我们得到了控制自变量后的品牌忠诚度系数的估计结果，系数估计值如图 21中柱状图所示。可以看到，在控制自变量之后，忠诚度最高的三个品牌分别为，奥迪、奔驰和林肯，宝马位居第四。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/39F3.tmp_.png"><img class="aligncenter size-full wp-image-12181" src="https://cos.name/wp-content/uploads/2016/05/39F3.tmp_.png" alt="39F3.tmp" width="512" height="289" srcset="https://cos.name/wp-content/uploads/2016/05/39F3.tmp_.png 512w, https://cos.name/wp-content/uploads/2016/05/39F3.tmp_-300x169.png 300w, https://cos.name/wp-content/uploads/2016/05/39F3.tmp_-500x282.png 500w" sizes="(max-width: 512px) 100vw, 512px" /></a>                           图 21 忠诚度系数估计值</pre>

##### ****（四）********模型评估****

得到模型估计结果后，本文进一步对模型效果进行了评估。为此，我们主要计算了覆盖率及捕获率指标，并绘制了成本收益曲线。具体地，当给定阈值时，当模型输出的叛变概率时，预测该用户将在下一步叛变，否则预测该用户将在下一步保持搜索同一品牌。接下来，计算两个指标：（a）覆盖率，即预测为叛变的人与总人数的比值；（b）捕获率，即预测为叛变的人中实际叛变的人数与总叛变人数的比值。其中，覆盖率可以看作是衡量成本的指标，而捕获率可以作为衡量收益的指标。注意到，当时，模型将所有用户预测为叛变，则此时捕获率为100%，即捕获了所有叛变的行为。然而，为此付出的代价是将未叛变行为错误预测为了叛变，即付出了多余的成本。我们希望，当给定一个合适的时，覆盖率能够控制在合理水平，而对应的捕获率较高。为此，我们将不同阈值对应的覆盖率、捕获率指标列在表 4中。可以看到，当给定阈值30%时，覆盖率约在48.6%时，捕获率达到81.1%。最后，我们以覆盖率为横轴，捕获率为纵轴绘制成本收益曲线，如图 22所示。可以看出，成本收益曲线成较凸型，这表明忠诚模型拟合效果良好。

<pre><a href="https://cos.name/wp-content/uploads/2016/05/FBAE.tmp_.png"><img class="aligncenter size-full wp-image-12183" src="https://cos.name/wp-content/uploads/2016/05/FBAE.tmp_.png" alt="FBAE.tmp" width="609" height="606" srcset="https://cos.name/wp-content/uploads/2016/05/FBAE.tmp_.png 609w, https://cos.name/wp-content/uploads/2016/05/FBAE.tmp_-150x150.png 150w, https://cos.name/wp-content/uploads/2016/05/FBAE.tmp_-300x300.png 300w, https://cos.name/wp-content/uploads/2016/05/FBAE.tmp_-500x498.png 500w" sizes="(max-width: 609px) 100vw, 609px" /></a>                        图 22 忠诚模型成本收益曲线</pre>

#### ****四、业务实施****

根据本文描述分析及数据建模结果，我们认为可以对高端车厂商在广告投放等业务层面提供一些可行性建议，具体建议如下。

###### ****（********1********）****人群细分

本文根据公开数据源提取了能够表征用户高端属性的关键词，并细分为生活、事业、学业各个方面。描述分析显示，不同属性人群在品牌车辆搜索行为中表现出不同特征，其中，具有高端属性的人群搜索高端车品牌的概率更大。因此，对于高端车厂商而言，应进行适合的市场细分，对于高端人群应定制合理的营销战略。在市场细分过程中，由描述分析结果可知，商学院用户表现出更加突出的高端属性，并且相对更多的关注高端车信息，是高端车厂商在积累客户资源的过程中需要重点关注的客户群体。

###### ****（********2********）****广告投放媒体

从目标人群而言，由于商学院用户对于信息新闻的触觉更加灵敏，因此，可以考虑在信息门户类网站（例如财经、科技类网站）增加投放广告比例，以吸引支付意愿及能力较高的商学院客户人群。从汽车媒体分类上而言，用户浏览不同特点汽车媒体（例如，门户网站汽车资讯、购车平台等）后可能行为特点有所不同，应考虑根据这种差异有定制性的投放广告。

###### ****（********3********）****长尾关键词投放

根据忠诚模型，搜索长尾关键词的用户一般为深度用户，其忠诚度更高。根据此规律，高端车厂商可以适当安排长尾词的广告投放，以增加忠诚用户的客户粘性。

###### ****（********4********）****互联网产品线设计

由忠诚模型可知，浏览百科、问答类网站的客户更不易叛变，这也表明对于搜索引擎而言可以适当增强此类产品线设计，比如引入广告投放位等，可以成为未来潜在盈利点。另外，对于高端车厂商而言，可以适当增加客服在该类网站上的应答，以期增加客户粘性。

****五、总结与讨论****

本文主要通过对用户在搜素引擎上的搜索文本进行分析，对普通人群、高端车用户与商学院用户进行了对比分析，发现高端车用户与商学院用户在生活、事业、学业上的高端属性得分更高。同时，本文对用户的高端车文本搜索序列进行建模，并对用户的品牌忠诚和叛变行为进行了刻画，通过系数估计结果，我们发现，搜索汽车配置信息越多、搜索后点击数越多、点击问答百科类网站次数越多，以及连续搜索某品牌次数越多的用户，在搜索行为上表现的更加忠诚；而两次搜索时间间隔越长、用户历史搜索的品牌数越多，其在搜索过程中更容易出现“叛变”行为。

本文认为目前文章可改进的地方有以下几点：（a）多数据源信息完善。目前而言，搜索引擎还没有建立完整的用户个人账户体系，但是，这一过程在逐渐完善。如果用户的个人信息资料建立完善，那么就可以更加完整的记录用户的搜索路径，完善其个人特征（例如，年龄、性别等特征）。另一方面，移动互联网的发展使得手机应用逐渐普及，这使得用户的生活轨迹（地理位置、轨迹数据）等可以被完整记录，通过匹配这一数据，可以还原用户的生活特征，并进行更加细节的用户画像。（b）模型扩展。注意到本文建立的忠诚模型因变量为搜索过程中是否对品牌忠诚，品牌差异性主要体现于模型的截距项参数上。然而，用户对于不同品牌的忠诚度行为模式可能存在更大差异，因此，需要进行更加细节的探索和建模。另外，在已知用户叛变的基础上，未来的研究可对用户对于其他品牌的选择行为进行讨论，从而对竞品投放的广告策略产生更有价值的指导。

**注：**

$^1$ 由数据保密性需求，本文使用数据均为虚拟数据

$^2$数据来源：国家统计局

$^3$ 资料来源：麦肯锡报告《乘势而上：中国高端汽车市场展望》（2013）

$^4$资料来源：IHS环球通视；麦肯锡M-View；麦肯锡中国高端汽车研究（2012）

$^5$资料来源：搜狐汽车网（auto.sohu.com）

<a href="#_ftn1" name="_ftnref1"></a>$^6$由于数据保密性需求，本文在保持符号不变的情况下对系数估计结果进行了数值变换

****参考文献****

【1】曹建海. 经济全球化与中国汽车产业发展[J]. 管理世界, 2003(4), 68&#8211;76.

【2】邓晓爱. 浅谈我国高端车企市场营销策略[J]. 经营管理者, 2013(23), 269&#8211;269.

【3】Ghose A, Yang S. An empirical analysis of search engine advertising: Sponsored search in electronic markets[J]. Management Science, 2009, 55(10), 1605&#8211;1622.

【4】Häubl G, Trifts V. Consumer decision making in online shopping environments: The effects of interactive decision aids[J]. Marketing science, 2000, 19(1), 4&#8211;21.

【5】Huang P, Lurie N H, Mitra S. Searching for experience on the web: an empirical examination of consumer behavior for search and experience goods[J]. Journal of Marketing, 2009, 73(2), 55&#8211;69.

【6】黄彪虎. 个性化营销[J]. 企业管理, 2001 (11), 58&#8211;59.

【7】Montgomery A, Srinivasan K. Learning about customers without asking[J]. Tepper School of Business, 2002, 324.

【8】Montgomery A L, Li S, Srinivasan K, et al. Modeling online browsing and path analysis using clickstream data[J]. Marketing Science, 2004, 23(4), 579&#8211;595.

【9】Ramos A, Cota S. Search engine marketing[M]. McGraw-Hill, Inc., 2008.

【10】宋泓, 柴瑜, 张泰. 市场开放, 企业学习及适应能力和产业成长模式转型——中国汽车产业案例研究[J]. 管理世界, 2004(8), 61&#8211;74.

【11】Skiera B, Eckert J, Hinz O. An analysis of the importance of the long tail in search engine marketing[J]. Electronic Commerce Research and Applications, 2010, 9(6), 488&#8211;494.

【12】Schmidt J B, Spreng R A. A proposed model of external consumer information search[J]. Journal of the academy of Marketing Science, 1996, 24(3), 246&#8211;256.

&nbsp;