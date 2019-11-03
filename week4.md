# 左耳听风ARTS第二周（2019年11月3日）
1.**Algorithm**
本次分享的还是来自于面试题：
public class Examination {

    /**
     * 找出数组中以bywh开头的字符串，并将找出的字符串转成小写，然后将转换后的字符串去重（比如有多个字符串是bywhtec,则只保留一个）
     * 最后将去重后的字符串排序后输出 该函数返回排序后的字符串
     * @param arr1
     * @return
     */
    public  static  String [] exam1(String [] arr1){

        String []sortedArr=null;
        List<String> collect = Arrays.stream(arr1).collect(Collectors.toList());
        for (int i = 0; i < collect.size(); i++) {
            String s = collect.get(i);
            if(!(s.indexOf("bywh") == 0)) {
                collect.remove(i);
                i--;
            } else {
                collect.set(i, s.toLowerCase());
//                it.remove();
            }
        }
        Set<String> sorted = new HashSet<>(collect);
        sortedArr = new String[sorted.size()];
        sorted.toArray(sortedArr);
//        System.out.println(sorted);
        return  sortedArr;
    }

    /*
     * 数组arr2中的元素下标偶数位为编码下标 奇数位为名称 请将数组arr1中的编码对应的名称打印出原来，arr1中的编码可在arr2中查询 （数组arr1有点问题）
     */
    public static  void  exam2(String [] arr1,String [] arr2){
        for (String a1 : arr1) {
            int arr2Length = arr2.length;
            for (int j = 0; j < arr2Length; j++) {
                String a2 = arr2[j];
                if (a1.toLowerCase().equals(a2.toLowerCase())) {
                    if (j + 1 < arr2Length) {
                        System.out.println(arr2[j + 1]);
                        break;
                    }
                }
            }
        }

    }

    /**
     * 请将arr1中的数字字符串筛选出来进行求和并打印出来；
     * @param arr1
     */
    public static  void  exam3(String [] arr1){
        int sum = 0;
        for (String s : arr1) {
            boolean flag = true;
            for (int i = 0; i < s.length(); i++) {
                if (!Character.isDigit(s.charAt(i))) {
                    flag = false;
                    break;
                }
            }
            if (flag) {
                sum += Integer.parseInt(s);
            }
        }
        System.out.println(sum);
    }

    public static void main(String[] args) {
        String[] arr1={"bywhTec","skfIrst","bywhwoRld","789","aBcd","bywhhEllo","bywhtEc","thRipoi","sdfirst","666", "secOnd","123","456","bywhTec"};
        String[] arr2={"bywhtec","博越文化","bywhhello","你好","bywhworld","世界","sdfirst","第一"};
        String[] sortedArr=exam1(arr1);

        System.out.println(Arrays.toString(sortedArr));
        System.out.println("===============");
        exam2(sortedArr,arr2);
        System.out.println("===============");
        exam3(arr1);
    }
}

主要是第一次上机测试，用的Eclipse 有点方 做的不甚理想。。。。

2.**Review**

   本周面试了大大小小几家公司 ，发现现在对人员的水平要求也变高了，索引要研读一下耗子叔的<<程序员练级攻略侧>>
   以及面试技巧等，感觉自己实战经验缺乏 这块也需要加强训练。

3.**Tip**
 （1）jdbc配置多个环境切换命令：java -jar XXX.jar --spring.proﬁles.active=dev

  (2)redis主从和redis集群的区别
 主从概念:
⼀个master可以拥有多个slave，⼀个slave⼜可以拥有多个slave，如此下去，形成了强⼤的多级服务器集群架构
master用来写数据，slave用来读数据，经统计：网站的读写比率是10:1
通过主从配置可以实现读写分离
 主从配置:  配置主服务器(master):====>redis.conf
集群是一组相互独立的、通过高速网络互联的计算机，它们构成了一个组，并以单一系统的模式加以管理。一个客户与集群相互作用时，集群像是一个独立的服务器。集群配置是用于提高可用性和可缩放性。 当请求到来首先由负载均衡服务器处理，把请求转发到另外的一台服务器上。
主从服务器分工明确，主服务器用来写，从服务器用来读，一个主服务器，多个从服务器；集群就好比，多个主从服务器，子，比如：全国有多个主从服务器，分别处理各自区域的信息，这样可以减少单个主从服务器中主服务器的压力。


4.**Share**
 还是那句话 有机会的话还是不建议选择外包，耗子数的专栏里面也写过这块描述，对自己要早做规划吧！！！