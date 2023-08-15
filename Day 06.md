454 四数相加
算法：自己没有想到如何使用哈希算法
首先定义 一个unordered_map，key放a和b两数之和，value 放a和b两数之和出现的次数。
遍历大A和大B数组，统计两个数组元素之和，和出现的次数，放到map中。
定义int变量count，用来统计 a+b+c+d = 0 出现的次数。
在遍历大C和大D数组，找到如果 0-(c+d) 在map中出现过的话，就用count把map中key对应的value也就是出现次数统计出来。
最后返回统计值 count 就可以了


字典是另一种可变容器模型，且可存储任意类型对象。
字典的每个键值 key:value 对用冒号 : 分割，每个键值对之间用逗号 , 分割，整个字典包括在花括号 {} 中 


class Solution(object):
    def fourSumCount(self, nums1, nums2, nums3, nums4):
        # 使用字典存储nums1和nums2中的元素及其和
        hashmap = dict()
        for n1 in nums1:
            for n2 in nums2:
                if n1 + n2 in hashmap:                       先将两个数组的和储存在哈希表中，再计算另外两个数组中各元素的和 如果它们的负数已经存在与哈希表中，则count直接等于哈希表中该数出现的次数
                    hashmap[n1+n2] += 1                      即为不同组合求和所得结果为0的组合数
                else:
                    hashmap[n1+n2] = 1
        
        # 如果 -(n1+n2) 存在于nums3和nums4, 存入结果
        count = 0
        for n3 in nums3:
            for n4 in nums4:
                key = - n3 - n4
                if key in hashmap:
                    count += hashmap[key]
        return count






383 赎金信
因为题目所只有小写字母，那可以采用空间换取时间的哈希策略， 用一个长度为26的数组还记录magazine里字母出现的次数。
然后再用ransomNote去验证这个数组是否包含了ransomNote所需要的所有字母。
依然是数组在哈希法中的应用。

在本题的情况下，使用map的空间消耗要比数组大一些的，因为map要维护红黑树或者哈希表，而且还要做哈希函数，是费时的！数据量大的话就能体现出来差别了。 所以数组更加简单直接有效！
all() 函数用于判断给定的可迭代参数 iterable 中的所有元素是否都为 TRUE，如果是返回 True，否则返回 False

for循环 对于数字 for i in range（数字）
对于字符串 for i in 字符串
ord()函数返回八位ASCII码






15 三数之和
可以使用哈希法 但题目中说不可以包含重复的三元组 把符合条件的三元组放进vector中，然后再去重，这样是非常费时的，很容易超时
这道题目可以使用双指针法
拿这个nums数组来举例，首先将数组排序，然后有一层for循环，i从下标0的地方开始，同时定一个下标left 定义在i+1的位置上，定义下标right 在数组结尾的位置上。
依然还是在数组中找到 abc 使得a + b +c =0， a = nums[i]，b = nums[left]，c = nums[right]。
接下来如何移动left 和right呢， 如果nums[i] + nums[left] + nums[right] > 0 就说明 此时三数之和大了，因为数组是排序后了，所以right下标就应该向左移动，这样才能让三数之和小一些。
如果 nums[i] + nums[left] + nums[right] < 0 说明 此时 三数之和小了，left 就向右移动，才能让三数之和大一些，直到left与right相遇为止。
时间复杂度：O(n^2)。


首先要想到的是要对数组进行排序  同时还要考虑到去重 因为是根据下标进行检索 下标不一样 但元素可能一样。如果排列组合 算是同一种情况 所以要进行去重
continue 语句用来告诉Python跳过当前循环的剩余语句，然后继续进行下一轮循环。






18 四数之和
四数之和与三数之和思路一样 都是使用双指针法 并在此基础上多加一个for循环












