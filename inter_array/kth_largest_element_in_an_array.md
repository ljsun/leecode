# Question

- leecode [数组中的第k个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

## 题目描述

在未排序的数组中找到第 **k** 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

**示例 1:**

```
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5

```

**示例 2:**

```
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```

## 题解

这道题其实和前面的一道求中位数的题十分相似，基本的方法就是使用快速排序进行查找。另一种思路是使用堆排序进行查找，但是还没有看。

### python 

```python
class Solution:
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        # 根据题意要找第K个最大的元素，可以使用快速排序的方法
        
        # 处理异常情况
        if len(nums) < 1:
            return None
        
        # 递归的寻找第k个最大的元素
        return self.kth(nums, 0, len(nums)-1, k)
    
    
    def kth(self, nums, left, right, k):
        
        if left >= right:
            return nums[right]
        
        # m的左边代表比nums[left]大的元素，包括m本身指向的元素【此时这些元素并不包括nums[left]本身】
        # m的右边包括比nums[left]小的元素
        m = left
        
        
        for i in range(left+1, right+1):
            if nums[i] > nums[left]:
                m += 1
                nums[m], nums[i] = nums[i], nums[m]
        
        # 将m指向元素与left指向元素交换，很重要
        nums[m], nums[left] = nums[left], nums[m]
        
        # 判断nums[m]是否是第k个最大的元素
        if m+1 == k:
            return nums[m]
        
        elif m+1 > k:
            return self.kth(nums, left, m-1, k)
        
        else:
            return self.kth(nums, m+1, right, k)
            
```

### 复杂度分析

> 时间上，最坏的情况，每查找一次，需要查找的数目只减少１，需要遍历$O(n+n-1+...+1)=O(n^2)$
>
> 平均情况下需要遍历$O(n+n/2+n/4+...+1)=O(2n)=O(n)$.故平均时间复杂度为$O(n)$。
>
> 空间上交换数组的值使用了额外的空间，额外空间复杂度为$O(1)$

