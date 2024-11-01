# testgithub


双塔模型实现前交叉：生成query或者user塔的伪向量，然后和item塔进行提前交互，得到最终的item向量。
<img width="329" alt="image" src="https://github.com/user-attachments/assets/5bb93e6d-9804-4c98-a406-50e39fee122a">

<img width="299" alt="image" src="https://github.com/user-attachments/assets/f6f6d8dd-d3a6-44d1-9674-94c41b1e6bca">



LTV预估或者观看时长预估。
最终消费金额预估，那么预估LTV这个回归问题的核心难点在于：整个群体的数据分布中，混合了如：泊松、指数等多种分布。其实包括观看时长预估也常常是不规则的回归分布。
这其中有一个大的问题是0附近数目比较多，其他部分容易不规则，最后观看时长，最终消费金额很难预估。
三种方法：
1）使用0膨胀正太分布损失函数，即在0附近使用二类分布，在其他地方使用回归分布
2）整体标签取对数，这样可以变成正态分布，容易拟合。
3）时长回归很难预估，可以变成分类模型，即要求a的观看时长比b的观看时长更长就行， 这个比较容易预估。



memonet： 探索推荐模型的scaling law，其实证明了所有的二阶cross-feature更有效的使用方式，是压缩（multi-hash编码避免冲突）和重建（每个使用mlp或者一阶特征attention来重建）---神经网络第一性原理。
a）In order to explain the success of large language models, many recent works[2, 23, 28, 34] discuss the memorization and generalization ability of these models. Some works[10, 16, 24] show that big models in NLP have great capabilities to memorize factual world knowledge cross feature is almost the most important knowledge contained in data of CTR tasks.introducing an independent memory mechanism into CTR ranking model to learn and memorize cross features’ representations
b）编码压缩使用"multi-hash codebook" 。segments the representation of cross feature into 𝑚 chunks and each chunk indicated by a different hash function represents part of the complete information. This helps distinguish cross features from each other in the same codeword because the probability of sharing the same representation exponentially decreases with the increase of hash function number
c）重建，使用网络重建二阶交叉特征的表示，一种是mlp，一种是使一阶特征attention来重建。第二种Attentive Memory Restoring(AMR)就是原始的一阶特征的embedding做attention，提取二阶cross-feature特征里边的信息，以去除多个cross-feature在coding-book里边冲突的信息。We find AMR outperforms LMR when the codeword number is relatively small while LMR performs better if we continue to increase the codeword’s number. T
d）. 特征缩减。二阶特征有噪声，且太多。用一阶特征做attention，去除一些二阶特征（按照一阶维度去掉，即某些特征相关的二阶特征都存在或者都不存在）。
e）效果 auc+0.01
