# 打印版本

```python
import sys
print(sys.version)
```

# pandas时间处理

```python
import pandas as pd
import numnpy as np
from datetime import timedelta

min_datetime = pd.to_datetime('2020-07-11')
str_time = (min_datetime + timedelta(days=-30)).strftime("%Y-%m-%d")
print(str_time)
#------
#output:
2020-06-11

from datetime import datetime
t = '2021-09-07'
y = datetime.strptimr(t,'%Y-%m-%d')
print(y)
#output:2021-09-07 00:00:00
```

#### Pandas Timedelta 转换格式

```python
import numpy as np
import pandas as pd

a = pd.datetime("20210721");b = pd.datetime("20210806") #type Timestamp
c = b-a #type Timedelta

    print(int(c/np.timedelta64(1,"D")))
#------
#output:
16
```

# 参数管理 argparse

#### 构建一个参数管理对象 ArgumentParser()

```python
#./Model_para.py
import argparse

class Hpara():
    parser = argparse.ArgumentParser()#构建一个参数管理对象

#数据集参数
    parser.add_argument('--train_path',default='./data/train_data.data',type=str)
    parser.add_argument('--test_path',default='./data/test_data.data',type=str)

    parser.add_argument('--len_vocab',default=4743,type=int)
    parser.add_argument('--label_num',default=7,type=int)
```

#### 解析参数 .parse_args()

```python
from Model_para import Hpara
hp = Hpara()
parser = hp.parser
para = parser.parse_args(args=[])

```

在Python中的代码中经常会见到这两个词 args 和 kwargs，前面通常还会加上一个或者两个星号。其实这只是编程人员约定的变量名字，args 是 arguments 的缩写，表示位置参数；kwargs 是 keyword arguments 的缩写，表示关键字参数。这其实就是 Python 中可变参数的两种形式，并且 *args 必须放在 **kwargs 的前面，因为位置参数在关键字参数的前面。

#### *args的用法

*args就是就是传递一个可变参数列表给函数实参，这个参数列表的数目未知，甚至长度可以为0。下面这段代码演示了如何使用args

```python
def test_args(first, *args):
    print('Required argument: ', first)
    print(type(args))
    for v in args:
        print ('Optional argument: ', v)

test_args(1, 2, 3, 4)
```

第一个参数是必须要传入的参数，所以使用了第一个形参，而后面三个参数则作为可变参数列表传入了实参，并且是作为元组tuple来使用的。代码的运行结果如下

```cpp
Required argument:  1
<class 'tuple'>
Optional argument:  2
Optional argument:  3
Optional argument:  4
```

#### **kwargs

而**kwargs则是将一个可变的关键字参数的字典传给函数实参，同样参数列表长度可以为0或为其他值。下面这段代码演示了如何使用kwargs

```python
def test_kwargs(first, *args, **kwargs):
   print('Required argument: ', first)
   print(type(kwargs))
   for v in args:
      print ('Optional argument (args): ', v)
   for k, v in kwargs.items():
      print ('Optional argument %s (kwargs): %s' % (k, v))

test_kwargs(1, 2, 3, 4, k1=5, k2=6)
```

正如前面所说的，args类型是一个tuple，而kwargs则是一个字典dict，并且args只能位于kwargs的前面。代码的运行结果如下

```text
Required argument:  1
<class 'dict'>
Optional argument (args):  2
Optional argument (args):  3
Optional argument (args):  4
Optional argument k2 (kwargs): 6
Optional argument k1 (kwargs): 5
```

#### 调用函数

args和kwargs不仅可以在函数定义中使用，还可以在函数调用中使用。在调用时使用就相当于pack（打包）和unpack（解包），类似于元组的打包和解包。

首先来看一下使用args来解包调用函数的代码，

```python
def test_args_kwargs(arg1, arg2, arg3):
    print("arg1:", arg1)
    print("arg2:", arg2)
    print("arg3:", arg3)

args = ("two", 3, 5)
test_args_kwargs(*args)

#result:
arg1: two
arg2: 3
arg3: 5
```

