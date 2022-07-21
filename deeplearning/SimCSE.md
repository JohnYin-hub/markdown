### 无监督SimCSE  Loss   torch方案

```python
def compute_loss(y_pred,lamda=0.05):
    idxs = torch.arange(0,y_pred.shape[0],device='cuda')
    y_true = idxs + 1 - idxs % 2 * 2
    similarities = F.cosine_similarity(y_pred.unsqueeze(1), y_pred.unsqueeze(0), dim=2)
    #torch自带的快速计算相似度矩阵的方法
    similarities = similarities-torch.eye(y_pred.shape[0],device='cuda') * 1e12
    #屏蔽对角矩阵即自身相等的loss
    similarities = similarities / lamda
    #论文中除以 temperature 超参 0.05
    loss = F.cross_entropy(similarities,y_true)
    return torch.mean(loss)
```

### 有监督监督SimCSE  Loss    torch方案

```python
def compute_loss(y_pred,lamda=0.05):
    row = torch.arange(0,y_pred.shape[0],3,device='cuda')
    col = torch.arange(y_pred.shape[0], device='cuda')
    col = torch.where(col % 3 != 0)[0].cuda()
    y_true = torch.arange(0,len(col),2,device='cuda')
    similarities = F.cosine_similarity(y_pred.unsqueeze(1), y_pred.unsqueeze(0), dim=2)
    #torch自带的快速计算相似度矩阵的方法
    similarities = torch.index_select(similarities,0,row)
    # 按行选取 x
    similarities = torch.index_select(similarities,1,col)
    # 按列选取xj+ 与 xj-
    similarities = similarities / lamda
    #论文中除以 temperature 超参 0.05
    loss = F.cross_entropy(similarities,y_true)
    return torch.mean(loss)
```

### 无监督SimCSE  Loss  tensorflow 方案

![image-20220331191026672](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20220331191026672.png)