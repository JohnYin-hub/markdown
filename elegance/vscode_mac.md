

# mac Shell 自动操作

利用MAC OS的***自动操作\***，可以实现右键打开vscode功能，提升开发效率。

![img](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/v2-9445633fd4aef3dce3df08b06353b75d_1440w.webp)

**具体操作步骤如下：**

**1、应用中心搜索『自动操作.app』**

![img](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/v2-38eeb26255db226c1b87a20c469b55c4_1440w.webp)

**2. 文件 - 新建 - 快速操作 - 选取**

![img](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/v2-f1181d0d7c899f27c88ded14cfc700ee_1440w.webp)

**3、按照下图操作步骤新建工作流程**

1）点击实用工具

2）双击运行shell脚本

3） 文件或文件夹

4）作为自变量

5）复制以下代码至『运行脚本』代码框中

```bash
for f in "$@"
do
    open -a "Visual Studio Code" "$f"
done
```

![img](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/v2-d5a8f18bd890bf8decee67489fe7729d_1440w.webp)



**4、cmd + s 保存工作流程即可**

![img](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/v2-35705f91e02bd2466dec956b9527a90b_1440w.webp)