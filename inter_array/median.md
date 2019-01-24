# Question

- lintcode: [Median](https://www.lintcode.com/problem/median/description)

## 题目描述

### Description

Given a unsorted array with integers, find the median of it.

A median is the middle number of the array after it is sorted.

If there are even numbers in the array, return the `N/2`-th number after sorted.

Problem Correction

### Example

Given `[4, 5, 1, 2, 3]`, return `3`.

Given `[7, 9, 4, 5]`, return `5`.

### Challenge

O(n) time.

## 题解１

首先自己想到的笨方法就是利用python自带的排序方法对原数组进行排序，然后直接利用索引求中位数。

### python

```python
class Solution:
    """
    @param nums: A list of integers
    @return: An integer denotes the middle number of the array
    """
    def median(self, nums):
        m = len(nums)
        if m < 1:
            return None
        
        nums.sort()
        
        return nums[(m-1)//2]
```

### 复杂度分析

> python中对sort方法使用的是高大上的Timsort排序方法，best case is $O(n)$，Average case is $O(nlogn)$，Worst case is $O(nlogn)$
>
> 空间上timsort的空间复杂度为$O(n)$

## 题解２

在这个题解中，我是想着不用别人集成好的排序方法，而是自己写排序方法。当然最后自己也没写出来，是看了billryan的讲解才知道怎么写的。。。

### python

```python
class Solution:
    """
    @param nums: A list of integers
    @return: An integer denotes the middle number of the array
    """
    
    def median(self, nums):
        # 刚才是用了别人的排序方法，现在不用，只用自己的排序方法
        # 看了billryan的讲解，发现使用快速排序比较适用于这道题
        
        # 首先处理异常情况
        m = len(nums)
        if m < 1:
            return None
        
        return self.kth(nums, 0, m-1, (m+1)//2)
     
    def kth(self, nums, left, right, k):
        # 找kth大的数
        
        if left >= right:
            return nums[left]
        
        m = left
        
        for i in range(left+1, right+1):
            if nums[i] < nums[left]:
                m += 1
                temp = nums[i]
                nums[i] = nums[m]
                nums[m] = temp
        
        temp = nums[left]
        nums[left] = nums[m]
        nums[m] = temp
        
        if m+1 == k:
            return nums[m]
        
        elif m+1 < k:
            return self.kth(nums, m+1, right, k)
        
        else:
            return self.kth(nums, left, m-1, k)

```

### 复杂度分析

> 时间上，把所有的情况平均时，快排的基值位于中间位置，即每次递归需要遍历的数组元素都减半，因此总的时间复杂度为$O(n(1+1/2+1/4+...))=O(2n)$，那么相应的最坏情况下，每次递归后需要遍历的数组元素只减１，此时复杂度就接近平方。
>
> 空间上，使用临时变量，额外的空间复杂度为$O(1)$