## 左耳听风ARTS第十二周（2020年01月19日）

 1.**Algorithm** 
去重复数组数据，不用 set
将一个无序数组去除重复元素，去重时不能使用 set
package cn.itcast.sort;
import java.util.Arrays;
public class SortAndRemove {
public static void main(String[] args) throws Exception {
final int[] original = new int[]{1, 1, 2, 8, 9, 8, 4, 7, 4, 9, 1};
System.out.println(Arrays.toString(original));
quicksort(original);
System.out.println(Arrays.toString(original));
final int[] unqiue = new int[original.length];
int prev = original[0];
unqiue[0] = prev;
int count = 1;
for (int i = 1; i < original.length; ++i) {
if (original[i] != prev) {
unqiue[count++] = original[i];
}
prev = original[i];
}
System.out.println(Arrays.toString(unqiue));
final int[] compressed = new int[count];
System.arraycopy(unqiue, 0, compressed, 0, count);
System.out.println(Arrays.toString(compressed));
}
private static void quicksort(final int[] values) {
if (values.length == 0) {
return;
}
quicksort(values, 0, values.length - 1);
}
private static void quicksort(final int[] values, final int low,
final int high) {
int i = low, j = high;
int pivot = values[low + (high - low) / 2];
while (i <= j) {
while (values[i] < pivot) {
i++;
}
while (values[j] > pivot) {
j--;
}
if (i <= j) {
swap(values, i, j);
i++;
j--;
}
}
if (low < j) {
quicksort(values, low, j);
}
if (i < high) {
quicksort(values, i, high);
}
}
private static void swap(final int[] values, final int i, final int
j) {
final int temp = values[i];
values[i] = values[j];
values[j] = temp;
}
}

 2.**Review** 

本周是在家复习并完成vhr的第3周，感觉自觉性这块比较差 加上又是过年 暗都没心思学。主要还是前端这块不熟悉啊...  对于debug前端和element树形结构不是懂得很多。还有init方法 学学阿来做笔记

3.**Tips**  
 
Maven介绍和使用：
https://mp.weixin.qq.com/s/FVAFxy0fCQVnhzqvdPTYMQ



4.**Share**  
程序员，请掌握这些核心生存技能
https://mp.weixin.qq.com/s/LJtNmmu9u1cLDeInK9Vp9w



