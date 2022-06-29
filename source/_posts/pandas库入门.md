---
banner_img: /images/uploads/686fced360d1fbcda9f936fe8203e6ae.jpeg
index_img: /images/uploads/7cecd777631c9b5ff93088e29c4fc97e.jpeg
title: Pandas库入门
date: 2022-06-29 20:53:13
updated: 2022-06-29 20:53:13
tags:
  - Python
  - Pandas
categories:
  - Python
  - 数据分析之概要
comments: true
---


## Pandas简介

**官网**：http://pandas.pydata.org

**Pandas**是Python第三方库，提供高性能易用数据类型和分析工具。

使用`import pandas as pd`调用pandas库，Pandas基于NumPy实现，常与NumPy和Matplotlib一同使用。

```python
import pandas as pd

d=pd.Series(range(20))

d
Out[9]: 
0      0  # 前一项是索引，后一项是值
1      1
2      2
3      3
4      4
5      5
6      6
7      7
8      8
9      9
10    10
11    11
12    12
13    13
14    14
15    15
16    16
17    17
18    18
19    19
dtype: int64
    
d.cumsum()  # 对前N项进行求和，第三项等于前两项的和，也就是索引值为i等于前i项之和
Out[10]: 
0       0
1       1
2       3
3       6
4      10
5      15
6      21
7      28
8      36
9      45
10     55
11     66
12     78
13     91
14    105
15    120
16    136
17    153
18    171
19    190
dtype: int64

```

## Pandas库的理解

**Pandas**库有两个数据类型：Series，DataFrame，Series相当于一个一维的数据类型，DataFrame相当于一个二维到多维的数据类型。

基于这两个数据类型，pandas支持了基本操作、运算操作、特征类操作、关联类操作

NumPy和Pandas的对比：

| NumPy              | Pandas             |
| ------------------ | ------------------ |
| 基础数据类型       | 扩展数据类型       |
| 关注数据的结构表达 | 关注数据的应用表达 |
| 维度：数据间关系   | 数据与索引间关系   |

> NumPy过于注重数据的结构化表示，数据的维度，但实际应用中过于注重数据结构不利于数据的使用，Pandas则注重数据使用，拥有非常明确有效的索引，通过索引对数据进行相关的分析和提取。

## Pandas库的Series类型

**Series**类型由一组数据及与之相关的数据索引组成。

```python
import pandas as pd

a=pd.Series([9,8,7,6])

a
Out[14]:   # 其中第一列为自动索引
0    9
1    8
2    7
3    6
dtype: int64  # NumPy中数据类型
```

```python
import pandas as pd

b=pd.Series([9,8,7,6],index=['a','b','c','d'])  # pandas的自定义索引，作为第二个参数，可以省略index=

b
Out[17]: 
a    9
b    8
c    7
d    6
dtype: int64
```

> Series要求每一个数据都有一个索引，要么由pandas生成自动索引，要么生成自定义索引

Series类型可以由如下类型创建：

+ Python列表

+ 标量值

  ```python
  import pandas as pd
  
  s=pd.Series(25,index=['a','b','c'])  # 由于25是一个标量，所以必须指定index索引，规定数据结构，比如由几个元素构成
  
  s
  Out[17]: 
  a    25
  b    25
  c    25
  dtype: int64
  ```

+ Python字典

  ```python
  import pandas as pd
  
  d=pd.Series({'a':9,'b':8,'c':7})  # 字典是由键值对构成的，所以我们可以把键作为值的索引
  
  d
  Out[17]: 
  a    9
  b    8
  c    7
  dtype: int64
      
  e=pd.Series(['a':9,'b':8,'c':7],index=['c','a','b','d'])  # 通过自定义索引我们可以改变原先字典的索引顺序，也就是从字典中进行选择操作同时超出的索引值会显示为NaN
  
  e
  Out[18]:
  c    7.0
  a	 9.0
  b 	 8.0
  d	 NaN
  dtype： float64
  ```

+ ndarray数组

  ```python
  import pandas as pd
  import numpy as np
  
  n=pd.Series(np.arange(5))  # 生成0-4的数值
  
  n
  Out[20]: 
  0    0
  1    1
  2    2
  3    3
  4    4
  dtype: int32
      
  m=pd.Series(np.arange(5),index=np.arange(9,4,-1))  # 生成索引9-5步长为-1
  
  m
  Out[22]: 
  9    0
  8    1
  7    2
  6    3
  5    4
  dtype: int32
  ```

+ 其他函数

### Series类型的基本操作

Series类型包括index和values两部分，操作类似ndarray和python字典类型。

