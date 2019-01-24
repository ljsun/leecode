# Question

##　题目描述

比较两个字符串A和B，判断A是否包含B中的所有字符。其中A和B中所有字符均为大写

**注意**

B在A中的字符不需要是连续的或者是排序的

**例子**

For `A = "ABCD"`, `B = "ACD"`, return `true`.

For `A = "ABCD"`, `B = "AABC"`, return `false`.

## 题解 hashmap统计词频

很显然，最先能想到的解法就是分别统计A和B的词频，然后比较词频。然而这种方法其实是比较蠢的。稍微好点的做法如下所示:

### python

```python
class Solution:
    """
    @param A : A string includes Upper Case letters
    @param B : A string includes Upper Case letters
    @return :  if string A contains all of the characters in B return True else return False
    """
    def compareStrings(self, A, B):
        letters = collections.defaultdict(int)
        for a in A:
            letters[a] += 1

        for b in B:
            letters[b] -= 1
            if letters[b] < 0:
                return False

        return True
```

### 复杂度分析

> 假设A与B的长度分别为m和n，很明显，最坏情况时间复杂度为$O(m+n)$，最好为$O(m)$
>
> 空间复杂度则为$O(m)$