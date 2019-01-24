# Question

- leecode [二叉树中的最大路径和](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)

## 题目描述

给定一个**非空**二叉树，返回其最大路径和。

本题中，路径被定义为一条从树中任意节点出发，达到任意节点的序列。该路径**至少包含一个**节点，且不一定经过根节点。

**示例 1:**

```
输入: [1,2,3]

       1
      / \
     2   3

输出: 6

```

**示例 2:**

```
输入: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

输出: 42
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
    def maxPathSum(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        
        # 路径和为路径上节点的权值之和
        
        # 如果把路径看做一条折线吧，那么这条折线一定有一个”最高点“，设这个节点为A，如何计算以A为最高节点的最大路径长度
        # 假设A有左右两个孩子（当然也可能为空），分别以左右孩子为起点向延伸，会有很多条路径，记以左孩子为起点的向下延伸的最大
        # 长度为max_left，同理也可以得到max_right. 那么以A为最高点的最大路径长度显然有四种情况
        # 1. max_left <= 0 && max_right <= 0, maxPathSum = A.val
        # 2. max_left <= 0 && max_right > 0, maxPathSum = A.val + max_right
        # 3. max_left > 0 && max_right <= 0, maxPathSum = A.val + max_left
        # 4. max_left > 0 && max_right > 0, maxPathSum = A.val + max_left + max_right
        
        # 按照这种方式，所有的节点都能够当做”最高点“，都能够算出个最大路径长度。
        # 但是路径不一定经过根节点，要么循环每一个节点当”最高点“，这样很蠢，因为节点很多，而且计算以根节点为”最高点“时是递归计算，
        # 计算过程中就能计算以其他节点为”最高点“的最长路径值，，，那肯定要以根节点为“最高点”递归计算时把每一个节点为“最高点”的最长路径值算了呀
        if root is None:
            return 0
        self.maxPathSum = root.val
        self.helper(root)
        return self.maxPathSum
    
    # 返回以root为根节点的单向路径最大长度
    # 由于路径不一定经过根节点，因此用result随时记录以root（代表每一个节点）为”最高点“的最大路径长度
    def helper(self, root):
        if root is None:
            return 0
        
        left_val = self.helper(root.left)
        right_val = self.helper(root.right)
        
        self.maxPathSum = max(self.maxPathSum, max(left_val, 0) + max(right_val, 0) + root.val)
        
        # 计算以root为根的单向最大路径长度
        return max(root.val, left_val + root.val, right_val + root.val)
```

### 复杂度分析

> 时间上相当于从上到下遍历了所有节点，复杂度为$O(n)$
>
> 空间上，递归使用的栈空间，栈空间应该和树的深度有关.