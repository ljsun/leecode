# Merge Sort - 归并排序

**核心**：将两个有序对数组归并成一个更大的有序数组。通常的做法为**递归排序**，将两个不同的有序数组归并到第三个数组中。

## python

```python
class Sort:                             
    ...:     def mergeSort(self, alist):
    ...:         if len(alist) <=1:                 
    ...:             return alist
    ...:         mid = len(alist) // 2
    ...:         left = self.mergeSort(alist[:mid])
    ...:         print("left = " + str(left))
    ...:         right = self.mergeSort(alist[mid:])
    ...:         print("right = " + str(right))
    ...:         return self.mergeSortArray(left, right)
    ...:     def mergeSortArray(self, A, B):
    ...:         sortedArray = []
    ...:         l = 0
    ...:         r = 0
    ...:         while l < len(A) and r < len(B):
    ...:             if A[l] < B[r]:
    ...:                 sortedArray.append(A[l])
    ...:                 l += 1
    ...:             else:
    ...:                 sortedArray.append(B[r])
    ...:                 r += 1
    ...:         sortedArray += A[l:]
    ...:         sortedArray += B[r:]
    ...:         return sortedArray
```

## 复杂度分析

> 时间上，时间复杂度为$O(NlogN)$，复杂度稳定
>
> 空间上，使用了等长的辅助空间，空间复杂度为$O(N)$

