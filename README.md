# Numpy.quantile
**numpy.quantile(a, q, axis=None, out=None, overwrite_input=False, interpolation='linear', keepdims=False, w=None)**

Compute the weighted q-th quantile of the data along the specified axis.

**Formula**    
Given an ordered sample ![formula](https://render.githubusercontent.com/render/math?math=X_1\le\X_2\le\cdot\cdot\cdot\le\X_n) with respective weights ![formula](https://render.githubusercontent.com/render/math?math=W_1,\W_2,\cdot\cdot\cdot,\W_n.)   
Define:  
![formula](https://render.githubusercontent.com/render/math?math=S_k=(k-1)W_k%2B(N-1)\sum_{i=1}^{k-1}W_i).
For an interpolation of quantile ![formula](https://render.githubusercontent.com/render/math?math=p), find ![formula](https://render.githubusercontent.com/render/math?math=k) such that ![formula](https://render.githubusercontent.com/render/math?math=\frac{S_k}{S_n}\le\p\le\frac{S_{k%2B1}}{S_n}). 
Our estimate would then be: ![formula](https://render.githubusercontent.com/render/math?math=X_k%2B(X_{k%2B1}-X_k)\frac{pS_n-S_k}{S_{k%2B1}-S_k})  
[Source](https://stats.stackexchange.com/questions/13169/defining-quantiles-over-a-weighted-sample)

**Parameters**
- **a : array_like**  
Input array or object that can be converted to an array.

- **q : array_like of float**  
Quantile or sequence of quantiles to compute, which must be between 0 and 1 inclusive.

- **w : array_like, optional**  
All weight value should be positive.
`w` must have the same shape with `a` or be a 1d array for broadcast.
When `w` is a 1d array, `axis` should be an `int` or `None` and
`w.size == a.shape[axis]` or `w.size == a.size`.
If `w` is set to `None`, it is equal to calling original np.quantile.

- **axis : {int, tuple of int, None}, optional**  
Axis or axes along which the quantiles are computed. The default is to compute the quantile(s) along a flattened version of the array.

- **out : ndarray, optional**  
Alternative output array in which to place the result. It must have the same shape and buffer length as the expected output, but the type (of the output) will be cast if necessary.

- **overwrite_input : bool, optional**  
If True, then allow the input array a to be modified by intermediate calculations, to save memory. In this case, the contents of the input a after this function completes is undefined.

- **interpolation : {‘linear’, ‘lower’, ‘higher’, ‘midpoint’, ‘nearest’}**  
This optional parameter specifies the interpolation method to use when the desired quantile lies between two data points ```i < j```:
    >linear: ```i + (j - i) * fraction```, where ```fraction``` is the fractional part of the index surrounded by ```i``` and ```j```.  
    >lower: ```i```.  
    >higher: ```j```.  
    >nearest: ```i``` or ```j```, whichever is nearest.  
    >midpoint: ```(i + j) / 2```.  

- **keepdims : bool, optional**  
If this is set to True, the axes which are reduced are left in the result as dimensions with size one. With this option, the result will broadcast correctly against the original array a.

**Returns**
- **quantile : scalar or ndarray**  
If q is a single quantile and axis=None, then the result is a scalar. If multiple quantiles are given, first axis of the result corresponds to the quantiles. The other axes are the axes that remain after the reduction of a. If the input contains integers or floats smaller than **float64**, the output data-type is **float64**. Otherwise, the output data-type is the same as that of the input. If out is specified, that array is returned instead.

**Examples**
```sh
>>> a = np.array([[10, 7, 4], [3, 2, 1]])
>>> a
array([[10,  7,  4],
       [ 3,  2,  1]])
>>> np.quantile(a, 0.5)
3.5
>>> w = np.array([[1, 2, 3], [3, 2, 1]])
>>> np.quantile(a, 0.5, w=w, axis=0)
array([6.5, 4.5, 2.5])
>>> w = np.array([1, 2, 3])
>>> np.quantile(a, 0.5, w=w, axis=1)
array([6.25, 1.75])
>>> np.quantile(a, 0.5, w=w, axis=1, keepdims=True)
array([[6.25],
       [1.75]])
>>> m = np.quantile(a, 0.5, axis=0)
>>> out = np.zeros_like(m)
>>> np.quantile(a, 0.5, axis=0, out=out)
array([6.5, 4.5, 2.5])
>>> m
array([6.5, 4.5, 2.5])
>>> w_equal = np.ones(3)
>>> np.array_equal(np.quantile(a, 0.5, axis=1), np.quantile(a, 0.5, w=w_equal, axis=1))
True
```