```python
import pandas as pd
b=pd.Series([9,8,7,6],['a','b','c','d'])

b
Out[23]: 
a    9
b    8
c    7
d    6
dtype: int64

b.index
Out[24]: Index(['a', 'b', 'c', 'd'], dtype='object') # pandas的Index类型

b.values
Out[25]: array([9, 8, 7, 6], dtype=int64)  # array类型
    
b['b']  # 使用自定义索引进行取值
Out[26]: 8

b[1]  # 使用默认索引取值
Out[27]: 8

b[['c','d',0]]  # 两套索引并存但不能混用
Out[28]:
c	 7.0
d	 6.0
0	 NaN
dtype: float64

b[['c','d','a']]  # 可以同时取出多个索引值
Out[29]: 
c    7
d    6
a    9
dtype: int64
```

Series类型的操作类似ndarray类型：

+ 索引方法相同，采用[]
+ NumPy中运算和操作可用于Series类型
+ 可以通过自定义索引的列表进行切片
+ 可以通过自动索引进行切片，如果存在自定义索引，则一同被切片。

```python
b
Out[30]: 
a    9
b    8
c    7
d    6
dtype: int64

b[3]
Out[31]: 6

b[:3]
Out[32]: # 与ndarray数组不同，Series类型在切片后仍然是Series类型，而ndarray是array数组类型
a    9
b    8
c    7
dtype: int64

b[b>b.median()]  # 输出大于所有元素中位数的元素
Out[33]: 
a    9
b    8
dtype: int64



np.exp(b)  # 进行e^x运算，输出仍然是Series类型
Out[34]: 
a    8103.083928
b    2980.957987
c    1096.633158
d     403.428793
dtype: float64
```

> Series类型本身是索引和值组成的类型，对它进行切片和运算都是生成Series类型，如果进行索引则于ndarray一样是数值

Series类型的操作类似Python字典类型

+ 通过自定义索引访问
+ 保留字in操作
+ 使用.get()方法

```python
b
Out[36]: 
a    9
b    8
c    7
d    6
dtype: int64

b['b']
Out[37]: 8

0 in b  # 判断元素是否在Series类型的索引中，并不判断值，只判断键，也不判断自动索引
Out[38]: False

'c' in b
Out[39]: True

b.get('f',100)  # 提取Series的索引为f的值，如果不存在则显示100
Out[40]: 100
```

### Series类型对齐操作

Series类型在运算中会自动对齐不同索引的数据

```python
import pandas as pd
a=pd.Series([1,2,3],['c','d','e'])

b=pd.Series([9,8,7,6],['a','b','c','d'])  # 索引的交集进行加和运算，其余的值不进行运算

a+b
Out[44]: # 加和后的Series对象拥有两个Series对象的索引并集
a    NaN
b    NaN
c    8.0
d    8.0
e    NaN
dtype: float64
```

> NumPy只关心数据的维度，所以运算是数据的维度之间的运算；Series类型拥有索引，所以关心的是数据基于索引的运算，所以运算的更为精确

### Series类型的name属性

Series对象和所以都可以有一个名字，存储在属性.name中

```python
import pandas as pd
b=pd.Series([9,8,7,6],['a','b','c','d'])

b
Out[45]: 
a    9
b    8
c    7
d    6
dtype: int64

b.name='Series对象' # 由于Series对象只有一维，所以b.name可以认为是值列的名字，也可以认为是整个Series对象的名字

b.index.name='索引列'  #index.name对应的是索引列的名字

b
Out[48]: 
索引列
a    9
b    8
c    7
d    6
Name: Series对象, dtype: int64
```

### Series类型的修改

Series对象可以随时修改并即刻生效

```python
import pandas as pd
b=pd.Series([9,8,7,6],['a','b','c','d'])

b['a']=15

b.name='Series'

b
Out[51]: 
索引列
a    15
b     8
c     7
d     6
Name: Series, dtype: int64

b.name='New Series'

b['b','c']=20

b
Out[54]: 
索引列
a    15
b    20
c    20
d     6
Name: New Series, dtype: int64
```

### Series类型总结

Series是一维带“标签”的数组

Series基本操作类似ndarray和字典，根据索引对齐。

---

## Pandas库的DataFrame类型

**DataFrame**类型是一个：

+ 表格型的数据类型，每列值类型可以不同
+ 它既有行索引、也有列索引，行索引叫index(axis=0),列索引叫column(axis=1)
+ 它常用于表达二维数据，但也可以表达多维数据

**DataFrame**可以由如下类型创建：

