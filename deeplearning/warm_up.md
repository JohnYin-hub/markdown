# torch.optim.lr_scheduler 模块

`torch.optim.lr_scheduler`模块提供了一些根据epoch训练次数来调整学习率（learning rate）的方法。

#### lr_scheduler调整策略：根据训练次数

torch.optim.lr_scheduler中大部分调整学习率的方法都是根据epoch训练次数，这里介绍常见的几种方法，其他方法以后用到再补充。
要了解每个类的更新策略，可直接查看官网doc中的源码，每类都有个get_lr方法，定义了更新策略。

#### 2.1 torch.optim.lr_scheduler.LambdaLR

语法：

```
class torch.optim.lr_scheduler.LambdaLR(optimizer, lr_lambda, last_epoch=-1)
```


更新策略：
$$
new_{lr}=λ×initial_{lr}
$$
其中n e w _ l r new\_lrnew_lr是得到的新的学习率，i n i t i a l _ l r initial\_lrinitial_lr是初始的学习率，λ \lambdaλ是通过参数lr_lambda和epoch得到的。

#### 参数：

- optimizer （Optimizer）：要更改学习率的优化器；
- lr_lambda（function or list）：根据epoch计算$\lambda$的函数；或者是一个list的这样的function，分别计算各个parameter groups的学习率更新用到的$\lambda$；
- last_epoch （int）：最后一个epoch的index，如果是训练了很多个epoch后中断了，继续训练，这个值就等于加载的模型的epoch。默认为-1表示从头开始训练，即从epoch=1开始。

**注意：**在将optimizer传给scheduler后，在shcduler类的__init__方法中会给optimizer.param_groups列表中的那个元素（字典）增加一个key = "initial_lr"的元素表示初始学习率，等于optimizer.defaults['lr']。

```python
import torch
import torch.nn as nn
from torch.optim.lr_scheduler import LambdaLR

initial_lr = 0.1

class model(nn.Module):
    def __init__(self):
        super().__init__()
        self.conv1 = nn.Conv2d(in_channels=3, out_channels=3, kernel_size=3)

    def forward(self, x):
        pass

net_1 = model()

optimizer_1 = torch.optim.Adam(net_1.parameters(), lr = initial_lr)
scheduler_1 = LambdaLR(optimizer_1, lr_lambda=lambda epoch: 1/(epoch+1))

print("初始化的学习率：", optimizer_1.defaults['lr'])

for epoch in range(1, 11):
    # train

    optimizer_1.zero_grad()
    optimizer_1.step()
    print("第%d个epoch的学习率：%f" % (epoch, optimizer_1.param_groups[0]['lr']))
    scheduler_1.step()

```

```python
初始化的学习率： 0.1
第1个epoch的学习率：0.100000
第2个epoch的学习率：0.050000
第3个epoch的学习率：0.033333
第4个epoch的学习率：0.025000
第5个epoch的学习率：0.020000
第6个epoch的学习率：0.016667
第7个epoch的学习率：0.014286
第8个epoch的学习率：0.012500
第9个epoch的学习率：0.011111
第10个epoch的学习率：0.010000
下面解析关键行：
第1~3行
import一些包。
第7~13行
简单定义一个网络类，并没有实现网络应有的功能，只是用来定义optimizer的。
第15行
实例化一个网络。
第17行
实例化一个Adam对象。
第18行
实例化一个LambdaLR对象。lr_lambda是根据epoch更新lr的函数。
第20行
打印出初始的lr。optimizer_1.defaults保存的是初始的参数。
第22~28行
模仿训练的epoch。
第25～26行
更新网络参数（这里省略了loss.backward()）。
第27行
打印这一个epoch更新参数所用的学习率，由于我们只给optimizer_1传了一个net.parameters()，所以optimizer_1.param_groups长度为1。
第28行
更新学习率。
```

补充：
cycleGAN中使用torch.optim.lr_scheduler.LambdaLR实现了前niter个epoch用initial_lr为学习率，之后的niter_decay个epoch线性衰减lr，直到最后一个epoch衰减为0。

