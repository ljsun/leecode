# Question

- leecode [寻找两个有序数组的中位数](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)

## 问题描述

给定两个大小为 m 和 n 的有序数组 `nums1` 和 `nums2`。

请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。

你可以假设 `nums1` 和 `nums2` 不会同时为空。

**示例 1:**

```
nums1 = [1, 3]
nums2 = [2]

则中位数是 2.0

```

**示例 2:**

```
nums1 = [1, 2]
nums2 = [3, 4]

则中位数是 (2 + 3)/2 = 2.5
```

## 题解1

比较笨的思想就是将两个有序数组合并为１个有序数组，然后求中位数

### python

```python
class Solution:
    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        #　思路１，增加额外的排序数组空间
        
        # 先处理异常情况
        if (nums1 is None or len(nums1) == 0) and (nums2 is None or len(nums2) == 0):
            return -1
        
        nums1_length = 0 if nums1 is None else len(nums1)
        nums2_length = 0 if nums2 is None else len(nums2)
        
        c = []
        
        index1, index2 = 0, 0
        while(index1 < nums1_length and index2 < nums2_length):
            if nums1[index1] < nums2[index2]:
                c.append(nums1[index1])
                index1 += 1
            else:
                c.append(nums2[index2])
                index2 += 1
            
            
        # 当nums1中还保留元素时
        while(index1 < nums1_length):
            c.append(nums1[index1])
            index1 += 1
        
        # 当nums2中还保留元素时
        while(index2 < nums2_length):
            c.append(nums2[index2])
            index2 += 1
            
        total_length = nums1_length + nums2_length
        
        if total_length % 2 == 0:
            return (c[total_length//2] + c[total_length//2-1]) / 2
        else:
            return c[total_length//2]
```

### 复杂度分析

> 时间上，遍历了两个数组，时间复杂度为$O(m+n)$
>
> 空间上，使用了额外的空间$O(m+n)$

## 题解２

## 题解３

