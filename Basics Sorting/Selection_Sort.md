# Selection Sort - 选择排序

核心：每一轮都从剩下的未排序元素中找到最大（小）的元素，然后放到相应的位置，这样的话相当于每一轮就确定了一个元素的位置，多轮之后就确定了所有元素的位置，即排好了序。

	1. 找到数组中的最大（小）元素并将其和第一个元素交换位置
	2. 在剩下的元素中找到最大（小）元素并将其与数组第二个元素交换，直至整个数组排序

性质：

- 比较次数 = (N-1)+(N-2)+(N-3)+...+2+1 ~ $N^2$/2
- 交换次数 = N
- 数据移动最少

```python
def selectionSort(alist):
    for i in range(len(alist)):
		min_index = i
        for j in range(i+1, len(alist)):
            if alist[j] < alist[min_index]:
				min_index = j
        temp = alist[i]
        alist[i] = alist[min_index]
        alist[min_index] = temp
        
    return alist
```

> 复杂度分析
>
> 时间上，复杂度为$O(n^2)$
>
> 空间上，使用了额外的空间为$O(1)$

