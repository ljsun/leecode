# Question

- lintcode [single number 3](https://www.lintcode.com/problem/single-number-iii/description)

## 问题描述

### Description

Given `2*n + 2` numbers, every numbers occurs twice except two, find them.

Have you met this question in a real interview?  Yes

Problem Correction

### Example

Given `[1,2,2,3,4,4,5,3]` return `1` and `5`

### Challenge

O(n) time, O(1) extra space.

## 题解

这道题两个思路，其一是利用hashmap，其二是利用位运算。关于位运算的讲解可以看yuanbin写的。

### python

```python
class Solution:
    """
    @param A: An integer array
    @return: An integer array
    """
    def singleNumberIII(self, A):
        # write your code here
        
        # deal with exception
        if A is None or len(A) == 0:
            return -1
        
        x1orx2 = 0
        for num in A:
            x1orx2 ^= num
            
        lastbit = x1orx2 - (x1orx2 & (x1orx2-1))
        
        singleone, singletwo = 0, 0
        for num in A:
            if (lastbit & num) == 0:
                singleone ^= num
            else:
                singletwo ^= num
        
        return singleone, singletwo
```

### 复杂度分析

> 时间上，遍历两次数组，时间复杂度为$O(2n)$
>
> 空间上，使用的额外空间为$O(1)$

