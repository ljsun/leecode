# Linked List - 链表

链表是线性表的一种。线性表是最基本、最简单、也是最常见的一种数据结构。线性表中数据元素之间的关系是一对一的关系，即除了第一个和最后一个数据元素外，其他全是首尾相接。线性表有两种存储方式，一种是顺序存储结构，另一种是链式存储结构。数组就是一种典型的顺序存储结构。

相反，链式存储结构的两个相邻的元素在内存中可能不是相邻的，每个元素都有一个指针域，指针域一般是存储着到下一个元素的指针。这种存储方式优点是定点插入和定点删除的时间复杂度是O(1)，不会浪费太多内存，添加元素时才会申请内存，删除元素时释放内存，缺点是访问的时间复杂度最坏为O(n)

顺序表的特性是随机读取，也就是访问一个元素的时间复杂度是O(1)，链式表的特性是插入和删除的时间复杂度是O(1)

链表是链式存储的线性表。根据指针域的不同，链表分为单向链表、双向链表、循环链表等。
链表的前提，我已经知道了头结点

## 链表的基本操作

### 反转链表

​	链表的基本形式是：1 -> 2 -> 3 -> null，反转需要变为 3 -> 2 -> 1 -> null

​	反转链表时需要注意

- 访问某个节点curr.next时，要检验curr是否为null
- 要把反转后的最后一个节点指向（即反转前的第一个节点）指向null

```python
class ListNode(object):
    def __init__(self, val):
        self.val = val
        self.next = None

    # 反转链表之单向链表
    # 迭代的方式
    def iter_reverse(self, head):
        prev = None
        while head:
            temp = head.next
            head.next = prev
            prev = head
            head = temp
        return prev

    # 反转链表之单向链表
    # 递归的方式
    # 参考链接https://blog.csdn.net/FX677588/article/details/72357389
    def recur_reverse(self, head):
        if head is None or head.next is None:
            return head

        next = head.next
        newHead = self.recur_reverse(next)
        next.next = head
        head.next = None
        return newHead

    # 反转链表之双向链表
    def double_iter_reverse(self, head):
        curr = None
        while head:
            curr = head
            head = curr.next
            curr.next = curr.prev
            curr.prev = head

        return curr
```
> 迭代方式时间复杂度O(n)，空间复杂度O(1)
> 递归方式时间复杂度O(n)，空间复杂度O(1)
#### 快慢指针

​	快慢指针也是一个可以用于很多问题的技巧。所谓快慢指针中的快慢指的是指针向前移动的步长，每次移动的步长较大即为快，步长较小即为慢。常用的快慢指针一般是在单链表中让快指针每次向前移动2，慢指针每次向前移动1。快慢两个指针都是从链表头开始遍历，于是快指针到达链表末尾的时候慢指针正好到达中间位置，于是可以得到中间元素的值。快慢指针在链表相关问题中主要有两个应用：

- 快速找出未知长度单链表的中间节点，设置两个指针 *fast、*slow都指向单链表的头结点，其中fast的移动速度是slow的2倍，当fast指向末尾节点时，slow正好就在中间了。
- 利用快慢指针的原理判断单链表是否有环。同样设置两个指针fast、slow都指向单链表的头结点，其中fast的移动速度是slow的2倍。如果fast=NULL，说明单链表是以NULL结尾，不是循环链表；如果fast=slow，则快指针追上慢指针，说明是循环链表。

```python
# 快慢指针判断是否有环
class NodeCircle(object):
    def __init__(self, val):
        self.val = val
        self.next = None

    def has_circle(self, head):
        slow = head
        fast = head
        while slow and fast:
            slow = slow.next
            fast = fast.next
            # 保证fast移动速度是slow的2倍
            if fast:
                fast = fast.next
            if fast == slow:
                break

        if fast and slow and fast == slow:
            return True
        else:
            return False
```
