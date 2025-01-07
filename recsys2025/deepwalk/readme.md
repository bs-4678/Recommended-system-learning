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