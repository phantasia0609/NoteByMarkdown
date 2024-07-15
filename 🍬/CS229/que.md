批次梯度下降

随机梯度下降

马腾雨 back？

homework

李航《机器学习方法》

Theory 书籍 偏理论

Project 书籍 偏实践，会有代码

归一化

获取特征

numpy 部分有个 python 基础知识体系

python 类方法

speech recognition



> 机器学习的部分模型

- Linear Regression
- logistic regression 分类 task 
- softmax reg  分类 task
- SVM
- Decision Tree
- Naive Bayes（分类垃圾邮件）
- Kmeans（经典聚类）etc：Kmeans++改进的 Kmeans 算法，继承到了那个 s 什么库scikit-learn
- PCA
- ICA



| Task                     | Type         | Model                                                        |
| ------------------------ | ------------ | ------------------------------------------------------------ |
| Regression               | Supervised   | Linear Regression、SVR（SVM的分类，下面的 SVC 同理）、DTR（决策树的分类） |
| Classification           | Supervised   | logistic regression、softmax regression、SVC、DTC            |
| Clustering               | Unsupervised | Kmeans、Hierarchal clustering（层次聚类）                    |
| Dimensionality Reduction | Unsupervised | PCA（降维，可视性好）、ICA、t-SNE（也是降维，可解释性不好，但是可视化好） |



one hot 独热编码|



Kaggle 有些要做的题（具体哪些问问）



- DataSet 如下

| Label(Price) | #features: bedroom | distance | size |
| ------------ | ------------------ | -------- | ---- |
|              |                    |          |      |
|              |                    |          |      |
|              |                    |          |      |
|              |                    |          |      |
|              |                    |          |      |
|              |                    |          |      |
|              |                    |          |      |



- trainingSet
- testSet
- 训练集和测试集
- ValidationSet 验证集
- 一般会划分成这三个集合



$$
\begin{aligned}
\frac{x}{y} \\
\hat{x}
\dot{x}
\bar{x}
x^{2}
\end{aligned}
$$