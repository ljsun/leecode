# Question

- leecode: [Two Sum](https://leetcode-cn.com/problems/two-sum/)

## 题目描述

给定一个整数数组和一个目标值，找出数组中和为目标值的**两个**数。

你可以假设每个输入只对应一种答案，且同样的元素不能被重复利用。

**示例:**

```python
nums = [2, 7, 11, 15], target = 9
nums[0] + nums[1] = 2 + 7 = 9
返回[0, 1]
```

## 题解１－暴力搜索

找两数之和是否为`target`，最先想到的思路就是写一个双循环遍历数组中的每一个元素。但是在这种情况下，时间复杂度显然为$O(n^2)$，显然并不符合题目的要求，而且自己想想就感觉太笨了。但是还是写了并提交了，结果显而易见，超时了！代码如下：class Solution:

```python
def twoSum(self, nums, target):
    """
    :type nums: List[int]
    :type target: int
    :rtype: List[int]
    """
    start_index = -1
    end_index = -1
    for i in range(len(nums)):
        for j in range(i+1, len(nums)):
            if (nums[i] + nums[j]) == target:
                return [i, j]
```
## 题解２－哈希表

双循环遍历的时间复杂度为$O(n^2)$，而只遍历一次例如只查找数组中的某一个元素的时间复杂度为$O(n)$，此时就想要是把问题转化为为只遍历一次就爽了，直接就降低了时间复杂度。那么应该怎么做呢？

我们先来看看两数之和为`target`的判断条件是－－$x_i + x_j = target$，可进一步转化为$x_i = target - x_j$，其中$i$和$j$是数组中的下标。一段神奇的数学推理就将找两数之和转化为了找一个数是否在数组中！

基本思路有了，现在就来看看怎么实现。很显然我们降低了时间复杂度，就必然增加空间复杂度（或者是存储空间）作为代价，显然我们需要额外的空间来（也就是哈希表）来保存已经处理过的$x_j$(**注意这里并不能先初始化哈希表，否则无法排除两个相同的元素相加为target的情况**)，如果不满足等式，就向后遍历，并把之前的处理的元素加入哈希表中，如果`target`减去当前索引后的值在哈希表中找到了，就将当前索引和哈希表中对应的索引返回

```python
def twoSum(self, nums, target):
    """
    :type nums: List[int]
    :type target: int
    :rtype: List[int]
    """
    hashset = {}
    for i, value in enumerate(nums):
        if (target - value) in hashset:
            return [hashset[target-value], i]
        else:
            # 将当前值添加进hashset
            if value not in hashset:
                hashset[value] = i
    return [-1, -1]
```
- 时间复杂度$O(n)$
- 空间复杂度$O(n)$

## 题解３－排序后使用两个索引

同样遵循着降低时间复杂度就要增加空间复杂度（或者是存储空间）的原则。另一个思路则是先对数组排序，然后使用两个指针索引分别指向首尾元素，逐步向中间靠拢，直至找到满足条件的索引为止。

```python
def twoSum(self, nums, target):
    """
    :type nums: List[int]
    :type target: int
    :rtype: List[int]
    """
    # 先对nums进行排序，并记录原有的index
    new_nums = []
    for index, value in enumerate(nums):
        new_nums.append([value, index])
    new_nums = sorted(new_nums, key=lambda x: x[0])
    start_index = 0
    end_index = len(new_nums)-1
    while start_index < end_index:
        if (new_nums[start_index][0] + new_nums[end_index][0]) > target:
            end_index -= 1
        elif (new_nums[start_index][0] + new_nums[end_index][0]) == target:
            return [min(new_nums[start_index][1], new_nums[end_index][1]), max(new_nums[start_index][1],                                        new_nums[end_index][1])]
        else:
            start_index += 1
        
    return [-1, -1]
```
### 复杂度分析

首先遍历一次原数组得到new_nums的时间复杂度为$O(n)$，空间复杂度也为$O(n)$。然后python标准库的排序方法时间复杂度为$O(n)$，然后使用两个指针索引遍历的时间复杂度为$O(n)$.