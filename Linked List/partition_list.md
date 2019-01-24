# Question

- leecode [分割链表](https://leetcode-cn.com/problems/partition-list/)

## 题目描述

给定一个链表和一个特定值* x*，对链表进行分隔，使得所有小于 *x* 的节点都在大于或等于 *x* 的节点之前。

你应当保留两个分区中每个节点的初始相对位置。

**示例:**

```
输入: head = 1->4->3->2->5->2, x = 3
输出: 1->2->2->4->3->5
```

## 题解

解题思路在代码注释中，注意细看每一条

### python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def partition(self, head, x):
        """
        :type head: ListNode
        :type x: int
        :rtype: ListNode
        """
        # 目前能够想到的就是遍历链表
        # 找到小于x的局部链表
        # 找到大于等于x的局部链表，然后进行拼接
        
        # 遍历链表的个人感觉有两种基本的方式，
        # 一种仅仅就是遍历链表，遍历链表的值，这种就需要一个链表指针就行
        # 另一种是遍历链表、修改链表结构，这种就需要两个或多个链表指针，一个用于永远
        # 指向链表的头节点，剩下的遍历链表修改链表结构
        
        # 处理异常情况
        if head is None:
            return None
        
        leftDummy = ListNode(0)
        rightDummy = ListNode(0)
        
        left = leftDummy
        right = rightDummy
        
        node = head
        
        while node:
            if node.val < x:
                left.next = node
                left = left.next
            else:
                right.next = node
                right = right.next
            node = node.next
        
        right.next = None
        left.next = rightDummy.next
        
        return leftDummy.next
```

### 复杂度分析

> 时间上，遍历一次链表，时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$

