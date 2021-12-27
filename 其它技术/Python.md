#### Python语言与其它语言的不同点

------

**布尔值为False和True**

**python语法没有自增与自减，只有使用+=或者-=**



#### 逻辑使用技巧

------

判断字符区间时，可以直接使用if s > ="a" and s <= "z"

判断数字区间时，可以直接使用if n > ="0" and s <= "9"

"  0000000000012345678"



#### 字符串

------

**1.字母处理：**

```
.upper()    # 全部大写
.lower()    # 全部小写
.swapcase()    # 大小写互换
.capitalize()    # 首字母大写，其余小写
.title()    # 首字母大写
```

**2.格式化相关**

```
.ljust(width)     # 获取固定长度，左对齐，右边不够用空格补齐
.rjust(width)     # 获取固定长度，右对齐，左边不够用空格补齐
.center(width)  # 获取固定长度，中间对齐，两边不够用空格补齐
.zfill(width)      # 获取固定长度，右对齐，左边不足用0补齐
```

**3.字符串搜索相关**

```
.find()    # 搜索指定字符串，没有返回-1，有返回索引，可以指定查找范围，如.find("a", 2, 4),代表查找索引[2:4)的范围
.index()    # 同上，找到返回索引，但是找不到会报错，可以指定查找范围，如.find("a", 2, 4),代表查找索引[2:4)的范围
.rfind()    # 从右边开始查找，返回索引，可以指定查找范围，如.find("a", 2, 4),代表查找索引[2:4)的范围
.count()    # 统计指定的字符串出现的次数，可以指定查找范围，如.find("a", 2, 4),代表查找索引[2:4)的范围
 
# 上面所有方法都可以用index代替，不同的是使用index查找不到会抛异常，而find返回-1
```

**4.字符串替换**

```python
.replace('old','new')    # 替换old为new，返回替换后的字符串，不修改原字符串
.replace('old','new',次数)    # 替换指定次数的old为new

s='hello world'
print(s.replace('world','python'))
print(s.replace('l','p',2))
print(s.replace('l','p',5))

执行结果：
hello python
heppo world
heppo worpd
```

**5.字符串去空格及去指定字符**

```
.strip()    # 去两边空格
.lstrip()    # 去左边空格
.rstrip()    # 去右边空格

.split()    # 默认按空格分隔
.split('指定字符')    # 按指定字符分割字符串为数组
```

**6.字符串判断相关**

```
.startswith('start')    # 是否以start开头
.endswith('end')    # 是否以end结尾
.isalnum()    # 是否全为字母或数字
.isalpha()    # 是否全字母
.isdigit()    # 是否全数字
.islower()    # 是否全小写
.isupper()    # 是否全大写
.istitle()    # 判断首字母是否为大写
.isspace()    # 判断字符是否为空格

# 补充
bin()    # 十进制数转八进制
hex()    # 十进制数转十六进制
range()    # 函数：可以生成一个整数序列
type()    # 查看数据类型
len()    # 计算字符串长度
format()    # 格式化字符串，类似%s，传递值能多不能少
```

**7.其它**

```
ord：返回Unicode字符对应的整数
print(ord('a'))

chr：返回整数所对应的Unicode字符
print(chr(97))
```



#### 列表（List）

------

**1.创建列表。**只要把逗号分隔的不同的数据项使用方括号括起来即可

```python
List = ['wade','james','bosh','haslem']
```

与字符串的索引一样，列表索引从0开始。列表可以进行截取、组合等

**2.添加新的元素**

```python
List.append('allen') #方式一：向list结尾添加 参数object
>>> a=[1,2,3,4]
>>> a.append(5)
>>> print(a)
[1, 2, 3, 4, 5]

List.insert(4,'lewis') #方式二：插入一个元素 参数一：index位置 参数二：object
>>> a=[1,2,4]
>>> a.insert(2,3)
>>> print(a)
[1, 2, 3, 4]

List.extend(tableList)  #方式三：扩展列表，参数：iterable参数
>>> a=[1,2,3]
>>> b=[4,5,6]
>>> a.extend(b)
>>> print(a)
[1, 2, 3, 4, 5, 6]
```

**3.遍历列表**

```python
for i in List:
	print i,
```

**4.访问列表中的值**
使用下标索引来访问列表中的值，同样你也可以使用方括号的形式截取字符，如下所示：

```python
>>> List = [1, 2, 3, 4, 5, 6, 7 ]
>>> print(List[3])
4
```

**5.从list删除元素**

```python
List.remove()   #删除方式一：参数object 如有重复元素，只会删除最靠前的
>>> a=[1,2,3]
>>> a.remove(2)
>>> print(a)
[1, 3]

List.pop()   #删除方式二：pop 可选参数index删除指定位置的元素 默认为最后一个元素
>>> a=[1, 2, 3, 4, 5, 6]
>>> a.pop()
6
>>> print(a)
[1, 2, 3, 4, 5]
>>> a.pop(1)
>>> print(a)
[1, 3, 4, 5]

del List #删除方式三：可以删除整个列表或指定元素或者列表切片，list删除后无法访问。
>>> a=[1, 2, 3, 4, 5, 6]
>>> del a[5]
>>> print(a)
[1, 2, 3, 4, 5]
>>> del a
>>> print(a)
Traceback (most recent call last):
  File "<pyshell#93>", line 1, in <module>
    print(a)
```

**6.排序和反转代码**

