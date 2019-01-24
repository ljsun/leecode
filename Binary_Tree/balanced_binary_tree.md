# Question

- leecode [平衡二叉树](https://leetcode-cn.com/problems/balanced-binary-tree/)

## 题目描述

给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

> 一个二叉树*每个节点 *的左右两个子树的高度差的绝对值不超过1。

**示例 1:**

给定二叉树 `[3,9,20,null,null,15,7]`

```
    3
   / \
  9  20
    /  \
   15   7
```

返回 `true` 。
**示例 2:**

给定二叉树 `[1,2,2,3,3,null,null,4,4]`

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4

```

返回 `false` 。

## 题解

在代码注释中

### python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
#     def isBalanced(self, root):
#         """
#         :type root: TreeNode
#         :rtype: bool
#         """
#         # 平衡二叉树的定义：或者是空树，或者左右子树高度差不大于１且左右子树全是平衡二叉树
#         # 就按照自己想的思路写，不要怕写不出来，也不要管什么时间问题，能写的出来再说
        
#         # 处理异常情况
#         if root is None:
#             return True
        
#         if abs(self.max_depth(root.left) - self.max_depth(root.right)) > 1:
#             return False
#         else:
#             if self.isBalanced(root.left) and self.isBalanced(root.right):
#                 return True
#             else:
#                 return False
        
#     def max_depth(self, root):
#         if root is None:
#             return 0
        
#         return max(self.max_depth(root.left), self.max_depth(root.right)) + 1
    
    
    # 感觉自己的思路方法有点蠢，也有点慢呀，因为每一次算depth时，都是从根到叶递归了一次，
    # 能不能从根到叶只递归一次
    # 再看别人的优化思路
        def isBalanced(self, root):
            """
            :type root: TreeNode
            :rtype: bool
            """
            return self.max_depth(root) != -1
        
        def max_depth(self, root):
            if root is None:
                return 0
            
            leftdepth = self.max_depth(root.left)
            rightdepth = self.max_depth(root.right)
            if leftdepth == -1 or rightdepth == -1 or abs(leftdepth-rightdepth) > 1:
                return -1
            
            return 1 + max(leftdepth, rightdepth)
```

### 复杂度分析

> 时间上，自己的思路是针对每一个节点，都递归一轮（以该节点为根，递归到叶节点），这样的时间复杂度应该是平方级别的$O(n^2)$. 而别人的优化思路只是从根节点递归到叶节点递归一轮，复杂度应该是线性级别的$O(n)$
>
> 空间上，递归都使用了栈空间，栈空间应该对应着树的深度.