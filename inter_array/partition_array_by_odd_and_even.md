# Question

- lintcode [Partition Array by Odd and Even](https://www.lintcode.com/problem/partition-array-by-odd-and-even/description)

## 题目描述

### Description

Partition an integers array into odd number first and even number second.

Problem Correction

### Example

Given `[1, 2, 3, 4]`, return `[1, 3, 2, 4]`

### Challenge

Do it in-place.

## 题解

这道题要求的是in-place交换数据，那么一般需要两根指针，一根用来遍历原数组，另一根用来指向需要被交换元素的位置。

**其实这道题应该细想想，争取把思路方法熟记于心**

### python

```python
class Solution:
    """
    @param: nums: an array of integers
    @return: nothing
    """
    def partitionArray(self, nums):
        # 使用两根指针，一根遍历数组，另一根用来指定偶数数据的位置
        if len(nums) < 2:
            return
        m = 0
        for i in range(len(nums)):
            if nums[i] % 2 != 0:
                # 开始进行替换
                temp = nums[i]
                nums[i] = nums[m]
                nums[m] = temp
                
                m += 1
```

### 复杂度分析

> 时间上，遍历了一次原数组，因此时间复杂度为$O(n)$
>
> 空间上，原数组时间复杂度为$O(n)$，使用的额外空间复杂度为$O(1)$