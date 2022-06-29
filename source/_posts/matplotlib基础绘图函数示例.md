---
banner_img: /images/uploads/matplotlib.png
index_img: /images/uploads/created_with_matplotlib-logo.svg.png
sticky: ""
title: 2.Matplotlib基础绘图函数示例
date: 2022-06-29 19:01:20
updated: 2022-06-29 19:01:20
tags:
  - Python
  - Matplotlib
categories:
  - Python
  - 数据分析之展示
comments: true
---


## pyplot的基础图标函数

| 函数                                 | 说明                           |
| ------------------------------------ | ------------------------------ |
| `plt.plot(x,y,fmt,...)`              | 绘制一个坐标图                 |
| `plt.boxplot(data,notch,position)`   | 绘制一个箱型图                 |
| `plt.bar(left,height,width,bottom)`  | 绘制一个条形图                 |
| `plt.barh(width,bottom,left,height)` | 绘制一个横向条形图             |
| `plt.polar(theta,r)`                 | 绘制极坐标图                   |
| `plt.pie(data,explode)`              | 绘制饼图                       |
| `plt.psd(x,NFFT=256,pad_to,Fs)`      | 绘制功率谱密度图绘制谱图       |
| `plt.specgram(x,NFFT=256,pad_to,F)`  | 绘制散点图                     |
| `plt.cohere(x,y,NFFT=256,Fs)`        | 绘制X-Y的相关性函数            |
| `plt.scatter(x,y)`                   | 绘制散点图，其中，x和y长度相同 |
| `plt.step(x,y,where)`                | 绘制步阶图                     |
| `plt.hist(x,bins,normed)`            | 绘制直方图                     |
| `plt.contour(X,Y,Z,N)`               | 绘制等值图                     |
| `plt.vlines()`                       | 绘制垂直图                     |
| `plt.stem(x,y,linefmt,markerfmt)`    | 绘制柴火图                     |
| `plt.plot_date()`                    | 绘制数据日期                   |

## pyplot饼图的绘制

```python
import matplotlib.pyplot as plt

labels='Frogs','Hogs','Dogs','Logs'  # 设定每块饼的名称
sizes=[15,30,45,10]  # 设定比例
explode=(0,0.1,0,0)  # 将30%在饼图中突出出来

plt.pie(sizes,explode=explode,labels=labels,autopct='%1.1f%%',shadow=False,startangle=90)  # autopct表示显示百分数的方式，shadow代表是二维饼图还是三维有阴影的立体效果，startangle表示饼图的起始角度

plt.axis('equal')  # 表示在不改变饼图的情况下，饼图的x，y轴方向上的尺寸应该是一样的
plt.show()

```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210723130114684.png)

## pyplot直方图的绘制

```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(0)
mu,sigma=100,20
a=np.random.normal(mu,sigma,size=100)

plt.hist(a, 10,normed=1,density=True,histtype='stepfilled',facecolor='b',alpha=0.75)  # bin代表直方的个数，根据所给数据在区间分布的多少绘制直方;density将元素出现的个数归一化为元素出现的概率，表示在纵坐标上，如果为False，则纵坐标代表在直方中出现的a的个数
plt.title("Histogram")

plt.show()
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210724181602431.png)

> 直方图可以很清晰的看出，一个数组在最低和最高之间个数的变化；可以归一化，协调，看到个数层面，取值层面的分布

## pyplot极坐标图的绘制

```python
import matplotlib.pyplot as plt
import numpy as np

N=20  # 设定绘制图形的数目
theta=np.linspace(0.0,2*np.pi,N,endpoint=False)  # 使用linspace函数生成0-2Π范围内一定步长的20个数字。
radii=10*np.random.rand(N)  # 使用rand函数生成0-1范围内的数字并乘10
width=np.pi/4*np.random.rand(N)  # Π/4乘以数组生成宽度

ax=plt.subplot(111, projection='polar') ## polar代表绘制极坐标图，存为变量ax
bars=ax.bar(theta,radii,width=width,bottom=0.0)  # 面向对象的方法
# theta，radii，width分别对应极坐标的left，height，width；left代表起始的位置，height代表从中心点想边缘绘制的长度，width代表弧度
for r,bar in zip(radii,bars):  # 设定每一个区域的颜色
    bar.set_facecolor(plt.cm.viridis(r/10.))
    bar.set_alpha(0.5)
    
plt.show()
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210724214137197.png)

## pyplot散点图的绘制

```python
import matplotlib.pyplot as plt
import numpy as np

fig,ax=plt.subplots()  # 面向对象
ax.plot(10*np.random.randn(100),10*np.random.randn(100),'o')
ax.set_title('Simple Scatter')

plt.show()
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210725120324252.png)

```python
# t
import matplotlib.pyplot as plt
import numpy as np

plt.plot(10*np.random.randn(100),10*np.random.randn(100),'o')
plt.title('Simple Scatter')
plt.show()
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210725121724655.png)