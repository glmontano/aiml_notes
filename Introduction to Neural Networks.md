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
