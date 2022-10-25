# DataFrame basic options

## Option1 : 与  pd.info()等效操作

```
#data
+-------+----------+----+
|session|timestamp1| id2|
+-------+----------+----+
|      1|         1|null|
|      1|         2| 5.0|
|      1|         3| NaN|
|      1|         4|null|
|      1|         5|10.0|
|      1|         6| NaN|
|      1|         6| NaN|
+-------+----------+----+
```

1. ##### 计算每一列的空值情况

   ```python
   #option1
   df.select([count(when(isnan(c) | col(c).isNull(), c)).alias(c) for c in df.columns]).show() #
   #部分数据可以使用(col(c)=="") ，因为有的是空字符串
   +-------+----------+---+
   |session|timestamp1|id2|
   +-------+----------+---+
   |      0|         0|  5|
   +-------+----------+---+
   ```

   ```python
   #option2
   df.select([count(when(isnan(c), c)).alias(c) for c in df.columns]).show() #
   +-------+----------+---+
   |session|timestamp1|id2|
   +-------+----------+---+
   |      0|         0|  3|
   +-------+----------+---+
   ```

2. ##### 计算每一列数据分布情况

   ```python
   df.describe().show()
   +-------+-------+------------------+---+
   |summary|session|        timestamp1|id2|
   +-------+-------+------------------+---+
   |  count|      7|                 7|  5|
   |   mean|    1.0| 3.857142857142857|NaN|
   | stddev|    0.0|1.9518001458970664|NaN|
   |    min|      1|                 1|5.0|
   |    max|      1|                 6|NaN|
   +-------+-------+------------------+---+
   ```

3. ##### 计算每一列数据类型

   ```python
   df.dtypes   
   [('session', 'bigint'), ('timestamp1', 'bigint'), ('id2', 'double')]
   df.printSchema() #展示数据类型、表结构
   ```

4. ##### 输出列名

   ```python
   1. df.schema.names  #等价于pd.columns#
   2. df.columns
   ```

## Option2：展示 show()、collect()

1. df.show()

   ```python
   df.show(truncate=100)#显示截断长度。
   ```

2. df.collect()

   ```python
   df.collect()
   #PySpark的collect()操作是用来将所有结点中的数据**收集到驱动结点上**(PySpark基于分布式架构)。
   #因此collect()操作一般用于小型数据及上，在大型数据及上使用可能会导致内存不足。
   ```

## Option3：聚合操作groupBy()

```python
#聚合经典三连
groupBy(c1).agg(collect(c2)).alias(c2)
groupBy(c1).count().sort("")
#空值聚合不算任何元素，空字符串可聚合
```

## Option4:自定义函数 sql.functions.udf()

1. ##### 方法一：F.udf()

   ```python
   import pyspark.sql.functions as F
   def lala(x):
   		...
   		return ...
   bibi = F.udf(lala,StringType())
   ```

2. ##### 方法二：@udf

   ```python
   #方法二：
   @udf
   def lala(x):
     	...
       return ...
   ```

## Option5 : 时间操作



## Option6 : 重复值处理

1. ##### 重复数据统计

   ```python
   df.select("Columns").distinct().count()#某一列去重后的数量
   df.distinct().count()#整体去除行重复后的数
   ```

2. ##### 去重操作

   ```python
   df.dropDuplicates().show()#去除所有重复行
   df.dropDuplicates(subset=[c for c in df.columns if c != 'id']).show()
   #限定条件删除某些重复行
   ```

3. ##### 创建唯一标识id

   ```python
   import pyspark.sql.functions as fn
   # 生成唯一id
   df.withColumn('new_id', fn.monotonically_increasing_id()).show()
   #备注：monotonically_increasing_id()生成的数据会放到大约10亿个分区中， 每个分区不重复数据8亿条
   ```

## Option7 : 合并操作 join

1. 基础合并
2. 多限定合并

## Option8 : 空值操作

## Option9 : 其他操作

