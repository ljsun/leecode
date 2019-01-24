# Question

- leecode [移除链表元素](https://leetcode-cn.com/problems/remove-linked-list-elements/)

## 题目描述

删除链表中等于给定值 **val **的所有节点。

**示例:**

```
输入: 1->2->6->3->4->5->6, val = 6
输出: 1->2->3->4->5
```

## 题解

注意要思路清晰

### python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeElements(self, head, val):
        """
        :type head: ListNode
        :type val: int
        :rtype: ListNode
        """
        
        # 这个感觉就是简单的移除链表元素的题目
        
        # 处理异常情况
        
        dummy = ListNode(0)
        dummy.next = head
        prev = dummy
        curr = head
        while curr:
            if curr.val == val:
                prev.next = curr.next
            else:
                prev = curr
            curr = curr.next
        
        return dummy.next
```

### 复杂度分析

> 时间上，遍历一次链表，时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$