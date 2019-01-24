# Question

- leecode [搜索二维矩阵2](https://leetcode-cn.com/problems/search-a-2d-matrix-ii/)

## 题目描述

编写一个高效的算法来搜索 *m* x *n* 矩阵 matrix 中的一个目标值 target。该矩阵具有以下特性：

- 每行的元素从左到右升序排列。
- 每列的元素从上到下升序排列。

**示例:**

现有矩阵 matrix 如下：

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]

```

给定 target = `5`，返回 `true`。

给定 target = `20`，返回 `false`。

## 题解

这道题其实感觉就是一个找规律的题，给定一个满足上述条件的矩阵，寻找矩阵中是否存在相应的target的值。

可以从右上角开始搜索，直到找到目标值或者找到左边或者下边边界为止

### python

```python
class Solution:
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        # 首先这道题只是每一行、每一列满足升序关系，
        # 行行之间、列列之间并不满足升序关系，
        # 所以就要找规律，看怎么才能找到我们想要的目标值
        
        # 处理异常情况
        m = len(matrix)
        if m == 0:
            return False
        n = len(matrix[0])
        if n == 0:
            return False
        
        # 从右上角开始搜索，直到找到目标值或者找到左下角为止
        row, col = 0, n-1
        while row < m and col >= 0:
            # 判断当前值和target之间的关系
            if matrix[row][col] < target:
                # 向下走
                row += 1
            elif matrix[row][col] == target:
                return True
            else:
                #　向左走
                col -= 1
            
        
        return False
```

### 复杂度分析

> 时间上，从右上角一直搜索到左边界或者下边界，因此时间复杂度为$O(m+n)$
>
> 空间上，申请的额外空间为$O(1)$

