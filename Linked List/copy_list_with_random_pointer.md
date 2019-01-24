# Question

- leecode [复制带随机指针的链表](https://leetcode-cn.com/problems/copy-list-with-random-pointer/)

**参考[yuanbin](https://algorithm.yuanbin.me/zh-hans/linked_list/copy_list_with_random_pointer.html)的图更清晰**

## 题目描述

给定一个链表，每个节点包含一个额外增加的随机指针，该指针可以指向链表中的任何节点或空节点。

要求返回这个链表的深度拷贝。 

## 题解１

借助外部哈希表，两次遍历链表。具体的说明在代码注释中

### python

```python
# Definition for singly-linked list with a random pointer.
# class RandomListNode(object):
#     def __init__(self, x):
#         self.label = x
#         self.next = None
#         self.random = None

class Solution(object):
    def copyRandomList(self, head):
        """
        :type head: RandomListNode
        :rtype: RandomListNode
        """
        # 首先弄清楚什么是深度copy。就是开辟一个新的空间
        # 这种带有随机指针的深度copy链表的通常做法是使用哈希表
        
        # 做法通常为
        # 根据next指针新建链表
        # 维护新旧节点的映射关系
        # 拷贝旧链表中的random指针
        # 更新新链表中的random指针
        
        dummy = RandomListNode(0)
        curr_node = dummy
        hashmap = {}
        while head:
            new_node = RandomListNode(head.label)
            new_node.random = head.random
            curr_node.next = new_node
            
            hashmap[head] = new_node
            
            head = head.next
            curr_node = curr_node.next
        
        # 更新新链表中的random指针
        curr_node = dummy.next
        while curr_node:
            if curr_node.random:
                curr_node.random = hashmap[curr_node.random]
            curr_node = curr_node.next
        
        return dummy.next
```

### 复杂度分析

> 时间上，遍历两次链表，因此时间复杂度为$O(2n)$
>
> 空间上，使用了额外的哈希表，使用的额外空间为$O(2n)$

## 题解２

在题解１中，我们遍历了两次链表，遍历两次的原因是当新节点的random指针要指向某个新节点时，该新节点还没没创建，因此我们可以提前创建新节点，然后只遍历一次链表

### python

```python
# Definition for singly-linked list with a random pointer.
# class RandomListNode(object):
#     def __init__(self, x):
#         self.label = x
#         self.next = None
#         self.random = None

class Solution(object):
    def copyRandomList(self, head):
        """
        :type head: RandomListNode
        :rtype: RandomListNode
        """
        # 首先弄清楚什么是深度copy。就是开辟一个新的空间
        # 这种带有随机指针的深度copy链表的通常做法是使用哈希表
        
        # 在方法１中，我们是遍历了两次，能不能一次遍历就把事给办了
        # 假设现在新链表的random节点要指向一个节点，但是这个节点按照正常顺序
        # 还没有被创建，我们能不能提前先创建出这个节点 ...
        
        dummy = RandomListNode(0)
        curr_node = dummy
        hashmap = {}
        
        while head:
            # head节点可能已经创建了
            if head in hashmap.keys():
                new_node = hashmap[head]
            else:
                # 需要创建新节点了
                new_node = RandomListNode(head.label)
            hashmap[head] = new_node
            curr_node.next = new_node
            # 判断需不需要处理random指针
            if head.random:
                if head.random in hashmap:
                    new_node.random = hashmap[head.random]
                else:
                    new_node.random = RandomListNode(head.random.label)
                    hashmap[head.random] = new_node.random
            
            head = head.next
            curr_node = curr_node.next
        
        return dummy.next
```

### 复杂度分析

> 时间上，遍历了一次链表，时间复杂度为$O(n)$
>
> 空间上，使用了额外的哈希表，使用的额外空间为$O(2n)$

## 题解２

前两种方法使用了额外的空间，我们能不能考虑不使用额外的空间 ，具体的图解看[yuanbin](https://algorithm.yuanbin.me/zh-hans/linked_list/copy_list_with_random_pointer.html)

### python

```python
# Definition for singly-linked list with a random pointer.
# class RandomListNode(object):
#     def __init__(self, x):
#         self.label = x
#         self.next = None
#         self.random = None

class Solution(object):
    def copyRandomList(self, head):
        """
        :type head: RandomListNode
        :rtype: RandomListNode
        """
        # 首先弄清楚什么是深度copy。就是开辟一个新的空间
        # 这种带有随机指针的深度copy链表的通常做法是使用哈希表
        
        # 现在考虑不使用额外空间，或者使用比较少的额外空间
        
        # 这种方法具体的图解见yuanbin
        # 具体的实施步骤为:
        # 将新节点依次拷贝到旧节点后面（旧节点指向对应的新节点）
        # 处理新节点的random指针
        # 将链表拆分为新链表与旧链表
        
        # 处理异常情况
        if head is None:
            return None
        
        # step1 复制新节点并链接到旧节点后面
        curr = head
        while curr:
            new_node = RandomListNode(curr.label)
            temp = curr.next
            curr.next = new_node
            new_node.next = temp
            curr = temp
        
        # step2 让新节点的random指针指向对应的新节点
        curr = head
        while curr:
            if curr.random:
                curr.next.random = curr.random.next
            curr = curr.next.next
        
        # step3 分离新旧链表【貌似有个前提，不能改变原链表】
        curr = head
        new_head = head.next
        while curr:
            newNode = curr.next
            curr.next = curr.next.next
            if newNode.next:
                newNode.next= newNode.next.next
            
            curr = curr.next
        return new_head

```

### 复杂度分析

> 时间上，虽然有三个循环，但并没有嵌套，因此时间复杂度仍为$O(n)$
>
> 空间上，使用的额外空间为$O(1)$

