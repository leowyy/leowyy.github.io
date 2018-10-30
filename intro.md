---
layout: page
title: A brief introduction
---

### Visualising data in high dimensions
Dimensionality reduction techniques allow us to visualize high dimensional data by creating a low dimensional map (in 2D or 3D). Such visualizations can often reveal interesting structure within the data that would otherwise be inscrutable. Below, we consider a simple example where 28x28 pixel images of handwritten digits are mapped to a 2D space.
<center><img src="{{ site.baseurl }}/public/intro/mnist_tsne.png" width="500"></center>

Recent DR techniques like t-SNE [Laurens, 2008](https://lvdmaaten.github.io/publications/papers/JMLR_2008.pdf) have achieved much success, but they are computationally expensive. Furthermore, they produce mappings which are one-use-only; the mapping found on one set of points cannot be used to project out-of-sample data. 

### Enter graph nets
Can we train a neural network to perform t-SNE? Instead of using a vanilla neural net, I'm exploring the use of spatial graph nets [Bresson, 2018](https://openreview.net/pdf?id=SJexcZc8G), which are better able to propagate local information between points that are similar in the high dimensional space. 

My initial results have been promising, but a lot remains to be done. For now, have a look at a visualisation of word embeddings produced by a trained graph net. See if you can find any interesting word associations.
