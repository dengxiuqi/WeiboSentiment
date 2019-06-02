# WeiboSentiment
基于FastText的中文微博情感分析  
数据来源： https://github.com/dengxiuqi/weibo2018  
#### 主要工作
* 用FastText生成词向量
* 结合Tf-Idf和词向量生成句向量
* 分别用SVM和神经网络训练分类器

#### 结果
在测试集上均取得0.8+的正确率