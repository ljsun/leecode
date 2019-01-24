# Question

- lintcode：[Subarray Sum](https://www.lintcode.com/problem/subarray-sum/description)

## 题目描述

Given an integer array, find a subarray where the sum of numbers is **zero**. Your code should return the index of the first number and the index of the last number.

### Example

Given `[-3, 1, 2, -3, 4]`, return `[0, 2]` or `[1, 3]`.

## 题解１　

看到这个题，首先能够想到的笨方法就是遍历所有的子串，然后判断子串和。但是这样做就是两个嵌套的循环，时间复杂度估计挺高的。同时要注意在遍历子串然后求和时，也要有技巧。让前一个子串的和加上当前索引值就得到当前的子串和。

### python 

```python
class Solution:
    """
    @param nums: A list of integers
    @return: A list of integers includes the index of the first number and the index of the last number
    """
    def subarraySum(self, nums):
        for i in range(len(nums)):
            curr_sum = nums[i]
            if curr_sum == 0:
                return [i, i]
            j = i+1
            while j < len(nums):
                curr_sum += nums[j]
                if curr_sum == 0:
                    return[i, j]
                j += 1
```

### 复杂度分析

> 该方法是要遍历所有的子串，因此时间复杂度为$O([n(n+1)]/2)$ ,从幂指数讲就是$O(n^2)$
>
> 由于没有申请额外的空间，因此空间复杂度为$O(n)$

## 题解２

我们可以换个思路来想， 定义$f(i)$与$f(j)$分别为子串0~i和子串0~j的值。假设现在存在从i到j的子串和为０，说明什么呢？说明$f(i)$与$f(j)$的值相同。那么我们就可以遍历求$f(i)$的值然后存起来，然后判断当前的$f$值在之前是否已经出现过

### python

```python
class Solution:
    """
    @param nums: A list of integers
    @return: A list of integers includes the index of the first number and the index of the last number
    """
    def subarraySum(self, nums):
        sum_i = []
        curr_sum = 0
        for i in range(len(nums)):

            curr_sum += nums[i]
            if curr_sum == 0:
                return [0, i]
            for j in range(len(sum_i)):
                if sum_i[j] == curr_sum:
                    return[j+1, i]

            sum_i.append(curr_sum)
```

### 复杂度分析

> 首先遍历求$f$的值时，需要复杂度为$O(n)$，然后还要从sum_i中进行查找，因此最终的时间复杂度为两者相乘。幂指数仍为２，最终的时间复杂度为$O(n^2)$
>
> 从空间上看，申请了额外的数组，因此空间复杂度为$O(n+n)$

##　题解３

在题解２中，我们是将$f$值存在数组中，我们完全可以使用hashmap来进行存储，因为hashmap的查找速度快。

### python

```python
class Solution:
    """
    @param nums: A list of integers
    @return: A list of integers includes the index of the first number and the index of the last number
    """
    def subarraySum(self, nums):
        sum_i = {}
        curr_sum = 0
        for i in range(len(nums)):

            curr_sum += nums[i]
            if curr_sum == 0:
                return [0, i]

            if curr_sum in sum_i:

                return [sum_i[curr_sum], i]

            sum_i[curr_sum] = i+1
```

### 复杂度分析

> 遍历数组需要的时间复杂度为$O(n)$，假设哈希表的长度为l，那么查找时间复杂度为$O(l)$。最终时间复杂度为二者相乘
>
> 空间上申请了额外的存储空间，因此空间复杂度为$O(n+l)$

## 题解４

同样是在题解２的基础上，我们可以先将计算得到的$f$值进行排序，然后再逐个遍历$f$值是否相同，此时就只用比较相邻的$f$值是否相同即可。

### python

```python
class Solution:
    """
    @param nums: A list of integers
    @return: A list of integers includes the index of the first number and the index of the last number
    """
    def subarraySum(self, nums):
        sum_index = []
        curr_sum = 0
        for i in range(len(nums)):
            curr_sum += nums[i]
            
            if curr_sum == 0:
                return [0, i]
            
            sum_index.append([curr_sum, i])
            
        sum_index.sort(key=lambda x:x[0])
        for idx in range(len(sum_index)-1):
            if sum_index[idx][0] == sum_index[idx+1][0]:
                if sum_index[idx][1] < sum_index[idx+1][1]:
                    return [sum_index[idx][1]+1, sum_index[idx+1][1]]
                else:
                    return [sum_index[idx+1][1], sum_index[idx][1]]
```

### 复杂度分析

> 遍历求子串和，时间复杂度为$O(n)$，空间复杂度为$O(n)$。
>
> 排序的时间复杂度为$O(nlogn)$，空间复杂度为$O(n)$
>
> 再次遍历排序后的和，最坏情况下时间复杂度为$O(n)$

