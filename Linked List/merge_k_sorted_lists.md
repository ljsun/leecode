# Question

- leecode [合并k个排序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/)

## 题目描述

合并 *k*个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

**示例:**

```
输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
```

## 题解１

这个是自己想到的笨方法，相当于在获得新链表的每一个节点时遍历下所有候选链表的相应节点，然后得到值最小的节点

### python

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        # 先仿照合并两个排序链表，写个笨方法
        
        # 处理异常情况
        
        dummy = ListNode(0)
        node = dummy
        while 1:
            curr_node_index = None
            curr_min = 1000000
            has_value = False
            for i in range(len(lists)):
                if lists[i] and lists[i].val < curr_min:
                    curr_min = lists[i].val
                    curr_node_index = i
                    has_value = True
            if has_value:
                node.next = lists[curr_node_index]
                lists[curr_node_index] = lists[curr_node_index].next
                node = node.next
            else:
                break
            
        return dummy.next
```

### 复杂度分析

> 时间上，双重循环，时间复杂度为$O(n*m)$
>
> 空间上，使用的额外空间为$O(1)$

## 题解２

这种思路自我感觉有点钻空子了，因为最核心的还是利用python内部的sorted函数了

具体思路是先将链表中的数据全部“怼”到list中，然后排序，最终生成返回的链表

### python

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        # 自己能想到的另一种思路，将数据全部都怼到list中，然后排序，返回新的链表
        
        newList=  []
        for l in lists:
            while l:
                newList.append([l.val, l])
                l = l.next
        
        # 对newList进行排序
        newList = sorted(newList, key=lambda x: x[0])
        
        dummy = ListNode(0)
        curr_node = dummy
        for node in newList:
            curr_node.next = node[1]
            curr_node = curr_node.next
        
        return dummy.next
```

### 复杂度分析

> 时间上，python内部的sorted时间复杂度为$O(nlog n)$
>
> 空间上，使用的额外空间为$O(2n)$

## 题解３

[yuanbin](https://algorithm.yuanbin.me/zh-hans/linked_list/merge_k_sorted_lists.html)提出的高端的二分搜索方法