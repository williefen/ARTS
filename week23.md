## 左耳听风ARTS第十二周（2020年03月15日）

 1.**Algorithm** （31. 表示数值的字符串 （https://www.acwing.com/problem/content/29/））

请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。

例如，字符串`"+100"`,`"5e2"`,`"-123"`,`"3.1416"`和`"-1E-16"`都表示数值。

但是`"12e"`,`"1a3.14"`,`"1.2.3"`,`"+-5"`和`"12e+4.3"`都不是。

**注意**:

1. 小数可以没有整数部分，例如.123等于0.123；
2. 小数点后面可以没有数字，例如233.等于233.0；
3. 小数点前面和后面可以有数字，例如233.666;
4. 当e或E前面没有数字时，整个字符串不能表示数字，例如.e1、e1；
5. 当e或E后面没有整数时，整个字符串不能表示数字，例如12e、12e+5.4;

#### 样例：

```
输入: "0"

输出: true
```

答： 
class Solution {
public:
    bool isNumber(string s) {
        int i = 0;
        while (i < s.size() && s[i] == ' ') i ++ ;
        int j = s.size() - 1;
        while (j >= 0 && s[j] == ' ') j -- ;
        if (i > j) return false;
        s = s.substr(i, j - i + 1);

        if (s[0] == '-' || s[0] == '+') s = s.substr(1);
        if (s.empty() || s[0] == '.' && s.size() == 1) return false;

        int dot = 0, e = 0;
        for (int i = 0; i < s.size(); i ++ )
        {
            if (s[i] >= '0' && s[i] <= '9');
            else if (s[i] == '.')
            {
                dot ++ ;
                if (e || dot > 1) return false;
            }
            else if (s[i] == 'e' || s[i] == 'E')
            {
                e ++ ;
                if (i + 1 == s.size() || !i || e > 1 || i == 1 && s[0] == '.') return false;
                if (s[i + 1] == '+' || s[i + 1] == '-')
                {
                    if (i + 2 == s.size()) return false;
                    i ++ ;
                }
            }
            else return false;
        }
        return true;
    }
};


链接：https://www.acwing.com/solution/acwing/content/737/

 2.**Review** 
答： 计划下周开始面试 希望疫情早点过去...

3.**Tips**  
答：DevOps（Development和Operations的组合词）是一组过程、方法与系统的统称，用于促进开发（应用程序/软件工程）、技术运营和质量保障（QA）部门之间的沟通、协作与整合。

它是一种重视“软件开发人员（Dev）”和“IT运维技术人员（Ops）”之间沟通合作的文化、运动或惯例。透过自动化“软件交付”和“架构变更”的流程，来使得构建、测试、发布软件能够更加地快捷、频繁和可靠。

它的出现是由于软件行业日益清晰地认识到：为了按时交付软件产品和服务，开发和运营工作必须紧密合作。

从定义来看，其实devops就是为了让开发、运维和QA可以高效协作的流程。（可以把DevOps看作开发、技术运营和质量保障（QA）三者的交集。）

DevOps
DevOps对应用程序发布的影响

在很多企业中，应用程序发布是一项涉及多个团队、压力很大、风险很高的活动。然而在具备DevOps能力的组织中，应用程序发布的风险很低，原因如下 [2] ：

（1）减少变更范围

与传统的瀑布模式模型相比，采用敏捷或迭代式开发意味着更频繁的发布、每次发布包含的变化更少。由于部署经常进行，因此每次部署不会对生产系统造成巨大影响，应用程序会以平滑的速率逐渐生长。

（2）加强发布协调

靠强有力的发布协调人来弥合开发与运营之间的技能鸿沟和沟通鸿沟；采用电子数据表、电话会议和企业门户（wiki、sharepoint）等协作工具来确保所有相关人员理解变更的内容并全力合作。

（3）自动化

强大的部署自动化手段确保部署任务的可重复性、减少部署出错的可能性。


与传统开发方法那种大规模的、不频繁的发布（通常以“季度”或“年”为单位）相比，敏捷方法大大提升了发布频率（通常以“天”或“周”为单位）。

实现DevOps需要什么？

硬性要求：工具上的准备

上文提到了工具链的打通，那么工具自然就需要做好准备。现将工具类型及对应的不完全列举整理如下：

代码管理（SCM）：GitHub、GitLab、BitBucket、SubVersion

构建工具：Ant、Gradle、maven

自动部署：Capistrano、CodeDeploy

持续集成（CI）：Bamboo、Hudson、Jenkins

配置管理：Ansible、Chef、Puppet、SaltStack、ScriptRock GuardRail

容器：Docker、LXC、第三方厂商如AWS

编排：Kubernetes、Core、Apache Mesos、DC/OS

服务注册与发现：Zookeeper、etcd、Consul

脚本语言：python、ruby、shell

日志管理：ELK、Logentries

系统监控：Datadog、Graphite、Icinga、Nagios

性能监控：AppDynamics、New Relic、Splunk

压力测试：JMeter、Blaze Meter、loader.io

预警：PagerDuty、pingdom、厂商自带如AWS SNS

HTTP加速器：Varnish

消息总线：ActiveMQ、SQS

应用服务器：Tomcat、JBoss

Web服务器：Apache、Nginx、IIS

数据库：MySQL、Oracle、PostgreSQL等关系型数据库；cassandra、mongoDB、redis等NoSQL数据库

项目管理（PM）：Jira、Asana、Taiga、Trello、Basecamp、Pivotal Tracker

在工具的选择上，需要结合公司业务需求和技术团队情况而定。（注：更多关于工具的详细介绍可以参见此文：51 Best DevOps Tools for #DevOps Engineers）

软性需求：文化和人

DevOps成功与否，公司组织是否利于协作是关键。开发人员和运维人员可以良好沟通互相学习，从而拥有高生产力。并且协作也存在于业务人员与开发人员之间。

出席了2016年伦敦企业级DevOps峰会的ITV公司在2012年就开始落地DevOps，其通用平台主管Clark在接受了InfoQ的采访，在谈及成功时表示，业务人员非常清楚他们希望在最小化可行产品中实现什么，工程师们就按需交付，不做多余工作。

这样，工程师们使用通用的平台（即打通的工具链）得到更好的一致性和更高的质量。此外，DevOps对工程师个人的要求也提高了，很多专家也认为招募到优秀的人才也是一个挑战。

作者：给你一颗小瓜子
链接：https://www.jianshu.com/p/c5d002cf25b9

4.**Share**  

闲鱼上面MOOC的教程很不错...

知乎刷力扣心得：

https://www.zhihu.com/question/280279208/answer/510354868

