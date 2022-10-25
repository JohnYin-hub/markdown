## Jupyter Notebook 配置

- #### 1 安装jupyternotebook后生成配置文件

```bash
[root jupyter_project]# jupyter notebook --generate-config
```

- #### 2 生成密码

​    终端输入ipython

```bash
[root jupyter_project]# ipython 
In [1]: from notebook.auth import passwd                     
In [2]: passwd()
Enter password:threatbook Verify password:threatbook 
Out[2]: 'sha1:ea48948e0e51:7f619460f77a6dc033ff09efdb64ff9c782285fe'
```

将生成的Out shar1密文copy下来

- #### 3 修改配置文件

```bash
[root jupyter_project]# vim ~/.jupyter/jupyter_notebook_config.py
```

在配置文件最后添加修改如下:

```bash
c.NotebookApp.ip='*' c.NotebookApp.password = u'sha1:ea48948e0e51:7f619460f77a6dc033ff09efdb64ff9c782285fe' c.NotebookApp.open_browser = False c.NotebookApp.port =8888
```

- ####  4 修改jupyter的主题:

```bash
[root jupyter_project]# pip install jupyterthemes 
[root jupyter_project]# jt -t monokai -f fira -fs 16 -cellw 94% -ofs 14 -dfs 14 -T -N (恢复默认主题,只需执行代码：jt -r)
```

重启jupyter notebook

```bash
[root jupyter_project]# jupyter notebook --ip=0.0.0.0 --allow-root
```

- #### 5 开启目录

```bash
[root jupyter_project]# pip install jupyter_contrib_nbextensions 
[root jupyter_project]# jupyter contrib nbextension install --user
```

导航栏下Nbextensions，勾选 Table of contants

- #### 6设置后台运行

命令1：

```bash
[root jupyter_project]# jupyter notebook --allow-root > jupyter.log 2>&1 &
```

命令2：#永不挂机

```bash
[root jupyter_project]# nohup jupyter notebook --allow-root > jupyter.log 2>&1 &
```

用&让命令后台运行, 并把标准输出写入jupyter.log中

nohup表示no hang up, 就是不挂起, 这个命令执行后即使终端退出, Jupyter也不会停止运行

## Jupyter notebook 永不挂机

```shell
nohup jupyter notebook --allow-root --port 1104 > jupyter.log 2>1 &
```

### 两个notebook   合并   nbmerge

```shell
#安装包
pip install nbmerge
#命令行操作文件
nbmerge 1.ipynb 2.ipynb > 3.ipynb
```

### 