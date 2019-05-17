# e3mall
javaweb企业级项目开发源码

第一天：

1、电商行业的背景。互联网行业工资高。
2、电商模式：b2b、b2c、c2c、o2o
3、项目架构：
	1）集群
	2）分布式
	3）基于soa架构
4、宜立方商城的系统架构。
5、工程搭建。
	maven管理工程。
	父工程
	聚合工程
	模块
	工程的继承、依赖。
6、ssm框架整合。
7、svn的使用
第二天：

1、dubbo，服务治理工具。实现系统之间通信。
	1）服务提供者
	2）服务消费者
	3）注册中心，使用zookeeper实现，相当于房产中介。
	4）监控中心。
2、工程改造。改造为基于soa架构的工程。
3、商品列表的查询。
	1）EasyUI的DataGrid控件。
	2）mybatis的分页插件。
第三天、第四天：

商品添加：
1、商品分类选择
	1）EasyUITree控件。异步加载。
2、商品图片。实现图片上传。
	1）图片服务器
		（1）FastDFS保存图片
			Tracker，相当于注册中心的作用，关键服务器集群。
			Storage，保存文件的服务器。
		（2）访问图片http服务器，推荐使用nginx
			a.静态资源的访问。配置server可以。
				a)通过端口区分不同的server
				b)通过域名区分不同的server
			b.反向代理
				proxy_pass http://upstream_name;
				需要配置upstream节点。
				节点中有应用服务的地址列表。
			c.负载均衡
				需要配置upstream节点中配置多个服务器就可以实现负载均衡
				调整每个服务器的权重。
	2）图片上传的实现
		（1）FastDFS的java客户端
		（2）使用KindEditor的多图片上传插件。
3、富文本编辑器的使用
	KindEditor。
4、商品添加。
第五天

1、商城首页展示。
2、页面内容动态展示，需要cms系统。
	1）内容分类管理
		树形结构。
	2）内容管理
		一个内容分类下对应一个内容列表。
3、商品首页动态展示。
	从数据库中取内容列表，根据内容分类id查询。
第六天

向业务逻辑添加缓存
1、使用redis做缓存
	1）string
	2）hash
	3）list
	4）set
	5）SortedSet
2、redis集群
	1）没有代理层。
	2）投票容错
	3）客户端连接任意节点即可。
	4）slot槽0-16383
3、jedis客户端。
	1）JedisPool
	3）JedisCluster
4、向业务逻辑中添加缓存。
5、缓存同步。
第七天：

搜索功能实现
1、solr服务搭建。
2、配置业务域。中文分析器的配置。
3、把商品数据导入到索引库
	solr的客户端：solrJ
4、搜索功能实现。
	使用solrJ实现搜索。
第八天

solrCloud的搭建
1、zookeeper集群
	推荐集群中应该是奇数节点。
2、solr集群
	配置文件统一管理。把配置文件上传到zookeeper。
	索引库分片。
3、solrJ连接集群。
	单机版：HttpSolrServer
	集群：CloudSolrServer
		1）zookeeper的地址列表
		2）设置DefaultCollection属性。
4、搜索功能切换到集群版。
第九天

1、使用MQ实现系统之间通信
Activemq，支持jms规范。
2、通信方式
	queue
	topic
3、Activemq整合spring
	发送消息：JmsTemplate
	接收消息：
		1）实现MessageListener接口
		2）配置MessageListenerContainer
3、添加商品同步索引库
第十天

商品详情页面
1、动态展示
jsp+redis
缓存需要有过期时间，提供缓存利用率。
2、网页静态化freemarker
	1）模板
		基于jsp改造。
	2）数据
		推荐使用map实现
3、静态化方案
	1、mq发送消息
	2、接收到消息，生成静态页面
	3、nginx访问静态页面。
第十一天：

sso系统：
主要解决的是Session共享的问题。
1、使用redis管理Session。
1）key：token
2）value：用户信息
3）可以需要设置有效期。
4）需要把token保存到cookie中。

2、根据token取用户信息
1）从cookie中取token
2）到redis中查询用户信息。
3）更新key的过期时间。

第十二天
购物车
1、未登录：使用cookie保存购物车数据
2、登录后：把购物车数据保存到redis。
2、购物车合并，应该以服务端的购物车为准。

第十三天：
订单系统
1、订单号生成。使用redis的incr
2、mycat。

第十四天：
系统部署
项目总结
