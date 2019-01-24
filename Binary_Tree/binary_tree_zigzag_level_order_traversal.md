# Question

- leecode [二叉树的锯齿形层次遍历](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)

## 题目描述

给定一个二叉树，返回其节点值的锯齿形层次遍历。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

例如：
给定二叉树 `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7

```

返回锯齿形层次遍历如下：

```
[
  [3],
  [20,9],
  [15,7]
]
```

## 题解

与正常的层次遍历相比，无非就是奇数行结果不变，偶数行结果反转

### python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def zigzagLevelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        # 首先是层次遍历，层次遍历一般使用迭代的方式进行遍历
        if root is None:
            return []
        
        curr_node = [root]
        result = []
        # flag = False 代表奇数行
        flag = False
        while curr_node:
            next_node = []
            temp_val = []
            for node in curr_node:
                temp_val.append(node.val)
                if node.left: next_node.append(node.left)
                if node.right: next_node.append(node.right)
            if flag:
                temp_val = temp_val[::-1]
                
            result.append(temp_val)
            curr_node = next_node
            flag = ~flag
        
        return result
```

### 复杂度分析

> 时间上，遍历所有节点，复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(n)$

