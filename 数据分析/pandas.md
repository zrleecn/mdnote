# 安装

```
pip install pandas
```


# 使用
## pandas常用的数据类型

### Series 一维数组

- series 一维数组 带标签数组
- DataFrame 二维 series容器


```python
import pandas as pd


# 创建一个series数组
a = pd.Series([3,2,4,8])
print(a)
# 设置索引
a = pd.Series([1,2,3,4], index=list("abcd"))
print(a)
# 字段作为参数 键作为索引 
a = pd.Series({"name":"zrlee", "age":"20"})
print(a)

```
#### 切片和索引

例子

```python
import pandas as pd

# 字段作为参数 键作为索引 
a = pd.Series({"name":"zrlee", "age":"20"})

# 通过索引获取数据
print("通过索引")
print(a['name'])
# 通过位置获取
print("通过行位置获取")
print(a[1])
# 取多个
print("取多个")
print(a[ ["age","name"] ])

print("切片")
print(a[0:1])
```

- index 获取键
- values 获取值

```python
import pandas as pd

a = pd.Series(list("abcdef"), index=list("ABCDEF"))
print(a)

# 循环获取索引
for i in a.index:
	print(i)
# 索引列表
print(list(a.index))
# 值列表
print(list(a.values))
```

## 

### DataFrame二维数组

 #### 创建一个二维数组

```python
import pandas as np 
import numpy as np
import string
t = pd.DataFrame(np.arange(12).reshape(3,4))

# 同时设置索引
t = pd.DataFrame(np.arange(12).reshape(3,4), index=list(string.ascii_uppercase[:3]), columns=list(string.ascii_uppercase[-4:]))



```

两个结果

```python
   0  1   2   3
0  0  1   2   3
1  4  5   6   7
2  8  9  10  11

   W  X   Y   Z
A  0  1   2   3
B  4  5   6   7
C  8  9  10  11
```

#### 通过传入字典创建

```python
dic = {
    "name":['zrlee','marry'],
    "age": [20,23],
    "tel":[123,321]
}
pd.DataFrame(dic)

# 第二种
dic = [
    {"name":"zrlee", "age":20,"tel":123},
    {"name":"marry", "age":23,"tel":321},
]
pd.DataFrame(dic)

结果
    name  age  tel
0  zrlee   20  123
1  marry   23  321


```

#### DataFrame的基础属性

```python
df.shape  # 行数 列数
df.dtypes  # 列数据类型
df.ndim  # 数据维度
df.index  # 行索引
df.columns  # 列索引
df.values # 对象值 二维ndarray数组
```

#### DataFrame 整体情况查询

```python
df.head(3)  # 显示头部几行 默认5行
df.tail(3) # 显示尾部几行 默认5行
df.info()  # 相关信息概览 行数 列数 列索引，列非空值個數 列類型 行类型占用内存
df.describe() # 快速综合统计结果 计数 均值 标准差 最大值 四分位数 最小值
```

#### DataFrame 排序方法

```python
import pandas as pd

dic = [
	{"name":"zrlee", "score":80},
	{"name":"marry", "score":75},
	{"name":"tom", "score":83},
	{"name":"sally", "score":78}
]

df = pd.DataFrame(dic)
# 默认是升序
# df = df.sort_values(by="score")
# 设置为降序
df = df.sort_values(by="score", ascending=False)
print(df)
```



#### dataFrame的索引 切片 取行 取列

##### 通过标签索引loc

```python
import pandas as pd

dic = [
	{"name":"zrlee", "score":80 , "gender":"男"},
	{"name":"marry", "score":75, "gender":"女"},
	{"name":"tom", "score":83, "gender":"男"},
	{"name":"sally", "score":78, "gender":"男"}
]

df = pd.DataFrame(dic, index=list("abcd"))
# 取列
df["name"]  # 取出来的是Series的类型
# 前两行
df[:2]
# 前两行的 name列
df[:2]['name']
# 取a行的成绩(score)
df.loc["a", "score"]
# 取出一行
df.loc["a", :]
# 取一列 
df.loc[:, "name"]
# 多行多列
df.loc[["a", "b"]]
# 取name score 两列所有行
df.loc[:,["name", "score"]]
# a行的name score列
df.loc[["a"], ["name", "score"]]

```

##### 通过位置索引获取 iloc

```python
import pandas as pd

dic = [
	{"name":"zrlee", "score":80 , "gender":"男"},
	{"name":"marry", "score":75, "gender":"女"},
	{"name":"tom", "score":83, "gender":"男"},
	{"name":"sally", "score":78, "gender":"男"}
]

df = pd.DataFrame(dic, index=list("abcd"))
# 取前2行
df.iloc[:2]
# 取列第0 行
df.iloc[0]

df.iloc[2:4]
df.iloc[:, 0]
# 0 2行 0 1列
df.iloc[[0,2], [0,1]]
```

##### 布尔索引

```python
import pandas as pd

dic = [
	{"name":"zrlee", "score":80 , "gender":"男"},
	{"name":"marry", "score":75, "gender":"女"},
	{"name":"tom", "score":83, "gender":"男"},
	{"name":"sally", "score":78, "gender":"男"}
]

df = pd.DataFrame(dic, index=list("abcd"))
# 成绩大于等于80
df[df["score"]>=80]
# 成绩小于80的女生 & 并 | 或
df[(df["score"]<80)&(df["gender"]=="女")]
```