将元组解包后传给对应的实参，kwargs的用法与其类似。

```bash
kwargs = {"arg3": 3, "arg2": "two", "arg1": 5}
test_args_kwargs(**kwargs)

#result
arg1: 5
arg2: two
arg3: 3
```

args和kwargs组合起来可以传入任意的参数，这在参数未知的情况下是很有效的，同时加强了函数的可拓展性。

# encoding 

```python
encoding =“utf-8”,"gbk","ISO-8859-1"
```

# 文件操作 

#### glob模块

```python
import glob  
  
#获取指定目录下的所有图片  
print(glob.glob(r"E:\Picture\*\*.jpg"))
  
#获取上级目录的所有.py文件  
print(glob.glob(r'../*.py') #相对路径)  

```

#### os模块历遍文件夹文件名

```python
import os
def walkFile(file):
    for root, dirs, files in os.walk(file):

        # root 表示当前正在访问的文件夹路径
        # dirs 表示该文件夹下的子目录名list
        # files 表示该文件夹下的文件list

        # 遍历文件
        for f in files:
            print(os.path.join(root, f))

        # 遍历所有的文件夹
        for d in dirs:
            print(os.path.join(root, d))

dir_name = os.listdir("path")#path文件夹下子文件名（一个层级关系）

```

#### os模块切换工作目录

```python
import os
print(os.getcwd())#打印当前工作目录
os.chdir(path)   #切换工作目录
os.chdir(os.path.dirname(__file__))#将当前文件所在路径设置为工作目录
'''
__file__是文件的绝对路径类似 /home/aa/bb.py
os.path.dirname()返回一个包含输入文件的目录，这是输出/home/aa
os.chdir()切换当前目录为输入值
'''
```

#### 列表写入txt

```python
lyst = [.....]
f = open("./lyst.txt","w")
f.write(str(lyst))
f.close
```

# Log 日志模块

#### logging 模块

