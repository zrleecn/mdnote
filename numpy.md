# 什么是NumPy

一个在Python中做科学计算的基础库，重在数值计算，也是大部分Python科学计算库的基础库，多用于大型、多维数组上执行数值运算。

# 安装
```
pip install numpy
```
# 使用

## 创建数组

```python
import numpy as np
import random
t1 = np.array([1,2,3])
print(t1)
print(type(t1))
t2 = np.array(range(10))
print(t2)
t3 = np.arange(10)
print(t3)
t4 = np.arange(4,10,2)  # 步长为2
print(t4)
print(t4.dtype)

# 指定创建的书的数据类型
a = np.array([1,0,1,1], dtype=np.bool)
print(a)

# 修改数组的数据类型
a1 = a.astype(np.int8)
print(a1)
print(a1.dtype)

a2 = [random.random()*random.random() for i in range(10)]

a3 = np.array(list(a2))
print(a3)
# 四舍五入 保留两位小数点
print(np.round(a3,2))
```
-  np.astype(np.int16) 修改数据类型


## NumPy - 数组属性


- shape 数组的形状
- reshape 

```
import numpy as np
import random

# shape属性 数组的形状
a1 = np.arange(12)
print(a1.shape)  # （5,）

a2 = np.array([
		[1,2,3],
		[4,5,6]
	])

print(a2.shape)  # (2,3)

a4 = a1.reshape(3,4)
print(a4)
print(a4.shape)
```

- flatten() 二维数组 转为一维数组

```python
import numpy as np
import random

a1 = np.arange(24)
print(a1)
# 二维数组4行6列
a2 = a1.reshape(4,6)
print(a2)

# 转成一维数组的方法
# 第一种
a3 = a2.reshape((24,))
print(a3)
# 或者是统计出来数组元素的个数
a4 = a2.reshape((a2.shape[0]*a2.shape[1],))
print(a4)
# 利用flatten()
a5 = a2.flatten()
print(a5)

```
- ndarray.ndim 返回数组的维度

```python
import numpy as np
import random

a1 = np.arange(24)
print("a1的维度=%s" % a1.ndim)
a2 = a1.reshape(4,6)
print("a2的维度=%s" % a2.ndim)
```



## 数组计算

### 广播

```python
import numpy as np
import random

a1 = np.arange(24)
print(a1)
# 所有元素都会加2
print(a1+2)

a2 = np.array([1,2,3,4])
a3 = np.array([1,2,3,4])
a4 = a2 * a3
print(a4)
print("a5=======================")
a5 = a1.reshape(6,4)
print(a5)
print(a5*a2)

print("a7=======================")
a7 = np.arange(6)
a7 = a7.reshape(6,1)
print(a7)

print(a5 + a7)


```


## NumPy 读取数据


```
np.loadtxt(frame, dtype=np.float, delimiter=None, skiprows=0,usecols=None, unpack=False)
```

| 参数      | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| frame     | 文件、字符串或者生成器可以是.gz或者bz2压缩文件               |
| dtype     | 数据的类型 默认float                                         |
| delimiter | 分隔符 默认是任何空格， 改为逗号                             |
| skiprows  | 跳过前n行 一般跳过第一行表头                                 |
| usecols   | 读取指定的列，索引，元祖类型                                 |
| unpack    | 如果是True 读入属性分别写入不同数组变量，False读入数组只写入一个数组变量，默认是False |


data.csv

```python
100,239,123,444
123,44,3,23
345,256,213,77
98,67,334,123
```

读取例子
```python
import numpy as np
import random

a = np.loadtxt('./data.csv', dtype=np.int16, delimiter=',', skiprows=0,usecols=None, unpack=False)

# unpack=True
b = np.loadtxt('./data.csv', dtype=np.int16, delimiter=',', skiprows=0,usecols=None, unpack=True)
print(a)
print(b)  # 行变列 列变行 相当于转置
```
csv是逗号分隔的 所以 delimiter参数设置成 ","


## Numpy 数组转置


```python
import numpy as np
import random

a = np.arange(24).reshape(4,6)
print(a)
print("="*30)
# 转置的三种方法 1
print(a.transpose())
print("="*30)
# 2
print(a.T)
print("="*30)
# 3
print(a.swapaxes(1,0))

```

## NumPy 索引切片


```python
import numpy as np
import random
# 二维数组
a = np.arange(24).reshape(4,6)
print(a)
print("=====================")
# 取第一行
print("第一行:\n%s" % str(a[0]))

# 连续的几行
print("第0~1行:\n%s" % str(a[0:2]))

print("第0,2行:\n%s" % str(a[0::2]))
print("=====================")
# 取列 逗号前面表示行 后面表示列 ：表示取所有的行
print("第2列\n %s" % str(a[:,1]))
print("第2,3列\n %s" % str(a[:,1:3]))
print("第2列，2，3行\n %s" % str(a[1:3,1]))


```

## Numpy 数值修改

