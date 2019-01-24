# Question

- Leecode [寻找旋转排序数组中的最小值２](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)

## 题目描述

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 `[0,1,2,4,5,6,7]` ****可能变为 `[4,5,6,7,0,1,2]` )。

请找出其中最小的元素。

注意数组中可能存在重复的元素。

**示例 1：**

```
输入: [1,3,5]
输出: 1
```

**示例 2：**

```
输入: [2,2,2,0,1]
输出: 0
```

## 题解

这道题与寻找旋转排序数组中的最小值这道题思路基本一致，都是寻找旋转排序数组的断点

但是由于重复值的存在，因此需要考虑的情况会更多。

- 当出现nums[mid] == nums[lb]时，无法判断mid所在的局部有序段，因此此时需要lb += 1
- 但是当真正写时，发现判断nums[mid]与nums[lb]的值会错过一些情况，

　　　　因此最终使用判断nums[mid]与nums[ub]，然后nums[mid]==nums[ub]时，ub -= 1

### python

```python
class Solution:
    def findMin(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # 与寻找旋转排序数组中的最小值这道题思路基本一致
        # 都是寻找旋转排序数组的断点
        # 由于重复值的存在，因此要考虑的情况可能比较多
        
        # 处理异常情况
        if not nums:
            return None
        m = len(nums)

        
        # 这种旋转排序数据的题，一般采用二分法时首先要确定mid所在哪个局部有序段。
        
        lb, ub = 0, m-1
        while lb+1 < ub:
            mid = lb + (ub-lb) // 2
            if nums[mid] < nums[ub]:
                ub = mid
            elif nums[mid] > nums[ub]:
                lb = mid
            else:
                # 此时无法判断mid到底是在哪个局部有序段
                ub -= 1 
                
        # 判断出while循环的几种情况
        # 1. 最基本的，lb对应最大元素，ub对应最小元素
        # 2. 特殊的出现全等、或者局部相等造成lb += 1时，最终的结果应该是ub最小
        # 3. 全递增时，ub最大
        
        # if nums[ub] < nums[lb]:
        #     return nums[ub]
        # else:
        #     return nums[0]
        return min(nums[ub], nums[lb])
```

### 复杂度分析

> 时间上，最坏情况下一直在执行ub-=1，此时复杂度为$O(n)$，正常情况下复杂度在$O(logn)$~$O(n)$
>
> 空间上，使用的额外空间为$O(1)$