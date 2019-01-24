# Question

- lintcode [O(1) Check Power of 2](https://www.lintcode.com/problem/o1-check-power-of-2/description)

## 题目描述

Using O(*1*) time to check whether an integer *n* is a power of `2`.

**O(*1*) 时间复杂度

Problem Correction

### Example

For `n=4`, return `true`;

For `n=5`, return `false`;

### Challenge

O(1) time

## 题解

首先这道题是自己没想出来，然后看别人才知道的。这道题要使用O(1)的复杂度，则要考虑使用位运算的特性。

其中2的幂的特性是２进制位中只有一个１，且是最高位。那么如何利用这个特性呢？２的幂减１后与原数值进行“与”操作的话，结果为０

### python

```python
class Solution:
    """
    @param n: An integer
    @return: True or false
    """
    def checkPowerOf2(self, n):
        # write your code here
        
        # 若要使用O(1)的复杂度，则要考虑使用位运算的特性
        # 2的幂的特性是２进制位中只有一个１．且是最高位
        # 如何利用这个特性
        # 2的幂减１后与原数值进行与操作的话，结果绝对为０
        
        # 处理特殊情况
        if n<1:
            return False
        
        
        return True if (n & (n-1)) == 0 else False
```

### 复杂度分析

> 时间上，复杂度为$O(1)$
>
> 空间上，复杂度为$O(1)$

