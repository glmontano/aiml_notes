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

There is a very high chance to be caught in a local-minima. However, for many cases we do not need to find ther global minima. There is evidence that this may be overfit, and therefore it is OK. Though, it is super complicated to find it.

## AdaGrad

Finding the right learning rate, eta, is also important. Also, learning rates should not be the same for every dimensioin, or in the determination  of the weights. Therefore, adaptation is also important.

Gradient descent, loosely speaking is falling to the local minimum. Momentum may be added in attempts to find a better optimum. This is at a cost of speed of convergence.

It accelerates the gradient descent algorithm by considering the exponentially weighted average of the gradients.

Stochastic gradient descent with momentum, empirically, works very well. Recall that the normal relationship in weight optmization is 

$w^{n} = w^{n-1} - \eta*g^{n}, where g^{n} = delta_{w}l(w)$

Introducing momentum turns the equation to

$w^{n} = w^{n-1} - \eta(Ag^{n} + (1-A)g^{n-1})$

The factor of eta is the weighted average of the current and previous delta

# 2.2 Other variants of Gradient Descent

We'll start by learning about adaptive learning rates. We want $\eta$ to get smaller and smaller as we approach a local minima, and conversely - larger when further away from it. Another important consideration is that non-linear surfaces don't look the same in different dimensions. Therefore, we need different learning rates for each dimension.

Adaptive learning rates is key.

## AdaGrad

AdaGrad that includes a learning rate that adapts in every iteration is given by

$$w^{n} = w^{n-1} - \frac{\eta}{\sqrt{s} + \varepsilon}g^{n},$$

where $$s = \Sigma_{n}\left(g^{n}\right)^{2}.$$

The $\varepsilon$ is added to protect the denominator from being zero. Note that as the number of iterations increase, or as the change in gradients increases, $s$ becomes large and therefore the $\eta$ is divided by a larger another, and the coefficient of $g^{n}$ becomes smaller. This represents the adapative nature of the AdaGrad.

Another thing to note is that $\eta$ is specific to the dimension being optimized ($w$). There will be a different $eta$ for each dimension, as previously stated.

AdaGrad works well for stochastic gradient descent on convex surfaces. However, should it be applied on complex non-convex surfaces, then AdaGrad's performance decreases. Furthermore, there is the risk that with many iterations the learning rate apporaches zero, and no further learning is initiated. At the worst case - no local minima is reached.

## RMSProp

RMSProp is another method, and superior to AdaGrad in complex non-convex surfaces. It acknowledges that the adaptive nature of the earning rate is too aggresive. That is, it solves the vanishing gradient problem. Instead of working with sum of squares - it uses the exponetnially decaying running average, or the weighted average of gradients in the denominator. Formulating this

$$w^{n} = w^{n-1} - \eta\frac{\eta}{\sqrt{s^{n}} + \varepsilon}g^{n},$$

where $$s^{n} = ps^{n-1}+(1-p)(g^{n})^{2}.$$

$p$ isthe moving average parameter, and default value of `0.9` may be used. This means that 90% of divider will some from the recent $s^{n-1}$, and 10% from $(g^{n})^{2}$.

The last $s$ has the highest weight, and the weights on the gradients decreases with the number of iterations. If the expectation is that the gradients decreases with iterations, then the previous gradients have a higher weight then the prompt, weighted those smaller gradients less.

## Adam

Adam stans for Adaptive Moment Estimation. It considers two main characteristics. First the RMSProp, and specifically the decaying nature of $s$ that affects the learning rate. Second, it works with momentum to reduce the risk of landing on a local minimum.

In summary `Adam = (RMSProp) + (SGD with Momentum)`. This is considered the most useful deep learning technique, and has been around since 2014. This is infused in the equation via

$$w^{n} = w^{n-1} - \eta\frac{\eta}{\sqrt{s^{n}} + \varepsilon}\left(\gamma g^{n} + (1-\gamma)g^{n-1}\right),$$

