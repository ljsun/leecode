# Question

- leecode [二叉搜索树的最小绝对差](https://leetcode-cn.com/problems/minimum-absolute-difference-in-bst/)

## 题目描述

给定一个所有节点为非负值的二叉搜索树，求树中任意两节点的差的绝对值的最小值。

**示例 :**

```
输入:

   1
    \
     3
    /
   2

输出:
1

解释:
最小绝对差为1，其中 2 和 1 的差的绝对值为 1（或者 2 和 3）。
```

## 题解

这道题要知道二叉搜索树的一个重要的性质，中序遍历的结果是一个有序数组

### python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def getMinimumDifference(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        # 二叉搜索树，左子树的值小于根节点，右子树的值大于根节点
        # 这题并没有做出来，因为自己并没有意识到一个性质，二叉搜索树的中序遍历是一个有序数组
        
        def inorder(root):
            if root:
                inorder(root.left)
                result.append(root.val)
                inorder(root.right)
        
        result = []
        inorder(root)
        
        # 取result中相邻元素的差的最小值
        diff = None
        for i in range(len(result)-1):
            curr_diff = abs(result[i]-result[i+1])
            if diff is None:
                diff = curr_diff
            else:
                if curr_diff < diff:
                    diff = curr_diff
        
        return diff
```

### 复杂度分析

> 时间上，遍历每个节点，复杂度为$O(n)$
>
> 空间上，递归使用隐式栈，使用空间与树深有关，大概为$O(logn)$。result使用的额外空间为$O(n)$

