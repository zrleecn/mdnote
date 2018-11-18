# 环境查看

1. 查看支持中文的系统文字

```shell
fc-list :lang=zh
```

2. Python版本及matplotlib配置文件位置查询

```python
$ python
Python 3.6.7 (default, Oct 22 2018, 11:32:17) 
[GCC 8.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import matplotlib 
>>> matplotlib.matplotlib_fname()
'/usr/local/lib/python3.6/dist-packages/matplotlib/mpl-data/matplotlibrc'



```

# 第一种方法

代码中指定文字字体

```python
from matplotlib import font_manager

# fname 参数跟上上面 fc-list :lang=zh 列表中选择其中一个即可
font = font_manager.FontProperties(fname='/usr/share/fonts/opentype/noto/NotoSansCJK-Medium.ttc')

# 使用中文的地方设定字体
plt.xlabel('城市', fontproperties=font)
```

## windows 上

```python
plt.rcParams['font.sans-serif']=['SimHei'] #用来正常显示中文标签
plt.rcParams['axes.unicode_minus']=False #用来正常显示负号
```

