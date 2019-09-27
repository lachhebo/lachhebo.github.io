---
title: "Development Journal 2: pyclustertend"
published: true
---

Here, I would like to present my experience creating the package pyclustertend.

# What is the pyclustertend project ?

pyclustertend is a python package to do cluster tendency. Cluster tendency consist to assess if clustering algorithms are relevant for a dataset.

Three methods for assessing cluster tendency are currently implemented and one suplementary method based on metrics obtained with a KMeans estimator.  :

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


### Example Metric : 


```python
    >>>from sklearn import datasets
    >>>from pyclustertend import assess_tendency_by_metrics
    >>>from sklearn.preprocessing import scale
    >>>X = scale(datasets.load_iris().data)
    >>>assess_tendency_by_metrics(X)
    2.0
```

# Source and Notes : 

The main article used to develop this package is available here : 

- https://www.researchgate.net/publication/224218006_An_Efficient_Formulation_of_the_Improved_Visual_Assessment_of_Cluster_Tendency_iVAT_Algorithm/link/0912f50fb54089734a000000


It's preferable to scale the data before using the hopkins or the vat algorithm as the uses teh distance between observaation. Moreover, the vat and ivat algorithms
do not really fit to big databases (more than 1k observation). For the user, a first solution is to sample the data before using those algorithm. As for the maintainer of this
implementation, it could be useful to represent the dissimalirty matrix in a smarter way to decrease the time complexity.


# Gathered skills :

I am proud of my work and hope to keep improving pyclustertend. I have improved myself in many ways. This experience has sharpen my skills in :

- Python Development 
- Continious Integration
- Data Science (mainly clustering)
- Retrieval of information
- Documentation 
- Pip packaging  