1. 批量更改列明

   ```python
   de.select([col(c).alias(c+"_2") for c in df.columns])
   ```


## Option10 : 数据类型

```python
#pyspark数据类型
“DataType”, “NullType”, “StringType”, “BinaryType”, “BooleanType”, “DateType”,
“TimestampType”, “DecimalType”, “DoubleType”, “FloatType”, “ByteType”, “IntegerType”,
“LongType”, “ShortType”, “ArrayType”, “MapType”, “StructField”, “StructType”

from pyspark.sql.types import *
```

## Option11:dataframe 转 list

1. 数据给驱动程序`collect()`并从每个logging中选取元素0

   ```python
    df.select(c).collect().map(_(0)).toList 
   ```

2. 我们在驱动程序`collect()`之间分配了map转换负载，而不是单个Driver。

   ```python
    df.select(c).rdd.map(r => r(0)).collect.toList 
   ```


## option12 spark & pandas 对比

| Pandas                                                       | Spark                                                        |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | :----------------------------------------------------------- |
| 工作方式                                                     | 单机single machine tool，没有并行机制parallelism 不支持Hadoop，处理大量数据有瓶颈 | 分布式并行计算框架，内建并行机制parallelism，所有的数据和操作自动并行分布在各个集群结点上。以处理in-memory数据的方式处理distributed数据。 支持Hadoop，能处理大量数据 |
| 延迟机制                                                     | not lazy-evaluated                                           | lazy-evaluated                                               |
| 内存缓存                                                     | 单机缓存                                                     | persist() or cache()将转换的RDDs保存在内存                   |
| DataFrame可变性                                              | Pandas中DataFrame是可变的                                    | Spark中RDDs是不可变的，因此DataFrame也是不可变的             |
| 创建                                                         | 从spark_df转换：pandas_df = spark_df.toPandas()              | 从pandas_df转换：spark_df = SQLContext.createDataFrame(pandas_df) 另外，createDataFrame支持从list转换spark_df，其中list元素可以为tuple，dict，rdd |
| list，dict，ndarray转换                                      | 已有的RDDs转换                                               |                                                              |
| CSV数据集读取                                                | 结构化数据文件读取                                           |                                                              |
| HDF5读取                                                     | JSON数据集读取                                               |                                                              |
| EXCEL读取                                                    | Hive表读取                                                   |                                                              |
|                                                              | 外部数据库读取                                               |                                                              |
| index索引                                                    | 自动创建                                                     | 没有index索引，若需要需要额外创建该列                        |
| 行结构                                                       | Series结构，属于Pandas DataFrame结构                         | Row结构，属于Spark DataFrame结构                             |
| 列结构                                                       | Series结构，属于Pandas DataFrame结构                         | Column结构，属于Spark DataFrame结构，如：DataFrame[name: string] |
| 列名称                                                       | 不允许重名                                                   | 允许重名 修改列名采用alias方法                               |
| 列添加                                                       | df[“xx”] = 0                                                 | df.withColumn(“xx”, 0).show() 会报错 from pyspark.sql import functions df.withColumn(“xx”, functions.lit(0)).show() |
| 列修改                                                       | 原来有df[“xx”]列，df[“xx”] = 1                               | 原来有df[“xx”]列，df.withColumn(“xx”, 1).show()              |
| 显示                                                         |                                                              | df 不输出具体内容，输出具体内容用show方法 输出形式：DataFrame[age: bigint, name: string] |
| df 输出具体内容                                              | df.show() 输出具体内容                                       |                                                              |
| 没有树结构输出形式                                           | 以树的形式打印概要：df.printSchema()                         |                                                              |
|                                                              | df.collect()                                                 |                                                              |
| 排序                                                         | df.sort_index() 按轴进行排序                                 |                                                              |
| df.sort() 在列中按值进行排序                                 | df.sort() 在列中按值进行排序                                 |                                                              |
| 选择或切片                                                   | df.name 输出具体内容                                         | df[] 不输出具体内容，输出具体内容用show方法 df[“name”] 不输出具体内容，输出具体内容用show方法 |
| df[] 输出具体内容， df[“name”] 输出具体内容                  | df.select() 选择一列或多列 df.select(“name”) 切片 df.select(df[‘name’], df[‘age’]+1) |                                                              |
| df[0] df.ix[0]                                               | df.first()                                                   |                                                              |
| df.head(2)                                                   | df.head(2)或者df.take(2)                                     |                                                              |
| df.tail(2)                                                   |                                                              |                                                              |
| 切片 df.ix[:3]或者df.ix[:”xx”]或者df[:”xx”]                  |                                                              |                                                              |
| df.loc[] 通过标签进行选择                                    |                                                              |                                                              |
| df.iloc[] 通过位置进行选择                                   |                                                              |                                                              |
| 过滤                                                         | df[df[‘age’]>21]                                             | df.filter(df[‘age’]>21) 或者 df.where(df[‘age’]>21)          |
| 整合                                                         | df.groupby(“age”) df.groupby(“A”).avg(“B”)                   | df.groupBy(“age”) df.groupBy(“A”).avg(“B”).show() 应用单个函数 from pyspark.sql import functions df.groupBy(“A”).agg(functions.avg(“B”), functions.min(“B”), functions.max(“B”)).show() 应用多个函数 |
| 统计                                                         | df.count() 输出每一列的非空行数                              | df.count() 输出总行数                                        |
| df.describe() 描述某些列的count, mean, std, min, 25%, 50%, 75%, max | df.describe() 描述某些列的count, mean, stddev, min, max      |                                                              |
| 合并                                                         | Pandas下有concat方法，支持轴向合并                           |                                                              |
| Pandas下有merge方法，支持多列合并 同名列自动添加后缀，对应键仅保留一份副本 | Spark下有join方法即df.join() 同名列不自动添加后缀，只有键值完全匹配才保留一份副本 |                                                              |
| df.join() 支持多列合并                                       |                                                              |                                                              |
| df.append() 支持多行合并                                     |                                                              |                                                              |
| 缺失数据处理                                                 | 对缺失数据自动添加NaNs                                       | 不自动添加NaNs，且不抛出错误                                 |
| fillna函数：df.fillna()                                      | fillna函数：df.na.fill()                                     |                                                              |
| dropna函数：df.dropna()                                      | dropna函数：df.na.drop()                                     |                                                              |
| SQL语句                                                      | import sqlite3 pd.read_sql(“SELECT name, age FROM people WHERE age >= 13 AND age <= 19”) | 表格注册：把DataFrame结构注册成SQL语句使用类型 df.registerTempTable(“people”) 或者 sqlContext.registerDataFrameAsTable(df, “people”) sqlContext.sql(“SELECT name, age FROM people WHERE age >= 13 AND age <= 19”) |
| 功能注册：把函数注册成SQL语句使用类型 sqlContext.registerFunction(“stringLengthString”, lambda x: len(x)) sqlContext.sql(“SELECT stringLengthString(‘test’)”) |                                                              |                                                              |
| 两者互相转换                                                 | pandas_df = spark_df.toPandas()                              | spark_df = sqlContext.createDataFrame(pandas_df)             |
| 函数应用                                                     | df.apply(f）将df的每一列应用函数f                            | df.foreach(f) 或者 df.rdd.foreach(f) 将df的每一列应用函数f df.foreachPartition(f) 或者 df.rdd.foreachPartition(f) 将df的每一块应用函数f |
| map-reduce操作                                               | map(func, list)，reduce(func, list) 返回类型seq              | df.map(func)，df.reduce(func) 返回类型seqRDDs                |
| diff操作                                                     | 有diff操作，处理时间序列数据（Pandas会对比当前行与上一行）   | 没有diff操作（Spark的上下行是相互独立，分布式存储的）        |

