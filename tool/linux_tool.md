# Linux命令-

### **查看目录下文件个数**

```bash
#查看当前目录下文件个数
ls -l |grep "^-" | wc -l

#查看当前目录下包含子目录的文件个数
ls -lR |grep "^-" | wc -l

#查看当前目录下目录个数
ls -l |grep "^d" | wc -l

#查看当前目录下包含子目录的目录个数
ls -lR |grep "^d" | wc -l

#查看当前文件某关键字的个数
cat xxx.txt | grep "xxx" | wc -l
```

### **Linux下 查看文件夹大小**

```bash
du -h --max-depth=1 /path（查看path路径下文件夹大小）
du [-abcDhHklmsSx] [-L <符号连接>][-X <文件>][--block-size][--exclude=<目录或文件>] [--max-depth=<目录层数>][--help][--version][目录或文件]

```

### **Find  查找命令**

```bash
#L.inux下用find查找当前目录的.a文件，并复制指定文件到\tmp\aout目录下
查找目录：find /（查找范围） -name '查找关键字' -type d
查找文件：find /（查找范围） -name 查找关键字 -print
mkdir -p /tmp/aout  && find ./ -name *.a | xargs cp -t /tmp/aout
```

### **磁盘查看工具**

```bash
# df用于检查文件系统磁盘占用情况
df -h命令可直接查看磁盘信息
df -i 查看节点信息
# du检查磁盘空间占用情况
disk usage
# fdisk用于磁盘分区
fdisk -l #显示
```

