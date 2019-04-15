---
layout: post
title: 'GraphTSNE'
---
## Overview
In recent years, research interest in graph-structured data has surged, following the success of graph convolutional networks and graph representation learning. Because of this, it is increasingly important for researchers and practitioners alike to gain human insight into such datasets by means of visualization. In this post, we will discuss GraphTSNE, a novel visualization technique for graph-structured data. 

### What is graph-structured data?
In this post, we will consider graph-structured datasets with two sources of information: graph connectivity between nodes and data features on nodes. Real-world examples of such datasets are abundant: just think social networks, functional brain networks and gene-regulatory networks, among many others. 

### Why visualization?
In contrast to the more general problem of dimensionality reduction, visualizations can be particularly useful as a tool to explore and hypothesize about given data. By placing high-dimensional data in a low-dimensional map (in 2D or 3D), such visualizations can often reveal interesting structure within the data that would otherwise be inscrutable. 

### Two approaches to visualization. Is there a middle ground?
In the literature on dimensionality reduction, we may consider two general approaches to visualizing graph-structured data. First, we can construct a visualization based on the feature similarity between nodes using the highly successful technique of t-SNE (van der Maaten & Hinton, 2008). Second, we can visualize the graph structure directly with a standard graph visualization technique like Laplacian Eigenmaps (Belkin & Niyogi, 2001). However, both approaches are unsatisfactory given that they cannot incorporate information from both node features and graph structure. This is why we have designed GraphTSNE to fill this gap. 
<center>
<img src="{{ site.baseurl }}/public/graphtsne/spectrum.png">
</center>

## Method
GraphTSNE relies on two modifications to a parametric version of t-SNE proposed by van der Maaten (2009). First, we use a graph convolutional network (GCN) (Sukhbaatar et al., 2016; Kipf & Welling, 2016; Hamilton et al., 2017) as the parametric model for the non-linear mapping between the high-dimensional data space and the low-dimensional embedding space. 

Second, we train our GCN using a modified t-SNE loss composed of two sub-losses: a graph clustering loss and a feature clustering loss. These sub-losses derive directly from the classical t-SNE loss, except that we supply it with two different distance metrics. The graph clustering loss takes as input the pairwise shortest-path (geodesic) distances between nodes. The feature clustering loss takes as input the pairwise distances measured by a suitable similarity measure between node features, eg the cosine similarity between two high-dimensional vectors. 

## A case study on Cora 
Let's consider a concrete dataset called the Cora citation network. In this network, each node is a document represented by a feature vector and a class label. But most importantly, each document lies within a network, where every edge between two documents represents a citation link. 
<center>
<img src="{{ site.baseurl }}/public/graphtsne/plots.png">
</center>
