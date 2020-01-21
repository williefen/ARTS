## 左耳听风ARTS第十二周（2020年01月21日）

 1.**Algorithm** （No.6）（NO.28）

Implement strStr().
Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.
public class Solution {
public int strStr(String haystack, String needle) {
if (haystack == null || needle == null)
return -1;
char[] cn = needle.toCharArray();
if (cn.length == 0)
return 0;
char[] ch = haystack.toCharArray();
for (int i = 0; i < ch.length - cn.length + 1; ++i) {
for (int j = 0; j < cn.length; ++j) {
if (ch[i + j] != cn[j])
break;
else if (j == cn.length - 1)
return i;
}
}
return -1;
}

 2.**Review** 

即将过年了，开始搞学成项目。 SSI技术 还有nginx访问静态页面。vhr的权限管理也完成了，在有外键的情况下先删除外键主表的相关记录，才能删从表的相关记录。

3.**Tips**  

ssi是什么？

![1579610454750](C:\Users\adminfeng\AppData\Local\Temp\1579610454750.png)

ssi包含类似于jsp页面中的incluce指令，ssi是在web服务端将include指定 的页面包含在网页中，渲染html网页响
应给客户端 。nginx、apache等多数web容器都支持SSI指令。

4.**Share**  

<Mysql 45讲> 感觉很不错噢，最近又有打卡活动！

