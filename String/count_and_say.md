# Question

- leetcode: [count and say](https://leetcode-cn.com/problems/count-and-say/)

## 问题描述

报数序列是一个整数序列，按照其中的整数的顺序进行报数，得到下一个数。其前五项如下：

1.     1
2.     11
3.     21
4.     1211
5.     111221

`1` 被读作  `"one 1"`  (`"一个一"`) , 即 `11`。
`11` 被读作 `"two 1s"` (`"两个一"`）, 即 `21`。
`21` 被读作 `"one 2"`,  "`one 1"` （`"一个二"` ,  `"一个一"`) , 即 `1211`。

给定一个正整数 *n*（1 ≤ *n* ≤ 30），输出报数序列的第 *n* 项。

注意：整数顺序将表示为一个字符串。

**示例 1:**

输入: 1
输出: "1"

**示例 2:**

输入: 4
输出: "1211"

## 题解１

首先这道题最重要的是应该看清题的意思，到底是如何进行计数的。很明显，第n项的报数值需要通过第n-1项的报数值来计算。这就比较符合递归的思路了。。因此首先可以想到这道题可以利用递归的思想来做。

### python

```python
class Solution:
    def countAndSay(self, n):
        """
        :type n: int
        :rtype: str
        """
        # 先想到用递归做一下
        # 先计算出n-1对应的计数
        if n == 1:
            return "1"
        previous_report = self.countAndSay(n-1)
        # 根据前一个计数来计算当前计数
        current_report = ''
        i = 0
        while i<len(previous_report):
            count = 1
            while (i+count)<len(previous_report) and previous_report[i]==previous_report[i+count]:
                count += 1
            current_report += str(count)
            current_report += previous_report[i]
            i += count
        return current_report
```

### 复杂度分析

> 首先递归需要计算n次。每一次计算时虽然是两个嵌套while循环，但其实只遍历了一次上一次的结果计数。因此总的时间复杂度是总的递归次数$*$每一次递归的遍历次数
>
> 从空间上看，由于需要空间来存储当前和上一次报数值，因此空间复杂度为$O(n+m)$

## 题解２

既然能够使用递归来解决这道题，那么也能够使用迭代来计算这道题

### python

```python
class Solution:
    def countAndSay(self, n):
        """
        :type n: int
        :rtype: str
        """
        # 既然能够用递归写出来，那么一般也能够用迭代写出来
        # 但是要求n对应的报数，还是要先求n-1对应的报数
        # 因此迭代时可以先求第一个报数，再求第二个报数。。。以此类推
        if n == 1:
            return "1"
        previous_report = "1"
        current_report = ""
        for i in range(2, n+1):
            # 计算当前i对应的report
            j = 0       
            while j<len(previous_report):
                count = 1
                while (j+count)<len(previous_report) and previous_report[j]==previous_report[j+count]:
                    count += 1
                current_report += str(count)
                current_report += previous_report[j]
                j += count
            
            previous_report = current_report
            current_report = ""
        
        return previous_report
```

### 复杂度分析

> 从时间上看，虽然嵌套了３个循环，但是两个while循环只遍历一次报数值。因此总的时间复杂度为for循环次数*每一次for循环对应的while循环遍历次数。
>
> 空间上，由于需要空间来存储当前和上一次报数值，因此空间复杂度为$O(n+m)$