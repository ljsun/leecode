# Queue-队列

Queue是一个FIFO（先进先出）的数据结构，在并发中使用较多，可以安全的将对象从一个任务传给另一个任务。

## 编程实现

### Python

Queue和Stack在Python中都是由list，[] 实现的。在python中list是一个dynamic array，可以通过append在list的尾部添加元素，通过pop()在list的尾部弹出元素实现Stack的FILO，如果是pop(0)则弹出头部的元素实现Queue的FIFO。

```python
queue = [] # same as list
size = len(queue)
queue.append(1)
queue.append(2)
queue.pop(0) # return 1
queue[0] # return 2 examine the first element
```

## Priority Queue - 优先队列

应用程序常常需要处理带有优先级的业务，优先级最高的业务首先得到服务。因此优先队列这种数据结构应用而生。优先队列中每个元素都有各自的优先级，优先级高的元素先得到服务；优先级相同的元素按照其在优先队列中的顺序得到服务。

**优先队列可以使用数组或链表实现，从时间和空间复杂度来说，往往使用二叉堆实现**

### Python

**具体的实现过程还未记录**

Python 中提供`heapq`的lib来实现 priority queue. 提供`push`和`pop`两个基本操作和`heapify`初始化操作.

| \       | methods              | time complexity |
| ------- | -------------------- | --------------- |
| enqueue | heapq.push(queue, e) | $$O(\log n)$$   |
| dequeue | heapq.pop(queue)     | $$O(\log n)$$   |
| init    | heapq.heapify(queue) | $$O(n\log n)$$  |
| peek    | queue[0]             | $$O(1)$$        |

## 双端队列

双端队列（deque，全名double-ended queue）可以让你在任何一端添加或者删除元素，因此是一种具有队列和栈的性质的数据结构。

### Python

Python的list就可以执行类似于deque的操作。但是效率会过于慢。为了提升数据的处理效率，一些高效的数据结构放在了collections中。在collections中提供了deque的类，如果需要多次对list执行头尾元素操作，使用deque。

```python
dq = Collections.deque()
```

#### Methods

| \             | methods          | time complexity |
| ------------- | ---------------- | --------------- |
| enqueue left  | dq.appendleft(e) | $$O(1)$$        |
| enqueue right | dq.append(e)     | $$O(1)$$        |
| dequeue left  | dq.popleft()     | $$O(1)$$        |
| dequeue right | dq.pop()         | $$O(1)$$        |
| peek left     | dq[0]            | $$O(1)$$        |
| peek right    | dq[-1]           | $$O(1)$$        |