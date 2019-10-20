# 左耳听风ARTS第二周（2019年10月13日）

[ARTS第一周]
Algorithm
https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/comments/
3. 无重复字符的最长子串 - 力扣（LeetCode）
​ 解答:(C++)
	class Solution {
	public:
		int lengthOfLongestSubstring(string s) {
			
			int  size,i=0,j,k,max=0;
			size = s.size();
			for(j = 0;j<size;j++){
				for(k = i;k<j;k++)
					if(s[k]==s[j]){
						i = k+1;
						break;
					}
				if(j-i+1 > max)
					max = j-i+1;
			}
			return max;
		}
	};


主要就是定几个参数 和变量 去统计已输入字符串中每个字母出现的次数,重复就继续下一次循环,计数器不变 ,未出现的字母则进行计数再循环.最后遍历完成输出结果.
Share
https://blog.csdn.net/qq_33673359/article/details/82692533
​
blog.csdn.net
Redis 集群的哨兵模式讲解和搭建可以按照步骤尝试
Tips:
本周主要是搭建vhr项目,参照江南一点雨github上面的说明说.前端采用的是vue+element-ui 对于vue的数据绑定和路由又有了一定的认识
Review:
主要是参照了spring5的源码介绍,详见<<Spring5 核心原理与30个类手写实战>>.