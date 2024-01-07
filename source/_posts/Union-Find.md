---
title: Union Find
date: 2022-08-31 09:37:01
---

### 前言

并查集在打竞赛的时候就学过了，现在差不多过了两年半，重拾算法，认真学学。当时在学的时候完全不理解并查集是什么意思，只能说当文科背了。认真看了英文版的ALgorithm 4th，才完全理解了这个并、查是什么意思，集应该是集合，也有可能是数据结构的意思，不知道是谁翻译的。如果阅读CS相关的书，尤其是基础书(即前置知识只需要你会写代码即可)，我推荐看英文版。虽然一开始看的很辛苦，但是一旦进入状态，基本能够了解作者想要告诉你什么，而且书里面的英语基本上是英文的大白话，除去几个专有名词需要查一下，其他基本上都是高中学过的单词。希望我能通过这段时间的英文教材阅读来练习自己以后阅读英文文档的能力吧。
关于并查集，我们直接看英文，Union - Find，Union即为并，即链接，Find为查找，查找出所在的集合。之所以叫这个名字，是因为Union和Find这两个方法是必不可少的，而且后续讨论优化也是在这两个方法中优化。

### 并查集

#### 特性

当我们说p q时，即说p连接了q，然后有以下特点 ：

- 反身性：p自身连接自己
- 对称性：如果p连接了q，则q连接了p
- 传递性：如果p连接了q且q连接了r，则p连接了r 

```csharp
public class UF
{
    UF(int N)//初始化
    void Union(int p,int q)//连接p和q，即让他们在同一个集合
    int Find(int p)//找到p所在的集合
    bool Connected(int p,int q)//判断p和q点是否在同一个集合
    int Count()//返回有多少个集合
}
```

简单来说，并查集就是让一个一个孤立的点连在一起，连在一起的点有一个共同的集合

#### 基本架构实现

这里给出基本架构，可以看到，需要更改的基本上是Find和Union

```csharp
public class UF
{
    private int[] id;//集合的id
    private int count;

    public UF(int N)
    {
        count = N;
        id = new int[N];
        for(int i = 0; i < N; i++)
            id[i] = i ;
    }

    public int Count()
    {
        return count;
    }

    public bool Connected(int p, int q)
    {
        return Find(p)==Find(q);
    }

    public int Find(int p)//Find函数，后面会实现

    public void Union(int p,int q)//Union函数，后面会实现
}
```

#### Quick-Find实现

先来快速看看实现的代码

```csharp
public int Find(int p)
{
    return id[p];
}
public void Union(int p, int q)
{
    int pId = Find(p);
    int qId = Find(q);
    if(pID == qID) return ;
    for(int i=0; i < id.Length; i++)
        if(id[i] == pId) 
            id[i] = qId;
    count--;
}
```

其实这里很简单，id就是p所在的集合编号，如果在Union中两个id不同，那么就会遍历全部集合，如果遍历到的点都属于p所在的集合，那么我们把遍历到的点的id改为q所属的集合的id。

不过我们想想，Find的时间复杂度为 O(1),而Union的时间复杂度为 O(N)。假设我们仅仅使用了N-1次连接我们就可以使整个连接成一个集合，那时间复杂度也至少是 N*(N-1),也就是O(N^2)，那当N大的时候消耗的时间将会很多。所以接下来我们来优化一下Union方法。

#### Quick-Union实现

先来快速看看两个方法里的代码

```csharp
public int Find(int p)
{
    while(p != parent[p]) 
        p = parent[p];
    return p;
}
public void Union(int p,int q)
{
    int pRoot = Find(p);
    int qRoot = Find(q);
    if(pRoot == qRoot) return ;
    id[pRoot] = qRoot;
    count--;
}
```

我们可以看到Find和Union做了些许改变，parent和root可以让我们很快的联想到树的结构，我们将树根作为集合的编号，这样子Union仅仅需要O(1)即可完成一次连接，而Find消耗的时间复杂度虽然变多了，但是还是可以接受的。不过这并不是一个稳定的算法，假如Union将树形集合连接成了一个树链，那么Find的总时间就会变为(1+2+...N) ~ N^2/2 ~ N^2,虽然最坏的情况也会比之前Quick-Find快，但是作为O(N^2)级别的时间复杂度，当数据量足够大也与Quick-Find差别不大。所以我们可以改变连接的方式，避免树链的出现。

