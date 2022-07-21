### 	datacompy Package （对比dataframe，pandas和pyspark都适用）

**Document**：[datacompy文档](https://capitalone.github.io/datacompy/index.html#)

### df1

| acct_id     | dollar_amt | name             | float_fld  | date_fld   |
| ----------- | ---------- | ---------------- | ---------- | :--------- |
| 10000001234 | 123.45     | George Maharis   | 14530.1555 | 2017-01-01 |
| 10000001235 | 0.45       | Michael Bluth    | 1          | 2017-01-01 |
| 10000001236 | 1345       | George Bluth     |            | 2017-01-01 |
| 10000001237 | 123456     | Bob Loblaw       | 345.12     | 2017-01-01 |
| 10000001238 | 1.05       | Lucille Bluth    |            | 2017-01-01 |
| 10000001238 | 1.05       | Loose Seal Bluth |            | 2017-01-01 |

### df2

| acct_id     | dollar_amt | name                 | float_fld |
| ----------- | ---------- | -------------------- | --------- |
| 10000001234 | 123.4      | George Michael Bluth | 14530.155 |
| 10000001235 | 0.45       | Michael Bluth        |           |
| 10000001236 | 1345       | George Bluth         | 1         |
| 10000001237 | 123456     | Robert Loblaw        | 345.12    |
| 10000001238 | 1.05       | Loose Seal Bluth     | 111       |

### on  pandas

```python
compare = datacompy.Compare(df1,df2,
    join_columns='acct_id',  #You can also specify a list of columns
    on_index=True,#用索引做连接
    abs_tol=0, rel_tol=0, #Absolute tolerance 包容度
    df1_name='Original',df2_name='New'#改名字
    ignore_case ="")
compare.matches(ignore_extra_columns=False)#是否是一致
```

```python
print(compare.intersect_rows[['name_df1', 'name_df2', 'name_match']])
#            name_df1              name_df2  name_match
# 0    George Maharis  George Michael Bluth       False
# 1     Michael Bluth         Michael Bluth        True
# 2      George Bluth          George Bluth        True
# 3        Bob Loblaw         Robert Loblaw       False
# 5  Loose Seal Bluth      Loose Seal Bluth        True
print(compare.df1_unq_rows)#独立行
print(compare.intersect_columns())#交集列名
# {'float_fld', 'acct_id', 'name', 'dollar_amt'}
print(compare.df1_unq_columns())#独立列名

compare.all_mismatch()#显示不同的row
```

