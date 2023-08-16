344 反转字符串
自己的思路：读取数组的lens 写一个for循环 让i所在的元素去和lens-1-i所在的元素进行替换    但感觉不太行的通 因为在进行之后的替换时 前面的元素已经被更新为新的元素
应该用双指针法
定义两个指针 一个从字符串前面 一个从字符串后面 两个指针同时向中间移动 交换元素

也可以使用切片的方法：s[:] = s[::-1]  -1表示反转




541 反转字符串II
在遍历字符串的过程中，只要让 i += (2 * k)，i 每次移动 2 * k 就可以了，然后判断是否需要有反转的区间  也就是找每个2k区间的起点
range（）用法：range(start, stop[, step])  分别表示起始位置和步长
join() 方法用于将序列中的元素以指定的字符连接生成一个新的字符串。
class Solution:
    def reverseStr(self, s: str, k: int) -> str:

        def reverse_substring(text):
            left, right = 0, len(text) - 1
            while left < right:
                text[left], text[right] = text[right], text[left]
                left += 1
                right -= 1
            return text
            
        res = list(s)

        for i in range(0 , len(s), 2*k):
            res[i:i+k] = reverse_substring(res[i:i+k])

        return ''.join(res)





05 替换空格
首先扩充数组到每个空格替换成"%20"之后的大小。

然后从后向前替换空格，也就是双指针法，过程如下：

i指向新长度的末尾，j指向旧长度的末尾。
很多数组填充类的问题，都可以先预先给数组扩容带填充后的大小，然后在从后向前进行操作。

这么做有两个好处：

不用申请新数组。
从后向前填充元素，避免了从前向后填充元素时，每次添加元素都要将添加元素之后的所有元素向后移动的问题。

class Solution:
    def replaceSpace(self, s: str) -> str:
        counter = s.count(' ')
        
        res = list(s)
        # 每碰到一个空格就多拓展两个格子，1 + 2 = 3个位置存’%20‘
        res.extend([' '] * counter * 2)
        
        # 原始字符串的末尾，拓展后的末尾
        left, right = len(s) - 1, len(res) - 1
        
        while left >= 0:
            if res[left] != ' ':
                res[right] = res[left]
                right -= 1
            else:
                # [right - 2, right), 左闭右开
                res[right - 2: right + 1] = '%20'
                right -= 3
            left -= 1
        return ''.join(res)






151 翻转字符串里的单词
可以使用split库函数，分隔单词，然后定义一个新的string字符串，最后再把单词倒序相加   但这种方法使用辅助空间

如果空间复杂度要求为O(1)，则使用以下方法：
移除多余空格，将整个字符串反转，将每个单词反转

strip() 方法用于移除字符串头尾指定的字符（默认为空格或换行符）或字符序列
split() 通过指定分隔符对字符串进行切片，如果参数 num 有指定值，则分隔 num+1 个子字符串






58 左旋转字符串
如果不能申请额外空间，只能在本串上操作
具体步骤为：

反转区间为前n的子串
反转区间为n到末尾的子串
反转整个字符串
最后就可以达到左旋n的目的，而不用定义新的字符串，完全在本串上操作。








