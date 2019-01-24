# Question

- leecode [两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

## 题目描述

给出两个 **非空** 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 **逆序** 的方式存储的，并且它们的每个节点只能存储 **一位** 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

**示例：**

```
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```

## 题解１

说实话，题解１是自己做出来的，虽然做的有点繁琐，写的也挺繁琐（主要情况比较多），但思路相对来说还算是比较清晰。

题解１与题解２的差别在于题解１并没有开辟新的链表空间

主要思路在注释中

### python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        # 处理异常情况，一会再写
        
        # 设置dummy节点
        l1_dummy = ListNode(0)
        l1_dummy.next = l1
        l2_dummy = ListNode(0)
        l2_dummy.next = l2
        
        l1_prev = None
        l2_prev = None
        
        # 用flag来表示是否有来自前面的进位
        flag = 0
        # 同时遍历l1和l2
        while l1 and l2:
            curr_val = l1.val + l2.val + flag
            # 判断是否需要进位
            if curr_val > 9:
                curr_val -= 10
                flag = 1
            else:
                flag = 0
            
            # 由于不知道l1与l2的长短，因此把当前curr_val同时保存到l1和l2
            l1.val = curr_val
            l2.val = curr_val
            
            l1_prev = l1
            l2_prev = l2
            
            l1 = l1.next
            l2 = l2.next
            
        # 判断出循环到底是l1还是l2为空
        if l1 is None and l2:
            while l2:
                curr_val = l2.val + flag
                if curr_val > 9:
                    curr_val -= 10
                    flag = 1
                else:
                    flag = 0
                l2.val = curr_val
                l2_prev = l2
                l2 = l2.next
            if flag:
                l2_prev.next = ListNode(flag)
            return l2_dummy.next
        elif l2 is None and l1:
            while l1:
                curr_val = l1.val + flag
                if curr_val > 9:
                    curr_val -= 10
                    flag = 1
                else:
                    flag = 0
                l1.val = curr_val
                l1_prev = l1
                l1 = l1.next
            if flag:
                l1_prev.next = ListNode(flag)
            return l1_dummy.next
        elif l1 is None and l2 is None:
            if flag:
                l1_prev.next = ListNode(flag)
            return l1_dummy.next
```

### 复杂度分析

> 时间上，遍历了一次链表，时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$

## 题解２

这个思路与代码是参考别人的

### python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        # 处理异常情况，一会再写
        
        # 设置dummy节点, 创建新的节点
        dummy = ListNode(0)
        node = dummy
        # flag代表是否有来自前方的进位
        flag = 0
        
        while l1 or l2 or flag:
            v1 = l1.val if l1 else 0
            v2 = l2.val if l2 else 0
            curr_val = v1 + v2 + flag
            if curr_val > 9:
                curr_val -= 10
                flag = 1
            else:
                flag = 0
            
            node.next = ListNode(curr_val)
            node = node.next
            
            if l1:
                l1 = l1.next
            if l2:
                l2 = l2.next
        
        return dummy.next
```

### 复杂度分析

> 时间上，遍历一次链表，时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(n)$

