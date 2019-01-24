# Question

- leecode [二叉搜索树中的搜索](https://leetcode-cn.com/problems/search-in-a-binary-search-tree/)

## 题目描述

给定二叉搜索树（BST）的根节点和一个值。 你需要在BST中找到节点值等于给定值的节点。 返回以该节点为根的子树。 如果节点不存在，则返回 NULL。

例如，

```
给定二叉搜索树:

        4
       / \
      2   7
     / \
    1   3

和值: 2
```

你应该返回如下子树:

```
      2     
     / \   
    1   3
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
    def searchBST(self, root, val):
        """
        :type root: TreeNode
        :type val: int
        :rtype: TreeNode
        """
        # 因为二叉树搜索树的结构已经定义了，所以感觉只要找到对应值的根节点就行
        # 使用迭代中序遍历
        
        if root is None:
            return None
        
        stack = []
        while root or len(stack) != 0:
            if root:
                stack.append(root)
                root = root.left
            else:
                root = stack.pop()
                if root.val == val:
                    return root
                
                root = root.right
        return None
```

### 复杂度分析

> 时间上，迭代遍历所有节点，时间复杂度为$O(n)$
>
> 空间上，使用了额外的辅助栈空间，最坏时辅助栈保存所有的节点，复杂度为$O(n)$