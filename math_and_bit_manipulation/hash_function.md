# Question

- lintcode [hash function](https://www.lintcode.com/problem/hash-function/description)

## 题目描述

### Description

In data structure Hash, hash function is used to convert a string(or any other type) into an integer smaller than hash size and bigger or equal to zero. The objective of designing a hash function is to "hash" the key as unreasonable as possible. A good hash function can avoid collision as less as possible. A widely used hash function algorithm is using a magic number 33, consider any string as a 33 based big integer like follow:

hashcode("abcd") = (ascii(a) * $33^3$ + ascii(b) * $33^2$ + ascii(c) *33 + ascii(d)) % HASH_SIZE 

                              = (97* $33^3$ + 98 * $33^2$ + 99 * 33 +100) % HASH_SIZE

                              = 3595978 % HASH_SIZE

here HASH_SIZE is the capacity of the hash table (you can assume a hash table is like an array with index 0 ~ HASH_SIZE-1).

Given a string as a key and the size of hash table, return the hash value of this key.f

**对于这个问题你不需要自己设计hash算法，你只需要实现上述描述的hash算法即可。

Problem Correction

### Clarification

For this problem, you are not necessary to design your own hash algorithm or consider any collision issue, you just need to implement the algorithm as described.

### Example

For key="abcd" and size=100, return 78

## 题解1

首先想到的笨思路就是一点一点递推计算（我这种笨人也只能想到这了）

### python

```python
class Solution:
    """
    @param key: A string you should hash
    @param HASH_SIZE: An integer
    @return: An integer
    """
    def hashCode(self, key, HASH_SIZE):
        
        if key is None or len(key) == 0:
            return -1
            
        length = len(key)
        
        total_sum = 0
        for i, char in enumerate(key):
            total_sum += ord(char) * (33 ** (length-i-1))
            
        mod = total_sum % HASH_SIZE
        
        return mod
```

## 题解２

这种求模的首先要牢记两个公式

(a * b) % p  = ((a % p) * (b % p)) % p

(a + b) % p =  ((a % p) + (b % p)) % p

而且hashcode(abc)  = (a×$33^2$+b×33+c)%M = (33(33×a+b)+c)%M = (33(33(33×0+a)+b)+c)%M

将hashcode(abc)按照上面两个公式展开，就可以用迭代的方式展开

### python

```python
class Solution:
    """
    @param key: A string you should hash
    @param HASH_SIZE: An integer
    @return: An integer
    """
    def hashCode(self, key, HASH_SIZE):
        # 就先按照最基本的思路去写
        
        # 先处理异常情况
        
        if key is None or len(key) == 0:
            return -1
            
        length = len(key)
        
        # 根据两个重要的公式求解，见题解
        
        hash_sum = 0
        
        for char in key:
            hash_sum = (33 % HASH_SIZE) * hash_sum + ord(char) % HASH_SIZE
            
            hash_sum %= HASH_SIZE
            
        
        return hash_sum
```

### 复杂度分析

> 时间上，循环ｎ次，复杂度为$O(n)$
>
> 空间上，额外空间为$O(1)$