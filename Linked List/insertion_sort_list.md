# Question

- leecode [对链表进行插入排序](https://leetcode-cn.com/problems/insertion-sort-list/)

## 题目描述

**插入排序算法：**

1. 插入排序是迭代的，每次只移动一个元素，直到所有元素可以形成一个有序的输出列表。
2. 每次迭代中，插入排序只从输入数据中移除一个待排序的元素，找到它在序列中适当的位置，并将其插入。
3. 重复直到所有输入数据插入完为止。

**示例 1：**

```
输入: 4->2->1->3
输出: 1->2->3->4

```

**示例 2：**

```
输入: -1->5->3->4->0
输出: -1->0->3->4->5
```

## 题解１

思路在代码注释中

### python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def insertionSortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        # 处理异常情况
        
        # 由于链表只能从前向后遍历，所以要是按照数组的插入排序的方法思路去做，估计是做不出来滴
        # 所以要理解插入排序的本质
        # 注意插入排序的本质是将未排序的元素逐一添加到已排序元素的序列中去
        # 下面这个方法是抄yuanbin的【由于自己脑子笨，所以最好理解并“背下”这种思路】
        dummy = ListNode(0)
        curr = head
        while curr:
            copy_dummy = dummy
            while copy_dummy.next and copy_dummy.next.val < curr.val:
                copy_dummy = copy_dummy.next
            # 记录curr的下一个节点
            temp = curr.next
            curr.next = copy_dummy.next
            copy_dummy.next = curr
            curr = temp
        
        return dummy.next
```

### 复杂度分析

> 时间上，最好情况是原链表正好是从小到大，最坏是原链表是从大到小，这两种情况复杂度都为$O(n^2)$
>
> 空间上，额外空间为$O(1)$

## 题解２

思路在代码注释中

### python

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def insertionSortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        # 处理异常情况
        
        # 由于链表只能从前向后遍历，所以要是按照数组的插入排序的方法思路去做，估计是做不出来滴
        # 所以要理解插入排序的本质
        # 注意插入排序的本质是将未排序的元素逐一添加到已排序元素的序列中去
        # 下面这个方法是抄yuanbin的【由于自己脑子笨，所以最好理解并“背下”这种思路】
        
        # 如何降低时间复杂度，对于已经是升序的部分，我们大可不必再进行操作
        # 个人认为大体就1-2-3->-1、4-1-2-3、1-2->-1-3这三种情况，把这三种情况先想明白怎么处理
        dummy = ListNode(0)
        dummy.next = head
        curr = head
        while curr:
            if curr.next and curr.next.val < curr.val:
                # 开始插入
                copy_dummy = dummy
                while copy_dummy and copy_dummy.next.val < curr.next.val:
                    copy_dummy = copy_dummy.next
                temp = curr.next.next
                curr.next.next = copy_dummy.next
                copy_dummy.next = curr.next
                curr.next = temp
            else:
                curr = curr.next
        return dummy.next
```

### 复杂度分析

> 时间上，最好情况是原链表正好从小到大，复杂度为$O(n)$. 最坏是原链表从大到小，复杂度为$O(n^2)$
>
> 空间上，使用的额外空间为$O(1)$