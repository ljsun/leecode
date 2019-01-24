# Question

- leecode [只出现一次的数字２](https://leetcode-cn.com/problems/single-number-ii/)

## 题目描述

给定一个**非空**整数数组，除了某个元素只出现一次以外，其余每个元素均出现了三次。找出那个只出现了一次的元素。

**说明：**

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

**示例 1:**

```
输入: [2,2,3,2]
输出: 3

```

**示例 2:**

```
输入: [0,1,0,1,0,1,99]
输出: 99
```

## 题解

这道题两个思路，其一是利用hashmap，其二是利用位运算。【位运算的还没想明白】

### python

```python
class Solution:
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # 。。。利用位操作的方法仍未想明白，还是利用额外的数组空间吧
        
        # 使用额外的hash空间，统计每个数字出现的次数
        
        if nums is None or len(nums) == 0:
            return -1
        
        hash_map = dict()
        
        for num in nums:
            if num in hash_map:
                hash_map[num] += 1
            else:
                hash_map[num] = 1
        
        for key, value in hash_map.items():
            if value == 1:
                return key
```

### 复杂度分析

> 时间上，遍历两次数组，复杂度为$O(2n)$
>
> 空间上，使用额外的hashmap空间，额外空间为$O(2n)$