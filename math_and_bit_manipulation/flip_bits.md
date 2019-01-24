# Question

- lintcode [Flip Bits](https://www.lintcode.com/problem/flip-bits/description)

## 题目描述

### Description

Determine the number of bits required to flip if you want to convert integer *n* to integer *m*.

**Both *n* and *m* are 32-bit integers.

Have you met this question in a real interview?  Yes

Problem Correction

### Example

Given *n* = `31` (11111), *m* = `14` (01110), return `2`

## 题解

关于题目的思路已经写在代码中，仍然不理解的点

- 原码、补码、反码、负数在计算机中是如何表示的
- 为什么在python中要进行 n& 0xffffffff

### python

```python
class Solution:
    """
    @param a: An integer
    @param b: An integer
    @return: An integer
    """
    def bitSwapRequired(self, a, b):
        # write your code here
        
        # step 1: 将a与b异或，异或的结果中１的个数就是要翻转的个数
        aorb = a ^ b
        
        # step 2: 如何计算异或结果中１的个数
        
        # method1: 使用bin包
        def NumberOf1_m1(n):
            count = 0
            
            # 为什么要和0xffffffff进行与操作，计算补码？
            
            return bin(n & 0xffffffff).count('1')
        
        # method2: 使用一个mask码，然后逐位与n进行“与”操作
        def NumberOf1_m2(n):
            count = 0
            mask = 1
            
            for i in range(32):
                if mask & n:
                    count += 1
                mask = mask << 1
            
            return count
        
        # method3: 让n和n-1不断的进行“与”操作，直至n为０
        def NumberOf1_m3(n):
            count = 0
            
            if n < 0:
                n = n & 0xffffffff
                
            while n != 0:
                count += 1
                n = n & (n-1)
            
            return count
            
        return NumberOf1_m3(aorb)
```

### 复杂度分析

> 时间上，复杂度都是常量级别，可认为就是$O(1)$
>
> 空间上，额外的时间复杂度为$O(1)$

