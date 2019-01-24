# Question

- lintcode: [Subarray Sum Closest](https://www.lintcode.com/problem/subarray-sum-closest/description)

## 题目描述

### Description

Given an integer array, find a subarray with sum closest to zero. Return the indexes of the first number and last number.

### Example

Given `[-3, 1, 1, -3, 5]`, return `[0, 2]`, `[1, 3]`, `[1, 1]`, `[2, 2]` or `[0, 4]`.

### Challenge

O(nlogn) time

## 题解１－暴力遍历

该题的目的是找到和最接近０的子串，那么最先想到的就是“笨方法”就是遍历数组中所有可能的子串

### python(TLE) 

```python
class Solution:
    """
    @param: nums: A list of integers
    @return: A list of integers includes the index of the first number and the index of the last number
    """
    def subarraySumClosest(self, nums):
        if len(nums) < 2:
            return [0, 0]
        gap_to_zero = 100000
        for i in range(len(nums)):
            curr_sum = 0
            for j in range(i, len(nums)):
                curr_sum += nums[j]
                curr_gap = abs(curr_sum-0)
                if curr_gap < gap_to_zero:
                    gap_to_zero = curr_gap
                    return_index = [i, j]
        
        return return_index
```

### 复杂度分析

> 首先两个嵌套的for循环，时间复杂度的最高幂指数为2。因此时间复杂度为$O(n^2)$
>
> 空间上，原始数组所占空间为$O(n)$，额外空间为$O(1)$

## 题解２－排序

其实这道题和zero_sum_subarray这道题有点类似，zero_sum_subarray的其中一个题解思路就是先排序，再遍历，这个思路完全可以用在这道题中。

### python(ACE) 

```python
class Solution:
    """
    @param: nums: A list of integers
    @return: A list of integers includes the index of the first number and the index of the last number
    """
    def subarraySumClosest(self, nums):
        # 想想怎么利用hashmap
        
        # 貌似hashmap的方法不再适用
        # 那么先进行排序呢？貌似可以
        if len(nums) < 2:
            return [0, 0]
        sum_i = []
        curr_sum = 0
        for i in range(len(nums)):
            curr_sum += nums[i]
            sum_i.append([curr_sum, i])
        
        # 然后对sum_i进行排序
        sum_i.sort(key=lambda x:x[0])
        
        # 遍历排序后的sum_i
        min_gap = 10000000
        for i in range(len(sum_i)-1):
            #　判断f(i)和f(i+1)的差值
            curr_gap = abs(sum_i[i][0] - sum_i[i+1][0])
            if curr_gap < min_gap:
                min_gap = curr_gap
                return_index = [min(sum_i[i][1], sum_i[i+1][1])+1, max(sum_i[i][1], sum_i[i+1][1])]
        return return_index
```

### 复杂度分析

> 先遍历一次数组求和的复杂度为$O(n)$，对sum_i进行排序的复杂度为$O(nlogn)$，最后再次遍历sum_i的复杂度为$O(n)$
>
> 空间上，原始数组的空间复杂度为$O(n)$，申请的额外数组sum_i的空间复杂度为$O(n+n)$

