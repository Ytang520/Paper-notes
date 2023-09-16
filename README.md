# Paper-notes
论文，文章和其他相关笔记汇总，方便回顾&查阅。涉及话题：Ordinal Regression, Fairness, Adversial Training



## Ordinal Regression:

- [Rank consistent ordinal regression for neural networks with application to age estimation](https://zhuanlan.zhihu.com/p/624840505)
  亮点：对输出层采用weight共享和bias不共享方法 解决 ordinal inconsistency 问题，提出 CORAL (Consistent Rank Logits)，并给出理论证明和实验验证；结果表明解决了inconsistency问题有助于改进分类结果

- [Ordinal Regression with Multiple Output CNN for Age Estimation](https://zhuanlan.zhihu.com/p/625156821)
  亮点：上文的参考文章；提出OR-CNN；给出数据集 AFAD；实验验证 multi-class classification 比起 generic regression 表现好



## Fairness









## 个人觉得不错的文章

- [Adversial Learning 的介绍文章](https://zhuanlan.zhihu.com/p/296809584)
  亮点：简单介绍了对抗学习的提出历史，和截至20年以来有趣发现；其中提到的 pure feature 提取的研究虽然比较直觉，不过给出相应的证明还是挺有趣的
  可进一步考察内容：
  - 对抗学习中acc下降的原因，或许与无法衡量robustness的样本质量有关 (是否为"好"样本，样本有多"好"
  - 进一步考察对抗学习和 pure attribute 之间关系（直接在 pure attribute 上进行扰动，而不是原始输入上扰动
  ![对抗训练经典图](https://user-images.githubusercontent.com/125520425/236224216-7a791529-d984-4250-bee1-0671f63b4032.png)