```python
import numpy as np
import random
# 二维数组
a = np.arange(24).reshape(4,6)
print(a)
print("=====================")

# 修改
a[:,0]=0  # 第一列改为0
print(a)

# print(a[a==0])

# 把数值等于0的改为10
print("\n0改为10")
a[a==0] = 10
print(a)

# 三元运算符 where(condition,value1, value2)
print("\n把大于10的改为0 小于10的改为4")
print(np.where(a>10, 0 , 4))  # 把大于10的改为0 小于10的改为4
```

## 数组的拼接

```python
import numpy as np
import random
# 二维数组
a = np.arange(12).reshape(2,6)
b = np.arange(12,24).reshape(2,6)
print(a)
print(b)
print("=====================")
# vstack((a,b)) 传入一个元祖
# 垂直拼接
print(np.vstack((a,b)))

# hstack((a,b))  水平拼接
print(np.hstack((a,b)))

```

## 交换数组的行列


```
import numpy as np
import random
# 二维数组
a = np.arange(24).reshape(4,6)

print(a)
print("="*10)
# 1,2 两行分别互换
a[[1,2],:]=a[[2,1],:]
print(a)
print("="*10)
# 1,2列互换
a[:,[1,2]] = a[:,[2,1]]
print(a)

```

## Numpy 其他方法
- 获取最大值最小值的位置
  - np.argmax(a, axis=0)
  - np.argmin(a, axis=1)
    axis指定哪个轴
- 创建一个全0的数组
  - np.zores((3,4))

- 创建一个全1的数组
  - np.ones((3,4))
- 创建一个对角线为1的方阵 （单位矩阵）
  - np.eye(3)

```python
import numpy as np
# 随机矩阵
a = np.random.randint(1,20,(3,4)) 
print(a)

# 找出每一列中最大值的位置
print("列最大位置")
print(np.argmax(a, axis=0))
print("行最大位置")
# 找出每一行中最大值的位置
print(np.argmax(a, axis=1))

# 生成全0的数组
np.zeros((3,4))
# 全1 数组
np.ones((3,4))
# 单位矩阵
np.eye(3)

```
![](http://libs.zrlee.cn/image/22a1f01c-e005-11e8-9f32-f2801f1b9fd1.png)

## Numpy 生成随机数组

| 函数                                   | 说明                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| np.random.rand(d0,d1,dn)               | 创建d0-dn维度的均匀分布随机数组浮点数 范围从0-1              |
| np.random.randn(d0,d1,dn)              | 创建d0-d维度的标准正态分布随机数组，浮点数平均值0 标准差1    |
| np.random.randint(low, hight, (shape)) | 从给定上下限范围选取随机整数                                 |
| np.random.uniform(low, hight,(size))   | 产生具有均匀分布的数组                                       |
| np.random.normal(loc, scale, (size)    | 从指定的正态分布中随机抽取样本，分布中心是loc 标准差是scale 形状是size |
| np.random.seed(s)                      | 随机种子，s是给定的种子值， 计算机生成的是伪随机数，给定相同的种子后每次生成的随机数都是一样的 |
![](http://libs.zrlee.cn/image/bccc9de8-e007-11e8-9f32-f2801f1b9fd1.png)

## Numpy 的注意点 copy和view

- a=b 完全不复制 a和b互相影响
- a=b[:] 视图操作， 一种切片，会创建新的对象a 但a的数据完全由b保管 他们两个的数据变化是一致的
- a = b.copy()复制， a和b互不影响
  ![](http://libs.zrlee.cn/image/e9ae3230-e008-11e8-9f32-f2801f1b9fd1.png)

## Numpy nan的注意点

- 两个nan不相等
- nan和任何数值计算都是nan

可以通过特性统计数组中nan的个数
判断是否为nan的方法 `np.isnan(array)`
![](http://libs.zrlee.cn/image/35c7711c-e00a-11e8-9f32-f2801f1b9fd1.png)
![](http://libs.zrlee.cn/image/de6ec6f8-e00a-11e8-9f32-f2801f1b9fd1.png)

封装一个函数 使数组中的nan改为0

```python
import numpy as np


def change_nan(a):
	for i in range(a.shape[1]):
		# 当前列
		temp_col = a[:,i] # current_col
		nan_num = np.count_nonzero(temp_col!=temp_col)
		if nan_num != 0 :
			temp_col[np.isnan(temp_col)] = 0

	return a



a = np.array([
	[1,3,6,11,23],
	[np.nan, 23, 45,66,12],
	[3, 5,np.nan, 4, 6]

	], dtype=np.float)
print(a)
print(change_nan(a))
```

- count_nonzero()

统计a数组nan的个数 np.count_nonzero(a!=a)

统计a数组数值等于5的个数 np.count_nonzero(a==5)


## Numpy 中常用的统计函数
- 求和 a.sum(axis=None)
- 均值 a.mean( axis=None)
- 中值 a.median(axis=None)
- 最大值a.max(axis=None)
- 最小值 a.min(axis=None)
- 极值 a.ptp(axis=None)
- 标准差 a.std(axis=None)
  ![](http://libs.zrlee.cn/image/2cec423c-e00c-11e8-9f32-f2801f1b9fd1.png)