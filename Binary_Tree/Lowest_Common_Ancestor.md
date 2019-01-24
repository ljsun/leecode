# Question

- leecode [二叉树的最近公共祖先]

## 题目描述

**示例 1:**

```
输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
输出: 3
解释: 节点 5 和节点 1 的最近公共祖先是节点 3。

```

**示例 2:**

```
输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
输出: 5
解释: 节点 5 和节点 4 的最近公共祖先是节点 5。因为根据定义最近公共祖先节点可以为节点本身。

```

 

**说明:**

- 所有节点的值都是唯一的。
- p、q 为不同节点且均存在于给定的二叉树中。

## 题解

题解在注释中，“记下来吧”

### python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        # 递归代码实现其实比较简单，感觉自己还并没有真正的会写一个递归的代码
        
        # 分析这道题
        # 首先注意前提条件：所有节点的值都是唯一的；p、q为不同节点且存在与给定的二叉树中
        # 首先从根节点递归向下遍历，若根节点root为null，则说明p q不在以root为根的树中，向上层返回吧
        # 如果根节点root就是p, q中的一个，则root就是结果，向上层返回吧
        # 如果根节点不为null，也不是p,q 则继续向下一层递归，看p或q是否在以root为根的树中
        
        
        if root is None or root is p or root is q:
            return root
        
        # 查看是否在以root.left和root.right为根的树中
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        
        if left is None and right is None:
            return None
    
        elif left and right:
            return root
        
        # 感觉在这个地方返回True或者False也行
        else:
            return left if left else right
```

### 复杂度分析

> 时间上，相当于从上到下遍历所有节点，复杂度为$O(n)$
>
> 空间上，递归使用栈空间，栈空间与递归的深度（树的深度）有关