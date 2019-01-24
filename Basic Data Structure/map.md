# Map - 哈希表 - hashmap

map在本质上个人认为就是字典或者是哈希表

## python

```python
hash_map = {}
hash_map['shaun'] = 98
has_map['wei'] = 99
point = hash_map.pop('shaun')
keys = hash_map.keys() # return key list
for key, values in hash_map.items():
	# do something with k, v
    pass
```

## Java

Java的实现中Map是一种将对象与对象相关联的设计。常见的有HashMap和TreeMap，HashMap被用用来快速访问，而TreeMap则保证键始终有序。Map可以返回键的Set，值的Collection，键值对的Set

```java
Map<String, Integer> map = new HashMap<String, Integer>();
map.put('bill', 98);
map.put('ryan', 99)
boolean exist = map.containKey('ryan');
int point = map.get('bill');
int point = map.remove('bill');
Set<String> set = map.keySet();
// iterate map
for (map.Entry<String, Integet> entry : map.entrySet()) {
  String key = entry.getKey();
  String value = entry.geyValue();
  // do something
}
```

