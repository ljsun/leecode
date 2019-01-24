# Question

## 题目描述

- lintcode: [Rotate String]()

### Description

Given a string and an offset, rotate string by offset. (rotate from left to right)

### Example

Given `"abcdefg"`.

```
offset=0 => "abcdefg"
offset=1 => "gabcdef"
offset=2 => "fgabcde"
offset=3 => "efgabcd"
```

### Challenge

Rotate in-place with O(1) extra memory.

## 题解

首先这种翻转字符串的问题，最重要的就是首先要找规律，怎么找呢？可以这样想，无论这个字符串再怎么偏移，每一个字符串只是位置变了，它们两边的邻居字符串并没有发生变化。因此可以想到最终的字符串就是由原始字符串的两段组成的。最重要的就是怎么将原始字符串分成正确的两段，然后这两段组合能够得到最终正确的结果。

经过自己试验几组可以发现，正确的分裂点就是在len(str) - offset%len(str)处。

### python 

```python
class Solution:

    """

    @param str: An array of char

    @param offset: An integer

    @return: nothing

    """
    
    def rotateString(self, str, offset):

        if len(str) >= 1:

            offset %= len(str)

            str[:] = str[-offset:] + str[:-offset]

```

### 复杂度分析

> 由于没有遍历的过程，因此时间复杂度为$O(1)$。
>
> 由于也没有申请额外的空间，因此空间复杂度为$O(1)$

