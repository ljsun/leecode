# Question

- leecode [将有序数组转化为二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)

## 题目描述

将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树*每个节点 *的左右两个子树的高度差的绝对值不超过 1。

**示例:**

```
给定有序数组: [-10,-3,0,5,9],

一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
```

## 题解

具体看代码注释，注意在下面代码中，如果只有两个节点，那么第一个节点为根节点，第二个为根节点的右子树

### python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        # 平衡二叉树是指：每一个节点的左右子树的高度差的绝对值不超过１
        # 所以尽可能使左右子树的节点个数相同
        
        if len(nums) == 0:
            return None
        
        low, up = 0, len(nums)-1
        
        return self.dfsrec(low, up, nums)
    
    def dfsrec(self, low, up, nums):
        # 寻找中间节点作为树的根节点
        if low > up:
            return None
        
        mid = (low + up) // 2
        root = TreeNode(nums[mid])
        
        root.left = self.dfsrec(low, mid-1, nums)
        root.right = self.dfsrec(mid+1, up, nums)
        
        return root
```

### 复杂度分析

> 时间上，遍历了所有节点，时间复杂度近似为$O(n)$
>
> 空间上，递归使用栈空间，使用栈空间大小大约为$O(logn)$