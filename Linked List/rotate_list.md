# Question

- leecode [旋转链表](https://leetcode-cn.com/problems/rotate-list/)

## 题目描述

给定一个链表，旋转链表，将链表每个节点向右移动 *k *个位置，其中 *k *是非负数。

**示例 1:**

```
输入: 1->2->3->4->5->NULL, k = 2
输出: 4->5->1->2->3->NULL
解释:
向右旋转 1 步: 5->1->2->3->4->NULL
向右旋转 2 步: 4->5->1->2->3->NULL

```

**示例 2:**

```
输入: 0->1->2->NULL, k = 4
输出: 2->0->1->NULL
解释:
向右旋转 1 步: 2->0->1->NULL
向右旋转 2 步: 1->2->0->NULL
向右旋转 3 步: 0->1->2->NULL
向右旋转 4 步: 2->0->1->NULL
```

## 题解

其实就是要思考如何从根据原链表“较快简单的”得到“旋转”后的链表。还有要注意寻找分割点的方法

具体思路在代码注释中

### python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def rotateRight(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        
        # 找到分割点，从后向前数第k个位置，然后将前半部分拼接到后半部分上
        # 如何寻找到最佳的分割点，利用两个指针呀
        
        # 处理异常情况
        if head is None:
            return None
        # 先找长度
        length = 0
        curr = head
        while curr:
            curr = curr.next
            length += 1
        
        offset = k % length
        fast = head
        position = 0
        while position < offset:
            fast = fast.next
            position += 1
        slow = head
        # slow与fast同时向前走
        while fast.next:
            fast = fast.next
            slow = slow.next
        
        fast.next = head
        head = slow.next
        slow.next = None
    
        return head
```

### 复杂度分析

> 时间上，虽然三个循环，但是并不嵌套，因此总的时间复杂度仍为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$

