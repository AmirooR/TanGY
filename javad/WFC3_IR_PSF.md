
HST WFC3/IR PSF
===================


We are working on building a super resolution-- at resolution higher than the that of native pixel in the data-- model for the pixel-convolved point spread function of **WFC3/IR** instrument of **HST**. 
$$
\mathbf{y}_{ij} = f_i\sum_{l}\mathbf{X}_{l}K^{(i)}_{lj}+ \mathbf{B}_{i}+\text{noise},
$$
where the variance of the noise model is
$$
\mathbf{var}_{ij} = \sigma^{2} + g\Big(f_i\sum_{l}\mathbf{X}_{l}K^{(i)}_{lj}\Big),
$$
 where the first term is variance of the a floor un-correlated Gaussian noise whose value ($\sigma^{2} \simeq 0.05$ ) comes along with the data we are working with. The origin of the second term is the Poisson noise whose variance is computed by multiplying a gain factor ($g\simeq 0.01$) and the PSF model rendered at the data grid. 

In our $\chi^{2}$ optimization, we add a term proportional to some smoothness prior with a strength set by some hyper-parameter $\epsilon$. 

An example of the model for bright stars is the following:
 ![enter image description here](http://broiler.astrometry.net/~mv1003/tangy/bright.png)
 And for relatively bright stars:
 ![enter image description here](http://broiler.astrometry.net/~mv1003/tangy/less_bright.png)
![enter image description here](http://broiler.astrometry.net/~mv1003/tangy/less_bright2.png)
And faint stars:
![enter image description here](http://broiler.astrometry.net/~mv1003/tangy/faint.png)

----------


TODO list
-------------
There are many parameters to tune, such as the smoothness strength, up-sampling factor, and perhaps parameters of the noise model. In order for us to be able to fully explore those options we need to speed-up the code.
The Problem is highly parallelizable, but we are not taking advantage of that. Furthermore, we can use something like cython to make the likelihood evaluation even faster.
In some cases, the sampling operator results in numerical artifacts-- due to numerical instabilities-- along the edges of each patch. We need to fix that as well! 
