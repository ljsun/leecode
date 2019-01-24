# Heap Sort - 堆排序

堆排序通常基于**二叉堆**实现。以大根堆为例，堆排序的实现过程分为两个子过程。第一步为取出大根堆的根节点（当前堆的最大值），由于取走了一个节点，故需要对余下的元素重新建堆。重新建堆后继续取根节点，循环直至取完所有节点，此时数组已经有序。

**以下以自底向上建堆为例**

## python

```python
class HeapSort:
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

    def sort(self, array):
        # 创建最大堆
        for start in range((len(array)-2)//2, -1, -1):
            self.sift_down(array, start, len(array)-1)

        # 堆排序
        for end in range(len(array)-1, 0, -1):
            array[0], array[end] = array[end], array[0]
            self.sift_down(array, 0, end-1)

if __name__ == '__main__':
    A = [19, 1, 10, 14, 16, 4, 4, 7, 9, 3, 2, 8, 5, 11]
    HeapSort().sort(A)
    print(A)
```

## 复杂度分析

[参考链接](https://blog.csdn.net/YuZhiHui_No1/article/details/44258297)

> 【自低向上建堆】初始化建堆时间为$O(n)$，更改堆元素后重新建堆时间$O(nlogn)$，因此总的时间复杂度为$O(nlogn)$
>
> 【自顶向下建堆建堆时间为$O(n)$
>
> 空间复杂度为$O(1)$

