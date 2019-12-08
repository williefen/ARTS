## 左耳听风ARTS第九周（2019年12月7日）

 1.**Algorithm** （No.4）

给定两个大小为 m 和 n 的有序数组 nums1 和 nums2。

请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。

你可以假设 nums1 和 nums2 不会同时为空。

示例 1:

nums1 = [1, 3]
nums2 = [2]

则中位数是 2.0
示例 2:

nums1 = [1, 2]
nums2 = [3, 4]

则中位数是 (2 + 3)/2 = 2.5



解答：

class Solution {

​       public double findMedianSortedArrays (int[] A, int[] B) {

​    int m = A.length;

​    int n = B.length;

​    int len = m + n;

​    int left = -1, right = -1;

​    int aStart = 0, bStart = 0;

​    for (int i = 0; i <= len / 2; i++) {

​        left = right;

​        if (aStart < m && (bStart >= n || A[aStart] < B[bStart])) {

​            right = A[aStart++];

​        } else {

​            right = B[bStart++];

​        }

​    }

​    if ((len & 1) == 0)

​        return (left + right) / 2.0;

​    else

​        return right;

​     }

}

 

2.**Review** 

本周是上班的第三周 也是这个月的月底。主要开发了修改了OA对接接口。其实也就是使用对称秘钥AES加密 用一组公钥解密 然后传参 查数据库返参。

但是对于代码的把握和熟练度还不够要多敲代码。

3.**Tips**  

最近开始看王争的新专栏<<设计模式之美>>  主要还是java写的代码 目前还是比较基础的讲解，有兴趣的小伙伴可以订阅。还有前端的一些技术 送个推荐的<<锋利的jQuery>>

4.**Share**  

公众号 ''芋道源码'' 有兴趣的小伙伴可以关注 有大量面试题 和框架源码解析。



