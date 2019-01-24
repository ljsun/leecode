# Question

- lintcode [Fibonacci](https://www.lintcode.com/problem/fibonacci/description)

## 题目描述

Find the *N*th number in Fibonacci sequence.

A Fibonacci sequence is defined as follow:

- The first two numbers are 0 and 1.
- The *i* th number is the sum of *i*-1 th number and *i*-2 th number.

The first ten numbers in Fibonacci sequence is:

`0, 1, 1, 2, 3, 5, 8, 13, 21, 34 ...`

## 题解

### python

```python
class Solution:
    """
    @param n: an integer
    @return: an ineger f(n)
    """
    def fibonacci(self, n):
        # 处理异常情况
        
        if n < 1:
            return -1
            
        if n == 1:
            return 0
        if n == 2:
            return 1
        
        f_n1 = 0
        f_n2 = 1
        i = 2        
        while i < n:
            f_c = f_n1 + f_n2
            
            f_n1 = f_n2
            
            f_n2 = f_c

            i += 1
        
        return f_c
```

### 复杂度分析

> 时间上，复杂度为$O(n)$
>
> 空间上，额外空间为$O(1)$

