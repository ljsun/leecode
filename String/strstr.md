# Question

- leecode: [Implement strStr()](https://leetcode-cn.com/problems/implement-strstr/)

## 问题描述

实现 [strStr()](https://baike.baidu.com/item/strstr/811469) 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  **-1**。

**示例 1:**

```
输入: haystack = "hello", needle = "ll"
输出: 2

```

**示例 2:**

```
输入: haystack = "aaaaa", needle = "bba"
输出: -1

```

**说明:**

当 `needle` 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

## 题解１－双重循环

对于这种字符串查找匹配的问题，最先能够想到的就是双重循环搜索的方式。但是由于只是返回第一个匹配的索引，因此对于这种双重循环也有它的优化之处，就是什么时候停止循环（找到截止索引）。首先对于目标字符串肯定是从头循环到尾逐个索引，但是对于源字符串，由于如果源字符串剩下的长度根本就不足以匹配目标字符串时，这时再去索引源字符串就没什么意义了，因此源字符串并不是从头索引到尾。

### Python

```python
class Solution:
  def strStr(self, haystack, needle):
      """
      :type haystack: str
      :type needle: str
      :rtype: int
      """
      if haystack is None or needle is None:
          return -1
      for i in range(len(haystack)-len(needle) + 1):
          for j in range(len(needle)):
              if haystack[i+j] != needle[j]:
                  break
          else:
              return i
      return -1
```
> 在第一位就逐位匹配成功，此时时间复杂度最低为$O(m)$。
>
> 最糟糕的情况则为源字符串一直匹配到$n-m$位，此时时间复杂度为$O((n-m)*m)$
>
> 空间复杂度则为$O(m+n)$

## 题解２－KMP算法

关于KMP算法的讲解详见[博客](https://blog.csdn.net/v_july_v/article/details/7041827)

### Python

```python
class Solution:
  def strStr(self, haystack, needle):
      """
      :type haystack: str
      :type needle: str
      :rtype: int
      """
      if haystack is None or needle is None:
          return -1
      if len(needle) == 0:
          return 0
      # 首先计算next数组
      def get_next():
          next = list(range(len(needle)))
          next[0] = -1
          k=-1
          j=0
          while j < len(needle) -1:
              if k==-1 or needle[j]==needle[k]:
                  k += 1
                  j += 1
                  next[j] = k
              else:
                  k = next[k]

          return next

      next = get_next()

      # 利用得到的next数组进行计算
      i = 0
      j = 0
      while i<len(haystack) and j<len(needle):
          if haystack[i] == needle[j] or j==-1:
              i += 1
              j += 1
          else:
              j = next[j]
      if j == len(needle):
          return i-j
      else:
          return -1
```
> 与双重循环题解一样，最好的情况就是在第一位就逐个匹配成功，时间复杂度为$O(m)$，最坏的情况就是一直匹配到$n-m$位才匹配成功（或者一直匹配到最后一位也不成功），时间复杂度为$O(n)$
>
> 再加上next数组的$O(m)$时间。因此最好情况时间复杂度为$O(m + m)$，最坏情况时间复杂度为$O(m + n)$。
>
> 空间复杂度为$O(m + n)$

