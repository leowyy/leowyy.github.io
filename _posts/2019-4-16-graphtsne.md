---
layout: post
title: 'GraphTSNE'
date: '16 Apr 2019'
---
<figure>
	<center>
	    <img src="{{ site.baseurl }}/public/graphtsne/graphtsne.gif" width="500">
	    <figcaption><b>GraphTSNE on the Cora Citation Network</b></figcaption>
    </center>
</figure>

In recent years, interest in graph-structured data has surged, following the success of graph convolutional networks and graph representation learning. Because of this, it is increasingly important for researchers and practitioners alike to gain human insight into such datasets by means of visualization. In this post, we will discuss GraphTSNE: a novel visualization technique for graph-structured data. 

### What is graph-structured data?
In particular, we will consider graph-structured datasets with two sources of information: graph connectivity between nodes and data features on nodes. Real-world examples of such datasets are _abundant_. Just think social networks, functional brain networks and gene-regulatory networks, among many others. 

### Why visualization?
In contrast to the more general problem of dimensionality reduction, visualizations can be particularly useful as a tool to explore and hypothesize about given data. By placing high-dimensional data in a low-dimensional map (in 2D or 3D), such visualizations can often reveal _interesting structure_ within the data that would otherwise be inscrutable. 

### Two approaches to visualization. Is there a middle ground?
In the literature on dimensionality reduction, we may consider two general approaches to visualizing graph-structured data. First, we can construct a visualization based on the feature similarity between nodes using the highly successful technique of t-SNE ([van der Maaten & Hinton](http://www.jmlr.org/papers/volume9/vandermaaten08a/vandermaaten08a.pdf), 2008). Second, we can visualize the graph structure directly with a standard graph visualization technique like Laplacian Eigenmaps ([Belkin & Niyogi](https://papers.nips.cc/paper/1961-laplacian-eigenmaps-and-spectral-techniques-for-embedding-and-clustering.pdf), 2001). 

Roughly speaking, the common objective in visualization is to obtain a low-dimensional representation that maximally preserves the _local structure_ of the original data, which could be in terms of pairwise feature distances _and/or_ graph distances. However, both approaches are unsatisfactory because they cannot incorporate information from _both_ node features and graph structure. This is why we have designed GraphTSNE to fill this gap. 
<center>
<img src="{{ site.baseurl }}/public/graphtsne/spectrum.png">
</center>

## Method
GraphTSNE relies on two modifications to a _parametric_ version of t-SNE proposed by [van der Maaten](http://proceedings.mlr.press/v5/maaten09a.html) (2009). First, we use a graph convolutional network (GCN) ([Sukhbaatar et al.](https://arxiv.org/abs/1605.07736), 2016; [Kipf & Welling](https://arxiv.org/abs/1609.02907), 2016; [Hamilton et al.](https://arxiv.org/abs/1706.02216), 2017) as the parametric model for the non-linear mapping between the high-dimensional data space and the low-dimensional embedding space. By stacking multiple graph convolutional layers, GCNs learn node representations by aggregating information from distant neighbors in the graph. In particular, our present work uses a two-layer residual gated GCN of [Bresson & Laurent](https://openreview.net/pdf?id=SJexcZc8G) (2018).

Second, we train our GCN using a modified t-SNE loss composed of two sub-losses: a graph clustering loss and a feature clustering loss. These sub-losses derive directly from the classical t-SNE loss, except that we supply the loss function with two different distance metrics. The graph clustering loss takes as input the pairwise shortest-path (geodesic) distances between nodes. Whereas, the feature clustering loss takes as input the pairwise distances measured by a suitable similarity measure between node features, e.g. the cosine similarity between two high-dimensional vectors. Lastly, we can explore the tradeoff between the two sub-losses by taking a weighted combination.

## A Case Study on Cora 
Let's consider a concrete benchmark dataset called the [Cora citation network](https://linqs.soe.ucsc.edu/data). In this network, each node is a document represented by a word-occurrence feature vector and a class label. Furthermore, each document lies within a network, where every edge between two documents represents a citation link. Intuitively, natural clusters in the network (i.e. papers with the same document class) tend to share similar features _and/or_ belong to the same graph community.

To understand the different contributions of the graph structure and node features, we can vary the extent of graph clustering with the alpha hyperparameter in our composite loss. At _a_ = 0, our method reverts to pure feature clustering as in classical t-SNE.  Whereas, at _a_ = 1, our method performs pure graph clustering, similar to tsNET ([Kruiger et al.](http://www.cs.rug.nl/~alext/PAPERS/EuroVis17/paper.pdf), 2017). Unlike spectral methods like Laplacian Eigenmaps, tsNET is more closely related to a popular class of graph layout algorithms called force-directed graph drawing ([Fruchterman & Reingold](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.13.8444&rep=rep1&type=pdf), 1991). In our paper, we propose a reasonable way (though certainly not the _only_ way) of determining a desirable value for _a_ based on visualization distance metrics. 

By incorporating both graph connectivity and node features, the visualizations produced with intermediate values of _a_ achieve better separation between classes and therefore, higher 1-NN generalization accuracy. This phenomenon has been well-studied in the context of semi-supervised classification ([Yang et al.](https://arxiv.org/abs/1603.08861), 2016; [Kipf & Welling](https://arxiv.org/abs/1609.02907), 2016; [Velickovic et al.](https://arxiv.org/abs/1710.10903), 2018) and unsupervised representation learning ([Hamilton et al.](https://arxiv.org/abs/1706.02216), 2017; [Velickovic et al.](https://arxiv.org/abs/1809.10341), 2019). At the proposed value of _a_, we demonstrate both _quantitatively_ and _qualitatively_ that GraphTSNE outperforms existing visualization techniques.

<center>
<img src="{{ site.baseurl }}/public/graphtsne/plots.png">
</center>

## Conclusion
In this post, we have looked at GraphTSNE as a novel visualization technique for graph-structured data. We believe that this represents an important contribution in the direction of better visualization techniques dedicated to graph machine learning. This is also why we have assembled a suite of evaluation metrics from the literature that will allow for the quantitative assessment of future developments. 

Our method is based on scalable and unsupervised training of a graph convolutional network, which is the key mechanism for naturally incorporating information from both graph connectivity and node features. Moving forward, we hope to explore the use of GraphTSNE as an _inductive_ visualization technique that will enable its use on larger and time-evolving datasets.

### Code and Paper 
If you are interested to use GraphTSNE, check out our code on GitHub: [https://github.com/leowyy/GraphTSNE](https://github.com/leowyy/GraphTSNE). Also, if you use GraphTSNE in your work, we welcome you to cite our ICLR'19 workshop [paper](https://arxiv.org/abs/1904.06915): <br>
```
@article{leow2019GraphTSNE,
  title={GraphTSNE: A Visualization Technique for Graph-Structured Data},
  author={Leow, Yao Yang and Laurent, Thomas and Bresson, Xavier},
  journal={arXiv preprint arXiv:1904.06915},
  year={2019}
}
``` 
<br>
... a given wire happens to be carrying "$$\lvert 0\rangle$$."
By that we mean that it's carrying the linear combination
$$\begin{psmallmatrix} 1 \\ 0 \end{psmallmatrix}$$ ...
