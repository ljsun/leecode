# Question

- leecode [回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)

## 题目描述

请判断一个链表是否为回文链表。

**示例 1:**

```
输入: 1->2
输出: false
```

**示例 2:**

```
输入: 1->2->2->1
输出: true
```

## 题解

这种判断回文串的最简单的思路就是反转，判断反转前与反转后是否有区别

### python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        # 不要怕代码难写就一下放弃了某些思路
        
        # 将链表的后半部分逆序，然后与前半部分比较
        
        # 处理异常情况
        
        # 先找链表的中间节点
        dummy = ListNode(0)
        dummy.next = head
        slow, fast = dummy, head
        while fast:
            fast = fast.next
            slow = slow.next
            if fast:
                fast = fast.next
        
        rhead = slow.next
        slow.next = None
        
        # 将后半部分链表逆序
        prev = None
        while rhead:
            temp = rhead.next
            rhead.next = prev
            prev = rhead
            rhead = temp
        rhead = prev 
        # 判断前半部分与逆序的后半部分
        while head and rhead:
            if head.val != rhead.val:
                return False
            else:
                head = head.next
                rhead = rhead.next
        return True
```

### 复杂度分析

> 时间上，虽然三个循环，但是并不嵌套，时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$

