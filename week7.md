## 左耳听风ARTS第七周（2019年11月24日） 

 1.**Algorithm** 

来源力扣官网第二题

No2.

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：

输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807

解答：

```
class example2 {
    public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {

        ListNode node = new ListNode(0);
        ListNode p = l1, q = l2, curr = node;
        int carry = 0;

        while (null != p && null != q) {

            int x = (null != p) ? p.val : 0;
            int y = (null != q) ? q.val : 0;

            int sum = carry + x + y;
            carry = sum / 10;

            curr.next = new ListNode(sum % 10);  //如果结果是两位数，各位数留在结果链表里
            curr = curr.next;

            if (p != null) {
                p = p.next;
            }

            if (q != null) {
                q = q.next;
            }
            if (carry > 0) {
                curr.next = new ListNode(carry);
            }

        }
        return node.next;
    }
}
```

2.**Review** 

上周主要是熟悉项目，本周做了一个SSO统一权限验证和电子签名上传。主要是对filter和 Interceptor配置不了解，JSP打断点调试不熟练 ，搞了三天才弄好。下周开始要慢慢熟练开发的模式了

3.**Tips**  

## 过滤器

Servlet中的过滤器Filter是实现了javax.servlet.Filter接口的服务器端程序，主要的用途是过滤字符编码、做一些业务逻辑判断等。其工作原理是，只要你在web.xml文件配置好要拦截的客户端请求，它都会帮你拦截到请求，此时你就可以对请求或响应(Request、Response)统一设置编码，简化操作；同时还可以进行逻辑判断，如用户是否已经登录、有没有权限访问该页面等等工作，它是随你的web应用启动而启动的，只初始化一次，以后就可以拦截相关的请求，只有当你的web应用停止或重新部署的时候才能销毁。

在javax.servlet.Filter接口中定义了3个方法：

void init(FilterConfig filterConfig) 用于完成过滤器的初始化

void destroy() 用于过滤器销毁前，完成某些资源的回收

void doFilter(ServletRequest request, ServletResponse response,FilterChain chain) 实现过滤功能，该方法对每个请求增加额外的处理

## 监听器

Servlet的监听器Listener，它是实现了javax.servlet.ServletContextListener接口的服务器端程序，它也是随web应用的启动而启动，只初始化一次，随web应用的停止而销毁。主要作用是：做一些初始化的内容添加工作、设置一些基本的内容、比如一些参数或者是一些固定的对象等等。

在javax.servlet.ServletContextListener接口中定义了2种方法：

void contextInitialized(ServletContextEvent sce) 监听器的初始化

void contextDestroyed(ServletContextEvent sce) 监听器销毁

## 拦截器

拦截器是在面向切面编程中应用的，就是在你的service或者一个方法前调用一个方法，或者在方法后调用一个方法比如动态代理就是拦截器的简单实现，在你调用方法前打印出字符串（或者做其它业务逻辑的操作），也可以在你调用方法后打印出字符串，甚至在你抛出异常的时候做业务逻辑的操作。拦截器不是在web.xml配置的，比如struts在struts.xml配置，在springMVC在[spring](https://link.zhihu.com/?target=http%3A//lib.csdn.net/base/javaee)与springMVC整合的配置文件中配置。

在springmvc中，定义拦截器要实现HandlerInterceptor接口，并实现该接口中提供的三个方法

preHandle方法：进入Handler方法之前执行。可以用于身份认证、身份授权。比如如果认证没有通过表示用户没有登陆，需要此方法拦截不再往下执行（return false），否则就放行（return true）。

postHandle方法：进入Handler方法之后，返回ModelAndView之前执行。可以看到该方法中有个modelAndView的形参。应用场景：从modelAndView出发：将公用的模型数据（比如菜单导航之类的）在这里传到视图，也可以在这里同一指定视图。

afterCompletion方法：执行Handler完成之后执行。应用场景：统一异常处理，统一日志处理等。

在springmvc中，拦截器是针对具体的HandlerMapping进行配置的，也就是说如果在某个HandlerMapping中配置拦截，经过该 HandlerMapping映射成功的handler最终使用该拦截器。

 在网上查询的过滤器和拦截器的区别，基本都是以下一模一样的5行话。
1、拦截器是基于[Java](https://link.zhihu.com/?target=http%3A//lib.csdn.net/base/java)的反射机制的，而过滤器是基于函数回调
2、过滤器依赖与servlet容器，而拦截器不依赖与servlet容器
3、拦截器只能对action请求起作用，而过滤器则可以对几乎所有的请求起作用
4、拦截器可以访问action上下文、值栈里的对象，而过滤器不能
5、在action的生命周期中，拦截器可以多次被调用，而过滤器只能在容器初始化时被调用一次

执行顺序：过滤前 - 拦截前 - Action处理 - 拦截后 -过滤后。个人认为过滤是一个横向的过程，首先把客户端提交的内容进行过滤(例如未登录用户不能访问内部页面的处理)；过滤通过后，拦截器将检查用户提交数据的验证，做一些前期的数据处理，接着把处理后的数据发给对应的Action；Action处理完成返回后，拦截器还可以做其他过程，再向上返回到过滤器的后续操作。

过滤器（Filter）：当你有一堆东西的时候，你只希望选择符合你要求的某一些东西。定义这些要求的工具，就是过滤器。
拦截器（Interceptor）：在一个流程正在进行的时候，你希望干预它的进展，甚至终止它进行，这是拦截器做的事情。
监听器（Listener）：当一个事件发生的时候，你希望获得这个事件发生的详细信息，而并不想干预这个事件本身的进程，这就要用到监听器。

URL：<https://www.cnblogs.com/heqiyoujing/p/11142815.html> 

4.**Share**  

公众号 《纯洁的微笑》（强哥） ，做过第三方支付的研发副总，搞过一些小项目 目前是自由职业者

<http://www.ityouknow.com/> 