where $$s^{n} = ps^{n-1}+(1-p)(g^{n})^{2}.$$ The scaler in the numerator, if you will, has a momentum factor, and the momentum parameter in $\gamma$.

## Caveat of Adam

All these methods are called ad-hoc tecniques, as there is no theorem surrounding their performance, only empirical evidence.

While Adam is incredibly fast, it has been observed that it will find worse local minima compared to SGD with momentum. while this has been considered, the benefits of speed outweights the mentioned costs.

# 2.3 Weight initialization and its Techniques

The weight optimization process is the automatic process of changing weights to lower the loss function. However, there requires a starting point or the weight initialisation.

Initially, weight initialisation was not thought to be important until further work unveiled that focus on such a matter leads to different rates of convergences and the local minima achieved.

Examples to demonstrate the importance are extremes on the Activation Function. Consider the Sigmoid Function, that _tails_ off at the end, and a inflexion point at 0. Should all weights be initialized at zreo, or a larger number, then the rate of change on these functions will be very small, and so will the learning. Conversly, picking a number closer to the inflexion point will lead to more suitable learning. Said differently, the optimization algorithm requires some asymmetry in the error gradient to begin the optimization effectively.

The type of initialization to use will depend on the Activaiton Function

## Xavier Initialization (XI)

Xavier Initialization is used for non-linear Actionvation Functions such as the Sigmoid or Tanh. XI states that

$$w_{i, j} \sim U\left(-\frac{1}{\sqrt{n}}, -\frac{1}{\sqrt{n}}\right),$$

where $n$ is the number of nodes in the previous layer. Looking at the distribution - it aims to not initialize from very small or larger numbers. 

While this works OK, it has undergone variations such as

$$w_{i, j} \sim N\left(0, \frac{1}{n}\right).$$

## He Initialziation (HI)

Consider a ReLu Activation Function that is not symmetric, and gives learning to where the domain is greater than zero. With some mathematical proof aiming to (i)  Keeping the variance betwee layers constant, the behavior of the ReLu funciton in $max(0, x)$, the distribution of the weights is given by

$$w_{i, j} \sim N\left(0, \frac{2}{n}\right).$$


# 2.4 Regularization

Recall that in terms of the content within data, it can be said that

$$\text{Data}:= \text{Information} + \text{noise}.$$

Models that are two simple will comtain little to no noise, and little information, and underperform in predictions. Complicated models will do well in capturing information, but will also capture too much noise, thereby performing poorly against a test dataset. In this case - the model overfits the data and this may also lead to predictions in noise, and not just the information itself.

The right model is one that is between too simple and too complex. It captures the right amount of information, with little to no noise.

This relationship from simple to complex can be explained by the number of parameters in that model. Simple models will have a small number of parameters (think of a linear equation), whereas a complicated model will have a large number of paramters (think of a multi-degree polynomial). The degrees of freedom allows parameters to move around, thereby allowing for the capturing of information, but also noise.

Coming back to Neural Networks - the number of paramters is large due to the number of layers and the number of nodes in each layer. As such, Neural Networks are prone to being classified as a complicated model, and overfitting the data. As such, methods to reduce the complexity to an adequate level is required.

Regularization is the method of reducing the complexity of the model after a first round of optimzation has occurred. It is sometimes called Shrinkage. 

## L1 or L2 Regularization

L1 and L2 Regularization techniques can be used for all machine and deep learning techniques.

L1 is called Larso Regularization, and L2 - Ridge Regularization.

The technique works by appending to optimization of the Loss function, a penalty term. Speaking loosely the minimization expression is now

$$\min_{w} L\left(y,\hat{y}\right) + \text{Penalty Term}.$$

If L1 then

$$\text{Penality Term} = \frac{\lambda}{2m}\sum|w_{i}|.$$

If L2 then

$$\text{Penality Term} = \frac{\lambda}{2m}\sum(w_{i})^{2}.$$

Lasso will result in some weights being zero and therefore dropping them. Ridge will not lead to zero weights, though, it will make them extremely small, having a similar effect of dropping weights.

