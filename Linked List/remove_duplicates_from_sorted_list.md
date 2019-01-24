# Question

- leecode [删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

## 题目描述

给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

**示例 1:**

```
输入: 1->1->2
输出: 1->2

```

**示例 2:**

```
输入: 1->1->2->3->3
输出: 1->2->3
```

## 题解

这道题从本质上来讲应该是比较简单的，但是写的时候还是要注意下细节

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
        temp = head
        while temp and temp.next:
            if temp.val == temp.next.val:
                temp.next = temp.next.next
            else:
                temp = temp.next
        
        return head
```

### 复杂度分析

> 时间上，遍历了一次链表，时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$

