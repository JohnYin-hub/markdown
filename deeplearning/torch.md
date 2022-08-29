

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

### torch 筛选数据

​	torch.nonezero() 和torch.index_select()搭配 筛选

```

```