Lasso is better in terms of explainability in linear regressions. Ridge is better for complicated networks for predictability.

## Data Augmentation

Data Augmentation is another method for regularization. It relies on using prior knowledge, or the existing data set, and appends the data with variations of it. These variations are large enough to introduce noise, but does not change the class label or value. This effectivey reduces the generalization error.

With respect to the MNIST data set of images - Data Augmentation can involve the following variants

  - Adding noise to the image
  - Rotation
  - Cropping
  - Shifts
  - Mirroring
  - Color adjustments
  - Generative Adverserial Network - to create new images

# 2.5 Dropout

Dropout is another regularization technique. It works by training multiple subsets of nodes in a layer. Let the probability of a node being in a subset be 50%. With this, multiple subsets of a layer are selected, and trained independently of other subsets. As an analogy, this has the effect of focusing training on nodes of the subsets, rather than the entire layer or 'class/team' of players.

Dropout is the term used as some nodes are dropped out during the mini-batch training process.

Once training is complete - the testing stage must consider all results of the dropbox regularization, or all mini-batches. This is done in two ways

  1. Scaling the weights by the probability of retention described above.
  2. Scaling the optimized weights at the stage of training, before testing is done as an aggregation. This is called Inverse Dropout.

Empirically, the probability of retention for hidden layers is best served by 50%. For the input layer, it should be close to 100%, such as 80%.

# 2.6 Batch Normalization

Batch Normaliation is another regularization technique used in Deep Learning. The motivation is to treat the changing variance of incoming results to each node due to different mini-batches or epochs in the weight-optimization process. For example, consider the input data that goes through various hidden layers with processed weight and an activation function. At various stages - the distribution of values will change, introducing noise and presenting difficulties in learning or convergence. This effect is known as **Internal Covariate Shift**, defined as: The change in the distribution of network activations due to the change in network parameters during training.

Batch Normalization works by restributing the values to have a mean of 0 and variance of 1. This is similar to the scaling that occurs at the beginning, where the inputs have the same statistics.

There are two instances in which this can happen.

  1. Post-Activation Normaliation: Normalize the output from the last layer
  2. Pre-Activation Normalization: Normalize the input from the last layer.

Typically, BN is performed on the output from a hidden layer (Post-Activation).

One final note is that since the output must be in terms of the value to be predicted - BN is not applied at this stage.

# 2.7 Types of Neural Networks

We've learnt about various neural networks and there characteristics. This includes

- Feed Forward NN: The ones we've seen
-   - Multi-layer perceptrons
    - Convulational NN
- Recurrent NN
-   Long-short term memory NN

- Deep Learning Networks: A NN with many layers.

A Feed-Forward Neural Network flows the inputs and outputs forward, with no instance of data feeding back to a previous layer. If there is a single hidden layer - then the NN is called a single-layer perceptron, if there are multiple layers then it is a multi-layers peceptrons, and if there are a large number of layers then it is a deep learning network.

## Convolutional Neural Networks
A Convolutional Neural Networks are popular in image recognition. At a high leve it works by mapping subset of an image to a neuron, though, another overlapping subset will be mapped to another neuron. The effective overlapping of the neurons, or the convolution of mappings and neurons maintains the spacial information of an image. This all happens on a single layer. This is also a feed-forward neural network.

The next layer will go through a similar convolutional layer, before entering a final normal neurol network.

This stucture maintains feautures in the best fashion possible.

## Recurrent Neural Network

These networks are used for time-series, where previous knowledge is important for future predictions. In this case - the input into a node is equal to the weight-linear combination of the previous inputs, with the weight-linear combination of the current inputs.

Using infomration from the past is known as a Recurrent Neural Network. Furthermore, this networkl is considered to have short-term memory.

## Long-Short Term Memory Networks

In this case, a node is replaced with a complicated structure to one that has memory in it. The neuron will learn how much memory to keep, which is determined in a weighted fashion.

## Generalized Adversarial Network

Two networks convolutional netowkr sowkring with eachother. One netowrk's role is to create, the second is to check it (discriminator).
