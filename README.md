# WeiboSentiment
基于各种机器学习和深度学习的中文微博情感分析    
语料来源： https://github.com/dengxiuqi/weibo2018   
##### "情感分析"是我本科的毕业设计, 也是我入门并爱上NLP的项目hhh, 就把它发出来供大家交流    
##### 转载引用, 请注明来源谢谢~

* 用FastText在语料库上训练并生成词向量, 该任务语料库较小, 用fastText可以增加n-gram特征, 比传统word2vec要好    
* 训练集10000条语料, 测试集500条语料     
* 分别用SVM, Bayes, DNN, LSTM, Attention+BiLSTM, XGBoost等多种模型搭建并训练`正负情感二分类器`
    * `SVM`其实不太适合做NLP, 只是当年我还很菜所以选了SVM(尬笑), 出于情怀就贴上来了
    * `Bayes`速度快, 效果好。可能是因为该任务语料规模较小,在大规模语料任务上性能会下降,而且磁带模型丢失了语序信息,可拓展性不强(2020.2.13更新)
    * `DNN`效果不好, 不过现在也很少有直接用DNN做NLP的, 所以这里仅作为从机器学习到深度学习的过渡模型了
    * `LSTM`用到了上游训练的FastText词向量, 并且考虑了语序信息, 效果有明显提升
    * `Attention+BiLSTM`效果很好, 但相比纯LSTM提升没那么明显，主要是因为该任务相对简单且语料少。迁移至更复杂任务后注意力的强大会越来越明显
    * `XGBoost`真是机器学习界的一大杀器, 在这种简单的NLP任务上真是又快又好(2020.6.4更新)
* 对不同话题下的100条微博进行简单的舆情分析(正负情感微博比例)

#### 实验结果
各种分类器在测试集上的测试结果  

|模型|准确率|
| :---: | :---: |
|XGBoost|0.874|
|Attention+BiLSTM|0.86|
|Naive Bayes|0.856|
|LSTM|0.854|
|SVM|0.82|
|DNN|0.81|

#### 舆情分析
数据来自于2018年6月的微博

|主题|正面:负面|
| :---: | :---: |
|特朗普|55:44|
|周杰伦|88:12|
|好莱坞|79:21|
|人工智能|79:21|
|毕业|78:22|

#### 工程结构

    WeiboSentiment   
    ├── 00.FastText.ipynb `生成FastText词向量`  
    ├── 01.SVM.ipynb `SVM分类器`  
    ├── 02.Bayes.ipynb `朴素贝叶斯`  
    ├── 03.DNN.ipynb `神经网络分类器`  
    ├── 04.LSTM.ipynb `LSTM分类器`  
    ├── 05.Attention+BiLSTM.ipynb `Attention+BiLSTM分类器`  
    ├── 06.XGBoost.ipynb `XGBoost分类器`   
    ├── SentimentAnlysis.ipynb `验证集分析`  
    ├── stopwords.txt `停用词典`      
    ├── utils.py　 `工具函数` 　
    ├── model `各种模型`   
    │　　├── model_100.txt `维度为100的FastText词向量`   
    │　　├── attention `Attention+LSTM模型`   
    │　　├── lstm `LSTM模型`    
    │　　└── nn `神经网络模型`   
    └── weibo2018 `微博语料数据`   
     　　├── topics `未标注情感的不同主题微博语料`   
     　　├── train.txt `训练集`   
     　　└── test.txt `测试集`  

#### 结果
在测试集上均取得0.8+的正确率