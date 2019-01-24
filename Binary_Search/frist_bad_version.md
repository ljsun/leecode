# Question

- lintcode [First Bad Version](https://www.lintcode.com/problem/first-bad-version/description)

## 题目描述

### Description

The code base version is an integer start from 1 to n. One day, someone committed a bad version in the code case, so it caused this version and the following versions are all failed in the unit tests. Find the first bad version.

You can call `isBadVersion` to help you determine which version is the first bad one. The details interface can be found in the code's annotation part.

**Please read the annotation in code area to get the correct way to call isBadVersion in different language. For example, Java is `SVNRepo.isBadVersion(v)`

### Example

Given n = `5`:

```
isBadVersion(3) -> false
isBadVersion(5) -> true
isBadVersion(4) -> true

```

Here we are 100% sure that the 4th version is the first bad version.

## 题解

其实仔细一想，这道题就是个搜索目标值的问题，这里先采用二分搜索。

### python

```python
class Solution:
    """
    @param n: An integer
    @return: An integer which is the first bad version.
    """
    def findFirstBadVersion(self, n):
        # write your code here
        # 感觉这本质上就是个二分搜索
        
        # 先处理一下异常情况
        if n == 1:
            return 1
        
        lb, ub = 0, n+1
        while lb+1 < ub:
            mid = lb + (ub-lb) // 2
            if not SVNRepo.isBadVersion(mid):
                lb = mid
            else:
                ub = mid
        
        return lb+1
                
```

### 复杂度分析

> 时间上，采用二分查找，时间复杂度为$O(logn)$
>
> 空间上，使用的额外的空间为$O(1)$

