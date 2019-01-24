# Question

- leecode [二叉搜索树中的插入操作](https://leetcode-cn.com/problems/insert-into-a-binary-search-tree/)

## 题目描述

给定二叉搜索树（BST）的根节点和要插入树中的值，将值插入二叉搜索树。 返回插入后二叉搜索树的根节点。 保证原始二叉搜索树中不存在新值。

注意，可能存在多种有效的插入方式，只要树在插入后仍保持为二叉搜索树即可。 你可以返回任意有效的结果。

例如, 

```
给定二叉搜索树:

        4
       / \
      2   7
     / \
    1   3

和 插入的值: 5

```

你可以返回这个二叉搜索树:

```
         4
       /   \
      2     7
     / \   /
    1   3 5

```

或者这个树也是有效的:

```
         5
       /   \
      2     7
     / \   
    1   3
         \
          4
```

## 题解１

使用递归的方法

### python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def insertIntoBST(self, root, val):
        """
        :type root: TreeNode
        :type val: int
        :rtype: TreeNode
        """
        # 二叉搜索树，左子树上的值均小于根节点的值，右子树上的值均大于根节点的值
        
        # 感觉最终插入的新值终究能成为叶节点
        
        # 递归插入
        if root is None:
            return None
        
        if root.left and root.val > val:
            self.insertIntoBST(root.left, val) 
        elif root.right and root.val < val:
            self.insertIntoBST(root.right, val)
        else:
            if root.val < val:
                root.right = TreeNode(val)
            else:
                root.left = TreeNode(val)
        
        return root
```

### 复杂度分析

> 时间上，使用递归，复杂度为$O(n)$
>
> 空间上，递归使用栈空间，空间大小与树的深度有关

## 题解２

使用迭代

### python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def insertIntoBST(self, root, val):
        """
        :type root: TreeNode
        :type val: int
        :rtype: TreeNode
        """
        # 二叉搜索树，左子树上的值均小于根节点的值，右子树上的值均大于根节点的值
        
        # 感觉最终插入的新值终究能成为叶节点
        # 迭代插入
        curr = root
        while curr:
            p_curr = curr
            if curr.val < val:
                # 走右子树
                curr = curr.right
            else:
                # 走左子树
                curr = curr.left
        
        if p_curr.val < val:
            p_curr.right = TreeNode(val)
        else:
            p_curr.left = TreeNode(val)
        
        return root
```

### 复杂度分析

> 时间上，循环迭代，复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$

