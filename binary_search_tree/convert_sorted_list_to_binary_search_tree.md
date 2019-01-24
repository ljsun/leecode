# Question

- leecode [有序链表转换为二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree/)

## 题目描述

给定一个单链表，其中的元素按升序排序，将其转换为高度平衡的二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树*每个节点 *的左右两个子树的高度差的绝对值不超过 1。

**示例:**

```
给定的有序链表： [-10, -3, 0, 5, 9],

一个可能的答案是：[0, -3, 9, -10, null, 5], 它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
```

## 题解１

看代码注释

### python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sortedListToBST(self, head):
        """
        :type head: ListNode
        :rtype: TreeNode
        """
        # 平衡二叉树是指：每个节点的左右子树的高度差的绝对值不超过１
        
        # 两种思路：将链表转化为list,然后创建树。直接通过链表创建树
        
        # 那么对于这道题而言其实就是如何寻找单向链表的中间节点 [快慢指针] [遍历得到链表长度，然后利用一个计数器获得中间节点]
        
        if head is None:
            return None
        
        # 获取链表长度
        curr = head
        length = 0
        while curr:
            curr = curr.next
            length += 1
        
        return self.dfsrec(head, length)
    
    def dfsrec(self, head, length):
        # 注意这个head不一定是链表的头节点
        if length == 0:
            return None
        # 寻找中间节点
        mid = head
        count = 0
        while count < (length-1) // 2:
            mid = mid.next
            count += 1
        
        root = TreeNode(mid.val)
        root.left = self.dfsrec(head, count)
        root.right = self.dfsrec(mid.next, length-1-count)
        
        return root
```

### 复杂度分析

> 时间上，遍历链表长度时间为$O(n)$，递归的过程中也要遍历链表，时间复杂度为$O(nlogn)$
>
> 空间上，递归使用栈空间，空间大小为$O(logn)$

## 题解２

参考别人的，因为给定的这个链表值顺序就是二叉树的中序遍历，利用这个中序遍历自底向上的建树【每一个节点都看作是一个子树的根节点，然后自下向上按照左根右的顺序建树】

[参考链接](https://segmentfault.com/a/1190000003816154)

### python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sortedListToBST(self, head):
        """
        :type head: ListNode
        :rtype: TreeNode
        """
        # 平衡二叉树是指：每个节点的左右子树的高度差的绝对值不超过１
        
        # 下面这种自底向上建树的是参考大神的
        
        if head is None:
            return None
        
        # 计算链表长度
        length = 0
        curr = head
        while curr:
            curr = curr.next
            length += 1
        
        self.head = head
        return self.dfsrec(0, length-1)
        
    
    def dfsrec(self, low, up):
        if low > up:
            return None
        
        # 自底向上先计算左子树、根、右子树
        mid = low + (up - low) // 2
        
        left = self.dfsrec(low, mid-1)
        
        root = TreeNode(self.head.val)
        # 这句话一定要紧挨着上面创建节点这句话，因为如果不挨着的话，很可能到
        # 另一层递归中，这个节点值又被创建一遍
        self.head = self.head.next
        
        right = self.dfsrec(mid+1, up)
        
        root.left = left
        root.right = right
        
        return root
```

### 复杂度分析

> 时间上，遍历链表长度时间为$O(n)$，递归的过程中也要遍历链表，时间复杂度为$O(n)$
>
> 空间上，递归使用栈空间，空间大小为$O(logn)$