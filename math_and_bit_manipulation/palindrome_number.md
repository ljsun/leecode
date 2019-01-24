# Question

- leecode [回文数](https://leetcode-cn.com/problems/palindrome-number/)

## 题目描述

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

**示例 1:**

```
输入: 121
输出: true

```

**示例 2:**

```
输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。

```

**示例 3:**

```
输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
```

## 题解

**判断回文数，这道题应该算是比较经典的题了**

思路１：转化为字符串来做

思路２：直接得到原数字的反整数，然后比对

思路３：每次比对首尾数字

### python - 思路２

```python
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        # 判断回文数，这道题应该算是比较经典的题了
        # 思路１：转化为字符串来做
        # 思路２：直接得到原数字的反整数，然后比对
        # 思路３：每次比对首尾数字
        
        if x < 0:
            return False
        
        revert = 0
        y = x
        while y != 0:
            revert = revert * 10 + y % 10
            y //= 10
            
        if revert == x:
            return True
        else:
            return False
```

### 复杂度分析

> 时间上，循环次数大致为$O(log_{10}N)$，因此时间复杂度为$O(log_{10}N)$
>
> 空间上，额外空间为$O(1)$

### python - 思路３

```python
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        # 判断回文数，这道题应该算是比较经典的题了
        # 思路１：转化为字符串来做
        # 思路２：直接得到原数字的反整数，然后比对
        # 思路３：每次比对首尾数字
        
        if x < 0:
            return False
        
        def getDigit(x, i, length):
            temp = x
            temp //= 10 ** (length - i - 1)
            return temp % 10
        length = 0
        temp = x
        while temp != 0:
            temp //= 10
            length += 1
        
        left, right = 0, length-1
        
        while left < right:
            if getDigit(x, left, length) != getDigit(x, right, length):
                return False
            left += 1
            right -= 1
        
        return True
    
```

### 复杂度分析

> 时间上，两个while循环，时间复杂度为取大的while循环，为$O(log_{10}N)$
>
> 空间上，使用的额外空间为$O(1)$