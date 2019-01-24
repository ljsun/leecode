# Question

- leecode [丑数](https://leetcode-cn.com/problems/ugly-number/)

## 题目描述

编写一个程序判断给定的数是否为丑数。

丑数就是只包含质因数 `2, 3, 5` 的**正整数**。

**示例 1:**

```
输入: 6
输出: true
解释: 6 = 2 × 3
```

**示例 2:**

```
输入: 8
输出: true
解释: 8 = 2 × 2 × 2

```

**示例 3:**

```
输入: 14
输出: false 
解释: 14 不是丑数，因为它包含了另外一个质因数 7。
```

## 题解

没啥可说的，就是自己笨没做出来

### python

```python
class Solution:
    def isUgly(self, num):
        """
        :type num: int
        :rtype: bool
        """
        # 这题感觉自己还是能做出来的，但是并没有。。。仔细思考思考。。。
        if num <= 0:
            return False
        
        while num % 2 == 0:
            num /= 2
        
        while num % 3 == 0:
            num /= 3
        
        while num % 5 == 0:
            num /= 5
        
        return num == 1
```

### 复杂度分析

> 时间上，这个没法准确判断
>
> 空间上，额外的空间为$O(1)$