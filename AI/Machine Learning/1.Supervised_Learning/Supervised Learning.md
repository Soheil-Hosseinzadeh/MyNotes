[[XGBoost]]
# 1-Linear Regression
>An example of Linear regression:
```python
import numpy as np
import sys
np.set_printoptions(threshold=sys.maxsize)
X = 30*np.random.rand(1000) + 1
Y = 3 * X + 8 + np.random.normal(0, 5, 1000)
print(X)
print(Y)
```

```python
n = len(X)
X_s = X.sum()
Y_s = Y.sum()
XiYi = (X*Y).sum()
Xi2 = (X**2).sum()
print(X_s)
print(Y_s)
print(XiYi)
print(Xi2)
```

We get to the `w1` and `w0` by solving derivations = 0.
```python
w1 = (XiYi - X_s*Y_s/n)/(Xi2 - (X_s**2)/n)
w0 = (Y_s - w1*X_s)/n
print(f"w0 is: {round(w0, 2)}")
print(f"w1 is: {round(w1, 2)}")
```

---
### Generalization
>Important note about overfitting risk:
- Higher degree for model and consecutively more number of parameters increase the overfitting risk.
- Higher number of training samples decrease the overfitting risk.

>You may choose some high degree for your model but use a huge majority of data as training data, then you won't probably get to overfitting issues although you are using more complex model for your training.

