## 左耳听风ARTS第十二周（2020年03月22日）

 1.**Algorithm** （面试题）

 编写一个截取字符串的函数，输入为一个字符串和字节数，输出为按字节截取的字符串。 但是要保证汉字不被截半个，如“我ABC”4，应该截为“我AB”，输入“我ABC汉DEF”，6，应该输出为“我ABC”而不是“我ABC+汉的半个”。

```
答：
public  static void fun(String src, int num) throws Exception {

    int  byteNum=0;
    if(null == src){
        System.out.println("The source String is null!");
        return;
    }

    byteNum=src.length();
    byte[] bt=src.getBytes("GB2312");

    if(num > byteNum){
        num =  byteNum;
    }

    if(bt[num] <0){
        String subStrx = new String(bt, 0, --num);
        System.out.println("subStrx1==" + subStrx);
    } else {
        String subStrx = new String(bt, 0, num);
        System.out.println("subStrx1==" + subStrx);
    }
 }
```

 2.**Review** 
答：三周的内容一起写吧，开始面试了  然后发现难度变大了 好好复习！

3.**Tips**  

**mysql与oracle的优缺点：**

优点：

开放性：[**oracle**](http://lib.csdn.net/base/oracle) 能所有主流平台上运行（包括 windows）完全支持所有工业标准采用完全开放策略使客户选择适合解决方案对开发商全力支持；

可伸缩性,并行性：Oracle 并行服务器通过使组结点共享同簇工作来扩展windownt能力提供高用性和高伸缩性簇解决方案windowsNT能满足需要用户把数据库移UNIXOracle并行服务器对各种UNIX平台集群机制都有着相当高集成度；

安全性：获得最高认证级别的ISO标准认证。 

性能：Oracle 性能高 保持开放平台下TPC-D和TPC-C世界记录；

客户端支持及应用模式：Oracle 多层次网络计算支持多种工业标准用ODBC、JDBC、OCI等网络客户连接 

使用风险：Oracle 长时间开发经验完全向下兼容得广泛应用地风险低 

缺点：

对硬件的要求很高；

价格比较昂贵；

管理维护麻烦一些；

操作比较复杂，需要技术含量较高；

\---------------------------------------------------------

优点：

体积小、速度快、总体拥有成本低，开源；

支持多种操作系统；

是开源数据库，提供的接口支持多种语言连接操作

[**mysql**](http://lib.csdn.net/base/mysql)的核心程序采用完全的多线程编程。线程是轻量级的进程，它可以灵活地为用户提供服务，而不过多的系统资源。用多线程和[**C语言**](http://lib.csdn.net/base/c)实现的MySql能很容易充分利用CPU；

MySql有一个非常灵活而且安全的权限和口令系统。当客户与MySql服务器连接时，他们之间所有的口令传送被加密，而且MySql支持主机认证；

支持ODBC for Windows， 支持所有的ODBC 2.5函数和其他许多函数， 可以用Access连接MySql服务器， 使得应用被扩展；

支持大型的数据库， 可以方便地支持上千万条记录的数据库。作为一个开放源代码的数据库，可以针对不同的应用进行相应的修改。

拥有一个非常快速而且稳定的基于线程的内存分配系统，可以持续使用面不必担心其稳定性； 

MySQL同时提供高度多样性，能够提供很多不同的使用者介面，包括命令行客户端操作，网页浏览器，以及各式各样的程序语言介面，例如C+，Perl，[**Java**](http://lib.csdn.net/base/java)，[**PHP**](http://lib.csdn.net/base/php)，以及[**Python**](http://lib.csdn.net/base/python)。你可以使用事先包装好的客户端，或者干脆自己写一个合适的应用程序。MySQL可用于Unix，Windows，以及OS/2等平台，因此它可以用在个人电脑或者是服务器上；

缺点：

不支持热备份；

MySQL最大的缺点是其安全系统，主要是复杂而非标准，另外只有到调用mysqladmin来重读用户权限时才发生改变；

没有一种存储过程(Stored Procedure)语言，这是对习惯于企业级数据库的程序员的最大限制；

MySQL的价格随平台和安装方式变化。[**Linux**](http://lib.csdn.net/base/linux)的MySQL如果由用户自己或系统管理员而不是第三方安装则是免费的，第三方案则必须付许可费。Unix或[**linux**](http://lib.csdn.net/base/linux) 自行安装 免费 、Unix或Linux 第三方安装 收费；



4.**Share**  

杀死占用的端口号:

netstat -ano|findstr "****"

tasklist|findstr "####"

taskkill /pid #### /F

