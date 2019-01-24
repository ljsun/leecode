# Question

- leecode [二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)

## 题目描述

给定一个二叉树，返回它的 *后序 *遍历。

**示例:**

```
输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [3,2,1]
```

## 题解

没啥说的，“记下来”

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
    
    def postorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        # 后序遍历的思路与前中序基本一致
        
        # 递归－分治
        # if root is None:
        #     return []
        # else:
        #     return self.postorderTraversal(root.left) + self.postorderTraversal(root.right) + [root.val]
        
        # 递归－遍历
        # if root:
        #     self.postorderTraversal(root.left)
        #     self.postorderTraversal(root.right)
        #     self.result.append(root.val)
        # return self.result
        
        # 迭代【还是“记下来吧“】,利用辅助栈
        # 处理异常情况
#         if root is None:
#             return []
#         result = []
#         stack = []
#         # prev代表添加进result的前一个节点
#         prev = None
#         stack.append(root)
#         while stack:
#             # 先看当前可能会添加进result的节点是否有孩子节点
#             # 【把每一个可能会加进result的节点curr看做是根节点】
#             curr = stack[-1]
#             noChild = curr.left is None and curr.right is None
#             # 再看上一个添加进result的节点是不是当前节点的左孩子或者右孩子
#             childVisited = prev is not None and (curr.left == prev or curr.right == prev)
            
#             if noChild or childVisited:
#                 root = stack.pop()
#                 result.append(root.val)
#                 prev = root
#             else:
#                 # 说明时机未到，继续向stack里面添加节点
#                 if curr.right:
#                     stack.append(curr.right)
#                 if curr.left:
#                     stack.append(curr.left)
            
        # return result
        
        # 反转先序遍历
        # 后序遍历的顺序为【左右根】，那么后续遍历结果就应该是【根右左】的转置，而【根右左】结果无非就是前序遍历【根左右】交换下左右访问顺序
        # 处理异常情况
        if root is None:
            return []
        result = []
        stack = []
        stack.append(root)
        while stack:
            # 把每一个stack中的节点都当做根节点，或者将从stack中pop的节点当做根节点
            curr = stack.pop()
            result.append(curr.val)
            if curr.left:
                stack.append(curr.left)
            if curr.right:
                stack.append(curr.right)
                
        return result[::-1]
```

### 复杂度分析

> 时间上，递归分治、递归遍历、反转先序遍历时间复杂度为$O(n)$. 迭代中，时间复杂度也为$O(n)$
>
> 空间上，递归分治、递归遍历使用空间复杂度为$O(n)$. 反转先序遍历时间复杂度近似为$O(n)$, 迭代空间复杂度近似为$O(n)$. 