

###### AI 帮你理解科学：https://www.aminer.cn/

### 模型保存和加载

##### 		方法1:整个模型

```python
#保存模型
torch.save(model.state_dict(), path)
#加载模型
model.load_state_dict(torch.load(path))
```

##### 		方法2:保存参数（官方推荐）

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

##### 		pickle保存模型

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

### **torch 筛选数据**

​	torch.nonezero() 和torch.index_select()搭配 筛选

```python
torch.nonzero(input,*,out=None,as_tuple)

label = torch.tensor([[1,0,0],
											[1,0,1]])
											
print(label.nonzero())
out:
tensor([[0,0],
				[1,0],
				[1,2]])
```

```python
#筛选生成索引
a = torch.tensor([9.3,4.2,8.5,2.7,5.9])
b = torch.nonzero(a>6,astuple=False)

b:
tensor[[0],
			 [2]]
#根据索引生成数据
c = torch.index_select(a,dim,index=b.sequeeze())
```

