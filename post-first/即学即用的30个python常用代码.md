---
title: 即学即用的30个python常用代码
date: 2019-09-24 11:22:10
thumbnail: https://i.loli.net/2019/09/24/nIZpoPwY9zguXiv.png
tags: python常用代码
categories: Python
---
## 1.检查重复元素

下面的方法可以检查给定列表中是否有重复的元素。它使用了 set() 属性，该属性将会从列表中删除重复的元素。


```python
def all_unique(lst):    
    return len(lst) == len(set(lst))  
      
x = [1,1,2,2,3,2,3,4,5,6]    
y = [1,2,3,4,5]    
all_unique(x) # False    
all_unique(y) # True
```

<!--more-->

## 2.变位词

检测两个字符串是否互为变位词（即互相颠倒字符顺序）


```python
from collections import Counter   
 
def anagram(first, second):    
    return Counter(first) == Counter(second)    
anagram("abcd3", "3acdb") # True
```



## 3.检查内存使用情况


```python
import sys    
variable = 30     
print(sys.getsizeof(variable)) # 24
```

## 4.字节大小计算

以下方法将以字节为单位返回字符串长度。


```python
def byte_size(string):    
    return(len(string.encode( utf-8 )))   
     
byte_size( 😀 ) # 4    
byte_size( Hello World ) # 11
```

## 5.重复打印字符n次


```python
n = 2; 
s ="Programming"; print(s * n); 
# ProgrammingProgramming
```

## 6.首字母大写


```python
s = "programming is awesome"    
print(s.title()) # Programming Is Awesome
```

## 7.分块


```python
from math import ceil 
   
def chunk(lst, size):    
    return list(    
        map(lambda x: lst[x * size:x * size + size],    
            list(range(0, ceil(len(lst) / size)))))    
chunk([1,2,3,4,5],2) # [[1,2],[3,4],5]
```

## 8.压缩

以下方法使用 fliter() 删除列表中的错误值（如：False, None, 0 和“”）


```python
def compact(lst):    
    return list(filter(bool, lst))    
compact([0, 1, False, 2,   , 3,  a ,  s , 34]) # [ 1, 2, 3,  a ,  s , 34 ]
```

## 9.间隔数

以下代码段可以用来转换一个二维数组。


```python
array = [[ a ,  b ], [ c ,  d ], [ e ,  f ]]    
transposed = zip(*array)    
print(transposed) # [( a ,  c ,  e ), ( b ,  d ,  f )]
```

## 10.链式比较

以下代码可以在一行中用各种操作符进行多次比较。


```python
a = 3    
print( 2 < a < 8) # True    
print(1 == a < 2) # False
```

## 11.逗号分隔


```python
hobbies = ["basketball", "football", "swimming"]
print("My hobbies are: " + ", ".join(hobbies)) # My hobbies are: basketball, football, swimming
```

## 12.计算元音字母数


```python
import re    
def count_vowels(str):    
    return len(len(re.findall(r [aeiou] , str, re.IGNORECASE)))    
count_vowels( foobar ) # 3    
count_vowels( gym ) # 0
```

## 13.首字母恢复小写


```python
def decapitalize(string):    
    return str[:1].lower() + str[1:]    
decapitalize( FooBar ) #  fooBar     
decapitalize( FooBar ) #  fooBar
```

## 14.平面化

以下方法使用递归来展开潜在的深度列表。


```python
def spread(arg):
    ret = []
    for i in arg:
        if isinstance(i, list):
            ret.extend(i)
        else:
            ret.append(i)
    return ret
def deep_flatten(lst):
    result = []
    result.extend(
        spread(list(map(lambda x: deep_flatten(x) if type(x) == list else x, lst))))
    return result
deep_flatten([1, [2], [[3], 4], 5]) # [1,2,3,4,5]
```

## 15.差异


```python
def difference(a, b):
    set_a = set(a)
    set_b = set(b)
    comparison = set_a.difference(set_b)
    return list(comparison)
difference([1,2,3], [1,2,4]) # [3]
```

## 16.寻找差异


```python
def difference_by(a, b, fn):
    b = set(map(fn, b))
    return [item for item in a if fn(item) not in b]
from math import floor
difference_by([2.1, 1.2], [2.3, 3.4],floor) # [1.2]
difference_by([{  x : 2 }, {  x : 1 }], [{  x : 1 }], lambda v : v[ x ]) # [ { x: 2 } ]
```

