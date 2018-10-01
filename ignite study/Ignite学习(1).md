## 序 ##
一次偶然的机会接触到[Apache Ignite](https://ignite.apache.org/)，在快速浏览了官方文档和一些用例后，发现Ignite一些特性刚好就是我们手头上项目需要的，就把它带到项目中来了。但在使用的过程中发现，虽然Ignite在2015年已经从Apache孵化器毕业成为顶级项目，但除了官方文档外，目前无论中文资料还是英文资料还都比较少。而官方文档中的一些例子对API的使用并没有讲的十分透彻，哪怕是照着例子依葫芦画瓢，还是要自己趟过不少坑。于是就想借着这次机会，好好学习总结一下Ignite众多的特性，希望能在项目中把该工具用的更好。

另外，作为一个工作7年+的程序猿，一直也有写技术博客心结。直到今年工作上遇到的一些事后，让自己很认真的回顾下曾经学过、用过的技术，脑海里只剩下一些模糊的印象，如果再要去追究一些技术细节，只能依靠万能的Google。 做为一名轻度拖延症患者，有些事不破不立，就利用这次机会把博客做为总结积累技术学习的平台。 

## Apache Ignite 介绍  ##
究竟Ignite是什么呢？先引用一段官网关于Ignite的描述：
> Ignite is memory-centric distributed **database**, **caching**, and **processing** platform for transactional, analytical, and streaming workloads 
delivering in-memory speeds at petabyte scale

从字面理解，就是Ignite是以内存为中心的分布式的数据库，缓存和处理平台。它可以在数据量达到PB级别，依然为事务性处理，数据分析和流式任务提供了内存级的操作速度。 再从官网借用一张架构图：
![](https://files.readme.io/0bad3a9-ignite_architecture.png)
在架构图中，图中的红色部分属于Ignite提供的组件。从下往上分别是：


- 存储层(持久化层)：在持久化层，我们可以看到Ignite同时支持原生持久化和用第三方存储做持久化，比如RMDBMS，HDFS等。 
- Ignite内存存储层：数据可以通过不同分区复制模式分布在Ignite集群所有节点，部分节点或者本地节点。这保证了即便某些节点故障后，数据任然可以被访问使用。
- API接口层以及应用层：这一层功能看着十分强大。和其他缓存系统比,比如Redis,Etcd等，Ignite对SQL,k/v和transaction的支持更加全面。

如果还想了解更多关于Ignite基本概念和资料，可以看看李玉珏翻译的[中文官方文档](https://liyuj.gitee.io/doc/java/#_1-1-ignite%E6%98%AF%E4%BB%80%E4%B9%88)。这也算是对英文不好的同学的福利。 

## Apache Ignite 集群命令行启动 ##

