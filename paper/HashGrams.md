# **Hash-Grams: Faster N-Gram Features for Classification and Malware Detection**

## 1、Background

- 论文链接 [Hash-Grams](https://www.edwardraff.com/publications/hash-grams-faster.pdf)
- 背景困境：在处理大语料数据上选 top-k个n-gram 是存在瓶颈的。

![image-20220829134818950](https://tva1.sinaimg.cn/large/e6c9d24ely1h5nl7upas1j20zo04vdi2.jpg)

- 相关工作有两个
  - 关于hash 算法
  - 关于top-k流处理

![image-20220829134848230](https://tva1.sinaimg.cn/large/e6c9d24ely1h5nl8cl2l8j20np02b74z.jpg)

## 2、Algorithm 

![image-20220829134913959](https://tva1.sinaimg.cn/large/e6c9d24ely1h5nl8qo7blj20ke0dpdia.jpg)

1. 创建大小为$B$的array T, $B$ = $2^{31} −19$ 表内所有值为0
2. 遍历所有语料，依次计算所有n-gram的 hash  $h(q)$
3. 计算的hash值 对$B$取余数，得到结果$q^\prime$  $q^\prime$ 表示 array T的索引
4. array T 对应$q^\prime$ 索引的地方$+=1$
5. 遍历完成后，对array T 做快排 选出 top-k个

## 3、Theory

- 存在抽屉原理（Pigeonhole Principle）会导致top-k 个哈希值有碰撞（collide）

![image-20220829134938257](https://tva1.sinaimg.cn/large/e6c9d24ely1h5nl95m1l4j20ns034q42.jpg)

- **hash gram 服从齐夫分布 Hash-Gramming under the Zipfian Distribution**  

- **齐夫分布** [齐夫定律维基百科](https://zh.m.wikipedia.org/zh/%E9%BD%8A%E5%A4%AB%E5%AE%9A%E5%BE%8B)

  ![image-20220829142658564](https://tva1.sinaimg.cn/large/e6c9d24ely1h5nmc2ynb3j206n02zdfo.jpg)

  其中 $k$ 代表频率排名名次；$N$代表所有的元素数量；$s$ 代表指数参数；$f()$代表排名为k的元素的频率

- 数学证明在**服从齐夫分布的情况下**哈希碰撞导致非top-k的元素被选中的几率是很小的。

  ![image-20220829134955980](https://tva1.sinaimg.cn/large/e6c9d24ely1h5nl9hv7foj20j606rq51.jpg)

- 数学证明的泛解释

![image-20220829135020530](https://tva1.sinaimg.cn/large/e6c9d24ely1h5nl9vu2pmj20cv0c3jta.jpg)

1. **从数学角度，**一共六个公式，式子一个比一个复杂。整个证明思路大概就是利用齐夫分布算各种条件频率，计算本来不在top-k，但错误的进入了top-k的概率。利用切比雪夫不等式（类似正太分布里面$3\sigma$ 的东西）证明这个概率是很低的。
2. **从感知角度，**这种概率低的原因是语料虽大(2TB)，元素虽多($N=6^{256}$)，但受齐夫分布的影响，数据集里的n-gram会大量重复，所有的n-gram大概就只有$L=500,000$ ，而$B=2^{31}-19$，故L远小于$B$ 自然抽屉原理的影响就很小。

## 4、Experimental

![image-20220829135044522](https://tva1.sinaimg.cn/large/e6c9d24ely1h5nlaau2btj20m9090abb.jpg)

## 5、Code

