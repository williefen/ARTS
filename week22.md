## 左耳听风ARTS第十二周（2020年03月08日）

 1.**Algorithm** （30. [串联所有单词的子串](https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words/)）

给定一个字符串 s 和一些长度相同的单词 words。找出 s 中恰好可以由 words 中所有单词串联形成的子串的起始位置。

注意子串要与 words 中的单词完全匹配，中间不能有其他字符，但不需要考虑 words 中单词串联的顺序。

示例 1：

输入：
  s = "barfoothefoobarman",
  words = ["foo","bar"]
输出：[0,9]
解释：
从索引 0 和 9 开始的子串分别是 "barfoo" 和 "foobar" 。
输出的顺序不重要, [9,0] 也是有效答案。
示例 2：

输入：
  s = "wordgoodgoodgoodbestword",
  words = ["word","good","best","word"]
输出：[]

答：（暴力双指针）

  vector<int> findSubstring(string s, vector<string>& words) {
        unordered_map<string,int> hash;
        vector<int> res;
        int n = s.length(),m = words.size();
        if(n == 0 || m == 0) return res;
        int len = words[0].length(),end = n - m * len;
        if(n < m * len) return res;
        for(auto word:words)
            hash[word] ++;
        int size = hash.size();
        for(int k = 0;k < len ; k ++)
        {
            unordered_map<string,int> cur_hash;
            int satisfy = 0;
            for(int i = k,j = k;j <= n - len;)
            {
                string cur = s.substr(j,len);
                if(hash.find(cur) == hash.end())
                {
                    j = j + len;
                    i = j;
                    cur_hash.clear();
                    satisfy = 0;
                }else 
                {
                    cur_hash[cur] ++;
                    if(cur_hash[cur] == hash[cur])
                        satisfy ++;
                    else if(cur_hash[cur] > hash[cur])
                    {
                        while(i < j && cur_hash[cur] > hash[cur])
                        {
                            string temp = s.substr(i,len);
                            i += len;
                            cur_hash[temp] --;
                            if(cur_hash[temp] == hash[temp] - 1)
                                satisfy --;
                        }
                    }
                    if(satisfy == size)
                    {
                        string temp = s.substr(i,len);
                        cur_hash[temp] --;
                        satisfy --;
                        res.push_back(i);
                        i = i + len;
                    }
                    j = j + len;
                }
            }
        }
        return res;
    }


链接：https://www.acwing.com/solution/LeetCode/content/3669/

 2.**Review** 
答： 计划下周开始面试 希望疫情早点过去...

3.**Tips**  
答：1. 简介

- Fork/Join 框架是 JDK 1.7 提供的并行执行任务框架，这个框架通过（递归）把问题划分为子任务，然后并行的执行这些子任务，等所有的子任务都结束的时候，再合并最终结果的这种方式来支持并行计算编程。

- 总体的设计参考了为 Cilk 设计的 **work-stealing 框架**。

- Fork/Join 并行方式是获取良好的并行计算性能的一种最简单同时也是最有效的设计技术，是 

  分治算法（Divide-and-Conquer）

   的并行版本。

  - Fork 操作启动一个新的并行 Fork/Join 子任务。
  - Join 操作一直等待直到所有的子任务都结束。
  - Fork/Join 算法，如同其他分治算法一样，总是会递归的、反复的划分子任务，直到这些子任务可以用足够简单的、短小的顺序方法来执行。

# 2. 工作窃取（work-stealing）

- ForkJoin 框架的核心在于轻量级调度机制，使用了 **工作窃取（Work-Stealing）**所采用的基本调度策略。

