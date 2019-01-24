# Question

- lintcode [majority-number-iii](https://www.lintcode.com/problem/majority-number-iii/description)

## 题目描述

### Description

Given an array of integers and a number k, the majority number is the number that occurs `more than 1/k` of the size of the array.

Find it.

There is only one majority number in the array.

Problem Correction

### Example

Given `[3,1,2,3,2,3,3,4,4,4]` and `k=3`, return `3`.

### Challenge

O(n) time and O(k) extra space

## 题解

本来这道题利用hashmap来保存数组中每一个数出现的次数正好，但是这样的话就不满足空间复杂度为$O(k)$。因此对hashmap中的数据进行筛减。分析知：可能的解的个数不会超过k个，通过这个原则对hashmap中的数据筛减从而得到最终的可能结果候选集。然后对候选集中数据再次进行判断得到最终的结果。

**本质上，hashmap中最终保存的值是出现次数前k-1的数，因为这些数才是可能的结果候选数**

### python - solution - one

```python

class Solution:
    """
    @param nums: A list of integers
    @param k: An integer
    @return: The majority number
    """
    def majorityNumber(self, nums, k):
        # 通过分析题，满足题解的值的个数最多为k-1
        
        # 处理异常情况
        if nums is None or len(nums) == 0:
            return -1
        
        # 第一次扫描数组
        hashmap = {}
        for num in nums:
            hashmap[num] = hashmap.get(num, 0) + 1
            if len(hashmap) >= k:
                # 由于最终的结果不可能大于k，所以开始删减元素
                for key in list(hashmap.keys()):
                    hashmap[key] -= 1
                    if hashmap[key] == 0:
                        hashmap.pop(key)
        
        # 判候选集里面的元素是否满足
        for key in hashmap.keys():
            if nums.count(key) > len(nums) / k:
                return key
```

### 复杂度分析

> 时间上，由于使用了nums.count(key)，因此时间复杂度为$O(n*k)$
>
> 空间上，使用的额外空间为$O(k)$

### python - solution - two

```python
class Solution:
    """
    @param nums: A list of integers
    @param k: An integer
    @return: The majority number
    """
    def majorityNumber(self, nums, k):
        # 通过分析题，满足题解的值的个数最多为k-1
        
        # 处理异常情况
        if nums is None or len(nums) == 0:
            return -1
        
        # 第一次扫描数组
        hashmap = {}
        for num in nums:
            hashmap[num] = hashmap.get(num, 0) + 1
            if len(hashmap) >= k:
                # 由于最终的结果不可能大于k，所以开始删减元素
                for key in list(hashmap.keys()):
                    hashmap[key] -= 1
                    if hashmap[key] == 0:
                        hashmap.pop(key)
        
        # 判候选集里面的元素是否满足【还要保证时间复杂度】
        
        # 先将hashmap中的数值置０，并重新计次数
        for key in hashmap.keys():
            hashmap[key] = 0
        for num in nums:
            if num in hashmap:
                hashmap[num] += 1
        
        # 找出最终结果
        result = -1
        max_count = 0
        for key, value in hashmap.items():
            if value > max_count:
                result = key
                max_count = value
        
        return result
```

### 复杂度分析

这个和soulution的区别是减少了时间复杂度【看代码应该能看得懂】

> 时间上，几个for循环是并列的方式，因此最终的时间复杂度为$O(N)$
>
> 空间上，使用的额外空间为$O(K)$

