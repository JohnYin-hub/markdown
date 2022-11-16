### 数据分析起手式

#### 抽取元素

- option1 np.random.choice()

```python
np.random.choice(np.arange(number1),number2,replace=True)
# 默认repalce=True 表示重复抽取
```

- Option2 np.random.permutation()

```python
np.ramdom.seed(1234)
inde = np.ramdom.permutation(np.arange())

# 不放回抽取
np.random.seed(1234)
index = np.random.choice(np.arange(number1),number2,replace=False)
# 取剩下的index---
res_index = np.setdiff1d(np.arange(number1),index)
```

#### pandas去重

```python
df[~df.duplicate()]
```

#### Pandas 离散数据类型排序

```python
#df["columns1"]是离散数据类型
list_sort = ['','','','','']
df["columns1"] = df["columns1"].astype("category".cat.set_categories(list_sorted))
df_sorts = df.sort_values(by=["columns1"],asending=Ture)
#------------------------sort参数：na_postion =“False”#default    可替换为first
```

#### 统计长度操作

```python
df["data_len"] = df["columns1"].apply(len)
print(data["data_len"].describe())
```

#### 重新索引

```python
df.reset_index()#有正常索引的再列出一列索引，concat会自动重置索引，groupby最适合用这个
```

#### 空值处理

```python
print(df[df.isnull().T.any()])
df.dropna(axis=0, how='any', thresh=None, subset=None, inplace=False)
#inplace 是否在原数据上操作
#how =“any”|"all",只要有缺失值就删除该行或该列|所有的值缺失才删除
#thresh 有多少个空值才删除
```

#### 哑变量处理

```python
pd.get_dummies(dataframe)
#返回一个哑变量的矩阵，需要修改表头
```

#### Mysql数据库操作

```sql
#终端操作
mysql -uroot -p #登录mysql
show databases 
use database
show tables
```

#### 
