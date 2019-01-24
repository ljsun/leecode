# Question

- leecode [删除排序链表中的重复元素２](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/)

## 题目描述

给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 **没有重复出现 **的数字。

**示例 1:**

```
输入: 1->2->3->3->4->4->5
输出: 1->2->5

```

**示例 2:**

```
输入: 1->1->1->2->3
输出: 2->3
```

## 题解

这道题自己没写出来，是看别人才会的。这道题有一个重点是使用**dummy**指针，但是个人感觉更重要的是有一个清晰的**思路**

### python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        # 由于head指向节点也有可能被删除，而且是单向链表，因此需要一个指向head节点的指针
        
        # 处理异常情况
        if head is None:
            return None
        dummy = ListNode(0)
        dummy.next = head
        
        node = dummy
        
        # 开始想着怎么判断重复并删除
        while node.next and node.next.next:
            if node.next.val == node.next.next.val:
                cur_val = node.next.val
                while node.next and node.next.val == cur_val:
                    node.next = node.next.next
            else:
                node = node.next
        return dummy.next
```

### 复杂度分析

> 时间上，遍历一次链表，时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$

