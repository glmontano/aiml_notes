# 1.1 Deep Learning and History - Part 1

- Used for image recognition
- Creates videos and photographs
- They are complex mechanisms, with complex techniques
- One example of complex structures include the microprocessor with logical cates (AND/OR gates)
- Another example is the brain made up of ~86BB neurons. Neurons are considered to be what makes humans intelligent, and scientists attempted to investigate neurons and see if it could be replicated.
- The fundametal building block of a neuron is called the Perceptron.

# 1.2 Deep Learning and History - Part 2

- Perceptron was first written in 1940 by McCulloch-Pitts
- McCulloch modelled the neuron by considering the Perceptron as a function that sums the binary inputs, before seeing whether its above some threshold. Therefore, the Perceptron is a step function. It may be of the form
  - If Sum(xi) >= T, then output 1
  - If Sum(xi) < T, then output 0

- Some inputs, however, are called inhibitary inputs. If they take a value of 1, then the output will be 0.

- In 1958 Rsonblatt created another model, and is considered to be the ongoing model that we use today.
  
- The function instead, is a weighted sum of the inputs, before applying a non-linear function. However, it is still compared to a threshold.

- Ideally, the threshold is left at zero, and the weights are adjusted instead.

- Furthermore, there is a weight or an input that is a constant in independent of the xis. This allows to move the the sum to the left or right.

- This model is used to today's neural networks

- Adapattation is something that AI cannot mimic, which humans can.

- It's important to remember that a neural network isn't a model and does not mimic the brain, rather, it's inspired by how the brain works.

# 1.3 Multi-Layer Perceptron

- One observation in the Perceptron model is that after it has been trained, it will perform a logistic regression.

- The model is of the form f(w1x1 + ... + wnxn + wn+1). A prediction is made from this, and compared to actual result. The error is minimized by changed the weights.

- The language is that once trained - the neuron becomes the perceptron.

- Once trained on the training dataset, we move we testing as usual

- We can go a step further by having layers of neurons. There is the
-   Input layer
-   Hidden layer
-   Output layer
-   The neurons are all connected, that is, the output from the input layer enters the hidden layers, which then enters the output layer.
-   Every neuron will have precedent connections, where each has a weighting, and therefore a weighting optimization
-   Non-linear results will enter linearing, before a non-linear function is applied and so on
-   The neurons in a layer may have their parameters in a single set. The number of weights on a layer is:
-       (Number of Precedents + 1) * (Number of Neurons in Layer).
-       The +1 is to consider the bias term.
-   The weights may also be called degrees of freedom
-   The non-linear function: The sigmoid function forms an S-shaped graph, where x approaches infinity, the probability becomes 1, and as x approaches negative infinity, the probability becomes 0.

# 1.4 MNIST Dataset

- The MNIST is a dataset consisting of 60,000 training points, of 28x28 images of numbers
- A 28x28 image is 724 inputs
- Handwritten digits may be ambigious, and we want the neural network to allow for this ambigutiy
- The model will not only have a node for every string of numbers, but it will also have a probability attached to it
- The input layer is 784, the output layer is 10 (one for every digit)
- Weights are adjusted so that the derivative of y-hat with respect to the weights, causes a output closer to y
- Thus far, we've just talked about the single activation function - the sigmoid
- 'Feed forward sutrcutre' is when the NN starts with the input, goes forward to the hidden, and finally output. All neurons are fully connected.
- The activation function is non-linear because if all were linear, then we'd effectively get a linear regression, which is not interesting for our purposes
- Upon training we can investigated
  - Loss functions
  - Back propagation
  - Gradient descent, which is the right way to find the weights
 
- Other Neural networks that are not feed forward
- Overfitting and regularization
- Solving for weights means solving a non-convex optimization problem
- Deep Neural Netowrks are Neural Networks with many hidden layers

# 1.5 Deep Learning Notations

- Notation is important.
- We use matrices and vectors to condense the linear combinations that enter the activation function
- We can have different activation function with every layer

# 1.6 Types of Activation Function - Part 1

There are various step functions that will be discussed here

- Step Function, which steps at x = 0, which is effectively the threshold. One issue with the step function is the sharp increase, and it is not differentiable at the threshold, which is a problem when optiizing weights.
  
- The ability to learn depends on the activation function being smooth. Efficient learning, that is.

- Sigmoid Function, which is a smoothed version of the step function. f(x) = 1/(1+exp(-x)). This is a very common activation function, and differentiable everywhere. It has the benefit of adjusting the range by applying a simply transformation.

- Another activation function in tanh = 2s(2x)-1, which goes from -1 to +1. It is a little sharper than the signmoid due to the compression to achieve the range of -[-1, +1]. An alterantive expression for hyperbolic tang is (exp(x) - exp(-x))/ (exp(x) + exp(-x)).

