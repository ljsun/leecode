# Question

- leecode: [Merge Sorted Array](https://leetcode-cn.com/problems/merge-sorted-array/)

## 问题描述

给定两个有序整数数组 *nums1 *和 *nums2*，将 *nums2 *合并到 *nums1 *中*，*使得 *num1 *成为一个有序数组。

**说明:**

- 初始化 *nums1* 和 *nums2* 的元素数量分别为 *m* 和 *n*。
- 你可以假设 *nums1 *有足够的空间（空间大小大于或等于 *m + n*）来保存 *nums2* 中的元素。

**示例:**

```
输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]
```

## 题解

首先这道题的重点在于不能够申请额外的数组空间，nums1需要in-place修改。想到的思路就是从后向前修改nums1，同时用另外两根指针分别指向nums1和nums2

### python

这个版本是按照上面的思路，自己写的。感觉写的比较繁琐，也比较“丑陋”

```python
class Solution:
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: void Do not return anything, modify nums1 in-place instead.
        """
        
        
        # 首先数组的最终长度是确定的，而且两个数组都是有序的
        # 我们可以先安排倒数第一个元素位置，再安排倒数第二个元素位置，依次类推
        
        # 处理异常情况
        if m < 1:
            for i in range(n):
                nums1[i] = nums2[i]
        elif n < 1:
            pass
        else:
            for i in range(m+n-1, -1, -1):
                # 现在决定nums1[i]的位置的值
                if m - 1 < 0:
                    nums1[i] = nums2[n-1]
                    n -= 1
                    
                elif n - 1 < 0:
                    break
                    
                elif nums1[m-1] < nums2[n-1]:
                    nums1[i] = nums2[n-1]
                    n -= 1
                elif nums2[n-1] <= nums1[m-1]:
                    nums1[i] = nums1[m-1]
                    m -= 1
```

下面这个版本是借鉴别人的，写的就比较简单直接

```python
class Solution:
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: void Do not return anything, modify nums1 in-place instead.
        """
        
        
        # 首先数组的最终长度是确定的，而且两个数组都是有序的
        # 我们可以先安排倒数第一个元素位置，再安排倒数第二个元素位置，依次类推
        
        # 处理异常情况
        # 上面这个思路是对的，但是写的有点乱，使用另一种写法
        if n < 1:
            return
        index = m + n -1
        while m > 0 and n > 0:
            if nums1[m-1] < nums2[n-1]:
                nums1[index] = nums2[n-1]
                n -= 1
            else:
                nums1[index] = nums1[m-1]
                m -= 1
            index -= 1

        # 出while循环有两种情况，m=0 或者 n=0
        while n > 0:
            nums1[index] = nums2[n-1]
            index -= 1
            n -= 1
```

### 复杂度分析

> 时间上，遍历了一次数组，因此时间复杂度为$O(m+n)$
>
> 空间上，原始的数组空间为$O(m+n)$，额外的空间为$O(1)$

