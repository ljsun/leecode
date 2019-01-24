# Question

- leecode: [Merge Two Sorted Arrays](https://www.lintcode.com/problem/merge-two-sorted-arrays/description)

## 题目描述

Merge two given sorted integer array *A* and *B* into a new sorted integer array.

### Example

A=`[1,2,3,4]`

B=`[2,4,5,6]`

return `[1,2,2,3,4,4,5,6]`

### Challenge

How can you optimize your algorithm if one array is very large and the other is very small?

## 题解

这道题是要返回一个新的数组，因此从前向后遍历即可，也就是从前向后依次比较A与B各个位置的值。

### python

```python
class Solution:
    """
    @param A: sorted integer array A
    @param B: sorted integer array B
    @return: A new sorted integer array
    """
    def mergeSortedArray(self, A, B):
        # write your code here
        # 这道题和之前leecode的题很类似，
        # 只不过这道题不用in-place修改，返回一个新数组
        C = []
        m = len(A)
        n = len(B)
        i, j = 0, 0
        while i<m and j <n:
            if A[i] < B[j]:
                C.append(A[i])
                i += 1
            else:
                C.append(B[j])
                j += 1

        # 出while循环有两种情况
        while j < n:
            C.append(B[j])
            j += 1
        
        while i < m:
            C.append(A[i])
            i += 1
    
        return C
```

### 复杂度分析

> 时间上，遍历了一次数组，因此时间复杂度为$O(m+n)$
>
> 空间上，申请了额外的数组空间，因此总的空间复杂度为$O(m+n+m+n)$

