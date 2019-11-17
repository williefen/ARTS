## 左耳听风ARTS第六周（2019年11月17日）

 1.**Algorithm**

本周分享的算法题来自题库。
NO.1
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1]. 即返回对应求和元素的下标。

法一：此题第一种办法就是暴力枚举，O(n^2)

class function(){

```
public static void main(String[] args) {
    int[] result=twoSum(new int[]{2, 7, 11, 15},18);
        for (int arr:result){
        System.out.println(arr);
       
    }
       // 第二种打印方式
        System.out.println(IntStream.of(arr).boxed().collect(Collectors.toList()))；
 }   
     public static   int[] twoSum(int[] nums, int target) {
            int []arr=new int[2];
            for (int i = 0; i <nums.length; i++) {
                // j = i + 1 的目的是减少重复计算和避免两个元素下标相同
                for (int j = i + 1; j < nums.length; j++) {
                    if (nums[j] == target - nums[i]) {
                      //  arr= new int[]{i, j};
                        arr[0]=i;
                        arr[1]=j;
                        return  arr;
                    }
                }
            }
            return arr;
    }
```



法二：优化的算法来此网上教学：

class solution{

```
  public static int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> m = new HashMap();
        for (int i = 0; i < nums.length; ++i) {
            int num = target - nums[i];
            if (m.containsKey(num)) {
                return new int[]{m.get(num), i};
            }
            m.put(nums[i], i);
        }
       throw new RuntimeException("no answer!");
    }
}
```

}

2.**Review** 

本周回顾，由于是入职的第一周还在熟悉项目，所以对于之前的知识没怎么复习。主要是熟悉公司的框架和业务。做的是一个采购管理系统，东西比较多 杂乱。对于前端的要求比较多，js和easyUI。

3.**Tips** 

EhCache 是一个纯Java的进程内缓存框架，具有快速、精干等特点，是Hibernate中默认CacheProvider。Ehcache是一种广泛使用的开源Java分布式缓存。主要面向通用缓存,Java EE和轻量级容器。它具有内存和磁盘存储，缓存加载器,缓存扩展,缓存异常处理程序,一个gzip缓存servlet过滤器,支持REST和SOAP api等特点。

Spring 提供了对缓存功能的抽象：即允许绑定不同的缓存解决方案（如Ehcache），但本身不直接提供缓存功能的实现。它支持注解方式使用缓存，非常方便。

## ehcache 和 redis 比较

- ehcache直接在jvm虚拟机中缓存，速度快，效率高；但是缓存共享麻烦，集群分布式应用不方便。
- redis是通过socket访问到缓存服务，效率比ecache低，比数据库要快很多， 
  处理集群和分布式缓存方便，有成熟的方案。如果是单个应用或者对缓存访问要求很高的应用，用ehcache。如果是大型系统，存在缓存共享、分布式部署、缓存内容很大的，建议用redis。

ehcache也有缓存共享方案，不过是通过RMI或者Jgroup多播方式进行广播缓存通知更新，缓存共享复杂，维护不方便；简单的共享可以，但是涉及到缓存恢复，大数据缓存，则不合适。

4.**Share** 

"菜鸟教程" 是新人学习的不错的网站 有很多前端的知识

松哥的博客可以关注一下 : http://www.javaboy.org

