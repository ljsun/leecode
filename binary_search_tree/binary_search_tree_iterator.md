# Question

- leecode [二叉搜索树迭代器](https://leetcode-cn.com/problems/binary-search-tree-iterator/)

## 题目描述

实现一个二叉搜索树迭代器。你将使用二叉搜索树的根节点初始化迭代器。

调用 `next()` 将返回二叉搜索树中的下一个最小的数。

 

**示例：**

**![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/25/bst-tree.png)**

```
BSTIterator iterator = new BSTIterator(root);
iterator.next();    // 返回 3
iterator.next();    // 返回 7
iterator.hasNext(); // 返回 true
iterator.next();    // 返回 9
iterator.hasNext(); // 返回 true
iterator.next();    // 返回 15
iterator.hasNext(); // 返回 true
iterator.next();    // 返回 20
iterator.hasNext(); // 返回 false
```

## 题解

重点要理解二叉树的迭代中序遍历

### python

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class BSTIterator:
    
    # 调用next()将返回二叉搜索树中的下一个最小的数，
    # 相当于获得中序遍历的第一个数，第二个数，第三个数 ...
    # 迭代中序遍历
    # ********一定要重点理解这个迭代遍历　进栈出栈的本质【一种自底向上左根右的遍历】

    def __init__(self, root):
        """
        :type root: TreeNode
        """
        self.stack = []
        self.push_in_stack(root)
        
    
    def push_in_stack(self, root):
        while root:
            self.stack.append(root)
            root = root.left
        
    
    def next(self):
        """
        @return the next smallest number
        :rtype: int
        """
        curr = self.stack.pop()
        if curr.right:
            self.push_in_stack(curr.right)
        
        return curr.val

    def hasNext(self):
        """
        @return whether we have a next smallest number
        :rtype: bool
        """
        # 判断是否已经遍历完毕
        if len(self.stack) != 0:
            return True
        else:
            return False


# Your BSTIterator object will be instantiated and called as such:
# obj = BSTIterator(root)
# param_1 = obj.next()
# param_2 = obj.hasNext()
```

