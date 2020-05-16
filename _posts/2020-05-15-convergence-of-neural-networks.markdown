---
layout: post
title: The convergence of neural networks
date: 2020-05-15 22:12:00 +0200
description: A post about the convergence properties of simple neural networks 
img: neural_network.jpg # Add image post (optional)
mathjax: true
tags: [neural networks, statistics, convergence, bias-variance tradeoff] # add tag
---

Neural Networks perform well, but how well? Using a statistical framework permits the caluclation of the _order of convergence_, or to be precise, an upper bound on this order. Some time ago I wrote my Master Thesis on the subject and I decided to post a short summary of some key insights here, lest I might lose track of the basics. If you are interested in the whole story, visit my [github repo](https://github.com/phi-ra/sieve_forecasting) with the whole thesis and code. 

# Considering ANNs as Nonparametric Estimators

## The Bias Variance Tradeoff

## Sieve Estimators

$$
	\hat{\psi}(\cdot) = \arg\min_{\theta \in \Theta_n}\frac{1}{n}\sum_{t=1}^{n}(y_t - \psi_n(x_{t}))^2 \;,
$$

# Setting up the Geometric Problem

# Some implications