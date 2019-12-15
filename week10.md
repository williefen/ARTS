## 左耳听风ARTS第十周（2019年12月15日）

 1.**Algorithm** （No.4）（NO.9）

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

示例 1:

输入: 121
输出: true
示例 2:

输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
示例 3:

输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
进阶:

你能不将整数转为字符串来解决这个问题吗？

class Solution {

​    public boolean isPalindrome(int x) {

​        

​         if(x < 0 || (x % 10 == 0 && x != 0)) {

​            return false;

​        }

 

​        int revertedNumber = 0;

​        while(x > revertedNumber) {

​            revertedNumber = revertedNumber * 10 + x % 10;

​            x /= 10;

​        }

 

​        // 当数字长度为奇数时，我们可以通过 revertedNumber/10 去除处于中位的数字。

​        // 例如，当输入为 12321 时，在 while 循环的末尾我们可以得到 x = 12，revertedNumber = 123，

​        // 由于处于中位的数字不影响回文（它总是与自己相等），所以我们可以简单地将其去除。

​        return x == revertedNumber || x == revertedNumber/10;

​     }

}

 

2.**Review** 

本周是上班的第四周 是十二月第二周。主要开发了修改了更改了东莞一中的验收内容。打印表单和修改表单的格式 然后是验收管理合并节点 写了一个监听 这些都是jeccg这个框架分配的 码云上面有这个框架可以学习一下。

但是对于代码的把握和熟练度还不够要多敲代码。

3.**Tips**  

ZooKeeper  相关概念分享  

Dubbo 通过注册中心在分布式环境中实现服务的注册与发现，而注册中心通常采用 ZooKeeper，研究注册中心相关源码绕不开 ZooKeeper，所以学习了 ZooKeeper 的基本概念以及相关 API 操作。  ZooKeeper 相关概念  session 客户端与服务端采用 TCP 长连接，服务端在为客户端创建 Session 会分配一个唯一 sessionId。在 Session timeout 时间内，客户端可以向服务端发送请求以及接受 watcher 事件通知。  数据结构 Zookeeper 将所有数据存储在内存中，数据模型是一棵树（Znode Tree)，由斜杠（/）的进行分割的路径，就是一个Znode，例如/foo/path1。  图1  Znode Znode 将会保存数据内容以及相关属性信息。在 Znode 中使用 Stat 数据结保存相关属性信息。Stat 属性中有三种版本信息，分别为 version：当前节点版本信息，cversion:当前节点子节点版本，aversion 当前节点的 ACL 版本。每次发生改动，版本数值将会单调递增。  更新，删除 Znode 可以传入版本数值，如果版本数值不对，将会导致删除/更新失败，这个特性类似于 CAS 操作。  Znode 有以下几种类型：  永久节点 一旦创建，将会一直存在，除非手动删除。dubbo 目录节点为永久节点。  临时节点  临时节点基于客户端 Session,Session 有效期内将会一直存在，Session 失效，节点将会自动删除。  利用这个机制，Dubbo 服务者创建的节点就是临时节点。如果 Dubbo 服务者程序意外宕机，在 Session 超时之后，也能自动删除服务节点，自动下线有问题的服务。  3 顺序节点  创建顺序节点将会自动在名字后追加整形数字，默认长度为 10 位。顺序节点也分为永久与临时。  利用临时顺序节点，我们可以用来实现分布式锁 。  Watcher 机制  客户端可以在指定节点注册监听器（Watcher），在触发特定事件后，ZooKeeper 服务端会将事件通知到客户端。在 Dubbo 中消费者基于 watcher 机制可以动态感知到新的服务者加入。  ZooKeeper 可以在三种请求中设置监听，分别为：  getData()，获取节点数据 getChildren() 获取子节点 exists() 判断节点是否存在 通知事件类型分为，增删改事件，以及子节点变动事件。  需要注意的是，watcher 通知过一次之后将会失效，若想继续监听通知，需要重新注册。   #知识分享

![img](https://images.zsxq.com/FlF0KzRaMOTpgUhWKCEjBvUs2sQk?imageMogr2/auto-orient/thumbnail/540x/format/jpg/blur/1x0/quality/75&e=1580486399&token=kIxbL07-8jAj8w1n4s9zv64FuZZNEATmlU_Vm6zD:i3euw5rqZblpGoAYt55gSFMigLA=)

4.**Share**  



https://t.zsxq.com/UvZNVZ7  来自知识星球某位大佬的分享 计算机基础知识



