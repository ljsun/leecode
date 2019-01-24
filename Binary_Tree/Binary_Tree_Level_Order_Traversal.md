# Quesion

- leecode [二叉树的层次遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

## 题目描述

给定一个二叉树，返回其按层次遍历的节点值。 （即逐层地，从左到右访问所有节点）。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7

```

返回其层次遍历结果：

```
[
  [3],
  [9,20],
  [15,7]
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
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        
        # 处理异常情况
        if root is None:
            return []
        
        # 就是遍历完第一层，遍历第二层，逐层遍历
        result = []
        temp_q = [root]
        while temp_q:
            next_temp_q = []
            temp_r = []
            for node in temp_q:
                temp_r.append(node.val)
                if node.left:
                    next_temp_q.append(node.left)
                if node.right:
                    next_temp_q.append(node.right)
            result.append(temp_r)
            temp_q = next_temp_q
        return result
```

### 复杂度分析

> 时间上，一共遍历n个节点，因此时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(n)$