![img](https:////upload-images.jianshu.io/upload_images/5714666-37899eed4b8098df.png?imageMogr2/auto-orient/strip|imageView2/2/w/381/format/webp)

work-stealing

- 每一个工作线程维护自己的调度队列中的可运行任务。

- 队列以双端队列的形式被维护。

  - 支持后进先出 LIFO 的 push 和 pop 操作。
  - 支持先进先出 FIFO 的 take 操作。

- 对于一个给定的工作线程来说，任务所产生的子任务将会被放入到工作者自己的双端队列中。

- 工作线程使用后进先出 LIFO（最新的元素优先）的顺序，通过弹出任务来处理队列中的任务。

- 当一个工作线程的本地没有任务去运行的时候，它将使用先进先出 FIFO 的规则尝试随机的从别的工作线程中拿（窃取）一个任务去运行。

- 当一个工作线程触及了 Join 操作，如果可能的话它将处理其他任务，直到目标任务被告知已经结束（通过 `isDone()` 方法）。所有的任务都会 **无阻塞** 的完成。

- 当一个工作线程无法再从其他线程中获取任务和失败处理的时候，它就会退出并经过一段时间之后再度尝试直到所有的工作线程都被告知他们都处于空闲的状态。

  - 在这种情况下，他们都会阻塞直到其他的任务再度被上层调用。

- 使用后进先出 LIFO 用来处理每个工作线程的自己任务，但是使用先进先出 FIFO 规则用于获取别的任务，这是一种被广泛使用的进行递归 Fork/Join 设计的一种调优手段

  。

  - 让窃取任务的线程从队列拥有者相反的方向进行操作会减少线程竞争。
  - 同样体现了递归分治算法的大任务优先策略。
  - 更早期被窃取的任务有可能会提供一个更大的单元任务，从而使得窃取线程能够在将来进行递归分解。

- 对于一些基础的操作而言，使用相对较小粒度的任务比那些仅仅使用粗粒度划分的任务以及那些没有使用递归分解的任务的运行速度要快。尽管相关的少数任务在大多数的 Fork/Join 框架中会被其他工作线程窃取，但是创建许多组织良好的任务意味着只要有一个工作线程处于可运行的状态，那么这个任务就有可能被执行。

***工作窃取算法的优点\***

- 利用了线程进行并行计算，减少了线程间的竞争。

***工作窃取算法的缺点\***

- 如果双端队列中只有一个任务时，线程间会存在竞争。
- 窃取算法消耗了更多的系统资源，如会创建多个线程和多个双端队列。

# 3. ForkJoinPool

- ForkJoinPool 类是 

  Fork/Join 框架

   的核心，和 ThreadPoolExecutor 一样是 ExecutorService 接口的实现类。

  - ForkJoinPool 不是为了替代 ExecutorService，而是它的补充，在某些应用场景下性能比 ExecutorService 更好。（见 *[Java Tip: When to use ForkJoinPool vs ExecutorService](http://www.javaworld.com/article/2078440/enterprise-java/java-tip-when-to-use-forkjoinpool-vs-executorservice.html?page=2)* ）

![img](https:////upload-images.jianshu.io/upload_images/5714666-842a238f405cc6bd.png?imageMogr2/auto-orient/strip|imageView2/2/w/577/format/webp)

ForkJoinPool 类图

- ForkJoinPool 的两大核心就是 

  分而治之（Divide-and-Conquer）和工作窃取（Work-Stealing）算法

  。

  - ForkJoinPool 最适合的是计算密集型的任务，如果存在 I/O，线程间同步，`sleep()` 等会造成线程长时间阻塞的情况时，最好配合使用 ManagedBlocker。

## 3.1 Fork/Join 框架的使用

- ThreadPoolExecutor 中每个任务都是由单个线程独立处理的，如果出现一个非常耗时的大任务（比如大数组排序），就可能出现线程池中只有一个线程在处理这个大任务，而其他线程却空闲着，这会导致 CPU 负载不均衡，空闲的处理器无法帮助工作繁忙的处理器。
- ForkJoinPool 可以用来解决这种问题，将一个大任务拆分成多个小任务后，使用 Fork 可以将小任务分发给其他线程同时处理，使用 Join 可以将多个线程处理的结果进行汇总。



链接：https://www.jianshu.com/p/50f814fb5937


4.**Share**  

闲鱼上面MOOC的教程很不错...

图灵学院的vip课感觉讲的很抽象 ，楠哥的直播很不错！o(∩_∩)o 哈哈

