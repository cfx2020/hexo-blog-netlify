---
banner_img: /images/uploads/686fced360d1fbcda9f936fe8203e6ae.jpeg
index_img: /images/uploads/7cecd777631c9b5ff93088e29c4fc97e.jpeg
title: 2.Pandas数据特征分析
date: 2022-06-29 20:57:04
updated: 2022-06-29 20:57:04
tags:
  - Python
  - Pandas
categories:
  - Python
  - 数据分析之概要
comments: true
---


## **对一组数据的理解**

**对一组数据的理解**：一组数据表达一个或多个含义，通过摘要，有损的提取数据特征的过程，我们可以得到：

+ 基本统计（含排序）
+ 分布/累计统计
+ 数据特征，相关性、周期等
+ 数据挖掘（形成知识）

## 数据的排序

`.sort_index()`方法在指定轴上根据索引进行排序，默认升序

`.sort_index(axis=0,ascending=True)`

```python
import pandas as pd

import numpy as np

b=pd.DataFrame(np.arange(20).reshape(4,5),index=['c','a','d','b'])

b
Out[83]: 
    0   1   2   3   4
c   0   1   2   3   4
a   5   6   7   8   9
d  10  11  12  13  14
b  15  16  17  18  19

b.sort_index()  # 默认0轴作用
Out[84]: 
    0   1   2   3   4
a   5   6   7   8   9
b  15  16  17  18  19
c   0   1   2   3   4
d  10  11  12  13  14

b.sort_index(ascending=False)  # 进行降序排序
Out[85]: 
    0   1   2   3   4
d  10  11  12  13  14
c   0   1   2   3   4
b  15  16  17  18  19
a   5   6   7   8   9


b=pd.DataFrame(np.arange(20).reshape(4,5),index=['c','a','d','b'])

b
Out[4]: 
    0   1   2   3   4
c   0   1   2   3   4
a   5   6   7   8   9
d  10  11  12  13  14
b  15  16  17  18  19

c=b.sort_index(axis=1,ascending=False)

c
Out[6]: 
    4   3   2   1   0
c   4   3   2   1   0
a   9   8   7   6   5
d  14  13  12  11  10
b  19  18  17  16  15

c=c.sort_index()

c
Out[8]: 
    4   3   2   1   0
a   9   8   7   6   5
b  19  18  17  16  15
c   4   3   2   1   0
d  14  13  12  11  10

```

`.sort_values()`方法在指定轴上根据数值进行排序，默认升序。

`Series.sort_values(axis=0,ascending=True)`

`DataFrame.sort_values(by,axis=0,ascending=True)`，by指axis轴上的某个索引或索引列表

```python
c=b.sort_values(2,ascending=False)  # 在axis=0的方向上，第二列进行数值降序排列

c
Out[11]: 
    0   1   2   3   4
b  15  16  17  18  19
d  10  11  12  13  14
a   5   6   7   8   9
c   0   1   2   3   4

c=c.sort_values('a',axis=1,ascending=False)  # 在axis=1的方向上，第a行进行数值降序排列

c
Out[13]: 
    4   3   2   1   0
b  19  18  17  16  15
d  14  13  12  11  10
a   9   8   7   6   5
c   4   3   2   1   0
```

对于空值NaN，将统一放到排序末尾

```python
a=pd.DataFrame(np.arange(12).reshape(3,4),index=['a','b','c'])

b=pd.DataFrame(np.arange(20).reshape(4,5),index=['c','a','d','b'])

a
Out[16]: 
   0  1   2   3
a  0  1   2   3
b  4  5   6   7
c  8  9  10  11

b
Out[17]: 
    0   1   2   3   4
c   0   1   2   3   4
a   5   6   7   8   9
d  10  11  12  13  14
b  15  16  17  18  19

c=a+b

c
Out[19]:   #不论是升序还是降序，NaN都放在排序末尾
      0     1     2     3   4
a   5.0   7.0   9.0  11.0 NaN
b  19.0  21.0  23.0  25.0 NaN
c   8.0  10.0  12.0  14.0 NaN
d   NaN   NaN   NaN   NaN NaN

c.sort_values(2,ascending=False)
Out[20]: 
      0     1     2     3   4
b  19.0  21.0  23.0  25.0 NaN
c   8.0  10.0  12.0  14.0 NaN
a   5.0   7.0   9.0  11.0 NaN
d   NaN   NaN   NaN   NaN NaN

c.sort_values(2,ascending=True)
Out[21]: 
      0     1     2     3   4
a   5.0   7.0   9.0  11.0 NaN
c   8.0  10.0  12.0  14.0 NaN
b  19.0  21.0  23.0  25.0 NaN
d   NaN   NaN   NaN   NaN NaN
```

