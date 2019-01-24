# Question

- leecode [二叉树中的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

## 题目描述

给定一个二叉树，返回它的*中序 *遍历。

**示例:**

```
输入: [1,null,2,3]
   1
    \
     2
    /
   3

输出: [1,3,2]
```

## 题解

没啥说的，“记下来”

如何去理解中序遍历的迭代版.  个人理解就是自底向上的左根右。首先如果root.left不为空，说明当前树还没到底，继续向下走【进栈】，直到root.left为空，说明当前节点是个叶节点了【说明到底了，而且重点**这个时候你要把这个叶节点看做是一个子树的根节点**】，到底了那就开始左根右吧，由于左为空，那就直接根，咋得到根呢？**stack.pop()出来的第一个不就是那个根嘛**，然后就开始右，右边呢是一个套路，又开始一直向左走直到底。

这就是个人理解的迭代版本中，进栈出栈的过程.

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
    
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        # 与前序遍历的思路基本相同，也分为递归和迭代两种
        
        # 递归－分治
        if root is None:
            return []
        else:
            return self.inorderTraversal(root.left) + [root.val] + self.inorderTraversal(root.right)
        
        # 递归－遍历
#         if root:
#             self.inorderTraversal(root.left)
#             self.result.append(root.val)
#             self.inorderTraversal(root.right)
        
#         return self.result

        # 迭代：还是利用辅助栈，只能说“记下来吧”
        # result = []
        # stack = []
        # while root or stack:
        #     if root:
        #         stack.append(root)
        #         root = root.left
        #     else:
        #         把每一个stack中的节点都当做根节点，或者将从stack中pop的节点当做根节点
        #         root = stack.pop()
        #         result.append(root.val)
        #         root = root.right
        # return result
```

### 复杂度分析

> 时间上，递归分治、递归遍历、迭代时间复杂度都为$O(n)$
>
> 空间上，这三种方法的空间复杂度都与树深有关。最坏时，递归分治、递归遍历使用额外空间为$O(n)$. 迭代使用额外空间为$O(n)$。
>