## 17.链式函数调用


```python
def add(a, b):
    return a + b
def subtract(a, b):
    return a - b
a, b = 4, 5
print((subtract if a > b else add)(a, b)) # 9
```

## 18.检查重复元素


```python
def has_duplicates(lst):
    return len(lst) != len(set(lst))
    
x = [1,2,3,4,5,5]
y = [1,2,3,4,5]
has_duplicates(x) # True
has_duplicates(y) # False
```

## 19.合并两个字典


```python
def merge_two_dicts(a, b):
    c = a.copy()   # make a copy of a 
    c.update(b)    # modify keys and values of a with the ones from b
    return c
a = {  x : 1,  y : 2}
b = {  y : 3,  z : 4}
print(merge_two_dicts(a, b)) # { y : 3,  x : 1,  z : 4}
```


```python
#在python3.5版本后你还可以：
def merge_dictionaries(a, b)
   return {**a, **b}
a = {  x : 1,  y : 2}
b = {  y : 3,  z : 4}
print(merge_dictionaries(a, b)) # { y : 3,  x : 1,  z : 4}
```

## 20.将两个列表转化成一个字典


```python
def to_dictionary(keys, values):
    return dict(zip(keys, values))
    
keys = ["a", "b", "c"]    
values = [2, 3, 4]
print(to_dictionary(keys, values)) # { a : 2,  c : 4,  b : 3}
```

## 21.使用枚举


```python
以下方法将字典作为输入，然后仅返回该字典中的键。
```


```python
list = ["a", "b", "c", "d"]
for index, element in enumerate(list): 
    print("Value", element, "Index ", index, )
# ( Value ,  a ,  Index  , 0)
# ( Value ,  b ,  Index  , 1)
#( Value ,  c ,  Index  , 2)
# ( Value ,  d ,  Index  , 3)
```

## 22.计算需要的时间


```python
import time
start_time = time.time()
a = 1
b = 2
c = a + b
print(c) #3
end_time = time.time()
total_time = end_time - start_time
print("Time: ", total_time)
# ( Time:  , 1.1205673217773438e-05)
```

## 23.Try else指令

你可以将 else 子句作为 try/except 块的一部分，如果没有抛出异常，则执行该子句。


```python
try:
    2*3
except TypeError:
    print("An exception was raised")
else:
    print("Thank God, no exceptions were raised.")
#Thank God, no exceptions were raised.
```

## 24.查找最常见元素

以下方法返回列表中出现的最常见元素。


```python
def most_frequent(list):
    return max(set(list), key = list.count)
  
list = [1,2,1,2,3,2,1,4,2]
most_frequent(list)
```

## 25.回文

以下方法可检查给定的字符串是否为回文结构。该方法首先将字符串转换为小写，然后从中删除非字母数字字符。最后，它会将新的字符串与反转版本进行比较。


```python
def palindrome(string):
    from re import sub
    s = sub( [W_] ,   , string.lower())
    return s == s[::-1]
palindrome( taco cat ) # True
```

## 26.没有 if-else 语句的简单计算器


```python
import operator
action = {
    "+": operator.add,
    "-": operator.sub,
    "/": operator.truediv,
    "*": operator.mul,
    "**": pow
}
print(action[ - ](50, 25)) # 25
```

## 27.元素顺序打乱


```python
from copy import deepcopy
from random import randint
def shuffle(lst):
    temp_lst = deepcopy(lst)
    m = len(temp_lst)
    while (m):
        m -= 1
        i = randint(0, m)
        temp_lst[m], temp_lst[i] = temp_lst[i], temp_lst[m]
    return temp_lst
  
foo = [1,2,3]
shuffle(foo) # [2,3,1] , foo = [1,2,3]
```

## 28.列表扁平化


```python
def spread(arg):
    ret = []
    for i in arg:
        if isinstance(i, list):
            ret.extend(i)
        else:
            ret.append(i)
    return ret
spread([1,2,3,[4,5,6],[7],8,9]) # [1,2,3,4,5,6,7,8,9]
```

## 29.变量变换


```python
def swap(a, b):
  return b, a
a, b = -1, 14
swap(a, b) # (14, -1)
```

## 30.获取确实键的默认值


```python
d = { a : 1,  b : 2}
print(d.get( c , 3)) # 3
```

