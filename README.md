# RS
推荐系统学习

在这里记录我的推荐系统学习记录


# [笔记](./mynotes/推荐系统.md)
一些学习过程中的笔记。可能不太全。
详见 **mynotes** 目录


# [音乐推荐](./music_rec/README.md)

ItemCF, GBDT+LR 的实践
（这里插一嘴，音乐推荐 spotify 算是鼻祖， 并且也发布了一些可以用作音乐推荐的工具包，有兴趣的可以去了解下spotify的发家之路。

# Recsys 2023 Challenge


## ItemCF

## DeepWalk 构建 embedding
### deepwalk构建
此目录使用session——item的信息 以交互时间从远到近排序，构建了行为序列。

以构建出的行为序列  如
session[ 12345] 的行为序列为  'item_9655'，'item_9233'，'item_155'

作为构建deepwalk图的依据

### deepwalk步骤
构建好deepwalk的图之后进行deepwalk步骤

随机选取一个item A， 然后在 item A指向的item中随机选取一个 item B  这样依次走
直到序列长度到达预期  这里选择了序列长度为16

走了100w个这样的路径 

将这100w个item路径输入 genius库的word2vec模型中 训练
### 结果
得到了item的embedding表示  ，并且可以通过item embedding表示计算item之间的相似度  进行I2I推荐
## Commirec-SA   多兴趣召回方法
使用movie-Lens数据集，
对兴趣向量和目标item做attention，选择相似度最大的那个兴趣向量做loss计算
将用户的交互行为按照时间排序，构建   用户:物品池  随机选择物品池中的一个物品，将其前N（本次实验中是20）个交互作为历史行为序列， 不足N 则用 0 padding 并构建mask

将用户行为序列输入 多兴趣提取模块  对多兴趣提取模块设置 K（兴趣向量的个数）
$H^{d*n}$ n为序列长度 d为embedding_dim
attention
$$ A = softmax(W_2^T tanh(W_1H))^T $$
最终的兴趣向量
$$V_u = HA $$
