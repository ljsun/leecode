# Question

## 问题描述

给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。

**示例:**

```
输入: ["eat", "tea", "tan", "ate", "nat", "bat"],
输出:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**说明：**

- 所有输入均为小写字母。
- 不考虑答案输出的顺序

## 题解１－双重for循环

首先能够想到的就是写两个for循环，然后将同一组的字母异位词放在一起。顶多能够想到的小trick就是对于已经添加进组的字母异位词不再进行判断。

### python

```python
class Solution:
  def groupAnagrams(self, strs):
      """
      :type strs: List[str]
      :rtype: List[List[str]]
      """
      groupanagrams = []
      # 再增加一个list来记录index
      extract_index = []
      for i in range(len(strs)):
          if i in extract_index:
              continue
          groupanagram = [strs[i]]
          extract_index.append(i)
          for j in range(i+1, len(strs)):
              if j in extract_index:
                  continue
              if sorted(strs[i]) == sorted(strs[j]):
                  groupanagram.append(strs[j])
                  extract_index.append(j)
          groupanagrams.append(groupanagram)

      return groupanagrams
```
### 复杂度分析

假设字符串长度为L，对字符串排序的时间为$O(LlogL)$，判断字符串是否相同需要的时间为$O(2L)$，双重for的时间为$\frac{1}{2}O(N^2)$。总的时间复杂度就是将他们相乘

空间复杂度，由于使用了额外的extract_index，因此空间复杂度为$O(2N)$

## 题解２－hashmap

hashmap确实是个好东西。首先对于同一个组的字母异位词，他们都有一个共同的性质，就是将他们排序后发现这是一个东西。因此同一组的排序后得到的就可以作为key，value就是个list，里面是同一组的字符串。

**注意下面代码的简洁性**

### python 

```python
class Solution:
  def groupAnagrams(self, strs):
      """
      :type strs: List[str]
      :rtype: List[List[str]]
      """
      groupanagrams = collections.defaultdict(list)
      for s in strs:
          groupanagrams[tuple(sorted(s))].append(s)

      return list(groupanagrams.values())
```
### 复杂度分析

假设字符串长度为L，排序字符串需要的时间复杂度为$O(LlogL)​$，遍历数组的时间复杂度为$O(N)​$。因此总的时间复杂度为$O(NLlogL)​$

存储所有字符串需要的空间为$O(NL)$，由于需要个字典存储排序后的字典，相当于将字符串又存了一次，因此总的空间复杂度为$O(2NL)$