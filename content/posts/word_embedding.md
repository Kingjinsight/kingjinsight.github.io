---
date:  "2026-07-14"
draft: false
title: "NLP | Word Embedding"
author: 'King Jin'
tags: ["Anthropic","AI","Safety","Transparency"]
showtoc: true
math: true
---

# Word2Vec and Word Embeddings

> Word embedding 把离散的符号（词）映射为 dense vectors，使语义关系可以用 vector space 中的距离和方向来表达。本文沿着 CS224N Lecture 2 的思路，依次梳理 Word2Vec、Negative Sampling、count-based methods、GloVe、evaluation、word senses 以及基于窗口的神经网络分类器；最后补充 Transformer 如何把初始的 token embedding 转化为 contextual representation。

## 1. One-hot Encoding

词表大小为 $V$ 时，第 $i$ 个词的 one-hot vector 为：

$$ e_i=[0,\ldots,0,1,0,\ldots,0]\in\mathbb{R}^{V} $$

这是一种 localist representation：每个词独占一个维度，vectors 之间互不重叠。它只能表示词在 vocabulary 中的 identity，既不包含词在句子中的位置信息，也不包含词与词之间的语义相似度。

不同词的 one-hot vectors 彼此正交：

$$ e_i^\top e_j=0,\quad i\neq j $$

因此在 one-hot 空间中，`cat`–`dog` 与 `cat`–`car` 之间的"距离"完全相同，无法体现两者语义相似度上的差异。

## 2. Word2Vec: Learning from Local Context

Word2Vec 的基本假设是 distributional hypothesis：经常出现在相似上下文中的词，通常具有相似的语义。

> **Tip — 核心机制**
>
> Word2Vec 并不直接对"词义"做监督学习，而是训练模型去预测 local context。共享相似上下文的词，在反复的参数更新之后，会逐渐获得相似的向量表示。

### 2.1 Skip-gram and CBOW

句子：

```text
the quick brown fox jumps
```

窗口大小为 2，中心词为 `brown`：

| Model     | Input                                     | Target                                  |
| --------- | ----------------------------------------- | --------------------------------------- |
| Skip-gram | `brown`                                   | 分别预测 `the`、`quick`、`fox`、`jumps` |
| CBOW      | `the`、`quick`、`fox`、`jumps` 的平均表示 | 预测 `brown`                            |

Skip-gram 把一个窗口拆成多个"词对"，训练样本数量更多，低频词通常能得到更充分的训练；CBOW 把上下文合并成一个平均表示，训练更快、结果也更平滑。两者默认都不编码窗口内的精确词序，因此仍然带有 bag-of-words 的局限性。

### 2.2 Input and Output Vectors

Word2Vec 为每个词维护两套 vectors：

$$ W_{in}\in\mathbb{R}^{V\times d},\qquad W_{out}\in\mathbb{R}^{V\times d} $$

同一个词 $w$ 对应：

$$ v_w=W_{in}[w],\qquad u_w=W_{out}[w] $$

- $v_w$：词作为 input / center word 时的表示；
- $u_w$：词作为 output candidate / outside word 时的表示。

对中心词 $c$ 与上下文词 $o$：

$$ score(c,o)=u_o^\top v_c $$

维护两套 vectors，是因为一个词在"作为中心词"和"作为上下文词"时扮演的是两种不同角色，分别对应两个独立的参数空间——并不是为了避免一个词和自己做点积。如果强行令 $W_{in}=W_{out}$，两种角色就必须共用同一份参数，会限制模型的表达能力。训练结束后通常只使用 $W_{in}$，也可以把两套 vectors 组合起来，例如取平均。

### 2.3 Softmax Objective and Loss

完整 Softmax：

$$ P(o\mid c)=\frac{\exp(u_o^\top v_c)}{\sum_{w\in V}\exp(u_w^\top v_c)} $$

Skip-gram 最大化真实上下文的 log probability：

$$ \max \sum_{o\in Context(c)}\log P(o\mid c) $$

训练代码中通常写成最小化 negative log-likelihood：

$$ L=-\sum_{o\in Context(c)}\log P(o\mid c) $$

Softmax 把 logits 转成概率分布；negative log-likelihood 则专门惩罚"真实上下文词的预测概率过低"这种情况。

## 3. Negative Sampling

Full Softmax 在每个训练样本上都要遍历词表中全部 $V$ 个词，计算复杂度约为 $O(Vd)$。Negative Sampling 直接替换了训练目标：不再问"词表中哪个词才是正确的 outside word"，而是判断"这个 word pair 是真实观察到的（observed pair），还是随机构造出来的噪声（noise pair）"。

真实词对 $(c,o)$ 标记为 1，再随机抽 $k$ 个负样本 $n_1,\ldots,n_k$ 标记为 0：

