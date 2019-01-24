# Question

- lintcode [First Postion of Target](https://www.lintcode.com/problem/first-position-of-target/description)

## 题目描述

### Description

For a given sorted array (ascending order) and a `target` number, find the first index of this number in `O(log n)` time complexity.

If the target number does not exist in the array, return `-1`.

Problem Correction

### Example

If the array is `[1, 2, 3, 3, 4, 5, 10]`, for given target `3`, return `2`.

### Challenge

If the count of numbers is bigger than 2^32, can your code work properly?

## 题解

其实这道题首先想到的就是二分搜索查找，但是发现自己仅仅只知道二分查找的原理。。。代码还很不熟。。因此这方面还是要细看

### python

```
class Solution:
    """
    @param nums: The integer array.
    @param target: Target to find.
    @return: The first position of target. Position starts from 0.
    """
    def binarySearch(self, nums, target):
        if nums is None or len(nums) == 0:
            return -1
            
        
        start, end = -1, len(nums)
        
        while start+1 < end:
            mid = start + (end-start)//2
            
            if nums[mid] < target:
                start = mid
            else:
                end = mid
        
        if nums[end] != target or end == len(nums):
            return -1
        
        else:
            return end
```

### 复杂度分析

> 时间上，二分查找时间复杂度为$O(logn)$
>
> 空间上，使用了额外的空间，额外空间复杂度为$O(1)$

