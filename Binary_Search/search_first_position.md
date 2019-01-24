# Question

- lintcode [Search Insert Position](https://www.lintcode.com/problem/search-insert-position/description)

## 题目描述

### Description

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume **NO** duplicates in the array.

### Example

`[1,3,5,6]`, 5 → 2

`[1,3,5,6]`, 2 → 1

`[1,3,5,6]`, 7 → 4

`[1,3,5,6]`, 0 → 0

### Challenge

O(log(n)) time

## 题解

题目中要求的时间复杂度为$O(logn)$，那么对于该题解能够想到的方法就是使用二分查找。

### python

```python
class Solution:
    """
    @param A: an integer sorted array
    @param target: an integer to be inserted
    @return: An integer
    """
    def searchInsert(self, A, target):
        # 这个就是最基本的二分搜索查找算法，
        # 但是自己不一定能够写的出来
        
        # 先处理异常情况
        m = len(A)
        if m < 1:
            return 0
            
        lb, ub = -1, len(A)
        
        while lb +1 < ub:
            mid = ub + (lb-ub) // 2
            if A[mid] < target:
                lb = mid
            elif A[mid] == target:
                return mid
            else:
                ub = mid
        
        return lb+1
```

### 复杂度分析

> 时间上，利用了二分搜索，因此时间复杂度为$O(logn)$.
>
> 空间上，申请的额外空间为$O(1)$

