# Question

- lintcode [Fast Power](https://www.lintcode.com/problem/fast-power/description)

## 题目描述

Calculate the** an % b** where a, b and n are all 32bit positive integers.

Have you met this question in a real interview?  Yes

Problem Correction

### Example

For $2^{31}$ % 3 = 2

For $100^{1000}$ % 1000 = 0

### Challenge

O(logn)

## 题解

这道题没做出来，看别人才会的。。。

做这道题，首先要掌握一个关键的特性：(a * b) % p = ((a % p) * (b % p)) % p

根据这个求模公式，可以将$a^n$为：

$a^n = a^{n/2} * a^{n/2} = a^{n/4} * a^{n/4} * a^{n/4} * a^{n/4} = ...$

### python

```python
class Solution:
    """
    @param a: A 32bit integer
    @param b: A 32bit integer
    @param n: A 32bit integer
    @return: An integer
    """
    def fastPower(self, a, b, n):
        # 又是看别人的才知道大概怎么去做
        
        # 做这个题，首先要知道一个小的trick
        
        # 具体的分析见题解
        if n == 1:
            return a % b
        
        elif n == 0:
            return 1 % b
            
        elif n < 0:
            return -1
        
        # 在这里要处理好n是奇偶的问题
        product = self.fastPower(a, b, n//2)
        product = product * product
        if n % 2 == 1:
            product = product * (a % b)
            
        product = product % b
        
        return product

```

### 复杂度分析

> 时间上，大约递归$logn$次，因此时间复杂度为$logn$
>
> 空间上，使用的额外空间为$O(1)$

