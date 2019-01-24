# Question

- leecode [任务调度器](https://leetcode-cn.com/problems/task-scheduler/)

## 题目描述

给定一个用字符数组表示的 CPU 需要执行的任务列表。其中包含使用大写的 A - Z 字母表示的26 种不同种类的任务。任务可以以任意顺序执行，并且每个任务都可以在 1 个单位时间内执行完。CPU 在任何一个单位时间内都可以执行一个任务，或者在待命状态。

然而，两个**相同种类**的任务之间必须有长度为** n **的冷却时间，因此至少有连续 n 个单位时间内 CPU 在执行不同的任务，或者在待命状态。

你需要计算完成所有任务所需要的**最短时间**。

**示例 1：**

```
输入: tasks = ["A","A","A","B","B","B"], n = 2
输出: 8
执行顺序: A -> B -> (待命) -> A -> B -> (待命) -> A -> B.

```

**注：**

1. 任务的总个数为 [1, 10000]。
2. n 的取值范围为 [0, 100]。

## 题解

没啥说的，自己没做出来，看别人的[教学视频](https://www.youtube.com/watch?v=YCD_iYxyXoo)才懂的

### python

```python
class Solution:
    def leastInterval(self, tasks, n):
        """
        :type tasks: List[str]
        :type n: int
        :rtype: int
        """
        
        # 处理异常情况
        if tasks is None:
            return -1
        
        task_map = {}
        for task in tasks:
            if task in task_map:
                task_map[task] += 1
            else:
                task_map[task] = 1
                
        max_freq = max(task_map.values())
        
        ans = (max_freq - 1) * (n + 1) 
        for freq in task_map.values():
            if freq == max_freq:
                ans += 1
        
        return ans if ans > len(tasks) else len(tasks)
```

### 复杂度分析

> 时间上，虽然两个for循环，但是其实后一个复杂度是固定的，为$O(26)$。所以时间复杂度取决于第一个为$O(n)$
>
> 空间上，使用了额外的hash空间，为$O(26)$