+ 二维ndarray对象

  ```python
  import pandas as pd
  import numpy as np
  
  d=pd.DataFrame(np.arange(10).reshape(2,5))
  
  d
  Out[56]:   # 生成了自动行索引和自动列索引
     0  1  2  3  4
  0  0  1  2  3  4
  1  5  6  7  8  9
  ```

+ 由一维ndarray、列表、字典、元组或Series构成的字典

  ```python
  import pandas as  pd
  dt={'one':pd.Series([1,2,3],index=['a','b','c']),
      'two':pd.Series([9,8,7,6],index=['a','b','c','d'])}
  
  d=pd.DataFrame(dt)
  
  d
  Out[2]:   # 一维Series的键变成了列索引，index变成了行索引，pandas会自动对齐，取并集。
     one  two
  a  1.0    9
  b  2.0    8
  c  3.0    7
  d  NaN    6
  
  pd.DataFrame(dt,index=['b','c','d'],columns=['two','three'])
  Out[3]:   # 指定新的列索引和行索引，pandas会根据dt自动选择元素
     two three
  b    8   NaN
  c    7   NaN
  d    6   NaN
  
  # 使用列表类型的字典创建
  d1={'one':[1,2,3,4],'two':[9,8,7,6]}
  
  d=pd.DataFrame(d1,index=['a','b','c','d'])
  
  d
  Out[6]: 
     one  two
  a    1    9
  b    2    8
  c    3    7
  d    4    6
  
  import pandas as  pd
  d1={'城市':['北京','上海','广州','深圳','沈阳'],
      '环比':[101.5,101.2,101.3,102.0,100.1],
      '同比':[120.7,127.3,119.4,140.9,101.4],
      '定基':[121.4,127.8,120.0,145.5,101.6]}
  
  d=pd.DataFrame(d1,index=['c1','c2','c3','c4','c5'])
  
  d
  Out[13]: 
      城市     环比     同比     定基
  c1  北京  101.5  120.7  121.4
  c2  上海  101.2  127.3  127.8
  c3  广州  101.3  119.4  120.0
  c4  深圳  102.0  140.9  145.5
  c5  沈阳  100.1  101.4  101.6
  
  d.index
  Out[14]: Index(['c1', 'c2', 'c3', 'c4', 'c5'], dtype='object')
  
  d.columns
  Out[15]: Index(['城市', '环比', '同比', '定基'], dtype='object')
  
  d.values
  Out[16]: 
  array([['北京', 101.5, 120.7, 121.4],
         ['上海', 101.2, 127.3, 127.8],
         ['广州', 101.3, 119.4, 120.0],
         ['深圳', 102.0, 140.9, 145.5],
         ['沈阳', 100.1, 101.4, 101.6]], dtype=object)
  
  d['同比']  # 获取列索引的值
  Out[17]: 
  c1    120.7
  c2    127.3
  c3    119.4
  c4    140.9
  c5    101.4
  Name: 同比, dtype: float64
  
  d.loc['c2']  # .ix属性已被pandas删除，使用.loc替代，获取行索引的值
  Out[21]: 
  城市       上海
  环比    101.2
  同比    127.3
  定基    127.8
  Name: c2, dtype: object
          
  d['同比']['c2']  # 获取指定的列和行的元素
  Out[24]: 127.3
  ```

+ Series类型

+ 其他DataFrame类型

## Pandas库的数据类型操作

要改变（删除，重排，增加）Series和DataFrame对象，我们可以使用如下方法

+ 对于增加或重排：重新索引
+ 删除：drop

### 重新索引

`.reindex()`能够改变或重排Series和DataFrame索引

```
import pandas as  pd
d1={'城市':['北京','上海','广州','深圳','沈阳'],
    '环比':[101.5,101.2,101.3,102.0,100.1],
    '同比':[120.7,127.3,119.4,140.9,101.4],
    '定基':[121.4,127.8,120.0,145.5,101.6]}

d=pd.DataFrame(d1,index=['c1','c2','c3','c4','c5'])

d
Out[13]: 
    城市     环比     同比     定基
c1  北京  101.5  120.7  121.4
c2  上海  101.2  127.3  127.8
c3  广州  101.3  119.4  120.0
c4  深圳  102.0  140.9  145.5
c5  沈阳  100.1  101.4  101.6

d=d.reindex(index=['c5','c4','c3','c2','c1'])

d
Out[31]: 
    城市     环比     同比     定基
c5  沈阳  100.1  101.4  101.6
c4  深圳  102.0  140.9  145.5
c3  广州  101.3  119.4  120.0
c2  上海  101.2  127.3  127.8
c1  北京  101.5  120.7  121.4

d=d.reindex(columns=['城市','同比','环比','定基'])

d
Out[33]: 
    城市     同比     环比     定基
c5  沈阳  101.4  100.1  101.6
c4  深圳  140.9  102.0  145.5
c3  广州  119.4  101.3  120.0
c2  上海  127.3  101.2  127.8
c1  北京  120.7  101.5  121.4

d['同比']['c2']
Out[24]: 127.3
```

