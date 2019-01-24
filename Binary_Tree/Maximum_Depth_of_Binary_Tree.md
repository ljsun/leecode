# Question

- leecode [二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)

## 题目描述

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

**说明:** 叶子节点是指没有子节点的节点。

**示例：**
给定二叉树 `[3,9,20,null,null,15,7]`，

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度 3 。

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
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """

        if root is None:
            return 0
        
        # 自己的思路
#         depth = 0
#         temp_q = [root]
#         while temp_q:
#             depth += 1
#             next_temp_q = []
#             for node in temp_q:
#                 if node.left:
#                     next_temp_q.append(node.left)
#                 if node.right:
#                     next_temp_q.append(node.right)
#             temp_q = next_temp_q
        
#         return depth
    
        # 递归的思路
#         max_left_depth = self.maxDepth(root.left)
#         max_right_depth = self.maxDepth(root.right)
        
#         return 1 + max(max_left_depth, max_right_depth)

        # 利用迭代后序遍历的模版？
        # 由于迭代后序遍历是从stack中一个个pop出节点，而后序是【左右根】，那么pop左右节点时，根节点一定在stack中，
```

### 复杂度分析

> 时间上，迭代、递归时间复杂度为$O(n)$
>
> 空间上，迭代空间复杂度为$O(n)$，递归使用的栈空间也为$O(n)$

