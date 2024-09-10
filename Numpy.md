https://www.numpy.org.cn/user/quickstart.html#%E7%AE%80%E5%8D%95%E6%95%B0%E7%BB%84%E6%93%8D%E4%BD%9C
https://numpy.org/doc/stable/user/quickstart.html

### Array
#### construction
```
a = np.array([[0, 1],
              [2, 3],
              [4, 6]])
```
Elements are stored in "C-style": by row/rightmost index “changes the fastest”:
```
b = a.flatten()    # array([0,1,2,3,4,5])
```
1. `np.array(list, dtype = float64)`, `np.array(list of list)`
2. `np.arange(start, end, step_size)` (not arrange), `np.linspace(start, end, length)`
3. `np.zeros((dim1, dim2))`, `np.ones(length)`
4. 1d array is not manipulated like a list: `arr1 + arr2` is not concatenate; there is no `append` method for `np.array`. Instead, do `b = np.append(b, new_element)`.
#### indexing
1. like list indexing: `a[-1]` the last row,
```
   a[::-1, :]    # = np.array([[4, 1],
                               [2, 3],
                               [0, 6]])
```
2. by a list-like object of indices: `a[[0, 2], :]`, `a[np.arange(2), 0]`
3. by a list-like object of boolean (same dim): `a[[True, False, True], [True, False]]`
4. by a boolean of the same shape: `a[a > 0]`
#### reshape
1. `a.shape    # (3, 2)` 
2. `c = a.reshape(2, 3)`, `c = a.reshape(2, -1)` the same, `-1` dim automatically calculated.
3. `np.concatenate((a, a), axis = 0)` -> shape (6, 2), bind arrays by row
   `np.concatenate((a, a), axis = 1)` -> shape (3, 4), bind arrays by column
4. `np.split(a, [1, 3], axis = 0)` -> `[array([[0, 1]]), array([[2, 3], [4, 5]])]`
#### copy
1. simple assignment `d = a` create a pointer to `a`, no copy.
2. shallow copy `d = a.view().reshape(2, 3)` can have different shape but share the same data
3. deep copy `d = a.copy()` copy the data object. Should use deep copy if `a` is a large intermediate result and we just need `d = a[-1, -1].copy()`. (Then `del a`)
### Function
1. vector operations (elementwise): `2*a + b`, `a**2`, `a > 0`
2. elementwise functions: `np.sin(a)`, `np.log(a)`
3. summary functions along axis: `np.sum(a, axis = 0)` (colSums), `np.max(a, axis = None)` (max over all element), `np.argmin()`, `np.cumsum()`, `np.sort()`, `np.mean()`, `np.std()`, `np.var()`
4. bool: `np.isnan(np.nan)`, `np.isinf(np.inf)`, `np.all()`, `np.any()`, `np.where()`
5. random: `U[0, 1]: np.random.rand(dim1, dim2, ...)`,  Gaussian `np.random.normal(mu, sigma, n)`

### Linear algebra and statistics
1. column vector `np.array([[0],[1],[2]])`, row vector `np.array([[0, 1, 2]])`
2. covariance `np.cov(a)` -> 3-by-3 cov mat, each row of `a` is considered observations of a random variable
3. Identity matrix `np.eye(n)`, inner/outer product `np.dot(a, b)`, `np.outer(a, b)`, matrix transpose `M.T`, trace `np.trace(M)`
4. matrix product `M @ x`. 1-d array `x = np.array([0, 1])` self-adjusted in matrix product: `M@x` gives 1-d array of `M[:, 1]`, `x@M` gives 1-d array of `M[1, :]` for a 2-by-2 matrix `M`.
5. inverse `np.linalg.inv(A)`, solve linear system `np.linalg.solve(A, b)`, eig decomposition `np.linalg.eig(A)`, SVD `np.linalg.svd(A)`