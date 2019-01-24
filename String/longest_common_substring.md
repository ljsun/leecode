# Question

## 题目描述

- lintcode: [Longest Common Substring](https://www.lintcode.com/problem/longest-common-substring/description)

### Description

Given two strings, find the longest common substring.

Return the length of it.

### Example

Given A = `"ABCD"`, B = `"CBCE"`, return `2`.

### Challenge

O(n x m) time and memory.

## 题解１－暴力逐位匹配

对于这种字符串匹配问题，对于我这种笨人来说，首先最能够想到的也只能够想到的就是逐位字符匹配，当前位如果匹配成功了，源字符串索引与目标字符串索引都向后移动一位。要是匹配不成功的话，索引指针就回朔，重新从第一位开始匹配。然后将最长的匹配长度记录在案。

### python

```python
class Solution:
    """
    @param A: A string
    @param B: A string
    @return: the length of the longest common substring.
    """
    def longestCommonSubstring(self, A, B):
        max_length = 0
        for i in range(len(A)):
            for j in range(len(B)):
                temp_length = 0
                while ((i+temp_length)<len(A) and (j+temp_length)<len(B) and A[i+temp_length] == B[j+temp_length]):
                    temp_length += 1
                if max_length < temp_length:
                    max_length = temp_length
        
        return max_length
```

### 复杂度分析

> 双重for循环，最坏的时间复杂度为$O(m*n*lcs)$，其中lcs = min{m, n}。其中最好的时间复杂度为$O(m*n)$
>
> 空间复杂度为$O(m+n)$

## 题解２－动态规划　

由于在上一个方法中存在着许多重复的计算匹配，我们完全可以将这些匹配结果保存下来，不用重复计算匹配，这正好符动态规划的思想

其实还没有理解关于动态规划的真正思想。。。

### python

```python
class Solution:
    """
    @param A: A string
    @param B: A string
    @return: the length of the longest common substring.
    """
    def longestCommonSubstring(self, A, B):
        # write your code here
        m, n = len(A), len(B)
       
        f = [[0 for i in range(n+1)] for _ in range(m+1)]
        
        for i in range(m):
            for j in range(n):
                if A[i] == B[j]:
                    f[i+1][j+1] = 1 + f[i][j]
       
        return max(map(max, f))
```

### 复杂度分析

> 改良过后仍然是双重for循环，因此时间复杂度为$O(m*n)$。
>
> 由于使用的额外的存储空间，因此空间复杂度$O(m+n+[(m+1)*(n+1)])$