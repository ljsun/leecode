# Question

- Leecode [搜索旋转排序数组２](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/)

## 题目描述

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 `[0,0,1,2,2,5,6]` 可能变为 `[2,5,6,0,0,1,2]` )。

编写一个函数来判断给定的目标值是否存在于数组中。若存在返回 `true`，否则返回 `false`。

**示例 1:**

```
输入: nums = [2,5,6,0,0,1,2], target = 0
输出: true

```

**示例 2:**

```
输入: nums = [2,5,6,0,0,1,2], target = 3
输出: false
```

## 题解

这道题是搜索旋转排序数组的延伸题目。因此在写时要多考虑一种情况　`nums[mid] == nums[lb]`的情况，因为在这种情况下，是不能判断mid元素到底是在哪个部分有序段。此时只能递增lb来缩小搜搜范围

### python

```python
class Solution:
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: bool
        """

        
        # 处理异常情况
        m = len(nums)
        if m < 1:
            return False
        
        # lb, ub本身的位置是判断不到的，但是之间的都能判断的到
        lb, ub = 0, m-1
        while lb+1 < ub:
            mid = lb + (ub-lb) // 2
            # 判断mid元素到底在哪一段
            # 与之前比多了一种nums[mid] == nums[lb]的情况
            if nums[mid] == target:
                return True
            if nums[mid] > nums[lb]:
                if nums[mid] > target and nums[lb] < target:
                    ub = mid
                else:
                    lb = mid
            elif nums[mid] < nums[lb]:
                if nums[mid] < target and nums[ub] > target:
                    lb = mid
                else:
                    ub = mid
            else:
                # 当nums[mid] == nums[lb]时应该怎么办
                lb += 1
        
        # 为什么在这里要判断  nums[lb] == target or nums[ub] == target
        # **感觉应该是由于lb += 1造成的**
        if nums[lb] == target or nums[0] == target or nums[m-1]==target:
            return True
        else:
            return False
```

### 复杂度分析

> 时间上，最坏情况下一直在执行 `lb += 1`，此时最坏时间复杂度为$O(n)$。正常时间复杂度为$O(logn)～O(n)$
>
> 空间上，使用的额外空间为$O(1)$

