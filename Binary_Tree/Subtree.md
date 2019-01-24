# Question

- leecode [另一个树的子树](https://leetcode-cn.com/problems/subtree-of-another-tree/)

## 题目描述

给定两个非空二叉树 **s** 和 **t**，检验 **s** 中是否包含和 **t** 具有相同结构和节点值的子树。**s** 的一个子树包括 **s** 的一个节点和这个节点的所有子孙。**s** 也可以看做它自身的一棵子树。

**示例 1:**
给定的树 s:

```
     3
    / \
   4   5
  / \
 1   2

```

给定的树 t：

```
   4 
  / \
 1   2

```

返回 **true**，因为 t 与 s 的一个子树拥有相同的结构和节点值。

## 题解１

s从上到下依次判断是否是子树

### python

```python
class Solution:
    def isSubtree(self, s, t):
        """
        :type s: TreeNode
        :type t: TreeNode
        :rtype: bool
        """
        # s从上到下依次判断t是否是s的子树
        
        if s is None:
            return False
        
        if self.identical(s, t):
            return True
        
        
        return self.isSubtree(s.left, t) or self.isSubtree(s.right, t)
    
    def identical(self, t1, t2):
        if t1 is None and t2 is None:
            return True
        
        if t1 is None or t2 is None:
            return False
        
        if t1.val != t2.val:
            return False
        
        return self.identical(t1.left, t2.left) and self.identical(t1.right, t2.right)
    
```

### 复杂度分析

> 时间上，即判断相同又判断左右子树，复杂度为$O(m+n)$
>
> 空间上，使用额外的栈空间，空间大小与数深度有关

## 题解２

使用遍历后的字符串进行判断是否是子树

### python

```python
class Solution:
    def isSubtree(self, s, t):
        """
        :type s: TreeNode
        :type t: TreeNode
        :rtype: bool
        """
        # 另一种思路，分别将两棵树序列化
        # 然后根据序列化的结果判断是否存在子树
        s_serialize = self.serialize(s)
        t_serialize = self.serialize(t)
        
        if t_serialize in s_serialize:
            return True
        else:
            return False
    
    def serialize(self, root):
        if root is None:
            return []
        
        def pre_order(root):
            if root:
                result.append('^' + str(root.val))
                pre_order(root.left)
                pre_order(root.right)
            else:
                result.append('^#')
                
        result = []
        pre_order(root)
        
        return ','.join(result)
```

### 复杂度分析

> 时间上，两次序列化，时间复杂度为$O(m+n)$ + python内部判断子串的时间【KMP是$O(p+k)$】
>
> 空间上，使用额外的栈空间，空间大小与树深有关

