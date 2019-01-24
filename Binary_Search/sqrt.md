# Question

- leecode [x的平方根](https://leetcode-cn.com/problems/sqrtx/)

## 问题描述

实现 `int sqrt(int x)` 函数。

计算并返回 *x* 的平方根，其中 *x *是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

**示例 1:**

```
输入: 4
输出: 2

```

**示例 2:**

```
输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。
```

## 题解

这道题最简单的思路就是使用二分查找的思路去做

### python 

```python
class Solution:
    def mySqrt(self, x):
        """
        :type x: int
        :rtype: int
        """
        # 首先处理异常情况
        if x is None:
            return None
        
        if x == 1 or x == 0:
            return x

        lb, ub = 0, x
        while lb + 1 < ub:
            mid = lb + (ub-lb) // 2
            if mid*mid > x:
                ub = mid
            else:
                lb = mid
        
        return ub-1
```

### 复杂度分析

> 从时间上看，使用了二分搜索，时间复杂度为$O(logn)$
>
> 空间上，使用的额外数组空间为$O(1)$

