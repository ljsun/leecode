# Question

- leecode [求众数](https://leetcode-cn.com/problems/majority-element/)

## 题目描述

给定一个大小为 *n *的数组，找到其中的众数。众数是指在数组中出现次数**大于** `⌊ n/2 ⌋` 的元素。

你可以假设数组是非空的，并且给定的数组总是存在众数。

## 题解

具体的分析思路在代码注释中。。因此可以用“两两抵消”的思路来做

### python

```python
class Solution:
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # 处理异常情况
        if nums is None or len(nums) == 0:
            return -1
        # 思路１：使用hash表记录每一个数出现的次数
#         hashMap = dict()
#         length = len(nums)
#         for num in nums:
#             if num in hashMap:
#                 hashMap[num] += 1
#             else:
#                 hashMap[num] = 1
            
#             # 判断次数
#             if hashMap[num] >= (length//2 + 1):
#                 return num
            
        # 思路２：题目中其实有一个很隐晦的条件，【给定的数组总是存在众数】
        key, count = -1, 0
        for num in nums:
            if count == 0:
                key = num
            if key == num:
                count += 1
            else:
                count -= 1
        
        return key
```

### 复杂度分析

> 时间上，思路１与思路２的复杂度都为$O(N)$
>
> 空间上，思路１的复杂度为$O(N)$，思路２的复杂度为$O(1)$

