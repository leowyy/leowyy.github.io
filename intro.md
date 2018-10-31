---
layout: page
title: A brief introduction
---
### TL;DR
I'm training a graph neural network to perform t-SNE on out-of-sample data.

### Visualising data in high dimensions
Dimensionality reduction (DR) techniques allow us to visualize high dimensional data by creating a _low dimensional map_ (in 2D or 3D). Such visualizations can often _reveal interesting structure_ within the data that would otherwise be inscrutable. Below, we consider a simple example where 28x28 pixel images of handwritten digits are visualized in a 2D space.
<center><img src="{{ site.baseurl }}/public/intro/mnist_tsne.png" width="500"></center>

Recent DR techniques like t-SNE [[Laurens, 2008]](https://lvdmaaten.github.io/publications/papers/JMLR_2008.pdf) have achieved much success, but they are computationally expensive. Furthermore, they produce mappings which are _one-use-only_; the mapping found on one set of points cannot be used to project out-of-sample data. 

### Enter graph nets
Can we train a neural network to perform t-SNE? Existing approaches include training a stack of RBMs [[Laurens, 2009]](https://lvdmaaten.github.io/publications/papers/AISTATS_2009.pdf) and applying a Gaussian kernel [[Gisbrecht, 2014]](https://www.sciencedirect.com/science/article/pii/S0925231214007036). Instead, I'm exploring the use of graph neural networks [[Bresson, 2018]](https://openreview.net/pdf?id=SJexcZc8G), which are better able to _propagate local information_ between points that are similar in the high dimensional space. 

My initial results have been promising, but a lot remains to be done. For now, have a look at a visualisation of word embeddings produced by a trained graph net. See if you can find any interesting word associations.
<center><img src="{{ site.baseurl }}/public/update_5/fasttext_train.png"></center>
