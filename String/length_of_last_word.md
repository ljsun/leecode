# Question

- leetcode: [Length of Last Word](https://leetcode-cn.com/problems/length-of-last-word/)

## 题目描述

给定一个仅包含大小写字母和空格 `' '` 的字符串，返回其最后一个单词的长度。

如果不存在最后一个单词，请返回 0 。

**说明：**一个单词是指由字母组成，但不包含任何空格的字符串。

**示例:**

输入: "Hello World"
输出: 5

## 题解　

首先可能是用python用多了，因此首先想到的方法就是将字符串按照空格分割，然后转化为list。取list中最后一个元素的长度。

### python

```python
class Solution(object):
    def lengthOfLastWord(self, s):
        """
        :type s: str
        :rtype: int
        """
        # 这道题的首先思路是将字符串以空格分隔转化为list
        if len(s) < 1:
            return 0
        s_split = s.split()
        return len(s_split[-1]) if len(s_split) > 0 else 0
```



### 复杂度分析

> 分割字符串时需要遍历一次，因此时间复杂度为$O(n)$
>
> 从存储空间上来看，开辟了新的list存储空间，因此空间复杂度为$O(n + n)$

## 其他思路

首先看到这个题，我感觉正常的思路应该是遍历字符串，然后记录最后记录最后一个word首尾的index。然后相减就得到了最后一个word的长度。

还有一种思路，直接利用强大的正则匹配直接把最后一个word匹配出来。