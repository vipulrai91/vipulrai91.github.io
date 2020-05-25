---
layout: post
tags:
  - python
  - numpy
  - machine learning
  - classification
comments: true
---

# Stochastic Gradient Descent uisng fast.ai framework

[From Wikipedia](https://en.wikipedia.org/wiki/Stochastic_gradient_descent)<br>
Stochastic gradient descent (often abbreviated SGD) is an iterative method for optimizing an objective function with suitable smoothness properties (e.g. differentiable or subdifferentiable). It can be regarded as a stochastic approximation of gradient descent optimization, since it replaces the actual gradient (calculated from the entire data set) by an estimate thereof (calculated from a randomly selected subset of the data).Especially in big data applications this reduces the computational burden, achieving faster iterations in trade for a slightly lower convergence rate.

The following example is taken from fast.ai course.

> Summary

[Lesson Video Link](https://course.fast.ai/videos/?lesson=2)

[Lesson resources and updates](https://forums.fast.ai/t/lesson-2-official-resources-and-updates/28630)

[Lesson chat](https://forums.fast.ai/t/lesson-2-chat/28722)

[Further discussion thread](https://forums.fast.ai/t/lesson-2-further-discussion/28706)

For complete info on the course, visit course.fast.ai

```python
%matplotlib inline
from fastai.basics import *
```

In this part of the lecture we explain Stochastic Gradient Descent (SGD) which is an **optimization** method commonly used in neural networks. We will illustrate the concepts with concrete examples.

## Linear Regression problem

The goal of linear regression is to fit a line to a set of points.

Let us create a data set of n = 100

```python
n=100
```

```python
x = torch.ones(n,2)

Returns a tensor filled with the scalar value `1`, with the shape defined
by the variable argument :attr:`sizes`.

x[:,0].uniform_(-1.,1)

Returns a tensor where x[:,0] is random number between -1\. and 1

x[:5]
```

```python
a = tensor(3.,2); a
```

Linear regression using Pytorch

```python
y = x@a + torch.rand(n)
```

```python
plt.scatter(x[:,0], y);
```

You want to find **parameters** (weights) a such that you minimize the error between the points and the line x@a. Note that here a is unknown. For a regression problem the most common error function or loss function is the **mean squared error**.

```python
def mse(y_hat, y): return ((y_hat-y)**2).mean()
```

Suppose we believe a = (-1.0,1.0) then we can compute y_hat which is our prediction and then compute our error.

```python
a = tensor(-1.,1)
```

```python
y_hat = x@a
mse(y_hat, y)
```

```python
plt.scatter(x[:,0],y)
plt.scatter(x[:,0],y_hat);
```

So far we have specified the _model_ (linear regression) and the _evaluation criteria_ (or loss function). Now we need to handle _optimization_; that is, how do we find the best values for a? How do we find the best _fitting_ linear regression.

## Gradient Descent

We would like to find the values of a that minimize mse_loss.

**Gradient descent** is an algorithm that minimizes functions. Given a function defined by a set of parameters, gradient descent starts with an initial set of parameter values and iteratively moves toward a set of parameter values that minimize the function. This iterative minimization is achieved by taking steps in the negative direction of the function gradient.

Here is gradient descent implemented in [PyTorch](https://pytorch.org).

```python
a = nn.Parameter(a); a
```

```python
def update():
    y_hat = x@a
    loss = mse(y, y_hat)
    if t % 10 == 0: print(loss)
    loss.backward()
    with torch.no_grad():
        a.sub_(lr * a.grad)
        a.grad.zero_()
```

```python
lr = 1e-1
for t in range(100): update()
```

```python
plt.scatter(x[:,0],y)
plt.scatter(x[:,0],x@a);
```

## **Animate it!**

```python
from matplotlib import animation, rc
rc('animation', html='jshtml')
```

```python
a = nn.Parameter(tensor(-1.,1))

fig = plt.figure()
plt.scatter(x[:,0], y, c='orange')
line, = plt.plot(x[:,0], x@a)
plt.close()

def animate(i):
    update()
    line.set_ydata(x@a)
    return line,

animation.FuncAnimation(fig, animate, np.arange(0, 100), interval=20)
```

In practice, we don't calculate on the whole file at once, but we use mini-batches.

## Vocab

- Learning rate
- Epoch
- Minibatch
- SGD
- Model / Architecture
- Parameters
- Loss function

For classification problems, we use _cross entropy loss_, also known as _negative log likelihood loss_. This penalizes incorrect confident predictions, and correct unconfident predictions.
