## 左耳听风ARTS第十二周（2020年1月05日）

 1.**Algorithm** （No.5）（NO.26）

Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.
Do not allocate extra space for another array, you must do this in place with constant memory.
For example,
Given input array nums =  [1,1,2] ,
Your function should return length =  2 , with the first two elements of nums being  1 and  2 respectively. It doesn't matter what you
leave beyond the new length.

解答：

public class Solution {
public int removeDuplicates(int[] nums) {
Integer temp = null, cur = null;
int j = 0;
for(int i = 0;i < nums.length; ++i) {
cur = nums[i];
if(temp == null || temp.intValue() != cur.intValue()) {
nums[j] = cur;
++j;
}
temp = cur;
}
return j;
}
}

 2.**Review** 

本周是在家复习并完成vhr的第一周，也是2020年第一周 再接再厉吧。对于vue +Element ui要多敲练习才能领悟其中的语法 先入门然后再研究其原理。。

3.**Tips**  

# spring控制反转IOC之实现--依赖注入--依赖查找+依赖拖拽



1.控制反转(Inversion of Control)与依赖注入(Dependency Injection)

控制反转即IoC (Inversion of Control)，它把传统上由程序代码直接操控的对象的调用权交给容器，通过容器来实现对象组件的装配和管理。所谓的“控制反转”概念就是对组件对象控制权的转移，从程序代码本身转移到了外部容器。

IoC是一个很大的概念，可以用不同的方式来实现。其主要实现方式有两种：<1>依赖查找（Dependency Lookup）：容器提供回调接口和上下文环境给组件。EJB和Apache Avalon都使用这种方式。<2>依赖注入（Dependency Injection）：组件不做定位查询，只提供普通的Java方法让容器去决定依赖关系。后者是时下最流行的IoC类型，其又有接口注入（Interface Injection），设值注入（Setter Injection）和构造子注入（Constructor Injection）三种方式。

![img](https://img-blog.csdn.net/20180320213948579?watermark/2/text/Ly9ibG9nLmNzZG4ubmV0L3FxXzE2NjkxNTMx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

图1 控制反转概念结构

依赖注入之所以更流行是因为它是一种更可取的方式：让容器全权负责依赖查询，受管组件只需要暴露JavaBean的setter方法或者带参数的构造子或者接口，使容器可以在初始化时组装对象的依赖关系。其与依赖查找方式相比，主要优势为：<1>查找定位操作与应用代码完全无关。<2>不依赖于容器的API，可以很容易地在任何容器以外使用应用对象。<3>不需要特殊的接口，绝大多数对象可以做到完全不必依赖容器。

 

2.好莱坞原则

IoC体现了好莱坞原则，即“不要打电话过来，我们会打给你”。第一次遇到好莱坞原则是在了解模板方法(Template Mathod)模式的时候，模板方法模式的核心是，基类（抽象类）定义了算法的骨架，而将一些步骤延迟到子类中。

![img](https://img-blog.csdn.net/20180320214022139?watermark/2/text/Ly9ibG9nLmNzZG4ubmV0L3FxXzE2NjkxNTMx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

图2 模板方法模式类图

 

现在来考虑IoC的实现机制，组件定义了整个流程框架，而其中的一些业务逻辑的实现要借助于其他业务对象的加入，它们可以通过两种方式参与到业务流程中，一种是依赖查找（Dependency Lookup），类似与JDNI的实现，通过JNDI来找到相应的业务对象（代码1），另一种是依赖注入，通过IoC容器将业务对象注入到组件中。

 

3. 依赖查找（Dependency Lookup）

下面代码展示了基于JNDI实现的依赖查找机制。

 

```
public class MyBusniessObject{



  private DataSource ds;



  private MyCollaborator myCollaborator;



 



  public MyBusnissObject(){



Context ctx = null;



try{



    ctx = new InitialContext();



    ds = (DataSource) ctx.lookup(“java:comp/env/dataSourceName”);



    myCollaborator =



 (MyCollaborator) ctx.lookup(“java:comp/env/myCollaboratorName”);



    }……
```

代码1依赖查找（Dependency Lookup）代码实现

依赖查找的主要问题是，这段代码必须依赖于JNDI环境，所以它不能在应用服务器之外运行，并且如果要用别的方式取代JNDI来查找资源和协作对象，就必须把JNDI代码抽出来重构到一个策略方法中去。

 

4. 依赖注入（Dependency Injection）

依赖注入的基本原则是：应用组件不应该负责查找资源或者其他依赖的协作对象。配置对象的工作应该由IoC容器负责，“查找资源”的逻辑应该从应用组件的代码中抽取出来，交给IoC容器负责。

下面分别演示3中注入机制。

代码2 待注入的业务对象Content.java

MyBusniess类展示了一个业务组件，它的实现需要对象Content的注入。代码3，代码4，代码5，6分别演示构造子注入（Constructor Injection），设值注入（Setter Injection）和接口注入（Interface Injection）三种方式。

 

代码3构造子注入（Constructor Injection）MyBusiness.java

 

代码4设值注入（Setter Injection） MyBusiness.java

 

代码5 设置注入接口InContent.java

 

代码6接口注入（Interface Injection）MyBusiness.java

 

5.依赖拖拽(Dependency Pull)

最后需要介绍的是依赖拖拽，注入的对象如何与组件发生联系，这个过程就是通过依赖拖拽实现。

代码7 依赖拖拽示例

而通常对注入对象的配置可以通过一个xml文件完成。

使用这种方式对对象进行集中管理，使用依赖拖拽与依赖查找本质的区别是，依赖查找是在业务组件代码中进行的，而不是从一个集中的注册处，特定的地点执行。

4.**Share**  

<Mysql必知必会> 推荐一下



