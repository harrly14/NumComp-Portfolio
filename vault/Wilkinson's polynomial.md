Wilkinson's polynomial is a specific polynomial defined as

$$w(x) = \prod^{20}_{k=1}(x-k) = (x-1)(x-2)\dots(x-20) = \sum_{k=0}^{20}a_{k}x^k$$

The product definition using the $\prod$ syntax represents the polynomial with its roots, whereas the summation definition using the $\sum$ syntax represents the polynomial with its coefficients. 

Converting roots to coefficients is [[Conditioning|well-conditioned]], because a tiny change in the roots doesn't result in a large change to the coefficients. However, converting the coefficients to the roots (also called [[Rootfinding]]) can be [[Conditioning|ill-conditioned]], especially for higher-degree or clustered roots, because a small change in the coefficients leads to vastly different roots. 

A classic illustration of this is: 
![[Pasted image 20260911164005.png]]

This image shows that tiny perturbations to Wilkinson's coefficients move some roots only slightly, but send others (especially more closely spaced ones) far off the real-axis.