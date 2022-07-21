# Linux命令-查看目录下文件个数

**1、查看当前目录下文件个数**

```BASH
ls -l |grep "^-" | wc -l
```

**2、查看当前目录下包含子目录的文件个数**

```bash
ls -lR |grep "^-" | wc -l
```

 **3、查看当前目录下目录个数**

```bash
ls -l |grep "^d" | wc -l
```

**4、查看当前目录下包含子目录的目录个数**

```bash
ls -lR |grep "^d" | wc -l
```

**5、查看当前文件某关键字的个数**

```bash
cat xxx.txt | grep "xxx" | wc -l
```

6、**Linux下用find查找当前目录的.a文件，并复制指定文件到\tmp\aout目录下。**

```bash
查找目录：find /（查找范围） -name '查找关键字' -type d
查找文件：find /（查找范围） -name 查找关键字 -print
mkdir -p /tmp/aout  && find ./ -name *.a | xargs cp -t /tmp/aout
```