$$ L_{NS}= -\log\sigma(u_o^\top v_c) -\sum_{i=1}^{k}\log\sigma(-u_{n_i}^\top v_c) $$

其中：

$$ \sigma(x)=\frac{1}{1+e^{-x}} $$

对 score $x=u^\top v$：

$$ \frac{\partial L_{positive}}{\partial x}=\sigma(x)-1 $$

$$ \frac{\partial L_{negative}}{\partial x}=\sigma(x) $$

梯度下降因此会增大Positive Sample的点积，减小Negative Sample的点积。每次只更新中心词、真实上下文词和少量Negative Sample对应的 vectors，计算复杂度降为 $O((k+1)d)$。

> **Warning**
>
> Negative sample 不等于语义上绝对无关 随机采样得到的Negative Sample，有时恰好与中心词语义相关，形成 false negative。单次训练中的这类信号可能是错的，但真实的观测词对会在大规模语料中反复出现，所以少量噪声通常不会压过整体的统计趋势。因此，Negative Sampling 是一种带噪声但计算高效的 alternative objective，而不是对 Full Softmax 概率的严格近似。


## 4. Count-based Methods: Co-occurrence, SVD, and GloVe

Word2Vec 是 predictive method：从局部窗口的预测任务中学习 vectors。Count-based methods 则先统计全局 co-occurrence，再把这份高维统计结构压缩为低维表示。

### 4.1 Co-occurrence Matrix

令：

$$ X_{ij}=\text{词 }j\text{ 在词 }i\text{ 的窗口中出现的次数} $$

第 $i$ 行就是 word $i$ 的完整 context profile。如果 `cat` 和 `dog` 的 rows 相似，即使它们不直接 co-occur，也会因为共享 `pet`、`animal`、`eat` 等 context words 而获得相似的 vectors。

问题是 $X\in\mathbb{R}^{V\times V}$ 巨大、稀疏，并且容易被高频词支配。

### 4.2 SVD / LSA

$$ X=U\Sigma V^\top $$

保留最大的前 $k$ 个 singular values：

$$ X\approx U_k\Sigma_kV_k^\top $$

singular value 越大，说明对应的 latent direction 能解释的 matrix variation 或 energy 越多。这里彼此正交的是 $U$、$V$ 中的 latent directions 本身，而不是每一个 word vector；因此 `cat` 与 `dog` 仍然可以在低维空间中彼此靠近。

### 4.3 GloVe

GloVe 先统计 global co-occurrence，再学习 low-dimensional vectors 来还原其中的规律，也就是用低维向量表达高维 co-occurrence matrix：

$$ w_i^\top\tilde w_j+b_i+\tilde b_j\approx\log X_{ij} $$

完整目标：

$$ J=\sum_{i,j}f(X_{ij}) \left( w_i^\top\tilde w_j+b_i+\tilde b_j-\log X_{ij} \right)^2 $$

训练循环：

```text
建立稀疏共现矩阵 X
-> 随机初始化两套向量和 bias
-> 取一个非零词对 (i,j)
-> prediction = dot product + bias
-> target = log X_ij
-> 计算加权平方误差
-> 梯度下降更新参数
-> 重复多个 epoch
```

- `log` 压缩了共现次数的数量级，避免极端高频的词对主导训练；
- bias 项吸收了每个词自身的总体使用频率，让点积部分专注于词与词之间的关系；
- $f(X_{ij})$ 用来降低稀有、噪声较大的词对的权重：共现次数越大，权重越高，但达到上限后不再增加，从而避免高频词对完全主导 loss。

GloVe 论文用概率比来解释语义差异：如果 `solid` 更偏向 `ice`，`gas` 更偏向 `steam`，而 `water` 同时关联两者，那么 $w_{ice}-w_{steam}$ 就会编码固体与气体之间的差异。

### 4.4 Method Comparison

| Method    | Training Signal | Optimization                 | Output         |
| --------- | --------------- | ---------------------------- | -------------- |
| SVD / LSA | 全局计数矩阵    | 直接矩阵分解                 | 低维静态表示   |
| Word2Vec  | 局部窗口预测    | Softmax 或 Negative Sampling | 静态 embedding |
| GloVe     | 全局共现次数    | 加权平方误差 + 梯度下降      | 静态 embedding |

三种 methods 的训练方式不同，但目标一致：把相似的 context profiles 压缩成相似的 vectors。

## 5. Word Embedding Evaluation

Intrinsic evaluation 检查向量空间本身；extrinsic evaluation 检查向量能否改善真实任务。两者描述的是不同的 evaluation target，和机器学习中常说的 validation set、test set 并不是一回事。

### 5.1 Intrinsic Evaluation

直接检查向量空间：

- cosine similarity 是否符合人类的相似度判断；
- 最近邻是否合理；
- analogy 是否形成稳定的线性方向。

Cosine similarity：

