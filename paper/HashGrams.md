# **Hash-Grams: Faster N-Gram Features for Classification and Malware Detection**

## 1、Background

- 论文链接 [Hash-Grams](https://www.edwardraff.com/publications/hash-grams-faster.pdf)
- 背景困境：在处理大语料数据上选 top-k个n-gram 是存在瓶颈的。

![image-20220602025854518](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20220602025854518.png)

- 相关工作有两个
  - 关于hash 算法
  - 关于top-k流处理

![image-20220602041734284](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20220602041734284.png)

## 2、Algorithm 

![image-20220602041638003](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20220602041638003.png)

1. 创建大小为$B$的array T, $B$ = $2^{31} −19$ 表内所有值为0
2. 遍历所有语料，依次计算所有n-gram的 hash  $h(q)$
3. 计算的hash值 对$B$取余数，得到结果$q^\prime$  $q^\prime$ 表示 array T的索引
4. array T 对应$q^\prime$ 索引的地方$+=1$
5. 遍历完成后，对array T 做快排 选出 top-k个

## 3、Theory

- 存在抽屉原理（Pigeonhole Principle）会导致top-k 个哈希值有碰撞（collide）

![image-20220602043124656](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20220602043124656.png)

- **hash gram 服从齐夫分布 Hash-Gramming under the Zipfian Distribution**  

- **齐夫分布** [齐夫定律维基百科](https://zh.m.wikipedia.org/zh/%E9%BD%8A%E5%A4%AB%E5%AE%9A%E5%BE%8B)

  ![{\displaystyle f(k;s,N)={\frac {1/k^{s}}{\sum \limits _{n=1}^{N}(1/n^{s})}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/64591d55c52d25dbe74f0aea6e9ba9e799623923)

  其中 $k$ 代表频率排名名次；$N$代表所有的元素数量；$s$ 代表指数参数；$f()$代表排名为k的元素的频率

- 数学证明在**服从齐夫分布的情况下**哈希碰撞导致非top-k的元素被选中的几率是很小的。

  ![image-20220602051757797](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20220602051757797.png)

- 数学证明的泛解释

![image-20220602055001615](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20220602055001615.png)

1. **从数学角度，**一共六个公式，式子一个比一个复杂。整个证明思路大概就是利用齐夫分布算各种条件频率，计算本来不在top-k，但错误的进入了top-k的概率。利用切比雪夫不等式（类似正太分布里面$3\sigma$ 的东西）证明这个概率是很低的。
2. **从感知角度，**这种概率低的原因是语料虽大2TB，元素虽多$N=6^{256}$，但受齐夫分布的影响，数据集里的n-gram会大量重复，所有的n-gram大概就只有$L=500,000$ ，而$B=2^{31}-19$所以L远小于$B$ 自然抽屉原理的影响就很小。

## 4、Experimental

![image-20220602060744500](C:\Users\John\AppData\Roaming\Typora\typora-user-images\image-20220602060744500.png)

## 5、Code

