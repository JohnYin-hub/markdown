## DataFrame Basic Option

#### apply 函数应用

- option1  : apply  多值输入

```python
df = pd.DataFrame(......)
def func(row):
  a = row["..."]
  b = row["..."]
  ...
  return A,B
df[["",""]] = df.apply(func,axis=1,result_type = "expand")  #expand参数
```

#### 重复值处理

- option1 : df.deduplicate

`duplicated`函数用于标记`Series`中的值、`DataFrame`中的记录行是否是重复，重复为`True`，不重复为`False`。

```python
df.duplicated(self, subset=None, keep='first')#默认所有列，第一次出现外，其余相同的被标记为重复 
df.duplicated(['col1','col2'],keep='last')#所有相同的都被标记为重复
              keep='first'  #除了第一次出现外，其余相同的被标记为重复 
              keep='last'   #除了最后一次出现外，其余相同的被标记为重复

return: 返回bool值
重复的row ： df[df.duplicated(self, subset=None, keep='first')]
去重后的df ：df[~df.duplicated(self, subset=None, keep='first')]
```

- option2 : df.drop_duplicates

```python
df.drop_duplicates(self, subset=None, keep='first',inplace=False)inplace为True直接修改原DF
```

#### 展示

- option1:  pd.set_option

```python
pd.set_option('max_colwidth',100) #设置value的显示长度为100，默认为50
pd.set_option('display.max_rows', None) #显示所有行
pd.set_option('display.max_columns', None)   #显示所有列
```

#### 空值处理

- option1  : df.isnull()常规操作

```python
df[df[""].isnull()]
```

- option2 : df.isnull()骚操作

```python
print(df[df.isnull().T.any()])
df.dropna(axis=0, how='any', thresh=None, subset=None, inplace=False)
#inplace 是否在原数据上操作
#how =“any”|"all",只要有缺失值就删除该行或该列|所有的值缺失才删除
#thresh 有多少个空值才删除
```

- option : df.fillna('missing') 填充值

```python
df.fillna('missing')
df.fillna(0)
df.fillna(df.mean()['one':'two']) #指定列平均值填充
df 的NA属于np NA ，其本质类型是float np.nan!=np.n
```

#### 存进去是列表，读出来是字符串

- option1 : eval()

  ```python
  df["data"] = df["data"].apply(lambda x:eval(x)
  ```


#### 时间处理模块

- option1 : pd.to_datetime()    映射时间戳

```python
min_datetime = pd.to_datetime('2020-07-11') # same to pd.to_datetime('20200711')
#output:Timestamp('2021-07-21 00:00:00')
```

- option2 : datatime.datetime.strptimr()   映射时间戳

```python
from datetime import datetime
t = '2021-09-07'
y = datetime.strptimr(t,'%Y-%m-%d')
print(y)
#output:2021-09-07 00:00:00
```

- option3 : datetime.timedelta()  时间更改

```python
str_time = (min_datetime + timedelta(days=-30)).strftime("%Y-%m-%d")
print(str_time)
#output:2020-06-11
```

- option4 : np.timedelta64()  numpy 时间差值

#### 转置Dataframe

- option1 : df.values.T

```python
df2 = pd.DataFrame(df.values.T, index=df.columns, columns=df.index)
#df.
```

#### 改名换列

- option1 : df.columns = ~~~  #暴力更改

```python
df.columns = ['a', 'b', 'c', 'd', 'e']
```

- option2 : df.rename   可修改部分列名

```python
DataFrame.rename(self, mapper=None, index=None, columns=None, axis=None,copy=True, inplace=False, level=None, errors=‘ignore’)

mapper：dict #可以是字典也可以是映射函数，更重要的是可以选择局部映射
df.rename(lambda x: x+11) #修改索引
df.rename({0:111}) #索引为0的改为11
```

#### 合并

- option1 ：pd.merge()

```python
merge(left,right,how="inner",on=None,
    left_on=None,right_on=None,
    left_index=False,right_index=False,
    sort=False,
    suffixes=("_x", "_y"),
    copy=True,
    indicator=False,
    validate=None,
)
```

#### 踩坑

- option1：Nan 值花式坑

```python
#isnull() 和 isna() 两个完全等效
pd.isnull()=pd.isna()
#Nan的数据类型是 float，Nan的布尔值返回的是True
type(Nan) = "float"
bool(Nan) = True
```