`.refindex(index=None,columns=None,...)`的参数：

| 参数            | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| `index,columns` | 新的行列自定义索引                                           |
| `fill_value`    | 重新索引中，用于填充缺失位置的值                             |
| `method`        | 填充方法，ffill当前值向前填充，bfill向后填充，指定`fill_value`的填充方法是当前位置前面的值填充还是后面的值填充 |
| `limit`         | 最大填充量                                                   |
| `copy`          | 默认为True，生成新的对象，False时，新旧相等不复制            |

```python
newc=d.columns.insert(4,'新增')


newd=d.reindex(columns=newc,fill_value=200)

newd
Out[41]: 
    城市     同比     环比     定基   新增
c5  沈阳  101.4  100.1  101.6  200
c4  深圳  140.9  102.0  145.5  200
c3  广州  119.4  101.3  120.0  200
c2  上海  127.3  101.2  127.8  200
c1  北京  120.7  101.5  121.4  200

```

### 索引类型

Series和DataFrame的索引是Index类型，Index对象是不可修改类型

索引类型的常用方法：

| 方法                 | 说明                                   |
| -------------------- | -------------------------------------- |
| `.append(idx)`       | 链接另一个Index对象，产生新的Index对象 |
| `.diff(idx)`         | 计算差集，产生新的Index对象            |
| `.intersection(idx)` | 计算交集                               |
| `.union(idx)`        | 计算并集                               |
| `.delete(loc)`       | 删除loc位置处的元素                    |
| `.insert(loc,e)`     | 在loc位置增加一个元素e                 |

```python
d
Out[46]: 
    城市     同比     环比     定基
c5  沈阳  101.4  100.1  101.6
c4  深圳  140.9  102.0  145.5
c3  广州  119.4  101.3  120.0
c2  上海  127.3  101.2  127.8
c1  北京  120.7  101.5  121.4

nc=d.columns.delete(2)  # 删除自动索引的第3列

ni=d.index.insert(5,'c0')  # 插入第五行的自定义索引为c0

nd=d.reindex(index=ni,columns=nc).ffill()  # 将ffill放入括号内会报错，因为要求index单调递增或递减

nd
Out[51]: 
    城市     同比     定基
c5  沈阳  101.4  101.6
c4  深圳  140.9  145.5
c3  广州  119.4  120.0
c2  上海  127.3  127.8
c1  北京  120.7  121.4
c0  北京  120.7  121.4
```

### 删除指定索引对象

`.drop()`能够删除Series和DataFrame指定行或列索引，默认操作0轴元素，因为Series对象只有0轴

```python
a=pd.Series([9,8,7,6],index=['a','b','c','d'])

a
Out[53]: 
a    9
b    8
c    7
d    6
dtype: int64

a.drop(['b','c'])
Out[54]: 
a    9
d    6
dtype: int64
    
d.drop('c5')
Out[56]: 
    城市     同比     环比     定基
c4  深圳  140.9  102.0  145.5
c3  广州  119.4  101.3  120.0
c2  上海  127.3  101.2  127.8
c1  北京  120.7  101.5  121.4

d.drop('同比',axis=1)
Out[57]: 
    城市     环比     定基
c5  沈阳  100.1  101.6
c4  深圳  102.0  145.5
c3  广州  101.3  120.0
c2  上海  101.2  127.8
c1  北京  101.5  121.4

```

## Pandas库的数据类型运算

### 算术运算法则

算术运算根据：

+ 行列索引，补齐后运算，运算默认产生浮点数
+ 补齐时缺项填充NaN（空值）
+ 二维和一维，一维和零维间为广播运算
+ 采用+-*/符号进行的二元运算产生新的对象