#### Weighted Quick-Union 实现

先来看看这次的Union代码，Find实现没有变，这次我们增加了一个Weight的实现,即树的权重(以集合里面有多少个点来计算，如果有N个点，则Weight为N)，加权树有一个特点，它可以保证树的最大深度<=lgN，因为不可能有树链的情况产生，且保证较小的树是直接加到根上的，这样最多仅仅让树的深度 +1

```csharp
public void Union()
{
    int pRoot = Find(p);
    int qRoot = Find(q);
    if(pRoot == qRoot) return ;
    if(weight[pRoot] < weight[qRoot]) 
    {
        parent[pRoot] = qRoot; 
        weight[qRoot] += weight[pRoot];
    }
    else 
    {
        parent[qRoot] = pRoot;
        weight[pRoot] +=weight[qRoot];
    }
    count--;
}
```

我们在这次Weighted Quick-Union做的改变就是尽可能地让小树直接连在大树的根上，这样子基本上不会出现有树链的情况。我们来证明一下，假设让小树直接连接在大树的根上，设两棵树的权重分别为 i ，j 且 i <= j，设 i+j = k,大树本身所需要的遍历时间不变，而小树的最大遍历时间会增加 1 ,即最大遍历时间变为 1 + lgi = lg(i+i) <= lg(i+j) = lg(k)，即 lgk 最多可能等于 lgi + 1。所以可以保证最坏时间复杂度为 N*(2*lgN)即为O(NlgN)。

我们可以更加极限一点，让每个点直接连着根，即路径压缩

#### Weighted Quick-Union with Path Compression 实现

我们仅仅需要在Find中爬树的过程中将爬过的点直接附着在根上，这样可以保证树的深度在Find后很难超过2，使时间复杂度接近 1

```csharp
public int Find(int p)
{
    int root = p;
    //首先先找出根
    while (root != parent[root])
        root = parent[root];
    //然后再次找根在遍历的过程中把每个节点直接附着在根上
    while (p != root)
    {
        int newp = parent[p];
        parent[p] = root;
        p = newp;
    }
    return root;
}
```

### Algorithm配套习题

由于配套习题实在是太多了，我们这里只看网站上提供的题目

**1.5.8** 给出反例来说明为什么这个quickFind中的Union方法是错误的

```csharp
public void union(int p, int q) {
   if (connected(p, q)) return;
   for (int i = 0; i < id.length; i++)
      if (id[i] == id[p]) id[i] = id[q];
   count--;
}
/*对比
public void Union(int p, int q)
{
    int pId = Find(p);
    int qId = Find(q);
    if(pID == qID) return ;
    for(int i=0; i < id.Length; i++)
        if(id[i] == pId) 
            id[i] = qId;
    count--;
}
*/
```

答：我们可以看到for循环中id[i] == id[p]这里，在遍历中，我们可能改变了id[p]的值，比如(id[i] == id[p],i==p)，这样子当 i > p 时，后面的都会失效。

**1.5.10** 在Weighted Quick-Union中，假设我们让id[rootp] == q 来代替id[rootp]==id[rootq].算法的结果会出错吗？

```csharp
public void Union()
{
    int pRoot = Find(p);
    int qRoot = Find(q);
    if(pRoot == qRoot) return ;
    if(weight[pRoot] < weight[qRoot]) 
    {
        parent[pRoot] = qRoot; 
        //parent[pRoot] = q;
        weight[qRoot] += weight[pRoot];
    }
    else 
    {
        parent[qRoot] = pRoot;
        weight[pRoot] +=weight[qRoot];
    }
    count--;
}
```

答：不会.但是这样子不能让小树直接附着在大树的根上，这样时间复杂度并不能达到我们想要的效果。

#### 算法网址及Github代码

有一些部分题目是写代码，直接放在github中了，可以看看网址，有图助于理解

- <https://algs4.cs.princeton.edu/15uf/>
- <https://github.com/talentstream/Algorithm-4th-Practice-/tree/main/Union-Find>
