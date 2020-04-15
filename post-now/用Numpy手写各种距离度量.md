用`Numpy` 实现常见的几种距离度量。

# 欧氏距离(Euclidean distance)

<center><img src="https://s1.ax1x.com/2020/04/12/GOnylT.png" alt="GOnylT.png" border="0" /></center>

```python
def euclidean(x, y):
    return np.sqrt(np.sum((x - y)**2))
```

# 曼哈顿距离(Manhattan distance)

<center><img src="https://s1.ax1x.com/2020/04/12/GOuVNn.png" alt="GOuVNn.png" border="0" /></center>

```python
def manhattan(x, y):
    return np.sum(np.abs(x - y))
```

# 切比雪夫距离(Chebyshev distance)

<center><img src="https://s1.ax1x.com/2020/04/12/GOuRv8.png" alt="GOuRv8.png" border="0" /></center>

```python
def chebyshev(x, y):
    return np.max(np.abs(x - y))
```

# 闵可夫斯基距离(Minkowski distance)

<center><img src="https://s1.ax1x.com/2020/04/12/GOKCP1.png" alt="GOKCP1.png" border="0" /></center>

```python
def minkowski(x, y, p):
    return np.sum(np.abs(x - y) ** p) ** (1 / p)
```

# 汉明距离(Hamming distance)

<center><img src="https://s1.ax1x.com/2020/04/12/GOKgo9.png" alt="GOKgo9.png" border="0" /></center>

```python
def hamming(x, y):
    return np.sum(x != y) / len(x)
```

# 马氏距离(Mahalanobis Distance)

<center><img src="https://s1.ax1x.com/2020/04/12/GOM66f.png" alt="GOM66f.png" border="0" /></center>

```python
def mahalanobis(x,y):
    X=np.vstack([x,y])
    XT=X.T
    SI = np.linalg.inv(np.cov(X)) #协方差矩阵的逆矩阵
    #马氏距离计算两个样本之间的距离，此处共有10个样本，两两组合，共有45个距离。
    n=XT.shape[0]
    d1=[]
    for i in range(0,n):
        for j in range(i+1,n):
            delta=XT[i]-XT[j]
            d=np.sqrt(np.dot(np.dot(delta,SI),delta.T))
            d1.append(d)
    return d1
```

# 标准化欧氏距离 (Standardized Euclidean distance)

<center><img src="https://s1.ax1x.com/2020/04/12/GOQFBD.png" alt="GOQFBD.png" border="0" /></center>

```python
def standardized-euclidean(x,y):
    return np.sqrt(((x - y) ** 2 /np.var(np.vstack([x,y]),axis=0,ddof=1)).sum())
```

# 皮尔逊相关系数(Pearson correlation coefficient)

<center><img src="https://s1.ax1x.com/2020/04/12/GOllxx.png" alt="GOllxx.png" border="0" /></center>

```python
def pearson(x,y):
    return np.corrcoef(x, y)
```

# 余弦相似度(Cosine similarity)

<center><img src="https://s1.ax1x.com/2020/04/12/GOlXWR.png" alt="GOlXWR.png" border="0" /></center>

```python
def cos_sim(x, y):
    x = np.mat(x)
    y = np.mat(y)
    num = float(np.vstack([x,y]) * y.T)
    denom = np.linalg.norm(np.vstack([x,y])) * np.linalg.norm(y)
    cos = num / denom
    sim = 0.5 + 0.5 * cos
    return sim
```

# 杰卡德相似度(Jaccard index)

<center><img src="https://s1.ax1x.com/2020/04/12/GO1VSI.png" alt="GO1VSI.png" border="0" /></center>

```python
def Jaccrad(model, reference):#terms_reference为源句子，terms_model为候选句子
    terms_reference= jieba.cut(reference)#默认精准模式
    terms_model= jieba.cut(model)
    grams_reference = set(terms_reference)#去重；如果不需要就改为list
    grams_model = set(terms_model)
    temp=0
    for i in grams_reference:
        if i in grams_model:
            temp=temp+1
    fenmu=len(grams_model)+len(grams_reference)-temp #并集
    jaccard_coefficient=float(temp/fenmu)#交集
    return jaccard_coefficient
```






