## Rank consistent ordinal regression for neural networks with application to age estimation



#### 文章概括：

1. 本文亮点：解决 ordinal inconsistency 问题，提出 CORAL (Consistent Rank Logits)，并给出理论证明和实验验证
2. classifier inconsistencies among the binary rankings 示例：

![image-20230425141405981](https://raw.githubusercontent.com/Ytang520/pic/main/img/202304251414394.png?token=A55UUKNWQR3VG6MD7VTE4DDEI5YBK)

3. 背景：（将 K-regression 问题转化为 K-1 classification 问题）

   1. OR-CNN：
      1. Cost-matrix：
         1. 描述：表征不同类别 (排序) 直接"差距"
         2. 性质：为 V-shape 结构时，满足consistency要求
      2. 不足：
         1. V-shape 不一定保证（原论文也指出这点
         2. 强行实现consistency复杂度高

   2. ensemble：集成多种分类模型

   3. multi-task CNN：共享 Slow-layer 参数

   4. Siamese：使样本和仔细选择过的anchor image pair-wise 比较，得到排序结果

4. 本文方法：

   1. 基本思路：

      1. 处理 output layer，使得分类结果单调；此处使用同一个单调函数，使得自变量取值在不断平移（horizontal shift

      2. 具体上，其使得权值共享，bias不共享，并且构造 loss (如下) 使得其满足要求，并给出证明（在weight都非负时成立）：

         ![image-20230425162534012](https://raw.githubusercontent.com/Ytang520/pic/main/img/202304251625681.png?token=A55UUKM7EERRWSVZDHRFIC3EI6HLY)

   2. 优点：
      1. 维持了consistency
      2. 避开了 V-shape Cost Matrix 构造，降低复杂度

5. 实验：

   1. 使用数据集：MORPH-2 dataset； CACD dataset； Asian Face Database (AFAD)

   2. 实验细节：
      1. 最优算法间比较没有考虑（即所有的方法epochs, sgd, lr, decay rate等等设置相同）
      2. 使用标准结构（避免因为自己设计框架引入的经验误差(empirical bias)

   3. 原文code位置：https://github.com/Raschka-research-group/coral-cnn.

   4. 实验表明：
      1. 该方法可以避免inconsistency
      2. MSE 和 RMSE最小，即 ==**inconsistency 避免后可能确实带来预测准确性的上升**==

6. Appendix 里给出了泛化误差上界





#### 个人思考：

1. 原文有趣点：

   1. ==原文采用了另一种 ordinal regression 的研究视角，即采用了 Sequential order 而非直接的Cumulative Order（详情可参考论文：Ordinal regression: A review and a taxonomy of models）==；结果表明有改善；
   2. 在 ouput layer 上处理（代码要求不高
   3. 权值共享 bias 不共享的操作==（着手在bias上而不是weight上==

2. 自行思考点：

   1. 是否 Adjacent Order 表现会更好？实现方法或许可以 两边夹+结果结合 or 多次iteration实现 ？

   2. 原始实验使得超参数和网络结构一致，==是否inconsistency的解决适合于所有的 ordinal regression 问题？==

   3. 权值共享bias不共享是一种方法（追求有些刻意

      1. 权值共享也是为了提取到有效的特征，定义 loss 来间接实现，是否会带来别的影响？
      2. ==方法是否可能造成 bias 主导分类结果，而非提取的特征？（尤其对于最低序和最高序==

      3. 证明上要求 weight 非负，具体能否实现需要进一步考虑（或许需要别的约束

   4. loss 是否有必要衡量所有的分类结果？（如果 sequential order 在结构设计中天然满足了，那么 loss 似乎不必要进行衡量

3. 可能改进点：
   1. 两边夹实现 Adjacent Order
   2. 局部 sequential order





