---
layout: post
math: true
toc: true
---

## Neural Network Overview
Neural Network is inspired by biological phenomena in the human brain - how information is transferred as signals in the human brain. There are many types of Neural Networks that exist. The basic neural network architecture can be classified as Feed-forward Neural Network, CNN, RNN, and etc.

### Gradient Descent:
Gradient Descent is a first-order iterative algorithm for finding a local minimum. It plays a crucial role in a neural network architecture. There are three types of gradient descent:
$$ \theta_{i+1} = \theta_i - \alpha \nabla J(\theta_i) $$
where $$ \alpha $$ is the learning rate.
- Batch GD: Uses all data points for parameter updates.
- Stochastic GD: Uses one random data point for updates.
- **Mini Batch GD**: Uses a few random data points for updates.

![gradient-descent-learning-rate](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/62ad48a5-0303-4895-9909-91fb08bb6412)

The learning rate $$ \alpha $$ cannot be too large; otherwise, it will diverge. We generally adjust the learning rate after several epochs.

### Activation Function
There are several commonly used activation functions such as ReLU, tanH, and the Sigmoid functions. Each of these functions has a specific usage.

![Activation functions](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/81de4de6-6986-4d64-b07a-5713d4265b7a)

As in linear regression notes, we know optimization requires the loss function to be convex. However, in deep learning, the loss function is generally non-convex due to non-linear activation functions. Because of this, we only guarantee finding a local minimum.

### Forward Propagation
Propagating the input signal through layers to get the output.
$$
\begin{align*}
    f_0 &= x \\
    f_r &= \sigma_r(\theta_{r-1} f_{r-1} + C_{r-1}), \quad r = 1, \ldots, L \\
    f_{L+1} &= \theta_{L} f_L + C_L
\end{align*}
$$

### Backward Propagation
**Backpropagation**: Adjusting the parameters based on the gradient of the error with respect to the network's parameters. Chain Rule is involved.
$$ \frac{\partial \text{error}}{\partial \theta_i} $$

## CNN Architecture
Convolutional Neural Network consists of multiple layers like the input layer, Convolutional layer, Pooling layer, and fully connected layers.

![CNN Architecture](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/6eea6464-6f42-49d5-9587-2092bbab40ab)

It's particularly useful for finding patterns in images to recognize objects.

### Kernel, Stride, and Padding
- Kernel is used to extract features from images; it can be viewed as a parameter in the model.
- Stride controls the movement of the Kernel across the input image. If strides = 2, it will skip the next 2 pixels.
- Padding controls the addition of extra pixels around the borders of the input images or feature map. If padding = 2, it will add two column/row pixels around the borders.

![Kernel, Stride, and Padding](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/5539aec8-7fe1-4b70-a2c7-25c5fa6e6775)

## ResNet
ResNet is the neural network architecture proposed by Kaiming He in the paper [Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385). It is widely known for its outstanding performance in image recognition. One of the problems ResNets solves is the famous known vanishing gradient. This is because when the network is too deep, the gradients from where the loss function is calculated easily shrink to zero after several applications of the chain rule. This results in the weights never updating their values, and therefore, no learning is being performed.

![ResNet Architecture](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/c654b38f-fa26-4316-b11f-658c598c82fe)
