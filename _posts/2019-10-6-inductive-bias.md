---
layout: post
title: 'Inductive Biases'
---
### What is an inductive bias?
The goal of supervised machine learning is generalisation, i.e. achieving low out-of-sample error by learning on a set of training data. When the out-of-sample data is drawn from the same distribution as the training data, this is called interpolation. 

In a philosophical lens, this process of generalisation is also known as inductive reasoning. Consider the prototypical argument based on
 *enumerative* induction.

P1: All of the swans we have seen are white.

C: We *expect* the next swan to be white. 

Do you agree with the structure of this argument? Ok, perhaps you are dissatisfied with the omission of actual numerical values (how many
 swans did we actually see?). But the argumentative structure is based on a commonly shared and intuitive belief that the world is 
 largely uniform. We hold these beliefs so that we can infer hypotheses about the future based on past observations. These assumptions 
 which are necessary for generalisation to happen are called inductive biases ([Mitchell](https://www.cs.cmu
 .edu/~tom/pubs/NeedForBias_1980.pdf), 1980).

### Choice of inductive bias: Strong vs Weak?
Inductive biases come in different flavours: strong vs weak, right vs wrong. While we always want to pick a right inductive bias, the choice between a strong and weak bias is not as clear. 

In classical statistical thinking, a strong inductive bias restricts the hypothesis set, thereby improving generalisation and increasing sample efficiency. This makes it tempting to introduce strong inductive biases, usually by encoding prior domain knowledge into the innate machinery of the learning algorithm. 

However, too much innate structure can actually worsen performance, because it could introduce assumptions that might not be true of real-world and noisy data. For this reason, much of modern machine learning has been transitioned away from the traditional paradigms of rule-based learning and feature extraction.

### Inductive biases in machine learning
Every machine learning algorithm has an inductive bias, albeit to varying extents. Every inductive bias constitutes a set of assumptions that require verification. Here are some examples. 

### Research Directions
Even though inductive biases are widely used in the machine learning, there is great debate about the *amount* we ought to be 
incorporating into our learning algorithms. Love them or hate them, inductive biases continue to guide many important research directions. 
