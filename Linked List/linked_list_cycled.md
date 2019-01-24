# Question

- leecode [环形链表2](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

## 题目描述

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 `null`。

为了表示给定链表中的环，我们使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 `pos` 是 `-1`，则在该链表中没有环。

**说明：**不允许修改给定的链表。

## 题解

这个题还是需要点智商的，自己当然没想出来，画个图其实比较清晰。关键点在于快指针移动速度是慢指针的２倍，因此移动距离也是慢指针的２倍

### python

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def detectCycle(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        # 返回入环时的第一个节点？。。。
        # 看别人的思路，画了个图，才大致知道思路
        
        fast = head
        slow = head
        
        while fast:
            fast = fast.next
            slow = slow.next
            if fast:
                fast = fast.next
            if fast == slow:
                break
        if fast and fast == slow:
            p = head
            while p != slow:
                p = p.next
                slow = slow.next
            return p
        else:
            return None
```

### 复杂度分析

> 时间上，由于确定在第二次相遇(p与slow相遇）时确定入环点，因此时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$