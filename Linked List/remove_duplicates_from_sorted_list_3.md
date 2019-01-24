

# Question

## 题目描述

```
Write a removeDuplicates() function which takes a list and deletes
any duplicate nodes from the list. The list is not sorted.

For example if the linked list is 12->11->12->21->41->43->21,
then removeDuplicates() should convert the list to 12->11->21->41->43.
```

## 题解１

最先能够想到的就是利用双重循环了（但是实际写起来咋还那么费劲呢？？？）

### python

```python
def deleteDuplicates(self, head):
   ...:     if head is None:
   ...:         return None
   ...:     curr = head
   ...:     while curr:
   ...:         inner = curr
   ...:         while inner.next:
   ...:             if curr.val == inner.next.val:
   ...:                 inner.next = inner.next.next
   ...:             else:
   ...:                 inner = inner.next
   ...:         curr = curr.next
   ...:     return head


```

### 复杂度分析

> 时间上，嵌套循环，时间复杂度为$O(n^2)$
>
> 空间上，使用的额外空间为$O(1)$

## 题解２

利用万能的hash表（当然这个方法也不是自己想出来的）

### python

```python
def deleteDuplicates(self, head):
   ...:     if head is None:
   ...:         return head
   ...:     hash = {}
   ...:     hash[head.val] = True
   ...:     curr = head
   ...:     while curr.next:
   ...:         if hash.has_key(curr.next.val):
   ...:             curr.next = curr.next.next
   ...:         else:
   ...:             hash[curr.next.val] = True
   ...:             curr = curr.next
   ...:     return head

```

### 复杂度分析

> 时间上，遍历了一次链表，时间复杂度为$O(n)$
>
> 空间上，使用的额外空间为$O(n)$