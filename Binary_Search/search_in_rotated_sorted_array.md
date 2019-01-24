# Question

- Leecode [搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)

> 插一个，对于有序的二分搜索来说，如果lb=-1, ub=m，那么lb和ub所在处的值是没有被判断的，而lb和ub之间的值都是被判断的了。即如果
>
> ```
> while lb+1<ub:
> 	mid = lb+(ub-lb)//2
> 	if nums[mid] == target:
> 		return ...
> 	elif:
> 	  ...
> 	else:
> 	  ...
> 如果程序执行到了这一步，说明lb与ub之间确实没有等于target的值。
> ```
>
> 

## 题目描述

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 `[0,1,2,4,5,6,7]` 可能变为 `[4,5,6,7,0,1,2]` )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 `-1` 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 *O*(log *n*) 级别。

**示例 1:**

```
输入: nums = [4,5,6,7,0,1,2], target = 0
输出: 4

```

**示例 2:**

```
输入: nums = [4,5,6,7,0,1,2], target = 3
输出: -1
```

## 题解1

由于这道题要求的时间复杂度为$O(log n)$级别。因此使用二分搜索就成为了一个主要的思路，那么怎么使用二分搜索呢？其实通过分析看到旋转后的数组仍然是个部分有序的数组。我们可以先找到target所在的部分有序段，然后再二分搜索一步步向下求。

### python

```python
class Solution:
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        # 思路１：找到旋转点，还原数组，然后再进行二分搜索
        #         这种复杂度就做不到O(logn)级别
        # 思路２：直接进行二分搜索
        #         画个图更清晰，旋转后的数组其实是两段有序的数组
        
        # 处理异常情况
        m = len(nums)
        if m < 1:
            return -1
        
        # lb, ub本身的位置是判断不到的，但是之间的都能判断的到
        lb, ub = 0, m-1
        while lb+1 < ub:
            mid = lb + (ub-lb) // 2
            # 判断mid元素到底在哪一段
            if nums[mid] == target:
                return mid
            elif nums[mid] > nums[lb]:
                if nums[mid] > target and nums[lb] < target:
                    ub = mid
                else:
                    lb = mid
            else:
                if nums[mid] < target and nums[ub] > target:
                    lb = mid
                else:
                    ub = mid
        
        if nums[0] == target:
            return 0
        elif nums[m-1] == target:
            return m-1
        else:
            return -1
                    
```

### 复杂度分析

> 时间上，本质上还是采用二分搜索，因此时间复杂度仍然为$O(logn)$
>
> 空间上，使用的额外空间为$O(1)$

## 题解２

仔细看可以发现旋转数组有一个中断点，中断点的左右两侧都是局部有序的。我们可以先利用二分搜索找到中断点，然后确定target可能在的局部有序段，然后再进行二分搜索。

这个代码写的还是有点乱。。。考虑了很多特殊情况，代码不能够直接判断特殊情况。

```python
class Solution:
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        # 思路１：找到旋转点，还原数组，然后再进行二分搜索
        #         这种复杂度就做不到O(logn)级别
        # 思路２：直接进行二分搜索
        #         画个图更清晰，旋转后的数组其实是两段有序的数组
        
        # 处理异常情况
        m = len(nums)
        if m < 1:
            return -1
        
        # lb, ub本身的位置是判断不到的，但是之间的都能判断的到
        # 最终出while循环的条件一定是lb+1=ub
        # 根据思路１，先二分搜索找到旋转点
        lb, ub = 0, m-1
        while lb+1 < ub:
            mid = lb + (ub-lb) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] > nums[lb]:
                lb = mid
            else:
                ub = mid
        
        # 三种特殊的情况，如１、　２
        #                   １、　２、　３
        #                   ２、　１
        if m == 2:
            index = lb if nums[lb] > nums[ub] else ub
        else:
            index = ub if nums[lb] < nums[ub] else lb
            
        # 根据找到的断点再次进行二分查找
        if target >= nums[0]:
            lb, ub = -1, index+1
        else:
            lb, ub = index, m
        
        while lb+1<ub:
            mid = lb+(ub-lb)//2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                lb = mid
            else:
                ub = mid
        
        return -1
```

### 复杂度分析

> 时间上，第一次二分搜索时间复杂度为$O(logn)$，第二次搜索时时间复杂度小于$O(logn)$。因此总的时间复杂度级别仍然是$O(logn)$级别。
>
> 空间上，使用的额外空间为$O(1)$