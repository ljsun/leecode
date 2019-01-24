# Question

- leecode [翻转链表2](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

## 题目描述

反转从位置 *m* 到 *n* 的链表。请使用一趟扫描完成反转。

**说明:**
1 ≤ *m* ≤ *n* ≤ 链表长度。

**示例:**

```
输入: 1->2->3->4->5->NULL, m = 2, n = 4
输出: 1->4->3->2->5->NULL
```

## 题解

这道题思路和别人想的差不多，就是自己没写出来（其实是写的太乱了，没成功）。。。还是看别人的代码

### python

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """
        # 处理异常情况
        
        # 先找到第m个节点，然后反转m~n位置的节点
        dummy = ListNode(0)
        
        dummy.next = head
        
        m_pre_node = dummy
        for i in range(m-1):
            m_pre_node = m_pre_node.next
            
        # 反转m~n之间的节点
        prev = None
        curr = m_pre_node.next
        while m<=n:
            temp = curr.next
            curr.next = prev
            prev = curr
            curr = temp
            m += 1
        
        m_pre_node.next.next = curr
        m_pre_node.next = prev
        
        return dummy.next
```

### 复杂度分析

> 时间上，虽然两个循环，但是时间复杂度仍为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$