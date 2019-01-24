# Question

- [lintcode](https://www.lintcode.com/problem/space-replacement/description)

## 题目描述

Write a method to replace all spaces in a string with `%20`. The string is given in a characters array, you can assume it has enough space for replacement and you are given the true length of the string.

You code should also return the new length of the string after replacement.

### Example

Given `"Mr John Smith"`, length = `13`.

The string after replacement should be `"Mr%20John%20Smith"`, you need to change the string in-place and return the new length `17`.

### Challenge

Do it in-place.

## 题解

其实这道题如果不要求就地替换字符串的话，就很简单。但它偏偏就是要就地替换字符串。那就意味不要再开辟新的存储空间。既然不让开辟新的存储空间，要么就是让程序更“聪明”一点，要么就是以牺牲时间复杂度为代价

另外这道题如果用python写的好像更麻烦一点，因为python的字符串好像直接将“20%”替换成了空格

### java

```java
public class Solution {
    /*
     * @param string: An array of Char
     * @param length: The true length of the string
     * @return: The true length of new string
     */
    public int replaceBlank(char[] string, int length) {
        // 首先这道题的难点在于希望就地替换字符串
        // 不要再开辟新存储空间，那么就是要以牺牲
        // 时间复杂度为代价
        int new_length = length;
        for (int i=0; i<length; i++){
            if (string[i] == ' '){
                new_length += 2;
            }
        }
        // 然后根据new_length来就地修改string
        int right = new_length - 1;
        for (int i=length-1; i>=0; i--){
            if (string[i] == ' '){
                string[right--] = '0';
                string[right--] = '2';
                string[right--] = '%';
            }
            else{
                string[right--] = string[i];
            }
        }
        return new_length;
    }
}
```



### 复杂度分析

> 首先遍历了两次数组，因此时间复杂度为$O(n+n)$
>
> 在空间上使用了`right`和`new_length`，因此总的空间复杂度为$O(n + 1 + 1)$