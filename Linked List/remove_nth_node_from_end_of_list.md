# Question

- leecode [删除链表的倒数第N个节点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)

## 题目描述

给定一个链表，删除链表的倒数第 *n *个节点，并且返回链表的头结点。

**示例：**

```
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.

```

**说明：**

给定的 *n* 保证是有效的。

## 题解

这题自己本应该能够想到的，画画图应该能够想到的。。。

### python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        # 首先并不知道总长度，而且只能正向遍历，所以如何得知哪个是倒数第n个节点？
        # 傻了，这道题利用快慢指针应该自己能够想到的
        
        # 处理异常情况
        if head is None:
            return None
        
        dummy = ListNode(0)
        fast = head
        slow = dummy
        dummy.next = head
        
        # 让fast指针先走(n+1)步
        i = 0
        while i < n:
            fast = fast.next
            i += 1
        
        # fast指针与slow指针一起向前走
        while fast and slow:
            fast = fast.next
            slow = slow.next
        
        # 此时slow指向倒数第(n+1)个节点
        slow.next = slow.next.next
        
        return dummy.next
```

### 复杂度分析

> 时间上，虽然两个循环，但是本质上还是只遍历一次链表，时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$

