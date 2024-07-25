## 1. Problem

Predict whether traffic in Ethernet scan data is increasing or decreasing using a neural network.

## 2. Solution

Use two consecutive data samples as input for the neural network. The network will predict the probability of these samples belonging to an increasing or decreasing trend (binary classification).

## 3. Neural Network Architecture

The neural network is composed of three layers:

* **Input Layer:** 10 nodes
* **Hidden Layer:** 5 nodes
* **Output Layer:** 1 node

### a. Pipeline for 1 Training Step with 1 Data-Label Pair

1. **Get Data and Create Label**
   * Take two consecutive samples from the training dataset or real-time data.
   * Compare the `avgTrafficRate` in the subsequent sample with the preceding sample.
     * If greater, assign label 1 (going up)
     * If not greater, assign label 0 (going down)

2. **Pre-processing**
   * Concatenate the 2 data samples into an array of length 10 for input.

3. **Forward**
   * For each input data, the model calculates the output `p` based on the current weights, biases, and activation functions:
                        H=ReLU(Input∗W0+b0)
                        p=Sigmoid(H∗W1+b1)
   * p always falls within the range of 0 to 1, representing the model's prediction. The closer 𝑝 is to 0, the more likely the model is predicting a label of 0; the closer 𝑝 is to 1, the more likely the model is predicting a label of 1.
   * Activation Functions
     * **ReLU:** `f(x) = max(0, x)`
     * **Sigmoid:** `f(x) = 1 / (1 + e^(-x))`

4. **Loss Function**
   * Loss functions measure the difference between the network's prediction `p` and the actual target (label) `y`. The smaller the loss, the closer the model's prediction is to the target.
   * * **Loss Function:** Binary Cross Entropy (BCE)
   * **BCE Loss:** `-(y * log(p) + (1 - y) * log(1 - p))`
    * Example: `p = 0.335`, `y = 0` => `loss = 0.117`
    * Example: `p = 0.100`, `y = 0` => `loss = 0.046`
    * Example: `p = 0.335`, `y = 1` => `loss = 0.475`
5. **Backward Propagation (Training)**
   * The goal of training is to minimize the loss as much as possible, which is achieved through calculating the gradient and updating the weights.
   * **Gradient**: The goal of training is to minimize the loss as much as possible, which is achieved through calculating the gradient and updating the weights.
       * **Output Layer**: Calculate the gradient of the loss with respect to the output    layer's weights.
       * **Hidden Layers**:  Propagate the gradient backward through the network, layer by layer, computing the gradient of the loss with respect to each layer's weights.
   * **Weight Update**: Update the weights using an optimization algorithm, gradient descent, where weights are adjusted in the opposite direction of the gradient of the loss function with 