```python
import pandas as pd
import numpy as np

a=pd.DataFrame(np.arange(12).reshape(3,4))
b=pd.DataFrame(np.arange(20).reshape(4,5))

a
Out[61]: 
   0  1   2   3
0  0  1   2   3
1  4  5   6   7
2  8  9  10  11

b
Out[62]: 
    0   1   2   3   4
0   0   1   2   3   4
1   5   6   7   8   9
2  10  11  12  13  14
3  15  16  17  18  19

a+b
Out[63]: 
      0     1     2     3   4
0   0.0   2.0   4.0   6.0 NaN
1   9.0  11.0  13.0  15.0 NaN
2  18.0  20.0  22.0  24.0 NaN
3   NaN   NaN   NaN   NaN NaN

a*b
Out[64]: 
      0     1      2      3   4
0   0.0   1.0    4.0    9.0 NaN
1  20.0  30.0   42.0   56.0 NaN
2  80.0  99.0  120.0  143.0 NaN
3   NaN   NaN    NaN    NaN NaN
```

四则运算的方法形式：

| 方法              | 说明                     |
| ----------------- | ------------------------ |
| `.add(d,**argws)` | 类型间加法运算，可选参数 |
| `.sub(d,**argws)` | 类型间减法运算，可选参数 |
| `.mul(d,**argws)` | 类型间乘法运算，可选参数 |
| `.div(d,**argws)` | 类型间除法运算，可选参数 |

```python
b.add(a,fill_value=100) # 将缺少的元素用100补齐
Out[65]: 
       0      1      2      3      4
0    0.0    2.0    4.0    6.0  104.0
1    9.0   11.0   13.0   15.0  109.0
2   18.0   20.0   22.0   24.0  114.0
3  115.0  116.0  117.0  118.0  119.0

a.mul(b,fill_value=0)  # 缺少的元素用0填充
Out[66]: 
      0     1      2      3    4
0   0.0   1.0    4.0    9.0  0.0
1  20.0  30.0   42.0   56.0  0.0
2  80.0  99.0  120.0  143.0  0.0
3   0.0   0.0    0.0    0.0  0.0
```

> fill_value参数替代NaN，替代后参与运算

```python
# 不同维度之间的运算，广播运算
b
Out[67]: 
    0   1   2   3   4
0   0   1   2   3   4
1   5   6   7   8   9
2  10  11  12  13  14
3  15  16  17  18  19

c=pd.Series(np.arange(4))

c
Out[69]: 
0    0
1    1
2    2
3    3
dtype: int32

c-10  # 低维会作用到高维的每一个元素
Out[70]: 
0   -10
1    -9
2    -8
3    -7
dtype: int32

b-c  # 一维的Series对象作用到b的1轴，也就是作用到b的每一行
Out[71]: 
      0     1     2     3   4
0   0.0   0.0   0.0   0.0 NaN
1   5.0   5.0   5.0   5.0 NaN
2  10.0  10.0  10.0  10.0 NaN
3  15.0  15.0  15.0  15.0 NaN

b.sub(c,axis=0)  # 规定axis=0才能让Series作用于0轴运算，也就是每一列与Series相减
Out[72]: 
    0   1   2   3   4
0   0   1   2   3   4
1   4   5   6   7   8
2   8   9  10  11  12
3  12  13  14  15  16
```

### 比较运算法则

比较运算：

+ 只能比较相同索引的元素，不进行补齐
+ 二维和一维、一维和零维间为广播运算
+ 采用> < >= <= == != 等符号进行的二元运算产生布尔对象

```python
# 同维度的比较运算
import pandas as pd
import numpy as np

a=pd.DataFrame(np.arange(12).reshape(3,4))

a
Out[73]: 
   0  1   2   3
0  0  1   2   3
1  4  5   6   7
2  8  9  10  11

d=pd.DataFrame(np.arange(12,0,-1).reshape(3,4))

d
Out[75]: 
    0   1   2  3
0  12  11  10  9
1   8   7   6  5
2   4   3   2  1

a>d
Out[76]: 
       0      1      2      3
0  False  False  False  False
1  False  False  False   True
2   True   True   True   True

a==d
Out[77]: 
       0      1      2      3
0  False  False  False  False
1  False  False   True  False
2  False  False  False  False

```

> 比较运算的同维度运算，尺寸要一致，否则报错

```python
# 不同维度的比较运算
import pandas as pd
import numpy as np

a=pd.DataFrame(np.arange(12).reshape(3,4))

a
Out[78]: 
   0  1   2   3
0  0  1   2   3
1  4  5   6   7
2  8  9  10  11


c=pd.Series(np.arange(4))

c
Out[79]: 
0    0
1    1
2    2
3    3
dtype: int32

a>c  # 不同维度，广播运算，默认在1轴运算，作用于每一行
Out[80]: 
       0      1      2      3
0  False  False  False  False
1   True   True   True   True
2   True   True   True   True

c>0
Out[81]: 
0    False
1     True
2     True
3     True
dtype: bool

```