## 数据的基本统计分析

适用于Series和DataFrame类型的基本统计分析函数

| 方法                | 说明                             |
| ------------------- | -------------------------------- |
| `.sum`              | 计算数据的总和，按0轴计算，下同  |
| `.count()`          | 非NaN值的数量                    |
| `.mean() .median()` | 计算数据的算术平均值，算术中位数 |
| `.var() .std()`     | 计算数据的方差，标准差           |
| `.min() .max()`     | 计算数据的最小值，最大值         |
| `.describe()`       | 针对0轴（各列）的统计汇总        |

只适用于Series类型

| 方法                  | 说明                                                 |
| --------------------- | ---------------------------------------------------- |
| `.argmin() .argmax()` | 计算数据最大值、最小值所在位置的索引位置（自动索引） |
| `.idxmin() .idxmax()` | 计算数据最大值、最小值所在位置的索引（自定义索引）   |

```python
import pandas as pd
import numpy as np

a=pd.Series([9,8,7,6],index=['a','b','c','d'])

a
Out[3]: 
a    9
b    8
c    7
d    6
dtype: int64

a.describe()  # describe函数能够返回一个Series对象，里面包含原Series对象的基本信息，可以用索引的方式提取
Out[4]: 
count    4.000000
mean     7.500000
std      1.290994
min      6.000000
25%      6.750000
50%      7.500000
75%      8.250000
max      9.000000
dtype: float64

type(a.describe())
Out[5]: pandas.core.series.Series

a.describe()['count']
Out[6]: 4.0

a.describe()['max']
Out[7]: 9.0
    
b=pd.DataFrame(np.arange(20).reshape(4,5),index=['c','a','d','b'])

b.describe()
Out[14]: 
               0          1          2          3          4
count   4.000000   4.000000   4.000000   4.000000   4.000000
mean    7.500000   8.500000   9.500000  10.500000  11.500000
std     6.454972   6.454972   6.454972   6.454972   6.454972
min     0.000000   1.000000   2.000000   3.000000   4.000000
25%     3.750000   4.750000   5.750000   6.750000   7.750000
50%     7.500000   8.500000   9.500000  10.500000  11.500000
75%    11.250000  12.250000  13.250000  14.250000  15.250000
max    15.000000  16.000000  17.000000  18.000000  19.000000

type(b.describe())
Out[17]: pandas.core.frame.DataFrame

b.describe().loc['max']  # .ix属性已取消，使用.loc替代
Out[19]: 
0    15.0
1    16.0
2    17.0
3    18.0
4    19.0
Name: max, dtype: float64

b.describe()[2]
Out[20]: 
count     4.000000
mean      9.500000
std       6.454972
min       2.000000
25%       5.750000
50%       9.500000
75%      13.250000
max      17.000000
Name: 2, dtype: float64

```

## 数据的累计统计分析

适用于Series和DataFrame类型

| 方法         | 说明                             |
| ------------ | -------------------------------- |
| `.cumsum()`  | 依次给出前1、2、…、n个数的和     |
| `.cumprod()` | 依次给出前1、2、…、n个数的积     |
| `.cummax()`  | 依次给出前1、2、…、n个数的最大值 |
| `.cummin()`  | 依次给出前1、2、…、n个数的最小值 |

```python
b=pd.DataFrame(np.arange(20).reshape(4,5),index=['c','a','d','b'])

b
Out[21]: 
    0   1   2   3   4
c   0   1   2   3   4
a   5   6   7   8   9
d  10  11  12  13  14
b  15  16  17  18  19

b.cumsum()  # 默认作用于0轴，计算列方向的前n项和
Out[22]: 
    0   1   2   3   4
c   0   1   2   3   4
a   5   7   9  11  13
d  15  18  21  24  27
b  30  34  38  42  46

b.cumprod()  # 计算列方向的前n项积
Out[23]: 
   0     1     2     3     4
c  0     1     2     3     4
a  0     6    14    24    36
d  0    66   168   312   504
b  0  1056  2856  5616  9576

b.cummin()  # 计算0轴方向之前的最小值
Out[24]: 
   0  1  2  3  4
c  0  1  2  3  4
a  0  1  2  3  4
d  0  1  2  3  4
b  0  1  2  3  4

b.cummax()  # 计算0轴方向之前的最大值
Out[25]: 
    0   1   2   3   4
c   0   1   2   3   4
a   5   6   7   8   9
d  10  11  12  13  14
b  15  16  17  18  19
```

