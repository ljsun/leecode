# Question

- leecode [二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)

## 题目描述

给定一个二叉树，返回它的 *前序 *遍历。

 **示例:**

```
输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [1,2,3]
```

## 题解

递归－分治、递归－遍历、迭代【还是“记下来吧”】

### python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def __init__(self):
        self.result = []
        
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        
        # 关于树的前序遍历方法有递归和迭代两种，
        # 然后在递归方法中，根据对返回值处理方式的不同，又分为分治和遍历两种
        
        
        # 递归－分治
        if root is None:
            return []
        else:
            return [root.val] + self.preorderTraversal(root.left) + self.preorderTraversal(root.right)
        
        # 递归－遍历
#         if root:
#             self.result.append(root.val)
#             self.preorderTraversal(root.left)
#             self.preorderTraversal(root.right)
        
#         return self.result
    
        # 迭代的方式
        # 【“记下来“】将遍历到的节点入栈，然后出栈时保存相应的结果值，为了保证出栈时的顺序就是
        # 入栈顺序，入栈时要先根再右后左【画下图看看】
#         if root is None:
#             return []
#         result = []
#         stack = []
#         stack.append(root)
#         while stack:
#		      把每一个stack中的节点都当做根节点，或者将从stack中pop的节点当做根节点
#             node = stack.pop()
#             result.append(node.val)
#             if node.right:
#                 stack.append(node.right)
#             if node.left:
#                 stack.append(node.left)
        
#         return result
```

### 复杂度分析

> 时间上，递归－分治、递归－遍历时间复杂度都为$O(n)$，迭代时间复杂度也为$O(n)$
>
> 空间上，递归－遍历使用额外空间为$O(n)$、递归－分治使用额外临时空间为$O(n)$
>
> 迭代使用额外空间为$O(n)$

