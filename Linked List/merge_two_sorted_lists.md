# Question

- leecode [合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

## 题目描述

将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

**示例：**

```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

## 题解

这道题应该并不难，使用dummy指针思路会比较清晰

### python

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        # 处理异常情况
        
        # 先尝试使用额外空间
        dummy = ListNode(0)
        node = dummy
        while l1 and l2:
            if l1.val < l2.val:
                node.next = l1
                l1 = l1.next
            else:
                node.next = l2
                l2 = l2.next
            node = node.next
        
        if l1:
            node.next = l1
        elif l2:
            node.next = l2
        
        return dummy.next
```

### 复杂度分析

> 时间上，相当于遍历了一次链表，时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$

