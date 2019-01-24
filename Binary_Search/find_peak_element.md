# Question

- leecode [寻找峰值](https://leetcode-cn.com/problems/find-peak-element/)

## 题目描述

峰值元素是指其值大于左右相邻值的元素。

给定一个输入数组 `nums`，其中 `nums[i] ≠ nums[i+1]`，找到峰值元素并返回其索引。

数组可能包含多个峰值，在这种情况下，返回任何一个峰值所在位置即可。

你可以假设 `nums[-1] = nums[n] = -∞`。

**示例 1:**

```
输入: nums = [1,2,3,1]
输出: 2
解释: 3 是峰值元素，你的函数应该返回其索引 2。
```

**示例 2:**

```
输入: nums = [1,2,1,3,5,6,4]
输出: 1 或 5 
解释: 你的函数可以返回索引 1，其峰值元素为 2；
     或者返回索引 5， 其峰值元素为 6。

```

**说明:**

你的解法应该是 *O*(*logN*)时间复杂度的。

## 题解

由于这道题要求的时间复杂度$O(logN)$，因此就想到使用二分搜索来做。分析使用二分搜索应该如何去做。若A[mid] > A[mid-1] && A[mid] > A[mid+1]，那么就可以找到一个peak为A[mid]；若A[mid-1]>A[mid]，那么根据题中条件在mid的左侧必定存在一个peak，为什么呢？假设左侧元素为A[0], A[1], ... , A[mid-1]。如果A[1]~A[mid-1]全部都不是peak，那么必有A[0]>A[1]>A[2] > ...  >A[mid-1]>A[mid]，那么此时A[0]是peak，因此左侧必存在peak。同理得若A[mid+1]>A[mid]，mid右侧必有peak

### python　关于最终出while循环的状态再细想

```python
class Solution:
    def findPeakElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        # 注意nums[-1] = nums[n] = -∞这个条件，
        # 这就说明只要首位元素大于第二个元素，首位元素就是峰值
        # 这是个很重要的假设
        
        # 先判断异常情况
        if not nums:
            return -1
        m = len(nums)
        if m <=1 :
            return 0
        
        # 为什么这里的赋值和之前二分搜索的赋值不太一样，
        # 因为之间的赋值需要让mid可能是首尾元素
        # 但是在这道题的需求中，不用
        l, r = 0, m-1
        while l+1 < r:
            mid = l + (r-l) // 2
            if nums[mid] < nums[mid-1]:
                r = mid
            elif nums[mid] < nums[mid+1]:
                l = mid
            else:
                return mid
            
        # 走到这一步说明了什么？说明l或者r已到达两端
        mid=l if nums[l] > nums[r] else r
        return mid
```

### 复杂度分析

> 时间上，采用二分搜索，复杂度为$O(logN)$
>
> 空间上，申请的额外空间为$O(1)$

