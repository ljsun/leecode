# Question

- leecode [求众数２](https://leetcode-cn.com/problems/majority-element-ii/)

## 题目描述

给定一个大小为 *n *的数组，找出其中所有出现超过 `⌊ n/3 ⌋` 次的元素。

**说明: **要求算法的时间复杂度为 O(n)，空间复杂度为 O(1)。

## 题解

既然题目中的要求是空间复杂度为$O(1)$，那么就不能使用哈希表来做。就只能在“两两抵消”的基础上使用“三三抵消”来做。。。

具体的想法是：由于要找出所有出现超过[n / 3]次的元素，分析知这样的元素最多不会超过３个。。先利用“三三抵消”思想找出候选的结果，然后再遍历一次数组，确定最终的结果。

**注意代码中繁琐的if条件**

### python

```python
class Solution:
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        
        # 处理异常情况
        if nums is None or len(nums) == 0:
            return []
        
        # 思路１：利用hashMap计算每个数出现的次数【在《求众数》中已经实现】
        
        # 思路２：分析题可得到，超过[n/3]的元素最多不超过２个
        # 所以先根据《求众数》中的抵消法找出可能为最终结果的两个数
        # 然后再判断这两个数数是否满足最终的结果要求
        
        key1, count1 = -1, 0
        key2, count2 = -1, 0
        
        for num in nums:
            if count1 == 0 and num != key2:
                key1 = num
                count1 += 1
                continue
            if count2 == 0 and num != key1:
                key2 = num
                count2 += 1
                continue
            
            if key1 == num:
                count1 += 1
                continue
            
            if key2 == num:
                count2 += 1
                continue
            
            count1 -= 1
            count2 -= 1
        
        # 判断key1, key2是否满足结果要求
        result = []
        count1, count2 = 0, 0
        for num in nums:
            if key1 == num:
                count1 += 1
            elif key2 == num:
                count2 += 1
        
        threshold = len(nums) // 3
        
        if count1 > threshold:
            result.append(key1)
        if count2 > threshold and key1 != key2:
            result.append(key2)
            
        return result
```

### 复杂度分析

> 时间上，遍历两次数组，复杂度为$O(N)$
>
> 空间上，额外的空间复杂度为$O(1)$

