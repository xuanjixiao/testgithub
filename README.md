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
