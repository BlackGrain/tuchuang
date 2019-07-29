

matplotlib的基本使用——学习笔记
---------

#### 1、matplotlib简介

​	[matplotlib](https://matplotlib.org/)是Python最流行的底层绘图库，主要做数据可视化图表，名字取材于MATLAB[^①]，模仿MATLAB构建。

#### 2、基本使用

* 导入
  
* ` from matplotlib import pyplot as plt `
  
* 绘图 

  * 折线图 
  * `plt.plot(x, y)`
  * 散点图
  * `plt.scatter(x, y)`
  * 条形图
  * `plt.bar(x, y, width=0.2, color="orange")`
  * 直方图
    * `bin_width = 3 `	#定义组距
    * `num_bins = int(max(a) - min(a)) / bin_width`  #组数
    * `plt.hist(a, num_bins)`   #绘图
  
  * 显示图案
    * `plot.show()`

>  **☞小例子2.1** 
>
> ```python
> from matplotlib import pyplot as plt
> x = range(2, 26, 2)
> y = [12, 13, 15, 17, 19, 20, 23, 20, 16, 13, 10, 9]
> plt.plot(x, y)
> plt.show()
> ```
>
> ![plt.plot](https://github.com/BlackGrain/tuchuang/blob/master/Matplotlib/plt.plot.png?raw=true)
>
> 用plot绘图很简单，点位置与对应x y相同索引的坐标位置，例中即为(2, 12), (4, 13), (6, 15), (8, 17)…..

#### 3、设置图像大小

* `fig = plt.figure(figsize=(20, 8), dpi=80)` 由此设置的图片大为（20\*80）\*（8*80）像素，即`1600`\*`640`像素

#### 4、调整x轴或y轴的刻度分布

* `plt.xticks(x)`设置x的刻度
* `plt.xticks(x[::2])`当刻度较为密集的时候开业使用步长取较为稀疏的刻度
  * `plt.xticks(x, _x, rotation=45)`参数`x`表示刻度，参数`_x`表示与刻度对应的标记字符串，参数`rotation`表示标记字符串的旋转角度。`x` ` _x`长度一致，互相对应。当`_x`缺失时，坐标轴标记即显示刻度。

> ** ☞小例子4.1 **
>
> ```python
> from matplotlib import pyplot as plt
> x = range(2, 26, 2)
> y = [12, 13, 15, 17, 19, 20, 23, 20, 16, 13, 10, 9]
> _x = ['{}:00时'.format(i) for i in x]
> plt.xticks(x, _x, rotation = 45)
> plt.plot(x, y)
> plt.show()
> ```
>
> ![ x.xticks](https://github.com/BlackGrain/tuchuang/blob/master/Matplotlib/plt.xticks.png?raw=true)
>
> 假如我们想要x轴的刻度更稀疏一些，我们可以这样做:
>
> * `plt.xticks(x[::2], _x[::2], rotation = 45)`取步长为2，注意x与_x参数一一对应
>
> 得到的结果为：
>
> ![步长为2](https://github.com/BlackGrain/tuchuang/blob/master/Matplotlib/plt.xticks.%5B%EF%BC%9A%EF%BC%9A2%5D.png?raw=true)
>
> 这样就大功告成啦！不过，我们还会发现一个小问题，我们的_x字符标签中的中文字"时"并没有正常显示,这是因为matplotlib默认不支持中文字符。设置中文显示方法中文请往下看。	

#### 5、设置中文显示

* 通过matplotlib 下的font_manager解决(windows/linux/mac)
  * `from matplotlib import font_manager`导入font_manager模块
  * `my_font = font_manger.FontProperties(fname="/System/Library/Fonts/PingFang.ttc")`实例化FontProperties，其中参数fname="字体目录"：
    * `Mac os`下的系统字体目录为：`/System/Library/Fonts/`
    * `Linux`下的系统字体目录为：`/usr/share/fonts`
    * `Windows`下的系统字体目录为：`C:\WINDOWS\Fonts`
    * 当然，我们也可以直接把字体文件放在工作区目录中使用，方便且通用。
  * 在需要使用中文的函数中添加参数`fontproperties=my_font`,如：
    * `plt.xticks(x, _x, rotation = 45, fontproperties=my_font)`
    * 此外，有一特例，图例函数`lengend()`中，需要添加参数为`prop=my_font`

> **☞小例子5.1**
>
> ```python
> from matplotlib import pyplot as plt
> from matplotlib import font_manager
> #实例化FontProperties
> my_font = font_manager.FontProperties(fname="/System/Library/Fonts/PingFang.ttc")
> x = range(2, 26, 2)
> y = [12, 13, 15, 17, 19, 20, 23, 20, 16, 13, 10, 9]
> _x = ['{}:00时'.format(i) for i in x]
> plt.xticks(x, _x, rotation = 45, fontproperties=my_font)
> plt.plot(x, y)
> plt.show()
> ```
>
> ![!中文显示](https://github.com/BlackGrain/tuchuang/blob/master/Matplotlib/%E4%B8%AD%E6%96%87%E6%98%BE%E7%A4%BA.png?raw=true)

#### 6、为轴添加描述信息

* `plt.xlabel("时间", fontproperties=my_font)` #设置x轴的label

* `plt.ylabel("温度", fontproperties=my_font)`#设置y轴的label

* `plt.title("2时到24时温度的变化情况", fontproperties=my_font)`#设置图片标题

  在`小例子5.1`中添加以上两条代码后，图像显示如下图：

  ![轴添加描述信息](https://github.com/BlackGrain/tuchuang/blob/master/Matplotlib/%E8%BD%B4%E7%9A%84%E6%8F%8F%E8%BF%B0%E4%BF%A1%E6%81%AF.png?raw=true)

#### 7、自定义绘制图形的风格

* `plt.plot(x, y, color ='r', linestyle='--', linewidth=5, alpha=0.5)`

  * `color='r'`	#线条颜色

  * `linestyle='--'`    #线条样式

  * `linewidth=5 `   #线条宽度

  * `alpha=0.5`    #透明度

    | 颜色字符`color`   | 风格字符`linestyle` |
    | :---------------- | :------------------ |
    | `r`红色           | `-`实线             |
    | `g`绿色           | `—`虚线 破折线      |
    | `b`蓝色           | `-.`点划线          |
    | `w`白色           | `:`点虚线           |
    |                   | `''`留空            |
    | `c`青色           |                     |
    | `m`洋红           |                     |
    | `y`黄色           |                     |
    | `k`黑色           |                     |
    |                   |                     |
    | `00ff00`16进制    |                     |
    | `0.8`灰度值字符串 |                     |

#### 8、图例的使用

当我们需要对多个图形进行对比时，我们会在一张图像中绘制多个图形。为了更明显地展现对比，我们需要对不同图形添加不同的图例。

* `plt.plot(x,  y, label="label") `    #在`plt.plot`中添加参数`label="label"`
* `plt.legend(prop=my_font, loc="best")`   #参数`prop=my_font`定义中文字符,参数`loc`定义图例的生成位置，具体请见matplotlib源码注释。

> **☞小例子**
>
>```python
>from matplotlib import pyplot as plt
>from matplotlib import font_manager
>my_font = font_manager.FontProperties(fname="/System/Library/Fonts/PingFang.ttc")
>
>x = range(2, 26, 2)
>y_summer = [20, 21, 23, 24, 27, 30, 34, 30, 25, 23, 21, 19]
>y_spring = [12, 13, 15, 17, 19, 20, 23, 20, 16, 13, 10, 9]
>
>plt.xlabel("时间", fontproperties=my_font)
>plt.ylabel("温度", fontproperties=my_font)
>plt.title("春、夏季2时到24时温度的变化情况", fontproperties=my_font)
>
>plt.plot(x, y_summer, label="夏天", linestyle='-', alpha=0.7)
>plt.plot(x, y_spring, label="春天", linestyle='--', alpha=0.7)
>
>plt.legend(prop=my_font, loc="best")
>
>plt.show()
>```
>
>![对比图](https://github.com/BlackGrain/tuchuang/blob/master/Matplotlib/%E5%A4%8F%E5%A4%A9%E5%86%AC%E5%A4%A9%E5%AF%B9%E6%AF%94%E5%9B%BE.png?raw=true)

#### 9、折线图

* 以折线的上升或下降来表示统计数量的增减变化的统计图

* **特点:** 能够显示数据的变化趋势，反映事物的变化情况。(变化)

  ![折线图](https://github.com/BlackGrain/tuchuang/blob/master/Matplotlib/%E6%8A%98%E7%BA%BF%E5%9B%BE.png?raw=true)

* `plt.plot()`以上案例都用`plot`，以下不做赘述

#### 10、散点图

* 用两组数据构成多个坐标点，考察坐标点的分布,判断两变量之间是否存在某种关联或总结坐标点的分布模式。
* **特点:** 判断变量之间是否存在数量关联趋势,展示离群点(分布规律)
* 方法:`plt.scatter(x, y)`

> **☞小例子10.1**
>
>```python
>from matplotlib import pyplot as plt
>from matplotlib import font_manager
>
>my_font = font_manager.FontProperties(fname="/System/Library/Fonts/PingFang.ttc")
>
># x坐标
>x_3 = list(range(1, 32))
>x_9 = list(range(35, 66))
>
># x轴标签
>x_3_ticks = ["三月{}日".format(i) for i in range(1, 32)]
>x_9_ticks = ["十月{}日".format(i) for i in range(1, 32)]
>
># y轴坐标
>y_3 = [11,17,16,11,12,11,12,6,6,7,8,9,12,15,14,17,18,21,16,17,20,14,15,15,15,19,21,22,22,22,23]
>y_9 = [26,26,28,19,21,17,16,19,18,20,20,19,22,23,17,20,21,20,22,15,11,15,5,13,17,10,11,13,12,13,6]
>
># x轴
>x_ticks = x_3_ticks + x_9_ticks
>x = x_3 + x_9
># y轴
>y = y_3 + y_9
>
>#图像大小
>fig = plt.figure(figsize=(10, 4), dpi=80)
>
># 刻度
>plt.xticks(x[::3], x_ticks[::3], rotation=45, fontproperties=my_font)
>
># 描述
>plt.xlabel("时间", fontproperties=my_font)
>plt.ylabel("天最高温度", fontproperties=my_font)
>plt.title("北京市三月份、十月份每日最高温度散点图", fontproperties=my_font)
>
># 绘制散点图
>plt.scatter(x_3, y_3, label="三月")
>plt.scatter(x_9, y_9, label="十月")
># 图例
>plt.legend(prop=my_font, loc="best")
>
>plt.show()
>```
>
>![](https://github.com/BlackGrain/tuchuang/blob/master/Matplotlib/%E5%A4%A9%E6%B0%94%E6%95%A3%E7%82%B9%E5%9B%BE.png?raw=true)

#### 11、条形图

* 排列在工作表的列或行中的数据可以绘制到条形图中。
* **特点:** 绘制连离散的数据,能够一眼看出各个数据的大小,比较数据之间的差别。
* 方法:plt.bar(x, y, width = , color = ）

> **☞小例子11.1**
>
>```python
>from matplotlib import pyplot as plt
>from matplotlib import font_manager
>
>my_font = font_manager.FontProperties(fname = "/System/Library/Fonts/PingFang.ttc")
>
>a = ["战狼2","速度与激情8","功夫瑜伽","西游伏妖篇","变形金刚5：最后的骑士","摔跤吧！爸爸",
>     "加勒比海盗5：死无对证","金刚：骷髅岛","极限特工：终极回归","生化危机6：终章","乘风破浪",
>     "神偷奶爸3","智取威虎山","大闹天竺","金刚狼3：殊死一战","蜘蛛侠：英雄归来","悟空传",
>     "银河护卫队2","情圣","新木乃伊",]
>
>b=[56.01,26.94,17.53,16.49,15.45,12.96,11.8,11.61,11.28,11.12,10.49,
>   10.3,8.75,7.55,7.32,6.99,6.88,6.86,6.58,6.23]
>
>x_ = range(len(a))
>y_ = b
>
># 图像大小
>fig = plt.figure(figsize=(20,8), dpi=80)
>
># 绘图
>plt.bar(x_, y_, width = 0.3, color = "C")
>
># 标签
>plt.xticks(x_, a, fontproperties=my_font, rotation=45)
>plt.xlabel("电影", fontproperties=my_font)
>plt.ylabel("票房（亿）", fontproperties=my_font)
>plt.title("票房前十排行", fontproperties=my_font)
>
>plt.show()
>```
>
>![](https://github.com/BlackGrain/tuchuang/blob/master/Matplotlib/%E7%94%B5%E5%BD%B1%E7%A5%A8%E6%88%BF.png?raw=true)

#### 12、直方图

* 由一系列高度不等的纵向条纹或线段表示数据分布的情况。 一般用横轴表示数据范围，纵轴表示分布情况。
* **特点：** 绘制连续性的数据,展示一组或者多组数据的分布状况(统计)
* 方法：
  * `bin_width = 3`#设置组距
  * `num_bins = int((max(a) - min(a))/bin_width)`#分为多少组
  * `plt.hist(a, num_bins)`#绘图，如果有参数`normed=1`则按频率分布绘制
  * `plt.xticks(list(range(min(a),max(a)))[::bin_width], rotation=45)`#设置标签
  * `plt.grid(linestyle="-.", alpha=0.5)`#显示网格

>☞小例子12.1
>
>```python
>from matplotlib import pyplot as plt
>from matplotlib import font_manager
>
>my_font = font_manager.FontProperties(fname = "/System/Library/Fonts/PingFang.ttc")
>
>a=[131,  98, 125, 131, 124, 139, 131, 117, 128, 108, 135, 138, 131, 102, 107, 114, 119, 128, 121, 142, 
>   127, 130, 124, 101, 110, 116, 117, 110, 128, 128, 115,  99, 136, 126, 134,  95, 138, 117, 111,78, 
>   132, 124, 113, 150, 110, 117,  86,  95, 144, 105, 126, 130,126, 130, 126, 116, 123, 106, 112, 138, 
>   123,  86, 101,  99, 136,123, 117, 119, 105, 137, 123, 128, 125, 104, 109, 134, 125, 127,105, 120, 
>   107, 129, 116, 108, 132, 103, 136, 118, 102, 120, 114,105, 115, 132, 145, 119, 121, 112, 139, 125, 
>   138, 109, 132, 134,156, 106, 117, 127, 144, 139, 139, 119, 140,  83, 110, 102,123,107, 143, 115, 136, 
>   118, 139, 123, 112, 118, 125, 109, 119, 133,112, 114, 122, 109, 106, 123, 116, 131, 127, 115, 118, 112, 
>   135,115, 146, 137, 116, 103, 144,  83, 123, 111, 110, 111, 100, 154,136, 100, 118, 119, 133, 134, 106, 129, 
>   126, 110, 111, 109, 141,120, 117, 106, 149, 122, 122, 110, 118, 127, 121, 114, 125, 126,114, 140, 103, 130, 
>   141, 117, 106, 114, 121, 114, 133, 137,  92,121, 112, 146,  97, 137, 105,  98, 117, 112,  81,  97, 139, 113,
>   134, 106, 144, 110, 137, 137, 111, 104, 117, 100, 111, 101, 110,105, 129, 137, 112, 120, 113, 133, 112,  83,  
>   94, 146, 133, 101,131, 116, 111,  84, 137, 115, 122, 106, 144, 109, 123, 116, 111,111, 133, 150]
>
># 图像大小
>fig = plt.figure(figsize=(20, 8), dpi=80)
>
>#设置组距
>bin_width = 3
>num_bins = int((max(a) - min(a))/bin_width) 
>
>#绘图，如果有参数`normed=1`则按频率分布绘制
>plt.hist(a, num_bins)
>
>#设置标签
>plt.xticks(list(range(min(a),max(a)))[::bin_width], rotation=45)
>
>#显示网格
>plt.grid(linestyle="-.", alpha=0.5) 
>plt.show()
>```
>
>![](https://github.com/BlackGrain/tuchuang/blob/master/Matplotlib/%E7%94%B5%E5%BD%B1%E5%B8%82%E5%9C%BA%E5%88%86%E5%B8%83.png?raw=true)

--------------

>补充：多子图
>
>```python
>fig, ax = plt.subplots(2, 3, sharex='col', sharey='row')
>for i in range(2):
>    for j in range(3):
>        ax[i, j].text(0.5, 0.5, str((i, j)),fontsize=18, ha='center')
>```

[^ ①]: MATLAB 是美国[MathWorks](https://baike.baidu.com/item/MathWorks)公司出品的商业[数学软件](https://baike.baidu.com/item/数学软件)，用于算法开发、数据可视化、数据分析以及[数值计算](https://baike.baidu.com/item/数值计算/3729797)的高级技术计算语言和交互式环境，主要包括MATLAB和Simulink两大部分。


