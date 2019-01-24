# Question

- leetcode [Search a 2D Matrix](https://leetcode-cn.com/problems/search-a-2d-matrix/)

## 题目描述

编写一个高效的算法来判断 *m* x *n* 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

- 每行中的整数从左到右按升序排列。
- 每行的第一个整数大于前一行的最后一个整数。

**示例 1:**

```
输入:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
输出: true

```

**示例 2:**

```
输入:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
输出: false
```

## 题解

这道实际上是个搜索目标值的问题，这里采用二分搜索。有两种思路：

- 先竖着搜索，判断target所在的行，然后再对所在的行进行搜索
- 直接把二维数组看做成一维数组，进行搜索

### python 

```python
class Solution:
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        
        # 搜索目标值，因此采用搜索算法
        
        # 先处理异常情况
        m = len(matrix)
        if m == 0:
            return False
        n = len(matrix[0])
        if n == 0:
            return False
        
        # 先判断target可能所在的行，竖着进行一次二分搜索
        lb, ub = -1, m
        while lb+1 < ub:
            mid = lb + (ub-lb) // 2
            if matrix[mid][0] < target:
                lb = mid
            elif matrix[mid][0] == target:
                return True
            else:
                ub = mid
        
        # 执行到这里，说明上面的return并没有成功.
        # 说明target可能在lb行
        if lb == -1:
            return False
        
        row_lb, row_ub = -1, n
        while row_lb+1 < row_ub:
            mid = row_lb + (row_ub-row_lb) // 2
            if matrix[lb][mid] < target:
                row_lb = mid
            elif matrix[lb][mid] == target:
                return True
            else:
                row_ub = mid
        return False
```

### 复杂度分析

> 时间上，利用了两次二分搜索，因此时间复杂度为$O(log(m)+log(n))$
>
> 空间上，使用的额外空间为$O(1)$

### python 

```python
class Solution:
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        
        # 搜索目标值，因此采用搜索算法
        
        # 先处理异常情况
        m = len(matrix)
        if m == 0:
            return False
        n = len(matrix[0])
        if n == 0:
            return False
        
        # 一次二分搜索, 把二维数组看做为一维数组
        lb, ub = -1, m*n
        while lb+1 < ub:
            mid = lb + (ub-lb) // 2
            mid_row = mid // n
            mid_column = mid % n
            if matrix[mid_row][mid_column] < target:
                lb = mid
            elif matrix[mid_row][mid_column] == target:
                return True
            else:
                ub = mid
        
        return False
        
```

### 复杂度分析

> 时间上，使用一次二分搜索，时间复杂度为$O(log(mn))$
>
> 空间上，使用的额外的空间为$O(1)$