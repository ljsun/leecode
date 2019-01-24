# Bubble Sort - 冒泡排序

核心：相邻元素之间进行比较，每次总是将大（小）的元素向后置，这样一轮过后，最大（小）的元素总是在最后一位。。经过多轮操作就完成了排序。

```python
def bubbleSort(alist):
	for i in range(len(alist), 0, -1):
		for j in range(i-1):
			if alist[j] > alist[j+1]:
				temp = alist[j]
                alist[j] = alist[j+1]
                alist[j+1] = temp
	return alist
```

> 复杂度分析：
>
> 时间上，复杂度为$O(n^2)$
>
> 空间上，额外空间为$O(1)$

