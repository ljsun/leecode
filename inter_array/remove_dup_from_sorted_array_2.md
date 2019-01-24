# Question

- leecode [删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array-ii/)

## 题目描述

给定一个排序数组，你需要在**原地**删除重复出现的元素，使得每个元素最多出现两次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在**原地修改输入数组**并在使用 O(1) 额外空间的条件下完成。

**示例 1:**

给定 nums = [1,1,1,2,2,3],

函数应返回新长度 length = 5, 并且原数组的前五个元素被修改为 1, 1, 2, 2, 3 。

你不需要考虑数组中超出新长度后面的元素。

**示例 2:**

给定 nums = [0,0,1,1,1,1,2,3,3],

函数应返回新长度 length = 7, 并且原数组的前五个元素被修改为 0, 0, 1, 1, 2, 3, 3 。

你不需要考虑数组中超出新长度后面的元素。

## 题解

这道题与删除排序数组中的重复项1很类似，但是这道题允许每个元素最多可以出现两次。那么继续删除排序数组中的重复项1的思路，我们如果开始从i=2遍历原数组呢（其实我们根本没想出来，看别人才知道的）？？

### python 

```python
class Solution:
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # 每个元素最多出现两次
        
        # 如果是从i=2开始遍历呢？
        
        # 处理异常情况
        if len(nums) < 3:
            return len(nums)
        
        new_index = 1
        for i in range(2, len(nums)):
            if nums[i] != nums[new_index] or nums[i] != nums[new_index-1]:
                new_index += 1
                nums[new_index] = nums[i]
        
        return new_index+1
```

### 复杂度分析

> 时间上，遍历一次原始数组，因此时间复杂度为$O(N)$
>
> 空间上，原始数组的空间复杂度为$O(N)$，额外的空间复杂度为$O(1)$