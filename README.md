# np-gaussian-process
Numpy implementation of Gaussian Process Regression.

- Reference from [gaussian-processes](http://krasserm.github.io/2018/03/19/gaussian-processes/).
- Full code is based on krasserm's bayesian-machine-learning repository [[GIT](https://github.com/krasserm/bayesian-machine-learning), [LICENSE](./3RD-PARTY.md)]

## Gaussian process regression

### 1. Kernel definition

This notebook will use Gaussian RBF as default kernel.

```python
kernel = gaussian_rbf
```

### 2. Define prior

Zero mean and covariance from kernel.

```python
X = np.arange(-5, 5, 0.2).reshape(-1, 1)
mu = np.zeros(X.shape)
cov = kernel(X, X)
```

<img src="res/prior.png" width="40%">

### 3. Compute posterior

Compute posterior with gaussian process regression.

```python
X_train = np.array([-4, -3, -2, -1, 1]).reshape(-1, 1)
Y_train = np.sin(X_train)

mu_s, cov_s = posterior_predictive(X, X_train, Y_train)
```

<img src="res/posterior.png" width="40%">

### 4. Training data with noise

Assume training data has noise with zero mean and 0.3 stddev.

```python
noise = 0.3
Y_train = np.sin(X_train) + noise * np.random.randn(*X_train.shape)

mu_s, cov_s = posterior_predictive(X, X_train, Y_train, sigma_y=noise)
```

<img src="res/noise_posterior.png" width="40%">

### 5. GPR with several parameters

Simulate gaussian process regression with several parameters.

<img src="res/param1.png" width="80%">
<img src="res/param2.png" width="80%">

### 6. Optimize hyper parameters with gradient based algorithm

Optimize parameters to maximize liklihood of posterior predictive.

<img src="res/optimized.png" width="40%">