---
layout: post
title: 对深度学习的一点思考
category: 个人思考
tagline: 
tags: [Deep Learning, 深度学习]
theme :
  name : bootstrap-3
---
{% include JB/setup %}

从建模的角度上看，深度学习技术或许真的是解决自然语言处理问题、图像识别问题和语音识别问题等AI问题的一种有效工具。虽然现在的RNN, CNN, DNN等DL模型还存在一些不足，比如在一些需求上难以取得工业级的令人满意的效果，模型不易解释，模型不易调优等，但随着DL理论和机器硬件的不断进步，将来也许会出现更强大的网络，使得对AI问题的处理效果能达到工业级的上线要求。笔者因为对自然语言处理问题更为熟悉，所以对当前常用于自然语言处理问题的RNN模型（当然CNN等模型也能用于自然语言处理问题），笔者更坚持这个观点，我的论据是：
1. Embedding: 用embedding向量去描述语言世界里的各种实体（不只是命名实体中的实体），比如对word, character, sub-word or word-piece等都可以做embedding。Embedding向量是稠密向量，相比于one-hot向量，有效减少了模型参数，不仅提高了模型运行速度，更重要的是减少了模型过拟合的可能性，从而提高模型可用的范围。从数学含义上讲，就是把实体映射到空间中的某个点。
2. 矩阵相乘: 用矩阵相乘做线性变化。从数学含义上讲，就是将作为输入的向量或者作为中间结果的向量从一个维度空间的点转换到另一个维度空间的点。
3. 非线性的激活函数: 矩阵相乘毕竟只是线性变换，其表达能力有限，不一定够解释真实的观测数据。设计恰当的网络结构和恰当的非线性激活函数，就能拟合出任何函数形式。
4. 虽然矩阵变换和非线性变化也出现在SVM、Logistic Regression、Softmax Regression等模型中,但这些模型还只属于浅层模型，但DL凭借其更深的网络层数、灵活的网络结构设计和embedding技术的融合，模型的表达能力更强。
5. 在自然语言处理中，经常碰到歧义问题，比如词义歧义，词性歧义，句法结构歧义。以词义歧义也就是通常说的一词多义问题为例，如果是按照pLSA, LDA等主题模型的思想，模型会假设每个词都能有多个topic，并通过模型训练直接给出topic分布。而按照当前的RNN模型的思想，建模时一般只给予其一个embedding向量（即使对初始embedding向量做fine tuning后变成另一个向量，但在inference时，也只会用一个embedding向量）。以前我觉得RNN的这种建模思路是不合理的，一个向量如何可以对应到多个含义上，但是在逐渐了解RNN后，可以感觉这样建模的路子也许是能走通的。对此，笔者的逻辑是这样的：一个词有多义，是因为其不同的上下文语境才有不同的含义，脱离上下文，该词的含义就无从谈起；刚好在DL中，结合上下文的embedding和矩阵相乘、非线性激活函数等计算后，得到的结果自然会随着上下文的变化而变化。可见研究方法与研究问题是可以对应上的，虽然不是完美的对应上。
6. LSTM, GRU, Bidirectional RNN, stacked RNN, residual connection, attention等一系列创新技术的引入，更进一步的加强了DL模型的表达能力。
7. 图像和语音是大自然本来存在的信号，而语言则不同，这是人类造出来的。在语料标注方面，图像识别、语音识别等问题却需要费时费力的人工标注的方式标注数据，而自然语言处理有一个很独特很庞大的标注数据源，这就是搜索引擎。用户已经把知识沉淀在query及其点击的doc/APP/music/movie等文字描述的实体上，如果做好脏数据过滤和异常数据过滤，那么这个数据源值得更深入的挖掘。

DL模型的优点是理论上模型的表达能力强，且在一些AI问题上取得了state-of-the-art结果。而其缺点也比较明显，模型参数不易理解，模型不易调优。如果学术界能在模型参数的理解上、每一层网络学习到的知识的可视化上取得研究突破的话，那么DL就真可以“飞入寻常百姓家”了。

* * *

**原创文章，转载请注明：**转载自[{{ site.title }}]({{ site.production_url }})

**本文链接地址：**[{{ page.title }}]({{ site.production_url }}{{ page.url }})

* * *
