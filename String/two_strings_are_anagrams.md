# Question

给定两个字符串 *s* 和 *t* ，编写一个函数来判断 *t* 是否是 *s* 的一个字母异位词。

**示例 1:**

```
输入: s = "anagram", t = "nagaram"
输出: true

```

**示例 2:**

```
输入: s = "rat", t = "car"
输出: false
```

**说明:**
你可以假设字符串只包含小写字母。

**进阶:**
如果输入字符串包含 unicode 字符怎么办？你能否调整你的解法来应对这种情况？

## 题解１－Hashmap

首先这个题的本质就是判断两个字符串是否包含相同的的字符。那么最先想到的就是分别统计两个字符串的字符词频，然后进行比较。然而就这样一个简单的思路也有不少的学问。对于python来说，如何快速的统计词频，最有效的方法是使用内部的collections。对于java来说，没有对应功能的collections类，就要靠自己想办法了。

### java

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        // 先判断是否为空或者长度是否相同
        if (s == null || t == null)  return false;
        if (s.length() != t.length()) return false;

        // 这里是256的原因是因为ascii和伪asicc字符（unicode)对应的编号为0~255
        final int CHAR_NUM = 256;
        int[] letterCounter = new int[CHAR_NUM];
        for (int i=0; i<s.length();i++){
            letterCounter[s.charAt(i)]++;
            letterCounter[t.charAt(i)]--;
        }
        for (int i=0; i<CHAR_NUM;i++){
            if (letterCounter[i] != 0)
                return false;
        }
        return true;
    }
}
```
### python

```python
class Solution:
  def isAnagram(self, s, t):
      """
      :type s: str
      :type t: str
      :rtype: bool
      """
      # 最先想到的，统计词频进行比较
      return collections.Counter(s) == collections.Counter(t)
```
### 复杂度分析

> - java: 由于要遍历字符串，因此时间复杂度最坏为$O(n+256)$，而且使用和额外的数组，因此空间复杂度为$O(n+n+256)$
> - python: 时间复杂度为内部统计时间＋比较时间。对于空间复杂度来说，使用了额外的空间来存储字符统计结果

## 题解２－排序字符串

通过理解题目的本质，另一种解法则是首先对字符串进行排序，然后逐位比较。

### python

```python
class Solution:
  def isAnagram(self, s, t):
      """
      :type s: str
      :type t: str
      :rtype: bool
      """
      # 其次还可以对字符串进行排序，然后逐位进行比较
      return sorted(s) == sorted(t)
```
### 复杂度分析

> - 逐位比较最糟糕的时间复杂度为$O(n)$，因此总的时间复杂度为排序的时间复杂度＋逐位比较的时间复杂度
> - 由于使用了额外的空间来存储排序后的字符，因此最终空间复杂度为$O(n + n + n + n)$，还是$O(n)$