# Stock price prediction with LSTM + BERT.



## Introduction

**`Exchange rates and stock prices`** move randomly, and that makes it too hard to predict them with ordinary time-series prediction models. In orger to achive high accuracy in prediction, a number of study has been performed. Some of the studies show there is **a strong relationship between exchange rates & stock prices and news articles**. This comes from a obvious idea that they have to do with the state of the country and the world. Therefore, using news articles as features can be expected to improve prediction accuracy, and this effect has been confirmed in practice.

**`BERT`**(Bidirectional Encoder Representations from Transformers [1]) is the state-of-the-art NLP(Natural Language Processing) model as of 2018. One of the features of BERT is that BERT is now able to "read context" by learning from both sides of a sentence (sentence starters and enders) with its built-in architecture called Transformer. Among all its uses of BERT, it is also used as **a vectorization of sentences due to its superior performance**. That information holds so much better text representation than conventional methods that the accuracy in many NLP domains was improved.



Here, considering the above, set up a hypothesis,

#### **"Can the features embeddings by BERT improve an accuracy of the exchange rate prediction??"**

In this notebook, Let's see how BERT text embeddings performs well in predicting stock rate.



## Data

[Daily News for Stock Market Prediction](https://www.kaggle.com/aaron7sun/stocknews) has both **News data** including historical news headlines from Reddit WorldNews Channel and **Stock data** (Dow Jones Industrial Average (DJIA))  [2].
This dataset is suitable for this experimentation and help us to save time of crawling news headlines.

- Combined_News_DJIA.csv
- upload_DJIA_table.csv"

Availabel here → [kaggle page](https://www.kaggle.com/aaron7sun/stocknews)



## Features

- **df_bert_embeddings.csv**
  Dataframe including original stock features and added bert-embeddings. This is used for training and evaluation of LSTM.
- **BERT_Embeddings_pca.npy**
  This file holds embeddings of Top 10 News Topics by BERT.
- **BERT_Embeddings_pca_train.npy**
  This file holds compressed 3 dimentional embeddings by PCA for training data.
- **BERT_Embeddings_pca_test.npy**
  This file holds compressed 3 dimentional embeddings by PCA for test data.



### BERT embeddings of Top 25 News Topics

BERT embeddings of Top 25 News Topics by BERT has too high 1536 dimentional data for model to learn this data. Therefore, compress the BERT embeddings using PCA into 3 dims data.

<center><strong>BERT embeddings (1536 dims) →→→  ( PCA ) →→→ BERT embeddings (3 dims)**</strong></center>

※ But I'm not sure that this transforming is the best way. I have to find a good way to make the best use of BERT embeddings. If you know, contact me, please.



## Result Example

Stock prices data is time-series data, therefore **LSTM model** is used to perform an experiment here. Training histories and evaluation results are below.

**<font color="red">Unfortunately, BERT embeddings does not contribute to the improvement of prediction accuracy this time.</font>** It seems that compressed BERT embeddings by PCA is not suitable for LSTM training.

|       data        |                       Original feature                       |             BERT embeddings of top10 news topics             |             BERT embeddings of top1 news topics              |
| :---------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|        Acc        | <font color="red"><strong>0.9576719576719577</strong></font> |                      0.8809523809523809                      |                      0.9444444444444444                      |
|   acc  history    | ![org_acc](/Users/macbookpro/Desktop/bert/exchange/results/org_acc.png) | ![bert_acc](/Users/macbookpro/Desktop/bert/exchange/results/bert_acc.png) | ![bert_top1_acc](/Users/macbookpro/Desktop/bert/exchange/results/bert_top1_acc.png) |
| loss<br />history | ![org_loss](/Users/macbookpro/Desktop/bert/exchange/results/org_loss.png) | ![bert_loss](/Users/macbookpro/Desktop/bert/exchange/results/bert_loss.png) | ![bert_top1_loss](/Users/macbookpro/Desktop/bert/exchange/results/bert_top1_loss.png) |

**※ Note that ACC=0.958 is the best score among [kaggle notebooks](https://www.kaggle.com/aaron7sun/stocknews/notebooks) (2021/01/05)**



## Future

- The way to handle embedded data needs to be improved.



## Reference

[[1]](https://arxiv.org/abs/1810.04805) Devlin, Jacob, et al. "Bert: Pre-training of deep bidirectional transformers for language understanding." *arXiv preprint arXiv:1810.04805* (2018).

[2] Sun, J. (2016, August). Daily News for Stock Market Prediction, Version 1. Retrieved [Date You Retrieved This Data] from https://www.kaggle.com/aaron7sun/stocknews.

