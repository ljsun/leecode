# Question

- leecode [重排链表](https://leetcode-cn.com/problems/reorder-list/)

## 题目描述

给定一个单链表 *L*：*L*0→*L*1→…→*L**n*-1→*L*n ，
将其重新排列后变为： *L*0→*L**n*→*L*1→*L**n*-1→*L*2→*L**n*-2→…

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

**示例 1:**

```
给定链表 1->2->3->4, 重新排列为 1->4->2->3.
```

**示例 2:**

```
给定链表 1->2->3->4->5, 重新排列为 1->5->2->4->3.
```

## 题解１[TLE]

这个是自己想到的笨方法，很“直接”的方法，就是在“生成”每一个节点时，都去寻找该节点所在的位置，然后一步步往下做

### python

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reorderList(self, head):
        """
        :type head: ListNode
        :rtype: void Do not return anything, modify head in-place instead.
        """
        # 就先按照自己想的笨方法一点点往下做
        
        # 处理异常情况
        
        # 计算链表的长度
        length = 0
        l = head
        while l:
            length += 1
            l = l.next
            
        # 开始重新排序链表
        curr_head = head
        for index in range(1, (length+1)//2 + 1):
            # 遍历得到curr_head和curr_tail
            count = 0
            curr_tail = curr_head
            while count < length-2*index+1:
                curr_tail = curr_tail.next
                count += 1
            if curr_tail == curr_head or curr_head.next == curr_tail:
                curr_tail.next = None
                break 
            temp = curr_head.next
            curr_tail.next = temp
            curr_head.next = curr_tail
            curr_head = temp
```

### 复杂度分析

> 时间上，有嵌套循环，复杂度为平方级别$O(n^2)$，细算下来，嵌套循环的循环次数为$1+3+5+ ... + length-2$
>
> 空间上，使用的额外空间为$O(1)$

## 题解２

其实这种思路也挺简单，只是如果老是处于代码应该怎么写，能不能实现前提下，就不太好想到这种思路【针对自己而言】

将链表分为两部分，后半部分反转，然后前半部分与后半部分一一对应起来就得到了要返回的链表

### python

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reorderList(self, head):
        """
        :type head: ListNode
        :rtype: void Do not return anything, modify head in-place instead.
        """
        # 其实这种思路知道后也挺简单的，只要敢想
        
        # 其实抛开代码，就人为的去做这道题，自然而然的思路应该是
        # 将链表分为两部分，后半部分反转，然后前半部分与后半部分一一对应起来
        
        # 先找到middel node，链表分为两部分
        # 使用快慢指针找到middle节点
        dummy = ListNode(0)
        dummy.next = head
        fast = head
        slow = dummy
        while fast:
            fast = fast.next
            slow = slow.next
            if fast:
                fast = fast.next
        right = slow.next
        slow.next = None
        
        # 反转后半部分链表
        prev = None
        while right:
            temp = right.next
            right.next = prev
            prev = right
            right = temp
        
        # 合并前半部分和后半部分链表
        left = head
        right = prev
        while left and right:
            l_temp = left.next
            r_temp = right.next
            
            left.next = right
            right.next = l_temp
            
            left = l_temp
            right = r_temp
```

### 复杂度分析

> 时间上，虽然有三个循环，但是并没有嵌套，因此时间复杂度是线性的，为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$