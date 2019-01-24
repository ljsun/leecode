# Question

- lintcode [Search for a range](https://www.lintcode.com/problem/search-for-a-range/description)

## 题目描述

### Description

Given a sorted array of *n* integers, find the starting and ending position of a given target value.

If the target is not found in the array, return `[-1, -1]`.

### Example

Given `[5, 7, 7, 8, 8, 10]` and target value `8`,
return `[3, 4]`.

### Challenge

O(log *n*) time.

## 题解

题目中要求时间复杂度为$O(logn)$，能够想到的就是利用两次二分查找，第一次找下界，第二次找上界。

### python

```python
class Solution:
    """
    @param A: an integer sorted array
    @param target: an integer to be inserted
    @return: a list of length 2, [index1, index2]
    """
    def searchRange(self, A, target):
        # 能想到的笨办法就是写两次二分查找
        # 一次找下界，另一次找上届
        
        # 处理异常情况
        m = len(A)
        if m < 1 or A[m-1]<target or A[0]>target:
            return [-1, -1]
        
        left, right = -1, -1
        
        lb, ub = -1, m
        
        while lb+1 < ub:
            mid = lb + (ub-lb) // 2
            if A[mid] < target:
                lb = mid
            else:
                ub = mid
        
        if A[lb+1] != target:
            return[-1, -1]
        else:
            left = lb+1
            
        lb, ub = -1, m
        
        while lb+1 < ub:
            mid = lb + (ub-lb) // 2
            if A[mid] > target:
                ub = mid
            else:
                lb = mid
        
        right = ub-1
    
    
        return [left, right]
```

### 复杂度分析

> 时间上，利用了两次二分搜索，因此时间复杂度为$2logn$，从指数级别来看的话，时间复杂度仍是$O(logn)$
>
> 空间上，申请的额外空间为$O(1)$