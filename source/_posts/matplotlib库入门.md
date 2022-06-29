---
banner_img: /images/uploads/matplotlib.png
index_img: /images/uploads/created_with_matplotlib-logo.svg.png
sticky: 1
title: 1.Matplotlib库入门
date: 2022-06-19 17:19:29
updated: 2022-06-19 17:19:29
tags:
  - Python
  - Matplotlib
categories:
  - Python
  - 数据分析之展示
comments: true
---


**Matplotlib**库是python优秀的数据可视化第三方库，官网为：http://matplotlib.org/

一些可视化效果可以查看：http://matplotlib.org/gallery.html

## Matplotlib库的使用

Matplotlib库由各种可视化类构成，内部结构复杂，受Matlab启发，Matplotlib的设计者想让用户可以很简单的使用Matplotlib画图，而不用去管复杂的实现类，所以Matplotlib提供了一个子库Matplotlib.pyplot。

### Matplotlib.pyplot

Matplotlib.pyplot是绘制各类可视化图形的命令子库，相当于快捷方式。

使用`import matplotlib.pyplot as plt`导入pyplot

```python
import matplotlib.pyplot as plt

plt.plot([3,1,4,5,2])
plt.ylabel("grade") # 打上纵标签
plt.savefig('test',dpi=600) # 第一个参数是文件名，第二个参数是图像质量，默认输出格式为png文件
plt.show()
```

![](https://raw.githubusercontent.com/cfx2020/image/main/pyplot.png?token=AONRX2UKBTSWDVZFLN2CUO3CV3SU6)

> plot函数在绘制图像的时候如没指定横坐标，或只输入了一组数组，则会把默认这组数组为纵坐标，并根据纵坐标的索引生成横坐标

```python
import matplotlib.pyplot as plt

plt.plot([0,2,4,6,8],[3,1,4,5,2])  # plot(x,y)两个数组分别代表横轴和纵轴
plt.ylabel("grade")
plt.axis([-1,10,0,6])  # axis函数前两个参数指定横轴的坐标区间，后两个参数为纵轴的坐标区间
plt.show()
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210722182701212.png?token=AONRX2TMLF6NY55WBOKUUXLCV3S7C)

### pyplot的绘图区域

`plt.subplot(nrows,ncols,plot_number)`函数可以在全局绘图区域中创建一个分区体系，并定位到一个子绘图区域。

+ nrows代表这块区域横轴方向分割的块数
+ ncols代表这块区域纵轴方向分割的块数
+ plot_number代表正在画的这张图在这块区域的那块位置

```python
import matplotlib.pyplot as plt
import numpy as np

def f(t):
    return np.exp(-t)*np.cos(2*np.pi*t)  # 使用exp函数实现能量衰减曲线
a= np.arange(0.0,5.0,0.02)

plt.subplot(211)  # 设置绘图区域为2x1
plt.plot(a,f(a))

plt.subplot(2,1,2)
plt.plot(a,np.cos(2*np.pi*a),'r--')  # 绘制能量衰减曲线的正弦波函数，并使用虚线绘图。
plt.show()
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210722191257837.png?token=AONRX2XDIM2QPNBHLP5FJZ3CV3TC2)

### pyplot的plot()函数

`plt.plot(x,y,format_string,**kwargs)`

+ x：X轴数据，列表或数组，可选

+ y：Y轴数据，列表或数组

+ format_string：控制曲线的格式字符串，可选

  由颜色字符、风格字符和标记字符组成

+ **kwargs：第二组或更多(x,y,format_string)

当绘制多条曲线时，各条曲线的x不能省略。

