# Learning_Record DAY1
数组是存放在连续内存空间上的相同类型数据的集合，可以方便的通过下标索引的方式获取到下标下对应的数据
注意：
     数组下标都会从0开始的
     数组内存空间的地址是连续的
所以在删除和添加元素时，就要移动其他元素的地址
数组的元素是不能被删除的 只能被覆盖掉

a[0][1] = 1; 其中[0]表示行 为第一索引， [1]表示列 为第二索引
二维数组在地址空间上也是连续的




LEETCODE 704 实战

Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.

You must write an algorithm with O(log n) runtime complexity.

 

Example 1:

Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
Example 2:

Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1

刚拿到这个题 明白是什么意思 但并没有一定的思路 在此记录一下学习心得：

题目中 数组为有序数组 并且无重复 (二分法适用前提)   说明使用二分法

什么是二分查找：二分查找的基本思想是将n个元素分成大致相等的两部分，取a[n/2]与x做比较，如果x=a[n/2],则找到x,算法中止；如果x<a[n/2],则只要在数组a的左半部分继续搜索x,如果x>a[n/2],则只要在数组a的右半部搜索x.
时间复杂度即是while循环的次数。

写二分法一定要注意区间问题 考虑好区间之后再去写
写二分法，区间的定义一般为两种，左闭右闭即[left, right]，或者左闭右开即[left, right)

二分法第一种写法
第一种写法，我们定义 target 是在一个在左闭右闭的区间里，也就是[left, right] （这个很重要非常重要）。
区间的定义这就决定了二分法的代码应该如何写，因为定义target在[left, right]区间，所以有如下两点：
while (left <= right) 要使用 <= ，因为left == right是有意义的，所以使用 <=
if (nums[middle] > target) right 要赋值为 middle - 1，因为当前这个nums[middle]一定不是target，那么接下来要查找的左区间结束下标位置就是 middle - 1

二分法第二种写法
如果说定义 target 是在一个在左闭右开的区间里，也就是[left, right) ，那么二分法的边界处理方式则截然不同。
有如下两点：
while (left < right)，这里使用 < ,因为left == right在区间[left, right)是没有意义的
if (nums[middle] > target) right 更新为 middle，因为当前nums[middle]不等于target，去左区间继续寻找，而寻找区间是左闭右开区间，所以right更新为middle，即：下一个查询区间不会去比较nums[middle]


len() 方法返回对象（字符、列表、元组等）长度或项目个数。即转换为数组下标





27 移除元素

只想到了暴力解法 并且想得不够全面

这里采用新方法：双指针法！！（快慢指针法）：通过一个快指针和慢指针在一个for循环下完成两个for循环的工作。
定义快慢指针

快指针：寻找新数组的元素 ，新数组就是不含有目标元素的数组
慢指针：指向更新 新数组下标的位置

即采用快指针先遍历数据，符合新数组的的元素存在慢指针中




