深拷贝和浅拷贝都是对象的拷贝，都会生成一个看起来相同的对象，本质区别是拷贝出来的对象的**地址**是否和原对象一样，**即是地址的复制还是值的复制**。  
1. 由于 Python 内部引用计数的特性，对于不可变对象，浅拷贝和深拷贝的作用是一致的，相当于复制了一份副本，原对象内部的不可变对象的改变，不会影响到复制对象。
2. 浅拷贝。其实是拷贝了原始元素的引用（内存地址），所以当拷贝可变对象时，原对象内可变对象对应元素的改变，会在复制对象的对应元素上有所体现。
3. 深拷贝。在遇到可变对象时，又在内部新建了一个副本。新对象跟原对象不共享内存，不管其内部元素如何变化，都不会影响到原来副本的可变对象。

###### 图片举例
1、b = a: 赋值引用，a 和 b 都指向同一个对象。  
![image](https://note.youdao.com/yws/public/resource/482136d1adccf86f42705a8cd4c87cf6/xmlnote/68FE1239A9DE4AD59E3C167F40BDF194/8996)  
2、b = a.copy(): 浅拷贝, a 和 b 是一个独立的对象，但他们的子对象还是指向统一对象（是引用）。  
![image](https://note.youdao.com/yws/public/resource/482136d1adccf86f42705a8cd4c87cf6/xmlnote/B8225551F1CD47CF9C50DB0DB048536D/8998)  
3、b = copy.deepcopy(a): 深拷贝, a 和 b 完全拷贝了父对象及其子对象，两者是完全独立的。  
![image](https://note.youdao.com/yws/public/resource/482136d1adccf86f42705a8cd4c87cf6/xmlnote/0DD93C8C1D724487AB83DE7C91B080A7/8997)


###### 代码举例

```
import copy

a = [1, 2, 3, 4, ['a', 'b']] #原始对象

b = a                       #赋值，传对象的引用
c = copy.copy(a)            #对象拷贝，浅拷贝
d = copy.deepcopy(a)        #对象拷贝，深拷贝
 
a.append(5)                 #修改对象a
a[4].append('c')            #修改对象a中的['a', 'b']数组对象
 
print( 'a = ', a )
print( 'b = ', b )
print( 'c = ', c )
print( 'd = ', d )
```
执行输出结果如下：

```
a =  [1, 2, 3, 4, ['a', 'b', 'c'], 5]
b =  [1, 2, 3, 4, ['a', 'b', 'c'], 5]
c =  [1, 2, 3, 4, ['a', 'b', 'c']]
d =  [1, 2, 3, 4, ['a', 'b']]
```
