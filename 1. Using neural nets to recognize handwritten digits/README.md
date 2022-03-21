# Using neural nets to recognize handwritten digits

## Perceptrons
![picture](http://neuralnetworksanddeeplearning.com/images/tikz0.png)

Suppose $x$ is the input value; $w$ is the learning weight; $b$ is the bias, which is equal to $-threshold$.The core equation of Perceptron algorithm is:

$$
output=\begin{cases}
 0 & \text{ if } w\cdot x+b\le 0 \\
 1 & \text{ if } w\cdot x+b>0
\end{cases}
$$

If you are familar with logistic regression, it turns out that the output is activated by the step function rather than sigmoid function. Therefore, naturally we can find that sigmoid function is acutally the smooth version of step function.

The decision boundary of whether Perceptron or Logistic Regression is ![](https://latex.codecogs.com/svg.latex?w\cdot&space;x&plus;b=0).