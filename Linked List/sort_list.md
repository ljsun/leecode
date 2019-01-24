# Question

- leecode [排序链表](https://leetcode-cn.com/problems/sort-list/)

## 题目描述

在 *O*(*n* log *n*) 时间复杂度和常数级空间复杂度下，对链表进行排序。

**示例 1:**

```
输入: 4->2->1->3
输出: 1->2->3->4

```

**示例 2:**

```
输入: -1->5->3->4->0
输出: -1->0->3->4->5
```

## 题解

这道题再次证明了自己对各个排序算法其实一点儿也不了解

### python

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def sortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        # 首先声明，这道题还要多做几遍【重要的是，各种排序算法其实自己并没有掌握】
        
        # 根据别人的思路，使用归并排序来做
        
        # 处理异常情况
        if head is None or head.next is None:
            return head
        # 寻找中间节点
        mid = self.findmid(head)
        head1 = head
        head2 = mid.next
        mid.next = None
        right = self.sortList(head1)
        left = self.sortList(head2)
        
        return self.merge(right, left)
        
    
    def merge(self, head1, head2):
        # 合并两个已经排好序的链表
        dummy = ListNode(0)
        curr_node = dummy
        while head1 and head2:
            if head1.val < head2.val:
                curr_node.next = head1
                head1 = head1.next
            else:
                curr_node.next = head2
                head2 = head2.next
            curr_node = curr_node.next
        
        # 判断到底是head1为None还是head2为None
        if head1:
            curr_node.next = head1
        elif head2:
            curr_node.next = head2
        
        return dummy.next
    
    def findmid(self, head):
        # 利用快慢指针寻找中间节点
        fast = head
        slow = ListNode(0)
        slow.next = head
        while fast:
            fast = fast.next
            slow = slow.next
            if fast:
                fast = fast.next
        
        return slow
```

### 复杂度分析

> 时间上，归并排序时间复杂度为$O(nlogn)$，即使加上findmid时间，最终的时间复杂度级别仍是$O(nlogn)$
>
> 空间上，使用的额外空间为$O(1)$