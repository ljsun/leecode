# Question

- leecode [二叉树的层次遍历 II](https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii/)

## 题目描述

给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

例如：
给定二叉树 `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7

```

返回其自底向上的层次遍历为：

```
[
  [15,7],
  [9,20],
  [3]
]
```

## 题解

看代码注释

### python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrderBottom(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        
        # 处理异常情况
        if root is None:
            return []
        
        # 逆序输出：要么得到正序后再逆序，要么利用辅助栈？
        # 先尝试得到正序，再逆序
#         result = []
#         temp_q = [root]
#         while temp_q:
#             next_temp_q = []
#             temp_r = []
#             for node in temp_q:
#                 temp_r.append(node.val)
#                 if node.left:
#                     next_temp_q.append(node.left)
#                 if node.right:
#                     next_temp_q.append(node.right)
#             result.append(temp_r)
#             temp_q = next_temp_q
        
#         # 将result进行逆序
#         result = result[::-1]
    
        # return result
```

### 复杂度分析

> 时间上，时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(n)$