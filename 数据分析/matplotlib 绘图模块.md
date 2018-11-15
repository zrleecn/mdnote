# 入门

## 小小案例

绘画出一天当中的温度变化图
```python
from matplotlib import pyplot as plt

# 显示中文
plt.rcParams[u'font.sans-serif'] = ['simhei']
x = range(2, 26, 2)
y = [15, 13, 14, 5, 17, 20, 25, 26, 24, 22, 18, 15]

# 设置图片大小
plt.figure(figsize=(10,7), dpi=80)

# 调整y轴的刻度
plt.yticks(range(min(y), max(y)))

# 调整x轴的刻度
_x = [] 
for i in x:
    _x.append(str(i) + "h")
plt.xticks(range(2,26,2), _x)

# xy轴标签
plt.xlabel("时间")
plt.ylabel("温度℃ ")
# 设置标题
plt.title("matplotlib test")
# 绘图
plt.plot(x, y)
# 保存图片
# plt.savefig('./fig1.svg')
# plt.grid(alpha=0.5) 网格 0.5透明度
plt.show()
```
- plot() 绘图
- xticks() x走刻度
- ytikes() y轴刻度
- title() 标题
- xlabel() x轴标签
- ylabel() y轴标签
- show() 显示图片
- savefig('./pic.svg') 保存图片 
- grid(appha=0.5)  网格 appha=0.5 透明度
- legend() 添加图例
- figure(figsize=(10,7), dpi=80) 设置图片大小

## 添加信息


```python
from matplotlib import pyplot as plt
import random
x = range(10)
y1 = [random.randint(1,10) for i in range(10) ]
y2 =  [random.randint(1,10) for i in range(10) ]

# label是添加图例的时候显示的值
plt.plot(x, y1, label="y1", color="orange")
plt.plot(x, y2, label="y2", color="cyan")
# 添加图例

# 添加x轴标签
plt.xlabel("x")
plt.ylabel("y")
plt.title("title")

plt.legend()
plt.show()

```
- plot()函数
```python
plt.plot(
    x,
    y,
    color='r', # 线条颜色 可以是十六进制 也可以是red blue 等这些
    linewidth=5, # 线条粗细
    alpha=0.5,  # 透明度
    linestyle=':' # 线条风格, ':'虚线, '-'实线, '--'虚线，'-.'点划线
    label='string' 结合legend图例使用

)
```

## 常见的统计图

### 散点图

```python
from matplotlib import pyplot as plt
import random
x = range(20)
y = [random.randint(10,20) for i in range(20)]

plt.scatter(x, y)
plt.show()

```

函数说明
- x：指定散点图的x轴数据；
- y：指定散点图的y轴数据；
- s：指定散点图点的大小，默认为20，通过传入新的变量，实现气泡图的绘制；
- c：指定散点图点的颜色，默认为蓝色；
- marker：指定散点图点的形状，默认为圆形；
- cmap：指定色图，只有当c参数是一个浮点型的数组的时候才起作用；
- norm：设置数据亮度，标准化到0~1之间，使用该参数仍需要c为浮点型的数组；
- vmin、vmax：亮度设置，与norm类似，如果使用了norm则该参数无效；
- alpha：设置散点的透明度；
- linewidths：设置散点边界线的宽度；
- edgecolors：设置散点边界线的颜色；

### 条形图

#### 垂直条形图bar()
bar函数完成条形图的绘制
案例
中国的四个直辖市分别为北京市、上海市、天津市和重庆市，其2017年上半年的GDP分别为12406.8亿、13908.57亿、9386.87亿、9143.64亿。对于这样一组数据，我们该如何使用条形图来展示各自的GDP水平呢？
​    from matplotlib import pyplot as plt

```python
# 构建数据
gdp = [12406.8,13908.57,9386.87,9143.64]
citys = ['北京市', '上海市', '天津市', '重庆市']
# 中文乱码处理
plt.rcParams['font.sans-serif'] = ['simhei']

# 绘图
plt.bar(range(len(gdp)), gdp, align='center',width=0.8, color='cyan', alpha=0.8)

# 添加标签
plt.xlabel('城市')
plt.ylabel('GDP')
# 添加刻度
plt.xticks(range(len(gdp)), citys )

# 设置y轴的刻度范围
plt.ylim([5000, 15000])
# 每个条形图添加数值标签
for i in range(len(gdp)):
    plt.text(i, gdp[i]+100, str(round(gdp[i], 1)), ha='center' )
plt.plot()
```

![](http://libs.zrlee.cn/image/2dc2c910-df26-11e8-9f32-f2801f1b9fd1.png)
#### 水平条形图 barh()


```python
from matplotlib import pyplot as plt

# 构建数据
price = [30.5,39.9,47.4,35.9,40.34]
shop = ['亚马逊','当当网','中国图书网','京东','天猫']
# 中文乱码处理
plt.rcParams['font.sans-serif'] = ['simhei']

plt.barh(range(len(price)), price, align='center', height=0.5)

plt.xlabel('价格')
plt.ylabel('平台')
# 添加刻度
plt.yticks(range(len(shop)), shop)
plt.xlim([28, 50])
# 绘图



# 每个条形图添加数值标签
for i in range(len(price)):
    plt.text(price[i]+0.8, i, str(round(price[i], 1)), ha='center' )

plt.plot()
plt.show()

```
![](http://libs.zrlee.cn/image/c6737944-df25-11e8-9f32-f2801f1b9fd1.png)




#### 绘制多个条形图
```python
from matplotlib import pyplot as plt
import random
plt.rcParams['font.sans-serif'] = ['simhei']

y1 = [i*random.randint(1,15) for i in range(1,5)]
y2 = [i*random.randint(1,15) for i in range(1,5)]

x1 = [i for i in range(1,5)]
x2 = [i+0.3 for i in range(1,5)]
# x刻度
plt.xticks([i+0.1 for i in range(1,5)], ["2014", "2015", '2016', '2017'])

plt.bar(x1, y1, width=0.3, label='男生')
plt.bar(x2, y2, width=0.3, label='女生')

plt.legend()
plt.show()

```


![](http://libs.zrlee.cn/image/Figure_1.png)
