## 左耳听风ARTS第七周（2019年11月30日）

 1.**Algorithm** （No.24）

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

 

示例:

给定 1->2->3->4, 你应该返回 2->1->4->3.



解答：

（1）递归接法

class Solution {

​    public ListNode swapPairs(ListNode head) {

​    if(head == null || head.next == null){

​            return head;

​        }

​        ListNode next = head.next;

​        head.next = swapPairs(next.next);

​        next.next = head;

​        return next;

​       }

} 



2.**Review** 

本周是上班的第三周 也是这个月的月底。主要开发了sso接口和OA对接接口。其实也就是crud 多事都是查询返回参数。没有写什么前端页面，

但是对于代码的把握和熟练度还不够要多敲代码。

3.**Tips**  

最近开始看王争的新专栏<<设计模式之美>>  主要还是java写的代码 目前还是比较基础的讲解，有兴趣的小伙伴可以订阅。

4.**Share**  

**redis 的主从复制及哨兵模式**

## 什么是主从复制

就是主机的数据更新后，根据redis的主从复制的配置方式，自动的将数据同步更新到从机上，使用的机制是master/slaver ,master一般以写操作为主，而slaver一般以读操作为主

## 主从复制能干嘛

主从复制可以用来进行读写分离和容灾恢复

## 主从复制的配置

### 1.配从不配主

从库连接主库的方式

```
slaveof 主库的ip 主库的端口
```

###### 注意：

1. 

每当从库与主库失去连接后，需要重新连接，除非你在从库的redis.config 配置文件中配如下配置：

1. 

每次当主机宕机以后，从机会原地待命等待和主机的连接，当主机恢复以后自动连接上主机

```

```

3.当主机宕机以后，从机想要变成主机首先，在想要变成主级的从机上执行

```
slaveof no one
```

然后在其他从机上重新连接新的主机如

```
slaveof ip 端口
```

## 哨兵模式（sentinel）

当主机宕机以后，不在以slave on one 的方式，而是以投票的方式，从从机中选出一个主机。 哨兵模式是重新启动的一个新的单独的进程。可以通过配置文件指定其端口号

#### 使用方式

第一步：在redis的根目录，也就是配置文件的目录下，新建一个文件sentinel.conf的文件。

第二步：修改sentinel.conf文件

```
#指定端口
port 26379
#添加保护模式
protected-mode no
sentinel monitor 被监控的数据库名   127.0.0.1 6379 1
```

最后的1表示最低通过的票数，当主机宕机后，从机自动投票看由谁接替master的位置。

第三步：启动哨兵

1. linux项目下进入redis 的目录

```
redis-sentinel sentinel.conf
```

1. win项目下 进入redis 的目录

```
redis-server sentinel.conf --sentinel
```