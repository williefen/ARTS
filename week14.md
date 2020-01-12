## 左耳听风ARTS第十二周（2020年01月12日）

 1.**Algorithm** （No.5）（NO.27）

Given an array and a value, remove all instances of that value in place and return the new length.
Do not allocate extra space for another array, you must do this in place with constant memory.
The order of elements can be changed. It doesn't matter what you leave beyond the new length.
Example:
Given input array nums =  [3,2,2,3] , val =  3
Your function should return length = 2, with the first two elements of nums being 2.
public class Solution {
public int removeElement(int[] nums, int val) {
int cur;
int j = 0;
for(int i = 0;i < nums.length; ++i) {
cur = nums[i];
if(val != cur) {
nums[j] = cur;
++j;
}
}
return j;
}
}

 2.**Review** 

本周是在家复习并完成vhr的第2周，感觉自觉性这块比较差 加上又是过年 暗都没心思学。主要还是前端这块不熟悉啊... 加油 小伙伴们。

3.**Tips**  

Flink 基础学习(六)时间 Time 和 Watermark 

https://mp.weixin.qq.com/s/WW3sHLljWQQDrxZB3-qSbg


你应该知道的 PriorityQueue ——深入浅出分析 PriorityQueue   
https://mp.weixin.qq.com/s/zxKpTL0bG0MqK1IXfxxBhw

Flink 基础学习之窗口 Window  
https://mp.weixin.qq.com/s/ZLUtpyTMv5po7mYeMl2rHQ

原生线程池这么强大，Tomcat 为何还需扩展线程池？  
https://mp.weixin.qq.com/s/ZNqluItJ6Qqrupzv0tg8vQ

一文带你深入理解 HTTP 的秘密。。。   
https://mp.weixin.qq.com/s/kOw-z_Z7NC_D8RPLCxO1dA

Kafka 进阶必备之控制器   
https://mp.weixin.qq.com/s/oP3_85cUlb98QhbV4t118w



4.**Share**  

https://www.java3.cn/article/46.html 

程序员应该干的八件事：

https://mp.weixin.qq.com/s/hBhJtFWGjvV48TtOJBTeVg