适用于Series和DataFrame类型的滚动计算（窗口计算）函数：

| 方法                       | 说明                                |
| -------------------------- | ----------------------------------- |
| `.rolling(w).sum()`        | 依次计算相邻w个元素的和             |
| `.rolling(w).mean()`       | 依次计算相邻w个元素的算术平均值     |
| `.rolling(w).var()`        | 依次计算相邻w个元素的方差           |
| `.rolling(w).std()`        | 依次计算相邻w个元素的标准差         |
| `.rolling(w).min() .max()` | 依次计算相邻w个元素的最小值和最大值 |

```python
b
Out[26]: 
    0   1   2   3   4
c   0   1   2   3   4
a   5   6   7   8   9
d  10  11  12  13  14
b  15  16  17  18  19

b.rolling(2).sum()  # 默认作用于0轴，求前w项和自己的和，如果前w项不足返回NaN
Out[27]: 
      0     1     2     3     4
c   NaN   NaN   NaN   NaN   NaN
a   5.0   7.0   9.0  11.0  13.0
d  15.0  17.0  19.0  21.0  23.0
b  25.0  27.0  29.0  31.0  33.0

b.rolling(3).sum()
Out[28]: 
      0     1     2     3     4
c   NaN   NaN   NaN   NaN   NaN
a   NaN   NaN   NaN   NaN   NaN
d  15.0  18.0  21.0  24.0  27.0
b  30.0  33.0  36.0  39.0  42.0

```

## 数据的相关分析

**相关分析**：两个事物，表示为X和Y，若：

+ X增大，Y增大，两个变量正相关
+ X增大，Y减小，两个变量负相关
+ X增大，Y无视，两个变量不相关

这是最浅显的相关分析，统计学上用协方差来显示事物的相关性：

**协方差**:
$$
cov(X,Y)=\frac{\sum^n_{i=1}(X_i-\bar{X})(Y_i-\bar{Y})}{n-1}
$$

+ 协方差>0，X和Y正相关
+ 协方差<0，X和Y负相关
+ 协方差=0，X和Y独立无关

**Pearson相关系数**：
$$
r=\frac{\sum^n_{i=1}(x_i-\bar{x})(y_i-\bar{y})}{\surd\sum^n_{i=1}(x_i-\bar{x})^2\surd\sum^n_{i=1}(y_i-\bar{y})^2}
$$
r的取值范围为[-1,1]，当取绝对值时有：

+ 0.8-1.0极强相关
+ 0.6-0.8强相关
+ 0.4-0.6中等程度相关
+ 0.2-0.4弱相关
+ 0.0-0.2极弱相关或无相关

适用于Series和DataFrame类型的相关分析函数

| 方法      | 说明                                               |
| --------- | -------------------------------------------------- |
| `.cov()`  | 计算协方差                                         |
| `.corr()` | 计算相关系数矩阵，Pearson、Spearman、Kendall等系数 |

```python
# 房价和rmb的相关性
import pandas as pd
import matplotlib.pyplot as plt

hprice=pd.Series([3.04,22.93,12.75,22.6,12.33],index=['2008','2009','2010','2011','2012'])

m2=pd.Series([8.18,18.38,9.13,7.82,6.69],index=['2008','2009','2010','2011','2012'])

hprice.corr(m2)
Out[32]: 0.5239439145220387
    
plt.plot(hprice.index,hprice.values,hprice.index,m2.values)
Out[37]: 
[<matplotlib.lines.Line2D at 0x1d0aadc3f40>,
 <matplotlib.lines.Line2D at 0x1d0aadd2040>]

```

![image-20210731180234926](https://raw.githubusercontent.com/cfx2020/image/main/image-20210731180234926.png)

