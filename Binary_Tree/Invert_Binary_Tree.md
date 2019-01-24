# Question

- leecode [翻转二叉树]

## 题目描述

翻转一棵二叉树。

**示例：**

输入：

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

输出：

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

## 题解

分为递归和迭代两种思路

### python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def invertTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        
        # 处理异常
#         if root is None:
#             return None
        
#         # 自己想到的思路就是先反转第１层，再第２层　... 这样的话就是迭代的思想去做
        
#         curr_layer = [root]
#         while curr_layer:
#             next_layer = []
#             for node in curr_layer:
#                 # 对node的左右子树进行反转
#                 if node.left or node.right:
#                     node.left, node.right = node.right, node.left
#                     if node.left:
#                         next_layer.append(node.left)
#                     if node.right:
#                         next_layer.append(node.right)
                    
#             curr_layer = next_layer
        
#         return root
        
        # 递归的思想去做
        if root is None:
            return None
        
        temp = root.left
        root.left = self.invertTree(root.right)
        root.right = self.invertTree(temp)
        
        return root
```

### 复杂度分析

> 时间上，迭代与递归相当于遍历所有节点，时间复杂度为$O(n)$
>
> 空间上，迭代与递归。迭代的话，额外的空间复杂度为相邻两层的最大节点数
>
> 递归的栈空间与树的深度有关，深度越大，使用的栈空间越大。