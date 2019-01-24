# Question

- Leecode [寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

## 题目描述

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 `[0,1,2,4,5,6,7]` ****可能变为 `[4,5,6,7,0,1,2]` )。

请找出其中最小的元素。

你可以假设数组中不存在重复元素。

**示例 1:**

```
输入: [3,4,5,1,2]
输出: 1
```

**示例 2:**

```
输入: [4,5,6,7,0,1,2]
输出: 0
```

## 题解

这道题能想到的思路就是利用二分搜索寻找旋转数组的断点

### python 

```python
class Solution:
    def findMin(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # 找最小值，感觉就是寻找旋转排序数组的断点
        
        # 处理异常情况
        if not nums:
            return None
        m = len(nums)
        if m == 0:
            return None
        if m == 1:
            return nums[0]

        # 二分法寻找断点
        lb, ub = 0, len(nums)-1
        while lb+1 < ub:
            mid = lb + (ub-lb) // 2
            if nums[mid] > nums[lb]:
                lb = mid
            else:
                ub = mid
        
        # 判断出while循环时的情况
        # 1. 最普通的情况，lb为最大元素、ub为最小元素
        # 2. 三个或者三个以上元素时，出现１、２、３这种只有递增没有递减时
        #    lb指向第二大元素，ub指向最大元素
        
        if nums[lb] > nums[ub]:
            return nums[ub]
        else:
            return nums[0]
```

### 复杂度分析

> 时间上，使用二分搜索，时间复杂度为$O(logn)$
>
> 空间上，使用的额外空间为$O(1)$