```python
List.reverse()
>>> a=[1, 2, 3, 4, 5, 6]
>>> a.reverse()
>>> print(a)
[6, 5, 4, 3, 2, 1]

>>> a=[1, 2, 3, 4, 5, 6]
>>> print(a[::-1])
[6, 5, 4, 3, 2, 1]

List.sort() #sort有三个默认参数 cmp=None,key=None,reverse=False 因此可以制定排序参数
>>> a=[2,4,6,7,3,1,5]
>>> a.sort()
>>> print(a)
[1, 2, 3, 4, 5, 6, 7]
#python3X中，不能将数字和字符一起排序，会出现此报错
>>> a=[2,4,6,7,3,1,5,'a']
>>> a.sort()
Traceback (most recent call last):
  File "<pyshell#104>", line 1, in <module>
    a.sort()
TypeError: unorderable types: str() < int()
        
List.sort(reverse = True) #sort反序排列
        
>>>sorted([5, 2, 3, 1, 4])
[1, 2, 3, 4, 5]                      # 默认为升序

>>>sorted([5, 2, 3, 1, 4], reverse = True)		 # 降序排列
[1, 2, 3, 4, 5]                     
```

**7.Python列表截取**

```python
Python的列表截取与字符串操作类型相同，如下所示：
L = ['spam', 'Spam', 'SPAM!']
操作：
Python 表达式 结果 描述
L[2] 'SPAM!' 读取列表中第三个元素
L[-2] 'Spam' 读取列表中倒数第二个元素
L[1:] ['Spam', 'SPAM!'] 从第二个元素开始截取列表
```

**8.*Python*列表操作的函数和方法**

```
列表操作包含以下函数:
1、cmp(list1, list2)：比较两个列表的元素 (python3已丢弃)
2、len(list)：列表元素个数 
3、max(list)：返回列表元素最大值 
4、min(list)：返回列表元素最小值 
5、list(seq)：将元组转换为列表 
6、sum([1,2,3,4])    # 传入可迭代对象、元素类型必须是数值型
```

```
列表操作常用操作包含以下方法:
1、list.append(obj)：在列表末尾添加新的对象
2、list.count(obj)：统计某个元素在列表中出现的次数
3、list.extend(seq)：在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）
4、list.index(obj)：从列表中找出某个值第一个匹配项的索引位置
5、list.insert(index, obj)：将对象插入列表
6、list.pop(obj=list[-1])：移除列表中的一个元素（默认最后一个元素），并且返回该元素的值
7、list.remove(obj)：移除列表中某个值的第一个匹配项
8、list.reverse()：反向列表中元素
9、list.sort([func])：对原列表进行排序
```



#### 字典

------

**字典特性：**

1）不允许同一个键出现两次。创建时如果同一个键被赋值两次，后一个值会被记住，如下实例：

```
dict = {'Name': 'Runoob', 'Age': 7, 'Name': '小菜鸟'}
print (dict)

输出：
{'Name': '小菜鸟', 'Age': 7}
```

2）键必须不可变，所以可以用数字，字符串或元组充当，而用列表就不行



**1.创建字典**

```python
dict1 = { 'abc': 456 }
dict2 = { 'abc': 123, 98.6: 37 }
```

**2.访问字典里的值**

```python
dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}
 
print ("dict['Name']: ", dict['Name'])
print ("dict['Age']: ", dict['Age'])
```

**3.修改和添加字典元素**

```python
dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}
 
dict['Age'] = 8               # 更新 Age
dict['School'] = "菜鸟教程"  	# 添加信息
```

**4.删除字典元素**

```python
dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}
 
del dict['Name'] # 删除键 'Name'
dict.clear()     # 清空字典
del dict         # 删除字典
```

**5.排序**

```python
#sorted
d={'a':1,'c':3,'b':2}    # 首先建一个字典d
#d.items()返回的是： dict_items([('a', 1), ('c', 3), ('b', 2)]) 
d_order=sorted(d.items(),key=lambda x:x[1],reverse=False)  			# 按字典集合中，每一个元组的第二个元素排列。     
print(d_order)     # 得到:  [('a', 1), ('b', 2), ('c', 3)]

#sort()
#Python中的字典是无序类型，没有自己的排序方法。但可以用列表的.sort()方法来进行排序。我们首先要把字典转换为列表，再进行排序。
d={'a':1,'c':3,'b':2}    # 首先建一个字典d
L=list(d.items())       # 得到列表: L=[('a', 1), ('c', 3), ('b', 2)]
L.sort(key=lambda x:x[1],reverse=False)  # 按列表中，每一个元组的第二个元素从小到大排序。
print(L)      # 得到:  [('a', 1), ('b', 2), ('c', 3)]
```

**6.其它函数方法**

```python
len(dict)
计算字典元素个数，即键的总数。

str(dict)
输出字典，可以打印的字符串表示。

type(variable)
返回输入的变量类型，如果变量是字典就返回字典类型。

radiansdict.clear()
删除字典内所有元素

radiansdict.get(key, default=None)
返回指定键的值，如果键不在字典中返回 default 设置的默认值

key in dict
如果键在字典dict里返回true，否则返回false，与dict[key]功能类似

radiansdict.items()
以列表返回一个视图对象

radiansdict.keys()
返回一个视图对象

radiansdict.values()
返回一个视图对象

radiansdict.setdefault(key, default=None)
如果key不存在于字典中，将会添加键并将值设为default;如何key已经存在，则不进行操作

radiansdict.update(dict2)
把字典dict2的键/值对添加到dict里，类型于List中的extend（如果这个新的dict对象中的key已经在当前的字典对象中存在了，则会覆盖掉key对应的value）

pop(key[,default])
删除字典给定键 key 所对应的值，返回值为被删除的值。key值必须给出。 否则，返回default值。

popitem()
随机返回一对键值并删除字典中的最后一对键和值。
```

