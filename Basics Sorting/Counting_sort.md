# Counting Sort

重点看参考

- [计数排序 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/%E8%AE%A1%E6%95%B0%E6%8E%92%E5%BA%8F)
- [Counting Sort Visualization](https://www.cs.usfca.edu/~galles/visualization/CountingSort.html)

刚开始看Counting Sort, 自己确实是有点蒙的。多看几遍感觉还可以，其实重点是要看计数数组和目标数组

维基百科上总结的四个步骤为【加了自己的白话】：

1. 定义计数数组C的长度大小，百科上说长度为【待排数组最大值－最小值＋１】，其实本质上就是保证待排数组的每一个都能与计数数组的某一个索引唯一对应【在第二步中有用】
2. 统计数组中每个值为i的元素出现的次数，存入计数数组C的第i项【个人感觉也没必要，保证每个值有对应的唯一索引项，放入那个唯一索引项就行】
3. 对所有计数累加（从C中第一个元素开始，每一项和前一项相加)【假设索引i对应的待排元素值为a，索引i处的值为b，那么累加后的这个索引值代表小于等于a的值一共有b个】
4. 反向填充目标数组：将每个元素ｉ放在新数组的第C[i]项，每放一个元素就将C[i]减１【目的是为了处理重复值元素，反向是保证原数组中重复元素相对位置在新数组中保持不变】

## python

```python
# encoding = utf-8
class CountSort(object):
    def __init__(self):
        pass

    def countSort(self, a):
        # 创建目标数组
        b = [0] * len(a)

        # 获取待排数组最大值与最小值，以便确定计数数组大小
        max_v = max(a)
        min_v = min(a)

        # k是计数数组大小
        k = max_v - min_v + 1
        c = [0] * k

        # 开始计数
        for i in a:
            c[i-min_v] += 1

        # 从前向后累加计数
        for i in range(1, len(c)):
            c[i] += c[i-1]

        # 反向填充目标数组
        for i in range(len(a)-1, -1, -1):
            b[c[a[i]-min_v]-1] = a[i]
            c[a[i]-min_v] -= 1

        print(b)

if __name__ == '__main__':
    a = [9, 8, 7, 7, 7]
    CountSort().countSort(a)
```

## 复杂度分析

> 最优最坏时间复杂度都为$O(n+k)$
>
> 最优最坏空间复杂度都为$O(n+k)$