- Another activation function: f(x) = x if x >= 0, else 0 or max(0,x). However, this is not smooth at x = 0, though it is smooth everywhere else. The benefit of this over the step, is that the derivative isn't 0 everywhere except x = 0. This is called ReLu. It has the benefit of allowing the network to learn, but to also to forget. It is commonly used in the hidden layers of a NN.

# 1.7 Types of Activation Function - Part 2

 - Linear activation function. Leaky ReLU := max(0.01x, x)

 - The output layer deserves, understandably, special consideration. Depending on the output, an activation function is selected. If 0 and 1 (classification problem) sigmoid can be used. If -1 or 1 then tanh

 - Assume now, the output needs to be weather (Real Space). Therefore, can use linear. However, only use this for output, and not the other layers. Else it will just be a linear regression network

 - There is more flexibility in the hidden layers - can use sigmoid, tanh, relu, but not linear for the reasons discussed

 - If there's a multiclass output: Use Softclass that odes the following:
 - The softmax function is often described as a combination of multiple sigmoids
 -   (1) It takes the Zs to the exponential, thereby allowing it to have a range of 0 to
 -   (2) Then it divides it by the sum of the exponentials on each Zi, therefore a weighted sum.
 -   (3) At this stage, we are guaranteeed for the sum to be equal to 1.
 -   This is important as the multiple outputs and their probabilities can equal to 1.

- The word features can be used from one layer to the other.

# 1.8 Training the Neural Network - Loss Function

   First we define the proximity between the prediction and the actual vector. We do this through the loss function, or L(y, yhat). 
   We can chose Avg(|yi-yhati|), thoough it runs into the problem of differentiability. As such, we resort to Avg(Y-Yhat).
   This is not useful for classification problems. The loss function used here is 'Cross Entophy Loss Function'. This is given by
   L(y, yhat) = -(ylog(yhat) + (1-y)log(1-yhat))
   In this case if there are perfect predictions: y = 0; yhat = 0 - then the loss function is 0. However, if y=0 and yhat = 1 then L is negative infinity, and therefore, the loss function delivers a large loss. This is what makes this a great loss function for classification problems.

# 1.9 The problem of local optimum and saddle point

The goal is to minimize the loss function, given changes in the weights. For machine learning, there is no nice closed formula. Though, we can rely on first principales on looking for where the derivative, or the change is close to 0. This can also be expressed and solving for a slope of zero.

We can express the loss function as a function of W, the weights. The movement towards the optimimum point, is by moving by eta times the loss-difference, where theta is small to remove aggresive movements in W. eta is called the learning rate.

Now, if the gradient is zero, it doesn't tell you where to move, and that's why the step-up activation function is inadequate, and the sigmoid is more reasonable.

All of this is called gradient descent.

One issue with gradient descent is that it will always find te local minimum, not the global minumum. The minimum found depends on the starting point of the gradient descent. That said, local minimums are OK (not proven), thought there must be an understanding that there may be a minimum wiht a lower loss function.

Given the iteration of activation functions before entering the loss function - GD is actually quite computationally complicated.

# 1.10 Backpropagation

Basic idea of backpropogation - is an efficient way of GD. Calculate the gradients of the last layer, which can be used for the gradients of the next gradients of the next layer and so on.

Another issue with GD are the millions of gradients that need to be calcualted, along with the losses, and the iterations depending on the side of eta. We will next learn about Stochastic Gradient Descent and Backward Propogation. They are efficient implementations of gradietn descent.

# 2.1 SGD with Momentum

The optimization problewm is non-convex, and there are local minima to consider.

There is a very high chance to be caught in a local-minima. However, for many cases we do not need to find ther global minima. There is evidence that this may be overfit, and therefore it is OK. Though, it is supoer complicated oto find it.

Finding the right learning rate, eta, is also important. Also, learning rates should not be the same for every dimensioin, or in the determination  of the weights. Therefore, adaptation is also important.

Gradient descent, loosely speaking is falling to the local minimum. Momentum may be added in attempts to find a better optimum. This is at a cost of speed of convergence.

It accelerates the gradient descent algorithm by considering the exponentially weighted average of the gradients.

Stochastic gradient descent with momentum, empirically, works very well. Recall that the normal relationship in weight optmization is 

w^{n} = w^{n-1} - eta*g^{n}, where g^{n} = delta_{w}l(w)

Introducing momentum turns the equation to

$ $w^{n} = w^{n-1} - eta(Ag^{n} + (1-A)g^{n-1}) $$

The factor of eta is the weighted average of the current and previous delta

# 2.2 Other variants of Gradient Descent

We'll start by learning about adaptive learning rates. We want eta to get smaller and smaller as we approach a local minima. Another important consideratoin is that non-linear surfaces dont' look the same in different dimensions. Therefore, we need differnt learning rates for each dimensions.

AdaGrad: 
   
   




