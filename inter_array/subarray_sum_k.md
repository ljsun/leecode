# Question

- GeeksforGeeks:  [Find subarray with given sum - GeeksforGeeks](https://practice.geeksforgeeks.org/problems/subarray-with-given-sum/0)

## 题目描述

Given an unsorted array **A **of size **N** of non-negative integers, find a continuous sub-array which adds to a given number.

**Input:**
The first line of input contains an integer **T** denoting the number of test cases. Then **T** test cases follow. Each test case consists of two lines. The first line of each test case is **N and S**, where N is the size of array and S is the sum. The second line of each test case contains **N** space separated integers denoting the array elements.

**Output:**
For each testcase, in a new line, print the **starting and ending positions**(**1** indexing) of **first such occuring subarray from the left** if sum equals to subarray, else print ** -1**.

**Constraints:**
1 <= T <= 100
1 <= N <= 107
1 <= Ai <= 1010

**Example:**
**Input:**
2
5 12
1 2 3 7 5
10 15
1 2 3 4 5 6 7 8 9 10
**Output:**
2 4
1 5

**Explanation : **
**Testcase1:** sum of elements from 2nd position to 4th position is 12
**Testcase2:** sum of elements from 1st position to 5th position is 15

## 题解

其实这道题和Zero Sum Subarray思路基本相同

### python

```python
def subArraySum(arr, n, sum): 
      
    # Pick a starting  
    # point 
    sum_i = {}
    curr_sum = 0
    for i in range(n):

        curr_sum += arr[i]
        if curr_sum == sum:
            return print(1, i+1)

        if (curr_sum - sum) in sum_i:
            # return [sum_i[curr_sum], i]
            return print(sum_i[curr_sum-sum]+1, i+1)

        sum_i[curr_sum] = i + 1

    return print("-1")


test=int(input())
t=0
while(t<test):
    n,m=input().split()
    n=int(n)
    m=int(m)
    array = list(map(int, input().split()))
    subArraySum(array, n, m)
    t=t+1
```

### 复杂度分析

> 遍历数组的时间复杂度为$O(n)$，假设dict的长度为L，那么查找时间复杂度为$O(logL)$。最终时间复杂度为二者相乘
>
> 空间上又申请了额外的dict空间，因此空间复杂度为$O(n + L)$