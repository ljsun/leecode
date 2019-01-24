# Stack - 栈

栈是一种LIFO(Last In First Out)的数据结构，常用的方法有取栈顶元素、弹出栈顶元素、判断栈是否为空.

## 编程实现

### python

```python
stack = []
len(stack)

import collections
stack = collections.deque()
```

### Methods

- len(stack) !=0 判断栈是否为空
- stack[-1] 取栈顶元素，不移除
- pop() 取出栈顶元素，并移除
- append(item) 向栈顶添加元素