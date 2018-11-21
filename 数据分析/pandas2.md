### 数据合并 join() 、merge()

参考地址https://blog.csdn.net/weixin_37226516/article/details/64137043

### 数据分组聚合

#### groupby() 、count() 分组聚合

- df.groupny(columns_name)

```python
import pandas as pd 
import numpy as np 

df = pd.DataFrame({
	"name": ["A", "B", "C", "E", "F", "G"],
	"age": [21,22,23,24,25,26],
	"score": [81,82,83,84,85,86],
	"gender": ["男","女","男","女","男","女"],
	"city": ["美国", "中国", "中国", "英国", "英国", "澳大利亚"]

	})


for i, j in df.groupby('city'):
	print("国家是%s的数据" % i)
	print(j)
	print("-"*40)
    
输出
国家是中国的数据
  name  age  score gender city
1    B   22     82      女   中国
2    C   23     83      男   中国
----------------------------------------
国家是澳大利亚的数据
  name  age  score gender  city
5    G   26     86      女  澳大利亚
----------------------------------------
国家是美国的数据
  name  age  score gender city
0    A   21     81      男   美国
----------------------------------------
国家是英国的数据
  name  age  score gender city
3    E   24     84      女   英国
4    F   25     85      男   英国
----------------------------------------
```

- count()

```python
grouped_data = df.groupby('city')
print(grouped_data.count())
print(grouped_data['name'].count())

      name  age  score  gender
city                          
中国       2    2      2       2
澳大利亚     1    1      1       1
美国       1    1      1       1
英国       2    2      2       2


city
中国      2
澳大利亚    1
美国      1
英国      2
```

```python
grouped_data = df.groupby('city')
# 返回的是Series类型 
age_count = grouped_data['name'].count()
# Series 可以直接进行索引操作
print("中国的人数%d" % age_count['中国'])

# 中国 按照性别分组统计
china_data = df[df['city']=='中国']
print(china_data.groupby('gender').count())
```

#### 其他的聚合函数

| 函数名   | 说明                 |
| :------- | -------------------- |
| count    | 分组中非nan的数量    |
| sum      | 非nan数值的和        |
| mean     | 非nan数值的平均值    |
| std、var | 标准差和方差         |
| min、max | 非nan的最大值 最小值 |

### 索引 复合索引

#### 获取索引 index

```python
import pandas as pd 
import numpy as np 

df = pd.DataFrame({
	"a": np.arange(7),
	"b": np.arange(7, 0, -1),
	"c": ['one', 'one', 'one', 'two', 'two', 'two', 'two'],
	"d": list('hijklmn')
})

print(df.index)
```



#### 重新设置索引 reindex()

`df.reindex([])`

#### 将多列设置成索引 

```python
import pandas as pd 
import numpy as np 

df = pd.DataFrame({
	"a": np.arange(7),
	"b": np.arange(7, 0, -1),
	"c": ['one', 'one', 'one', 'two', 'two', 'two', 'two'],
	"d": list('hijklmn')
})
# 把d一列作为索引
print(df.set_index(['d']))

# 把 c d 作为索引
print(df.set_index(['c', 'd']))


   a  b    c
d           
h  0  7  one
i  1  6  one
j  2  5  one
k  3  4  two
l  4  3  two
m  5  2  two
n  6  1  two



       a  b
c   d      
one h  0  7
    i  1  6
    j  2  5
two k  3  4
    l  4  3
    m  5  2
    n  6  1
```

```python
import pandas as pd 
import numpy as np 

df = pd.DataFrame({
	"a": np.arange(7),
	"b": np.arange(7, 0, -1),
	"c": ['one', 'one', 'one', 'two', 'two', 'two', 'two'],
	"d": list('hijklmn')
})
# 把 c d 作为索引
c = df.set_index(['c', 'd'])
# a列 one和j索引
print(c['a']['one']['j'])
结果输出2

# loc 通过索引获取第j行
print(c.loc['one'].loc['j'])
输出
a    2
b    5
```

#### swaplevel() 交换索引顺序

```python
import pandas as pd 
import numpy as np 

df = pd.DataFrame({
	"a": np.arange(7),
	"b": np.arange(7, 0, -1),
	"c": ['one', 'one', 'one', 'two', 'two', 'two', 'two'],
	"d": list('hijklmn')
})
# 把 c d 作为索引
c = df.set_index(['d', 'c'])['a']
print(c)
# 从内层索引获取
print(c.swaplevel()['one'])
```

### 例子

数据来源https://raw.githubusercontent.com/zygmuntz/goodbooks-10k/master/books.csv

```python
import pandas as pd 
import numpy as np 
from matplotlib import pyplot as plt
# 全球排行名前10000本书本的数据  需求： 不同年份的书的数量，不同年份的书的平均情况
df = pd.read_csv('./book.csv')
plt.rcParams[u'font.sans-serif'] = ['simhei']
# print(df.info())
# 拿到 有年份的数据
book = df[pd.notnull(df['original_publication_year'])]
print(book.info())

# 不同年份书本数量
book_years_count = book.groupby(by='original_publication_year').count()['title'].sort_values(ascending=False)

# print(book_years_count)
# 不同年份书本平均评分
# book_mead_ratings = book['average_rating'].groupby(by=book['original_publication_year']).mean()

# print(book_years_count.iloc[:10].values)

plt.bar(range(10), book_years_count.iloc[:10].values)
plt.xticks(range(10), book_years_count.iloc[:10].index,rotation=15)
plt.xlabel('年份')
plt.ylabel("数量")
plt.title("前10的书本")
plt.show()


```

![](http://libs.zrlee.cn/image/d9a039dd-2293-4b27-b538-e5579ed2354a.PNG)

