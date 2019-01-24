# Quick Sort - 快速排序

**核心**：快排是一种采用分治思想的排序算法，大致分为三个步骤。

1. 定基准－－首先随机选择一个元素为基准
2. 划分区－－所有比基准小的元素置于基准左侧，比基准大的元素置于右侧
3. 递归调用－－递归地调用此切分过程

## out-in-place - 非原地快排

**容易实现和理解的一个方法是采用递归，使用python实现如下所示：**

```python
def qsort1(alist):                      
    ...:     print(alist)
    ...:     if len(alist) <= 1:
    ...:         return alist
    ...:     else:
    ...:         pivot = alist[0]
    ...:         return qsort1([x for x in alist[1:] if x < pivot]) + [pivot] + qsort1([x for x in alist[1:] if x >=
    ...: pivot])

```

**【递归＋非原地排序】**的实现虽然简单易懂，但是如此一来【快速排序】便不再是最快的普通排序算法了，因为递归调用过程中非原地排序需要生成新数组，空间复杂度颇高

### 复杂度分析

在最好的情况下，快速排序的基准元素正好是整个数组的中位数，可近似为二分，此时的递归层数为$log n$.　分析下此时的空间复杂度。**首先来看看什么叫空间复杂度**－－简单来讲可以认为是程序在运行过程中所占用的空间复杂度大小。那么对于递归的 out-in-place 调用而言，排除函数调用等栈空间，**最好情况下，每往下递归调用一层，所需要的存储空间是上一层中的一半。完成最底层的调用后即向上返回执行出栈操作，故并不需要保存每层所有元素的值。**所以需要的总的存储空间就是$\sum_{i=0} \frac {n}{2^i} = 2n$

那么在最坏情况下out-in-place需要消耗多少额外空间呢？最坏情况是每次递归需要存储的元素只是少１．故总的时间复杂度为$\sum_{i=0}^{n}(n-i+1) = O(n^2)$

> 时间复杂度，最好情况下为$O(NlogN)$，最坏情况下为$O(N^2)$

## in-place - 原地排序

### one index for partition

```python
def qsort2(alist, l, u):
    ...:     print(alist)
    ...:     if l >= u:
    ...:         return 
    ...:     m = l
    ...:     for i in range(l+1, u+1):
    ...:         if alist[i] < alist[u]:
    ...:             m += 1
    ...:             alist[m], alist[i] = alist[i], alist[m]
    ...:     alist[m], alist[l] = alist[l], alist[m]
    ...:     qsort2(alist, l, m-1)
    ...:     qsort2(alist, m+1, u)

```

### 复杂度分析

> 时间上，最好情况下为$O(NlogN)$，最坏情况下为$O(N^2)$
>
> **空间上，个人认为：最好情况下的空间复杂度（使用的栈空间）为$O(N/2)$**
>
> **最坏情况下的空间复杂度（使用栈空间）为$O(N)$**



### Two-way partitioning

```
def qsort3(alist, lower, upper):
    ...:     print(alist)
    ...:     if lower >= upper:
    ...:         return
    ...:     pivot = alist[lower]
    ...:     left, right = lower+1, upper
    ...:     while left <= right:
    ...:         while left <= right and alist[left] < pivot:
    ...:             left += 1
    ...:         while left <= right and alist[right] >= pivot:
    ...:             right -= 1
    ...:         if left > right:
    ...:             break
    ...:         alist[left], alist[right] = alist[right], alist[left]
    ...:     alist[lower], alist[right] = alist[right], alist[lower]
    ...:     qsort3(alist, lower, right-1)
    ...:     qsort3(alist, right+1, upper)

```

### 复杂度分析

> 时间上，最好情况下为$O(NlogN)$，最坏情况下为$O(N^2)$。和one index for partition相比有什么有点呢？**貌似是在全等数组情况下提高了时间复杂度**【**至今也不是太理解**】
>
> **空间上，个人认为：最好情况下的空间复杂度（使用的栈空间）为**$O(N/2)$
>
> **最坏情况下的空间复杂度（使用栈空间）为$O(N)$**