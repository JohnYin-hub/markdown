# Pytorch Simcse loss

- #### 无监督SimCSE  Loss   torch方案

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

- #### 有监督监督SimCSE  Loss    torch方案


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

# Tensorflow SimCSE loss

- #### 无监督SimCSE  Loss  tensorflow 方案

```python
def simcse_loss(y_true, y_pred):
    """
    simcse loss
    """
    idxs = tf.range(0, tf.shape(y_pred)[0])
    idxs_1 = idxs[None, :]
    idxs_2 = (idxs + 1 - idxs % 2 * 2)[:, None]
    y_true = tf.equal(idxs_1, idxs_2)
    y_true = tf.cast(y_true, tf.keras.backend.floatx())
    y_pred = tf.math.l2_normalize(y_pred, axis=1)
    similarities = tf.matmul(y_pred, y_pred, transpose_b=True)
    similarities = similarities - tf.eye(tf.shape(y_pred)[0]) * 1e12
    similarities = similarities / 0.05
    loss = tf.keras.losses.categorical_crossentropy(y_true, similarities, from_logits=True)
    return tf.reduce_mean(loss)
```

- #### 有监督SimCSE Loss tensorflow 方案

```python
def simcse_hard_neg_loss(y_true, y_pred):
    """
    simcse loss for hard neg or random neg
    """
    row = tf.range(0, tf.shape(y_pred)[0], 3)
    col = tf.range(tf.shape(y_pred)[0])
    col = tf.squeeze(tf.where(col % 3 != 0), axis=1)
    y_true = tf.range(0, len(col), 2)
    y_pred = tf.math.l2_normalize(y_pred, axis=1)
    similarities = tf.matmul(y_pred, y_pred, transpose_b=True)
    similarities = tf.gather(similarities, row, axis=0)
    similarities = tf.gather(similarities, col, axis=1)
    similarities = similarities / 0.05
    loss = tf.keras.losses.sparse_categorical_crossentropy(y_true, similarities, from_logits=True)
    return tf.reduce_mean(loss)
```

