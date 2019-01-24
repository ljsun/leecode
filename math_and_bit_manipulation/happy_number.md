# Question

## 题目描述

编写一个算法来判断一个数是不是“快乐数”。

一个“快乐数”定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，然后重复这个过程直到这个数变为 1，也可能是无限循环但始终变不到 1。如果可以变为 1，那么这个数就是快乐数。

**示例: **

```
输入: 19
输出: true
解释: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

## 题解

具体的分析过程见代码注释

### python

```python
class Solution:
    def isHappy(self, n):
        """
        :type n: int
        :rtype: bool
        """
        # 好吧，又是看别人的才有思路，真滴是太蠢了
        
        # 仔细分析呀，一直进行这样的计算，要么最终变成１，要么最终
        # 在一个环形队列里面出不来
        
        # 处理异常情况
        if n == 1:
            return True
        if n < 1:
            return False
        
        def pow_sum(n):
            sum = 0
#             while n > 0:
#                 sum += (n % 10) * (n % 10)
#                 n //= 10
            
#             return sum
            for i in str(n):
                sum += int(i) ** 2
            
            return sum
        
        hash_set = set([])
        n = pow_sum(n)
        hash_set.add(n)
        while n != 1:
            n = pow_sum(n)
            
            if n == 1:
                return True
            
            if n in hash_set:
                return False
            
            if n not in hash_set:
                hash_set.add(n)
        
        return True
            
```

### 复杂度分析

> 时间复杂度根据循环次数而定
>
> 空间复杂度根据环形队列的大小而定