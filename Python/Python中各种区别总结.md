### Python 中数组和列表的区别
Python 中的数组和列表具有相同的存储数据方式。但是，数组只能包含单个数据类型元素，而列表可以包含任何数据类型元素。
- 列表list中的元素的数据类型可以不一样；数组array里的元素的数据类型必须一样
- 列表list不可以进行数学四则运算；数组array可以进行数学四则运算
- 相对于array，列表会使用更多的存储空间

### Python 中 append() 和 extend() 的区别
- append() 方法用于在列表末尾添加新的对象
- extend() 函数用于在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）
```
a = [1, 2]
b = [1, 2]
a.append(3)
print(a)
输出：[1, 2, 3]

b.extend([3])
print(b)
输出：[1, 2, 3]

b.extend(3)
print(b)
TypeError: 'int' object is not iterable
```
