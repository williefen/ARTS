## 左耳听风ARTS第十二周（2020年02月23日）

 1.**Algorithm** （leecode26）

给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

示例 1:

给定数组 nums = [1,1,2], 

函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 

你不需要考虑数组中超出新长度后面的元素。
示例 2:

给定 nums = [0,0,1,1,1,2,2,3,3,4],

函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。

你不需要考虑数组中超出新长度后面的元素。

答：

class Solution {

  public int removeDuplicates(int[] nums) {

​           for( int i=0;i<nums.length-1;i++){       

​            }  

​       }

}




 2.**Review** 

 本周主要是开发一个鉴权demo框架。对于UsersDetail  、SecurityContextHolder这两个接口有了更深的认识的。

3.**Tips**  

从Spring Security 3.0开始，组件spring-security-corejar包中的内容进行了精简，不再包含任何web应用安全，LDAP或命名空间配置的代码。

**SecurityContextHolder**

最基本的对象，用来存储当前的安全上下文（security context），包含了当前登录的用户信息。默认使用ThreadLocal保存细节信息，因此这些信息对于同一个线程内容调用的方法都是可用的。当用户的请求处理完成后，框架会自动清理线程而不必用户关心。但是由于某些应用由于其对线程的使用方式，并不适合使用ThreadLocal，则需要根据情况，在启动前设置SecurityContextHolder的策略。

在SecurityContextHolder中保存了当前活跃用户的信息。Spring Security使用一个Authentication对象来表示这些信息。在程序的任何地方，都可以用以下代码来获取当前认证用户的信息。

![img](http://5b0988e595225.cdn.sohucs.com/images/20190306/44b64b4d582746988ad601cedaf152f3.png)

**UserDetailsService**

在接口UserDetailService中只有一个方法，接收一个字符串返回一个UserDetails对象，当认证成功后，UserDetails会被用来构造一个Authentication对象保存在SecurityContextHolder中。

![img](http://5b0988e595225.cdn.sohucs.com/images/20190306/394d4a6407d849e2a40f7125e54f3634.png)

UserDetailsService的实现，主要是用来加载用户信息，并向其他组件提供这些信息，并不能进行认证用户的操作，认证的操作由AuthenticationManager完成。

如果用户想自定义一个认证流程，则需要实现AuthenticationProvider接口。

**GrantedAuthority**

Authentication的getAuthorities( )方法返回GrantedAuthority的对象数组。GrantAuthority对象一般由UserDetailsService加载。

**总结**

ScurityContextHolder获取SecurityContext

SecurityContext保存了Authentication以及其他一些请求相关的安全信息

Authentication表示一个认证用户信息

GrantedAuthority表示授予用户的权限信息

UserDetails包含了构建Authentication对象需要的必要信息，这些信息来自于应用的DAO或其他数据源

UserDetailsService根据传入用户名字符串构建一个UserDetails对象

1.2 认证环节

一个基本的认证环节包括：

1.用户输入用户名和密码

2.系统验证用户名密码正确

3.系统获取该用户的角色、权限等信息。

以上三个步骤完成了一个认证过程，在Spring Security中，相应地完成了以下动作：

1.后端获取到用户名和密码并用之生成一个UsernamePasswordAuthenticationToken对象，UsernamePasswordAuthenticationToken是Authentication的一个实现类。

2.token被传入AuthenticationManager的实例中进行校验

3.认证成功后，AuthenticationManager会返回一个Authentication实例，其中包括了用户所有细节信息，包括角色、权限等

通过调用SecurityContextHolder.getContext().setAuthentication(…)建立安全上下文，传入Authentication对象

完成以上过程后，当前用户认证完成。

4.**Share**  

闲鱼上面很多有意思的资料 小伙伴可以了解一下...

