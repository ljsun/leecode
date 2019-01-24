# Question

## 题目描述

- leetcode: [Reverse Words in a String](https://leetcode-cn.com/problems/reverse-words-in-a-string/)

给定一个字符串，逐个翻转字符串中的每个单词。

**示例:  **

```
输入: "the sky is blue",
输出: "blue is sky the".

```

**说明:**

- 无空格字符构成一个单词。
- 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
- 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。

## 题解

首先这个题使用python写的话就很简单了，因为python对list的切片操作十分方便。可以将原始的字符串先转化为list，然后进行翻转。

### python

```python
class Solution(object):
  def reverseWords(self, s):
      """
      :type s: str
      :rtype: str
      """
      # 首先去除字符串前面或后面的空格，并进行split
      s = s.strip().split()
      #此时的s是个list
      return ' '.join(s[::-1])
```
### 复杂度分析

> split()需要遍历因此split时间复杂度为$O(m)$,list进行翻转时间复杂度为$O(n)$，因此最终时间复杂度为$O(m+n)$
>
> 由于翻转list后又需要新的存储空间，因此一共的空间复杂度为$O(m+n+n)$

