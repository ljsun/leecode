# Question

- leecode [环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)

## 题目描述

**示例 1：**

```
输入：head = [3,2,0,-4], pos = 1
输出：true
解释：链表中有一个环，其尾部连接到第二个节点。
```

## 题解

解题思路在代码注释中

### python

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        # 判断链表中是否有环，依稀记得使用fast和slow指针
        
        # 处理异常情况
        if head is None:
            return False
        
        # fast移动速度是slow的2倍，如果有环，则fast总能追上slow
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
            return True
        else:
            return False
```

### 复杂度分析

> 时间上，没有环时，复杂度为$O(n/2)$，有环时，时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$