```python
mport matplotlib.pyplot as plt
import numpy as np

a=np.arange(10)
plt.plot(a,a*1.5,a,a*2.5,a,a*3.5,a,a*4.5)
plt.axis([-1,10,-1,40])
plt.show()
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210722195141855.png?token=AONRX2UTLPK6H65S2QT3TS3CV3TEM)

**format_string**参数是控制曲线格式的字符串，由颜色字符、风格字符和标记字符组成。



| <div style="width:100px">颜色字符</div>|<div style="width:100px">说明</div>|
| ----------- | ------------ |
| `'b'`       | 蓝色         |
| `'g'`       | 绿色         |
| `'r'`       | 红色         |
| `'c'`       | 青绿色       |
| `'#008000'` | RGB某颜色    |
| `'m'`       | 洋红色       |
| `'y'`       | 黄色         |
| `'k'`       | 黑色         |
| `'w'`       | 白色         |
| `'0.8'`     | 灰度值字符串 |



| <div style="width:100px">风格字符</div> | <div style="width:100px">说明</div>   |
| -------- | ------ |
| `'-'`    | 实线   |
| `'--'`   | 破折线 |
| `'-.'`   | 点划线 |
| `':'`    | 虚线   |
| `'',' '` | 无线条 |



| <div style="width:100px">标记字符 | <div style="width:100px">说明</div>               |
| -------- | ------------------ |
| `'.'`    | 点标记             |
| `','`    | 像素标记（极小点） |
| `'o'`    | 实心圈标记         |
| `'v'`    | 倒三角标记         |
| `'^'`    | 上三角标记         |
| `'>'`    | 右三角标记         |
| `'<'`    | 左三角标记         |
| `'1'`    | 下花三角标记       |
| `'2'`    | 上花三角标记       |
| `'3'`    | 左花三角标记       |
| `'4'`    | 右花三角标记       |
| `'s'`    | 实心方形标记       |
| `'p'`    | 实心五角标记       |
| `'*'`    | 星形标记           |
| `'h'`    | 竖六边形标记       |
| `'H'`    | 横六边形标记       |
| `'+'`    | 十字标记           |
| `'x'`    | x标记              |
| `'D'`    | 菱形标记           |
| `'d'`    | 瘦菱形标记         |
| `'|'`    | 垂直线标记         |


```python
import matplotlib.pyplot as plt
import numpy as np

a=np.arange(10)
plt.plot(a,a*1.5,'go-',a,a*2.5,'rx',a,a*3.5,'*',a,a*4.5,'b-.')

plt.show()
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210722212414639.png?token=AONRX2VGRCZO2HAYCUDBX2LCV3THE)

** **kwargs**是可选参数，以上的颜色，风格，标记也都可以表示：

+ color：控制颜色，`color='green'`
+ linestyle：线条风格，`linestyle='dashed'`
+ marker：标记风格，`marker='o'`
+ markerfacecolor：标记颜色，`markerfacecolor='bule'`
+ markersize：标记尺寸，`markersize=20`
+ ……

### pyplot的中文显示

**pyplot**并不默认支持中文显示，需要rcParams修改字体实现

```python
import matplotlib.pyplot as plt
import matplotlib

matplotlib.rcParams['font.family']='SimHei' #黑体
plt.plot([3,1,4,5,2])
plt.ylabel('纵轴（值）')
plt.show()
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210722214020212.png?token=AONRX2S4Z2KMIDHHNZVNSQDCV3TJM)

rcParams的属性：



| <div style="width:100px">属性 </div>         | <div style="width:100px">说明</div>                                     |
| ------------- | ---------------------------------------- |
| `font.family` | 用于显示字体的名字                       |
| `font.style`  | 字体风格，正常’normal‘或斜体’italic‘     |
| `font.size`   | 字体大小，整数字号或者’large‘、’x-small‘ |

| <div style="width:100px">中文字体</div>   | <div style="width:100px">说明</div>     |
| ---------- | -------- |
| `SimHei`   | 黑体     |
| `Kaiti`    | 楷体     |
| `LiSu`     | 隶书     |
| `FangSong` | 仿宋     |
| `YouYuan`  | 幼圆     |
| `STSong`   | 华文宋体 |


```python
import matplotlib.pyplot as plt
import matplotlib
import numpy as np

matplotlib.rcParams['font.family']='STSong'
matplotlib.rcParams['font.size']=20  # 将所有字体都变为中文字体，是全局的

a = np.arange(0.0,5.0,0.02)

plt.xlabel('横轴：时间')
plt.ylabel('纵轴：振幅')
plt.plot(a,np.cos(2*np.pi*a),'r--')
plt.show()
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210722215539763.png?token=AONRX2WMG7EOVSCITE46WY3CV3TLY)

为了能够使用局部的中文字体我们在有中文输出的地方，增加一个`fontproperties`属性。这也是最推荐的方法上面的代码变为：

```python
import matplotlib.pyplot as plt
import numpy as np

a = np.arange(0.0,5.0,0.02)

plt.xlabel('横轴：时间',fontproperties='SimHei',fontsize=20)
plt.ylabel('纵轴：振幅',fontproperties='SimHei',fontsize=20)
plt.plot(a,np.cos(2*np.pi*a),'r--')
plt.show()
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210722220043902.png?token=AONRX2WNZ43YBLYAAT3RLZLCV3TNG)

#### pyplot的文本显示函数



| <div style="width:100px">函数</div>           | <div style="width:100px">说明</div>                     |
| -------------- | ------------------------ |
| `plt.xlabel()` | 对X轴增加文本标签        |
| `plt.ylabel`   | 对Y轴增加文本标签        |
| `plt.title`    | 对图形整体增加文本标题   |
| `plt.text`     | 在任意位置增加文本       |
| `plt.annotate` | 在图形中增加带箭头的注解 |


```python
import matplotlib.pyplot as plt
import numpy as np

