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

   1. 

