# Question

- leecode [加一](https://leetcode-cn.com/problems/plus-one/)

## 题目描述

给定一个由**整数**组成的**非空**数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储一个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

**示例 1:**

```
输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。

```

**示例 2:**

```
输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。
```

## 题解

这道题也没啥说的，就是自己笨，没做出来

### python

```python
class Solution:
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        # 先自己想。。。用递归去做？
        
        lastIndex = len(digits) - 1
        while lastIndex >= 0:
            # 当不需要进位时
            if digits[lastIndex] != 9:
                digits[lastIndex] += 1
                return digits
            else:
                digits[lastIndex] = 0
                lastIndex -= 1
        digits.insert(0, 1)
        return digits
```

### 复杂度分析

> 时间上，复杂度为$O(n)$
>
> 空间上，额外的空间为$O(1)$

