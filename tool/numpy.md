# numpy 创建向量

- #### np.array 直接创建，接受list或tuple参数

```python
print(np.array([1,2,3]))
print(np.array([[1,2,3],[4,5,6]]))
print(np.array((1,2,3)))
```

- #### np.arange 创建等差矩阵或者向量

```python
print(np.arange(1, 10, 2)) 	#参数为：(起始点，终点，步长)；注意！ 不包括终点
print(np.arange(20))  		# 参数为一个值，直接定义。 0-19，不包涵20.步长默认为一
#第二种用法可以联系python的range记忆，功能和拼写类似。
for i in range(10):
    print(i)
```

- #### 整数与正太分布

```python
np.random.randn(2,3,4)  正态
np.random.randint(1,100,10)  # 随机10个数,范围从1到100,构成向量
np.random.randint(1,13,[2,3]) # 随机2行3列的矩阵,值从1到13随机
np.random.randint(low=1, high=13, size=[2, 3]) #同上
```

- #### np.zeros 创建全部为零的矩阵或者向量

```python
#用tuple表示形状
print(np.zeros((3,3)))
```

- #### np.ones创建全部为一的矩阵或者向量

```python
print(np.ones((3,3)))
# 利用dtype属性直接创建相应类型的矩阵
print(np.zeros((3,4), dtype = bool))
print(np.ones((3,4), dtype = bool))
```

- #### np.random.random 产生0-1 之间的随机数（不包含1）

```python
#参数为一个整形：生成包含3个0-1之间的数的向量
print(np.random.random(3))
#参数为tuple
print(np.random.random((2,3)))   #产生特定形状的0-1之间的矩阵,这里参数用list也可以但是不推荐。
```

- #### np.random.rand 功能同random.random 但是参数有差别

```python
#rand 直接接受int型参数表示shape , random接受list或tuple
print(np.random.rand(3,5))
print(np.random.rand([3,5])) # 报错
print(np.random.rand((3,5))) # 报错
print(np.random.random(3,4)) # 报错 
```

- ##### np.linspace 创建等差向量或矩阵

```python
#参数：(起始点，终点，分割份数) 注意！包括终点
print(np.linspace(0, 10, 5))  # => [ 0. ,  2.5,  5. ,  7.5, 10. ]   
#注意！与arange的区别， arange定义步长，linspace定义等差元素的个数。 
```

- ##### np.logspace 创建等差指数向量或矩阵

```python
#logspace(start, stop, num, endpoint=True, base=10.0, dtype=None, axis=0,) 创建base为底的等距元素个数的指数矩阵， 前三个参数与linspace()效果一致。
# 创建以 2 为底，1-10产生等差数列包含10个值，那么这个数列就是1到10，这十个值将会成为2的指数生成向量： 
print(np.logspace(1, 10, 10, base = 2))
# 1-10产生等差数列包含3个值： 1 5.5 10 ，这三个值将会成为2的指数生成向量。
print(np.logspace(1, 10, 3, base = 2))
# 1-10产生的等差数列包含四个值： 1 4 7 10，这四个值将会成为2的指数生成向量。
print(np.logspace(1, 10, 4, base = 2))
```

- #### np.diag 获取或创建对角线向量

```python
# diag(v,k=0) 创建对角线数组 v 只能是一维或二维矩阵
# 如果v是一维返回以v为对角线的二维数组
# 如果v是二维返回k位置的对角线数组
# v是一维
print(np.diag([1,2,3,4]))
print(np.diag((1,2,3,4)))
# 对角线偏移 k>0 向右偏反之向左偏，偏移之后会保证[1,2,3,4]完整
print(np.diag([1,2,3,4], k = 1)) # 主对角线偏移 1 的矩阵
print(np.diag([1,2,3,4], k = -1)) # 主对角线偏移 1 的矩

# v是二维
a = np.arange(1, 10, 1).reshape(3,3)
print(a)
print(np.diag(a)) 			#返回主对角线向量
print(np.diag(a, k = 1))	#返回右偏移1的对角线向量

# v 是三维 报错
a = np.arange(1, 19, 1).reshape(3,3,2)
print(a)
print(np.diag(a))  #ValueError: Input must be 1- or 2-d
```