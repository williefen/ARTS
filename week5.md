## 左耳听风ARTS第五周（2019年11月10日）

1.**Algorithm**

本周还是分享一道面试题 来自某公司的笔试题。

https://leetcode-cn.com/problemset/all

提供一个方法在一个不定长的有序非重复随机整数队列list内找出与num的差的绝对值最小且不等于数值num（list不一定含有num）的整数。

List<Integer> findMiniDifferenceNumber(List<Integer>list,int num){

public List<Integer> findMini(List<Integer> list,int num){
    HashMap<Integer,Integer> hlist = new HashMap<>();
    List<Integer> newlist=new ArrayList<>();
    for (int i=0;i<list.size();i++){
        if ( hlist.get(list.get(i))< list.get(i)){
            newlist.add(list.get(i));
          newlist.add(hlist.get(list.get(i)));
            return newlist;
        }
      hlist.put(num-list.get(i),list.get(i));
    }
      return newlist;
}

}

2.**Review**

本周面了三四家公司吧 大抵说来笔试题大多是基础题，算法和数据结构的，需要平时对这方面加强一些。数据库高可用和优化 、Redis的了解到运用 搭建主从集群 、SSM框架的运用的原理等。

3.**Tips**

分布式事务 ，如何实现分布式事务

网站：（<https://www.cnblogs.com/cblogs/p/9432652.html>）

答：分布式事务就是指事务的参与者、支持事务的服务器、资源服务器以及事务管理器分别位于不同的分布式系统的不同节点之上。简单的说，就是一次大的操作由不同的小操作组成，这些小的操作分布在不同的服务器上，且属于不同的应用，分布式事务需要保证这些小操作要么全部成功，要么全部失败。本质上来说，分布式事务就是为了保证不同数据库的数据一致性。

上面说过出现分布式事务的两个原因，其中有个原因是因为微服务过多。我见过太多团队一个人维护几个微服务，太多团队过度设计，搞得所有人疲劳不堪，而微服务过多就会引出分布式事务，这个时候我不会建议你去采用下面任何一种方案，而是请把需要事务的微服务聚合成一个单机服务，使用数据库的本地事务。因为不论任何一种方案都会增加你系统的复杂度，这样的成本实在是太高了，千万不要因为追求某些设计，而引入不必要的成本和复杂度。

在XA协议中分为两阶段:

第一阶段：事务管理器要求每个涉及到事务的数据库预提交(precommit)此操作，并反映是否可以提交.

第二阶段：事务协调器要求每个数据库提交数据，或者回滚数据。

优点： 尽量保证了数据的强一致，实现成本较低，在各大主流数据库都有自己实现，对于MySQL是从5.5开始支持。

对于TCC的解释:

 Try阶段：尝试执行,完成所有业务检查（一致性）,预留必须业务资源（准隔离性）

 Confirm阶段：确认执行真正执行业务，不作任何业务检查，只使用Try阶段预留的业务资源，Confirm操作满足幂等性。要求具备幂等设计，Confirm失败后需要进行重试。

 Cancel阶段：取消执行，释放Try阶段预留的业务资源 Cancel操作满足幂等性Cancel阶段的异常和Confirm阶段异常处理方案基本上一致。

4.**Share**

https://blog.csdn.net/WSRspirit/article/details/81412344

审批流程的详细描述吧