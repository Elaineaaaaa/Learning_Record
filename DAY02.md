977: 有序数组的平方
采用双指针方法： 快指针遍历数组 并平方 慢指针进行排序
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        fast = 0
        slow = 0
        n = len(nums)

        while fast < n:
            nums[slow] = nums[fast]^2
            fast += 1
            if nums[slow]<nums[slow - 1]:
                nums[slow-1] = nums[slow]
            slow += 1
        return nums[slow]

以上作法不对 完全可以利用 python自带函数 sort（）来进行排序 暴力解法

双指针法的思路是：
在区间左右两端各设置一个指针，比较左右两端的元素平方后的大小，在移动指针进行比较。
float('inf') float('-inf') 分别表示float类型正负无穷
[float（‘inf’）]*len(nums) 表示列表的元素数目及数据类型


补充 ：列表和数组的区别
列表和数组的最大区别就是列表内可以存储任意类型的元素、不论是数字还是字符串、哪怕是集合和字典都能够存储在列表之中。 但是数组只能够用来存储单一类型的数据，如果为整数，那数组内的元素就必须都为整数。

写该题的双指针代码时 一定要注意i l r每个在循环中是加还是减的状态 以及学会如何定义列表
res = [float('inf')] * len(nums) 这里使用这样定义列表的方式 即定义了一个长度与原列表相同的列表
如果使用常规的定义列表的方式 list = [] 这样列表中是没有元素的 会out of range
如果要在这样的列表里填充元素 应该为list.append(' ')








209: 长度最小的子数组
思路为 先用一个循环 遍历整个数组 求每两个元素的和与target相比较 如果没有大于等于target的值 则遍历数组求每三个元素的和 如此循环
但十分复杂麻烦

总体思路不对 如果用暴力解法 应该要：先定义一个最小区间的变量，利用两个for循环，变量i的范围为l = len（nums）； 变量j的范围为（i，l）

滑动窗口：就是不断的调节子序列的起始位置和终止位置，从而得出我们要想的结果。
只使用一个for循环 循环的索引为滑动窗口的终止位置

实现滑动窗口，主要确定如下三点：

窗口内是什么？
如何移动窗口的起始位置？
如何移动窗口的结束位置？
窗口就是 满足其和 ≥ s 的长度最小的 连续 子数组。

窗口的起始位置如何移动：如果当前窗口的值大于s了，窗口就要向前移动了（也就是该缩小了）。

窗口的结束位置如何移动：窗口的结束位置就是遍历数组的指针，也就是for循环里的索引。

class Solution:
    def minSubArrayLen(self, s: int, nums: List[int]) -> int:
        l = len(nums)
        left = 0
        right = 0
        min_len = float('inf')
        cur_sum = 0 #当前的累加值
        
        while right < l:
            cur_sum += nums[right]
            
            while cur_sum >= s: # 当前累加值大于目标值
                min_len = min(min_len, right - left + 1)      只要和大于等于target 就储存金min_len 之后不断循环遍历比较 直到找到最小的len
                cur_sum -= nums[left]                         减去左边的 左边移动 继续往后面寻找其他符合条件的数组
                left += 1
            
            right += 1
        
        return min_len if min_len != float('inf') else 0





59 旋转矩阵
模拟顺时针画矩阵的过程:

填充上行从左到右
填充右列从上到下
填充下行从右到左
填充左列从下到上
由外向内一圈一圈这么画下去。
一定要注意：每画一条边都要坚持一致的左闭右开，或者左开右闭的原则，这样这一圈才能按照统一的规则画下来。  区间的统一性
每一个拐角处的处理规则，拐角处让给新的一条边来继续画。



        nums = [[0] * n for _ in range(n)]
        startx, starty = 0, 0               # 起始点
        loop, mid = n // 2, n // 2          # 迭代次数、n为奇数时，矩阵的中心点
        count = 1                           # 计数

        for offset in range(1, loop + 1) :      # 每循环一层偏移量加1，偏移量从1开始
            for i in range(starty, n - offset) :    # 从左至右，左闭右开
                nums[startx][i] = count
                count += 1
            for i in range(startx, n - offset) :    # 从上至下
                nums[i][n - offset] = count
                count += 1
            for i in range(n - offset, starty, -1) : # 从右至左
                nums[n - offset][i] = count
                count += 1
            for i in range(n - offset, startx, -1) : # 从下至上
                nums[i][starty] = count
                count += 1                
            startx += 1         # 更新起始点
            starty += 1

        if n % 2 != 0 :			# n为奇数时，填充中心点
            nums[mid][mid] = count 
        return nums




        还没有看懂 回去研究！！



        














