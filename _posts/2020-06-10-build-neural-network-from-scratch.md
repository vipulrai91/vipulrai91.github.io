---
layout: post
cover-img: assets/img/neural_net/nerve_cell.jpg
tags:
  - deep learning
  - neural network
  - Tensorflow
  - Keras
comments: true
---

# We will be building a simple neural network to classify digits from scratch

## What is a neural network ?

A [neural network](https://en.wikipedia.org/wiki/Neural_network) is a network or circuit of neurons, or in a modern sense, an artificial neural network, composed of artificial neurons or nodes.Thus a neural network is either a biological neural network, made up of real biological neurons, or an artificial neural network, for solving artificial intelligence (AI) problems.

In simple words a neural network is a connection of different layers where each layers comprise of single or multiple nodes(neurons) which are connected to each other to perform a task.

There could be multiple layers:

- single input layer
- single or multiple hidden layers
- output layer

![Neural Network](/assets/img/neural_net/440px-Neural_network_example.svg.png?=2&s=100)

We are going to use Tensorflow and Keras,since version TF 2, Keras is integrated into the TF APIs.

The basic components of our code will be:

- Layers: Collection of nodes or neurons, as described above
- Weights: What the network will learn and update
- Activation Function: Activation function decides, whether a neuron should be activated or not by calculating weighted sum and further adding bias with it. The purpose of the activation function is to introduce non-linearity into the output of a neuron.
- Optimizer: To check how our much our results are deviating from the ground truth (In simple terms how far our prediction is from the expected values)
- Bias : Additional parameter using which we can control if we want the node to fire or not

There are many other components, but since this a basic nn we will be using only these

Also, this will be a linear function with 2 layers, so we will be training our model to fit in the equation for line i.e.<br>
y = wx + b<br>
where,<br>
w = weights or gradient<br>
b = bias<br>
y = target/ to predict/ dependent variable/ output<br>
x = predictor/ features /independent variable / input to the model

Let's start with imports

<script src="https://gist.github.com/vipulrai91/389076b5558304db97233eb421324fbd.js">
</script>

Create a basic layer

<script src="https://gist.github.com/vipulrai91/25e71bc5f83f8077e1e7bb1139a7c6f3.js">
</script>

Create a Sequential class to chain these layers as this is going to be 2 layer network

<script src="https://gist.github.com/vipulrai91/e4fc5c0fa2d14ffa0265764a81d8f7e4.js">
</script>

Create the model and batch generator - we process input in batches so it can be optimized to use the ram, memory and other resources and also don't throw memory errors

<script src="https://gist.github.com/vipulrai91/e4f8bf404f038abd7908ee9b1acceb78.js">
</script>

Now as we can see we have created a model which has 2 layers of type NaiveDense

For layer 1 the activation function is 'relu' - it basically takes the max of 0 or other number ie, relu = max(0,n)

For layer 2 the activation function is 'softmax' - it basically gives the probability of the labels , in our case we will be classifying no from 0-9 , so the output will be a list of probability with a length of 10

LEARNING_RATE is the rate at which we want the model to update

We use SGD as optimizer

<script src="https://gist.github.com/vipulrai91/46fbcb4ec004a4a84561a1566e9d0310.js">
</script>

We create the training step and open gradient tape scope to calculate the gradients

Finally, we create the fit function which when called will start the training process

We will use mnist data set which is already built in TF module.We already imported this.

```python
from tensorflow.keras.datasets import mnist
```

We train the model for 10 epochs, ie the training process will see each data point for 10 times.

Finally we can check the accuracy.

This simple model gave me an accuracy of 88%, which is good given that this was basic model and we did little optimizations.

References:<br>
Image by [Colin Behrens](https://pixabay.com/users/ColiN00B-346653/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=2213009) from [Pixabay](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=2213009)<br>
[Wikipedia](https://en.wikipedia.org/wiki/Neural_network)<br>
[Keras Deep Learning with Python, Second Edition by François Chollet](https://www.manning.com/books/deep-learning-with-python-second-edition)