a = np.arange(0.0,5.0,0.02)
plt.plot(a,np.cos(2*np.pi*a),'r--')

plt.xlabel('横轴：时间',fontproperties='SimHei',fontsize=15,color='green')
plt.ylabel('纵轴：振幅',fontproperties='SimHei',fontsize=15)
plt.title(r'正弦波实例 $y=cos(2\pi x)$',fontproperties='SimHei',fontsize=25)  # 使用Latex语法
plt.text(2,1,r'$\mu=100$',fontsize=15)  # 规定文本显示在横轴为2，纵轴为1的位置上

plt.axis([-1,6,-2,2])
plt.grid(True)  # 加入网格
plt.show()
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210723102027009.png?token=AONRX2QZUV4NUYEAIL555KDCV3TPA)

`plt.annotate(s,xy=arrow_crd,xytext=text_crd,arrowprops=dict)`是注释函数

+ s：注释的文本
+ xy：箭头显示位置
+ xytext：文本显示位置
+ arrowprops：字典类型，定义整个箭头显示的属性

```python
import matplotlib.pyplot as plt
import numpy as np

a = np.arange(0.0,5.0,0.02)
plt.plot(a,np.cos(2*np.pi*a),'r--')

plt.xlabel('横轴：时间',fontproperties='SimHei',fontsize=15,color='green')
plt.ylabel('纵轴：振幅',fontproperties='SimHei',fontsize=15)
plt.title(r'正弦波实例 $y=cos(2\pi x)$',fontproperties='SimHei',fontsize=25)
plt.annotate(r'$\mu=100$', xy=(2,1), xytext=(3,1.5), 
             arrowprops=dict(facecolor='black',shrink=0.1,width=2)) # shrink规定比例因子，给箭头两侧留白

plt.axis([-1,6,-2,2])
plt.grid(True)
plt.show()
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210723105054971.png?token=AONRX2UCUAXBUC7WTG744ATCV3TQ2)

### pyplot的子绘图区域

`pyplot.subplot`函数只能将一块绘图区域分割为规则的子绘图区域，但在实际应用中，我们希望可以划分不规则的区域，所以就有了`plt.subplot2grid()`函数，这个函数辅助`plt.subplot()`函数划分绘图区域。

`plt.subplot2grid(GridSpec,CurSpec,colspan=1,rowspan=1)`

设计理念：设定网格，选中网格，确定选中行列区域数量，编号从0开始。

+ GridSpec：划分网格为几块区域
+ CurSpec：选择网格的第几行几列
+ colspan和rowspan：确定选择网格的横向和纵向的延伸数量。

```python
import matplotlib.pyplot as plt

plt.subplot2grid((3,3), (0,0), colspan=3)
...
plt.subplot2grid((3,3), (1,0), colspan=2)
...
plt.subplot2grid((3,3), (1,2), rowspan=2)
...
plt.subplot2grid((3,3), (2,0))
...
plt.subplot2grid((3,3), (2,1))
...
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210723110722972.png?token=AONRX2WJ2CB2E3FBCM4A6ZLCV3TSY)

使用subplot2grid函数固然可以划出不规则区域，但每次都要在选择子绘图区域时，都要确定整个绘图区域（例子中的第一个参数），所以我们可以使用GridSpec类和subplot函数来规定整体绘图区域。

```python
import matplotlib.pyplot as plt
import matplotlib.gridspec as gridspec

gs=gridspec.GridSpec(3, 3)  # 划分一个3x3网格

ax1=plt.subplot(gs[0,:])  # 先规定行，再规定l
ax2=plt.subplot(gs[1,:-1])
ax3=plt.subplot(gs[1:,-1])
ax4=plt.subplot(gs[2,0])
ax5=plt.subplot(gs[2,1])
```

![](https://raw.githubusercontent.com/cfx2020/image/main/image-20210723112623176.png?token=AONRX2W7REK27SJNTPPWURDCV3TUA)

## 关键

不可能掌握每一种画图方法，要根据数据选取恰当的图形展示数据含义，然后通过文档来绘图。