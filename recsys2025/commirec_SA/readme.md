## 多兴趣召回

### youtubednn

### commirec-SA
对兴趣向量和目标item做attention，选择相似度最大的那个兴趣向量做loss计算
将用户的交互行为按照时间排序，构建   用户:物品池  随机选择物品池中的一个物品，将其前N（本次实验中是20）个交互作为历史行为序列， 不足N 则用 0 padding 并构建mask

将用户行为序列输入 多兴趣提取模块  对多兴趣提取模块设置 K（兴趣向量的个数）
$H^{d*n}$ n为序列长度 d为embedding_dim

attention

$$ A = softmax(W_2^T tanh(W_1H))^T $$

A的维度为K*seq

输入 -> 输出

batchsize, seq_len, embedding_dim

↓ 与W1 [embedding_dim, hidden_dim]相乘 这里hidden_dim取 4*embedding_dim

batchsize,seq_len, hidden_dim

↓ 与W2 [hidden_dim, K]相乘 K自己设定

batchsize, seq_len,K

经过转置得到A[batchsize, K, seq_len]

A和输入相乘

[batchsize, K, embedding_dim]

最终的兴趣向量
$$V_u = HA $$


模型输出结果为



胶囊网络

数据集是 movielens 数据集

|user_id| item_id |timestamp|
|------|---|---|


参考：
    [https://zhuanlan.zhihu.com/p/180058376]
