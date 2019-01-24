# Question

- leecode [Validate Binary Search Tree](https://leetcode-cn.com/problems/validate-binary-search-tree/)

## 题目描述

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

- 节点的左子树只包含**小于**当前节点的数。
- 节点的右子树只包含**大于**当前节点的数。
- 所有左子树和右子树自身必须也是二叉搜索树。

**示例 1:**

```
输入:
    2
   / \
  1   3
输出: true
```

## 题解１

看代码注释，关于迭代中序遍历的，最好背下来

### python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        # 二叉搜索树等价于中序遍历为升序序列,
        # 故可以通过判断中序序列来判断二叉搜索树
        
        if root is None:
            return True
        
        stack = []
        pre = None
        while root or len(stack) != 0:
            if root:
                stack.append(root)
                root = root.left
            else:
                root = stack.pop()
                if pre is not None and pre >= root.val:
                    return False
                pre = root.val
                root = root.right
        return True
```

### 复杂度分析

> 时间上，迭代遍历所有节点，时间复杂度为$O(n)$
>
> 空间上，使用了额外辅助栈空间，空间大小与树深有关。最坏情况下栈保存所有节点，额外空间为$O(n)$

## 题解２

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
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        # 从上向下递归，及时的更新每一个节点的上限和下限
        return self.isBSTRec(root, -sys.maxsize-1, sys.maxsize)
    
    def isBSTRec(self, root, lower, upper):
        if root is None:
            return True
        
        if root.val <= lower or root.val >= upper:
            return False
    
        return self.isBSTRec(root.left, lower, root.val) and self.isBSTRec(root.right, root.val, upper)
```

### 复杂度分析

> 时间上，遍历所有所有节点，复杂度为$O(n)$
>
> 空间上，递归使用栈空间，空间大小与树深有关

