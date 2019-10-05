---
layout: post
title: 'Inductive Biases'
---
### What is an inductive bias?
The goal of supervised machine learning is generalisation, i.e. achieving low out-of-sample error by learning on a set of training data. When the out-of-sample data is drawn from the same distribution as the training data, this is called interpolation. 

In everyday life, we hold certain inductive beliefs (eg spatial/temporal smoothness) so that we can infer hypotheses about the future based
 on past observations. 
These assumptions which are necessary for generalisation are called inductive biases ([Mitchell](https://www.cs.cmu
 .edu/~tom/pubs/NeedForBias_1980.pdf), 1980).

### Choice of inductive bias: Strong vs Weak?

| <center><img src="{{ site.baseurl }}/public/inductive/strong.png"></center> | <center><img src="{{ site.baseurl }}/public/inductive/weak.png"></center> |
|     :---:      |     :---:      |
|     *Explicit feature extractors in computer vision tasks.*     |     *A convolutional neural network. Feature extraction are not innate, but learned from data.*     |

Inductive biases come in different flavours: strong vs weak, right vs wrong. While we always want to pick a right inductive bias, the choice between a strong and weak bias is not as clear. 

In classical statistical thinking, a strong inductive bias restricts the hypothesis set, thereby improving generalisation and increasing 
sample efficiency. This makes it tempting to introduce strong inductive biases, usually by encoding prior domain knowledge into the 
innate machinery of the learning process. 

However, too much innate structure can actually worsen performance, because it could introduce assumptions that might not be true of real-world and noisy data. For this reason, much of modern machine learning has been transitioned away from the traditional paradigms of rule-based learning and feature extraction.

### Inductive biases in machine learning
Every machine learning algorithm has an inductive bias, albeit to varying extents. Every inductive bias constitutes a set of assumptions that require verification. Here are some examples. 

| Model / Optimisation | Inductive Bias / Assumption |
| :--- | :--- |
| Linear regression | Output variable depends linearly on the inputs |
| SVM | Maximum margin |
| Convolutional neural networks | Translational invariance <br>Local relations between inputs |
| RNN / Attention | Long range dependencies <br>Sequential relations between inputs |
| Graph convolutional networks | Homophily <br>Structural equivalence |
| Deep learning | Distributed representations |
| Regularisation | Regularity / smoothness of a function as measured by a certain function space norm |
| Bidirectionality | Left and right contextual information |
| Multitask learning | Prefer hypothesis that explain more than one task |

### Research Directions
Even though inductive biases are widely used in the machine learning, there is great debate about the *amount* we ought to be 
incorporating into our learning algorithms. Love them or hate them, inductive biases continue to guide many important research directions. 

**ML theory through the lens of inductive bias** <br>
1. Inductive bias of deep convolutional networks through pooling geometry. Cohen & Shashua. *ICLR*, 2017.

**Novel forms of inductive bias** <br>
1. Attention is all you need. Vaswani et al. *NeurIPS*, 2017. 
2. Semi-supervised classification with graph convolutional networks. Kipf & Welling. *ICLR*, 2017. 
3. Recursive deep models for semantic compositionality over a sentiment treebank. Socher et al. *EMNLP*, 2013. 
4. Long short-term memory. Hochreiter & Schmidhuber. *Neural Computation*, 1997.  

**Injection of inductive bias** <br>
1. Weight agnostic neural networks. Gaier & Ha. *NeurIPS*, 2019.
2. Neural relational inference for interacting systems. Kipf et al. *ICML*, 2018.
3. Deep reinforcement learning with relational inductive biases. Battaglia et al. *ICLR*, 2019.
