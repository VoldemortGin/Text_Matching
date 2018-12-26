# Text\_Matching

## 文本匹配算法

### Lexical级别

向量化

可以利用cosine相似性，求查询向量和文档向量的夹角，越小越相似。

提取词，文本向量中词对应的值可以是**0/1值**，0代表词在文本中出现过，1代表词在文本中未出现过；可以是**TF值**（词频）；可以是**DF值**（文档频率，DF越高表示单词越普遍，因此其区分度越低，其权重也越低）；可以是**TF-IDF值**，可以是**N-Gram**，可以是**Embedding**（词级别Embedding、文档级别Embedding）。

基于语意的特征提取方法：基于语境框架的文本特征提取方法、基于本体论的文本提取方法、基于知网的概念特征提取方法等。

[一种基于N一Gram改进的文本特征提取算法](https://wenku.baidu.com/view/d4976f0bf78a6529647d5369.html)

[基于N-Gram文本特征提取的改进算法](http://xueshu.baidu.com/s?wd=paperuri%3A%28f2da6e23f512901233f8c0603df9fe5d%29&filter=sc_long_sign&tn=SE_xueshusource_2kduw22v&sc_vurl=http%3A%2F%2Fkns.cnki.net%2FKCMS%2Fdetail%2Fdetail.aspx%3Ffilename%3DXDJS201234000%26dbname%3DCJFD%26dbcode%3DCJFQ&ie=utf-8&sc_us=5068616763849130906)

影响词权值的因素：词频、词性、文档频次、标题（例如可以初步设定标题的位置权重为5，摘要和结论部分为3，正文为1）、位置、句法结构、专业词库、信息熵、文档/词语长度、词语间关联、单词区分能力、词语直径（比较粗糙的度量特征）、首次出现位置、词语分布偏差（例如词汇在文章出现的平均位置）。

TF（不宜根据词频大幅度删词）、DF（根据预先设置阈值去除文档频次特别低或者特别高的特征，他们分别代表了没有代表性和没有区分度两种极端的情况）、TF-IDF、信息增益、互信息、期望交叉熵、二次信息熵（QEMI）、卡方统计量可以用做词降维。

互信息：

互信息(Mutual Information)是信息论里一种有用的信息度量，它可以看成是**一个随机变量中包含的关于另一个随机变量的信息量**，或者说是一个随机变量由于已知另一个随机变量而减少的不肯定性。

互信息理论进行特征抽取是基于如下假设：在某个特定类别出现频率高,但在其他类别出现频率比较低的词条与该类的互信息比较大。通常用互信息作为特征词和类别之问的测度，**如果特征词属于该类的话，它们的互信息量最大**。由于该方法不需要对特征词和类别之问关系的性质作任何假设，因此非常适合于文本分类的特征和类别的配准工作。

期望交叉熵：

交叉嫡也称KL距离。它**反映了文本主题类的概率分布和在出现了某特定词汇的条件下文本主题类的概率分布之间的距离**，词汇w的交叉嫡越大，对文本主题类分布的影响也越大。

它与KL距离不同之处在于加上了一个词的概率分布，原因是减少很多低频词出现在最终的特征集中。

它与信息增益唯一的不同之处在于没有考虑单词未发生的情况，只计算出现在文本中的特征项。

信息增益：

衡量标准是看特征能够为分类系统带来多少信息，带来的信息越多，该特征越重要。信息增益最大的问题在于它**只能考察特征对整个系统的贡献**，而**不能具体到某个类别上**，这就使得它**只适合用来做所谓“全局”的特征选择**（指所有的类都使用相同的特征集合），而**无法做“本地”的特征选择**（每个类别有自己的特征集合，因为有的词，对这个类别很有区分度，对另一个类别则无足轻重）。

信息增益方法的不足之处在于它考虑了特征未发生的情况。特别是在类分布和特征值分布高度不平衡的情况下，绝大多数类都是负类，绝大多数特征都不出现。此时的函数值由不出现的特征决定，因此，信息增益的效果就会大大降低。信息增益表现出的分类性能偏低。因为信息增益考虑了文本特征未发生的情况，虽然特征不出现的情况有可能对文本类别具有贡献，但这种贡献往往小于考虑这种情况时对特征分值带来的干扰。

卡方统计量：

计算某个特征全局的Chi值，选择Chi值较大的特征。

### BM25

计算查询和文档之间的相关性。对查询的分词进行语素分析，每个词看成语素Qi；D表示一个结果文档，Wi表示语素Qi的权重。计算语素Qi和与文档D的相关性得分。Wi的计算：较常用的是IDF。

要点在于语素分析、语素权重判定、语素与文档的相关性判定。

综合来看，BM25考虑了4个因素：IDF因子、文档长度因子、文档词频因子和查询词频因子。

### 基于语义相似度的文本相似度算法

语义相关度计算获得相似度矩阵的方向有两个：基于知网HowNet或者基于WordNet。

[文本相似度算法](https://www.cnblogs.com/liangxiaxu/archive/2012/05/05/2484972.html)

## 参考

[原创:史上对BM25模型最全面最深刻的解读以及lucene排序深入讲解](http://www.mamicode.com/info-detail-1701866.html)

[经典检索算法：BM25原理](https://www.jianshu.com/p/53e379483f3e)

[搜索中的权重度量利器: TF-IDF和BM25](https://my.oschina.net/stanleysun/blog/1617727)

[搜索引擎的文档相关性计算和检索模型（BM25/TF-IDF）（很好的一篇文章，介绍了很多特征提取方法）](https://blog.csdn.net/heiyeshuwu/article/details/43429447)

[特征选择之卡方检验](https://www.jianshu.com/p/b670b2a23187)
