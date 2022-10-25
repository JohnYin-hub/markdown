# Linux命令-

# 文件操作命令

- #### 查看目录下文件个数

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

- #### **Linux下 查看文件夹大小**


```bash
du -h --max-depth=1 /path（查看path路径下文件夹大小）
du [-abcDhHklmsSx] [-L <符号连接>][-X <文件>][--block-size][--exclude=<目录或文件>] [--max-depth=<目录层数>][--help][--version][目录或文件]

```

- #### **Find  查找命令**


```bash
#L.inux下用find查找当前目录的.a文件，并复制指定文件到\tmp\aout目录下
查找目录：find /（查找范围） -name '查找关键字' -type d
查找文件：find /（查找范围） -name 查找关键字 -print
mkdir -p /tmp/aout  && find ./ -name *.a | xargs cp -t /tmp/aout
```

# 磁盘查看工具

```bash
# df用于检查文件系统磁盘占用情况
df -h命令可直接查看磁盘信息
df -i 查看节点信息
# du检查磁盘空间占用情况
disk usage
# fdisk用于磁盘分区
fdisk -l #显示
```

# tmux 终端分屏工具

- #### 基础操作

```bash
tmux new -s roclinux   			#创建会话
tmux detach 								#detach会话 或者按下Ctrl+b d
tmux kill-session -t <name> # 杀死会话

tmux list-keys 							# 列出所有快捷键，及其对应的 Tmux 命令
tmux list-commands					# 列出所有 Tmux 命令及其参数
tmux info										# 列出当前所有 Tmux 会话的信息
tmux source-file ~/.tmux.conf # 重新加载当前的 Tmux 配置

```

- #### 分屏操作

```bash
tmux split-window 		# 划分上下两个窗格
tmux split-window -h 	# 划分左右两个窗格
```

- #### 快捷键操作

```bash
Ctrl+b % 					  #划分左右两个窗格。
Ctrl+b " 					  #划分上下两个窗格。
Ctrl+b <arrow key> #光标切换到其他窗格。<arrow key>是指向要切换到的窗格的方向键，比如切换到下方窗格，就按方向键↓。
Ctrl+b ; 					  #光标切换到上一个窗格。
Ctrl+b o 						#光标切换到下一个窗格。
Ctrl+b { 						#当前窗格与上一个窗格交换位置。
Ctrl+b } 						#当前窗格与下一个窗格交换位置。
Ctrl+b Ctrl+o 			#所有窗格向前移动一个位置，第一个窗格变成最后一个窗格。
Ctrl+b Alt+o 				#所有窗格向后移动一个位置，最后一个窗格变成第一个窗格。
Ctrl+b x 						#关闭当前窗格。
Ctrl+b ! 						#将当前窗格拆分为一个独立窗口。
Ctrl+b z 						#当前窗格全屏显示，再使用一次会变回原来大小。
Ctrl+b Ctrl+<arrow key> #按箭头方向调整窗格大小。
Ctrl+b q 						#显示窗格编号。

按住Ctrl+b 上下左右键控制窗格大小
```