$$ \cos(v_i,v_j)=\frac{v_i^\top v_j}{|v_i||v_j|} $$

Dot product 同时受 direction 和 magnitude 影响；cosine normalization 去掉了 magnitude 的影响，更专注于两个 vectors 的方向是否相似。

经典 analogy：

$$ v_{king}-v_{man}+v_{woman}\approx v_{queen} $$

Intrinsic evaluation 速度快、成本低，适合快速筛选模型，但分数高不代表在真实任务上表现更好。

### 5.2 Extrinsic Evaluation

把 embedding 放进 NER、情感分类、翻译等下游任务，比较 accuracy、F1 等任务指标。如果产品目标是 NER，就应该优先选择 NER F1 更高的 embedding，而不是 analogy 分数更高的 embedding。

## 6. Word Senses and Polysemy

Word2Vec 与 GloVe 都为每个词只保存一个固定向量。`bank` 的金融义和河岸义会被压进同一个表示：

$$ v_{bank}\approx p_1v_{finance}+p_2v_{river} $$

多个 senses 叠加在同一个 vector 中的现象，可以理解为 superposition：高频 sense 的权重更大，低频 sense 容易被淹没。

针对这个问题，早期的改进思路包括：

- **Multiple prototypes**：先对同一个词的所有出现语境做聚类，把每一类看作一个独立的词义，再为每个词义分别学习一个向量，多个向量各自单独存储；
- **Global context**：利用更大范围的句子或篇章信息，在实际使用时动态判断当前语境对应的是哪一个词义；
- **Sparse coding**：假设混合向量是由少量"语义原子"线性组合而成，通过 sparse coding 从这个混合向量中反解出各个独立的语义成分。

## 7. Window-based Neural Classifier for NER

NER 要为每个 target word 预测 `PERSON`、`LOCATION`、`ORGANIZATION` 或 `O`。只看 target word 本身容易产生歧义，因此 CS224N 使用 fixed window：

```text
Museums in Paris are amazing
```

以 `Paris` 为中心、窗口大小为 2，拼接五个词向量：

$$ x=[v_{Museums};v_{in};v_{Paris};v_{are};v_{amazing}] $$

这里用的是 concatenation 而不是平均，因此保留了相对位置信息，这一点和 CBOW 的 averaging 不同。

线性分类器：

$$ z=Wx+b $$

加入 hidden layer 与非线性激活后：

$$ h=\tanh(W_1x+b_1) $$

$$ z=W_2h+b_2 $$

非线性激活是必要的：如果没有 `tanh` 这样的激活函数，多层线性变换最终仍会合并成一个线性变换，无法学到"目标词大写 + 左侧出现 `in` + 周围出现地点相关词"这类特征组合。

Softmax 把类别 logits 转成概率：

$$ p_c=\frac{e^{z_c}}{\sum_j e^{z_j}} $$

Cross-Entropy：

$$ L=-\sum_c y_c\log p_c=-\log p_{true} $$

若 `Paris` 的真实类别是 `LOCATION`，$p_{LOCATION}$ 越高，loss 越小。反向传播会更新分类器；若 embedding 没被冻结，也会让词向量随之适应 NER 任务。

## 8. Transformer Token Embeddings

前面的 Word2Vec 和 GloVe 为每个词学习一个 static vector。Transformer 仍然从 embedding lookup 开始，但会用 self-attention 为每一次 token occurrence 计算不同的 contextual representation。

现代 Transformer 有自己的 embedding matrix：

$$ E\in\mathbb{R}^{V\times d} $$

从头训练时它通常随机初始化，并随着整个模型一起，通过语言模型的 loss 联合更新。它既不是直接加载 Word2Vec 训练好的 vectors，也不是人为写入的词典释义，而是模型自己学出来的"什么样的初始表示最有助于完成预测任务"。

初始 token 表示：

$$ x_i=E[token_i] $$

Self-attention 再根据当前上下文动态计算：

$$ q_i=x_iW_Q,\qquad k_j=x_jW_K,\qquad v_j=x_jW_V $$

$$ \alpha_{ij}=\operatorname{softmax}_j\left(\frac{q_i^\top k_j}{\sqrt{d_k}}\right) $$

$$ context_i=\sum_j\alpha_{ij}v_j $$

所以两个句子中的 `bank`，它们的 initial embedding 是相同的，但经过 context computation 之后得到的 hidden states 会不同。也就是说，Transformer 保留了固定的 embedding lookup，同时又为每次 token occurrence 动态计算 contextual representation。Inference 阶段只计算临时的 hidden states，不会现场重新训练或修改 embedding matrix。

## 9. Connections

- Belongs to: Architecture
- Related: Evaluation, GloVe, neural classifiers, contextual token representations
- Used in: Phase 1 / CS224N, NER、词语相似度、analogy **evaluation**
