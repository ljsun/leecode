# Quesion

- leecode [删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

## 题目描述

给定一个排序数组，你需要在**原地**删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在**原地修改输入数组**并在使用 O(1) 额外空间的条件下完成。

**示例 1:**

给定数组 nums = [1,1,2], 

函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 

你不需要考虑数组中超出新长度后面的元素。

**示例 2:**

给定 nums = [0,0,1,1,1,2,2,3,3,4],

函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。

你不需要考虑数组中超出新长度后面的元素。

## 题解

首先数组已经排过序了，而且题目中需要原地删除数组，不需要额外的空间。可以使用两根指针，一根用来遍历原始数组，另一根用来记录新的数组。

### python

```python
class Solution:
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # 先判断长度，消除异常情况
        if len(nums) < 2:
            return len(nums)

        # 使用两根指针，一根遍历源数组，一根用来指向新数组
        new_index = 0
        for i in range(1, len(nums)):
            if nums[i] != nums[new_index]:
                new_index += 1
                nums[new_index] = nums[i]
        
        return new_index+1
```

### 复杂度分析

> 时间上，遍历了一次数组，因此时间复杂度为$O(N)$
>
> 空间上，原始数组空间复杂度为$O(N)$，额外的空间复杂度为$O(1)$