```python
'''
整体说明：
01 日志就是记录一些信息，方便查询或者辅助开发。
02 日志有两种形式，一种是记录到文件中，一种是显示屏幕（控制台）中。
03 日志有3个版本，低配版、标配版、高配版。
04 日志的5种等级，由低到高的顺序如下：
    （1）logging.debug('调试模式')，默认值为10
    （2）logging.info('正常运行') ，默认值为20
    （3）logging.warning('警告')，默认值为30
    （4）logging.error('错误')，默认值为40
    （5）logging.critical('系统崩了')，默认值为50
05 默认的日志级别设置为warning。
'''

# 低配版本：只能写入文件或者是屏幕显示。
import logging

logging.basicConfig(
    # level= 10,
    level=logging.DEBUG,  # 设置显示的级别
    format='%(asctime)s %(filename)s [line:%(lineno)d] %(levelname)s %(message)s ',  # 设置日志显示格式
    datefmt="%Y-%m-%d",  # 设置日期，与astime对应
    filename='a.log',  # 默认我a模式，使用的是gbk形式编码。
    filemode="a"  # 可以修改模式，但是一般不用修改
)

logging.debug("调试模式")
logging.info("正常运行")
logging.warning("警告")
logging.error("错误")
logging.critical("系统崩溃了")

# 标配版本：既能在文件中写入，又在屏幕显示。
import logging
# 创建logging对象
logger = logging.getLogger()
# 创建文件对象
fh1 = logging.FileHandler("a1,log",encoding="utf8")  # 一定要指定编码方式，否则程序会报错。
fh2 = logging.FileHandler("a2.log",encoding="utf8")

# 创建屏幕对象
sh =logging.StreamHandler()

# 定义显示格式
formater1 = logging.Formatter(
    fmt='%(asctime)s %(filename)s [line:%(lineno)d] %(levelname)s %(message)s', # fmt变量名是固定的。
    datefmt= "%Y-%m-%d %H:%M:%S",
)

formater2 = logging.Formatter(
    fmt='%(asctime)s %(filename)s [line:%(lineno)d] %(levelname)s %(message)s', # fmt变量名是固定的。
    datefmt= "%Y-%m-%d %H:%M:%S",
)
formater3 = logging.Formatter(
    fmt='%(asctime)s %(filename)s %(message)s', # fmt变量名是固定的。
    datefmt= "%Y-%m-%d %H:%M:%S",
)

# 给对象绑定格式
fh1.setFormatter(formater1)
fh2.setFormatter(formater2)
sh.setFormatter(formater3)

# 给logger对象添加其他对象
logger.addHandler(fh1)
logger.addHandler(fh2)
logger.addHandler(sh)

# 设置logger级别
logger.setLevel(30)
sh.setLevel(40)
fh1.setLevel(40)
fh2.setLevel(50)

logging.debug('调试模式')  # 10
logging.info('正常运行')  # 20
logging.warning('警告')  # 30
logging.error('错误')  # 40
logging.critical('系统崩了')  # 50

# 高配版本：通过导入文件（导入字典的方式）写日志Django

import os
import logging.config

# 定义三种日志输出格式 开始

standard_format = '[%(asctime)s][%(threadName)s:%(thread)d][task_id:%(name)s][%(filename)s:%(lineno)d]' 
                  '[%(levelname)s][%(message)s]' #其中name为getlogger指定的名字

simple_format = '[%(levelname)s][%(asctime)s][%(filename)s:%(lineno)d]%(message)s'

id_simple_format = '[%(levelname)s][%(asctime)s] %(message)s'

# 定义日志输出格式 结束

# print(__file__)
logfile_dir = os.path.dirname(os.path.abspath(__file__))  # log文件的目录

logfile_name = '高配版.log'  # log文件名

# # 如果不存在定义的日志目录就创建一个
# if not os.path.isdir(logfile_dir):
#     os.mkdir(logfile_dir)

# log文件的全路径
logfile_path = os.path.join(logfile_dir, logfile_name)


# log配置字典
# 第一层键值对的键固定的关键字不能改变，即version、disable_existing_loggers、formatters、filters、handlers、loggers不能改变。

LOGGING_DIC = {
    'version': 1, # 版本
    'disable_existing_loggers': False,  #
    'formatters': {
        'standard': {
            'format': standard_format
        },
        'simple': {
            'format': simple_format
        },
        'id_simple_format':{
                'format': id_simple_format
        }
    },
    'filters': {},
    'handlers': {
        #打印到终端的日志
        'console': {
            'level': 'ERROR',  # 设置在终端显示的等级
            'class': 'logging.StreamHandler',  # 打印到屏幕
            'formatter': 'simple'
        },
        #打印到文件的日志,收集info及以上的日志
        'default': {
            'level': 'DEBUG',  # 设置在文件打印的等级
            'class': 'logging.handlers.RotatingFileHandler',  # 保存到文件
            'formatter': 'standard',
            'filename': logfile_path,  # 日志文件
            'maxBytes': 300,  # 日志大小 300bytes
            'backupCount': 5, # 最多只有5个文件
            'encoding': 'utf-8',  # 日志文件的编码，再也不用担心中文log乱码了
        },
    },
    'loggers': {
        #logging.getLogger(__name__)拿到的logger配置
        '': {
            'handlers': ['default', 'console'],  # 这里把上面定义的两个handler都加上，即log数据既写入文件又打印到屏幕
            'level': 'DEBUG',
            'propagate': True,  # 向上（更高level的logger）传递
        },
    },
}



logging.config.dictConfig(LOGGING_DIC)  # 导入上面定义的logging配置
# # logging.config  # 将你写好的logging 字典 在导入logging.config后，传到logging模块中
logger = logging.getLogger()  # 生成一个log实例  通过字典自己设置的个性化的log对象


logging.debug('调试模式')  # 10
logging.info('正常运行')  # 20
logging.warning('警告')  # 30
logging.error('错误')  # 40
logging.critical('系统崩了')  # 50
```

