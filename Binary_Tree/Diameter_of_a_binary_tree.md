# Question

- leecode [二叉树的直径](https://leetcode-cn.com/problems/diameter-of-binary-tree/)

## 题目描述

给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过根结点。

**示例 :**
给定二叉树

```
          1
         / \
        2   3
       / \     
      4   5 
```

返回 **3**, 它的长度是路径 [4,2,1,3] 或者 [5,2,1,3]。

**注意：**两结点之间的路径长度是以它们之间边的数目表示

## 题解１

结题思路在代码注释中

### python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def diameterOfBinaryTree(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        
        # 这种题的解法一般就是从根节点开始递归
        # 你要分析呀，根节点为root的树的直径可能是什么？无非就是两种情况
        # 直径经过根节点，那么直径就是左子树深度＋右子树深度，不经过根节点，那么直径就是左子树直径或者右子树直径
        # 最终结果就是这三者的最大值
        
        if root is None:
            return 0
        
        res = self.depth(root.left) + self.depth(root.right)
        return max(res, self.diameterOfBinaryTree(root.left), self.diameterOfBinaryTree(root.right))
        
    def depth(self, root):
        if root is None:
            return 0
        
        left_dep = self.depth(root.left)
        right_dep = self.depth(root.right)
        
        return max(left_dep, right_dep) + 1
```

### 复杂度分析

> 时间上，使用了两次递归，复杂度基本上是$O(n^2)$级别的
>
> 空间上，递归使用栈空间，空间大小与数的深度有关

## 题解２

思路在代码注释中

### python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def diameterOfBinaryTree(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        
        # 这种题的解法一般就是从根节点开始递归
        # 你要分析呀，根节点为root的树的直径可能是什么？无非就是两种情况
        # 直径经过根节点，那么直径就是左子树深度＋右子树深度，不经过根节点，那么直径就是左子树直径或者右子树直径
        # 最终结果就是这三者的最大值
        
        # 有没有感觉上面的写法虽然虽然思路简单，但是有点繁琐呀
        # 其实完全可以一个递归就完成的。因为其实细分析下来就是以每一个节点为根的左右子树深度之和的最大值
    
        self.result = 0
        self.depth(root)
        return self.result
        
    def depth(self, root):
        if root is None:
            return 0
        
        left_dep = self.depth(root.left)
        right_dep = self.depth(root.right)
        
        self.result = max(self.result, left_dep + right_dep)
        
        return max(left_dep, right_dep) + 1
```

### 复杂度分析

> 时间上，一次递归，复杂度为$O(n)$级别
>
> 空间上，递归使用栈空间，空间大小与树的深度有关