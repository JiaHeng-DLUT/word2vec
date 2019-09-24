# Introduction to word2vec

* word2vec 就是用一个一层的神经网络（CBOW 的本质）把 one-hot representation 的词向量映射为 distributed representation 的词向量，为了加快训练速度，用了 Hierarchical Softmax，Negative Sampling 等 tricks。
* statistical language model: 统计语言模型就是给你几个词，在这几个词出现的前提下来计算某个词出现的（事后）概率。
* Continuous Bag of Words Model: 根据某个词前面的C个词或者前后C个连续的词，来计算某个词出现的概率。
* Skip-Gram Model: 根据某个词，然后分别计算它前后出现某几个词的各个概率。
* 然后再跟另一个NxV大小的系数矩阵W2相乘得到1xV的输出层，这个输出层每个元素代表的就是词库里每个词的事后概率。输出层需要跟ground truth也就是“爱”的one hot形式做比较计算loss。这里需要注意的就是V通常是一个很大的数比如几百万，计算起来相当费时间，除了“爱”那个位置的元素肯定要算在loss里面，word2vec就用基于huffman编码的Hierarchical softmax筛选掉了一部分不可能的词，然后又用nagetive samping再去掉了一些负样本的词所以时间复杂度就从O\(V\)变成了O\(logV\)。Skip gram训练过程类似，只不过输入输出刚好相反。
* 训练完成后对于某个词就可以拿出它的1xN的隐藏层作为词向量，就可以w2v\(中国\)－w2v\(北京\)＝w2v\(法国\)－w2v\(巴黎\)了。

### References

1. [无痛理解word2vec](https://zhuanlan.zhihu.com/p/22477976)
2. 