#### 字符串方法

| 方法                  | 说明                                                         |
| --------------------- | ------------------------------------------------------------ |
| cat                   | 实现元素级的字符串链接操作，可指定分隔符                     |
| contains *            | 返回表表示个字符串是否含有指定模式的布尔型数组               |
| count                 | 模式的出现次数                                               |
| endswith startwith    | 相当于对各个元素执行x.endswitch(pattern) 或x.startwith(pattern) |
| findall               | 计算各字符串的模式列表                                       |
| get                   | 获取各元素的第i各字符                                        |
| join                  | 根据指定的分隔符将Series中各元素的字符串连接起来             |
| lower upper *         | 转换大小写                                                   |
| match                 | 根据指定的正则表达式对各元素执行re.match                     |
| pad                   | 在字符串的左边 右边或者左右两边添加空白符                    |
| center                | 相当于pad(side="both")                                       |
| repeat                | 重复值                                                       |
| slice                 | 对Series中各个字符串进行子串截取                             |
| split *               | 根据分隔符或正则表达式对字符串进行拆分                       |
| strip、rstrip、lstrip | 去除空白字符 包括换行符                                      |
| len *                 | 计算字符串的长度                                             |

 ```python
import pandas as pd

dic = [
	{"name":"zrlee", "score":80 , "gender":"男"},
	{"name":"marry", "score":75, "gender":"女"},
	{"name":"tom", "score":83, "gender":"男"},
	{"name":"sally", "score":78, "gender":"男"}
]

df = pd.DataFrame(dic, index=list("abcd"))

print(df[df["name"].str.len()>3])

print(df["name"].str.endswith("ee"))
print(df["name"].str.contains("om"))
# 改成大写
df["name"] = df["name"].str.upper()
print(df)
 ```

###

## pandas 获取外部数据

### 从csv文本中读取
- pandas.read_csv()

data.csv

```python
name,age,job,sal
zrlee,20,program,15000
marry,20,test,15000
mark,20,sk,15000
```

读取方法

```python
import pandas as pd
df = pd.read_csv("./data.csv")
print(df)
```

输出

```python
    name  age      job    sal
0  zrlee   20  program  15000
1  marry   20     test  15000
2   mark   20       sk  15000
```

其他的读取方法
![image](http://libs.zrlee.cn/image/351f4ac2-81ef-4a6e-9932-003d54073b26.png)

### 从mongodb中读取

```python
import pandas as pd
import pymongo

# 创建客户端连接对象
client = MongoClient()
# 操作表
collection = client['db_name']['collection_name']
# 获取数据
data = list(collection.find())
t1 = data[0]
print(pd.Series(t1))
```

### 

## 数据缺失处理

数据缺失通常有两种情况

- 一种是空 None等 在pandas是NaN （和numpy的nan是一样的）
- 一种是0

判断数据是否为NaN

- pd.isnull(df) 
- pd.notnull(df)

处理方式

- 方式一 删除NaN所在的行列dropna(axis=0, how="any", inplace=Flase)

  - axis=0 为行     1为列

  - any 只要有一个为nan就删除这一行(列) all 整行(列)都为NaN时候才删除
  - inplace=True 在原来数组直接修改

- 方式二 填充数据 t.fillna(t.mean()), t.fiallna(t.median()), f.fillna(0)

处理为0的数据

t[t==0] = np.nan

并不是每次为0的数据都需要处理

计算平均值的情况 nan是不参与计算的 但是0会

```python
import pandas as pd
import numpy as np
dic = [
	{"name":"zrlee", "score":80 , "gender":"男"},
	{"name":"marry", "score":75, "gender":"女"},
	{"name":"tom", "score":83, "gender":"男"},
	{"name":"sally", "score":78, "gender":"男"}
]

df = pd.DataFrame(dic, index=list("abcd"))
# 把第二行的成绩改为nan
df.iloc[1,2] = np.nan
print(df)
# 判断nan
print(df.isnull())
# 获取score为NaN的一列
print(df[pd.isnull(df["score"])])
# 删除只要有一个元素为NaN的一行
print(df.dropna(axis=0, how="any", inplace=False))

# 数据填充 分数为NaN的填充为平均值
print(df.fillna(df['score'].mean()))

# 填充指定的字段 并修改
df['score'] = df['score'].fillna(df['score'].mean())
print(df)
```

## pandas常用的统计方法

```python
mean() 平均值
tolist() 转换成列表
max() 最大值
min() 最小值
median() 中值
```



```python
import pandas as pd
import numpy as np
dic = [
	{"name":"zrlee", "score":80 , "gender":"男"},
	{"name":"marry", "score":75, "gender":"女"},
	{"name":"tom", "score":83, "gender":"男"},
	{"name":"sally", "score":78, "gender":"男"},
	{"name":"aaa", "score":np.nan, "gender":"男"},

]

df = pd.DataFrame(dic, index=list("abcde"))

print(df.info())
# 获取平均分数
print(df['score'].mean())
# 获取人数
print(len(set(df['name'])))
print(len(df['name'].unique())) # 名字唯一

# 最大值
print(df["score"].max())
print(df["score"].median())
# print(df["name"].str.split(",").tolist())
```

