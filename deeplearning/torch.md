

###### AI 帮你理解科学：https://www.aminer.cn/

###### 模型保存和加载

#### 		方法1:整个模型

```python
#保存模型
torch.save(model.state_dict(), path)
#加载模型
model.load_state_dict(torch.load(path))
```

#### 		方法2:保存参数（官方推荐）

```python
#保存模型
state = {'model': model.state_dict(), 'optimizer': optimizer.state_dict(), 'epoch': epoch}
torch.save(state, path)
#加载模型
checkpoint = torch.load(path)
model.load_state_dict(checkpoint['model'])
optimizer.load_state_dict(checkpoint['optimizer'])
epoch = checkpoint(['epoch'])
```

#### 		pickle保存模型

```python
import pickle #pickle模块

#保存Model(注:save文件夹要预先建立，否则会报错)
with open('save/clf.pickle', 'wb') as f:
    pickle.dump(clf, f)

#读取Model
with open('save/clf.pickle', 'rb') as f:
    clf2 = pickle.load(f)
    #测试读取后的Model
    print(clf2.predict(X[0:1]))
```

###### 关于 conda

#### 		conda自动启用环境

```
conda create --name <name>
conda create --name <name> python=3.8  #可命令环境的python版本
conda config --set auto_activate_base false

conda remove --name xxxx  --all #彻底删除旧环境
```

#### 		pip切换镜像源

```
/Usr/home/.pip/pip.conf
[global]
index-url = http://mirrors.aliyun.com/pypi/simple/
[install]
trusted-host=mirrors.aliyun.com
#----------------------------------------------------
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --set show_channel_urls yes

#-----------------------------------------------------
conda config --show-sources
```

