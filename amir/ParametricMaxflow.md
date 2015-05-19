#Parametric Maxflow code of Vladimir
[TOC]
## Introduction
In order to compare our approximateES for parametric maxflow results with the original exact inference, I just started to read parametric maxflow code of Vladimir Kolmogorov. It took some time for me to compile it on linux. There is a *Matlab®* wrapper in the code which simplifies the stuff. However, it uses *mex_grabcut.dll* for computing unary terms which is not runnable in unix. Good news is that we can save the unaries, use other unaries, or rewrite the grabcut ( which is in contradiction with being our current state of  **GoshaDY**).

## Code details
### Main.m
There is *Main.m* file which is a well written script. It sets parameters, reads an image, and calls *PrepareEnergy()* function. Then, it converts the results to *.mat* format.

### PrepareEnergy.m
This is a simple example of finding a white object on a dark background in an image, where you impose spatial coherence. Currently, it finds the global optimum of the enrgy: $$
E = \sum_{i \in \text{all pixels}} \lambda \theta_i(l_i) + \sum_{i,j \in \mathcal{E}} [[ l_i \neq l_j ]] (\lambda_1 + \lambda_2 exp(-\beta |x_i - x_j|^2)
$$
where $l_i$ is the label of pixel $i$, and $x_i$ is the colour at pixel $i$, $\theta_i(l_i)$ is the unary potential at pixel $i$ when it has the label $l_i$, and $[[a]]$ is `1` if argument $a$ is true, and $\lambda_{min} \leq \lambda \leq \lambda_{max} $. 

The function reads a *trimap* as its initial input to *Grabcut*, computes unary and pairwise potentials (also $\beta$), calls the *parametric graphcut*, and stores the results.


> Written with [StackEdit](https://stackedit.io/).