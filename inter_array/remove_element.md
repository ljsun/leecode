# Question

- leecode [remove element](https://leetcode-cn.com/problems/remove-element/)

## 题目描述

给定一个数组 *nums **和一个值 **val*，你需要**原地**移除所有数值等于 *val *的元素，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在**原地修改输入数组**并在使用 O(1) 额外空间的条件下完成。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

**示例 1:**

给定 nums = [3,2,2,3], val = 3,

函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。

你不需要考虑数组中超出新长度后面的元素。

**示例 2:**

给定 nums = [0,1,2,2,3,0,4,2], val = 2,

函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。

注意这五个元素可为任意顺序。

你不需要考虑数组中超出新长度后面的元素。

## 题解１

首先感觉这道题的难度在于需要原地移除数值等于val的元素。原地移除最好的方式就是把想要移除的元素的值覆盖。我们希望用不移除的元素去覆盖要移除的元素，这就需要在遍历数组的同时也“记住”要移除的元素的位置。因此就需要额外的指针。

### python

```python
class Solution:
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        # 这道题稍微就难在需要原地移除数值等于val的元素
        # 原地移除最好的方式就是把想要移除的元素的值覆盖
        # 我们要把不移除的元素去覆盖要移除的元素，因此就需要
        # 两个指针，一个指向要移除的元素，一个来遍历当前元素
        i = 0
        for j in range(len(nums)):
            if nums[j]!=val:
                nums[i] = nums[j]
                i += 1
        
        return i
```

### 复杂度分析

> 从时间上看需要遍历一次数组，因此时间复杂度为$O(n)$
>
> 空间复杂度为$O(1)$

## 题解２

上面的题解存在一个问题，当需要移除的元素很少时，就需要赋值运算进行很多次。而且这样得到的结果元素顺序和原数组的顺序相同，这就相当于无形中给自己添加了额外的限制。因此赋值的判断条件改为num[j] == val

### python

```python
class Solution:
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        # 这道题稍微就难在需要原地移除数值等于val的元素
        # 原地移除最好的方式就是把想要移除的元素的值覆盖
        # 我们要把不移除的元素去覆盖要移除的元素，因此就需要
        # 两个指针，一个指向要移除的元素，一个来遍历当前元素
        left, right = 0, len(nums)
        while left < right:
            if nums[left] == val:
                nums[left] = nums[right-1]
                right -= 1
            else:
                left += 1
        return right
```

### 复杂度分析

> 只遍历了一次数组，因此时间复杂度为$O(n)$
>
> 空间复杂度为$O(1)$