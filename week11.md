## 左耳听风ARTS第十一周（2019年12月22日）

 1.**Algorithm** （No.4）（NO.19）

Given a linked list, remove the n th node from the end of list and return its head.
For example,
Given linked list: 1->2->3->4->5, and n = 2.
After removing the second node from the end, the linked list becomes 1->2->3->5.

解答：

public class Solution {
public ListNode removeNthFromEnd(ListNode head, int n) {
if(head.next == null) {
return null;
}
int i = 0;
ListNode p1 = head, p2 = head;
while(p1.next != null) {
p1 = p1.next;
++i;
if(i > n) {
9
p2 = p2.next;
}
}
if(i == n - 1) {
head = head.next;
} else {
p2.next = p2.next.next;
}
return head;
}
}

 

2.**Review** 

本周是上班的第四周 是十二月第三周。主要开发了番职的代办接口 验收模块调整 还有合同模板，特别是把word转化成html 在网上搜索了工具类。感觉自己很多不熟悉的东西要学。  这些都是jeccg这个框架分配的 码云上面有这个框架可以学习一下。

但是对于代码的把握和熟练度还不够要多敲代码。

3.**Tips**  

Ehcache 在java项目广泛的使用。它是一个开源的、设计于提高在数据从RDBMS中取出来的高花费、高延迟采取的一种缓存方案。正因为Ehcache具有健壮性（基于java开发）、被认证（具有apache 2.0  license）、充满特色（稍后会详细介绍），所以被用于大型复杂分布式web application的各个节点中。 1.  够快 Ehcache的发行有一段时长了，经过几年的努力和不计其数的性能测试，Ehcache终被设计于large, high concurrency systems. 2. 够简单 开发者提供的接口非常简单明了，从Ehcache的搭建到运用运行仅仅需要的是你宝贵的几分钟。其实很多开发者都不知道自己用在用Ehcache，Ehcache被广泛的运用于其他的开源项目 比如：hibernate 3.够袖珍 关于这点的特性，官方给了一个很可爱的名字small foot print ，一般Ehcache的发布版本不会到2M，V 2.2.3  才 668KB。 4. 够轻量 核心程序仅仅依赖slf4j这一个包，没有之一！ 5.好扩展 Ehcache提供了对大数据的内存和硬盘的存储，最近版本允许多实例、保存对象高灵活性、提供LRU、LFU、FIFO淘汰算法，基础属性支持热配置、支持的插件多 6.监听器 缓存管理器监听器 （CacheManagerListener）和 缓存监听器（CacheEvenListener）,做一些统计或数据一致性广播挺好用的 如何使用？ 够简单就是Ehcache的一大特色，自然用起来just so easy!   redis  redis是在memcache之后编写的，大家经常把这两者做比较，如果说它是个key-value store 的话但是它具有丰富的数据类型，我想暂时把它叫做缓存数据流中心，就像现在物流中心那样，order、package、store、classification、distribute、end。现在还很流行的LAMP PHP架构 不知道和 redis+mysql 或者 redis + mongodb的性能比较（听群里的人说mongodb分片不稳定）。 先说说reidis的特性  1. 支持持久化      redis的本地持久化支持两种方式：RDB和AOF。RDB 在redis.conf配置文件里配置持久化触发器，AOF指的是redis没增加一条记录都会保存到持久化文件中（保存的是这条记录的生成命令），如果不是用redis做DB用的话还会不要开AOF ，数据太庞大了，重启恢复的时候是一个巨大的工程！ 2.丰富的数据类型     redis 支持 String 、Lists、sets、sorted sets、hashes 多种数据类型,新浪微博会使用redis做nosql主要也是它具有这些类型，时间排序、职能排序、我的微博、发给我的这些功能List 和 sorted set   的强大操作功能息息相关 3.高性能    这点跟memcache很想象，内存操作的级别是毫秒级的比硬盘操作秒级操作自然高效不少，较少了磁头寻道、数据读取、页面交换这些高开销的操作！这也是NOSQL冒出来的原因吧，应该是高性能   是基于RDBMS的衍生产品，虽然RDBMS也具有缓存结构，但是始终在app层面不是我们想要的那么操控的。 4.replication     redis提供主从复制方案，跟mysql一样增量复制而且复制的实现都很相似，这个复制跟AOF有点类似复制的是新增记录命令，主库新增记录将新增脚本发送给从库，从库根据脚本生成记录，这个过程非常快，就看网络了，一般主从都是在同一个局域网，所以可以说redis的主从近似及时同步，同事它还支持一主多从，动态添加从库，从库数量没有限制。 主从库搭建，我觉得还是采用网状模式，如果使用链式（master-slave-slave-slave-slave·····）如果第一个slave出现宕机重启，首先从master  接收 数据恢复脚本，这个是阻塞的，如果主库数据几TB的情况恢复过程得花上一段时间，在这个过程中其他的slave就无法和主库同步了。   5.更新快    这点好像从我接触到redis到目前为止 已经发了大版本就4个，小版本没算过。redis作者是个非常积极的人，无论是邮件提问还是论坛发帖，他都能及时耐心的为你解答，维护度很高。有人维护的话，让我们用的也省心和放心。目前作者对redis 的主导开发方向是redis的集群方向。  所以如果希望简单就用ehcache，如果开发任务比较复杂，希望得到比较多的支持什么的就redis 

4.**Share**  

<<锋利的jquery>> 松哥推荐的

https://t.zsxq.com/UvZNVZ7  来自知识星球某位大佬的分享 计算机基础知识



