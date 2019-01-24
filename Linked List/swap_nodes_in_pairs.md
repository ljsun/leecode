# Question

- leecode [两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

## 题目描述

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

**示例:**

```
给定 1->2->3->4, 你应该返回 2->1->4->3.
```

## 题解１

迭代的方法，这也是自己想到并实现的少有的方法.

### python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        # 处理异常情况
        if head is None or head.next is None:
            return head
        
        dummy = ListNode(0)
        
        curr = head
        prev = dummy
        while curr:
            if curr.next:
                temp = None
                if curr.next.next:
                    temp = curr.next.next
                # 当前节点下一个节点
                curr_next = curr.next
                # 反指
                curr_next.next = curr
                # 让prev指向反指过来的节点
                prev.next = curr_next
                # 让链表不断掉
                curr.next = temp
                # 重置prev，为下一组交换做准备
                prev = curr
                # 指向下一组的开始节点
                curr = curr.next
            else:
                curr = curr.next
        return dummy.next
```

### 复杂度分析

> 时间上，遍历一次链表，时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$

## 题解２

参考[yuanbin大神](https://algorithm.yuanbin.me/zh-hans/linked_list/swap_nodes_in_pairs.html)的递归的方法