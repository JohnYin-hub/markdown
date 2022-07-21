

### Zeppling 起手式

```python
%ipyspark
import pyspark
print("version",pyspark.__version__)
```

```python
%ipyspark
from pyspark.sql import HiveContext
import pandas as pd
hive_context = HiveContext(sc)
raw_df = hive_context.sql("select * from priv_edr.new_raw_log")
```

### pyspark自定义函数

```python
import pyspark.sql.functions as F
---------------------------------------两种方式均可
def lala(x):
		...
		return ...

bibi = F.udf(lala,StringType())
#######################################
@udf
def lala(x):
  	...
    return ...
 
```

### Pyspark 远程下载

```python
#将dataframe转换为csv格式，合并为一个csv文件，保存至edr服务器hdfs下（/data/edr 是有编辑权限的目录）
DF = spark.createDataFrame()
DF.repartition(1).write.mode('overwrite').format('csv').save('/data/edr/chongchao.csv')

```

##### 通过跳板机登陆edr服务器

```
ssh usrname@106.75.103.111 #登陆跳板机 端口22122 
ssh edr@10.42.45.106       #登陆edr服务器

mkdir xxxx                 #在edr用户目录下创建xxxx文件夹
hdfs dfs -get /data/edr/xxx.csv ./    #从hdfs目录取出csv文件
```

##### 将服务器的文件拷贝到跳板机

```
tar zcvf xxx.csv.tar.gz ./xxx.csv/    #压缩csv文件
scp	-r -P 22122 xxx.csv.tar.gz usename@106.75.103.111:/home/usrname/  #远程拷贝到跳板机
```

### 排序技巧

```python
df.orderBy(desc("colname"))
#or
df.sort('p_date',ascending=False)
```

### org.apache.spark.sql.functions 函数总览

org.apache.spark.sql.functions是一个Object，提供了约两百多个函数。
大部分函数与Hive的差不多。
除UDF函数，均可在spark-sql中直接使用。
经过import org.apache.spark.sql.functions._ ，也可以用于Dataframe，Dataset。
大部分支持Column的函数也支持String类型的列名。这些函数的返回类型基本都是Column。

