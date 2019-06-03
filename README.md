# WeiboSentiment
基于FastText的中文微博情感分析  
微博语料来源： https://github.com/dengxiuqi/weibo2018  
#### 主要工作
* 用FastText生成词向量
* 结合Tf-Idf和词向量生成句向量
* 分别用SVM, 神经网络, LSTM和基于Attention的LSTM训练分类器
* 用训练的模型对不同话题下的100条微博文本进行情感分类

#### 实验结果
不同分类器在测试集上的测试结果  

|模型|准确率|
| :---: | :---: |
|SVM|0.82|
|神经网络|0.81|
|LSTM|0.854|
|Attention+LSTM|0.86|

用效果最好的Attention+LSTM对不同主题语料进行情感分析(每个主题都有100条语料)  

|主题|正面:负面|
| :---: | :---: |
|同济大学|88:12|
|周杰伦|88:12|
|好莱坞|79:21|
|人工智能|79:21|
|毕业|78:22|
|特朗普|55:44|

#### 工程结构
WeiboSentiment  
├── model `各种模型`   
│　　├── model_100.txt `维度为100的FastText词向量`   
│　　├── attention `Attention+LSTM模型`   
│　　├── lstm `LSTM模型`    
│　　└── nn `神经网络模型`   
├── weibo2018 `微博语料数据`   
│　　├── topics `未标注情感的不同主题微博语料`   
│　　├── train.txt `训练集`   
│　　└── test.txt `测试集`   
├── FastText.ipynb `生成FastText词向量`  
├── Attention.ipynb `Attention+LSTM分类器`  
├── LSTM.ipynb `LSTM分类器`  
├── NN.ipynb `神经网络分类器`  
├── SVM.ipynb `SVM分类器`      
├── stopwords.txt `停用词典`      
└── utils.py　 `工具函数` 　

#### 结果
在测试集上均取得0.8+的正确率