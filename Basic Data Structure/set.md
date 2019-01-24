# Set

Set是一种保存不重复元素的数据结构。常被用作测试归属性，因此其查找的性能十分重要。

## 编程实现

### python

`set`是python自带的基本数据结构，有多种初始化方式。可以认为set是只有key的dict.

```python
s = Set()
s1 = {1, 2, 3}
s.add('shaunwei')
'shaun' in s # return false
s.remove('shaunwei')
```

