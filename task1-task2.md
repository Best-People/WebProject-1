# Task1
   
2017年5月组建web工程小组，共九个人，团队的核心是以开发一个西电网上商城为主，整个项目的具体操作流程是：需求分析→系统架构→搭建数据库→系统配置→编码实现→项目测试。小组各成员将自己的任务上传至GitHub上以方便成员沟通。
在项目的过程中我们尽量会明确每个人的职责和角色，积极放权，使成员进行自我管理和自我激励；增加项目团队成员的非工作沟通和交流的机会，如工作之余的聚会、郊游等，提高团队成员之间的了解和交流

 # Task2
     
  项目建议书
1项目名称
西电网上商城
2项目简介
西电网上商城是一个较为综合性的B2C平台系统，类似于很多国内的大型购物网站，京东 淘宝。用户可以浏览商品，下订单，以及参加各种活动。而后台管理则可以在管理系统中管理商品 订单的信息。还有处理用户的投诉。
3 项目背景
  网上购物的逐渐兴起，各类对网上商城的管理系统也变得多了起来，而且技术也已经变得趋于成熟，根据我们的调查，网上电子交易的发展每年的增长是非常迅速的，13年电商的规模已经突破十万亿大关，而又关电子商务的系统，技术已经非常成熟了。

下单，购物车，付款，都有着很多前人做的例子，我们将这些业务进行汇总，然后自己做出来一个网上商城系统，作为一套的完整开发流程，我们的网站是非常的方便的还有高效的。
4项目组成部分
   大体上商城分为
后台管理系统
前台系统
会员系统
搜索系统
单点登录系统
5 项目执行概要
   传统的架构单工程的模式存在着耦合度太高，开发困难，系统的拓展性太差，无法进行分布式部署的缺点，计划上我们将前后台分离，把不同的模块拆分成不同的工程，采用集群部署的方式，纵向拓展。
 6 需求概要
     功能需求，面向客户的部分需要页面美观，响应迅速，以用户体验为主，后台部分需要简介是管理人员一目了然
    性能需求：数据精确度，价格单位保留到分，购物流程应该简单明了，信息描述清晰
7预算
编号	项目	费用	总计	百分比
1	网站开发与维护	400	  400	28.93%
2	域名购买	39	 39	 3.50%
3	服务器租赁	57.5/月	 575	  51.62%
4	推广费用	200	 200	17.95%
8 组织信息
本组成员9人 组长：关鑫  组员：李万治、呼奎、潘磊、曹潇、温文轩、薛智元、刘琳、巩嫣然。
    组长关鑫负责项目构建监督、维护和总结 李万治、呼奎、潘磊、曹潇、温文轩、薛智元、负责web网站的规划与建设 刘琳、巩嫣然负责网站设计与美化

9 项目建议
   1 关于项目定位，我们主要是面向西电的学生，更应当重视学生的体验。
   2 关于盈利模式，由于面向群体的原因，我们应当减少广告的植入，竞价方式应当以学生的好评为主，众筹就是不错的方式
   3 商品展示部分，可以加入机器学习知识，根据用户的浏览习惯推出更加适合的页面产品推荐
   4 服务问题，网上商城可以让同学和商家即时联系，无需等待，业务系统必须高效
5 支付和物流 应该支持更多的方式 支付宝 网银 银联等，物流系统方面也要提供物流公司的接口。
10 项目总结
交付的产品名称：西电网上商城
使用的工具：
Eclipse 4.5.0(Mars)，自带maven插件，需要手工安装svn插件。
Maven 3.3.3
Tomcat 7.0.53（Maven Tomcat Plugin）
JDK 1.7
Mysql 5.6
Nginx 1.8.0
Redis 3.0.0
Win8 操作系统
SVN（版本管理）
模块清单：
  1、用户注册/登陆 
  2、用户信息修改 
3、实现购物 
4、查看购物车 
5、商品管理  
6、订单管理
7、用户管理 
功能实现总结
检查学生的信息是否存在：
查询数据库信息是否有返回true否则返回false
注册用户：
直接写入数据库
用户登录：
接收登陆数据，在数据库中查询，一旦用户登陆成功，则立即生成一个唯一ticket，然后使用map方式将ticket 和user的json数据value，存入redis当中
前台注册，前台处理service调用sso系统注册，返回状态码。前台返回注册信息，页面406错误。
登陆访问前台登陆，然后service调用sso系统登陆系统，查询并缓存，返回ticket给前台。前台判断ticket，存储到cookie中，并给前台返回成功数据。遇到问题：nignx转发使用域名转发。
添加购物车-登陆保存在购物车中-持久化
 -未登录保存cookie中-登陆合并kookie-持久化
用户在购物车跟新商品数量
接口接收useruid+itemId+num - 后台查询，如果有则更新数量

购物车页面删除某个商品
接口接收userid和itemid，后台直接删除
前台添加商品购物车，接受itemid+num，访问service（后台查询item拼接顺序），然后从thredlocal中获取userid，调用购物车系统，返回页面
显示购物车所有商品 空参接受，从thredlocal获取userid，然后访问 购物车查询所有系统
前台跟新购物车数量 接受itemid和num，当前线程获取userid，请求 购物车系统
未登录的购物车
添加购物车 获取itemid + num，获取user失败，则cookie获取购物车key，redis查询，便利 和商品对比，如果有则修改数量，没有则添加商品
显示购物车数量 如果user获取失败，则获取cookie中的key，redis查询数据转换为list返回
删除购物车种商品 获取user失败，则获取cookie中key，redis查询数据，便利对比，删除
