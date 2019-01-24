# Question

- lintcode [Count 1 in Binary](https://www.lintcode.com/problem/count-1-in-binary/description)

## 题目描述

### Description

Count how many `1` in binary representation of a 32-bit integer.

Problem Correction

### Example

Given `32`, return `1`

Given `5`, return `2`

Given `1023`, return `9`

### Challenge

If the integer is *n* bits with *m* 1 bits. Can you do it in O(m) time?

## 题解

首先声明，以后遇到这种位运算的题目，尽量使用java去写，因为在python3中，int和long型合并了，所以就不存在溢出的情况。。。就不太好写。。

**其次，一定把原码、反码、补码看看**，，，，**现在还不会**

下面来说这道题

**记住一点**，，，，，**x&(x-1)的含义为去掉二进制数中１的最后一位，无论x是正数还是负数（针对ｊａｖａ和C++而言）**

### java

```java
public class Solution {
    /*
     * @param num: An integer
     * @return: An integer
     */
    public int countOnes(int num) {
        // 又是自己没做出来
        
        // 没啥可说的，一定要牢记这个公式方法
        // x & (x - 1) 就把x中的最低位的１给去除了
        
        int count = 0;
        
        while (num != 0){
            num = num & (num -1);
            count += 1;
        }
            
        return count;
    }
}
```

### 复杂度分析

> 时间上，复杂度依赖与数中１的个数，时间复杂度为$O(m)$
>
> 空间上，额外的复杂度为$O(1)$