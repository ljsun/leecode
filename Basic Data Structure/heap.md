# 堆 - heap

[参考链接 - 纸上谈兵：堆](https://www.cnblogs.com/vamei/archive/2013/03/20/2966612.html)

[参考链接 - 维基百科：堆](https://zh.wikipedia.org/wiki/%E5%A0%86%E7%A9%8D)

[参考链接 - algorithm.yuanbin.me：堆](https://algorithm.yuanbin.me/zh-hans/basics_data_structure/heap.html)

**维基百科：**堆（英语：Heap）**是[计算机科学](https://zh.wikipedia.org/wiki/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6)中的一种特别的树状[数据结构](https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84)。若是满足以下特性，即可称为堆：“给定堆中任意节点 P 和 C，若 P 是 C 的母节点，那么 P 的值会小于等于（或大于等于） C 的值”。若母节点的值恒**小于等于**子节点的值，此堆称为**最小堆（英语：min heap）**；反之，若母节点的值恒**大于等于**子节点的值，此堆称为**最大堆（英语：max heap）**。在堆中最顶端的那一个节点，称作**根节点（英语：root node）**，根节点本身没有**母节点（英语：parent node）。

通常情况下，堆指的是二叉堆，二叉堆的逻辑结构是完全二叉树，物理结构通常是数组。根节点最大的堆叫做最大堆或大根堆，根节点最小的叫最小堆或小根堆。**常被用作实现优先队列**

为什么是叫优先队列，因为每次pop时，总是pop出根节点【而根节点要么是值最大，要么是值最小的节点】

## 特点

1. 逻辑形式为完全二叉树，物理形式通常为数组
2. 在索引为０开始的数组中：
   - 父节点`i`的左子节点位置`(2*i+1)`
   - 父节点`i`的右子节点位置`(2*i+2)`
   - 子节点`i`的父节点位置`floor((i-1)/2)`

## 堆的基本操作

1. **插入操作[push]：**在进行插入操作的时候，会破坏堆的性质，所以要进行名为`percolate_up`的操作（以小根堆为例），以进行恢复。新插入的节点new放在完全二叉树最后的位置，再和父节点比较。如果new节点比父节点小，那么交换两者。交换之后，继续和新的父节点比较... 直到new节点不比父节点小，或者最终new节点成为了新的根节点。
2. **删除操作[pop]**：当删除根节点后，我们会得到对应的两棵子树（这两棵子树是以之前删除的节点为根），我们需要基于它们重构堆，进行`percolate_down`的操作：让最后一个节点last成为新的根节点，然后last节点不断的和子节点比较。如果last节点比两个子节点中小的那个大，则和该子节点交换。直到last节点不大于任一子节点（或者last节点成为叶节点）为止。
3. **创建最大堆：将堆所有数据重新排序**（利用插入操作思想）

- **删除对应shift_down方法，**
- **插入对应shift_up方法**
- **自低向上建堆对应shift_down方法**
- **自顶向下建堆对应shift_up方法**

**下面以自低向上建堆为例**

### python

```python
class MaxHeap:
    def __init__(self, array=None):
        if array:
            self.heap = self._max_heapify(array)
        else:
            self.heap = []

    def sift_down(self, array, start, end):
        """最大堆调整"""
        while True:
            child = 2 * start + 1
            if child > end:
                break
            if child + 1 <= end and array[child] < array[child+1]:
                child += 1
            if array[start] < array[child]:
                array[start], array[child] = array[child], array[start]
                start = child
            else:
                break

    def shft_up(self, array, i):
        # move node up the tree
        # 节点i的值一直和父节点比较。最终，把节点i的值放在对应的位置
        # 认为节点i向上移的时候，对应的堆是建好的，即[0。。。i-1]是建好的堆
        if i == 0:
            return
        father = (i - 1) // 2
        if array[father] < array[i]:
            array[father], array[i] = array[i], array[father]
            self.shft_up(array, father)

    def _max_heapify(self, array):
        # 创建最大堆
        for start in range((len(array)-2)//2, -1, -1):
            self.sift_down(array, start, len(array)-1)

        return array

    def push(self, item):
        self.heap.append(item)
        self.shft_up(self.heap, len(self.heap)-1)

    def pop(self):
        self.heap[0], self.heap[-1] = self.heap[-1], self.heap[0]
        item = self.heap.pop()
        self.sift_down(self.heap, 0)
        return item
```

**自顶向下建堆的具体思想**：
假设原数组为A，那么一般需要一个新的数组B来存储建好的堆。过程为:

- 将A中的元素逐个放入B中，放入时比较该元素与father元素的值看需不需要交换
- 如果不需要，则放下一个元素，如果需要则交换，然后比较交换后的元素继续与其父元素比较直到不需要交换为止**【因此在上面说自顶向下建堆对应shift_up操作】**
- 对A中所有的元素都进行上述操作