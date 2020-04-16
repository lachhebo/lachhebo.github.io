---
layout: post
title: "pyclustertend, a python package to assess cluster tendency"
date:   2019-09-26
categories: DataScience ML scikit-learn Python
published: true
---

Here, I would like to present my experience creating the package pyclustertend. pyclustertend is a python package available on Pypi specialized in cluster tendency which consist to assess if clustering algorithms are relevant for a dataset.

Three methods for assessing cluster tendency are currently implemented and one suplementary method based on metrics obtained with a KMeans estimator :

- [x] Hopkins Statistics
- [x] VAT
- [x] iVAT

- [x] Metric based method (silhouette, calinksi, davies bouldin)

## Installation :

```shell
    pip install pyclustertend
```

## Usage :

### Example Hopkins :

```python
    >>>from sklearn import datasets
    >>>from pyclustertend import hopkins
    >>>from sklearn.preprocessing import scale
    >>>X = scale(datasets.load_iris().data)
    >>>hopkins(X,150)
    0.18950453452838564
```

### Example VAT :

```python
    >>>from sklearn import datasets
    >>>from pyclustertend import vat
    >>>from sklearn.preprocessing import scale
    >>>X = scale(datasets.load_iris().data)
    >>>vat(X)
```

<img height="350" src="https://raw.githubusercontent.com/lachhebo/pyclustertend/screenshots/vat.png" />

### Example iVat :


```python
    >>>from sklearn import datasets
    >>>from pyclustertend import ivat
    >>>from sklearn.preprocessing import scale
    >>>X = scale(datasets.load_iris().data)
    >>>ivat(X)
```

<img height="350" src="https://raw.githubusercontent.com/lachhebo/pyclustertend/screenshots/ivat.png" />


# Source and Notes :

It's preferable to scale the data before using hopkins or vat algorithm as they use distance between observations. Moreover, vat and ivat algorithms
do not really fit to massive databases. For the user, a first solution is to sample the data before using those algorithms. As for the maintainer of this implementation, it could be useful to represent the dissimalirity matrix in a smarter way to decrease the time complexity.


# Gathered skills :

I am proud of my work and hope to keep improving pyclustertend. I have improved myself in many ways. This experience has sharpen my skills in :

- Python Development
- Continious Integration
- Data Science (mainly clustering)
- Retrieval of information
- Documentation
- Pip packaging  
